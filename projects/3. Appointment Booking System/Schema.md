A. Provider
```
// backend/models/Provider.js (NOT "User"!)
const providerSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  timezone: { type: String, default: 'America/New_York' },
  serviceDuration: { type: Number, default: 30 }, // Minutes per appointment
  bufferTime: { type: Number, default: 15 }, // Minutes between bookings
  businessName: { type: String, default: '' }, // Optional: "John's Dental Clinic"
  createdAt: { type: Date, default: Date.now }
});

module.exports = mongoose.model('Provider', providerSchema);
```

B. Availability

```
const mongoose = require('mongoose');

const daySchema = new mongoose.Schema({
  isWorking: { type: Boolean, default: true },
  start: { type: String, default: '09:00' }, // "HH:MM" format
  end: { type: String, default: '17:00' }
}, { _id: false });

const availabilitySchema = new mongoose.Schema({
  user: { 
    type: mongoose.Schema.Types.ObjectId, 
    ref: 'User', 
    required: true, 
    unique: true // One availability document per user
  },
  weeklySchedule: {
    monday: { type: daySchema, default: () => ({}) },
    tuesday: { type: daySchema, default: () => ({}) },
    wednesday: { type: daySchema, default: () => ({}) },
    thursday: { type: daySchema, default: () => ({}) },
    friday: { type: daySchema, default: () => ({}) },
    saturday: { type: daySchema, default: () => ({ isWorking: false }) },
    sunday: { type: daySchema, default: () => ({ isWorking: false }) }
  },
  customUnavailableDates: [{
    date: { type: Date, required: true },
    reason: { type: String, default: 'Unavailable' }
  }],
  updatedAt: { type: Date, default: Date.now }
});

module.exports = mongoose.model('Availability', availabilitySchema);

```


C. Appointment

```
const mongoose = require('mongoose');

const appointmentSchema = new mongoose.Schema({
  provider: { 
    type: mongoose.Schema.Types.ObjectId, 
    ref: 'User', 
    required: true,
    index: true 
  },
  clientName: { type: String, required: true },
  clientEmail: { type: String, required: true },
  clientPhone: { type: String, default: '' },
  notes: { type: String, default: '' },
  startTime: { type: Date, required: true },
  endTime: { type: Date, required: true },
  status: { 
    type: String, 
    enum: ['upcoming', 'completed', 'cancelled', 'no-show'], 
    default: 'upcoming',
    index: true 
  },
  cancellationReason: { type: String, default: '' },
  createdAt: { type: Date, default: Date.now }
});

// **** CRITICAL: PREVENT DOUBLE-BOOKING RACE CONDITION ****
// This ensures no two appointments can have the same provider + startTime
appointmentSchema.index({ provider: 1, startTime: 1 }, { unique: true });

module.exports = mongoose.model('Appointment', appointmentSchema);

```

3. The Core Logic  Slot generator Service
Here backend generates the available slots

A. Public Booking (No Auth Required)

```
const express = require('express');
const router = express.Router();
const Appointment = require('../models/Appointment');
const User = require('../models/User');
const generateAvailableSlots = require('../services/slotGenerator');

// GET available slots for a specific date
router.get('/slots', async (req, res) => {
  try {
    const { providerId, date } = req.query;
    if (!providerId || !date) {
      return res.status(400).json({ error: 'providerId and date are required' });
    }

    // Get provider details
    const provider = await User.findById(providerId);
    if (!provider) {
      return res.status(404).json({ error: 'Provider not found' });
    }

    const slots = await generateAvailableSlots(
      providerId,
      date,
      provider.timezone,
      provider.serviceDuration,
      provider.bufferTime
    );

    res.json({ slots });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: 'Failed to generate slots' });
  }
});

// POST create a new booking
router.post('/book', async (req, res) => {
  try {
    const { providerId, clientName, clientEmail, clientPhone, notes, startTime } = req.body;

    // Validate input
    if (!providerId || !clientName || !clientEmail || !startTime) {
      return res.status(400).json({ error: 'Missing required fields' });
    }

    // Fetch provider to get service duration
    const provider = await User.findById(providerId);
    if (!provider) {
      return res.status(404).json({ error: 'Provider not found' });
    }

    // Calculate end time
    const startDate = new Date(startTime);
    const endDate = new Date(startDate.getTime() + provider.serviceDuration * 60000);

    // Create appointment
    const appointment = new Appointment({
      provider: providerId,
      clientName,
      clientEmail,
      clientPhone: clientPhone || '',
      notes: notes || '',
      startTime: startDate,
      endTime: endDate,
      status: 'upcoming'
    });

    // **** THE RACE CONDITION GUARD ****
    // The unique index on { provider: 1, startTime: 1 } will throw an error
    // if another booking already exists at this exact time
    await appointment.save();

    // TODO: Send confirmation email with .ics attachment (see section 6)
    // sendConfirmationEmail(appointment, provider);

    res.status(201).json({ 
      message: 'Appointment booked successfully!',
      appointment 
    });

  } catch (error) {
    // Check if it's a duplicate key error (E11000)
    if (error.code === 11000) {
      return res.status(409).json({ 
        error: 'This time slot was just taken by someone else. Please choose another time.' 
      });
    }
    console.error(error);
    res.status(500).json({ error: 'Failed to book appointment' });
  }
});

module.exports = router;

```


B. Provider Appointment (Auth Required-Protected)

```
const express = require('express');
const router = express.Router();
const Appointment = require('../models/Appointment');
const auth = require('../middleware/auth'); // Your JWT middleware

// GET all appointments for the logged-in provider
router.get('/', auth, async (req, res) => {
  try {
    const { status, startDate, endDate } = req.query;
    const filter = { provider: req.user._id };

    if (status) filter.status = status;
    if (startDate || endDate) {
      filter.startTime = {};
      if (startDate) filter.startTime.$gte = new Date(startDate);
      if (endDate) filter.startTime.$lte = new Date(endDate);
    }

    const appointments = await Appointment.find(filter)
      .sort({ startTime: 1 })
      .limit(100); // Prevent massive queries

    res.json(appointments);
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: 'Failed to fetch appointments' });
  }
});

// PATCH cancel an appointment
router.patch('/:id/cancel', auth, async (req, res) => {
  try {
    const { reason } = req.body;
    const appointment = await Appointment.findOne({
      _id: req.params.id,
      provider: req.user._id // Ensure the provider owns this booking
    });

    if (!appointment) {
      return res.status(404).json({ error: 'Appointment not found' });
    }

    if (appointment.status === 'completed') {
      return res.status(400).json({ error: 'Cannot cancel a completed appointment' });
    }

    appointment.status = 'cancelled';
    appointment.cancellationReason = reason || 'Cancelled by provider';
    await appointment.save();

    // TODO: Send cancellation email to client

    res.json({ message: 'Appointment cancelled successfully', appointment });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: 'Failed to cancel appointment' });
  }
});

// PUT update appointment status (mark as completed/no-show)
router.patch('/:id/status', auth, async (req, res) => {
  try {
    const { status } = req.body;
    if (!['completed', 'no-show'].includes(status)) {
      return res.status(400).json({ error: 'Invalid status' });
    }

    const appointment = await Appointment.findOneAndUpdate(
      { _id: req.params.id, provider: req.user._id },
      { status },
      { new: true }
    );

    if (!appointment) {
      return res.status(404).json({ error: 'Appointment not found' });
    }

    res.json(appointment);
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: 'Failed to update status' });
  }
});

module.exports = router;

```

5. Setting up availability (provider settings page)

```
const express = require('express');
const router = express.Router();
const Availability = require('../models/Availability');
const auth = require('../middleware/auth');

// GET provider's availability settings
router.get('/', auth, async (req, res) => {
  try {
    let availability = await Availability.findOne({ user: req.user._id });
    if (!availability) {
      // Create default availability if it doesn't exist
      availability = new Availability({ user: req.user._id });
      await availability.save();
    }
    res.json(availability);
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: 'Failed to fetch availability' });
  }
});

// PUT update availability settings
router.put('/', auth, async (req, res) => {
  try {
    const { weeklySchedule, customUnavailableDates } = req.body;
    
    const availability = await Availability.findOneAndUpdate(
      { user: req.user._id },
      { 
        weeklySchedule, 
        customUnavailableDates,
        updatedAt: new Date()
      },
      { new: true, upsert: true } // Create if doesn't exist
    );

    res.json(availability);
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: 'Failed to update availability' });
  }
});

module.exports = router;

```


6) Sending Email
after booking successfull email is sent

7) background job: Auth-send reminders 

8) Frontend
 - public booking page
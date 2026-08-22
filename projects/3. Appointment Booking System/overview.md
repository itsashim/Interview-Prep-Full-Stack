# System Architecture Overview

1) Provider sets their weekly working hours and holidays.
2) Client visits the public booking page → selects a date → frontend asks backend: "Give me all available slots for this date".
3) Backend calculates available slots by checking:
- Is it a working day?
- Is it a holiday?
- Are there any existing bookings at that time?
4) Client selects a slot, fills in their details, and submits.
5) Backend attempts to save the booking. If another booking snuck in at the exact same millisecond, MongoDB throws a duplicate error → backend catches it and tells the frontend "Slot taken!"
6) Confirmation email is sent with an .ics calendar file.



my summary
So the we fetch all the provider settings for his profile, 
see in what days he is available, and he then choose the start time and end time of his working hours and selects the buffer time and meeting duration, 
and our system generate the slots automatically and for the custom appointments, he then creates his own custom slot if any other slot is affected the other slot will be deleted and get dismissed ,
in frontend user is unauthenticated user browse the provider sees the available slots goes to book one and enters all the detail after booking is completed email is sent and after that we set a reminder cron job for both provider and client is my concept clear
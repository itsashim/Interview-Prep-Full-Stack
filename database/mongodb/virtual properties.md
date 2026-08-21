# Virtual Properties
document attributes that you can get and set but that do not get persisted to the MongoDB database
[1]. Instead, they are computed dynamically on the application side using an Object Data Modeling (ODM) library like Mongoose [1].

# Key Characteristics
No Database Storage: They do not occupy space in your MongoDB collections [1].
Computed Values: They are typically used to combine existing document fields [1].
Getter/Setter Support: They can read data (getters) or split data to update other fields (setters) [1].

# Common Use CasesCombining fields: 
Merging names, addresses, or formatting dates [1].
Calculated metrics: Computing a total price from a price and tax field.
Virtual Populate: Creating relationships between collections without storing manual arrays of ObjectIds.


# code examples

```
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String
});

// Define the virtual property
userSchema.virtual('fullName').get(function() {
  return `${this.firstName} ${this.lastName}`;
});

const User = mongoose.model('User', userSchema);

// Usage
const user = new User({ firstName: 'John', lastName: 'Doe' });
console.log(user.fullName); // Outputs: John Doe
```

```
const mongoose = require('mongoose');

// 1. The Schema (with both objects)
const userSchema = new mongoose.Schema(
  {
    // First object: Fields stored in the database
    firstName: String,
    lastName: String
  }, 
  {
    // Second object: Settings to make virtuals visible
    toJSON: { virtuals: true }
  }
);

// 2. The Virtual Property
userSchema.virtual('fullName').get(function() {
  return `${this.firstName} ${this.lastName}`;
});

// 3. The Model
const User = mongoose.model('User', userSchema);

// --- Test Output ---
const user = new User({ firstName: 'John', lastName: 'Doe' });
console.log(user.toJSON());
/* 
Outputs:
{
  firstName: 'John',
  lastName: 'Doe',
  fullName: 'John Doe'  <-- Visible due to the second object setting
}
*/

```
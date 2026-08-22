# Data validation with mongoose

## Validation
validation is checking if the values are in right format for each field in schema and also to check if that value have been entered for all of the required fields

Mongoose validation is the process of checking whether the data meets certain rules before it is saved to the MongoDB. 

Validation is defined in the Mongoose Schema and runs before the document is saved. 

## Sanitization
Ensures the inputted data is clean so no malicious code will be injected into our database or application. in this step we remove unwanted characters or even code from the input data. 

Never accept the input data from the user as it is we have to sanitize that user input data.



### 1. Basic Validation

```
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },
  age: {
    type: Number,
    min: 18,
    max: 100
  },
  email: {
    type: String,
    required: true,
    unique: true
  }
});

const User = mongoose.model("User", userSchema);

```
required: true → field must be provided.
min → minimum value for numbers.
max → maximum value for numbers.
unique: true → creates a unique index; it is not itself a Mongoose validator.


### 2. String Validation
Mongoose provides several useful string validations

```
const userSchema = new mongoose.Schema({
  username: {
    type: String,
    required: true,
    minlength: 3,
    maxlength: 20,
    trim: true
  }
});

```

| Validator | Purpose |
| :--- | :--- |
| `required` | Value must exist |
| `minlength` | Minimum string length |
| `maxlength` | Maximum string length |
| `match` | Must match a regular expression |
| `enum` | Value must be one of specified values |
| `trim` | Removes leading/trailing whitespace |

Example:

```
const userSchema = new mongoose.Schema({
  gender: {
    type: String,
    enum: ["male", "female", "other"]
  }
});

```


### 3. Number Validation

```
const productSchema = new mongoose.Schema({
  price: {
    type: Number,
    required: true,
    min: 0
  },
  stock: {
    type: Number,
    min: 0,
    max: 10000
  }
});

```

### 4. Custom Validation

```
const userSchema = new mongoose.Schema({
  age: {
    type: Number,
    validate: {
      validator: function(value) {
        return value >= 18;
      },
      message: "Age must be at least 18"
    }
  }
});
//
//
const userSchema = new mongoose.Schema({
  username: {
    type: String,
    validate: {
      validator: value => value.length >= 5,
      message: "Username must contain at least 5 characters"
    }
  }
});

```


### 5. Validation Error Handling

If validation fails when calling save(), Mongoose rejects the operation with a ValidationError.

```
const user = new User({
  name: "",
  age: 15
});

try {
  await user.save();
} catch (error) {
  console.log(error);
}


// you can inspect individual validation errors
catch (error) {
  for (const field in error.errors) {
    console.log(error.errors[field].message);
  }
}
```

### 6. Validation During Updates
By default mongoose validator don't run on `Update` operations. Use runValidators: true

```
await User.findOneAndUpdate(
  { _id: userId },
  { age: 10 },
  { runValidators: true }
);

```

This is important when using methods such as 
updateOne()
updateMany()
findOneAndUpdate()


## Mongoose validation happens primarily at the application/schema level before data is persisted, while MongoDB itself provides separate database-level features such as schema validation and indexes.

A common Mongoose Schema looks like:

```
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, "Name is required"],
    minlength: [3, "Name must be at least 3 characters"],
    maxlength: [50, "Name cannot exceed 50 characters"],
    trim: true
  },

  email: {
    type: String,
    required: [true, "Email is required"],
    match: [/^\S+@\S+\.\S+$/, "Invalid email address"]
  },

  age: {
    type: Number,
    required: true,
    min: [18, "Age must be at least 18"]
  }
});


```

@ Mongoose validation lets you enforce rules such as required fields, type restrictions, length limits, ranges, allowed values, regular expressions, and custom business rules before saving data.\



# More on Custom Validation

```
validate: {
    validator: function(val){
        console.log(this); This points to current document when we are creating  new document in mongodb, doesn't work for update , that's why don't rely only on `this` keyword
        console.log(val); // this is the value input of user
    }, 
    message: "Must be greater than actual price, your value {VALUE}" // we can access the value in message as well 
}

```

@ There are many libraries for data validation that we can use.
for example: we have a validation library called validator

```
import validator from "validator";

const userSchema = new mongoose.Schema({
  age: {
    type: Number,
    validate: [validator.isISBN, "Book ISBM not found"]
  }
});

// This way we can take advantage of all the validation out there
```
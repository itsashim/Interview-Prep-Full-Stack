# This Keyword

**this** is a special keyword in js that points to the object from where the function is being called.

**this** refers to the object that is currently calling the function.

**this** is a special JavaScript keyword whose value is determined by how a function is called. For regular functions, the call site determines this; arrow functions inherit this from their surrounding scope.

```
class Student{
    name: "Ashim",
    sayName: () => {
        console.log(this.name); // Ashim
    }
 }

 const s1 = new Student();
 s1.sayName();
 // Ashim
```


with object

```

const student  = {
    name: "Ashim",
    sayName() {
        console.log(this.name);
    }
}

student.sayName();


:- will not work with arrow function , Arrow functions do not have their own this.
Instead, the arrow function takes this from its surrounding scope.
```


Normal function: this depends on who calls the function.

Arrow function: this comes from the surrounding scope.


# cheatseat
# Object method
obj.method();
➡️ this is generally obj.

# Constructor with new
new Person();
➡️ this is the newly created object.

# Arrow function
➡️ Arrow functions don't create their own this. They inherit it from the surrounding lexical scope.

# Plain function call
➡️ In strict mode, this is undefined.
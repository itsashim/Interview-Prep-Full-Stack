# Constructor Function

A constructor function is a function that is used to create multiple objects using same structure and properties.
It's a blueprint and `new` creates objects from that blueprint.

```
function SayName(name){
    this.name = name;
}
```

const person1 = new SayName("Ashim");

console.log(person1.name); // Ashim

# Constructor method

A constructor is a special method inside a class that is automatically called when an object is created with new keyword 

```
class Person {
 constructor(name){
    this.name = name;
 }
}

const person1 = new Person("Ashim");
console.log(person1.name); // Ashim
```


# How New keyword works
Creates a new empty object.
Makes this refer to that object.
Runs the constructor function.
Returns the new object.
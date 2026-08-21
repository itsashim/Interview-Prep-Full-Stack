# Mongoose middleware / Pre Post Hooks

Four types of middleware in mongoose, as we have next() function in nodejs to call next middleware in the stack , we have next function to Mongoose as well, 
we can have middleware running before and after a certain event.

1) Document
2) Query
3) Aggregate
4) Model: Not included now


we define the middleware in the schema just like the virtual properties

1) Document Middleware
.pre() runs before and after saving data to the database

```
// Document middleware runs only on .save() commands and the .create() 
//command the middleware will be executed
dataSchema.pre('save', function(next){
    console.log(this); // this keyword will point to the currently processed document 
    next(); // will call next middleware in the stack
});

dataSchema.post('save', function(doc, next){
    console.log(doc); // access of finished doc
    next();
})

```

2) Query middleware
It runs before  and after any find query is executed.
the 'this' keyword will now point to the query not to the document because of 'find' hook 
because we are processing query

```
// excutes right before the query execution
dataSchema.pre('find', function(next){
    next();
})


// executes after the query has been executed
dataSchema.post('find', function(docs,next){
    console.log(docs); // it can have the access to the docs after the qurey is executed
    next();
})

```


3) Aggregation Middleware
It runs before and after any aggregation happens

```

// runs before aggregationis executed
dataSchema.pre('aggregate', function(next){
    this.pipeline().unshift({$match: {$secretTour: { $ne: true}}});
    console.log(this); // points to current aggregation object
    console.log(this.pipeline()); // points to current aggregation object pipeline
    next();
})

// it also has post middleware

```

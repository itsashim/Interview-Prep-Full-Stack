############# Mongoose ###############

Mongoose is an Object Document Mapper (ODM). It sits between Express app and MongoDB and gives you:
 - Schema
        - defines what a document should have, their types, defaults, requiredness. (this is what enforces the structure since raw MongoDB doesn't)
 - Models
        - a compiler version of Schema you used to query the DB
 - Validations

 It gives lot's more functionality out of the box , it allows for rapid and simple development of MongoDB database
 interactions
 it gives features such as:
 - schema to model data and relationships
 - easy data validation
 - simple query API
 - middleware etc


 # Schema
 - It where we model our data, where we describe the model of the data, default values and validations, 
 and create a model out of it, Model is a wrapper around schema which provides  interface to the database for CRUD operations. 


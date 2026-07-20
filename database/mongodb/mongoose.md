############# Mongoose ###############

Mongoose is an Object Document Mapper (ODM). It sits between Express app and MongoDB and gives you:
 - Schema
        - defines what a document should have, their types, defaults, requiredness. (this is what enforces the structure since raw MongoDB doesn't)
 - Models
        - a compiler version of Schema you used to query the DB
 - Validations

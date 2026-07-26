
# API
Application programing interface: a piece of software that can be used by another piece of software, 
inorder to allow applicatiosn to talk to each other.

# REST API
Representational States Transfer, 
Restful API means api that follows REST architecture

- Seperate API into logical resources
- Expose structured resource-based URLs
- Use HTTP methods (verbs)
- Send data as JSON
- Be stateless



# CRUD
GET /tours
GET /tours/:id

(used to create new resouce)
POST /tours

DELETE /tours/:id

used to update existing resouce
PUT /tours/:id (client is supposed to send entire updated object)
PATCH /tours/:id (client is supposed to send only the part of the object that has been changed)


# JSON
Json is very light data interchange format used by any programming language.
widely used because its readable. It's very typtical for the value to be string

## Jsend, JSON:API, Odata json protocol are the formatting standards

## Enveloping
wraping the data into additional object is enveloping  


# Stateless RESTFUL API
All the state is handle on the client. This means that each request must contain all the information
necessary to process a certain request.
basically make the api where server doesn't have to remeber any state from the client, and everything is handled from the client side.

example state: 
logged IN, current Page



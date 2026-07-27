
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


# URL , path parameters, query parameter

base_url: https://google.com
params: https://google.com/:param/:optionalParam?
query params: https://google.com/:param?location=biratnagar


# URL / Path Parameters (params)
Path parameters are used to locate a specific resource in a hierarchical system.
The web application cannot pinpoint the exact item you want without this data.
How it looks: https://example.com
How backend defines it: /products/:category
Key Use Case: 
Fetching an exact item by its unique ID, slug, or category name.

#  Query Parameters / Query Strings (query)
 Query parameters extend the URL to let you send additional, optional commands to the server.
 They consist of key-value pairs separated by an equals sign (=), with multiple pairs chained together using an ampersand (&).
 
 How it looks: https://example.comHow 
 backend defines it: /products (the route matching logic ignores everything after the ?).
 Key Use Cases:
 Searching: ?q=running+shoes
 Pagination: ?page=3&limit=20
 Filtering: ?size=10&color=red
 Tracking: ?utm_source=newsletter
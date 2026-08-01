# Enviroment
There can be different types of environment it is basically used to set up and config db, and other important project configuration and keys

# Environment variables
it is like global variables


# NODE_ENV=development nodemon server.js 
this will change the env variable , so we can put this in the scripts of package.json like this

"scripts": {
    "start:prod": "NODE_ENV=production nodemon server.js"
}
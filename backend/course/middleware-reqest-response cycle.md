# Middleware: 
function that is executed between Requests and response, 
all the middeware in our app is Middleware stack, a middleware that appears that first in the code is executed at first that the middle that appears later.
the order of the code matters a lot in express.
every middle has next() function when called we move to another middleware in the middleware stack.

like this we finish res and req cycle 


# Creating Middleware in express


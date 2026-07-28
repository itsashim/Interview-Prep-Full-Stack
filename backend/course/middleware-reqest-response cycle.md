# Middleware: 
function that is executed between Requests and response, 
each middle function we have access to req , res and next() 
all the middeware in our app is Middleware stack, a middleware that appears that first in the code is executed at first that the middle that appears later.
the order of the code matters a lot in express.
every middle has next() function when called we move to another middleware in the middleware stack.

like this we finish res and req cycle 


# Creating Middleware in express

// but the code placement must be on the top because the order is very important in express
`app.use((req,res,next)=> {
    console.log("excecutes in all of the req or res");
    req.ownVariable = "ashim"; // this variable can be further used in another middleware as every // middleware has the access of req and res
    next(); // calls another middleware in the stack
})`



`app.use("/api/v1/tours", tourRouter)

const tourRouter = express.Router();

tourRouter.route("/").get(getAllTours);

`

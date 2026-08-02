# Node js runs on V8 engine and libuv 
- V8 engine converts js code to machine code
- libuv provides event loop, thread pool to node js

To understand the node architecture , first we have to understand 
- Node process : It is instance of program in execution on a computer
- Thread : In the node process , Node js runs a single thread, Thread is basically a sequence of instructions, we can imagine that thread is a box in our computer system where our code is executed in processor

!Node runs in a single thread so we have to be very careful not to block that thread

# What happens in single thread

1) Initialize code: When we start the node js all the top level code is executed i.e all the code that is not inside any callbacks
2) All the top level code are executed
3) all the modules are required
4) all the callback are registered
5) and Event loop starts running: Some task are too heavy that will block the single thread, this is where thread pool comes

# Thread pool
It is provided by libuv which give us four new threads that are completely seperate from the single thread , we can configure upto 128 threads. So these threads together form thread pool , 
Event loop automatically offloads heavy task to thread pool.

increase or changed the threads

process.env.UV_THREADPOOL_SIZE = 4;

# offloading
heavy tasks like: 
-file system api
-cryptography
-compression
-DNS lookup
can block the single thread in node js Event loop. so in order to prevent blocking event loop automatically offloads tasks like this in thread pool, that process is offloading.


# All about Event Loop

- It excecutes code that's inside callback function (non-top-level-code)
- Node js is Event-driven architecture
    - Events are emitted
    - Event loop picks them up
    - callbacks are called
It is called observer pattern, where instead of calling a function the we observe if any events are emmited to handle them,
 
node js has event emitter objects -> we developer handle those events by event listener -> and we attach a callback function

# The things that emit events
- new http request
- timer expired
- finished file reading

=> Event loop does the orcestration, receives events, call their callback function , offload expensive task to the thread pool

# What is Inside the Event loop
When we start node js,  event loop is started

Now we have to understand that event loop has many phases each phase has their own callback queue, 

1st phase [Callback queue]
2nd phase [Callback queue]
3rd phase [Callback queue]
4th phase [Callback queue]

1) 1st phase: callback of expired timers are processed in this phase, these are the first one to be processed by the event loop.

2) 2nd phase: I/0 polliing , stuffs like newworking and file access, 99% of our code will execute here

3) 3rd phase: Set immediate callbacks: special kind of timer if we want to process callbacks immediately

4) 4th phase: close callbacks: closed events like webserver shutdown or websocket shutdown.


Callback in each queue are processed one by one until there are no one left in queue and only then the event loop will enter the next phase.

here , after the first phase callback queue is finished, event loop enters the second phase and so on...
but for example if the timer expires at another phase besides first phase then the callback of that timer will have to wait for the entire event loop to complete and when event loop re-enters the first phase then the callback of that timer will be processed, that means event loop travels sequentially

1st -> 2nd -> 3rd -> 4th 
doesn't move back if any process if left or a callback is fired



Special phases
6) Pricess.NEXTTICK()
7) Other microtask

These are special phases because in this phase the promises are processed and these queue executes right after the current phase of callback queue is empty that means it doesn't wait for entire event loop to get finished.

After event loop finishes the first tick or first cycle it checks if any pending timers or I/O taks if no exit program if yes runs the event loop again.


Event loop takes care of all incoming events and performs ochestraction by
offloading heavier tasks into the thread pool and doing the most simple work itself.
Event loop makes asynchronous programming possible in nodejs. 

Node js is single threaded , that means hundred , thousand,  millions of user will access same thread at a same time this makes node lightweight and scalable.

where as other language like php it creates new thread for each users
that makes that languages resource intensive



# Don't block the thread
- Don't use synce versions of functions in fs, crupto and zlib modules in your callback funtions
- don't perform complex calculations
- be careful with JSON in large objects
- Don't use too complext regular expressions



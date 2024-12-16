### Call Stack
one thread == one call stack == one thing at a time

call stack is a data structure which records where in the program we are

if we go into a function , we put something on to the stack and if we return from a function, we pop off from the stack.

## blocking, what happens when things are slow

Things that are slow but are in stack: like doing while loop from 1 to 10 billion, image processing, network requests, etc. 

we have to wait till the blocking tasks are completed to execute other tasks on the queue

it is because we are running the code in the browser

the simplest solution is using asynchronous callbacks

concurrency and the event loop: one thing at a time, except not really. 
JS runtime can only do one thing at a time, it can't an AJAX request or setTimeout while doing other code. 
 The reason we can do things concurrently is that the browser is more than just the runtime. it gives web APIs which are threads that we can make calls to and those pieces of the browser are aware of the concurrency.

for nodejs, there is C++ APIs instead of web APIs. the threading process is hidden. 

setTimeout is an API provided by the browser, it doesn't live in the JS runtime V8 source.

console.log('hi')
setTimeout (function cb(){
consoel.log("in the time out")
}, 5000);
console.log('Learn some thing')

first the main function is executed,
then immeditely hi is displayed

the setTimeOut function is executed in webapi, the browser is going to handle that. so it goes to webapi stack from the main stack get gets executed there until it is completed. in the meantime, learn some thing is displayed because it gets executed since the setTimeOut is not in the call stack.

 the web api cant modify the code or put stuff onto the stack when it's ready. if it did it would appear randomly in the middle of the code. It is managed by task queue or callback queue. the setTimeOut function once it gets executed, it is sent to this task queue.
## Event Loop

It's main job is to look at the stack and look at the task queue. If the stack is empty, it takes the first thing on the queue and pushes it on to the stack which effectively runs it. 
in the above setTimeOut case, after the stack is empty, it is will be sent to main stack and then only" in the time out" is displayed in the console. 

 **Don't Block the Event loop**: It means that that don't put slow & shitty codes in the stack. 
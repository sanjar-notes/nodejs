# 62. Worker Threads module
Created Sunday 12 February 2023 at 02:38 am

## Why
- A lighter alternative to cluster module.
- The cluster module runs multiple instances of Node.js (the runtime). The worker threads module, on the other hand, runs multiple threads within a single Node.js instance.

## How
- When process isolation is not needed (i.e. no need for separate instances of V8, event loop and memory), use worker threads.
- In short, worker threads are less resource heavy, but don't offer isolation.

Doing the same thing again, as with cluster module. A normal endpoint and a slow endpoint. Note their individual load times. Next, run slow page first quickly run normal page. It can be seen that the normal page also takes a long time, i.e. it's blocked.

Worked thread is yet another solution to this "CPU intensive" problem, but it's tight and less resource heavy as compared to using the cluster module. It has less isolation though, compared to the cluster module.


## What (syntax)
Keywords - `Worker` constructor, `parentPort`, `.on('message')`.

```js
// in main-thread.js
const { Worker } = require("node:worker_threads");

const worker = new Worker("./worker-thread.js");

worker.on('message', (msg) => {
	console.log(msg);
})
```

```js
// in worker-thread.js
import { parentPort } = require("node:worker_threads");

const msg = slowRunningCode;
parentPort.postMessage(msg);
```
- There are other events too, like `exit`, `error`
- An un-handled error in a worker will stop the parent too. Handle error either inside the worker or using the `'error'` event in the parent.
- **Derived**: A worker doesn't have to post a message. It can run just as a side effect.
- **Derived**: Async ops (promises, nextTicks, timeouts, timeintervals) from the main and worker threads all run in the same event loop - since all worker threads run on a single Node.js instance (i.e. they share the V8 instance, event loop and memory).

#### Notes (doubts): 
1. The "worker_threads" module talks about threads alone, it doesn't care on which (or how many) cores they run.
2. Also there's no constraint that one Node.js process use a single core (just like any other process - it can use as many threads and cores it wants). There are two doubt scenarios here: 
	1. If not using "worker_threads": using multiple cores and threads is possible. Parallelism also possible (except with JS code). <details><summary> Explanation</summary>It definitely doesn't even if one does not use "worker_threads", since OS level file IO and networking code (except the callback) will run on threads other than the main thread anyway. The only limitation here is that there'll only be one *JS thread*</details>
	2. Using "worker_threads" - same as \#1, except that the limitation of single JS thread is removed.
3. The cluster module is even easier to understand, since it has whole instances of Node.js running.
4. There's no guarantee that a worker will be run in parallel. It'll happen only if a thread, and more importantly a CPU core, is available.


#### How many workers to run
If the goal is true parallelism, the maximum number of workers is same as number of CPU cores on the machines. Number of threads don't matter (they are generally > number of cores) here. Number of CPU cores:
```js
const os = require("node:os");
console.log(os.cpus().length);
```

- However, if the app also interacts with the file system, does networking in an async way (which is usually the case), it is better to have some CPU cores left for these things (i.e. Node.js internal code that's not JS).
- Leave a core for the OS, as it's managing important processes other than the Node.js app - maybe Docker, cron jobs, firewalls, etc.


## How does this solve the issue
The server starts - it's running on the main thread (single thread and single core - say t1 on c1). The first request (slow) is received, the main thread spins up a worker thread. Now since the main-thread is busy listening for requests, the worker-thread actually runs on a different core (say t2 on c2). The second request (fast endpoint arrives), it's received by the main-thread, which is free, and is handled (by t1 on c1). That's it.

Experiment 3: Had there been another call for slow, yet another thread would have spun up (and handled by yet another core  t3 on c3). Let's test this - run /slow, /slow and /fast. Expectation, all take the same time, as if called individually when the server is free. I'm assuming all other processes, including OS are running on a single CPU core. **Confirmed, works!**. 
[Server code](https://github.com/exemplar-codes/codevolution-nodejs/commit/0e24dbbf749bb0f291029293be205603f1e477fd), client side code:
```js
async function fast() {
	fetch('http://localhost:8000').then(_ => _.json()).then(console.log);
}

async function slow() {
	fetch('http://localhost:8000/slow').then(_ => _.json()).then(console.log);
}

// experimenting machine has 8 CPUs
[slow(), fast()]             // OK
[slow(), slow(), fast()]     // OK
[slow() /*6 times*/, fast()] // 6 cores for slow, 1 for OS, 1 for the main thread (fast)
[slow() /*7 times*/, fast()] // 7 cores for slow. 1 for main thread competing with OS.
```
# Node.js Internals – Theory

## 1. Node.js Architecture

Node.js follows a **single-threaded, event-driven, non-blocking architecture** designed to handle large numbers of concurrent connections efficiently.

### Key Components of Node.js Architecture
- JavaScript Engine (V8)
- Node.js Core APIs
- Native Bindings
- Event Loop
- libuv
- Thread Pool

Node.js executes JavaScript on a single main thread but uses background threads for heavy or blocking operations.

---

## 2. JavaScript Engine (V8)

- V8 is an open-source JavaScript engine developed by Google.
- It converts JavaScript code directly into **machine code** using Just-In-Time (JIT) compilation.
- V8 handles:
  - Memory allocation
  - Garbage collection
  - Execution of JavaScript code
- Node.js uses V8 to execute JavaScript outside the browser.

---

## 3. Node.js Core APIs

- Core APIs are built-in modules provided by Node.js.
- Examples:
  - `fs` – file system operations
  - `http` – creating web servers
  - `path` – file path handling
  - `os` – operating system details
- These APIs allow developers to interact with the system without writing low-level code.

---

## 4. Native Bindings

- Native bindings act as a bridge between JavaScript and C/C++ code.
- They connect:
  - JavaScript Core APIs
  - Low-level system functions implemented in C/C++
- Native bindings help Node.js access system-level features efficiently.

---

## 5. Event Loop

- The event loop is the core mechanism that enables non-blocking behavior.
- It continuously checks:
  - Callback queues
  - Microtask queues
- It executes callbacks when the main call stack is empty.
- Even though Node.js is single-threaded, the event loop makes it scalable.

---

## 6. libuv

### What is libuv?
- libuv is a C library used by Node.js.
- It provides asynchronous I/O capabilities.
- It works across different operating systems.

### Why Node.js Needs libuv
- JavaScript alone cannot handle low-level system operations.
- libuv abstracts OS-specific features like:
  - File system access
  - Networking
  - Timers

### Responsibilities of libuv
- Event loop implementation
- Thread pool management
- Asynchronous file and network operations
- Handling timers and system events

---

## 7. Thread Pool

### What is a Thread Pool?
- A thread pool is a group of background threads.
- Used to execute tasks that are blocking or CPU-intensive.

### Why Node.js Uses a Thread Pool
- To prevent blocking the main event loop
- To maintain high performance and responsiveness

### Operations Handled by the Thread Pool
- File system operations (`fs`)
- DNS lookups
- Compression
- Cryptographic operations

---

## 8. Worker Threads

### What are Worker Threads?
- Worker threads allow running JavaScript in multiple threads.
- Each worker has its own event loop and memory.

### Why are Worker Threads Needed?
- For CPU-intensive tasks
- To improve performance for heavy computations
- To avoid blocking the main thread

### Difference Between Thread Pool and Worker Threads

| Thread Pool | Worker Threads |
|------------|----------------|
| Managed by libuv | Managed by developer |
| Used internally | Explicitly created |
| Runs native code | Runs JavaScript code |
| Limited control | Full control |

---

## 9. Event Loop Queues

### Macro Task Queue
- Contains tasks scheduled for later execution.
- Examples:
  - `setTimeout`
  - `setInterval`
  - I/O callbacks
  - `setImmediate`

### Micro Task Queue
- Contains high-priority tasks.
- Examples:
  - `Promise.then()`
  - `process.nextTick()`

### Execution Priority
- Microtask queue is executed **before** the macrotask queue.
- After each macrotask, all microtasks are processed.

---

## 10. Summary

- Node.js uses a single-threaded model with background workers.
- libuv enables non-blocking I/O.
- Thread pool handles blocking system tasks.
- Worker threads handle CPU-heavy JavaScript code.
- Event loop coordinates task execution efficiently.

---

## GitHub Submission

📌 **GitHub Repository Link:**  
(Add your GitHub repo link here)

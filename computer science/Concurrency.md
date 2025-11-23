### Multiplexing

Multiplexing threads is a technique where many lightweight logical threads share a smaller number of actual
operating-system threads, switching between tasks without creating a huge number of OS-level threads.

1. Lower overhead
   Creating and scheduling OS threads is expensive; lightweight threads are cheaper.
2. More control
   Your application decides when to pause or resume tasks.
3. Better scalability
   You can handle thousands or millions of concurrent tasks efficiently.

- Event-loop models: Node.js, Deno
- Green/virtual threads: Go goroutines, Java Loom virtual threads
- Async runtimes: Rust Tokio, Python asyncio

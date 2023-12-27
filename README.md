### Concurrency and Parallelism

Concurrency is a programming property (overlapped execution) that can occur even for a single-core machine, whereas parallelism is a property of execution hardware (simultaneous execution).

### Evolving Java support for concurrency

- Initially, Java had locks (via **synchronized** classes and methods), Runnables and Threads. 
- In 2004, Java 5 introduced the java.util.concurrent package, which supported more expressive concurrency, particularly the **ExecutorService** interface. ExecutorServices can execute both Runnables and Callables.
- Java 7 added java.util.concurrent.RecursiveTask to support **fork/join** implementation.
- Java 8 added support for Streams and their parallel processing. It also added the **CompletableFuture** implementation of Future.

```java
sum = Arrays.stream(numbers).parallel().sum();
```
The parallel Stream iteration abstracts a given use pattern of threads.

- Java 9 provided explicit support for distributed asynchronous programming via the publish-subscribe protocol, specified by the java.util.concurrent.Flow interface.  

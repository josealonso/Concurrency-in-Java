### Concurrency and Parallelism

Concurrency is a programming property (overlapped execution) that can occur even for a single-core machine, whereas parallelism is a property of execution hardware (simultaneous execution).

### Evolving Java support for concurrency

- Initially, Java had locks (via **synchronized** classes and methods), Runnables and Threads. 
- In 2004, Java 5 introduced the java.util.concurrent package, which supported more expressive concurrency, particularly the **ExecutorService** interface. ExecutorServices can execute both Runnables and Callables.
- Java 7 added java.util.concurrent.RecursiveTask to support **fork/join** implementation.
- Java 8 added support for Streams and their parallel processing. It also added the **CompletableFuture** implementation of Future.

```java
int sum = Arrays.stream(numbers).parallel().sum();
```
The parallel Stream iteration abstracts a given use pattern of threads.

- Java 9 provided explicit support for distributed asynchronous programming via the publish-subscribe protocol, specified by the java.util.concurrent.**Flow** interface. 

### Executors and thread pools

- Java threads access operating-system threads directly. The problem is that operating-system threads are expensive to create and to destroy (involving interaction with page tables), and moreover, only a limited number exist.- The Executor framework allows Java programmers to decouple task submission from task execution.

```java
// Factory method used to create a pool of threads
ExecutorService newFixedThreadPool(int nThreads);
```

It is common to have a long-running ExecutorService that manages an always-running Internet service.  

### Synchronous or blocking APIs

```java
int y = f(x);
int z = g(x);
System.out.println(y + z);
```

1.- Using threads:

```java
class ThreadExample {
  public static void main(String[] args) throws InterruptedException {
    Result result = new Result();

    Thread t1 = new Thread(() -> { result.left = f(x); } );
    Thread t2 = new Thread(() -> { result.right = g(x); });
    t1.start();
    t2.start();
    t1.join();
    t2.join();
    System.out.println(result.left + result.right);
  }
  private static class Result {
    private int left;
    private int right;
  }
}
```

2.- Using the *Future* API interface instead of *Runnable*:

```java
public class ExecutorServiceExample {
  public static void main(String[] args)
    throws ExecutionException, InterruptedException {
    ExecutorService executorService =    Executors.newFixedThreadPool(2);
    Future<Integer> y = executorService.submit(() -> f(x));
    Future<Integer> z = executorService.submit(() -> g(x));
    System.out.println(y.get() + z.get());

    executorService.shutdown();
  }
}
```

### Changing to an asynchronous API

change the signature of f and g to

```java
Future<Integer> f(int x);
Future<Integer> g(int x);
```

and change the calls to

```java
Future<Integer> y = f(x);
Future<Integer> z = g(x);
System.out.println(y.get() + z.get());
```


























 

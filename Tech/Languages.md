# Java
- JIT (Just In Time compiler) enables high performance in Java. JIT converts the bytecode into machine language and then JVM (interpreter) starts the execution.
- Multi-threaded: A flow of execution is known as a Thread. JVM creates a thread which is called the main thread. The user can create multiple threads by extending the thread class or by implementing the `Runnable` interface.

## Memory Management
Java Stack memory is used for the execution of a thread. They contain method-specific values that are short-lived and references to other objects in the heap that is getting referred from the method. Stack memory is always referenced in **LIFO (Last-In-First-Out)** order. Whenever a method is invoked, a new block is created in the stack memory for the method to hold local primitive values and reference to other objects in the method. As soon as the method ends, the block becomes unused and becomes available for the next method. Stack memory size is very little compared to Heap memory.

## Garbage Collection

Garbage collection is built into the JVM by consuming CPU resources. JVM automatically determines what memory is no longer being used by a Java application and recycles this memory for other uses.

## Multithreading

Multithreading is a Java feature that allows concurrent execution of two or more parts of a program for maximum utilization of CPU. Each part of such program is called a thread. So, threads are light-weight processes within a process.

- Each thread has a private JVM stack, created at the same time as thread
- Threads can be created by using two mechanisms :
    1. Extending the Thread class
    2. Implementing the Runnable Interface
# Go

- strong support for concurrent programming with channels and goroutines for efficient and scalable concurrent code

## Channels

A channel is a built-in **concurrency primitive** used for communication and **synchronization** between **goroutines** (concurrently executing functions). Channels provide a way for goroutines to send and receive data to and from each other in a safe and synchronized manner, enabling effective communication and coordination in concurrent Go programs.

Some key points:

1. **Channel Declaration**:
    - declared using the **`chan`** keyword followed by the data type of the values that will be sent and received through the channel.
    - For example, **`ch := make(chan int)`** creates an integer channel named **`ch`**.
2. **Sending and Receiving**:
    - You can send data into a channel using the **`<-`** operator followed by the channel name. For example, **`ch <- 42`** sends the integer **`42`** into the channel **`ch`**.
    - You can receive data from a channel using the **`<-`** operator on the left side of an assignment. For example, **`value := <-ch`** receives a value from the channel **`ch`** and assigns it to the **`value`** variable.
3. **Blocking Operations**:
    - Sending to a channel (**`ch <- value`**) or receiving from a channel (**`value := <-ch`**) will block the execution of the current goroutine until there is a corresponding receive or send operation on the other end of the channel.
    - This blocking behavior makes channels useful for synchronization and coordination between goroutines.
4. **Buffered Channels**:
    - By default, channels are unbuffered, which means they allow one value to be sent or received at a time, and both sender and receiver must be ready.
    - Buffered channels can be created with a specified capacity using **`make(chan T, capacity)`**. They allow a limited number of values to be sent before blocking.
5. **Closing Channels**:
    - Channels can be closed using the **`close`** function: **`close(ch)`**.
    - Closing a channel indicates that no more values will be sent on it. Receivers can use the comma-ok idiom to detect when a channel is closed and no more data is expected.
6. **Select Statement**:
    - The **`select`** statement is used to choose one of several communication operations that are ready to execute. It provides a way to handle multiple channels in a non-blocking manner.
    - It is often used in conjunction with channels for managing multiple goroutines and handling various communication cases.
7. **Channel Direction**:
    - You can specify the direction of a channel in function parameters to restrict whether a function can send or receive on the channel.
    - For example, **`func sendData(ch chan<- int)`** indicates that **`sendData`** can only send data to the channel, while **`func receiveData(ch <-chan int)`** can only receive data from the channel.

## Goroutines vs Threads

||Goroutines|Threads|
|---|---|---|
|Resource Overhead|Minimal resource overhead; designed to be lightweight with the Go runtime being able to manage thousands or even millions of goroutines efficiently.|Relatively heavyweight in terms of resource consumption. Each thread typically requires a significant amount of memory for its stack and other data structures.|
|Concurrency Control|Managed by the Go runtime, which schedules them on a limited number of operating system threads (usually one per CPU core). The scheduler multiplexes goroutines onto OS threads to achieve concurrency.|Managed by the operating system's kernel scheduler. Creating and managing threads can be more expensive in terms of system resources, and the kernel handles their scheduling.|
|Communication and Synchronization|Synchronize using channels, which are built-in data structures designed for safe communication between concurrent processes. Channels make it easier to avoid race conditions and other concurrency issues.|Use lower-level mechanisms such as mutexes and semaphores for communication and synchronization which can be error-prone and more challenging to work with than channels.|
|Parallelism (not to be confused with Concurrency)|Goroutines are suitable for both concurrent and parallel programming. They allow you to write code that efficiently utilizes multiple CPU cores by running goroutines in parallel.|Threads are typically associated with parallelism, but can also be used for concurrent programming. However, managing many threads in a parallel application can be more challenging due to the associated overhead.|
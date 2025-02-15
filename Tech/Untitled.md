# Threads
## Process vs Threads
![](images/Pasted%20image%2020250215140727.png)
Threads execute within a process. Threads are an operating environment feature, rather than a CPU feature (though the CPU typically has operations to make the thread efficient)

- A process is independent and does not contained within another process, whereas all threads are logically contained within a process.
- Processes are heavily weighted, whereas threads are light-weighted.
- A process can exist individually as it contains its own memory and other resources, whereas a thread cannot have its individual existence.
- A proper synchronization between processes is not required. In contrast, threads need to be synchronized in order to avoid unexpected scenarios.
- Processes can communicate with each other using inter-process communication only; in contrast, threads can directly communicate with each other as they share the same address space.

# Memory

### Heap vs Stack

Heap memory is used by all the parts of the application whereas stack memory is used only by one thread of execution. Whenever an object is created, it's always stored in the Heap space and stack memory contains the reference to it.
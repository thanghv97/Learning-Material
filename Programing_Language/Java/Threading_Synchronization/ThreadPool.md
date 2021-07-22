# **Introduction to Thread Pools in Java**
This article is a look at thread pools in Java – starting with the different implementations in the standard Java library and then looking at Google's Guava library.
  + [Introduction](#Introduction)
  + [Thread Pools in Java](#Thread-Pools-in-Java)
    + [Executors, Executor and ExecutorService](#Executors-Executor-and-ExecutorService)
    + [ThreadPoolExecutor](#ThreadPoolExecutor)

## **Introduction**

## **Thread Pools in Java**
### **Executors, Executor and ExecutorService**  

### **ThreadPoolExecutor**
The ThreadPoolExecutor is an extensible thread pool implementation with lots of parameters and hooks for fine-tuning. However, the main configuration parameters that we'll discuss here are: ```corePoolSize```, ```maximumPoolSize```, and ```keepAliveTime```.  

The pool consists of a fixed number of core threads that are kept inside all the time, and some excessive threads that may be spawned and then terminated when they are not needed anymore. The corePoolSize parameter is the number of core threads that will be instantiated and kept in the pool. When a new task comes in, if corePoolSize or more threads are running, the executor always prefers queuing a request rather than adding a new thread. If ok, the pool is allowed to grow up to maximumPoolSize.
    <p align=center>
      <image width="480" height="360" src="_Images/TP_00_ThreadPoolExecutor.png">
    </p>

The ThreadPoolExecutor decides when to start a new thread based on the type of queue used to hold the tasks. There are three possibilities:  

1. **Direct handoffs**

2. **Unbounded Queue**
> 

3. **Bounded Queues** 
> *A bounded queue (for example, an ArrayBlockingQueue) helps prevent resource exhaustion when used with finite maximumPoolSizes, but can be more difficult to tune and control. Queue sizes and maximum pool sizes may be traded off for each other: Using large queues and small pools minimizes CPU usage, OS resources, and context-switching overhead, but can lead to artificially low throughput. If tasks frequently block (for example if they are I/O bound), a system may be able to schedule time for more threads than you otherwise allow. Use of small queues generally requires larger pool sizes, which keeps CPUs busier but may encounter unacceptable scheduling overhead, which also decreases throughput.*
    <p align=center>
      <image width="480" height="480" src="_Images/TP_01_BoundedQueueAlgorithm.png">
    </p>
*For example, say that the pool’s core size is 4, its maximum size is 8, and the maximum size of the ArrayBlockingQueue is 10. As tasks arrive and are placed in the queue, the pool will run a maximum of 4 threads (the core pool size). Even if the queue completely fills up—so that it is holding 10 pending tasks—the executor will only utilize 4 threads.*  
*An additional thread will only be started when the queue is full, and a new task is added to the queue. Instead of rejecting the task (since the queue is full), the executor starts a new thread. That new thread runs the first task on the queue, making room for the pending task to be added to the queue.*  


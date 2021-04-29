# **Threading**
From its first days, some of Java’s appeal has been because it is multithreaded. Even in the days before multicore and multi-CPU systems were the norm, the ability to easily write threaded programs in Java has been considered one of its hallmark features. This post explores how to get the maximum performance out of Java threading and synchronization facilities.
  + [Thread Pools and ThreadPoolExecutors](#Thread-Pools-and-ThreadPoolExecutors)

## **Thread Pools and ThreadPoolExecutors**
  + *Refer [Thread Pools](#) to understand clearly Thread Pools and ThreadPoolExecutors in Java. In this section, we just considered how to improve performance for Thread Pools.* 

The key factor in using a thread pool is that tuning the size of the pool is crucial to getting the best performance. Thread pool performance varies depending on basic choices about thread pool size, and under certain circumstances, an oversized thread pool will be quite detrimental to performance.
  + [Setting the maximum number of threads](#Setting-the-maximum-number-of-threads)  
  + [Setting the minimum number of threads](#)  
  + [Thread pool task sizes](#)  
  + [Sizing a ThreadPoolExecutor](#Sizing-a-ThreadPoolExecutor)  

### **Setting the maximum number of threads**
  So what is the optimal maximum number of threads for a given workload on given hardware? There is no simple answer to this; it depends on characteristics of the workload and the hardware on which it is run. In particular, the optimal number of threads depends on how often each individual task will block.

### **Setting the minimum number of threads**

### **Sizing a ThreadPoolExecutor**
The ThreadPoolExecutor decides when to start a new thread based on the type of queue used to hold the tasks. There are three possibilities:  

```Synchronous Queue```

```Unbounded Queue```

```Bounded Queue```  

*Executors that use a bounded queue employ a quite complicated algorithm to determine when to start a new thread. For example, say that the pool’s core size is 4, its maximum size is 8, and the maximum size of the queue is 10. As tasks arrive and are placed in the queue, the pool will run a maximum of 4 threads (the core pool size). Even if the queue completely fills up—so that it is holding 10 pending tasks—the executor will only utilize 4 threads.*  
*An additional thread will only be started when the queue is full, and a new task is added to the queue. Instead of rejecting the task (since the queue is full), the executor starts a new thread. That new thread runs the first task on the queue, making room for the pending task to be added to the queue.*
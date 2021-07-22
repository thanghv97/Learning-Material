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
  So what is the optimal maximum number of threads for a given workload on given hardware? There is no simple answer to this; it depends on the characteristics of the workload and the hardware on which it is run. In particular, the optimal number of threads depends on how often each individual task will block.

### **Setting the minimum number of threads**

### **Sizing a ThreadPoolExecutor**
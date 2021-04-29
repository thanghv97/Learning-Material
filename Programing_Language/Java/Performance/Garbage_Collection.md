# **Garbage Collection**
  + [Overview](#garbage-collection-overview)
  + [Memory Model](#memory-model)
  + [GC Algorithms](#garbage-collection-algorithms)

## **Garbage Collection Overview**
  <img align="right" width="400" height="170" src="_Images/GC_00_Illustration.png">One of the most attractive features of Java is that developers needn't explicitly the lifecycle of objects: objects are created when needed, and when the object is no longer in use, the JVM automatically frees the objects. In this post, we will try to introduce [what is *garbage collection(GC)*](#What-is-garbage-collection) and [how to improve performance by tuning GC](#How-to-improve-performance-by-tuning-GC)

  ### What is garbage collection?
  At a basic level, GC consists of finding objects that no longer in use and freezing the memory associated with those objects. The JVM will periodically search the heap for **unreachable objects** - *An object is said to be unreachable if it doesn't contain any reference of it, also note that objects which are part of "*island of isolation*" are also unreachable objects*. When it finds unreachable objects, the JVM can free the memory occupied by those objects and use it to allocate additional objects. However, it is usually insufficient simply to keep track of that free memory and use it for future allocations; at some point, memory must be coalesced to prevent memory fragmentation.
    <p align=center>
      <image width="480" height="360" src="_Images/GC_01_Heap_Allocation.png">
    </p>
  The implementations are a little more detailed, but the performance of GC is dominated by these basic operations: 
  + finding unreachable objects
  + making their memory available
  + compacting the heap

  Different collectors take different approaches to these operations, which is why they yield different performance characteristics. There are four main garbage collectors available in a current JVM. These collectors will be introduced in [GC algorithms](#garbage-collection-algorithms).
  
  However, when GC tracks object references or moves objects around in memory, it must make sure that application threads are not using those objects. This is particularly true when GC moves objects around: the memory location of the object changes during that operation, and hence no application threads can be accessing the object. The pauses when all application threads are stopped are called **stop-the-world** pauses. `These pauses generally have the greatest impact on the performance of an application, and minimizing those pauses is the key consideration when tuning GC.`

## **Memory Model**
  + *To understand clearly about GC, refer [Memory Model](#../JVM/Memory_Model.md) of JVM to have a little knowledge about architecture of memory in Java.*

  Though the details differ somewhat, all garbage collectors work by splitting the heap into different generations. These are called the old (or tenured) generation, and the young generation. The young generation is further divided into sections known as eden and the survivor spaces (S0&S1).
  <p align=center>
    <image width="360" height="200" src="_Images/GC_02_Heap_Stack.png">
  </p>

  + Objects are first allocated in the young generation, which is some subset of the entire heap. When the young generation fills up, the garbage collector will stop all the application threads and empty out the young generation. Objects that are no longer in use are discarded, and objects that are still in use are moved elsewhere. This operation is called a **minor GC**.
  + As objects are moved to the old generation, eventually it too will fill up, and the JVM will need to find any objects within the old generation that are no longer in use and discard them. This is where GC algorithms have their biggest differences. The simpler algorithms stop all application threads, find the unused objects and free their memory, and then compact the heap. This process is called a **full GC**, and it generally causes a long pause for the application threads. On the other hand, it is possible—though more computationally complex—to find unused objects while application threads are running like CMS or G1 algorithms.

  In the next content of this post, we will approach the different GC algorithms to solve the above design model and how to choose an algorithm that suits our application.

## **Garbage Collection Algorithms**
  The JVM provides four different algorithms for performing GC:
  + [The serial garbage collector](#The-serial-garbage-collector)
  + [The throughput collector](#The-throughput-collector)
  + [The CMS collector](#The-cms-collector)
  + [The G1 collector](#The-g1-collector)

### The serial garbage collector
#### *description*
  + The serial garbage collector is the simplest of the four. This is the default collector if the application is running on a client-class machine (32-bit JVMs on Windows or single-processor machines).  
  + The serial collector uses a single thread to process the heap. It will stop all application threads as the heap is processed (for either a minor or full GC) During a full GC, it will fully compact the old generation. Hence, it is not a good idea to use it in multi-threaded applications like server environments.  
  + The Serial GC is the garbage collector of choice for most applications that do not have small pause time requirements and run on client-style machines. To enable Serial Garbage Collector, we can use the following argument:
  ```
             java -XX:+UseSerialGC -jar Application.java  
  ```
  > ***Note** that unlike with most JVM flags, the serial collector is not disabled by changing the plus sign to a minus sign (i.e., by specifying -XX:-UseSerialGC). On systems where the serial collector is the default, it is disabled by specifying a different GC algorithm.*


### The throughput collector
#### *description*
  + This is the default collector for server-class machines (multi-CPU Unix machines, and any 64-bit JVM).
  + The throughput collector uses multiple threads to collect the young generation, which makes minor GCs much faster than when the serial collector is used. The throughput collector can use multiple threads to process the old generation as well. That is the default behavior in JDK 7u4 and later releases, and that behavior can be enabled in earlier JDK 7 JVMs by specifying the *-XX:+UseParallelOldGC* flag. Because it uses multiple threads, the throughput collector is often called the parallel collector.
  + The throughput collector stops all application threads during both minor and full GCs, and it fully compacts the old generation during a full GC. To enable it, use the flags:
  ```
            java -XX:+UseParallelGC --XX:+UseParallelOldGC -jar Application.java
  ```
#### *mechanism*
  + The throughput collector has two basic operators: it collects the young generation, and it collects the old generation.
### The CMS collector
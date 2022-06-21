## Java Memory Management

Memory management in Java is the process of allocating working memory space to new objects and properly removing unreferenced objects to create space for those new object allocations. Java has automatic memory deallocation system known as _Garbage Collector_.

Garbage collector automatically deallocate memory of objects which are no longer referenced from application. If programmer writes code which does not unreference objects even after they are not required then this might lead to memory leak.

### Java Memory Structure
Generally, Java memory is divided into two parts: *Stack* and *Heap*.
#### 1. Stack
Stack memory is responsible for holding refenreces to heap objects and storing primitive type values. The stack memory is allocated per thread, therefore each time a thread is created and started, it has its own stack memory and it cannot other thread's stack memory.

#### 2. Heap
Heap memory contains acatual objects which are referenced by variables from stack.
There is single heap memory for each running JVM process regardless of how many threads are running.
The size of heap memory is large as compared to stack memory. The unused objects in heap are automatically collected by Garbage Collector.

Heap memory is divided into 3 parts:
##### **2.1. Young Generation:** 
Newly created are allocated to young generation. New generation is inturn has 3 parts, **Eden**, **Survivor1** and **Survivor2**. All the new objects are created in Eden space. wehn Eden is full, a minor garbage collection happens, and live objects are moved to Survivor1 and then Survivor2.
The Survivor1 and Survivor2 contains objects that survived the minor GC. Objects which survive Eden, Survivor1 and Survivor2 are moved to Old generation.
In Old generation, GC is less frequent so S1 and S2 are used to make sure that only long surviving objects are moved to Old generation.

##### **2.2. Old Generation:** 
Age is set of the objects allocated in Young generation. Age is defined as number of Minor GC object survived. When that age is met, those live objects are moved to the old generation. A **Major GC** runs on the old generation to collect dead objects.

##### **2.3. Permanent Generation:** 
Permanent generation is used by JVM to store metadata about the classes and methods. JVM also stores Java standard libraries in permanent generation. This space is cleaned as a part of **full garbage collection**.

### Memory Errors in Java
#### 1. OutOfMemoryError
OutOfMemoryError is thrown when there is no more space left in the heap to create and store a new object. This happens when GC could not free up any space to store new objects.
Eg. Adding data to list infinitely
```Java
public void addList() {
  String str = "Str";
  List<String> list = new ArrayList<>();
  while(true) {
    list.add(str);
  }
}
```

#### 2. StackOverflowError
Stack memory is fixed and cannot be enlarged or shrunk. Therefore, if we use all the stack memory, there will be no space left for upcoming method calls on stack memory.
Eg. infinite recursive call
```Java
public void recMethod(int n) {
  recMethod(n);
}
```

### Java Garbage Collection

Garbage Collection is the process of collecting memory occupied by unreferenced objects. Garbage Collector is controlled by JVM. Garbage Collection is done whenever JVM detects the low availability of working memory resources. 
JVM also considers programmer's request `(System.gc())`to perform garbage collection but it’s not always guaranteed that JVM will comply with request.

#### Garbage Collection process:
There are 3 steps in Java Garbage Collection:

##### 1. Mark Objects as alive.
In this step, the GC identifies all the live objects in memory by traversing the objects graph in heap memory.
When GC visits an object, it marks it as accessible and thus alive. Every object the garbage collector visits is marked as alive. All the objects which are not reachable from GC Roots are garbage and considered as candidates for garbage collection.

##### 2. Sweep Dead Objects
After marking phase, we have the memory space which is occupied by live (visited) and dead (unvisited) objects. The sweep phase releases the memory fragments which contain these dead objects.

##### 3. Compact remaining Objects in memory
Memory can be compacted after the garbage collector deletes the dead objects, so that the remaining objects are in a contiguous block at the start of the heap.
The compaction process makes it easier to allocate memory to new objects sequentially.

<u>Example:</u>
When an object is created, it is first put into the **Eden space** of the **Young Generation**. Once a minor GC happens, the live objects from **Eden** are promoted to the **Survivor1**. When the next minor garbage collection happens, the live objects from both **Eden** and **Survivor1** are moved to the **Survivor2**.

This cycle continues for a specific number of times. If the object is still used after this point, the next garbage collection cycle will move it to the **old generation** space.

### Types of Garbage Collector:
##### 1. Serial GC
GC happens serially. All garbage collection events are conducted serially in one thread. Compaction is executed after each garbage collection.
When it runs, it leads to a "stop the world" event where the entire application is paused.

<u>Pros:</u> Fast promotion and minor GC, Smallest Footprint

<u>Cons:</u> Single thread

<u>Usecases</u>: limited memory embedded systems

<u>Usage parameter:</u> `-XX:+UseSerialGC`

##### 3. Parallel GC
Multiple threads are used for minor garbage collection in the Young Generation. A single thread is used for major garbage collection in the Old Generation.
Running the Parallel GC also causes a "stop the world event" and the application freezes while both minor and major GC.

<u>Pros:</u>  Fast promotion and minor GC, Higher throughput

<u>Cons:</u> worst case latency (due to compaction)

<u>Usecases</u>: Batch applications

 <u>Usage parameter:</u>`-XX:+UseParallelGC`
 
##### 4. Parallel Old GC
 It is same as Parallel GC except that it uses multiple threads for both Young Generation and Old Generation.

 <u>Pros:</u> 

<u>Cons:</u>

<u>Usecases</u>: 

 <u>Usage parameter:</u>`-XX:+UseParallelOldGC`
 
##### 5. Concurrent Mark and Sweep
Major garbage collection is multi-threaded, like Parallel Old GC, but CMS runs concurrently alongside application processes to minimize “stop the world” events.

<u>Pros:</u>  Low "stop the world" pauses, low worst case latency

<u>Cons:</u> Slow promotion, Reduced throughput, Higher footprint

<u>Usecases</u>: General applications

<u>Usage parameter:</u>`-XX:+UseConcMarkSweepGC`

##### 6. G1 GC
it does not have separate regions for young and old generations. Instead, each generation is a set of regions, which allows resizing of the young generation in a flexible way.
It partitions the heap into a set of equal size regions (1MB to 32MB – depending on the size of the heap) and uses multiple threads to scan them. A region might be either an old region or a young region at any time during the program run.

<u>Pros:</u>  -   Incremental collection, Lower worst-case latency, Relatively faster promotion(no free list), More throughput (no compaction)

<u>Cons:</u> Higher footprint

<u>Usecases</u>: predictable latency apps, Large heaps

<u>Usage parameter:</u>`-XX:+UseG1GC`

##### 7. Shenandoah
Shenandoah is a new GC that was released as part of JDK 12. Shenandoah’s key advantage over G1 is that it does more of its garbage collection cycle work concurrently with the application threads. G1 can evacuate its heap regions only when the application is paused, while Shenandoah can relocate objects concurrently with the application.

<u>Pros:</u>  Lower average latency, Not generational, Concurrent compaction

<u>Cons:</u> -   Higher footprint

<u>Usecases</u>: -   Lower latency than G1

<u>Usage parameter:</u>`-XX:+UnlockExperimentalVMOptions -XX:+UseShenandoahGC`.

### Default garbage collectors:
-   Java 7 - Parallel GC
-   Java 8 - Parallel GC
-   Java 9 - G1 GC
-   Java 10 - G1 GC

References:
- [Garbage collection basics 1](https://www.youtube.com/watch?v=EeRFOVMf7rE)
- [Garbage collection basics 2](https://www.youtube.com/watch?v=bu12JCTeWOo)
- [Garbage collectors comparisons](https://www.youtube.com/watch?v=2AZ0KKeXJSo)

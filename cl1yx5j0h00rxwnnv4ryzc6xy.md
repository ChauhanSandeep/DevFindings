## Thread Pools in Java

### Rules for thread pool creation
Here are Sun's rules for thread creation in simple terms:

1. If the number of threads is less than the `corePoolSize`, create a new Thread to run a new task.
2. If the number of threads is equal (or greater than) the `corePoolSize`, put the task into the queue.
3. If thread count exceeds `queueCapacity`, and the number of threads is less than the `maxPoolSize`, create a new thread to run tasks in.
4. If the queue is full, and the number of threads is greater than or equal to `maxPoolSize`, reject the task.

### Example
#### Question:
How threads will be created with below configuration:
<li>Starting thread pool size is 1</li>
<li>Core pool size is 5 </li>
<li>Max pool size is 10 </li>
<li>Queue is 100.</li>

#### Answer:
<li>As requests come in threads will be created up to 5</li>
<li>Then tasks will be added to the queue until it reaches 100. </li>
<li>When the queue is full new threads will be created up to maxPoolSize(10). </li>
<li>Once all the threads are in use and the queue is full tasks will be rejected. As the queue reduces so does the number of active threads.</li>

### Snippet
```
{
    executor.setCorePoolSize(100);
    executor.setQueueCapacity(10000);
    executor.setMaxPoolSize(250);
    executor.setThreadNamePrefix("asyncThreadPool-");
    executor.initialize();
    return executor;
}
```

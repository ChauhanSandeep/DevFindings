---
title: "Heap dump analysis using Eclipse Memory Analyzer"
datePublished: Sat Apr 16 2022 13:25:38 GMT+0000 (Coordinated Universal Time)
cuid: cl1nls7mw01dn9onv2xphgfo1
slug: heap-dump-analysis-using-eclipse-memory-analyzer
cover: https://cdn.hashnode.com/res/hashnode/image/unsplash/6EnTPvPPL6I/upload/v1649314549697/J2xiSWpy4.jpeg
tags: java

---

When your Java application runs out of memory or behaves unexpectedly, understanding what’s consuming the heap is crucial. This is where Eclipse Memory Analyzer Tool (MAT) shines as an essential part of your troubleshooting toolkit. In this post, I’ll walk you through setting up MAT, capturing heap dumps, and interpreting the core views that help you identify memory issues effectively.

## Setting up MAT

First things first, MAT requires Java 11 or higher. If you’re on a Mac, you can install a compatible JDK using Homebrew with the following command:

```bash
brew install adoptopenjdk
```

After installation, ensure your terminal uses this Java version by updating your PATH environment variable:

```bash
export PATH=“/usr/local/opt/openjdk@11/bin:$PATH”' >> ~/.zshrc && source ~/.zshrc
```

Once your Java environment is ready, download the MAT installer (dmg) for Mac from the [official website](https://www.eclipse.org/downloads/download.php?file=/mat/1.12.0/rcp/MemoryAnalyzer-1.12.0.20210602-macosx.cocoa.x86_64.dmg) and complete the installation.

## Capturing Heap Dump

A heap dump captures the snapshot of your JVM’s memory at a specific point in time, allowing you to analyze what objects are present and how memory is allocated.

To take a heap dump manually, you can use the jmap tool. Running this command will perform a full garbage collection (GC) first, cleaning up unreferenced objects, then capture the heap:

```bash
jmap -dump:live,file=<File path>hdump.hprof <processId>
```

This would do a full GC first and then take heap dump. If you don't want to do GC before taking heap dump then use

```plaintext
jmap file=<File path>hdump.hprof <processId>
```

For automated analysis, you can configure the JVM to generate a heap dump whenever an OutOfMemoryError occurs by adding these JVM options:

```plaintext
-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=<File path>hdump.hprof
```

After capturing the dump, open MAT and import the .hprof file to begin your analysis. You should be able to see the overview of heap dump

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651420376514/RxY4adwvk.png align="left")

## **Understanding Heap Concepts**

Before diving into MAT’s views, it’s important to understand two key memory terms:

* **Shallow Heap:** The memory consumed by a single object itself.
    
* **Retained Heap:** The total memory that would be freed if an object and all the objects it exclusively references were removed.
    

Think of shallow heap as the size of one cup of coffee, while retained heap is the entire coffee-making setup dedicated to that cup, including beans, machine, and filters.

## Exploring MAT Views

MAT provides several views to help you pinpoint memory issues:

### 1\. Dominator Tree

This shows the largest objects dominating the heap and the objects referenced by them — removing one would free up a whole tree of objects. It shows shallow heap, retained heap, and their percentage of total memory.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651424083831/XufMVuqHf.png align="left")

*Right click on the object &gt; List Object &gt; With incoming references*. This will show all the objects which reference current object.

*Right click on the object &gt; List Object &gt; With outgoing references*. This will show all the objects which current object refers to.

### 2\. Histogram

The histogram gives a count of instances per class along with their shallow and retained heap sizes. It helps identify classes that might be leaking or over-allocating memory.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651424027378/IPokvTt-h.png align="left")

### 3\. Top Consumer

This view groups the most expensive objects by class and package, making it easier to spot problematic areas quickly.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651423819813/hc5OAF9vT.png align="left")

### 4\. Duplicate classes

Sometimes, classes get loaded multiple times by different class loaders, leading to subtle memory leaks. MAT highlights these duplicates so you can investigate.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651423923245/JkZlhy4w3.png align="left")

## Conclusion

Heap dump analysis using MAT provides a powerful lens into your JVM’s memory usage, helping uncover memory leaks and inefficiencies. By understanding shallow and retained heap and leveraging MAT’s views, you gain actionable insights into your application’s behavior under the hood.

References:

1. [MAT setup suggestions](https://blog.ycrash.io/2021/03/08/eclipse-mat-tidbits/)
    
2. [Analyze heap dump](https://reflectoring.io/create-analyze-heapdump/)
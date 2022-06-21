## Heap dump analysis using Eclipse Memory Analyzer

## Setup

#### 1. Install MAT
To use MAT we need to have Java version at least greater than 11 at the time of writing.
We can install the latest java easily using the below homebrew command and set it to default java version using below commands

```
brew install adoptopenjdk
export PATH=“/usr/local/opt/openjdk@11/bin:$PATH”' >> ~/.zshrc && source ~/.zshrc
```
Download MAT dmg for mac using this
[link](https://www.eclipse.org/downloads/download.php?file=/mat/1.12.0/rcp/MemoryAnalyzer-1.12.0.20210602-macosx.cocoa.x86_64.dmg)

#### 2. Take Heap Dump
Take heap dump locally using jmap.
```
jmap -dump:live,file=<File path>hdump.hprof <processId>
```
This would do a full GC first and then take heap dump. If you don't want to do GC before taking heap dump then use
```
jmap file=<File path>hdump.hprof <processId>
```

Add below arguments in environment variables to automatically take heap dump when the application goes out of memory.
```
-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=<File path>hdump.hprof
```

Open MAT and import the heap dump (with .hprof extension). You should be able to see the overview of heap dump

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651420376514/RxY4adwvk.png align="left")

## MAT Basics
### 1. Shallow vs Retained Heap
#### 1. Shallow Heap
Shallow heap is the memory consumed by one object.

#### 2. Retained Heap
Retained heap of an object is the sum of shallow sizes of all the objects which will be unreferenced if the current object is removed.

## MAT Views
### 1. Dominator Tree
List the biggest objects and objects referenced by them. This also shows the Shallow heap, retained heap and percentage of total memory consumed by these objects.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651424083831/XufMVuqHf.png align="left")

_Right click on the object > List Object > With incoming references_. This will show all the objects which reference current object.

_Right click on the object > List Object > With outgoing references_. This will show all the objects which current object refers to.

### 2. Histogram
Histogram lists the number of instances per class, shallow and retained heap size

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651424027378/IPokvTt-h.png align="left")

### 3. Top Consumer
Shows the most expensive objects grouped by class and by package

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651423819813/hc5OAF9vT.png align="left")

### 4. Duplicate classes
Detect classes loaded by multiple class loader.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651423923245/JkZlhy4w3.png align="left")

## Conclusion
In this post, we covered the basics of MAT and heap dump analysis. We also covered basic views provided in MAT.
In the next post we will go through the memory issue we faced in production and the thought process of solving it.

We would also cover Open Object Query to directly run SQL-like query on Java heap.

References:

1. [MAT setup suggestions](https://blog.ycrash.io/2021/03/08/eclipse-mat-tidbits/)
2. [Analyze heap dump](https://reflectoring.io/create-analyze-heapdump/)

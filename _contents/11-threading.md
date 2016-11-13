---
title: Threading
---

# Threading
In Java, there are two ways of implementing threads:
* Implement Runnable interface, and pass class into a Thread constructor
** Better if needing to subclass another class, since it is an interface
** Better if don't need the full Thread class overhead
* Extend Thread class and call subclass constructor directly.

#### Process vs Thread
**Process**: instance of a program in execution

**Thread**: exists within a process, can access data from the process and its siblings

### Synchronization and Locks
Threads within the same process share memory space. This is good, because threads
can share data, but also can cause memory to be changed by two threads at the same
time.

#### Synchronized keyword
**synchronized** restricts access to shared resources. Can be applied to methods
or code blocks, and restricts threads from executing the code simultaneously

* Methods: prevents threads from executing the code simultaneously on the *same*
object. For static methods, locks are used on the class (since the static method
could act on static fields).
* Code Blocks: same as a method(``` synchronized(this) { // code }```)

#### Lock keyword
A lock is used to synchronize access to a resource by associating the resource
with the lock. Threads must first gain the lock, then can manipulate the resource.

#### Deadlocks
A deadlock is where two threads are holding a lock while waiting on a second lock,
which the other thread is holding.

All conditions must be met before a deadlock can occur:
1. Mutual exclusion: Only one process can access a resource at a time.
2. Hold and wait: Processes holding a resource can request another resource
without releasing current resources.
3. No preemption: A process cannot force another process to remove its lock.
4. Circular wait: Two or more processes form a circular chain where each process
is waiting on another resource in the chain.

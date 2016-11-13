---
title: Java language details
---
# Java

### Final keyword
**final** has a different meaning depending on what it is applied to:
* Variable: Cannot be changed once initialized
* Method: Cannot be overridden by subclass
* Class: Cannot be subclassed

### Finally keyword
**finally** is used in try/catch blocks and guarantee a section of code will execute
regardless of whether an exception is thrown or not. Will be executed *after* try
and catch statements, but before control is returned to the calling function.

This means that a return statement will still cause a **finally** block to be executed.

TODO: What happens if there is a return statement in a finally block?

### Finalize method
The garbage collector calls the finalize method of an object just before actually
destroying the object.

### Overloading
Methods in Java can be overloaded, which means that the same method name exists
but with different parameters (either number, argument classes, or both).

### Overriding
Methods in Java can be overridden by subclasses, if the method has the same name
and signature as a method in its parent class.

### Garbage Collection
JVM uses a heap to create objects, and is usually allocated in advance by the OS.

Java keeps track of root objects including:
* Local Variables in the main thread
* All threads
* Static variables (unless their classes are garbage collected)

Java performs garbage collection by occasionally running through all roots and
marking all reachable objects as *In Use*. All other objects are marked as
*Free* and can be reused for future allocations.

**Note that this means no explicit deletion, and no memory returned to the OS.**

### Method Parameters
Method parameters are passed by value, not reference. However, for Objects,
the value is a pointer to that Object, so changing object fields can work,
but reassigning the Object is impossible.

## Introduction to Thread Dumps
Thread Dump is a text which represents runtime state of a program at a particular point of time. In other words, snapshot of all the threads alive on the JVM.
Also, a collection of all the callstacks of all the threads that are tracked by the JVM.

### Call Stack - LIFO
* Its a cascading representation of all the methods the thread is called, upto a particular point in time.

### Tools to generate thread dump
* kill -3 PID: Doesn't do any post processing. Handled by JVM Process. Prints thread dump into sysout
* jcmd : prints in the terminal.
* jstack



## Structure of a Thread Dump
A thread dump contains JVM threads, application threads and heap report.
### Individual elements on one thread
* Name
* Number ID
* JVM Priority
* OS Priority
* Thread Address
* Native ID
* Condition
* Thread State
* Thread Call Stack

### Thread States 
* Runnable : Thread is actively invoking code.
* Waiting : The thread will wait indefinitely unless some other thread wakes it up.
* Timed_Waiting : Similar to waiting state. but timed.
* Blocked
* New
* Terminated
### Native Methods
* These are interactions with the host/operating system. These are usually overloaded methods with zero at the end. Ex: socketRead0(Native Method)

## Isolating Performance Issues: A file system congestion
* If successive thread dumps have same thread at the same state, means that either its a long running process or stuck.




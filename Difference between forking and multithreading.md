Difference between forking and multithreading

> [原文链接](https://leetcode.com/discuss/interview-question/125024/Difference-between-forking-and-multithreading/)

A fork gives us a brand new process which is a copy of the current process with the same code segment. 
It looks exactly like the parent process with different process id having it's own memory. 
Parent process creates a separate address space for the child with same code segments but executes independently of each other. 
Because the system issues a new memory space and environment for the child process, it is knows as heavy-weight process.
While threads can execute in parallel with same context. 
Also, memory and other resources are shared between the threads causing less overhead. 
A thread process is considered a sibling while a forked process is considered a child. 
Also, threads are known as light-weight processes as they don't have any overhead as compared to processes (as it doesn't issue any separate command for creating completely new virtual address space). 
A single process can have multiple threads. For all threads of any process, communication between them is direct. While process needs some interprocess communication mechanism to talk to other processes. 
Thought, threads seem to be more useful for any reason, do note that changes in any thread may lead to changes in other threads of the same process. 
While, changes in child processes is independent as parent process has its own execution copy.

Using fork and multi-threading has different use cases.

fork()
fork is one of a few mechanisms to create a new process in Linux.
other alternatives are
system() -- Inefficient and risky
vfork() -- similar to fork but doesn't create identical copy of parent address
space, you have to call exec or exit immediately in child.
Now coming to fork(), it creates a new child process and creates a new address space identical to parent.
So whenever you run any program in your shell it calls fork() and then executes your binary in that new child process, because to create a new process it has to be child of some process, that is how Linux works.

When we want to run any unrelated programs we use fork and run the unrelated binary in new child process and now that's a separate process.

Multi-threading.
In simple words in a single program , if we want to perform multiple task in parallel we use multi-threading.
Taking an example of some ticket booking server. You have multiple tickets(shared resource) available,
we have a socket listening for incoming connections from client , as soon a connection is established we can create a new thread to handle that request, 
In the mean time original thread will continue to listen for new connection and so on. 
Here you have one program and one related resource, so here fork() doesn't make sense. 
Multithreading is useful in these kind of situations.

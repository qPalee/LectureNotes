# Week 4

### Concurrency

#### What is a thread
A thread of execution is the smallest sequence of programmed instructions that can be managed independently by a scheduler, which is typically part of the OS

In the stack, each thread has its own copy of stack related info, but both threads can refer to the common heap, global data and other resources such as opened files, sockets etc

#### pthreads
A thread is created using `pthread_create()`

The syntax is:
```c
int pthread_create(
	pthread_t *thread_id, /* id number for thread */
	const pthread_attr_t *attr, /* controls thread attributes */
	void *(*function)(void*), /* function to be executed */
	void *arg /* argument of function */
)
```
It returns 0 if thread creation is successful, otherwise it will return a nonzero value

Threads cant have multiple arguments, so we must package them into an struct
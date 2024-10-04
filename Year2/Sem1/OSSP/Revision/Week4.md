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

#### Synchronisation
By default threads don't synchronise with the main program.

If the main program finishes running it will return, killing all active threads from that process

This can be prevented in 3 main ways
##### pthread_join()
This is a blocking function with syntax
```C
int pthread_join(
	pthread_t thread_id, //ID of thread to 'join'
	void **value_pntr //address of functions return value
);
```
We will set the value_pntr to NULL always

This stops threads being killed however now we have data inconsistencies due to race conditions
##### Race Conditions
A race condition occurs when 2 or more threads need to perform operations on the same data, but the result depends on the order the operations are performed

This is solved by enforcing <span style="color:#00bfff">mutual exclusion</span>
Threads will get exclusive access to the shared resource in turn

###### mutex
Mutex is how mutual exclusion is done with pthreads

Syntax for declaration and initialisation of a mutex object:
`pthread_mutex_t mutex1 = PTHREAD_MUTEX_INITIALIZER;`

Mutex objects are often declared as global objects

Example of mutex being used
```C
pthread_mutex_lock(&mutex1);
counter++;
pthread_mutex_unlock(&mutex1);
```
The code segment that resides between `mutex_lock()` and `mutex_unlock()` is called <span style="color:#00bfff">critical region</span>
![[Pasted image 20240514124140.png]]


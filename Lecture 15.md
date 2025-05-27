# Multitasking & Control Systems

## Subsumption Architecture
- Invented by Rodney Brooks.
- We don't need no stinking planning.
- The world is its own best representation.
- Based on massively parallel simple microcontrollers.
- Sensor → microcontroller → actuator
- Robot's limbs are driven by reflexes.
- Brain can override reflexes.


## Opposite Extreme
- Multitasking on a single processor
- Processes appear to operate concurrently.
- Fault can produce catastrophic failure.
- Latency
- Performance (with multi-cores)
- Timing

## Software / Hardware

### Cost factor
- Does the central processor cost more than many small processors?
- Costs can be measured in
  - materials purchase price
  - cost of assembly
  - cost of design (NRC: Nonrecurring engineering costs)
  - cost of operation
  - cost of maintenance
- Discreet components generally cost more than heavily integrated circuits.

### Design Factor
- Designing a good distributed system is something of a black art. 
- A central design may be easier to understand and implement.

### Speed Factor
- A distributed system can have the right processor and communications channel for each part. 
- A central system could get overwhelmed if all processes need to be serviced immediately.

### Robustness Factor
- Design of fault tolerance will vary depending on whether tasks are in hardware or software.
- Early vacuum tube computers could not run long until a tube would blow out.
- Many semi-conductor memories are constructed with spare rows, so that when the device is initially tested, defects in the crystal that prevent rows from operating can be bypassed.

## Concurrency
- Multiprogramming – Execution on multiple cores or processors.
- Multitasking – Concurrent execution of several processes.
- Multitasking can be done with or without multiprogramming.
- A single processor doing multitasking may or may not have an operating system.
- When there is no OS, the programmer needs to be aware of the pitfalls.


## Parallelism: 

### Single Instruction
- SISD – Single instruction, single data. Plain vanilla computing.
- SIMD – Single instruction, multiple data. The same instructions run on several arithmetic and logical units (ALUs), but operate on different data sets.
- This is one way to build a massively (meaning hundreds of) parallel processor.
- DSPs or Intel PCs are generally capable of working on four different data sets simultaneously.

### Multiple Instruction
- MISD – Multiple instruction, single data. Multiple cores run different programs, but have access to the same data space. Collision safeguards are required.
MIMD – Multiple instruction, multiple data. Different things are happening on separated data sets. Coordination becomes a problem.

## Threads
- Threads are programs that run concurrently and share data.
- An interrupt service routine is a thread.
- Other threads depend on a scheduler.
- E.A. Lee & S.A. Seshia, Introduction to Embedded Systems, MIT Press, 2nd Ed. 2017, Chapter 11

## Pthreads
- pthread_create() -  start a thread
- pthread_join() – Don’t allow the calling routine to exit until the thread has returned.
- Some embedded processor code never returns, and can be problematic if launched as a thread.
- The order in which threads are executed depends on the scheduler.
- Be sure you understand Lee & Seshia Examples 11.4 and 11.5.

### Example 
https://ptolemy.berkeley.edu/books/leeseshia/

<img width="645" alt="image" src="https://github.com/user-attachments/assets/60955bf1-7551-4239-bf91-d9d44c5191ab" />

## Simple multithreads
- printN (executed as a thread) is called the start routine.
- pthread_create() starts a thread and returns.
- Without pthread_join(), the threads may never execute.
- The program will print “1” ten times and “2” ten times.
- They will be printed in an indeterminate interleaved order.
- The order may vary between executions.

## Examples where you find out whats wrong

### Variants: What happens?

``` c++
Int main (void) {
pthread_t thread1, thread2, thread3;
int x1=1, x2=2, x3=3;
void *exit;
pthread_create( &thread1, NULL, printN, *x1);
pthread_create( &thread2, NULL, printN, *x2);
pthread_create( &thread3, NULL, printN, *x3);
pthread_join(thread3, &exit);
return 0;  }
```

### Variants 2: What happens?
``` c++
Int main (void) {
pthread_t thread1, thread2, thread3;
int x1=1, x2=2, x3=3;
void *exit;
pthread_create( &thread1, NULL, printN, *x1);
pthread_create( &thread2, NULL, printN, *x1);
pthread_create( &thread3, NULL, printN, *x3);
pthread_join(thread1, &exit);
pthread_join(thread2, &exit);
pthread_join(thread3, &exit);
return 0;  }
```

### Variants 3: What happens?
``` c++
Int main (void) {
pthread_t thread1, thread2, thread3;
int x1=1, x2=2, x3=3;
void *exit;
pthread_create( &thread1, NULL, printN, *x1);
pthread_join(thread1, &exit);
pthread_create( &thread2, NULL, printN, *x2);
pthread_join(thread2, &exit);
pthread_create( &thread3, NULL, printN, *x3);
pthread_join(thread3, &exit);
return 0;  }
```

### Lee & Seshia Example 11.5
<img width="643" alt="Screenshot 2025-05-27 at 9 36 36 AM" src="https://github.com/user-attachments/assets/7ad67038-2b4a-4f0b-9555-29398ee3a3f5" />










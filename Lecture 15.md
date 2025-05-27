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


## Thread slicing
- Each thread has its own stack.
- Cooperative multitasking lets a thread run until it makes a library call, with the scheduler determining whether it should continue.
- If using this method, don't let a thread hog too much time.
- A timer interrupt gives each thread a fixed time slice, typically 1 to 10 ms.


## Race Condition
- Two concurrent subroutines or two electrical signals try to access the same resource simultaneously, with an unpredictable outcome.
- A mutual exclusion lock (mutex) can prevent software race conditions.
- pthread_mutex_lock() blocks until the thread can acquire the lock.
- Locks are similar to enabling and disabling interrupts.

<img width="702" alt="image" src="https://github.com/user-attachments/assets/fbc80ea1-f34f-4da9-9096-e31c45c56716" />


## Threading addListener

<img width="782" alt="image" src="https://github.com/user-attachments/assets/e05176e7-24ed-40ba-9014-9c54779adcb8" />


## Mutex locks 

<img width="768" alt="image" src="https://github.com/user-attachments/assets/22316f69-dae0-42fe-8c9f-e00b6e87bcba" />


### Mutex prevents data corruption
- Now two different threads can call addListener.
- Suppose thread1 is at line 23 of addListener when control is transferred to thread2.
- Thread2 calls addListener.
- Thread2 attempts to executepthread_mutex_lock (&lock);but it fails since the lock is in use.
- Execution halts on thread2; control is transferred back to thread1, at least until it unlocks the lock.


## Deadlock
- Deadlock can happen when each thread holds a lock which the other is trying to obtain.
- Deadlock must always be avoided.
- Suppose that two resources are protected by lockA and lockB.
- Suppose thread1 and thread2 need both resources.
- Thread1 sets lockA and starts using resource A.
- Thread2 sets lockB and starts using resource B.
- Suppose both threads have started, but thread2 is currently executing. Thread2 tries to set a lock for resource A but is denied.
- Control transfers to thread1, which then tries to get resource B, but  is blocked.
- Both thread have one of the resources locked and are waiting for the other. That never happens.
- Deadlock!

## Pitfalls
- Sequential consistency is not guaranteed when using threads.
- Sharing variables between threads is dangerous.
- Even with the careful use of locks, an untimely interrupt can be disastrous, and will usually not show up in testing.
- Avoid using threads (other than interrupts) in embedded systems without RTOS.

# Control Systems

## An embedded system is often more than ON/OFF
- Automotive cruise control
- Temperature regulation
- Maintain pressure, temperature, etc. for chemical engineering
- Point a spacecraft to optimize solar panels and antennae
- Maneuver a quadcopter
- Lay 3D print material in precise position

## Motor Control is Common
- Control is often about having an electric motor follow a desired speed profile
- For other applications the system needs to quickly react to changing conditions


## Classic Control Theory
- For a given system, how do you estimate its current state and move it to a desired state?
- Several courses in EE curriculum.
- Highly mathematical with differential equations, matrices and probabilities.
- Favors linear control systems.
- Sophisticated methods try to characterize the system state.
- The methods for today’s lecture treat the true state as a black box.


### Control by reducing error between estimated and desired states
<img width="529" alt="Screenshot 2025-05-27 at 10 09 54 AM" src="https://github.com/user-attachments/assets/7fa53d8c-fdab-4ed2-8dac-c6c9e4b0202a" />

### Control strategies
1) Measure the error, and apply a signal that is proportional to the error.This does not work so well if there is a time lag in system response.
2) Keep a running average of error, and control to reduce average error.This method can be a bit sluggish.
3) Measure the rate at which error is changing.Quick acting, but a bit jittery.

### 3 strategies are derivatives
- x = ∫v = distance
- x’ = v = velocity
- x” = v’ = acceleration
- We are trying to minimize the error in speed
- One method is proportional to speed error.
- The sum of recent speeds is ∫x’ = x
- The change in speed is the derivative dx’/dx = x”
- A good PID tutorial:
  - https://www.youtube.com/watch?v=wkfEZmsQqiA 


## PID has three magic numbers
- Typical values: KP = 0.45, KI = 0.40, KD = 0.05
- More real world considerations for PID controllers are covered in tutorials 2, 3, 4, 5, 6 and 7.
- There are various methods to tune PIDs to come up with good numbers for KP, KI, and KD
- Trial and error usually works.
- Unlike more sophisticated control methods, PID treats the plant as a black box and does not model its dynamics.

### Arduino PID library
<img width="345" alt="Screenshot 2025-05-27 at 10 31 22 AM" src="https://github.com/user-attachments/assets/3d757ff6-d619-4fbc-9ed8-7574929696f9" />



# Memory considerations

## C vs. C++ 
- C offers advantages over C++ for small systems:
- C is often faster.
- C++ statements can generate considerable overhead.
- Almost every chip has a C compiler; C++ is not as widespread.
- Classes are convenient, but you can write object oriented code in almost any language.
- C “struct” does much of C++ “class”.


## Memory Allocation
- In smaller embedded systems, it may be best to avoid malloc().
- How will you handle running out of memory? You probably do not have an OS to provide virtual memory.
- The memory needs of the program are often known. Reserving space for global variables is practical, and not a problem if the program is not too big.
- Memory can be shared with union;
- Specify hardware with enough memory.


## Memory
- Huge influence on speed
- Some memory is volatile – goes away on power off.
- Systems may mix fast and slow memory to save cost or power.
- Cache is fast memory.
- Memory can be mapped to include registers and I/O.

## Random Access Memory (RAM)
- Volatile.
- SRAM (Static) is faster than DRAM (Dynamic) but takes more area on silicon.
- DRAM needs to be periodically refreshed.
- Extra slow response if you try to use it at the same time that hardware is refreshing it.
- DRAM access time varies.
- An address mapped to SRAM will execute faster.

## Read Only Memory (ROM)
- Non-volatile.
- Factory masked ROM cannot be changed.
- Old EPROM (Erasable Programmable) was held under a UV light for 30 minutes to erase.
- EEPROM (Electrically) can take ms to erase.
- Fairly fast to read, but slow to write.

## Arduino and EEPROM
- The Arduino has 1024 bytes of EEPROM
- EEPROM.write() takes 3.3 ms.
- Specified life is 100,000 cycles.
- Write too much, and you wear out the Arduino.
- EEPROM is intended for parameters or firmware that rarely change.


## FLASH form of EEPROM
- Read is slower than SRAM or DRAM.
- Write is way slow.
- NOR is random access
- NAND is faster than NOR, but is a block (100 – 1000 bits) at a time.
- Typically NOR < 1M writes; NAND < 10M

## Non-volatile Peripherals
- Disks require seek time to position read/write head.
- Head is very close to surface; can crash into it if system is vibrating.
- Slow
- SD (secure digital) card is block addressable flash memory. 

## Cache
- Scratchpad is working memory.
- Cache is a duplicate of a memory location.
- The cache memory is faster than the original.
- Logical Address
  - MMU  → Physical Address.
- The Memory Management Unit can make memory access vary by a factor of 1000.

## Alignment
- Words of 16, 32, 64 bits need to be aligned so that they have the same start position.
- The first byte may be MSB (big endian).
- The first byte may be LSB (little endian).
- Some processors map unused address space into bit access addresses.

## Faults
- Segmentation fault: in multi-tasking, code is restricted to an area of memory.
- Garbage collection: automatically doing free().
- Memory leak: programmer never frees memory; Can bring embedded system to a halt.
- No good real-time way to do defragmentation.
- Better to avoid malloc() / free().
- Do not use recursion: stack overflow.

## C memory
- Data normally passed by value.
- Pointers passed by reference.
- Do not expect data on the stack to be valid after subroutine returns.










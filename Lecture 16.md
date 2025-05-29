<img width="1251" alt="image" src="https://github.com/user-attachments/assets/665178c4-bca2-4f81-aea8-685e3625bbbd" />5/29/25

# Scheduling

## Scheduling Decision
- Assignment: which processor should execute the task
- Ordering: in what order each processor executes its tasks
- Timing: the time at which each task executes.

## Types of schedulers
- Fully-static scheduler makes all decisions at design time;
  - but most execution times are data-dependent.
- Static order (off-line) scheduler does assignment and ordering at design time, but executes at run time
  - May depend on mutex and precedence
- Static assignment scheduler performs the assignment at design time and everything else at run time
- Fully-dynamic scheduler performs all decisions at run time

## Preemptive scheduling
- While a task is executing, a preemptive scheduler may stop (preempt) it and begin another task.
- A non-preemptive scheduler always lets tasks run to completion (except maybe for interrupts).
- A task may get preempted if it tries to acquire a mutex but is blocked on the lock.
- A task may be preempted when it releases a lock if a higher priority task needs the lock.

## Task Model: May (or may not) assume
- All tasks are known before scheduling
- New tasks arrive unexpectedly
- All tasks execute periodically
- Tasks are sporadic with irregular repetitions but minimum time between
- Precedence constraints: Task i must precede j
- Tasks have preconditions

<img width="505" alt="image" src="https://github.com/user-attachments/assets/8e4a2bd5-f259-4358-bbbe-e08952e525bf" />

## Deadlines
- In Hard Real-time systems, not completing a task by its deadline is an error
- Soft Real-time systems can continue functioning if a deadline is missed
- Priority may supplement or replace deadlines
  - Fixed priority remains constant
  - Dynamic priority can change during execution

## Scheduling metrics
- A schedule in which all tasks meet their deadlines is called feasible
- A scheduler is optimal with respect to feasibility if it produces a feasible schedule whenever possible.
- Processor utilization is the percentage of time it is executing tasks.
- Maximum lateness is max(finish time – deadline).  
  - It is <=0 for feasible.
- Makespan = max (finish time) – min (release time)

## Rate monotonic (RM) scheduling
- For periodic tasks, the best fixed priority preemptive scheduler does the shortest tasks first
- Give the fastest tasks the highest priority.
- On the Arduino Due or TI 123 (ARM), one interrupt can interrupt another. You are allowed to assign interrupt priorities.
- For interrupts, give fastest interrupt service routines (ISRs) the highest priority.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/5b0c0889-4e37-40b8-a415-2751b5d2e477" />
Assumes that context switch time is negligible, which isn’t always true.

## Tail chaining
- If ISR A is executing when a lower priority interrupt B is asserted, A continues to completion.
- When A completes, it transfers control to ISR B instead of returning to the main routine.
- When ISR B completes, it will return to the main routine.
- Transfer to or from an ISR normally takes 12 cycles on TI 123, largely spent in pushing to the stack.
- Tail chaining only requires 6 cycles, since a push/pop sequence is avoided.

## Utilization
- Utilization is the sum of all ratios of task execution time to period.
- As long as utilization <= 69%, rate monotonic (RM) scheduling is guaranteed to work for any number of tasks.
- RM often works above 69% utilization. There are always students who don’t get this.
- Once utilization gets to 83% or above, rate monotonic scheduling usually does not work.
- There are particular cases where RM can work even at 100% utilization.
<img width="871" alt="image" src="https://github.com/user-attachments/assets/b72609ac-f444-4b3b-8943-84a66d2e2839" />

### Utilization formula
- Students love a formula
- <img width="135" alt="Screenshot 2025-05-29 at 9 18 20 AM" src="https://github.com/user-attachments/assets/842c82c5-9f32-448d-acf7-7eabc6f2d8fe" />
- For n tasks, as long as utilization p follows this bound, you are guaranteed that RM will always produce a feasible schedule.
- If p does not follow the bound, it does not tell you whether a particular schedule is feasible.
- The formula is good theory but rather useless in practice.
- It tells us that it is a good idea to design systems so that utilization stays under 70%

## RM Exercise
- Periodic task T1 has a period of 12 time units and execution time of 1; task T2 has period of 24 time units and execution time of 10 time units; task T3  has period of 8 and takes 3 time units to execute. The tasks are preemptive. 
a) Using Rate Monotonic (RM) scheduling, show the timing for the three tasks.

<img width="559" alt="Screenshot 2025-05-29 at 9 20 35 AM" src="https://github.com/user-attachments/assets/a9a2006f-978b-4854-a36c-6b1ee0f01cba" />

### Solution 
Tasks have no priorities. RM does the tasks with shortest execution times first.

<img width="558" alt="Screenshot 2025-05-29 at 9 20 22 AM" src="https://github.com/user-attachments/assets/3e64077f-1282-4ea6-ad5f-f15b99cfe26c" />


## Earliest deadline first (EDF)
- In the case of non-periodic tasks that do not have priorities, but instead have deadlines, the solution is obvious: do the task with the soonest deadline first. 
This is also called Jackson's algorithm, after the first person to publish the idea. 
A minor modification (select the earliest deadline at the moment) can handle periodic tasks.
EDF is harder to implement than RM, but gives better performance.

### Exercise 
- Periodic task T1 has a period of 12 time units and execution time of one time unit; task T2 has period of 24 time units and execution time of 10 time units; task T3 takes 3 time units to execute and has period of 8. The tasks are preemptive. 
b) If the tasks are non-preemptive, how would they be scheduled with Earliest Deadline First (EDF)?																							

<img width="559" alt="Screenshot 2025-05-29 at 9 20 35 AM" src="https://github.com/user-attachments/assets/a9a2006f-978b-4854-a36c-6b1ee0f01cba" />

### Solution 
At time 18, either T1 or T3 could be scheduled, since they have the same deadline.

<img width="555" alt="Screenshot 2025-05-29 at 9 33 53 AM" src="https://github.com/user-attachments/assets/f735d951-acb0-4fd6-8292-6a76519fe0fe" />

c) Does EDF meet all deadlines? 
- No. The second instance of T3 misses its deadline.

d) What is the maximum lateness for EDF?
- 1 time unit.

e) What is the utilization?
- For both RM and EDF, the processor is idle for 3 of 24 time units. Utilization is 21/24 or 87.5%. This is higher than the 69% guaranteed RM feasibility. It is higher than the 78% guaranteed 3-task RM feasibility.

## Latest deadline; EDF*
- However, EDF is not optimal if there are precedences.
- LDF selects the last task to execute as the one with the latest deadline that no other task depends on.
- LDF does its scheduling backwards.
- To support the arrival of tasks, EDF* uses modified deadlines that take into account dependencies.

### Exercise
It is desired to schedule two periodic tasks, which may be preemptive. Task 1 has period p1 = 4 and execution time e1 = 2. Task 2 has period p2 = 6 and execution time e2 = 3. Show that scheduling is feasible with Earliest Deadline First (EDF) with 100% utilization.
<img width="559" alt="Screenshot 2025-05-29 at 9 20 35 AM" src="https://github.com/user-attachments/assets/a9a2006f-978b-4854-a36c-6b1ee0f01cba" />

### Solution
<img width="526" alt="Screenshot 2025-05-29 at 9 54 25 AM" src="https://github.com/user-attachments/assets/f38a968b-fce9-45fc-90db-9e788c0d0de3" />

### Exercise
Same question above, but: Show that Rate Monotonic (RM) scheduling does not meet deadlines

### Solution
<img width="530" alt="Screenshot 2025-05-29 at 9 57 08 AM" src="https://github.com/user-attachments/assets/e8712570-3a70-48cb-a81a-c4ddb354860c" />

## EDF, LDF, EDF* with precedences(all execution times = 1)
<img width="454" alt="image" src="https://github.com/user-attachments/assets/f9b1c232-e126-4131-8a41-460b5e2bc267" />

## Priority 

### Inversion
<img width="746" alt="image" src="https://github.com/user-attachments/assets/f9c3a809-1672-49b3-8307-9b99207f4567" />

- Priority inversion can be a problem, and it may arise unexpectedly.
- A solution is to use priority inheritance: When a task has a lock, and blocks a higher priority task, the task holding the lock is assigned the priority of the task it is blocking.

### Inheritance
<img width="826" alt="image" src="https://github.com/user-attachments/assets/9a9ec6ab-c60d-4a05-ac7c-b6000b3ad1d4" />

### Ceiling
<img width="781" alt="image" src="https://github.com/user-attachments/assets/63d510aa-3576-424a-bef1-c9977f3bac06" />
- Some deadlocks can be prevented by using the priority ceiling.
- Every lock is assigned a priority equal to the highest priority task that can lock it.
- A task can acquire a lock only if that task has higher priority than any lock currently in use.


## Deadlock
<img width="761" alt="image" src="https://github.com/user-attachments/assets/cfcc0f80-b079-4c0e-9359-fa16eca55df7" />

## Multiple tasks on multiple processors
- Scheduling multiple tasks on multiple processors is NP hard; however, this does not mean infeasible.
- It means that as the numbers of tasks and processors get large, the computations become ever more difficult.
- The key to solving NP-hard problems is to limit choices.
- Keep the number of tasks and processors small.
- A Hu scheduler adds up the execution times of tasks within a dependency branch, and assigns priorities.

## Weird stuff
- Local improvement can result in system-wide degradation in multi-processor scheduling.
- Reducing the execution time of a task can change task orders, resulting in a longer total execution time.
- Increasing the  number of processors can result in slower makespan
- Weakening precedence constrains can increase the schedule length

## Base case
<img width="689" alt="image" src="https://github.com/user-attachments/assets/c883a3e9-d380-4daa-ae5b-527101078233" />

### Reducing execution times by 1 unit
<img width="697" alt="image" src="https://github.com/user-attachments/assets/9160ca3e-143b-4709-b973-d9061c8853aa" />

Makespan increases from 12 to 13 units!

### Adding a fourth processor
<img width="625" alt="image" src="https://github.com/user-attachments/assets/0f620e0f-a059-43ba-85ef-6c4062611c83" />

Makespan increases from 12 to 15 units!

### Tasks 7 and 8 no longer depend on 4
<img width="597" alt="image" src="https://github.com/user-attachments/assets/f25c5f80-5342-4a84-b8e9-c5e268757efc" />

57% utilization

Worst makespan yet: 16 units!

### What if all of the above?
- Decrease all task execution times by one unit
- Add a 4th processor
- No dependencies

## Mutex anomaly
<img width="573" alt="image" src="https://github.com/user-attachments/assets/99c29ad5-9cd4-4b3d-a627-7aa48aac3496" />
- Tasks 1 and 2 are assigned to processor 1; 3, 4 & 5 to processor 2
- Tasks 2 and 4 need the same resource, protected by a mutex
- Decreasing task 1’s execution time increases the total time














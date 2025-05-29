5/29/25

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











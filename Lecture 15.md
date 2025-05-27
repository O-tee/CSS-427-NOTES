<img width="2338" alt="image" src="https://github.com/user-attachments/assets/8ba21918-f15d-4c61-9cb7-9b17dd492222" /># Multitasking & Control Systems

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

## Speed Factor
- A distributed system can have the right processor and communications channel for each part. 
- A central system could get overwhelmed if all processes need to be serviced immediately.

## Robustness Factor
- Design of fault tolerance will vary depending on whether tasks are in hardware or software.
- Early vacuum tube computers could not run long until a tube would blow out.
- Many semi-conductor memories are constructed with spare rows, so that when the device is initially tested, defects in the crystal that prevent rows from operating can be bypassed.
















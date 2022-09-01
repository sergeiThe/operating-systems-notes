# Processes
#process #os #queue #tables #register 

#### OS must do the following:
1. Control dispatch of multiple processes
2. Provide processes with their own resources and protect resources of each process from other processes
3. Let processes exchange data (securely)
4. Let processes synchronize 



## How does operating system control dispatch of applications


## Process

- Identifier (ID)
- State - at what stage the process currently is
- Priority - some processes are more important than others
- Program counter - current or next process (architecture dependent)
- Memory pointer
- Context 
- Status information of I/O
- Other info


![[processstate.png]]
*Process state model*

![[queueprocess.png]]
*Process queue*

## Creation of a process

OS creates data structure for the process

Processes are usually created by OS, however often processes (spawn) new processes.   Parent process & child process.


## Destroying of a process

- Signal HALT
- User action
- Error
- Parent process ended which leads to ending of child processes


![[5 states of processes.png]]
*5 states of processes*


![[doublequeue.png]]
*Double queue*

![[multiqueue.png]]
*Multiqueue*

![[stopped processs.png]]
*Suspended process*

![[2stoppedprocesses.png]]
*2 suspended processes*

## Suspension reasons

- [[Swapping]]
- OS decision
- User decision
- Schedule
- Parent process decision


![[resources1.png]]
*Processes and resources*


## Control structures of OS

1. OS must have information of current process states and resources
2. There is a table for each unit that is being controlled by OS

- [[Memory tables]]
- [[I-O tables|I/O Tables]]
- [[File Tables]]
- [[Process tables]]


There are two [[Work modes|work modes]]

## Process switch

- Which process stimulated the switch
- What must OS do with all structures while switching

1. Save process state (registers)
2. Update control block of the process
3. Move control block of the process in the corresponding queue: ready/blocked-ready/suspend
4. Choose another process for execution
5. Update control block of the process, to which we have to switch
6. Update data structures for memory management
7. Restore process state











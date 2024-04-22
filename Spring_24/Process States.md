---
aliases:
  - Interrupts
  - Processes
  - Scheduler
  - Dispatcher
---
In operating systems, a process goes through various states during its lifetime. The concept of process states is crucial for understanding the execution and management of processes. The typical process states include:

1. **New:**
   - In this state, a process is being created but has not yet been admitted to the pool of executable processes. The operating system is still setting up the necessary data structures for the process.

2. **Ready:**
   - Once the setup is complete, the process moves to the ready state. It is waiting to be assigned to a processor by the operating system's scheduler. In this state, the process is ready to execute and waiting in the ready queue.

3. **Running:**
   - The process moves to the running state when the scheduler assigns it to a processor. It actively executes its instructions during this phase. In a multiprogramming environment, multiple processes may take turns being in the running state.

4. **Blocked (or Waiting):**
   - A process enters the blocked state when it cannot proceed until some event occurs, such as the completion of an I/O operation or the reception of a signal. The process is moved to a blocked queue until the required event takes place.

5. **Terminated:**
   - The process enters the terminated state when it has finished execution or has been explicitly terminated by the operating system or another process. Resources associated with the process are released, and its PCB (Process Control Block) is usually removed.

The transitions between these states create what is known as the process lifecycle or process state diagram. Here's a brief overview of the transitions:

- **Admission:**
  - New → Ready: A process moves from the new state to the ready state once it's set up and ready to execute.

- **Dispatch:**
  - Ready → Running: The scheduler dispatches a process from the ready queue to the running state.

- **Blocking:**
  - Running → Blocked: A process moves to the blocked state when it must wait for an event, like I/O completion.

- **Unblocking:**
  - Blocked → Ready: When the event for which a process was waiting occurs, it moves back to the ready state.

- **Completion:**
  - Running → Terminated: A process moves to the terminated state when it completes execution.

Processes can transition between these states due to events like I/O operations, system calls, or the scheduler's decisions. The transition between states is managed by the operating system, and the state information is typically stored in the process's PCB. Understanding these states helps in designing efficient process management systems within an operating system.
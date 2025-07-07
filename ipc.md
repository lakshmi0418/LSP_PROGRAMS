#IPC THEORY QUESTIONS
```c
1. What is meant by an IPC Mechanism?

IPC (Inter-Process Communication) refers to the methods and mechanisms that allow different processes (running programs) to communicate with each other, share data,

2. Why we use IPC Mechanism?

IPC stands for Inter-Process Communication.
It is used to allow multiple processes to communicate and coordinate with each other
IPC provides a way for processes to exchange data, signals, or synchronization messages.
For example, a client process can send a request to a server process using IPC.
IPC is also used to prevent race conditions and ensure that shared data is accessed safely.
Different IPC mechanisms include pipes, message queues, shared memory, semaphores, signals, and sockets.

3. What are the types of IPC Mechanism's?
    Pipes:
Allow one-way communication between related processes (usually parent and child).
 Data flows in a FIFO (first-in-first-out) manner.
 Named Pipes (FIFOs)
 Like pipes but can be used between unrelated processes.
Identified by a name in the filesystem.
  Message Queues
Allow processes to exchange discrete messages.
Kernel manages the queue; supports asynchronous communication.
 Shared Memory
Multiple processes share a memory segment.
Fastest IPC but requires synchronization (e.g., semaphores).
Semaphores
Used primarily for synchronization between processes.
Control access to shared resources to avoid race conditions.
 Signals
Send simple notifications or interrupts between processes.
No data is transferred, only a signal number.
Sockets
Support communication between processes over a network or on the same machine.
Supports both connection-oriented (TCP) and connectionless (UDP) communication.

4. What is meant by “unicast” and “multicast” IPC?

unicast IPC is a one-to-one communication model:
A single sender process communicates with a single receiver process.
It’s directed communication — the message is intended for a specific process.
Most IPC mechanisms like pipes, message queues, shared memory, and signals (with specific PID) use unicast.
 Example:
A parent process sends data to one child process through a pipe.

ulticast IPC is a one-to-many communication model:
 One sender process sends a message to multiple receiver processes simultaneously.
example:
A server broadcasts an event notification to multiple clients using multicast UDP or signals sent to a process group.

5. What is meant by PIPES?

PIPES refer to a method of inter-process communication (IPC) used in operating systems."

"They allow data to flow from one process to another in a unidirectional or bidirectional manner."

"A common example is in Unix or Linux, where the pipe operator | is used to pass the output of one command as input to another."
6. What is meant by Blocking Calls?

A blocking call is a function or operation that does not return control to the program until it has completed its task."

"During a blocking call, the execution of the program is paused and waits for the operation to finish."

7. What are the types of Blocking Calls?

8. What are the different types of I/O Calls?
9. What are the I/O calls we are used in IPC Mechanisms?
10. What are the Blocking Calls used in IPC?

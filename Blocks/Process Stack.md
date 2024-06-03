The process management stack in the Linux kernel refers to the comprehensive set of mechanisms, data structures, and functions the kernel uses to manage processes. This encompasses process creation, scheduling, context switching, termination, and inter-process communication. Here's a detailed breakdown of the process management stack from the ground up:
### 1. Process Descriptor (`task_struct`)

The central data structure for process management is the `task_struct`. This structure holds all the information about a process, including its state, scheduling parameters, memory management details, file descriptors, and more.

```c
struct task_struct {
    // Process state
    volatile long state;

    // Scheduling information
    struct sched_entity se;

    // Process identifiers
    pid_t pid;
    pid_t tgid;

    // Memory management info
    struct mm_struct *mm;
    
    // Signal handling info
    struct signal_struct *signal;

    // List of open files
    struct files_struct *files;

    // Process list links
    struct list_head tasks;
    
    // More fields...
};
```

### 2. Process States

Processes can be in various states, which are stored in the `state` field of `task_struct`. Common states include:

- `TASK_RUNNING`: The process is runnable.
- `TASK_INTERRUPTIBLE`: The process is waiting for an event and can be interrupted.
- `TASK_UNINTERRUPTIBLE`: The process is waiting and cannot be interrupted.
- `TASK_STOPPED`: The process is stopped.
- `TASK_ZOMBIE`: The process has terminated but has not been reaped by its parent.

### 3. Process Creation

Processes are created using system calls such as `fork()`, `vfork()`, and `clone()`. These calls create a new process by duplicating the calling process, with `clone()` allowing more fine-grained control over what is shared between parent and child.

```c
pid_t fork(void);
pid_t vfork(void);
pid_t clone(int flags, void *stack, int *parent_tid, int *child_tid, unsigned long tls);
```

### 4. Process Scheduling

The scheduler determines which process runs on the CPU. The default scheduler in Linux is the Completely Fair Scheduler (CFS), which uses a red-black tree to manage scheduling entities (`sched_entity`).

```c
struct sched_entity {
    struct load_weight load;
    struct rb_node run_node;
    u64 vruntime;
    // More fields...
};
```

The CFS aims to provide fair CPU time to all processes by maintaining a virtual runtime (`vruntime`) for each process.

### 5. Context Switching

Context switching is the process of saving the state of the currently running process and loading the state of the next process to run. This involves saving the CPU registers, program counter, and stack pointer of the current process and restoring these for the next process.

### 6. Process Termination

Processes terminate using the `exit()` system call. The `do_exit()` function in the kernel handles process termination, releasing resources and changing the process state to `TASK_ZOMBIE`.

```c
void do_exit(long code);
```

### 7. Inter-Process Communication (IPC)

Linux provides several IPC mechanisms:

- **Signals**: Notifications sent to processes to notify them of events.
- **Pipes and FIFOs**: Unidirectional data channels.
- **Message Queues**: Allow processes to exchange messages.
- **Shared Memory**: Allows multiple processes to access the same memory region.
- **Semaphores**: Synchronization primitives.

### 8. Process Hierarchy and Namespaces

Processes in Linux are organized in a hierarchical structure, where each process has a parent and can have multiple children. Process identifiers (PIDs) are used to uniquely identify processes. PID namespaces allow processes to have the same PID in different namespaces, providing isolation.

### 9. Kernel Threads

Kernel threads are similar to user-space processes but run entirely in kernel space. They are used for various background tasks within the kernel.

### Important Kernel Data Structures

1. **`task_struct`**: Main process descriptor.
2. **`mm_struct`**: Describes a process's memory layout.
3. **`signal_struct`**: Holds signal-related information.
4. **`files_struct`**: Manages the list of open files.
5. **`sched_entity`**: Contains scheduling information.

### Key System Calls for Process Management

- **`fork()`**: Creates a new process.
- **`exec()`**: Replaces the current process image with a new one.
- **`wait()`**: Waits for a state change in a child process.
- **`exit()`**: Terminates the calling process.
- **`kill()`**: Sends a signal to a process or a group of processes.
---
![[Process Management Stack (Recap).drawio.png]]

---

## Related to: 
- [[Third Session]]
- [[ProcessStackRecord]]
# Process Stack Record

- # Sessions Output (A quick review)
    1. Process [Kernal-Userspace]
    2. Signal
    3. Create output --> Core-dump
    4. Monitoring Processes
    5. Understand --> Priority
    6. Init Process
    >⚡ `How is userspace = init-process ? What even is an init-process ?`
---
- ## Most important stacks
    - **Process** Stack
    - **Network** Stack
    - **Filesystem** Stack
---
- ## Process Management Stack
    - Userspace is just a bunch of processes running
    - Process : Program Running in memory (RAM)

- ## Process C/S :-
    - Kernel assign PID (Process ID) to each processs
    - Kernel assign **PPID** (Process ID) to each process (**What is the difference between PID and PPID ?**)
    - Priority --> **[PR - NI]**
    - Type --> [Init Process - Zombie - **Daemon**]
    - States --> [Sleep - Waiting - Running - Blocking - Zombie]
    - Each process has allocated RAM (Virtual Memory)

- ## What Processes can do :-
    - Interact with resources [files - syscalls]
    - Send **signals** to other processes (But what are signals ?)
    - **Fork** (create .. how though ?) another process

- ## Operations we can do on process stack
   - There is two modes (Foreground and Background) that we can choose from when running a process or a command (**Difference Important in customization**)
        - Foreground processes blocks bash from operating till it finishes running
        - Background processes don't block bash from operating
        - `pstree` **(*IMPORTANT AF COMMAND*, search to know more)**
        - `top` **(IMPORTANT COMMAND)** --> CPU column in `top` is how much of a thread a process takes and not how much of a cpu a process takes up
        - `jobs` *(IMPORTANT COMMAND)*
        - `fg` *(IMPORTANT COMMAND)*
        - `kill` *(IMPORTANT COMMAND, CHECK FLAGS AND IT IS NOT ONLY FOR KILL SIGNALS)*
    - Assigning priorities
        1. Assign at runtime `nice` from **user space** (ranges from **[-20,19]** *with -20 being highest priority*), `renice` changes priority at runtime
        2. **Kernel space** assigned **PR** ranges from **[-51,49]**, the kernel maps the niceness priority depending on internal decisions from [-20,19] to [-51,49]
---
- ## Signals
    - A Software Interrupt that interrupts a process or used in Inter-Process Communication (Not mainly used in Inter-Process Communication, we use SOMEIP)
- ## Signals C/S:-
    - Name
    - Number
    - Sender (User Using Terminal or Process or Kernel)
    - Receiver (Process)
    - Action (There is types of actions like **Core**, **Term**, **Ign**, **Stop**)
        1. Action from kernel POV:
            - **core**: Terminate **process** then produce **core-dump** file for tracing
        > 🤔    But what is a Core-Dump file ?

            - **term**: Only Terminate process
        2. Action from receiver process POV:
            - Do process before doing the signal or not depending on the signal
    >   Gap of knowledge: **Signal Handler**, last function to be called before termination ?
> ❗Difference between signal and syscall ? signal is sent to process and syscall is sent to kernel
- ## Operations
    - Run 🏃
    - Stop 🛑
    - Send process to background
    - Send process to foreground
    - Send signal to process
    - Change process priority
    - Check this link --> https://www.man7.org/linux/man-pages/man7/signal.7.html
---
- ## Extras
-   > ⁉️ What is **CrossCutting** concept ? "Related to the '*Everything is a file*' mindset in linux"

-   > ❗What are  **threads**  and its relation to pipelining ?
-   **`lscpu`** Check this command and the data it outputs
- https://stackoverflow.com/questions/8887531/which-real-time-priority-is-the-highest-priority-in-linux
-   https://www.youtube.com/watch?v=aNEqC-U5tHM
-   Check Signals Documentation
---
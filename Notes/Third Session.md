# Third Session Record
---
- # Use Case Discussion
    - How should you break the use case to solve it ?
        - Measuring time --> `time` command and `strace`
        - Identify System Stack --> `strace -e trace = $stackname [command]` this last command gives how a command calls a certain stack from kernel to use its functionality, for more info use documentation of `strace`
        - Break down the total execution time --> `strace`
        - Analyze the results from the 3 previous steps --> depends on user trying to identify the problem
> What is the difference here in the time given by `time` command and by `strace` command ? ***SEARCH FOR ANSWER***
---
- ## `ls` vs `find`
    - `find` is recursive by nature
    - Both of them interact with **process stack**, **file system stack** and **memory stack**
    - `ls` uses less resources and is simpler but `find` provides a lot more less functionality than `find` command
---
- ## `cp` vs `rsync`
    - They do the same functionality but `rsync` can copy and move files to a or from a remote machine on the network
    - Both of them interact with **process stack**, **file system stack** and **memory stack**, but `rsync` interacts with **network stack**
    - `cp` takes less time if we remove the extra functionality of `rsync`
---
- # Timing
    1. Time wasted in user space is called ***user*** time
    2. Time wasted in kernel space is called ***sys*** time
    3. ***real*** time = ***user*** + ***sys*** + timing (waiting time) --> 
> Usually waiting time is decided by process management stack while running other processes
---
- # Process Management Stack Recap and Discussions
    - Everything is a file
    - Files of interactions
    - Foreground and background
    - Priority Assignment
    - Signals --> Termination
    - Observe Terminated process using `pstree`
---
- ## Run --> Actors
    - There is processes ran by kernel (`systemd` and `systemv`)
    - There is processes ran by user (like applications or programs)
---
- ## Everything Is A File and Files of Interactions
    - **Crosscutting concept** is a rule that applies to all our software we write, in our Linux case the crosscutting concept is **`"Everything is a file & syscall"`**
    - Take an example a C++ application wants to:
        - Access Hardware Driver
        - Access Process Management Stack
        - Access Network Management Stack
        - Access Memory Management Stack
    - It writes to a file called "UART file" `Char Device` and it accesses the hardware device drivers through it
    - Same goes in every other aspect of accessing the stacks or device drivers --> `opening a socket using a file in network stack, reading current processes through a file in process stack aka "/proc/pid"`
---
- ## Foreground vs Background
    - Foreground processes break control from the user of terminal while background processes do not break it
    - To run a command or a process in background add `&` in the end
> We will visit this topic again and when to choose between them when explaining init process `SystemV`
---
- ## Priority Assignment (`Nice` vs `Renice`)
    - We most of the time use `nice` in the industry
    - When do we use `renice` at run-time ? in Embedded Linux
---
- ## Signals --> Control Processes
    -  Action ***P*** --> Last action the process does before it dies "Signal_Handler"
    -  Action ***K*** --> The action the kernel can do depending on `core` or `term` types of signals
        - `core` --> takes snapshot of process and makes **`core_dump`** file
        - `term` --> Just terminates the signal
    -   Some processes types does not do action ***P*** (does not call the `Signal_Handler`), while other do
    -   `Kill -[SignalName] [pid]` to kill a process
    -   Difference between **Syscalls** and **Signals**: Difference is the direction and reciever
        - **Syscalls** interrupts kernel to do a certain function : `User Space --> Kernel`
        - **Signals** interrupts processes to control it to do something : `Kernel --> Process`, `Process --> Kernel --> Process`
> Revise last record note **(the part about signals)**
---
- ## Observe Terminated process using `pstree`
    - Read docs on `watch` command
    - Solution is left as an exercise for the reader :"D
---
- ## Extras
    -   `strace` documentation --> https://man7.org/linux/man-pages/man1/strace.1.html
    -   More on Processes and Signals --> https://www.youtube.com/watch?v=ls5cGi12kGw&list=PLtK75qxsQaMKLUENMaPlD_O2qS8ZBGjuy
    -   System Programming Course --> https://www.youtube.com/watch?v=TavEuAJ4z9A&list=PLhy9gU5W1fvUND_5mdpbNVHC1WCIaABbP
    -   **`NOTE THAT THERE IS A HUGE GAP OF KNOWLEDGE IN THIS SESSION ABOUT SIGNALS AND PROCESSES IN GENEREL, USE THE "READ MORE DOCUMENT", YOUTUBE VIDS AND USECASE TO FILL SOME GAPS`**
---
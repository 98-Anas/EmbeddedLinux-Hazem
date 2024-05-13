# Second Session

- ## Embedded Linux System Components (A quick review)
    - ### Init Process:     --> *Point 1*
        - System V *(Gap of knowledge)* 
        
        >       ⚠️ Older Projects Work on this init process..
        - Systemd --> *Part of the course*
    - ### UserSpace
        - Apps --> ***C++* (focused)**  **-->** **Point 2**
            - Commands
            - User-Defined
  - ### libc  --> *Point 3*
        - glibc 
        - ulibc --> What is this ? *(Gap of knowledge)*
    - ### Customization of a kernal --> *Point 4* *(Big gaps of knowledge)*
        - Buildroot
        - YOCTO
        
---
- ## Some Recap on Syscall
    - Each Syscall has:
        -  Name
        -  Entry Point
        -  Stack that introduces it to the Userspace (or to glibc)
        -  Number in interrupt table
---
- ## Difference Between Invoking Syscall directly and by Calling a function from libc
    -  Syscall Direct
        - All logic from scratch
        - Depends on Kernal (Which may face us with H.W depen. problems)
    - Calling Function
        - Simpler
        - Abstraction from kernal
        - Contains all logic needed
>        ⛔  We will never direct call systemcalls, It's forbidden for Kernal Newbies
---
- ## Systable
    - Is a hashtable that contains what each syscall number lead to from the different implementations
    - Depends on Architecture, as the hashmap itself changes with archs *(Kinda ? needs more search)*
        - The above reason tells us again why calling syscalls directly makes our life more miserable
    >   Check Runtime graph on website to see full map of how a process invokes a system call with a certain system call ID, which glibc then checks against the systable 
        >>   ### ☠️    THE SYSTABLE ITSELF IS PART OF THE KERNAL AND NOT THE LIBC, AS IT DEPENDS ON THE ARCHITECTURE

- ### The Question on Stack Exchange **"Dependance between sycall, systable and Archs"**
    > Here is a link https://unix.stackexchange.com/questions/421750/where-do-you-find-the-syscall-table-for-linux
    - What the hell is an ABI ? 
        - >https://stackoverflow.com/questions/2171177/what-is-an-application-binary-interface-abi
        - If(Time.free()) Edit the generator repo to get the syscall table but for arm arch *(rpi is arm)*
            - >https://github.com/FiloSottile/mostly-harmless/tree/main/filippo.fly.dev/filippo.io/linux-syscall-table 
---

- ## Operations (Commands) Needed from User Space  *"Observability"*
    - **Strace** for System tracing
        - > ### Note: Strace by default outputs on *stderr* buffer, grep by default takes *stdoutput* buffer, so doing something like "strace ls | grep "arch_prctl" will not work like you'd expect, as grep will take the output of ls command itself.."
            - Stdin  : 0
            - Stdout : 1
            - Stderr : 2
    - **Ltrace** for Library Tracing
    - **Perf** for Analysis

>   ## Hint: use tldr for quick info/examples on new commands, don't forget to {*tldr --update*} before using it
---
- ## Questions and Discussions: 
    -   The whole section was a discussion especially **the question about systable and archs**
---
- ## Additional Resources
    - https://www.youtube.com/watch?v=gojeTqXdBH0&t=59s&ab_channel=%D8%A8%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8ABigData -->
        *This one is a long tutorial but it's a general one*

    - https://www.youtube.com/watch?v=VbEx7B_PTOE&list=PLIhvC56v63IJIujb5cyE13oLuyORZpdkL&ab_channel=NetworkChuck --> *This is a general one also, but it builds quick knowledge in widely used commands. it's also bite-sized*
    - https://cpu.land/ --> *Connecting baremetal knowledge to linux kernal intro **(kinda)***
    - https://www.amazon.com/Linux-Internals-Simplified-beginners-guide/dp/B087SHCBD4 --> *A small book for easing into linux internals system*
    - https://www.amazon.com/Learning-Modern-Linux-Handbook-Practitioner/dp/1098108949 --> *The book which Eng. Hazem gave us the intro chapters from. cool intro ngl*
    ---
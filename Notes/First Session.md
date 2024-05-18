# First Session

- ## Difference between Customization of a kernel and introducing a new architecture
    * Customization is taking a kernel that supports the board, but we need to remove some stacks and need some other stacks. Introducing a new architecture is adding a folder with all needed H.W dependent code in /Linux/arch/ folder tree


>       🚀  Check /Linux/arch/ folder for some extra information

---
- ## If we Change Hardware, what do we change in the Embedded Linux System ?
    *   Change Arch folder
    *   We change Drivers 
    *   Re-Compile code source With a compiler compatible with the new Arch.
        *   for everything:   
            *   C++ App
            *   glibc 
            *   Kernel
            *   Drivers
>       ⚠️   We recompile Because Assembly syntax is changed, cuz CPU arch is changed

---
- ## Questions and Discussions: 
    - ### What Is glibc ?
        * A library that provides a wrapper for **syscalls** to Kernel Space **(instead of direct system calls)**
        * Why it exists ?
            * Simpler
                * if the function needs more than one syscall and some extra logic like error handling automatically
            * Standardize Naming Conventions 
                * if systemcalls depend on kernel version or hardware we'll not need to change it if we use glibc
                * Abstract App --> Kernel Space
    - ### Use Case on Website..
        - Problems in the system: 
            - it runs sluggishly, often experiencing delays.
            - The Ethernet driver functions intermittently
            - Certain C++ applications fail to run, displaying an error message related to the *libstdc++.so.6* component of the GNU Library (glibc).
        - Solution Suggested:
        
            a.  Problem in customization or in board specifications, either we use less stacks in the kernel or we order a stronger board for better specifications needed for the project in demand
            2.  The problem here was we used a wrong version of the driver, a new version of it fixed this bug **(We should've read the full docs of the driver with release notes of this version and the previous versions)**
            3.  The problem here was the C++ application was searching for a wrong linked version from *libstdc++* component
---
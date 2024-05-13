# First Session

- ## Difference between Customization of a kernal and introducing a new architecture
    * Customization is taking a kernal that supports the board, but we need to remove some stacks and need some other stacks. Introducing a new architecture is adding a folder with all needed H.W dependant code in /linux/arch/ folder tree


>       🚀  Check /linux/arch/ folder for some extra information

---
- ## If we Change Hardware, what do we change in the Embedded Linux System ?
    *   Change Arch folder
    *   We change Drivers 
    *   Re-Compile code source With a compiler compatible with the new Arch.
        *   for everything:   
            *   C++ App
            *   glibc 
            *   Kernal
            *   Drivers
>       ⚠️   We recompile Because Assembly syntax is changed, cuz cpu arch is changed

---
- ## Questions and Discussions: 
    - ### What Is glibc ?
        * A library that provides a wrapper for **syscalls** to Kernal Space **(instead of direct system calls)**
        * Why it exists ?
            * Simpler
                * if the function needs more than one syscall and some extra logic like error handling automatically
            * Standardize Naming Conventions 
                * if systemcalls depend on kernal version or hardware we'll not need to change it if we use glibc
                * Abstract App --> Kernal Space
    - ### Use Case on Website..
        - Problems in the system: 
            - it runs sluggishly, often experiencing delays.
            - The Ethernet driver functions intermittently
            - Certain C++ applications fail to run, displaying ane rror message related to the *libstdc++.so.6* component of the GNUCLibrary (glibc).
        - Solution Suggested:
        
            a.  Problem in customization or in board specifications, either we use less stacks in the kernal or we order a stronger board for better specifications needed for the project in demand
            2.  The problem here was we used a wrong version of the driver, a new version of it fixed this bug **(We should've read the full docs of the driver with release notes of this version and the previous versions)**
            3.  The problem here was the C++ application was searching for a wrong linked version from *libstdc++* component
---
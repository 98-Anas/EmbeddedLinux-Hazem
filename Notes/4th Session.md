# Fourth Session

- # Recap on Filesystems
    - Attributes of a filesystem
    - Why VFS exist ?
    - How to write on a **sd card**
> Making a mount point permanent ? add it in the /etc/fstab config file
---
- ## Attributes of a filesystem
    -   Type
    -   Mount Point
    -   R/W, RD
    -   Max amount of R/W of device
---
- ## Why VFS exists ?
    - Not Couple our kernel to a specific FS
    - extend storage in runtime
---
- ## How to write on a **sd card** ?
    1. Create partitions
    2. Create FS
    3. Mount user space storage to the sd card driver detected (But it will be temporary mount) 
---
- # Commands for userspace
    - ## Paths:
        - `cd`
        - `pwd`
        - `export`
    - ## Directories:
        - `mkdir`
        - `rm -r`
        - `cp`
        - `mv`
        - `cd`
        - *`chmod`*
    - ## Files:
        - `touch`
        - `cat`
        - *`source`*
        - `rm`
        - `mv`
        - `cp`
---
- # First Use case
    - ## Create FHS (File Hierarchy Standard) Directories:
        - View Standard FS dirctories of ubuntu image:
            ```bash
            cd /
            tree -L 1
            ```
        - Create your own FS directories
        ```bash
            mkdir myfilesystem
            cd myfilesystem
            mkdir bin boot dev etc
            echo "Primary hierarchy root and root directory of the entire file system hierarchy" >> purpose.txt
            cd bin
            echo "Essential command binaries that need to be available in single-user mode; for all users, e.g., cat, ls, cp." >> purpose.txt
            cd ..
            ... (Repeat for the rest)
        ```
    - ## Hard and Soft Links
        - Views of a file :
        `File Path --> Inode (data string of fileName and Location in Physical memory`
        - There is two types of Links for paths, Symbolic Links and Hard Links
            - Hard Links: You create a new path that points to Inode of file 'x' 
            `NewPath --> Inode --> file 'x'
            ,Old Path ---> Inode --> file 'x'`
            - Symbolic Links: We create a new path that points to a new Inode that points to old Inode
            `New Path --> NewInode --> OldInode --> file 'x'`
        > For checking hard links, use `find <TARGETDIR> -type f -samefile  <THEFILENAME>`
        -   Usage of symbolic links: When different applications need to link dynamically to a certain library and this library have a new version every now and then, what we do is `C++ Application *--SymbolicNotDependingOnVersion-->* ` 
---
- ## Extras
    -   Learn Vim --> https://vim-adventures.com/


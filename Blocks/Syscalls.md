System calls (syscalls) are the mechanism by which user-space applications request services from the kernel. These services include tasks that require higher privileges than those granted to user-space applications, such as interacting with hardware, managing processes, and performing I/O operations. Syscalls provide a controlled interface for user-space programs to access the kernel's capabilities while maintaining system stability and security.

### Key Characteristics of Syscalls

1. **Privilege Level Transition**:
   - Syscalls involve a transition from user mode (with limited privileges) to kernel mode (with full privileges). This transition ensures that user-space applications cannot directly execute privileged instructions or access critical system resources.

2. **Standardized Interface**:
   - Syscalls provide a standardized interface for performing a variety of system-level operations. Each syscall is identified by a unique number and has a defined set of parameters.

3. **Isolation and Protection**:
   - By using syscalls, the operating system isolates user-space applications from the kernel, protecting the system from potential errors or malicious actions by applications.

### Common Syscalls

Syscalls cover a wide range of functionalities. Some common categories and examples include:

1. **File Operations**:
   - `open()`, `close()`, `read()`, `write()`, `lseek()`, `stat()`

2. **Process Management**:
   - `fork()`, `execve()`, `exit()`, `waitpid()`, `getpid()`, `kill()`

3. **Memory Management**:
   - `mmap()`, `munmap()`, `brk()`

4. **Inter-Process Communication (IPC)**:
   - `pipe()`, `shmget()`, `shmat()`, `semget()`, `semop()`, `msgget()`, `msgsnd()`, `msgrcv()`

5. **Network Operations**:
   - `socket()`, `bind()`, `listen()`, `accept()`, `connect()`, `send()`, `recv()`, `shutdown()`

### How Syscalls Work

1. **User-Space Application**:
   - An application in user space makes a function call provided by a library (e.g., glibc) to perform an operation that requires kernel services.

2. **Library Wrapper**:
   - The library function prepares the arguments and invokes the appropriate syscall. This often involves using an assembly instruction (such as `syscall` on x86_64 architectures) to switch to kernel mode.

3. **Transition to Kernel Mode**:
   - The CPU switches from user mode to kernel mode, saving the state of the user-space process and executing the syscall handler in the kernel.

4. **Kernel Processing**:
   - The kernel performs the requested operation, such as reading data from a file or creating a new process. It ensures that the operation adheres to security policies and resource management rules.

5. **Return to User Mode**:
   - After completing the operation, the kernel returns the result to the user-space application, and the CPU switches back to user mode, restoring the application's state.

### Example of a Syscall in C

Here’s an example of using the `open` and `read` syscalls in a C program:

```c
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>

int main() {
    int fd = open("example.txt", O_RDONLY);
    if (fd == -1) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    char buffer[100];
    ssize_t bytesRead = read(fd, buffer, sizeof(buffer) - 1);
    if (bytesRead == -1) {
        perror("read");
        close(fd);
        exit(EXIT_FAILURE);
    }

    buffer[bytesRead] = '\0';
    printf("Read: %s\n", buffer);

    close(fd);
    return 0;
}
```

### Direct Invocation of Syscalls

In some cases, you might need to invoke syscalls directly, bypassing the standard library wrappers. This can be done using the `syscall` function provided by glibc:

```c
#include <unistd.h>
#include <sys/syscall.h>
#include <stdio.h>
#include <fcntl.h>

int main() {
    int fd = syscall(SYS_open, "example.txt", O_RDONLY);
    if (fd == -1) {
        perror("syscall open");
        return 1;
    }

    char buffer[100];
    ssize_t bytesRead = syscall(SYS_read, fd, buffer, sizeof(buffer) - 1);
    if (bytesRead == -1) {
        perror("syscall read");
        syscall(SYS_close, fd);
        return 1;
    }

    buffer[bytesRead] = '\0';
    printf("Read: %s\n", buffer);

    syscall(SYS_close, fd);
    return 0;
}
```

### Summary

- **Syscalls** are the bridge between user-space applications and the kernel, providing controlled access to system resources and operations.
- **User-Space Interaction**: Applications use library functions (like those in glibc) to make syscalls, which handle the details of transitioning to kernel mode and back.
- **Kernel Processing**: The kernel executes the requested operation, ensuring it follows security and resource management policies.
- **Common Syscalls**: Examples include `open()`, `read()`, `write()`, `fork()`, `execve()`, `mmap()`, `socket()`, and many others.
- **Direct Invocation**: Syscalls can be directly invoked using the `syscall` function for low-level programming needs.
---

![[System call Interface.drawio (2).png]]

---

## Related to: 
- [[Second Session]]
- 
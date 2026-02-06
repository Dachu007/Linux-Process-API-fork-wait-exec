# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
int pid = fork();

if (pid == 0) { 
    printf("I am child, my PID is %d\n", getpid()); 
    printf("My parent PID is: %d\n", getppid()); 
    sleep(2);  // Keep child alive for verification
} else { 
    printf("I am parent, my PID is %d\n", getpid()); 
    wait(NULL); 
}
}
```













## OUTPUT

<img width="703" height="157" alt="Screenshot from 2026-02-06 09-16-41" src="https://github.com/user-attachments/assets/43e923f4-d40e-4dde-899b-9be4fc81ab0b" />

<img width="704" height="224" alt="Screenshot from 2026-02-06 09-21-54" src="https://github.com/user-attachments/assets/bc138770-ae47-4f3f-8d69-ec2b76164da8" />










## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family

```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
int status;

printf("Running ps with execl\n");
if (fork() == 0) {
    execl("ps", "ps", "-f", NULL);
    perror("execl failed");
    exit(1);
}
wait(&status);

if (WIFEXITED(status)) {
    printf("Child exited with status: %d\n", WEXITSTATUS(status));
} else {
    printf("Child did not exit successfully\n");
}

printf("Running ps with execlp (without full path)\n");
if (fork() == 0) {
    execlp("ps", "ps", "-f", NULL);
    perror("execlp failed");
    exit(1);
}
wait(&status);

if (WIFEXITED(status)) {
    printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
} else {
    printf("Child did not exit successfully\n");
}

printf("Done.\n");
return 0;
}
```


## OUTPUT



<img width="1626" height="698" alt="Screenshot from 2026-02-06 09-18-33" src="https://github.com/user-attachments/assets/d572754a-92df-4905-b3e3-a89e26c826d0" />















## RESULT:
The programs are executed successfully.

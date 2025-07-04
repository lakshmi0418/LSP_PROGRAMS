#PROCESS MANAGEMENT
```c
/Write a C program to illustrate the use of the execve() function.
#include<stdio.h>
#include<unistd.h>
int main()
{
        char *args[]={"ls","-l",NULL};
        char *env[]={NULL};
        if(execve("/bin/ls",args,env)==-1)
        {
                printf("failed");
                return 1;
        }
        printf("if execvp is sucecc this was not running");
}

// Write a program in C to create a zombie process and explain how to avoid it
#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/wait.h>
#include<stdlib.h>
int main()
{
        pid_t pid=fork();
        if(fork<0)
        {
                printf("fork failed");
                return 1;
        }
        if(pid==0)
        {
                printf("child process:%d",getpid());
                exit(0);
        }
        else
        {
                printf("parent=%d child=%d",getpid(),pid);
                wait(NULL);
                printf("take the child");
        }
}

/ Write a program in C to create a daemon process.
#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/wait.h>
#include<stdlib.h>
#include<fcntl.h>
#include<sys/stat.h>
int main()
{
        pid_t pid=fork();
        int stat;
        if(fork<0)
        {
                printf("fork failed");
                return 1;
        }
        if(pid>0)
        {
                //parent exit
                printf("daemon process%d\n",pid);
                exit(EXIT_SUCCESS);
        }
        // Child continues and becomes session leader
    setsid();

    // Fork again to ensure it can't acquire terminal
    pid=fork();
    if(pid<0)
    {
            exit(EXIT_FAILURE);
}
if(pid>0)
{
        exit(EXIT_SUCCESS);
}
//set permissions
umask(0);
//change working directory root
chdir("/");
//close file descriptors
close(STDIN_FILENO);
close(STDOUT_FILENO);
close(STDERR_FILENO);
//daemon write a loop every 5 sec
while(1)
{
        FILE *fp=fopen("/temp/file.txt","a+");
        if(fp!=NULL)
        {
                fprintf(fp,"daemon running\n ");
                return 1;
        }
        sleep(5);
}
}

/Write a C program to demonstrate the use of fork() system call.
//he fork() system call creates a new process.

//The child process prints a message with its PID.

//The parent process prints a message with its PID and the child's PID.

#include<stdio.h>
#include<unistd.h>
int main()
{
        pid_t pid=fork();
        if(pid<0)
        {
                perror("fork failed");
                return 1;
        }
        if(pid==0)
        {
                printf("child pid%d",getpid());
        }
        else
        {
                printf("parent and chiled lids%d %d",getpid(),pid);
        }
}

/Write a C program to illustrate the use of the execvp() function.
#include<stdio.h>
#include<unistd.h>
int main()
{
        char *args[]={"ls","-l",NULL};
        if(execvp(args[0],args)==-1)
        {
                printf("failed");
                return 1;
        }
        printf("if execvp is sucecc this was not running");
}
//Write a C program to create a child process using fork() and demonstrate process
//communication using named pipes (FIFOs).
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <string.h>
#include <sys/wait.h>

#define FIFO_NAME "myfifo"

int main() {
        char buf[20];
    // Create the named pipe (FIFO)
    if (mkfifo(FIFO_NAME, 0666) == -1) {
        perror("mkfifo");
        // Continue if already exists
    }
     pid_t pid=fork();

        if(pid<0)
        {
                perror("fork failed");
                exit(EXIT_FAILURE);
        }
        if(pid==0)
        {
                int fd=open(FIFO_NAME,O_RDONLY);
                printf("hello child\n");
                read(fd,buf,sizeof(buf));
                exit(0);
        }
        else
        {
                int fd=open(FIFO_NAME,O_WRONLY);
 printf("hello parent\n");
                const char *recv="parent received";
   write(fd,recv,strlen(recv)+1);
                printf("received msg%s\n",recv);

                wait(NULL);
        }
}
/Write a program in C to create a child process using fork() and print its PID.
#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
int main()
{
        pid_t pid=fork();
        if(pid==0)
        {
                printf("create child process%d",getpid());
        }
        else
        {
                printf("parentid=%d,child=%d",getpid(),pid);
        }
}
//Write a C program to create multiple child processes using fork() and display theirPIDs.

#include<stdio.h>
#include<unistd.h>
#include<sys/wait.h>
int main()
{
        int n=3;
        for(int i=0;i<n;i++)
        {

        pid_t pid=fork();
        if(pid<0)
        {
                perror("fork failed");
                return 1;
        }
        if(pid==0)
        {
                printf("i=%d child pid=%d par pid=%d\n",i+1,getpid(),getppid());
        }
        else
        {
                printf("%d chiled lids%d %d\n",i+1,pid);
                wait(NULL);
        }

        }}
// Write a C program to demonstrate the use of the waitpid() function for process
//synchronization.
 //waitpid() function for process synchronization between a parent and child process. The child performs some work (simulated using sleep()), and the parent waits for it to finish using waitpid()
#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/wait.h>
#include<stdlib.h>
int main()
{
        pid_t pid=fork();
        int stat;
        if(fork<0)
        {
                printf("fork failed");
                return 1;
        }
        if(pid==0)
        {
                printf("child process:%d\n",getpid());
                sleep(10);//simulate some work
                printf("child finished%d\n",getpid());
                exit(EXIT_SUCCESS);
        }
        else
        {
                printf("parent=%d",getpid());
                waitpid(pid,&stat,0);
                printf("take the child");
        }
        if(WIFEXITED(stat))
        {
                printf("child exited%d\n",WEXITSTATUS(stat));
        }
else
        {
                printf("child not exit");
}
printf("parent procee continus%d\n ",getpid());
}
//Write a C program to demonstrate the use of the system() function for executing shell commands.
#include<stdio.h>
#include<sys/types.h>
#include<stdlib.h>
int main()
{
        int res;
        //list all the cur directory contents
        res=system("ls -l");
        if(res==-1)
        {
                perror("error");
        }
        //creating directory
        res=system("mkdir basic");
        if(res==-1)
        {
                perror("error");
        }
        res=system("date");
        if(res==-1)
        {
                perror("error");
        }
        res=system("rmdir temp");
        if(res==-1)
        {
                perror("error");
        }
        return 0;
}
/Write a C program to create a process using fork() and pass arguments to the child
//process.
#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/wait.h>
#include<stdlib.h>
int main()
{
        char *arg1="hello";
        char *arg2="world";
        pid_t pid=fork();
        if(pid<0)
        {
                perror("failed");
                exit(EXIT_FAILURE);
        }
        if(pid==0)
        {
                printf("chiled process%d",getpid());
                execl("./child","child",arg1,arg2,NULL);
                perror("execlp");
                exit(EXIT_FAILURE);
        }
        else
        {
                wait(NULL);
                printf("child finished parent process%d",getpid());
        }

}
//Write a C program to demonstrate the use of the execvpe() function.
#define _GNU_SOURCE
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
int main()
{
        char *args[]={"ls","-l","/process",NULL};
        char *env[]={"myvar=hellofromenv",NULL};
        if(execvpe("ls",args,env)==-1)
        {
                perror("failed");
                exit(EXIT_FAILURE);
        }
}
//Write a C program to create a process group and change its process group ID (PGID).
#include<stdio.h>
#include<sys/types.h>
#include<unistd.h>
#include<stdlib.h>
int main()
{
        pid_t pid=fork();
        if(pid==0)
        {
                printf("childid%d\n",getpid());
                printf("childgid %d\n",getpgrp());
                if(setpgid(0,0)==-1)
                {
                        perror("failed");
                }
                printf("after setpgid%d\n",getpgrp());
        }
        else
        {
                sleep(2);
                printf("parent id%d\n",getpid());
                printf("parent gid%d\n",getpgrp());
        }

}
//Write a C program to create a child process using vfork() and demonstrate its usage
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
int main()
{
        pid_t pid=vfork();
        printf("parent process %d",getpid());
        if(pid<0)
        {
                perror("no create fork");
        }
        if(pid==0)
        {
                printf("chidid:%d parent:%d",getpid(),getppid());
                // Example: Replace child process image
        execlp("/bin/echo", "echo", "Hello from child process!", NULL);
        }
        else
        {
                printf("parent process resumed\n");
        }
}

//Write a C program to create a child process using fork() and communicate between
//parent and child using pipes.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<string.h>
#include<sys/wait.h>
int main()
{
        int pipefd[2];
        char buf[100];
//      pid_t pid=fork();
        if(pipe(pipefd)==-1)
        {
                perror("failed to pipe");
                exit(EXIT_FAILURE);
        }
         pid_t pid=fork();

        if(pid<0)
        {
                perror("fork failed");
                exit(EXIT_FAILURE);
        }
        if(pid==0)
        {
                close(pipefd[1]);
                read(pipefd[0],buf,sizeof(buf));
                printf("received msg%s\n",buf);
                close(pipefd[0]);
        }
        else
        {
                close(pipefd[0]);
                char msg[]="hello world";
                write(pipefd[1],msg,strlen(msg)+1);
                close(pipefd[1]);

 wait(NULL);
        }
}

/Write a C program to demonstrate the use of the prctl() system call to change process
//attributes.
#define _GNU_SOURCE  // Required for prctl constants

#include <stdio.h>
#include <stdlib.h>
#include <sys/prctl.h>
#include <string.h>
#include <unistd.h>
int main()
{
        const char *newname="hello world";
        if(prctl(PR_SET_NAME,(unsigned long)newname,0,0,0)==-1)
        {
                perror("set failed");
                exit(EXIT_FAILURE);
        }
        const char *name;
        printf("new %s\n",newname);
        if(prctl(PR_GET_NAME,name,0,0,0)==-1)
        {
                perror("set failed");
                exit(EXIT_FAILURE);
        }
        printf("name%s\n",name);
        / /Sleep to allow checking via 'ps -C my_process' in another terminal
    printf("Sleeping... Check process name via 'ps -C 'hello world\n");
    sleep(30);
}
/Write a C program to create a child process using fork() and demonstrate process
//communication using sockets.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<string.h>
#include<sys/wait.h>
#include<sys/socket.h>
int main()
{
        int socket_pair[2];
        char buf[100];
//Create a pair of connected sockets
    if (socketpair(AF_UNIX, SOCK_STREAM, 0, socket_pair) == -1) {
        perror("socketpair failed");
        exit(EXIT_FAILURE);
    }

//      pid_t pid=fork();
/*      if(pipe(pipefd)==-1)
        {
                perror("failed to pipe");
                exit(EXIT_FAILURE);
        }*/
         pid_t pid=fork();

        if(pid<0)
        {
                perror("fork failed");
                exit(EXIT_FAILURE);
        }
        if(pid==0)
        {
                close(socket_pair[1]);
                printf("hello child\n");
                read(socket_pair[0],buf,sizeof(buf));
                const char *recv="child recived";
write(socket_pair[1],recv,strlen(recv)+1);
                printf("received msg%s\n",buf);
                close(socket_pair[0]);
                exit(0);
        }
        else
        {
                close(socket_pair[0]);
                printf("hello parent\n");
                read(socket_pair[0],buf,sizeof(buf));
                const char *recv="parent received";
                write(socket_pair[1],recv,strlen(recv)+1);
                printf("received msg%s\n",buf);
                close(socket_pair[1]);

                wait(NULL);
        }
}
```


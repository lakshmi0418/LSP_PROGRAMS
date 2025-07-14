```c
//Implement a program that uses pipes for communication between a parent and child
//process. Show how data can be passed between processes using pipes.
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
#include<sys/wait.h>
int main()
{
        int fd[2];
        pid_t pid;
        char read_msg[100];
        char write_msg[]="hello from parent";
        if(pipe(fd)==-1)
        {
                perror("pipe");
                return 1;
        }
        pid=fork();
        if(pid<0)
        {
                perror("fork");
                return 1;
        }
        if(pid>0)
        {
                close(fd[0]);
                write(fd[1],write_msg,strlen(write_msg)+1);
                close(fd[1]);
                wait(NULL);
        }
        else
        {
                close(fd[1]);
                read(fd[0],read_msg,sizeoF(read_msg));
                printf("chiled received%s\n",read_msg);
                close(fd[0]);
```

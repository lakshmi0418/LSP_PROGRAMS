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
}
return 0;
}
    //Create a program where two processes communicate synchronously using pipes.
//Ensure that one process waits for the other to finish before proceeding.
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
#include<sys/wait.h>
int main()
{
        int child_fd[2];
        int parent_fd[2];
        pid_t pid;
        //char read_msg[100];
        //char write_msg[]="hello from parent";
        if((pipe(child_fd)==-1)||(pipe(parent_fd)==-1))
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
        if(pid==0)
        {
                close(child_fd[1]);
                close(parent_fd[0]);
                char buf[100];
                read(child_fd[0],buf,sizeof(buf));
                printf("child buf recv:%s\n",buf);
                char reply[]="hello parent";
                write(parent_fd[1],reply,strlen(reply)+1);
                close(child_fd[0]);
                close(parent_fd[1]);
}
        else
        {
                close(child_fd[0]);
                close(parent_fd[1]);
                char msg[]="hello child";
                write(child_fd[0],msg,strlen(msg)+1);
                //printf("child buf recv:%s\n",buf);
                //char reply[]="hello parent";
                waitpid(pid,NULL,0);
                char buf[100];
                read(parent_fd[0],buf,sizeof(buf));
                printf("parent received%s\n",buf);
                close(child_fd[1]);
                close(parent_fd[0]);

}
return 0;
}
    /Implement a program that uses Named pipes for communication between two processes.
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
                read(fd[0],read_msg,sizeof(read_msg));
                printf("chiled received%s\n",read_msg);
                close(fd[0]);
}
return 0;
}
//44. Write a C program to create a message queue using the msgget system call. Ensure
//that the program checks for errors during the creation process
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/ipc.h>
#include<sys/msg.h>
int main()
{
        key_t key;
        int msg_id;
        //create unique key
        key=ftok("dummy",65);
        if(key==-1)
        {
                perror("ftok");
                return 1;
        }
        // Create a message queue with read/write permissions for owner
        msg_id=msgget(key,IPC_CREAT|0666);
        if(msg_id==-1)
        {
                perror("msgget");
                return 1;
        }
        printf("msgqueue created successfully%d:",msg_id);
}
/evelop two separate C programs, one for sending messages and the other for
//receiving messages through a created message queue.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/ipc.h>
#include<sys/msg.h>
#include<string.h>
struct sample
{
        int msg;
        char msg_txt[100];
};
int main()
{
        key_t key;
        int msg_id;
        struct sample message;
        //create unique key
        key=ftok("dummy",65);
        if(key==-1)
        {
                perror("ftok");
                return 1;
        }
        // Create a message queue with read/write permissions for owner
        msg_id=msgget(key,IPC_CREAT|0666);
        if(msg_id==-1)
        {
                perror("msgget");
                return 1;
        }
        printf("enter msg");
        if((fgets(message.msg_txt,100,stdin))==NULL)
        {
                perror("fgets error");
                return 1;
}
        if(msgsnd(msg_id,&message,strlen(message.msg_txt)+1,0)==-1)
        {
                perror("send error");
                return 1;
        }
        printf("msgqueue sending  successfully%s:",message.msg_txt);
}
/evelop two separate C programs, one for sending messages and the other for
//receiving messages through a created message queue.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/ipc.h>
#include<sys/msg.h>
#include<string.h>
struct sample
{
        int msg;
        char msg_txt[100];
};
int main()
{
        key_t key;
        int msg_id;
        struct sample message;
        //create unique key
        key=ftok("dummy",65);
        if(key==-1)
        {
                perror("ftok");
                return 1;
        }
        // Create a message queue with read/write permissions for owner
        msg_id=msgget(key,IPC_CREAT|0666);
        if(msg_id==-1)
        {
                perror("msgget");
                return 1;
        }
        /*printf("enter msg");
        if((fgets(message.msg_txt,100,stdin))==NULL)
        {
                perror("fgets error");
                return 1;
}*/
        if(msgrcv(msg_id,&message,sizeof(message.msg_txt),1,0)==-1)
        {
                perror("send error");
                return 1;
        }
        printf("msgqueue recv  successfully%s:",message.msg_txt);
/*if (msgctl(msg_id, IPC_RMID, NULL) == -1) {
        perror("msgctl(IPC_RMID) failed");
        exit(EXIT_FAILURE);
    }*/

}
//Create a program to remove an existing message queue using the msgctl system call.
//Ensure that the program prompts the user for confirmation before deleting the
//message queue.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/ipc.h>
#include<sys/msg.h>
int main()
{
        key_t key;
        int msg_id;
        //create unique key
        key=ftok("dummy",65);
        if(key==-1)
        {
                perror("ftok");
                return 1;
        }
        // Create a message queue with read/write permissions for owner
        msg_id=msgget(key,IPC_CREAT|0666);
        if(msg_id==-1)
        {
                perror("msgget");
                return 1;
        }
        printf("msgqueue created successfully%d:",msg_id);
        printf("enter the response:(y/n)");
        char resp=getchar();
        if(resp!='y')
        {
                perror("response errror");
                return 1;
        }
        /* Remove the queue */
    if (msgctl(msg_id, IPC_RMID, NULL) == -1) {
        perror("msgctl(IPC_RMID) failed");
exit(EXIT_FAILURE);
    }
    printf("message queue deleted:%d",msg_id);


}
         

```

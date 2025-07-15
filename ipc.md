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
        exit(EXIT_:FAILURE);
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
         //Design a multithreaded program where threads communicate through named pipes
#include<stdio.h>
#include<pthread.h>
#include<fcntl.h>
#include<unistd.h>
#include<string.h>
#include<pthread.h>
#include<stdlib.h>
#include<sys/stat.h>
#define fifo_path "/tmp/myfifo" 
void *reader(void *arg)
{
        int fd=open(fifo_path,O_WRONLY);
        char *s="hello writer";
        write(fd,s,strlen(s));
        close(fd);
        return NULL;
}
void *writer(void *arg)
{
        int fd=open(fifo_path,O_RDONLY);
        char s[100];
        read(fd,s,sizeof(s));
        printf("recv=%s",s);
        close(fd);
        return NULL;
}
int main()
{
        pthread_t red,wri;
        //create  named pipe
        mkfifo(fifo_path,0666);
        pthread_create(&red,NULL,reader,NULL);
        pthread_create(&wri,NULL,writer,NULL);
        pthread_join(red,NULL);
        pthread_join(wri,NULL);
        unlink(fifo_path);

}
//message queues. Ensure that one process waits for the other to finish before
//proceeding.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/ipc.h>
#include<sys/msg.h>
#include<string.h>
#include<sys/wait.h>
struct msg_buf
{
        long type;
        char text[100];
};
int main()
{
        key_t key=ftok("temp",65);
        int msg_id=msgget(key,0666 | IPC_CREAT);
        if(fork()==0)
        {
        struct msg_buf msg;
        msg.type=1;
        strcpy(msg.text,"hello child");
        msgsnd(msg_id,&msg,sizeof(msg.text),0);
        printf("child send\n");
        }
        else
        {
                struct msg_buf msg;
        msgrcv(msg_id,&msg,sizeof(msg.text),1,0);
        printf("par recv=%s",msg.text);
       // printf("parent receice\n");
        wait(NULL);
        msgctl(msg_id,IPC_RMID,NULL);
        }

}
//50. Design a program that uses a message queue for synchronization between multiple
//processes.

#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/ipc.h>
#include<sys/msg.h>
#include<string.h>
#include<sys/wait.h>
#define size 100
#define num 3
struct msg_buf
{
        long type;
        char text[size];
};
int main()
{
        key_t key=ftok("temp1",65);
        int msg_id=msgget(key,0666 | IPC_CREAT);
        for(int i=0;i<num;i++)
        {
        if(fork()==0)
        {
        struct msg_buf msg;
        msg.type=1;
        snprintf(msg.text,size,"hello child%d",i+1);
        msgsnd(msg_id,&msg,sizeof(msg.text),0);
        printf("child send%d\n",i+1);
        }
        else
        {
                struct msg_buf msg;
        msgrcv(msg_id,&msg,sizeof(msg.text),1,0);
        printf("par recv=%s",msg.text);
        }
for(int i=0;i<num;i++)
        {
                wait(NULL);
        }
       // printf("parent receice\n");
        //wait(NULL);
        msgctl(msg_id,IPC_RMID,NULL);
        //}

}
//Write a C program that initializes a shared memory segment using shmget.

#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/ipc.h>
#include<sys/msg.h>
#include<string.h>
#include<sys/shm.h>
#define size 1024

int main()
{
        key_t key=ftok("temp2",65);
        if(key==-1)
        {
                perror("key failed");
                return 1;
        }
        int shm_id=shmget(key,size,0666 | IPC_CREAT);
        if(shm_id==-1)
        {
                perror("failed msg id");
                return 1;
        }
printf("shared memory seg created\n");
printf("key=%d\n",key);
printf("shm_id=%d\n",shm_id);

}
#include<sys/msg.h>
#include<string.h>
#include<sys/shm.h>
#define size 1024

int main()
{
        char * shared_mem;
        key_t key=ftok("temp2",65);
        if(key==-1)
        {
                perror("key failed");
                return 1;
        }
        //get the existing shared memory seg
        int shm_id=shmget(key,size,0666 | IPC_CREAT);
        if(shm_id==-1)
        {
                perror("failed msg id");
                return 1;
        }
        shared_mem=(char *)shmat(shm_id,NULL,0);
        if(shared_mem==(char*)(-1))
        {
                perror("attached");
                return 1;
        }
        //read and write to shared memory
        printf("write to shared memory\n");
       strcpy(shared_mem,"hello shared memry");
printf("%s\n",shared_mem);
if(shmdt(shared_mem)==-1)
{
        perror("detach");
        return 1;
}
printf("detach  sahred mem\n");
}
//Create a program that forks multiple processes, and each process communicates using
//shared memory.

#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/ipc.h>
#include<sys/msg.h>
#include<string.h>
#include<sys/shm.h>
#include<sys/wait.h>
#define size 1024
#define num 3
int main()
{
        char * shared_mem;
        key_t key=ftok("temp2",65);
        if(key==-1)
        {
                perror("key failed");
                return 1;
        }
        //get the existing shared memory seg
        int shm_id=shmget(key,size,0666 | IPC_CREAT);
        if(shm_id==-1)
        {
                perror("failed msg id");
                return 1;
        }
        shared_mem=(char *)shmat(shm_id,NULL,0);
        if(shared_mem==(char*)(-1))
        {
                perror("attached");
                return 1;
        }
        for(int i=0;i<num;i++)
        {
 if(fork()==0)
                {
                        /// Each child writes to its own part of shared memory
            char message[size];
            snprintf(message, size, "Message from child %d\n", i + 1);
            strcpy(shared_mem + (i * size), message);

            // Detach and exit
            shmdt(shared_mem);
            exit(0);
        }
        }
                for(int i=0;i<num;i++)
                {
                        wait(NULL);
                }
                printf("paren reads all msgs\n");
                for(int i=0;i<num;i++)
                {
                        printf("%s",shared_mem+(i*size));
                }
        shmdt(shared_mem);
        shmctl(shm_id,IPC_RMID,NULL);
}

```

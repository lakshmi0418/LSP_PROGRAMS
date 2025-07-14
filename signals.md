```c
//Write a C program to catch and handle the SIGINT signal.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
void sighandler(int sig)
{
        const char msg[]="catch sigint";
        write(STDOUT_FILENO,msg,sizeof(msg)-1);
        exit(EXIT_SUCCESS);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=sighandler;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        if(sigaction(SIGINT,&sa,NULL)==-1)
        {
                perror("errro");
                return 1;
        }
        printf("ctrl+c sig handler");
        while(1)
        {
                pause;
        }
        return 0;
}

//14. Write a program to handle the SIGWINCH signal (window size change.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
#include<sys/ioctl.h>
void signahandle(int sig)
{
struct winsize ws;
if(ioctl(STDOUT_FILENO,TIOCGWINSZ,&ws)==-1)
{
        perror("ioctl");
        return;

}
printf("window size:row %d col %d ",ws.ws_row,ws.ws_col);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGTSTP,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
printf("Installed SIGWINCH handler");

    // Keep the process alive to await signals
    while (1) {
        pause();
    }
//Create a C program to ignore the SIGCHLD signal temporarily
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<sys/types.h>
#include<sys/wait.h>
void fork_wait()
{
        pid_t pid=fork();
       if(pid==0)
       {
exit(0);
       }
       else
       {
               printf("child %d",pid);
       }

}
int main()
{
        struct sigaction sa_ignore,sa_old;
        sigemptyset(&sa_ignore.sa_mask);
        sa_ignore.sa_flags=0;
        if(sigaction(SIGCHLD,&sa_ignore,&sa_old)==-1)
        {
                perror("errro sigignore");
                return 1;
        }
        printf("ignore sigchld\n");
                fork_wait();
        if(sigaction(SIGCHLD,&sa_old,NULL)==-1)
                        {
                        perror("restore") ;
                        return 1;
                        }

printf("restored\n");
        fork_wait();
        sleep(5);
        //clear child
        wait(NULL);
        printf("clean child\n");

}
//Write a program to block the SIGTERM signal using sigprocmask()
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
int main()
{
        sigset_t blockmask,oldmask;
        sigemptyset(&blockmask);
        sigaddset(&blockmask,SIGTERM);
while(sigprocmask(SIG_BLOCK,&blockmask,&oldmask)==-1)
{
perror("error blocked");
return 1;
}
printf("blocked signal%d\n",getpid());
sleep(2);
while(sigprocmask(SIG_SETMASK,&oldmask,NULL)==-1)
{
        perror("error unblocked");
        return 1;
}
printf("unblocked\n");
}
/Implement a C program to handle the SIGALRM signal using sigaction().
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<signal.h>
#include<sys/time.h>
#include<string.h>
static int tick;
void handlealrm()
{
        char buf[100];
        int n=snprintf(buf,sizeof(buf),"%d",++tick);
        write(STDOUT_FILENO,buf,n);
}
int main()
{
        struct sigaction sa;
        struct itimerval timer;
        memset(&sa,0,sizeof(sa));
        sa.sa_handler=handlealrm;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags;
        while(sigaction(SIGALRM,&sa,NULL)==-1)
        {
                perror("in alam");
                return 1;
        }
        //timerset every 1 sec
        timer.it_value.tv_sec=1;
        timer.it_value.tv_usec=0;
        timer.it_interval.tv_sec=1;
        timer.it_interval.tv_usec=0;
        while(setitimer(ITIMER_REAL,&timer,NULL)==-1)
        {
                perror("timererrror");
                return 1;
        }
printf("timer started ctrl+c");
while(1)
{
        pause();
}
}
//Write a C program to install a custom signal handler for SIGTERM
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
void signahandle()
{
        const char s[]="Received SIGTERM — exiting now.\n";
        write(STDOUT_FILENO,s,sizeof(s)-1);
        _exit(EXIT_SUCCESS);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGTERM,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
        printf("install custom signal handler%d\n",getpid());
        while(1)
        {
                pause();
        }
        return EXIT_SUCCESS;
}
/Implement a program to handle the SIGSEGV signal (segmentation fault
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
void signahandle(int sig,siginfo_t *info,void *context)
{
        char s[100]="Received SIGTERM — exiting now.\n";
        int len=snprintf(s,sizeof(s),"sigsegadr%p  signal=%d",info->si_addr,sig);
        write(STDOUT_FILENO,s,len);
        _exit(EXIT_SUCCESS);
}
int main()
{
        struct sigaction sa;
        sa.sa_sigaction=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGSEGV,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
        printf("install sigsegv");
        int *p=NULL;
        *p=40;
        printf("vnever exucute%d",*p);

        return EXIT_SUCCESS;
}
/Create a program to handle the SIGILL signal (illegal instruction).
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
void signahandle(int sig,siginfo_t *info,void *context)
{
        const char *code_desk;
        switch(info->si_code)
        {
        case ILL_ILLOPC:code_desk="illigal opcade";break;
        case ILL_ILLOPN:code_desk="illigal oprand";break;
       case ILL_ILLADR:code_desk="illigal address";break;
       case ILL_ILLTRP:code_desk="illigal trap";break;
       default:printf("invalid");
}

        char s[100]="Received SIGTER\n";
        int len=snprintf(s,sizeof(s),"SIG= %d sigill=%s sigadr=%p",sig,code_desk,info->si_addr);
        write(STDOUT_FILENO,s,len);
        _exit(EXIT_SUCCESS);
}
int main()
{
        struct sigaction sa;
        sa.sa_sigaction=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=SA_SIGINFO;
        while(sigaction(SIGILL,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }

        printf("SIGILL handler installed\n");
    fflush(stdout);
asm("ud2"); // causes illegal opcode exception

    // not print
    printf("This won't print.\n");
}
//Write a program to handle the SIGABRT signal (abort)
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
void signahandle()
{
        char s[100]="Received SIGabrt — exiting now.\n";
        //int len=snprintf(s,sizeof(s),"sigsegadr%p  signal=%d",info->si_addr,sig);
        write(STDOUT_FILENO,s,strlen(s)-1);
        _exit(EXIT_SUCCESS);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGABRT,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
        printf("install sSIGABRT");
        abort();//raises SIGABRT and invokes handler, then exits
        printf("vnever exucut");

        return EXIT_SUCCESS;
}
//Implement a C program to handle the SIGQUIT signal.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
static volatile sig_atomic_t quit_count = 0;
void signahandle()
{
        char s[100]="Received SIGquit — exiting now.\n";
        //int len=snprintf(s,sizeof(s),"sigsegadr%p  signal=%d",info->si_addr,sig);
        write(STDOUT_FILENO,s,strlen(s)-1);
        quit_count++;
        while(quit_count>=3)
        {
                const char exit_msg[] = "Exiting after 3 SIGQUITs.\n";
        write(STDOUT_FILENO,exit_msg,strlen(exit_msg)-1);
        _exit(EXIT_SUCCESS);
        }
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGQUIT,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
printf("Custom SIGQUIT handler installed (PID %d).\n", getpid());
    printf("Press Ctrl+\\ up to 3 times to exit.\n\n");

    while (1) {
        pause();  // Wait indefinitely for signals
    }
}
/Write a program to handle the SIGTERM signal (termination reque
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
void signahandle()
{
        char s[100]="Received SIGTERM — exiting now.\n";
        //int len=snprintf(s,sizeof(s),"sigsegadr%p  signal=%d",info->si_addr,sig);
        write(STDOUT_FILENO,s,strlen(s)-1);
        _exit(EXIT_SUCCESS);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGTERM,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
 printf("Installed SIGTERM handler (PID %d). Send SIGTERM to test.\n", getpid());

    // Keep the process alive to await signals
    while (1) {
        pause();
    }

        return EXIT_SUCCESS;
}
//Write a program to handle the SIGTSTP signal (terminal stop).
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
void signahandle()
{
        char s[100]="Received stop  — exiting now.\n";
        //int len=snprintf(s,sizeof(s),"sigsegadr%p  signal=%d",info->si_addr,sig);
        write(STDOUT_FILENO,s,strlen(s)-1);
        _exit(EXIT_SUCCESS);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGTSTP,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
printf("Installed SIGstop handler (PID %d). Send SIGstop to test.\n", getpid());

    // Keep the process alive to await signals
    while (1) {
        pause();
    }


        return EXIT_SUCCESS;
}
//Write a program to handle the SIGVTALRM signal (virtual timer expired).
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
#include <sys/time.h>
void signahandle()
{
        char s[100]="virtual timer  — exiting now.\n";
        //int len=snprintf(s,sizeof(s),"sigsegadr%p  signal=%d",info->si_addr,sig);
        write(STDOUT_FILENO,s,strlen(s)-1);
        _exit(EXIT_SUCCESS);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGVTALRM,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
struct itimerval timer = {
        .it_value = {1, 0},      // first expiration after 1 sec CPU time
        .it_interval = {1, 0}    // then every 1 sec CPU time
    };

    if (setitimer(ITIMER_VIRTUAL, &timer, NULL) == -1) {
        perror("setitimer");
        return EXIT_FAILURE;
    }

    printf("Started virtual timer: SIGVTALRM every 1s of CPU time.\n");
    fflush(stdout);
/ Busy loop to consume CPU time
    volatile unsigned long count = 0;
    while (1) {
        count++;
        if (count % 1000000000UL == 0)
            write(STDOUT_FILENO, ".", 1);
    }

    return EXIT_SUCCESS;
}
//14. Write a program to handle the SIGWINCH signal (window size change.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
#include<sys/ioctl.h>
void signahandle(int sig)
{
struct winsize ws;
if(ioctl(STDOUT_FILENO,TIOCGWINSZ,&ws)==-1)
{
        perror("ioctl");
        return;

}
printf("window size:row %d col %d ",ws.ws_row,ws.ws_col);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGTSTP,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
printf("Installed SIGWINCH handler");

    // Keep the process alive to await signals
    while (1) {
        pause();
    }
return EXIT_SUCCESS;
}

//Implement a C program to handle the SIGXFSZ signal (file size limit exceeded)i.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
void signahandle()
{
        char s[100]="error file size.\n";
        //int len=snprintf(s,sizeof(s),"sigsegadr%p  signal=%d",info->si_addr,sig);
        write(STDOUT_FILENO,s,strlen(s)-1);
        _exit(EXIT_SUCCESS);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGXFSZ,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
printf("Installed SIGtxfsz handler");

    // Keep the process alive to await signals
    char buf[100]={0};
    while (1) {
            if(STDOUT_FILENO,buf,sizeof(buf));
            {
                    perror("error");
                            return 1;
        //pause();
    }
    }
//Create a program to handle the SIGPWR signal (power failure restart).
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
void signahandle()
{
        char s[100]="sigpower caught restored.\n";
        //int len=snprintf(s,sizeof(s),"sigsegadr%p  signal=%d",info->si_addr,sig);
        write(STDOUT_FILENO,s,strlen(s)-1);
        _exit(EXIT_SUCCESS);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGPWR,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
printf("SIGPWR handler installed. PID=%d\n", getpid());
    printf("Simulating work... (try `kill -SIGPWR %d` to test)\n", getpid());

    // Main work loop
    while (1) {
        sleep(10);
        printf("Working... alive.\n");
        fflush(stdout);
    }

        return EXIT_SUCCESS;
}
//Write a program to handle the SIGSYS signal (bad system call)..
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
void signahandle(int sig)
{
        char s[100]="error catch sigsys.\n";
        //int len=snprintf(s,sizeof(s),"sigsegadr%p  signal=%d",info->si_addr,sig);
        write(STDOUT_FILENO,s,strlen(s)-1);
        _Exit(128 + sig);/// exit with signal-style code
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGSYS,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
printf("SIGSYS handler installed. PID=%d\n", getpid());
    printf("To test: invoke a bad syscall (e.g., with seccomp filter) or try calling syscall(-1,...)\n");

    // Example: provoke SIGSYS by an invalid syscall
    syscall(-1, 0, 0, 0);

    // If the above doesn't trigger, just pause
    pause();


        return EXIT_SUCCESS;
}

/19. Write a C program to handle the SIGIO signal (I/O is possible on a descriptor)
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
#include<sys/ioctl.h>
void signahandle(int sig)
{
struct winsize ws;
if(ioctl(STDOUT_FILENO,TIOCGWINSZ,&ws)==-1)
{
        perror("ioctl");
        return;

}
printf("window size:row %d col %d ",ws.ws_row,ws.ws_col);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGTSTP,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
printf("Installed SIGWINCH handler");

    // Keep the process alive to await signals
    while (1) {
        pause();
    }
/0. Implement a C program to handle the SIGINFO signal (status request fheyyboard)

#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
#include<sys/ioctl.h>
void signahandle(int sig)
{
printf("siginfo received\n");
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGIO,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
//printf("Installed SIGWINCH handler");
//printf("Program is running. Press Ctrl+T to send SIGINFO.\n");


    // Keep the process alive to await signals
    while (1) {
        pause();
    }


        return EXIT_SUCCESS;
}
/1. Create a C program to handle the SIGRTMIN signal (minimum real-time signal)
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
#include<sys/ioctl.h>
void signahandle(int sig,siginfo_t *info,void *con)
{
        printf("catch signal%d (SIGRTMIN)\n", sig);
printf("Signal sent by PID: %d\n", info->si_pid);
    printf("Signal value: %d\n", info->si_value.sival_int);

}
int main()
{
        struct sigaction sa;
        sa.sa_flags=SA_SIGINFO;

        sa.sa_sigaction=signahandle;
        sigemptyset(&sa.sa_mask);
//      sa.sa_flags=SA_SIGINFO;

        while(sigaction(SIGRTMIN,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
        printf("Process PID: %d\n", getpid());
    printf("Waiting for SIGRTMIN (send it using: `kill -SIGRTMIN %d` or `sigqueue`)...\n", getpid());

//printf("Installed SIGWINCH handler");
//printf("Program is running. Press Ctrl+T to send SIGINFO.\n");


    // Keep the process alive to await signals
    while (1) {
 pause();
    }


        return EXIT_SUCCESS;
}

/1. Create a C program to handle the SIGRTMAX signal (maximum real-time signal)
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
#include<sys/ioctl.h>
void signahandle(int sig,siginfo_t *info,void *con)
{
        printf("catch signal%d (SIGRTMAX)\n", sig);
printf("Signal sent by PID: %d\n", info->si_pid);
    printf("Signal value: %d\n", info->si_value.sival_int);

}
int main()
{
        struct sigaction sa;
        sa.sa_flags=SA_SIGINFO;

        sa.sa_sigaction=signahandle;
        sigemptyset(&sa.sa_mask);
//      sa.sa_flags=SA_SIGINFO;

        while(sigaction(SIGRTMAX,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
        printf("Process PID: %d\n", getpid());
    printf("Waiting for SIGRTMAX (send it using: `kill -SIGRTMAX %d` or `sigqueue`)...\n", getpid());

//printf("Installed SIGWINCH handler");
//printf("Program is running. Press Ctrl+T to send SIGINFO.\n");


    // Keep the process alive to await signals
    while (1) {
 pause();
    }


        return EXIT_SUCCESS;
}

//Write a program to handle the SIGABRT signal (abort)
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
void signahandle()
{
        char s[100]="Received SIGabrt — exiting now.\n";
        //int len=snprintf(s,sizeof(s),"sigsegadr%p  signal=%d",info->si_addr,sig);
        write(STDOUT_FILENO,s,strlen(s)-1);
        _exit(EXIT_SUCCESS);
}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        while(sigaction(SIGABRT,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
        printf("install sSIGABRT");
        abort();//raises SIGABRT and invokes handler, then exits
        printf("vnever exucut");

        return EXIT_SUCCESS;
}

//Create a C program to handle the SIGSEGV_SIGBUS signal (segmentation fault or bus
//error).
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
#include<sys/ioctl.h>
void signahandle(int sig,siginfo_t *info,void *con)
{
        const char*signame;
        switch(sig)
        {
case SIGSEGV:signame="sigsegv";break;
case SIGBUS:signame="sigbus";break;
default:signame="invalid";break;
        }
        printf("catch signal%s \n", signame);
printf("Signal sent by PID: %p\n", info->si_addr);
    printf("terminating");

 exit(EXIT_FAILURE);  // Safely exit
}
int main()
{
        struct sigaction sa;
        sa.sa_flags=SA_SIGINFO;

        sa.sa_sigaction=signahandle;
        sigemptyset(&sa.sa_mask);
//      sa.sa_flags=SA_SIGINFO;
        if(sigaction(SIGSEGV,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
if(sigaction(SIGBUS,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
        int ch;
printf("1:sigsegv\n2:sigbus3\n:3:invalid\n");
        printf("enter choioce\n");
        scanf("%d",&ch);
        if(ch==1)
        {
                printf("trigger sigsegv");
                int *ptr=NULL;
                *ptr=10;
        }
        else if(ch==2)
        {
                printf("trigger sigbus");
                int *ptr[10];
                int *mis=(int *)(ptr+1);
                *mis=1234;
        }
        else
        {
                printf("invalid");
        }




    // Keep the process alive to await signals
    while (1) {
        pause();
    }

return EXIT_SUCCESS;
}
/25. Implement a program to handle the SIGUSR1_SIGUSR2 signal (user-defined sig//nal).
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
#include<sys/ioctl.h>
void signahandle(int sig,siginfo_t *info,void *con)
{
        if(sig==SIGUSR1)
        {
                printf("cautch sigusr1\n");
        }
        else if(sig==SIGUSR2)
        {
                printf("cautch sigusr2\n");
        }
        else
        {
                printf("undefined signal\n" );
        }
printf("sent pid %d\n",info->si_pid);


}
int main()
{
        struct sigaction sa;
        sa.sa_sigaction=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        if(sigaction(SIGUSR1,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
if(sigaction(SIGUSR2,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }


printf("process pid %d\n",getpid());
printf("waiting for sigusr1 and sigusr2");

    // Keep the process alive to await signals
    while (1) {
        pause();
    }


        return EXIT_SUCCESS;
}

//Create a C program to handle the SIGCONT_SIGSTOP signal (continue or stop
//executing).
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
#include<sys/ioctl.h>
void signahandle(int sig)
{
printf("catch sig continue\n");

}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags=0;
        if(sigaction(SIGCONT,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
printf("Process PID: %d\n", getpid());
    printf("You can stop this process using: kill -STOP %d\n", getpid());
    printf("And resume it using: kill -CONT %d\n", getpid());

    while (1) {
        printf("Running... (press Ctrl+Z or send SIGSTOP/SIGCONT externally)\n");
        sleep(5);
    }



        return EXIT_SUCCESS;
}
//Write a C program to catch and handle the SIGSEGV signal.
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
void signahandle(int signum)
{
        printf("Caught signal0 %d (SIGSEGV). Segmentation fault occurred.\n", signum);
    // You can add more cleanup or diagnostic information here if needed.
    exit(1);  // Exit the program after handling the signal
}
int main()
{
        signal(SIGSEGV,signahandle);
        printf("Cause Segmentation fault occurred.\n");
    // You can add more cleanup or diagnostic information here if needed.
    //exit(1);  // Exit the program after handling the signal
        int *p=NULL;
        *p=40;
        printf("vnever exucute%d",*p);

        return EXIT_SUCCESS;
}

//Write a program to block the SIGTERM signal using sigprocmask()
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
int main()
{
        sigset_t blockmask,oldmask;
        sigemptyset(&blockmask);
        sigaddset(&blockmask,SIGTERM);
while(sigprocmask(SIG_BLOCK,&blockmask,&oldmask)==-1)
{
perror("error blocked");
return 1;
}
printf("blocked signal%d\n",getpid());
sleep(2);
while(sigprocmask(SIG_SETMASK,&oldmask,NULL)==-1)
{
        perror("error unblocked");
        return 1;
}
printf("unblocked\n");
}
~              //9. Write a program to implement a timer using signals.
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<signal.h>
#include<sys/time.h>
#include<string.h>
static int tick;
void handlealrm()
{
        char buf[100];
        int n=snprintf(buf,sizeof(buf),"%d",++tick);
        write(STDOUT_FILENO,buf,n);
}
int main()
{
        struct sigaction sa;
        struct itimerval timer;
        memset(&sa,0,sizeof(sa));
        sa.sa_handler=handlealrm;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags;
        while(sigaction(SIGALRM,&sa,NULL)==-1)
        {
                perror("in alam");
                return 1;
        }
        //timerset every 1 sec
        timer.it_value.tv_sec=1;
        timer.it_value.tv_usec=0;
        timer.it_interval.tv_sec=1;
        timer.it_interval.tv_usec=0;
        while(setitimer(ITIMER_REAL,&timer,NULL)==-1)
        {
                perror("timererrror");
                return 1;
        }
rintf("timer started ctrl+c");
while(1)
{
        pause();
}
}
/30. Write a program to handle a real-time signal using sigqueue()
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<signal.h>
#include<sys/time.h>
#include<string.h>
static int tick;
void handlealrm()
{
        char buf[100];
        int n=snprintf(buf,sizeof(buf),"%d",++tick);
        write(STDOUT_FILENO,buf,n);
}
int main()
{
        struct sigaction sa;
        struct itimerval timer;
        memset(&sa,0,sizeof(sa));
        sa.sa_handler=handlealrm;
        sigemptyset(&sa.sa_mask);
        sa.sa_flags;
        while(sigaction(SIGALRM,&sa,NULL)==-1)
        {
                perror("in alam");
                return 1;
        }
        //timerset every 1 sec
        timer.it_value.tv_sec=1;
        timer.it_value.tv_usec=0;
        timer.it_interval.tv_sec=1;
        timer.it_interval.tv_usec=0;
        while(setitimer(ITIMER_REAL,&timer,NULL)==-1)
        {
                perror("timererrror");
                return 1;
        }
printf("timer started ctrl+c");
while(1)
{
        pause();
}
}
/Why we use raise system call explain it programmatically
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<signal.h>
#include<string.h>
#include<sys/ioctl.h>
volatile sig_atomic_t caught=0;
void signahandle(int sig)
{
//perror("error raise");
caught=sig;

}
int main()
{
        struct sigaction sa;
        sa.sa_handler=signahandle;
        sigemptyset(&sa.sa_mask);
        //sa.sa_flags=0;
        if(sigaction(SIGINT,&sa,NULL)==-1)
        {
                perror("errorr");
                return 1;
        }
printf("sig raise");
if(raise(SIGINT)!=0)
{
        perror("raise");
        return 1;
}
if(caught)

        printf("handle run");
        else
        printf("handle not run");
        return EXIT_SUCCESS;
}//Write a program to handle SIGALRM (alarm clock) signal for implementing a
//timeout mechanism in system progra
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>

// Signal handler for SIGALRM
void handle_alarm(int sig) {
    printf("\nTimeout! No input received.\n");
    exit(1); // Exit the program after timeout
}

int main() {
    char input[100];

    // Set the signal handler for SIGALRM
    signal(SIGALRM, handle_alarm);

    // Set alarm for 5 seconds
    alarm(5);

    printf("You have 5 seconds to enter your name: ");
    fflush(stdout); // Ensure prompt is printed

    // Wait for user input
    if (fgets(input, sizeof(input), stdin) != NULL) {
        // Cancel alarm if input is received in time
        alarm(0);
        printf("Hello, %s", input);
    }

    return 0;
}
//Write a c program on pause system call
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>

// Signal handler for SIGUSR1
void handle_signal(int sig) {
    if (sig == SIGUSR1) {
        printf("Received SIGUSR1 signal. Resuming execution.\n");
    }
}

int main() {
    // Register signal handler
    signal(SIGUSR1, handle_signal);

    printf("Process ID: %d\n", getpid());
    printf("Waiting for SIGUSR1 signal using pause()...\n");

    // Pause until a signal is received
    pause();

    printf("pause() returned. Program exiting.\n");

    return 0;
}

//Write a program on watch dog timer and it explain its working
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>

// Watchdog timeout duration (in seconds)
#define WATCHDOG_TIMEOUT 5

// Watchdog signal handler
void watchdog_handler(int signum) {
    printf("\n[WATCHDOG] Timeout! No heartbeat received.\n");
    printf("[WATCHDOG] Taking corrective action (exiting program).\n");
    exit(1);  // Simulate system reset or crash recovery
}

// Function to reset watchdog timer
void reset_watchdog() {
    alarm(WATCHDOG_TIMEOUT);  // Reset the timer
}

int main() {
    // Register signal handler for watchdog timeout (SIGALRM)
    signal(SIGALRM, watchdog_handler);

    printf("Starting main program. Watchdog is monitoring...\n");
    reset_watchdog();  // Start watchdog

    for (int i = 0; i < 10; i++) {
        printf("Iteration %d: Program is alive.\n", i + 1);

        if (i == 5) {
            // Simulate program hang or freeze (no watchdog reset)
            printf("Simulating program hang... watchdog will trigger!\n");
            sleep(WATCHDOG_TIMEOUT + 2);  // Longer than watchdog timeout
        } else {
            sleep(1);
reset_watchdog();  // Feed/kick the watchdog
        }
    }

    printf("Program completed without watchdog timeout.\n");
    return 0;
}

//Write a program to demonstrate signal handling in a multithreaded environment.
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>
#include <signal.h>

// Function run by worker threads
void* worker_thread(void* arg) {
    int thread_num = *(int*)arg;
    while (1) {
        printf("Worker thread %d is working...\n", thread_num);
        sleep(2); // Simulate work
    }
    return NULL;
}

// Signal-handling thread
void* signal_handler_thread(void* arg) {
    sigset_t *set = (sigset_t*)arg;
    int sig;

    printf("Signal handler thread started. Waiting for signals...\n");

    while (1) {
        if (sigwait(set, &sig) == 0) {
            if (sig == SIGINT) {
                printf("Signal handler thread: Caught SIGINT (Ctrl+C). Cleaning up and exiting.\n");
                exit(0);
            } else {
                printf("Signal handler thread: Received unexpected signal %d\n", sig);
            }
        } else {
            perror("sigwait failed");
        }
    }
    return NULL;
}

int main() {
    pthread_t workers[2];
    pthread_t sig_thread;
    sigset_t set;

    // Block SIGINT in all threads (will be handled by signal thread only)
    sigemptyset(&set);
    sigaddset(&set, SIGINT);
    if (pthread_sigmask(SIG_BLOCK, &set, NULL) != 0) {
        perror("pthread_sigmask");
        exit(1);
    }

    // Create worker threads
    int t1 = 1, t2 = 2;
    pthread_create(&workers[0], NULL, worker_thread, &t1);
    pthread_create(&workers[1], NULL, worker_thread, &t2);

    // Create signal handling thread
    pthread_create(&sig_thread, NULL, signal_handler_thread, (void*)&set);

    // Wait for threads (will never return unless interrupted)
    pthread_join(workers[0], NULL);
    pthread_join(workers[1], NULL);
    pthread_join(sig_thread, NULL);

    return 0;
}
//Write a program to demonstrate IPC using signals.
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>
#include <sys/types.h>

// Signal handler in the child
void handle_signal(int sig) {
    if (sig == SIGUSR1) {
        printf("Child: Received SIGUSR1 from parent\n");
    } else if (sig == SIGUSR2) {
        printf("Child: Received SIGUSR2 from parent\n");
    }
}

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        perror("fork failed");
        exit(1);
    }

    if (pid == 0) {
        // Child process
        printf("Child: PID = %d, waiting for signals...\n", getpid());

        // Register signal handlers
        signal(SIGUSR1, handle_signal);
        signal(SIGUSR2, handle_signal);

        // Infinite loop to keep the child alive
        while (1) {
            pause(); // Wait for signal
        }
    } else {
/ Parent process
        printf("Parent: Sending signals to child PID = %d\n", pid);

        sleep(2);
        kill(pid, SIGUSR1);

        sleep(2);
        kill(pid, SIGUSR2);

        sleep(2);
        printf("Parent: Exiting now.\n");
        kill(pid, SIGKILL); // Stop child after demo
    }

    return 0;
}



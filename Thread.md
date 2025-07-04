#THREADS
```c
/write a C program to create a thread that prints "Hello, World!"?
#include<stdio.h>
#include<pthread.h>
void *print(void *arg)
{
        printf("hello world\n");
        return NULL;
}
int main()
{
        pthread_t threadid;
        if(pthread_create(&threadid,NULL,print,NULL)!=0)
        {
                perror("thread error");
                return 1;
        }
        pthread_join(threadid,NULL);
}
//Modify the above program to create multiple threads, each printing its own message?
#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>
#define n 5
void *print(void *arg)
{
        int numthreads=*((int *)arg);
        printf("numofthreads%d\n",numthreads);
        free(arg);
        return NULL;
}
int main()
{
        pthread_t nthread[n];
        int i;
        for(i=0;i<n;i++)
        {
                int *numthread=malloc(sizeof(int));
                *numthread=(i+1);
                if(pthread_create(&nthread[i],NULL,print,numthread)!=0)
                {
                        perror("error thraed");
                        return 1;
                }
        }
        for(i=0;i<n;i++)
        {
                pthread_join(nthread[i],NULL);
        }

}
//Develop a C program to create two threads that print numbers from 1 to 10 concurrently?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        int num=*((int *)arg);
        for(int i=1;i<=10;i++)
        {
        printf("%d %d\n",i,num);
        }
        sleep(1000);
}
int main()
{
        pthread_t thread1;
        pthread_t thread2;
        int id1=1,id2=2;
        pthread_create(&thread1,NULL,print,&id1);
        pthread_create(&thread2,NULL,print,&id2);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        pthread_join(thread2,NULL);
}
/Implement a C program to create a thread that calculates the factorial of a given number?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        int num=*((int *)arg);
        int fact=1;
        while(num)
        {
                fact=fact*num;
                num--;
        }
        printf("fact=%d",fact);
}
int main()
{
        pthread_t thread1;
        int n=5;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
//Write a C program to create two threads that print their thread IDs?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        pthread_t id=pthread_self();//get current thread id
        printf("thread ids:%lu\n",(unsigned long)id);

}
int main()
{
        pthread_t thread1;
        pthread_t thread2;
        pthread_create(&thread1,NULL,print,NULL);
        pthread_create(&thread2,NULL,print,NULL);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        pthread_join(thread2,NULL);
}
//6.Develop a C program to create a thread that prints the sum of two numbers?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
typedef struct
{
        int a;
        int b;
}numbers;
void *print(void *arg)
{
        numbers *num=(numbers*)arg;
        int sum=num->a+num->b;
        printf("%d %d %d",num->a,num->b,sum);
}
int main()
{
        pthread_t thread1;
         numbers *num=malloc(sizeof(numbers));
         num->a=10;
         num->b=20;
        pthread_create(&thread1,NULL,print,num);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        free(num);
}

//Implement a C program to create a thread that calculates the square of a number?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        int num=*((int *)arg);
        int res=num*num;
        printf("%d",res);
}
int main()
{
        pthread_t thread1;
        int n=5;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
//Write a C program to create a thread that prints the current date and time?
#include<stdio.h>
#include<pthread.h>
#include<time.h>
void *print(void *arg)
{
        time_t now;
        struct tm *timeinfo;
        time(&now);
        timeinfo=localtime(&now);
        printf("current time=%s",asctime(timeinfo));
}
int main()
{
        pthread_t thread;
        pthread_create(&thread,NULL,print,NULL);
        pthread_join(thread,NULL);
}
//.Develop a C program to create a thread that checks if a number is prime?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        int cnt=0;
        int num=*((int *)arg);
        for(int i=1;i<=num;i++)
        {
                if(num%i==0)
                {
                        cnt++;
                }
        }
        if(cnt==2)
        {
        printf("prime");
        }
        else
        {
                printf("not");
        }

}
int main()
{
        pthread_t thread1;
        int n=4;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
//10.Implement a C program to create a thread that checks if a given string is a palindrome?
#include<stdio.h>
#include<pthread.h>
#include<string.h>
void *print(void *arg)
{
        char *p=(char *)arg;
        int i=0;
        int j=strlen(p)-1;
        while(i<j)
        {
                if(p[i]!=p[j])
                {
                        printf("not polynidrome");
                        return NULL;
                }
                i++;
                j--;
        }
        printf("polyndrome");
        return NULL;
}
int main()
{
        pthread_t threadid;
        char s[100]="meaam";
        if(pthread_create(&threadid,NULL,print,s)!=0)
        {
                perror("thread error");
                return 1;
        }
        pthread_join(threadid,NULL);
}

//11.Write a C program to create a thread that prints "Hello, World!" with thread
//synchronization?
#include<stdio.h>
#include<pthread.h>
//create mutex
pthread_mutex_t lock;
void *print(void *arg)
{
        pthread_mutex_lock(&lock);
        printf("hello world\n");
        pthread_mutex_unlock(&lock);
        return NULL;
}
int main()
{
        pthread_t threadid;
        //init mutex;
        pthread_mutex_init(&lock,NULL);
        if(pthread_create(&threadid,NULL,print,NULL)!=0)
        {
                perror("thread error");
                return 1;
        }
        pthread_join(th//2.Develop a C program to create two threads that print their thread IDs and synchronize their
//output?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
//creating mutex
pthread_mutex_t lock;
void *print(void *arg)
{
        pthread_mutex_lock(&lock);
        pthread_t id=pthread_self();//get current thread id
        printf("thread ids:%lu\n",(unsigned long)id);
        pthread_mutex_unlock(&lock);

}
int main()
{
        pthread_t thread1;
        pthread_t thread2;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread1,NULL,print,NULL);
        pthread_create(&thread2,NULL,print,NULL);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        pthread_join(thread2,NULL);
        pthread_mutex_destroy(&lock);
}

readid,NULL);
        pthread_mutex_destroy(&lock);

}
//3.Implement a C program to create a thread that generates random numbers and
//synchronizes access to a shared buffer?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
#include<time.h>
#define size 10
int buf[size];
int Index=0;
//creating mutex
pthread_mutex_t lock;
void *print(void *arg)
{
        srand(time(NULL));
        for(int i=0;i<size;i++)
        {
        pthread_mutex_lock(&lock);
        int num=rand()%100;
                buf[Index++]=num;
        printf("num=%d\n",num);


        pthread_mutex_unlock(&lock);
        usleep(100);
        }
        return NULL;

}
int main()
{
        pthread_t thread1;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread1,NULL,print,NULL);
        //wait for threads to complte
        pthread_join(thread1,NULL);
for(int i=0;i<size;i++)
        {
                printf("buf=%d",buf[i]);
        }
        pthread_mutex_destroy(&lock);
}

//14.Write a C program to create a thread that performs addition of two numbers with mutex
//locks?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
pthread_mutex_t lock;
typedef struct
{
        int a;
        int b;
}numbers;
void *print(void *arg)
{

        numbers *num=(numbers*)arg;
        pthread_mutex_lock(&lock);
        int sum=num->a+num->b;
        printf("%d\n %d\n %d\n",num->a,num->b,sum);
        pthread_mutex_unlock(&lock);
        return NULL;
}
int main()
{
        pthread_t thread1;
        pthread_mutex_init(&lock,NULL);
         numbers *num=malloc(sizeof(numbers));
         num->a=10;
         num->b=20;
        pthread_create(&thread1,NULL,print,num);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        free(num);
        pthread_mutex_destroy(&lock);
        return 0;
}
//15.Implement a C program to create two threads that increment and decrement a shared
//variable, respectively, using mutex locks?
#include<stdio.h>
#include<pthread.h>
int shared_var=0;
pthread_mutex_t lock;//mutex for synchronisation
void *inc(void *arg)
{
        for(int i=0;i<5;i++)
        {
                pthread_mutex_lock(&lock);
                shared_var++;
                printf("inc thread:sharedvar%d\n",shared_var);
                pthread_mutex_unlock(&lock);
        }
        return NULL;
}
void *dec(void *arg)
{
        for(int i=0;i<5;i++)
        {
                pthread_mutex_lock(&lock);
                shared_var--;
                printf("dec thread:sharedvar%d\n",shared_var);
                pthread_mutex_unlock(&lock);
        }
        return NULL;
}
int main()
{
        pthread_t incthread;
        pthread_t decthread;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&incthread,NULL,inc,NULL);
        pthread_create(&decthread,NULL,dec,NULL);
        pthread_join(incthread,NULL);
        pthread_join(decthread,NULL);
printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        return 0;
}

//16.Develop a C program to create a thread that reads input from the user and synchronizes
//access to shared resources?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
pthread_mutex_t lock;
#define maxl 100
char shared[maxl];
void *userinput(void *arg)
{


        pthread_mutex_lock(&lock);
        printf("enterinput");
        fgets(shared,maxl,stdin);
        printf("userinput%s",shared);
        pthread_mutex_unlock(&lock);
        return NULL;
}
int main()
{
        pthread_t thread1;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread1,NULL,userinput,NULL);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        printf("mainthread see%s",shared);
        pthread_mutex_destroy(&lock);
        return 0;
}
//17.Implement a C program to create a thread that prints prime numbers up to a given limit
//with mutex locks?
#include<stdio.h>
#include<pthread.h>
pthread_mutex_t lock;//mutex for synchronisation
void *rangeprime(void *arg)
{
        for(int n=2;n<10;n++)
        {
         int cnt=0;
        for(int i=1;i<=n;i++)
        {
                if(n%i==0)
                {
                        cnt++;

                }
        }
                if(cnt==2)
                {
                pthread_mutex_lock(&lock);

                printf("prime%d\n",n);
               pthread_mutex_unlock(&lock);
        }
        }
        return NULL;
}
int main()
{
        pthread_t thread;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread,NULL,rangeprime,NULL);
        pthread_join(thread,NULL);
//      printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        return 0;
}

//8.Implement a C program to create a thread that calculates the sum of Fibonacci numbers up
//to a given limit using dynamic programming with mutex locks?

#include<stdio.h>
#include<pthread.h>
pthread_mutex_t lock;//mutex for synchronisation
void *rangefib(void *arg)
{
        int a=0,b=1;
        for(int n=1;n<10;n++)
        {
                int c=a+b;
         a=b;
          b=c;
                pthread_mutex_lock(&lock);

                printf("fib%d\n",c);
               pthread_mutex_unlock(&lock);
        }

        return NULL;
}
int main()
{
        pthread_t thread;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread,NULL,rangefib,NULL);
        pthread_join(thread,NULL);
//      printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        return 0;
}

//Write a C program to create a thread that checks if a given year is a leap year using
//dynamic programming with mutex locks?

#include<stdio.h>
#include<pthread.h>
pthread_mutex_t lock;//mutex for synchronisation
typedef struct
{
        int year;
}input;
void *leap(void *arg)
{
input *in=(input*)arg;
int res=in->year;
int leap=(res%400==0)||(res%100!=0&&res%4==0);
                pthread_mutex_lock(&lock);
        printf("%d leap year=%s",res,leap?"leap year":"not leap");


               pthread_mutex_unlock(&lock);

        return NULL;
}
int main()
{
        pthread_t thread;
        input n1={.year=2001};
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread,NULL,leap,&n1);
        pthread_join(thread,NULL);
//      printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        return 0;
}
//Write a C program to create a thread that checks if a given string is a palindrome using
//dynamic programming with mutex locks?

#include<stdio.h>
#include<pthread.h>
#include<string.h>
#include<stdbool.h>
#define maxl 100
bool computed[maxl][maxl];
bool dp[maxl][maxl];
pthread_mutex_t lock;//mutex for synchronisation
typedef struct
{
        char str[maxl];
}input;
void *poly(void *arg)
{
input *in=(input*)arg;
char *s=in->str;
int n=strlen(s)-1;
for (int i = n - 1; i >= 0; i--) {
        for (int j = i; j < n; j++) {
            pthread_mutex_lock(&lock);
            if (!computed[i][j]) {
                dp[i][j] = (s[i] == s[j]) && (j - i < 2 || dp[i+1][j-1]);
                computed[i][j] = true;
                // Only print once, for full string
                if (i == 0 && j == n - 1) {
                    printf("Thread: \"%s\" is %sa palindrome.\n",
                        s, dp[i][j] ? "" : "NOT ");
                }
            }
 pthread_mutex_unlock(&lock);
        }
}
return NULL;
}
int main()
{
        pthread_t thread;
        input Input;
    printf("Enter a string: ");
    fgets(Input.str, maxl, stdin);
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread,NULL,poly,&Input);
        pthread_join(thread,NULL);
//      printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        return 0;
}
//21.Implement a C program to create a thread that performs selection sort on an array of
//integers?
#include<stdio.h>
#include<pthread.h>
#define size 10
int a[size]={1,2,3,5,0,3,7,9,2};
void *sort(void *arg)
{
        for(int i=0;i<size-1;i++)
        {
                int minj=i;
                for(int j=i+1;j<size-1;j++)
                {
                        if(a[j]<a[minj])
                        {
                                minj=j;
                        }
                }
                int temp=a[i];
                a[i]=a[minj];
                a[minj]=temp;
        }

        return NULL;
}

int main()
{
        pthread_t thread;
        pthread_create(&thread,NULL,sort,NULL);
        pthread_join(thread,NULL);
        for(int i=0;i<size-1;i++)
        {
                printf("%d ",a[i]);
        }
}
//22.Develop a C program to create a thread that calculates the area of a triangle?

#include<stdio.h>
#include<pthread.h>
float res;
typedef struct
{
        float len;
        float b;
}area;
void *leap(void *arg)
{
area *in=(area*)arg;
res=0.5*(in->len*in->b);


        return NULL;
}
int main()
{
        pthread_t thread;
        area b1;
printf("enterlen and breath");
scanf("%f%f",&b1.b,&b1.len);
        pthread_create(&thread,NULL,leap,&b1);
        pthread_join(thread,NULL);
        printf("final value shered%f",res);

        return 0;
}

//23.Write a C program to create a thread that calculates the sum of squares of numbers from 1
//to 100?

#include<stdio.h>
#include<pthread.h>
#define size 100
int sum;
void *sumsquare(void *arg)
{
for(int i=1;i<=size;i++)
{
        sum=sum+(i*i);
}


        return NULL;
}
int main()
{
        pthread_t thread;
        pthread_create(&thread,NULL,sumsquare,NULL);
        pthread_join(thread,NULL);
        printf("final value shered%d",sum);

        return 0;
}
//24.Write a C program to create a thread that generates a random array of integers?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
#include<time.h>
#define size 10
int buf[size];
int Index=0;
//creating mutex
pthread_mutex_t lock;
void *print(void *arg)
{
        srand(time(NULL));
        for(int i=0;i<size;i++)
        {
        pthread_mutex_lock(&lock);
        int num=rand()%100;
                buf[Index++]=num;
        printf("num=%d\n",num);


        pthread_mutex_unlock(&lock);
        usleep(100);
        }
        return NULL;

}
int main()
{
        pthread_t thread1;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread1,NULL,print,NULL);
        //wait for threads to complte
        pthread_join(thread1,NULL);

        for(int i=0;i<size;i++)
{
                printf("buf=%d",buf[i]);
        }
        pthread_mutex_destroy(&lock);
}
/25.Implement a C program to create a thread that performs bubble sort on an array of
//integers?
#include<stdio.h>
#include<pthread.h>
#define size 10
int a[size]={1,2,3,5,0,3,7,9,2,10};
void *sort(void *arg)
{
        for(int i=0;i<size;i++)
        {
                for(int j=0;j<size-i-1;j++)
                {
                        if(a[j]>a[j+1])
                        {
                int temp=a[j];
                a[j]=a[j+1];
                a[j+1]=temp;
        }
                }
        }
        return NULL;
}

int main()
{
        pthread_t thread;
        pthread_create(&thread,NULL,sort,NULL);
        pthread_join(thread,NULL);
        for(int i=0;i<size;i++)
        {
                printf("%d ",a[i]);
        }
}

/6.Develop a C program to create a thread that calculates the greatest common divisor (GCD)
//of two numbers?
#include<stdio.h>
#include<pthread.h>
#include<stdlib.h>
int gcdres=0;
int a=98;
int b=56;
int gcd(int x,int y)
{
        while(y!=0)
        {
                int t=y;
                y=x%y;
                x=t;
        }
        return x;
}
void *gcdnum(void *arg)
{
        gcdres=gcd(a,b);
        return NULL;
}
int main()
{
        pthread_t thread;
        pthread_create(&thread,NULL,gcdnum,NULL);
        pthread_join(thread,NULL);
        printf("gcd:%d",gcdres);
        return 0;
}
~              
/7.Write a C program to create a thread that calculates the sum of Fibonacci numbers up to a
//given limit?

#include<stdio.h>
#include<pthread.h>

pthread_mutex_t lock;//mutex for synchronisation
void *rangefib(void *arg)
{
        int a=0,b=1;
        for(int n=1;n<10;n++)
        {
                int c=a+b;
         a=b;
          b=c;
                pthread_mutex_lock(&lock);

                printf("%d\n",c);
               pthread_mutex_unlock(&lock);
        }

        return NULL;
}
int main()
{
        pthread_t thread;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread,NULL,rangefib,NULL);
        pthread_join(thread,NULL);
//printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        return 0;
}

/8.Implement a C program to create a thread that calculates the sum of even numbers from 1
//to 100?

#include<stdio.h>
#include<pthread.h>
#define max 100
int shared_sum=0;
pthread_mutex_t lock;
void *sumeven(void *arg)
{
        for(int i=2;i<=max;i=i+2)
        {
                pthread_mutex_lock(&lock);
shared_sum=shared_sum+i;
printf("shared_sum%d\n",shared_sum);
               pthread_mutex_unlock(&lock);
        }

        return NULL;
}
int main()
{
        pthread_t thread;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread,NULL,sumeven,NULL);
        pthread_join(thread,NULL);
printf("final value shered%d",shared_sum);
        pthread_mutex_destroy(&lock);
        return 0;
}

//29.Develop a C program to create a thread that calculates the factorial of a given number
//using iteration?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
pthread_mutex_t lock;
int res=0;
void *print(void *arg)
{
        int n=*((int *)arg);
        int fact=1;
        for(int i=1;i<=n;i++)
        {
                fact=fact*i;

        }
        pthread_mutex_lock(&lock);
        res=fact;
        pthread_mutex_unlock(&lock);
        return NULL;
}
int main()
{
        pthread_t thread1;
        pthread_mutex_init(&lock,NULL);
        int n=5;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        printf("finarsult%d=",res);
        pthread_mutex_destroy(&lock);
        return 0;
}
//Write a C program to create a thread that checks if a given year is a leap year using
//dynamic programming with mutex locks?

#include<stdio.h>
#include<pthread.h>
pthread_mutex_t lock;//mutex for synchronisation
typedef struct
{
        int year;
}input;
void *leap(void *arg)
{
input *in=(input*)arg;
int res=in->year;
int leap=(res%400==0)||(res%100!=0&&res%4==0);
                pthread_mutex_lock(&lock);
        printf("%d leap year=%s",res,leap?"leap year":"not leap");


               pthread_mutex_unlock(&lock);

        return NULL;
}
int main()
{
        pthread_t thread;
        input n1={.year=2001};
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread,NULL,leap,&n1);
        pthread_join(thread,NULL);
//      printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        return 0;
}

//31.Implement a C program to create a thread that performs multiplication of two matrices?

#include<stdio.h>
#include<pthread.h>
#include<stdlib.h>
#define max 2
int a[max][max]={{1,2},{3,4}};
int b[max][max]={{3,4},{5,6}};
int c1[max][max]={0};
pthread_mutex_t lock= PTHREAD_MUTEX_INITIALIZER;;//mutex for synchronisation
typedef struct
{
        int row;
        int col;
}mat;
void *mul(void *arg)
{
        mat *in=(mat*)arg;
        int r=in->row;
        int c=in->col;
        int sum=0;
        for(int k=0;k<max;k++)
        {
                sum=sum+a[r][k]*b[k][c];
        }
pthread_mutex_lock(&lock);
c1[in->row][in->col]=sum;
pthread_mutex_unlock(&lock);
        free(in);
        return NULL;
}
int main()
{
        pthread_t thread[max*max];
        int id=0;
        pthread_mutex_init(&lock,NULL);
for(int i=0;i<max;i++)
        {
                for(int j=0;j<max;j++)
                {
                        mat *arg=malloc(sizeof(mat));
                        arg->row=i;
                        arg->col=j;



        pthread_create(&thread[id++],NULL,mul,arg);
                }
        }
        for(int i=0;i<id;i++)
        {
        pthread_join(thread[i],NULL);
        }
        for(int i=0;i<max;i++)
        {
for(int j=0;j<max;j++)
{

        printf("final value shered%d ",c1[i][j]);
        }
printf("\n");
}
        pthread_mutex_destroy(&lock);
        return 0;
}

/32.Develop a C program to create a thread that calculates the average of numbers from 1 to
//100?

#include<stdio.h>
#include<pthread.h>
#define num 100
double average=0.0;
pthread_mutex_t lock;//mutex for synchronisation

void *avg(void *arg)
{
        long long sum=0;

for(int i=1;i<=num;i++)
{
         sum=sum+i;
}
double average1=(double)sum/num;
                pthread_mutex_lock(&lock);
        average=average1;


               pthread_mutex_unlock(&lock);

        return NULL;
}
int main()
{
        pthread_t thread;

        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread,NULL,avg,NULL);
        pthread_join(thread,NULL);
printf("final value shered%.2f",average);
        pthread_mutex_destroy(&lock);
        return 0;
}
        /Implement a C program to create a thread that generates a random string?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
#include<string.h>
#include<time.h>
#define size 10
void *randstr(void *arg)
{
        char *str=(char *)malloc(size*sizeof(char));
        if(str==NULL)
        {
                perror("memory failed");
        }
        const char set[]="avulalaxmivasuboinaammu";
                srand(time(NULL)^pthread_self());
                        for(int i=0;i<size;i++)
                        {
                                int key=rand()%(int)sizeof(set)-1;
                                str[i]=set[key];
                        }
                        printf("randomstring%s:",str);
                        free(str);




}
int main()
{
        pthread_t thread1;
        pthread_create(&thread1,NULL,randstr,NULL);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
/Write a C program to create a thread that checks if a given number is a perfect square?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
#include<string.h>
#include<time.h>
#include<math.h>
void *persquare(void *arg)
{
        int num=*((int*)arg);
        int res=sqrt(num);
        if(res*res==num)
        {
                printf("square ");
        }
        else
        {
                printf("not");
        }
        return NULL;




}
int main()
{
        pthread_t thread1;
        int num=48;
        pthread_create(&thread1,NULL,persquare,&num);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        return 0;
}

//Write a C program to create a thread that calculates the sum of digits of a given number?
#include<stdio.h>
#include<pthread.h>
#include<string.h>
void *printsum(void *arg)
{
        int num=*((int *)arg);
        int sum=0;
        while(num)
        {
                int r=num%10;
                sum=sum+r;
                num=num/10;
        }
        printf("sum=%d\n",sum);
        return NULL;
}
int main()
{
        pthread_t threadid;
        int n=12345;
        if(pthread_create(&threadid,NULL,printsum,&n)!=0)
        {
                perror("thread error");
                return 1;
        }
        pthread_join(threadid,NULL);
}
//6.Implement a C program to create a thread that calculates the factorial of a given number
//using recursion?
#include<stdio.h>
#include<pthread.h>
#include<string.h>
int recfact(int n)
{
        if(n==0||n==1)
{
        return 1;
}
return n*recfact(n-1);
}


void *print(void *arg)
{
        int n=*((int *)arg);
        if(n<0)
        {
                printf("neg");
        }
        else
        {
                int res=recfact(n);
                printf("%d:",res);
        }
}
int main()
{
        pthread_t threadid;
        int n=5;
        if(pthread_create(&threadid,NULL,print,&n)!=0)
        {
                perror("thread error");
                return 1;
 }
        pthread_join(threadid,NULL);
}
//37.Develop a C program to create a thread that finds the maximum element in an array
#include<stdio.h>
#include<pthread.h>
#include<string.h>
#include<stdlib.h>
//#define size 10
typedef struct{
        int *a;
        int size;
}aray;


void *maxi(void *arg)
{
aray *n=(aray*)arg;
int *b=n->a;
int n1=n->size;
int max=b[0];
for(int i=0;i<n1;i++)
{
        if(b[i]>max)
        {
                max=b[i];
        }
}

printf("max=%d",max);
return NULL;
}
int main()
{
        pthread_t threadid;
        int a1[]={1,5,6,2,3};
        int size=sizeof(a1)/sizeof(a1[0]);
        aray *arg = (aray *)malloc(sizeof(aray));
//      aray *arg=malloc(sizeof(aray));
        arg->a=a1;
        arg->size=size;

        if(pthread_create(&threadid,NULL,maxi,arg)!=0)
        {
                perror("thread error");
                return 1;
        }
        pthread_join(threadid,NULL);
}

//Write a C program to create a thread that sorts an array of strings?
#include<stdio.h>
#include<pthread.h>
#include<stdlib.h>
#include<string.h>
typedef struct
{
        char **a;
        int size;
}sortchar;
void *sort(void *arg)
{
        sortchar *data=(sortchar*)arg;
        char **a=data->a;
        int size=data->size;
        for(int i=0;i<size;i++)
        {
                for(int j=0;j<size-i-1;j++)
                {

                        if(strcmp(a[j],a[j+1])>0)
                        {
                char *temp=a[j];
                a[j]=a[j+1];
                a[j+1]=temp;
        }
                }
        }
        return NULL;
}

int main()
{
        pthread_t thread;
        int n=3;
        char **a=malloc(n*sizeof(char*));
        printf("enterstrings");
for(int i=0;i<n;i++)
        {
               a[i]=malloc(100*sizeof(char));
                               fgets(a[i],100,stdin);
        }
        sortchar data={a,n};
        pthread_create(&thread,NULL,sort,&data);
        pthread_join(thread,NULL);
        for(int i=0;i<n;i++)
        {
                printf("%s",a[i]);
        }
}
//Implement a C program to create a thread that calculates the square of a number?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        int num=*((int *)arg);
        int res=num*num;
        printf("%d",res);
}
int main()
{
        pthread_t thread1;
        int n=5;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
//Develop a C program to create a thread that calculates the average of numbers in an array?

#include<stdio.h>
#include<pthread.h>
#include<stdlib.h>
#define num 100
double average=0.0;
typedef struct
{
        int *a;
        int n;
}avg;
void *avge(void *arg)
{
        avg *data=(avg*)arg;
        int *b=data->a;
        int n=data->n;
        long long sum=0;

for(int i=0;i<n;i++)
{
         sum=sum+b[i];
}
double average1=(double)sum/n;
        average=average1;

        return NULL;
}
int main()
{
        pthread_t thread;
        int n=5;
        int *a=malloc(n*sizeof(int));
        printf("enter elemnets");
        for(int i=0;i<n;i++)
        {
                scanf("%d",&a[i]);
}
        avg data;
        data.a=a;
        data.n=n;


        pthread_create(&thread,NULL,avge,&data);
        pthread_join(thread,NULL);
printf("final value shered%.2f",average);
        return 0;
}
//.Write a C program to create a thread that generates a random password??
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
#include<string.h>
#include<time.h>
#define size 10
void *randstr(void *arg)
{
        char *str=(char *)malloc(size*sizeof(char));
        if(str==NULL)
        {
                perror("memory failed");
        }
        const char set[]="avulalaxmivasuboinaammu";
                srand(time(NULL)^pthread_self());
                        for(int i=0;i<size;i++)
                        {
                                int key=rand()%(int)sizeof(set)-1;
                                str[i]=set[key];
                        }
                        printf("randomstring%s:",str);
                        free(str);




}
int main()
{
        pthread_t thread1;
        pthread_create(&thread1,NULL,randstr,NULL);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
/Implement a C program to create a thread that checks if a number is even or odd?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        int num=*((int *)arg);
        if(num%2==0)
        {
                printf("even");
        }
        else
        {
                printf("odd");
        }
return NULL;
}
int main()
{
        pthread_t thread1;
        int n=5;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        return 0;
}

//Implement a C program to create a thread that calculates sum of elemnets in arrayr?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
int sum;
typedef struct
{
        int *a;
        int n;
}ary;
void *print(void *arg)
{
        ary *data=(ary*)arg;
        int *b=data->a;
        int n1=data->n;
        for(int i=0;i<n1;i++)
        {
                sum=sum+b[i];
        }
        return NULL;
}
int main()
{
        pthread_t thread1;
        int n=5;
        int *a=malloc(n*sizeof(int));
        printf("enter elements");
        for(int i=0;i<n;i++)
        {
                scanf("%d",&a[i]);
        }
        ary data;
        data.a=a;
        data.n=n;
        pthread_create(&thread1,NULL,print,&data);
        //wait for threads to complte
pthread_join(thread1,NULL);
        printf("final%d=",sum);
}

/4.Write a C program to create a thread that calculates the factorial of numbers from 1 to 10?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        int num=*((int *)arg);
        int fact;
        for(int i=1;i<=num;i++)
        {
                 fact=1;
                 int temp=i;
        while(temp)
        {
                fact=fact*temp;
                temp--;
        }

        printf("fact=%d\n",fact);
        }
        return NULL;
}
int main()
{
        pthread_t thread1;
        int n=10;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
//22.Develop a C program to create a thread that calculates the area of a rectangle?

#include<stdio.h>
#include<pthread.h>
float res;
typedef struct
{
        float len;
        float b;
}area;
void *leap(void *arg)
{
area *in=(area*)arg;
res=(in->len*in->b);


        return NULL;
}
int main()
{
        pthread_t thread;
        area b1;
printf("enterlen and breath");
scanf("%f%f",&b1.b,&b1.len);
        pthread_create(&thread,NULL,leap,&b1);
        pthread_join(thread,NULL);
        printf("final value shered%f",res);

        return 0;
}
/3.Implement a C program to create a thread that generates random numbers and
//synchronizes access to a shared buffer?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
#include<time.h>
#define size 10
int buf[size];
int Index=0;
//creating mutex
pthread_mutex_t lock;
void *print(void *arg)
{
        srand(time(NULL));
        for(int i=0;i<size;i++)
        {
        pthread_mutex_lock(&lock);
        int num=rand()%100;
                buf[Index++]=num;
        printf("num=%d\n",num);


        pthread_mutex_unlock(&lock);
        usleep(100);
        }
        return NULL;

}
int main()
{
        pthread_t thread1;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread1,NULL,print,NULL);
        //wait for threads to complte
        pthread_join(thread1,NULL);
for(int i=0;i<size;i++)
        {
                printf("buf=%d",buf[i]);
        }
        pthread_mutex_destroy(&lock);
}
/25.Implement a C program to create a thread that performs sort on an array of
//integers?
#include<stdio.h>
#include<pthread.h>
#define size 10
int a[size]={1,2,3,5,0,3,7,9,2,10};
void *sort(void *arg)
{
        for(int i=0;i<size;i++)
        {
                for(int j=0;j<size-i-1;j++)
                {
                        if(a[j]>a[j+1])
                        {
                int temp=a[j];
                a[j]=a[j+1];
                a[j+1]=temp;
        }
                }
        }
        return NULL;
}

int main()
{
        pthread_t thread;
        pthread_create(&thread,NULL,sort,NULL);
        pthread_join(thread,NULL);
        for(int i=0;i<size;i++)
        {
                printf("%d ",a[i]);
        }
}
//48.Write a C program to create a thread that searches for a given number in an array?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
int sum;
typedef struct
{
        int *a;
        int n;
}ary;
void *print(void *arg)
{
        ary *data=(ary*)arg;
        int *b=data->a;
        int n1=data->n;
        int key=5;
        int flag;
        for(int i=0;i<n1;i++)
        {
                if(b[i]==key)
                {
                        flag=1;
                        break;
                }
        }
        if(flag==1){
                        printf("found");
        }
                else
                {
                        printf("not");
                }

        return NULL;
}
nt main()
{
        pthread_t thread1;
        int n=5;
        int *a=malloc(n*sizeof(int));
        printf("enter elements");
        for(int i=0;i<n;i++)
        {
                scanf("%d",&a[i]);
        }
        ary data;
        data.a=a;
        data.n=n;
        pthread_create(&thread1,NULL,print,&data);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        //printf("final%d=",sum);
}
//10.Implement a C program to create a thread that checks if a given string is a palindrome?
#include<stdio.h>
#include<pthread.h>
#include<string.h>
void *print(void *arg)
{
        char *p=(char *)arg;
        int i=0;
        int j=strlen(p)-1;
        while(i<j)
        {
        p[i]^=p[j];
        p[j]^=p[i];
        p[i]^=p[j];
        i++;
        j--;
        }
        printf("%s",p);
        return NULL;
}
/write a C program to create a thread that prints "Hello, World!"?
#include<stdio.h>
#include<pthread.h>
void *print(void *arg)
{
        char input[100];
        printf("enter string");
        fgets(input,100,stdin);
        printf("%s",input);
}
int main()
{
        pthread_t threadid;
        if(pthread_create(&threadid,NULL,print,NULL)!=0)
        {
                perror("thread error");
                return 1;
        }
        pthread_join(threadid,NULL);
}
//31.Implement a C program to create a thread that performs addition of two matrices?

#include<stdio.h>
#include<pthread.h>
#include<stdlib.h>
#define max 2
int a[max][max]={{1,2},{3,4}};
int b[max][max]={{3,4},{5,6}};
int c1[max][max]={0};
pthread_mutex_t lock= PTHREAD_MUTEX_INITIALIZER;;//mutex for synchronisation
typedef struct
{
        int row;
        int col;
}mat;
void *mul(void *arg)
{
        mat *in=(mat*)arg;
        int r=in->row;
        int c=in->col;
        int sum=0;
        for(int k=0;k<max;k++)
        {
                sum=sum+a[r][k]+b[k][c];
        }
pthread_mutex_lock(&lock);
c1[in->row][in->col]=sum;
pthread_mutex_unlock(&lock);
        free(in);
        return NULL;
}
int main()
{
        pthread_t thread[max*max];
        int id=0;
        pthread_mutex_init(&lock,NULL);

for(int i=0;i<max;i++)
        {
                for(int j=0;j<max;j++)
                {
                        mat *arg=malloc(sizeof(mat));
                        arg->row=i;
                        arg->col=j;



        pthread_create(&thread[id++],NULL,mul,arg);
                }
        }
        for(int i=0;i<id;i++)
        {
        pthread_join(thread[i],NULL);
        }
        for(int i=0;i<max;i++)
        {
for(int j=0;j<max;j++)
{

        printf("final value shered%d ",c1[i][j]);
        }
printf("\n");
}
        pthread_mutex_destroy(&lock);
        return 0;
}
/write a C program to create a thread that prints "Hello, World!"?
#include<stdio.h>
#include<pthread.h>
void *print(void *arg)
{
        char input[100];
        int cnt=0;
        printf("enter string");
        fgets(input,100,stdin);
        for(int i=0;input[i];i++)
        {
                cnt++;
        }
        printf("%d",cnt);
}
int main()
{
        pthread_t threadid;
        if(pthread_create(&threadid,NULL,print,NULL)!=0)
        {
                perror("thread error");
                return 1;
        }
        pthread_join(threadid,NULL);
}

//Write a C program to create two threads using pthreads library. Each thread should print
//"Hello, World!" along with its thread ID?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        pthread_t id=pthread_self();//get current thread id
        printf("hello world from thread ids:%lu\n",(unsigned long)id);

}
int main()
{
        pthread_t thread1;
        pthread_t thread2;
        pthread_create(&thread1,NULL,print,NULL);
        pthread_create(&thread2,NULL,print,NULL);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        pthread_join(thread2,NULL);
}
//Write a C program to create two threads using pthreads library. Each thread should print
//"Hello, World!" along with its thread ID?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        char *ms=(char*)arg;
        pthread_t id=pthread_self();//get current thread id
        printf("hello world from thread mesages:%s ids:%lu\n",ms,(unsigned long)id);

}
int main()
{
        pthread_t thread1;
        pthread_t thread2;
        char *msg1="hellothrea1";
        char *msg2="hellothread2";
        pthread_create(&thread1,NULL,print,msg1);
        pthread_create(&thread2,NULL,print,msg2);
        //wait for threads to complte
        pthread_join(thread1,NULL);
        pthread_join(thread2,NULL);
}
/Write a C program to demonstrate thread synchronization using mutex locks. Create two
//threads that increment a shared variable using mutex locks to ensure proper synchronization?
#include<stdio.h>
#include<pthread.h>
int shared_var=0;
pthread_mutex_t lock;//mutex for synchronisation
void *inc(void *arg)
{
        for(int i=0;i<5;i++)
        {
                pthread_mutex_lock(&lock);
                shared_var++;
                //printf("inc thread:sharedvar%d\n",shared_var);
                pthread_mutex_unlock(&lock);
        }
        return NULL;
}
int main()
{
        pthread_t incthread;
        pthread_t incthread1;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&incthread,NULL,inc,NULL);
        pthread_create(&incthread1,NULL,inc,NULL);
        pthread_join(incthread,NULL);
        pthread_join(incthread1,NULL);
        printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        return 0;
}

//6.Extend the previous program to use semaphore instead of mutex locks for thread
//synchronization?
#include<stdio.h>
#include<pthread.h>
#include<semaphore.h>
int shared_var=0;
sem_t sem;
//pthread_mutex_t lock;//mutex for synchronisation
void *inc(void *arg)
{
        for(int i=0;i<5;i++)
        {
                sem_wait(&sem);
                shared_var++;
                //printf("inc thread:sharedvar%d\n",shared_var);
                sem_post(&sem);
        }
        return NULL;
}
int main()
{
        pthread_t incthread;
        pthread_t incthread1;
        sem_init(&sem,0,1);
        pthread_create(&incthread,NULL,inc,NULL);
        pthread_create(&incthread1,NULL,inc,NULL);
        pthread_join(incthread,NULL);
        pthread_join(incthread1,NULL);
        printf("final value shered%d",shared_var);
        sem_destroy(&sem);
        return 0;
}

//rite a C program to implement the producer-consumer problem using pthreads. Create
//two threads - one for producing items and another for consuming items from a shared buffer?
#include<stdio.h>
#include<pthread.h>
int cnt=0;
pthread_mutex_t lock;//mutex for synchronisation
pthread_cond_t notempty;
pthread_cond_t notfull;
char buf[100];
int size=5;
void *produce(void *arg)
{
        int item=1;
        while(1)
        {

        pthread_mutex_lock(&lock);
        while(cnt==size)
        {
                pthread_cond_wait(&notfull,&lock);
        }
        buf[cnt]=item;
        printf("thread:item%d\n",item);
        cnt++;
        item++;
        pthread_cond_signal(&notempty);
                pthread_mutex_unlock(&lock);
        }
        return NULL;
}
void *consume(void *arg)
{
        int item=1;
        while(1)
        {

        pthread_mutex_lock(&lock);
        while(cnt==0)
        {
                pthread_cond_wait(&notfull,&lock);
        }
        int item=buf[cnt-1];
        printf("thread:consumeitem%d\n",item);
  cnt--;
        pthread_cond_signal(&notempty);
                pthread_mutex_unlock(&lock);
        }
        return NULL;
}

int main()
{
        pthread_t incthread;
        pthread_t incthread1;
        pthread_mutex_init(&lock,NULL);
        pthread_cond_init(&notempty,NULL);
        pthread_cond_init(&notfull,NULL);
        pthread_create(&incthread,NULL,produce,NULL);
        pthread_create(&incthread1,NULL,consume,NULL);
        pthread_join(incthread,NULL);
        pthread_join(incthread1,NULL);
//      printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        pthread_cond_destroy(&notfull);
        pthread_cond_destroy(&notempty);
        return 0;
}




int main()
{
        pthread_t threadid;
        char s[100]="embedded";
        if(pthread_create(&threadid,NULL,print,s)!=0)
        {
                perror("thread error");
                return 1;
        }
        pthread_join(threadid,NULL);
}
//Write a C program to demonstrate thread cancellation. Create a thread that runs an infinite
//loop and cancels it after a certain condition is met from the main thread?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
void *infi(void *arg)
{
        while(1)
        {
                printf("thread running\n");
                sleep(1);
                pthread_testcancel();
        }
        return NULL;
}
int main()
{
        pthread_t incthread;
        //pthread_t incthread1;
        pthread_create(&incthread,NULL,infi,NULL);
        //pthread_create(&incthread1,NULL,inc,NULL);
        //cancellthread
        printf("cancel thread\n");
        pthread_cancel(incthread);
        pthread_join(incthread,NULL);
        printf("mainthreadjoiningcancelld\n");
        return 0;
}

//Write a C program to demonstrate thread cancellation. Create a thread that runs an infinite
//loop and cancels it after a certain condition is met from the main thread?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
void *infi(void *arg)
{
        while(1)
        {
                printf("thread running\n");
                sleep(1);
                pthread_testcancel();
        }
        return NULL;
}
int main()
{
        pthread_t incthread;
        //pthread_t incthread1;
        pthread_create(&incthread,NULL,infi,NULL);
        //pthread_create(&incthread1,NULL,inc,NULL);
        //cancellthread
        printf("cancel thread\n");
        pthread_cancel(incthread);
        pthread_join(incthread,NULL);
        printf("mainthreadjoiningcancelld\n");
        return 0;
}
/Write a C program to create a thread that prints the even numbers between 1 and 20?

#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        int num=*((int *)arg);
        for(int i=2;i<=num;i++)
        {
        if(i%2==0)
        {

        printf("even=%d\n",i);
        }
        }
        return NULL;
}
int main()
{
        pthread_t thread1;
        int n=10;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
//Develop a C program to create two threads that print odd and even numbers alternately?
#include<stdio.h>
#include<pthread.h>
pthread_mutex_t lock;//mutex for synchronisation
pthread_cond_t cond;
int cnt=1;
#define max 10
void *odd(void *arg)
{
        while(cnt<=max)
        {

        pthread_mutex_lock(&lock);
        if(cnt%2!=0)
        {
                printf("odd:%d\n",cnt++);
        pthread_cond_signal(&cond);
        }
        else
        {
        pthread_cond_wait(&cond,&lock);
        }
                pthread_mutex_unlock(&lock);
        }
        return NULL;
}
void *even(void *arg)
{
        while(cnt<=max)
        {

        pthread_mutex_lock(&lock);
        if(cnt%2==0)
        {
                printf("odd:%d\n",cnt++);
                pthread_cond_signal(&cond);
        }


            else
        {
        pthread_cond_wait(&cond,&lock);
        }
                pthread_mutex_unlock(&lock);
        }
        return NULL;
}




int main()
{
        pthread_t incthread;
        pthread_t incthread1;
        pthread_mutex_init(&lock,NULL);
        pthread_cond_init(&cond,NULL);
        pthread_create(&incthread,NULL,odd,NULL);
        pthread_create(&incthread1,NULL,even,NULL);
        pthread_join(incthread,NULL);
        pthread_join(incthread1,NULL);
//      printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        pthread_cond_destroy(&cond);
        pthread_cond_destroy(&cond);
        return 0;
}
/3.Implement a C program to create a thread that calculates the sum of squares of numbers
//from 1 to 10??
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
int sum=0;
void *print(void *arg)
{
        int num=*((int *)arg);
        for(int i=1;i<=num;i++)
        {
        int res=i*i;
        sum=sum+res;
        printf("res=%d sum=%d",res,sum);
        }
}
int main()
{
        pthread_t thread1;
        int n=5;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
//64.Write a C program to create a thread that calculates the product of numbers from 1 to 5?
//from 1 to 10??
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
int res=1;
void *print(void *arg)
{
        int num=*((int *)arg);
        for(int i=1;i<=num;i++)
        {
        res=res*i;
        printf("product=%d\n ",res);
        }
}
int main()
{
        pthread_t thread1;
        int n=5;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
/7.Write a C program to create a thread that calculates the sum of Fibonacci numbers up to a
//given limit?

#include<stdio.h>
#include<pthread.h>

pthread_mutex_t lock;//mutex for synchronisation
void *rangefib(void *arg)
{
        int a=0,b=1;
        for(int n=1;n<10;n++)
        {
                int c=a+b;
         a=b;
          b=c;
                pthread_mutex_lock(&lock);

                printf("%d\n",c);
               pthread_mutex_unlock(&lock);
        }

        return NULL;
}
int main()
{
        pthread_t thread;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread,NULL,rangefib,NULL);
        pthread_join(thread,NULL);
//printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        return 0;
}
/37.Develop a C program to create a thread that finds the maximum element in an array
#include<stdio.h>
#include<pthread.h>
#include<string.h>
#include<stdlib.h>
//#define size 10
typedef struct{
        int *a;
        int size;
}aray;


void *maxi(void *arg)
{
aray *n=(aray*)arg;
int *b=n->a;
int n1=n->size;
int max=b[0];
for(int i=0;i<n1;i++)
{
        if(b[i]>max)
        {
                max=b[i];
        }
}

printf("max=%d",max);
return NULL;
}
int main()
{
        pthread_t threadid;
        int a1[]={1,5,6,2,3};
        int size=sizeof(a1)/sizeof(a1[0]);
        aray *arg = (aray *)malloc(sizeof(aray));
//      aray *arg=malloc(sizeof(aray));
        arg->a=a1;
        arg->size=size;

        if(pthread_create(&threadid,NULL,maxi,arg)!=0)
        {
                perror("thread error");
                return 1;
        }
        pthread_join(threadid,NULL);
}
/Implement a C program to create a thread that prints the ASCII values of characters in a
//given string?
//from 1 to 10??
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
int res=1;
void *print(void *arg)
{
        char *p=(char *)arg;
        for(int i=0;p[i];i++)
        {
        printf("ascii=%d\n",p[i]);
        }
}
int main()
{
        pthread_t thread1;
        char n[100]="abcd";
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
/.Develop a C program to create a thread that calculates the sum of all prime numbers up to
//a given limit?
#include<stdio.h>
#include<pthread.h>
int sum=0;
pthread_mutex_t lock;//mutex for synchronisation
void *rangeprime(void *arg)
{
        for(int n=2;n<10;n++)
        {
         int cnt=0;
        for(int i=1;i<=n;i++)
        {
                if(n%i==0)
                {
                        cnt++;

                }
        }
                if(cnt==2)
                {
                pthread_mutex_lock(&lock);

                printf("prime%d\n",n);
                sum=sum+n;
                printf("sum=%d\n",sum);
               pthread_mutex_unlock(&lock);
        }
        }
        return NULL;
}
int main()
{
        pthread_t thread;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread,NULL,rangeprime,NULL);
        pthread_join(thread,NULL);
 pthread_mutex_destroy(&lock);
        return 0;
}

//9.Write a C program to create a thread that calculates the area of a circle using a given
//radius?

#include<stdio.h>
#include<pthread.h>
#define PI 3.14
float res;
void *circle(void *arg)
{

int *n=(int* )arg;
        res=PI*(*n)*(*n);
                //printf("res=%d\n",res);
        return NULL;
}
int main()
{
        pthread_t thread;
        int r=2;
        pthread_create(&thread,NULL,circle,&r);
        pthread_join(thread,NULL);
        printf("final value shered%f",res);

        return 0;
}

//Develop a C program to create a thread that calculates the average of numbers in an array?

#include<stdio.h>
#include<pthread.h>
#include<stdlib.h>
#define num 100
double average=0.0;
typedef struct
{
        int *a;
        int n;
}avg;
void *avge(void *arg)
{
        avg *data=(avg*)arg;
        int *b=data->a;
        int n=data->n;
        long long sum=0;

for(int i=0;i<n;i++)
{
         sum=sum+b[i];
}
double average1=(double)sum/n;
        average=average1;

        return NULL;
}
int main()
{
        pthread_t thread;
        int n=5;
        int *a=malloc(n*sizeof(int));
        printf("enter elemnets");
        for(int i=0;i<n;i++)
        {
                scanf("%d",&a[i]);
avg data;
        data.a=a;
        data.n=n;


        pthread_create(&thread,NULL,avge,&data);
        pthread_join(thread,NULL);
printf("final value shered%.2f",average);
        return 0;
}
/Implement a C program to create a thread that prints the factors of a given number?
#include<stdio.h>
#include<pthread.h>
int sum=0;
//pthread_mutex_t lock;//mutex for synchronisation
void *factors(void *arg)
{
        int n=(*(int *)arg);
        for(int i=1;i<n;i++)
        {
                if(n%i==0)
                {
                        printf("factors:%d\n",i);
                }
        }
        return NULL;
}
int main()
{
        pthread_t thread;
        //pthread_mutex_init(&lock,NULL);
        int n=6;
        pthread_create(&thread,NULL,factors,&n);
        pthread_join(thread,NULL);
//      printf("final value shered%d",shared_var);
        //pthread_mutex_destroy(&lock);
        return 0;
}
/72.Develop a C program to create a thread that prints the English alphabet in uppercase?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
int res=1;
void *print(void *arg)
{
        char *p=(char *)arg;
        *p=*p-32;
        printf("ascii=%c\n",*p);

}
int main()
{
        pthread_t thread1;
        char ch='a';
        pthread_create(&thread1,NULL,print,&ch);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
//Implement a C program to create a thread that calculates the square of a number?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        int num=*((int *)arg);
        int res=num*num;
        printf("%d",res);
}
int main()
{
        pthread_t thread1;
        int n=5;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
//74.Implement a C program to create a thread that checks if a given number is divisible by
//another given number?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *print(void *arg)
{
        int num=*((int *)arg);
        int key=5;
        if(num%key==0)
        {
                printf("divisible by 5");
        }
        else
        {
                printf("not");
        }
}
int main()
{
        pthread_t thread1;
        int n=21;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
//5.Develop a C program to create a thread that prints the multiplication table of a given
//number up to a given limit?
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#define cnt 10
void *print(void *arg)
{
        int num=*((int *)arg);
        for(int i=1;i<=cnt;i++)
        {
                printf("%d*%d=%d\n",num,i,num*i);
        }
}
int main()
{
        pthread_t thread1;
        int n=2;
        pthread_create(&thread1,NULL,print,&n);
        //wait for threads to complte
        pthread_join(thread1,NULL);
}
/Write a C program to create a thread that prints the current date and time?
#include<stdio.h>
#include<pthread.h>
#include<time.h>
void *print(void *arg)
{
        time_t now;
        struct tm *timeinfo;
        time(&now);
        timeinfo=localtime(&now);
        printf("current time=%s",asctime(timeinfo));
}
int main()
{
        pthread_t thread;
        pthread_create(&thread,NULL,print,NULL);
        pthread_join(thread,NULL);
}
//15.Implement a C program to create two threads that increment and decrement a shared
//variable, respectively, using mutex locks?
#include<stdio.h>
#include<pthread.h>
int shared_var=0;
pthread_mutex_t lock;//mutex for synchronisation
void *inc(void *arg)
{
        for(int i=0;i<5;i++)
        {
                pthread_mutex_lock(&lock);
                shared_var++;
                printf("inc thread:sharedvar%d\n",shared_var);
                pthread_mutex_unlock(&lock);
        }
        return NULL;
}
void *dec(void *arg)
{
        for(int i=0;i<5;i++)
        {
                pthread_mutex_lock(&lock);
                shared_var--;
                printf("dec thread:sharedvar%d\n",shared_var);
                pthread_mutex_unlock(&lock);
        }
        return NULL;
}
int main()
{
        pthread_t incthread;
        pthread_t decthread;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&incthread,NULL,inc,NULL);
        pthread_create(&decthread,NULL,dec,NULL);
        pthread_join(incthread,NULL);
        pthread_join(decthread,NULL);
printf("final value shered%d",shared_var);
        pthread_mutex_destroy(&lock);
        return 0;
}

//78.Develop a C program to create a thread that prints numbers from 10 to 1 in descending order
//using mutex locks?
#include<stdio.h>
#include<pthread.h>
pthread_mutex_t lock;
void *print(void *arg)
{
        int num=*((int*)arg);
        for(int i=num;i>0;i--)
        {
                pthread_mutex_lock(&lock);
                printf("%d\n",i);
                pthread_mutex_unlock(&lock);
        }
        return NULL;
}
int main()
{
        pthread_t thread;
        int n=10;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&thread,NULL,print,&n);
        pthread_join(thread,NULL);
        pthread_mutex_destroy(&lock);
        return 0;
}

```

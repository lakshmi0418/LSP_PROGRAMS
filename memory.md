#MEMORY MANAGEMENT
```c
//Write a C program to demonstrate dynamic memory allocation using malloc()
#include<stdio.h>
#include<stdlib.h>
int main()
{
        int n=4;
        int *p=malloc(n*sizeof(int));
        if(p==NULL)
        {
                printf("error in memry");
                return 1;
        }
        for(int i=0;i<n;i++)
        {
                scanf("%d",&p[i]);
        }
        for(int i=0;i<n;i++)
        {
                printf("%d",p[i]);
        }
free(p);
}

//Write a C program to demonstrate dynamic memory allocation using calloc(),realloc
#include<stdio.h>
#include<stdlib.h>
int main()
{
        int n=4,n1=6;
        int *p=calloc(n,sizeof(int));
        if(p==NULL)
        {
                printf("error in memry");
                return 1;
        }
        for(int i=0;i<n;i++)
        {
                scanf("%d",&p[i]);
        }
        for(int i=0;i<n;i++)
        {
                printf("%d",p[i]);
        }
        p=realloc(p,n1*(sizeof(int)));
        for(int i=0;i<n1;i++)
        {
                scanf("%d",&p[i]);
        }
        for(int i=0;i<n1;i++)
        {
                printf("%d",p[i]);
        }

free(p);
}

/Implement a C program to simulate memory allocation using the first-fit algorithm
#include<stdio.h>
#define max 100
#define max1 200
int main()
{
        int blocks[max1],process[max],initi[max];
        int nblocks=3,nproces=4;
        printf("number of blocks");
        for(int i=0;i<nblocks;i++)
        {
                scanf("%d",&blocks[i]);
        }
        printf("number of process");
        for(int i=0;i<nproces;i++)
        {
                scanf("%d",&process[i]);
                initi[i]=-1;
        }
        for(int i=0;i<nproces;i++)
        {
                for(int j=0;j<nblocks;j++)
                {
                if (blocks[j] >= process[i]) {
                initi[i] = j;
                blocks[j] -= process[i];  // Reduce available memory in that block
                break;
            }
        }
    }

printf("\nProcess No.\tProcess Size\tBlock No.\n");
    for (int i = 0; i < nproces; i++) {
        printf("%d\t\t%d\t\t", i + 1, process[i]);
        if (initi[i] != -1)
            printf("%d\n", initi[i] + 1);  // Block numbers shown as 1-based
        else
 printf("Not Allocated\n");
    }
}

/Best_fit 
#include<stdio.h>
#define max 100
#define max1 200
int main()
{
        int blocks[max1],process[max],initi[max];
        int nblocks=3,nproces=4;
        printf("number of blocks");
        for(int i=0;i<nblocks;i++)
        {
                scanf("%d",&blocks[i]);
        }
        printf("number of process");
        for(int i=0;i<nproces;i++)
        {
                scanf("%d",&process[i]);
                initi[i]=-1;
        }
        //BEST FIT
        for(int i=0;i<nproces;i++)
        {
                int bestIdx=-1;
                for(int j=0;j<nblocks;j++)
                {
                        if (blocks[j] >= process[i]) {
                if (bestIdx == -1 || blocks[j] < blocks[bestIdx]) {
                    bestIdx = j;

            }
        }
    }
        }

printf("\nProcess No.\tProcess Size\tBlock No.\n");
    for (int i = 0; i < nproces; i++) {
        printf("%d\t\t%d\t\t", i + 1, process[i]);


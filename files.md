### FILE MANAGEMENT

```c
//write a C program to create a new text file and write "Hello, World!" to it?
#include<stdio.h>
int main()
{
        FILE *fp=fopen("file.txt","w");
        if(fp==NULL)
        {
                printf("file was not created");
                return 1;
        }
        fprintf(fp,"helloworld\n");
        fclose(fp);
return 0;
}
,,,

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
/Develop a C program to open an existing text file and display its contents?
#include<stdio.h>
int main()
{
        FILE *fp=fopen("1.c","r");
        if(fp==NULL)
        {
                printf("not open");
                return 1;
        }
        char ch;
        while((ch=fgetc(fp))!=EOF)
        {
                putchar(ch);
        }
        fclose(fp);
        return 0;
}

,,,

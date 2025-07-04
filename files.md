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

//Develop a C program to open an existing text file and display its contents?
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
//implement a C program to create a new directory named "Test" in the currentdirectory?
#include<stdio.h>
#include<stdlib.h>
#include<sys/stat.h>
int main()
{
        //mode_t old_mask=umask(0); 
        int status=mkdir("Test1",0777);
        //umask(old_mask);
        if(status==0)
        {
                printf("created\n");
        }
        else
        {
                perror("not create");
        }
}

//Write a C program to check if a file named "sample.txt" exists in the current directory?
#include<stdio.h>
int main()
{
        FILE *fp=fopen("1.c","r");
        if(fp!=NULL)
        {
                printf("file exist");
        }
        else
                printf("file not exist");
        return 0;
}
 
/Develop a C program to rename a file from "oldname.txt" to "newname.txt"?
#include<stdio.h>
int main()
{
        int result=rename("file.txt","newfile.txt");
        if(result==0)
        {
                printf("rename suc");
        }
        else
                printf("rename failed");
}

//Implement a C program to delete a file named "delete_me.txt"
#include<stdio.h>
int main()
{
        int result=remove("dummy.c");
        if(result==0)
        {
                printf("delete suc");
        }
        else
                printf("delete failed");
}


        }


/Write a C program to copy the contents of one file to another?
#include<stdio.h>
int main()
{
    FILE *fp=fopen("1.c","r");
    if(fp==NULL)
            {
                    printf("open sucess");
                    return 1;
}
FILE *fp1=fopen("dummy.c","w");
if(fp1==NULL)
            {
                    printf("open sucess");
                    return 1;
}
char ch;
while((ch=fgetc(fp))!=EOF)
{
        fputc(ch,fp1);/Develop a C program to move a file from one directory to another?
#include<stdio.h>
int main()
{
        char source[]=".";
        char dest[]="..";
        if(rename(source,dest)==0)
        {
                printf("%s %s",source,dest);
                return 0;
        }
        else
        {
                FILE *fp=fopen("source","rb");
                if(fp==NULL)
                {
                        printf("source not found%s",source);
                        return 1;
                }
                FILE *fp1=fopen("dest","wb");
                if(fp1==NULL)
                {
                        printf("dest not found");
                        return 1;
                }
                char buf[00];

                size_t bytesr;
                while(bytesr=fread(buf,1,sizeof(buf),fp))
                {
                        fwrite(buf,1,bytesr,fp1);
                }

//Implement a C program to list all files in the current directory?
#include<stdio.h>
#include<dirent.h>
int main()
{
        DIR *dir=opendir(".");
        if(dir==NULL)
        {
                printf("error opening");
                return 1;
        }
        struct dirent *e;
        while((e=readdir(dir))!=NULL)
        {
                printf("%s\n ",e->d_name);
        }
}

        }
}


}
fclose(fp);
fclose(fp1);
}

/Write a C program to get the size of a file named "file.txt"?
#include<stdio.h>
int main()
{
        const char *na="newfile.txt";
        FILE *fp=fopen(na,"rb");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        fseek(fp,0,SEEK_END);
        int size=ftell(fp);
        printf("%s%d",na,size);
}

/implement a C program to create a new directory named "Backup" in the parentdirectory?
#include<stdio.h>
#include<sys/types.h>
#include<sys/stat.h>
int main()
{
        const char *direct="../test";
        if(mkdir(direct,0755)==0)
        {
                printf("create new dire%s",direct);
        }
        else
                printf("error");
}


//Develop a C program to check if a directory named "Test" exists in the currentdirectory?
#include<stdio.h>
#include<dirent.h>
int main()
{
        const char *name="test";
        DIR *dir=opendir(name);
        if(dir)
        {
                printf("exist %s",name);
        }
        else
                printf("not exist");
}

//Write a C program to recursively list all files and directories in a given directory?
#include<stdio.h>
#include<dirent.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<string.h>
void listfiles(const char *path)
{
        DIR *dir=opendir(path);
        struct dirent *entry;
        while((entry=readdir(dir))!=NULL)
        {
if(strcmp(entry->d_name,".")==0 || strcmp(entry->d_name,"..")==0)
        continue;
char path1[1024];
snprintf(path1,sizeof(path1),"%s/%s",path,entry->d_name);
printf("%s",path1);
  struct stat statbuf;
        if (stat(path1, &statbuf) == 0 && S_ISDIR(statbuf.st_mode))
        {
listfiles(path1);
        }
//if(path==d.name)
//      listfiles(path);
        }
}
int main()
{
        const char *direct=".";
        listfiles(direct);
}

  /14. Develop a C program to delete all files in a directory named "Temp"?
#include<stdio.h>
#include<dirent.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<string.h>
int main()
{
        const char *path="temp";
        DIR *dir=opendir(path);
        struct dirent *entry;
        while((entry=readdir(dir))!=NULL)
        {
if(strcmp(entry->d_name,".")==0 || strcmp(entry->d_name,"..")==0)
        continue;
char path1[1024];
snprintf(path1,sizeof(path1),"%s/%s",path,entry->d_name);
if(remove(path1) == 0) {
            printf("Deleted: %s\n", path1);
        } else {
            perror("Error deleting file");
        }
        }
}
/Implement a C program to count the number of lines in a file named "data.txt"?
#include<stdio.h>
int main()
{
        FILE *fp;
        int cnt=0;
        fp=fopen("dummy.c","r");
        if(fp==NULL)
        {
                printf("not there");
                return 1;
        }
        char ch;
        while((ch=fgetc(fp))!=EOF)
        {
if(ch=='\n'){
        cnt++;
}
}
printf("%d",cnt);
}

//Write a C program to append "Goodbye!" to the end of an existing file named
//message.txt"?

#include<stdio.h>
int main()
{
        FILE *fp=fopen("dummy.c","a");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        fprintf(fp,"good bye");
        fclose(fp);
}

        cnt++;
}
}
printf("%d",cnt);
}



/Write a C program to append "Goodbye!" to the end of an existing file named
//message.txt"?

#include<stdio.h>
int main()
{
        FILE *fp=fopen("dummy.c","a");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        fprintf(fp,"good bye");
        fclose(fp);
}           

//Implement a C program to change the permissions of a file named "file.txt" to read-
//only?
#include<stdio.h>
#include<sys/types.h>
#include<sys/stat.h>
int main()
{
        const char *name="dumm.c";
        if((chmod(name,S_IRUSR||S_IRGRP||S_IROTH))==-1)
        {
                printf("failed");
                return 1;
        }
        printf("%s",name);
}

//Write a C program to change the ownership of a file named "file.txt" to the user
//"user1"?
#include<stdio.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<pwd.h>
#include<stdlib.h>
#include<unistd.h>
int main()
{
        const char *filename="dummy.c";
        const char *username="user1";
         struct passwd *user_info = getpwnam(username);
        if(user_info == NULL) {
        perror("User not found");
        return 1;
    }
        uid_t user_uid=user_info->pw_uid;
        gid_t user_gid=user_info->pw_gid;
        if(chown(filename,user_uid,user_gid)==-1)
        {
                perror("error");
                return 1;
        }
printf("Ownership of '%s' has been changed to user '%s'.\n", filename, username);

        //printf("%s%s",filename,username);
}



/Develop a C program to get the last modified timestamp of a file named "file.txt"?
#include<stdio.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<pwd.h>
#include<stdlib.h>
#include<unistd.h>
#include<time.h>
int main()
{
        struct stat filesta;
const char *filename="file.txt";
        if(stat(filename,&filesta)==-1)
        {
                perror("erroe file state");
                return 1;
        }
        printf("last modified= %s %s",filename,ctime(&filesta.st_mtime));
}

/mplement a C program to create a temporary file and write some data to it
#include<stdio.h>
int main()
{
        FILE *temp1=tmpfile();
        if(temp1==NULL)
        {
                printf("file not create");
                return 1;
        }
        const char *data="this is temporary data";
        if(fputs(data,temp1)==EOF){
perror("failed to write");
        fclose(temp1);
        return 1;
        }
        rewind(temp1);
        char buf[256];
        while(fgets(buf,sizeof(buf),temp1))
        {
                printf("%s",buf);
}
}




```

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
//Write a C program to check if a given path refers to a file or a directory?
#include <stdio.h>
#include <sys/stat.h>

int main() {
    const char *path = "temp";
    struct stat pathStat;

    if (stat(path, &pathStat) == -1) {
        perror("Error getting path status");
        return 1;
    }

    if (S_ISDIR(pathStat.st_mode)) {
        printf("The path '%s' is a directory.\n", path);
    } else if (S_ISREG(pathStat.st_mode)) {
        printf("The path '%s' is a regular file.\n", path);
    } else {
        printf("The path '%s' is something else.\n", path);
    }
}


/Develop a C program to create a hard link named "hardlink.txt" to a file named
//"source.txt"?
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
int main()
{
        const char *src="dummy.c";
const char *hard="hard.c";
if(link(src,hard)==-1)
{
        perror("error");
        return 1;
}
printf("%s %s",src,hard);
}
//23.Implement a C program to read and display the contents of a CSV file named
//"data.csv"?
#include<stdio.h>
#include<string.h>
int main()
{
        FILE *fp=fopen("dummy.csv","r");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        char ch;
        char buf[100];
        while(fgets(buf,sizeof(buf),fp))
        {
                char *tok=strtok(buf,",");


        while(tok!=NULL)
        {

        printf("%s",tok);
tok=strtok(NULL,",");
//      fclose(fp);
}
}
}

/Write a C program to get the absolute path of the current working directory
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
int main()
{
        char buf[100];
        if(getcwd(buf,sizeof(buf))!=NULL)
        {
                printf("%s",buf);
        }
        else
                printf("error");
}

 //Develop a C program to get the size of a directory named "Documents"?
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <sys/stat.h>
#include <string.h>

long getDirectorySize(const char *dirPath) {
    DIR *dir;
    struct dirent *entry;
    struct stat statbuf;
    long totalSize = 0;

    // Open the directory
    dir = opendir(dirPath);
    if (dir == NULL) {
        perror("Error opening directory");
        return -1;  // Return -1 if there's an error opening the directory
    }

    // Read each entry in the directory
    while ((entry = readdir(dir)) != NULL) {
        // Skip the special entries "." and ".."
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0) {
            continue;
        }

        // Construct the full path of the file/directory
        char fullPath[1024];
        snprintf(fullPath, sizeof(fullPath), "%s/%s", dirPath, entry->d_name);

        // Get the file stats using stat()
        if (stat(fullPath, &statbuf) == -1) {
            perror("Error getting file stats");
            closedir(dir);
            return -1;
        }    return -1;
        }

        // If it's a regular file, add its size to the total size
        if (S_ISREG(statbuf.st_mode)) {
            totalSize += statbuf.st_size;
        }
        // If it's a directory, recursively get the size of that directory
        else if (S_ISDIR(statbuf.st_mode)) {
            long subDirSize = getDirectorySize(fullPath);
            if (subDirSize != -1) {
                totalSize += subDirSize;
            }
        }
    }

    // Close the directory
    closedir(dir);

    return totalSize;
}

int main() {
    const char *dirPath = "Documents";  // Directory to calculate size

    // Get the size of the directory
    long size = getDirectorySize(dirPath);
    if (size != -1) {
        printf("Total size of '%s' is: %ld bytes\n", dirPath, size);
    }

    return 0;
}

/Develop a C program to create a FIFO (named pipe) named "myfifo" in the current
//directory?
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>
int main()
{
        const char *fifopath="myfifo1";
        if(mkfifo(fifopath,0666)==-1)
        {
                perror("error");
                return 1;
        }
        printf("myfifo created");
}

}

// Implement a C program to read data from a FIFO named "myfifo"?
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>
int main()
{
        const char *fifopath="myfifo";
        char buf[100];
        int fd=open(fifopath,O_RDONLY);
        if(fd==-1)
        {
                perror("error");
                return 1;
        }
        printf("waiting data from fifo");
        ssize_t bytes;
        while((bytes=read(fd,buf,sizeof(buf)-1))>0)
        {
                buf[bytes]='\0';
                printf("receicve=%s",buf);
        }
}


/ Write a C program to truncate a file named "file.txt" to a specified lengt
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>
int main()
{
        const char *filename="dummy.c";
        int length=100;
        int fd=open(filename,O_RDWR);
        if(fd==-1)
        {
                perror("error");
                return 1;
        }
        if(ftruncate(fd,length)==-1)
        {
                perror("error trunc");
                return 1;

        }
printf("truncated0");
}
//Develop a C program to search for a specific string in a file named "data.txt" and
//display the line number(s) where it occurs?
#include<stdio.h>
#include<string.h>
int main()
{
         FILE *fp;
         const char *filename="dummy.c";
         char search[100];
         char buf[100];
         int linenum=0;
         printf("enter string");
         fgets(search,sizeof(search)-1,stdin);

fp=fopen(filename,"r");
if(fp==NULL)
{
        printf("not found");
        return 1;
}
while(fgets(buf,sizeof(buf),fp))
{
        linenum++;

if(strstr(buf,search)!=NULL)
{
        printf("%d%s",linenum,buf);

}
}/mplement a C program to get the file type (regular file, directory, symbolic link, etc.) of
//a given path?
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <unistd.h>
int main()
{
        struct stat pathstat;
        char path[100];
        printf("enter the path");
        fgets(path,sizeof(path)-1,stdin);
        if(stat(path,&pathstat)==-1)
        {
                perror("not status");
                return 1;
        }
         if(S_ISREG(pathstat.st_mode))
        {
                printf("%s regule",path);
        }
        else if(S_ISDIR(pathstat.st_mode))
        {
                printf("%s dir",path);
        }
       else  if(S_ISLNK(pathstat.st_mode)){
                printf("%s link",path);
        }
        else
        {
                printf("unknown");
        }
}

/Write a C program to create a new empty file named "empty.txt"?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        FILE *fp=fopen("empty.txt","w");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        printf("created success");
}

//Develop a C program ?o "et "the 
//permissions (mode) of a file named "file.txt"?
#include<stdio.h>
#include<sys/stat.h>
void print(mode_t mode)
{
        printf((S_ISDIR(mode))?"d":"-");
//wner
printf((mode & S_IRUSR)?"r":"-");
printf((mode & S_IWUSR)?"w":"-");
printf((mode & S_IXUSR)?"x":"-");
//grp
printf((mode & S_IRGRP)?"r":"-");
printf((mode & S_IWGRP)?"w":"-");
printf((mode & S_IXGRP)?"x":"-");
//other
printf((mode & S_IROTH)?"r":"-");
printf((mode & S_IWOTH)?"w":"-");
printf((mode & S_IXOTH)?"x":"-");
}
int main()
{
        struct stat filestat;
        if(stat("file.txt",&filestat)==-1)
        {
                printf("error stat");
                return 1;
        }
        print(filestat.st_mode);
}

//mplement a C program to recursively delete a directory named "Temp" and all its
//contents?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <unistd.h>
#include <sys/stat.h>
void rem_dir(const char *path)
{
        //open dir
        DIR *dir=opendir(path);
        if(!dir)
        {
                perror("error");
        //      return 1;
        }
        //readdir
        struct dirent *entry;
        while((entry=readdir(dir))!=NULL)
        {
                if(strcmp(entry->d_name,".")==0 ||strcmp(entry->d_name,"..")==0)continue;
                char full[1024];
                snprintf(full,sizeof(full),"%s/%s",path,entry->d_name);
                //stat
                struct stat buf;
                if(stat(full,&buf)==-1)
                {
                        perror("state err");
                        continue;
                }
                //stat
                if(S_ISDIR(buf.st_mode))
                {
                        remove(full);
                }
        else {
// Remove file
            if (remove(path) == -1) {
                perror("remove");
            }
        }

}
}
int main()
{
        const char//rite a C program to read and display the first 10 lines of a file named "log.txt"?
#include<stdio.h>
int main()
{
        FILE *fp=fopen("35.c","r");
        if(fp==NULL)
        {
                printf("file not create");
                return 1;
        }
        char line[256];
        int cnt=0;
        while(cnt<10&&fgets(line,sizeof(line),fp)!=NULL)
        {
                printf("%s",line);
                cnt++;
        }
}
 *path="temp";
        rem_dir(path);
}


//Develop a C program to read data from a text file named "input.txt" and write it to
//another file named "output.txt" in reverse order?
#include<stdio.h>
int main()
{
        FILE *fp=fopen("1.c","r");
        if(fp==NULL)
        {
                printf("1 not fund");
                return 1;
        }
        fseek(fp,0,SEEK_END);
        int size=ftell(fp);
        FILE *fp1=fopen("rev.c","w");
        if(fp==NULL)
        {
                printf("2 not fund");
                fclose(fp);
                return 1;
        }
        for(int i=size-1;i>=0;i--)
        {
                fseek(fp,i,SEEK_SET);
                char ch=fgetc(fp);
                fputc(ch,fp1);
        }
        fclose(fp);
        fclose(fp1);
}

//mplement a C program to create a new directory named with the current date in the
// format "YYYY-MM-DD"?
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <sys/stat.h>
#include <sys/types.h>
int main()
{
        time_t t=time(NULL);
                struct tm tm=*localtime(&t);
        char dir_name[100];
        snprintf(dir_name,sizeof(dir_name),"%04d-%02d-%02d",tm.tm_year+1990,tm.tm_mon+1,tm.tm_mday);
        if(mkdir(dir_name,0755)==0)
        {
                printf("create suc%s",dir_name);
        }
        else
        {
                perror("error craet");
        }
}

//Write a C program to read and display the contents of a binary file named "binary.bin"?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        FILE *fp=fopen("dummy.bin","r");
        if(fp==NULL)
        {
                printf("not create");
                return 1;
        }
        char buf[100];
        int byte;
        while(byte=fread(buf,1,sizeof(buf),fp)>0)
        {
                for(int i=0;i<byte;i++)
                {
                printf("%02x",buf[i]);
                }//evelop a C program to get the size of the largest file in a directory?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <unistd.h>
#include <sys/stat.h>
void rem_dir(const char *path)
{
 char largest_file[256]={0};
 long largest_size=0;
 //open dir
        DIR *dir=opendir(path);
        if(!dir)
        {
                perror("error");
        //      return 1;
        }
        //readdir
        struct dirent *entry;
        while((entry=readdir(dir))!=NULL)
        {
                if(strcmp(entry->d_name,".")==0 ||strcmp(entry->d_name,"..")==0)continue;
                char full[1024];
                snprintf(full,sizeof(full),"%s/%s",path,entry->d_name);
                //stat
                struct stat buf;
                if(stat(full,&buf)==-1)
                {
                        perror("state err");
                        continue;
                }
               if (S_ISREG(buf.st_mode) && buf.st_size > largest_size) {
            largest_size = buf.st_size;
            strncpy(largest_file, full, sizeof(largest_file) - 1);
        }
    } closedir(dir);

    if (largest_size > 0) {
        printf("Largest file: %s\n", largest_file);
        printf("Size: %ld bytes\n", largest_size);
    }

}


int main()
{
        const char *path="/home/hi/lsp";
        rem_dir(path);
}

//Implement a C program to check if a file named "data.txt" is readable?
#include<stdio.h>
int main()
{
        FILE *fp=fopen("dummy.c","r");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        printf("readable file");
        return 0;
}

/evelop a C program to check if a file named "config.ini" is writable?
#include<stdio.h>
int main()
{
        FILE *fp=fopen("dummy.c","r");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        printf("readable file");
        FILE *fp1=fopen("config.ini","w");
        char ch;
        while((ch=fgetc(fp))!=EOF)
        {
                fputc(ch,fp1);
        }
        if(fp1==NULL)
        {
                printf("error");
                return 1;
        }
        printf("write  file");
/Implement a C program to read the contents of a text file named "instructions.txt" and execute the instructions as shell commands?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        FILE *fp=fopen("instructions.txt","r");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        //printf("readable file");
        char command[256];
        while(fgets(command,sizeof(command)-1,fp))
        {
                if(command[0]=='\0' || command[0]=='#')
                        continue;

        int status=system(command);
        if(status==-1)
        {
                perror("error exe");
        }
        else{
                printf("execute=%s",command);
}
}
}

// Write a C program to get the number of hard links to a file named "file.txt"?
#include <stdio.h>
#include <sys/stat.h>
int main()
{
        struct stat file_stat;
        if(stat("file.txt",&file_stat)==-1)
        {
                perror("error in stat");
                return 1;
        }
        printf("hardlinks%ld",(long)file_stat.st_nlink);
}
     printf("execute=%s",command);
}
}
}


        fclose(fp);
        fclose(fp1);
}

// Write a C program to get the number of hard links to a file named "file.txt"?
#include <stdio.h>
#include <sys/stat.h>
int main()
{
        struct stat file_stat;
        if(stat("file.txt",&file_stat)==-1)
        {
                perror("error in stat");
                return 1;
}
        printf("hardlinks%ld",(long)file_stat.st_nlink);
}

//Develop a C program to copy the contents of all text files in a directory into// a single file named "combined.txt"?
#include <sys/stat.h>
#include<stdio.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<string.h>
void merge(const char *path)
{
        //open dir
        DIR *dir=opendir(path);
char file_path[256];
FILE *current_file;
     if(!dir)

    {
               perror("error");

              //      return 1;

   }

    FILE *fp=fopen("combined.txt","w");

    if(fp==NUUL)
        {
                perror("error");
                return ;
        }
        //readdir
        struct dirent *entry;
        while((entry=readdir(dir))!=NULL)
        {
                if(strcmp(entry->d_name,".")==0 ||strcmp(entry->d_name,"..")==0)continue;

                // Check if the file has a ".txt" extension

        const char *ext = strrchr(entry->d_name, '.');

if (ext && strcmp(ext, ".txt") == 0) {
         snprintf(file_path, sizeof(file_path), "%s/%s", path, entry->d_name);

            current_file = fopen(file_path, "r");
            if (!current_file) {
                perror("fopen");
                continue;
            }
            char ch;
            while((ch=fgetc(fp))!=EOF)
            {
                    fputc(ch,fp);
            }
            printf("%s",file_path);


        }
        }
int main()
{
        const char *path="temp";
        merge(path);
}

/Implement a C program to recursively calculate the total size of all files in a directoryand its subdirectories?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <unistd.h>
#include <sys/stat.h>
int size(const char *path)
{
        int total_size=0;
        //open dir
        DIR *dir=opendir(path);
        if(!dir)
        {
                perror("error");
        //      return 1;
        }
        //readdir
        struct dirent *entry;
        while((entry=readdir(dir))!=NULL)
        {
                if(strcmp(entry->d_name,".")==0 ||strcmp(entry->d_name,"..")==0)continue;
                char full[1024];
                snprintf(full,sizeof(full),"%s/%s",path,entry->d_name);
                //stat
                struct stat buf;
                if(stat(full,&buf)==-1)
                {
                        perror("state err");
                        continue;
                }
                if (S_ISDIR(buf.st_mode)) {
            // Recursively add size of subdirectory
            total_size += size(full);
        } else if (S_ISREG(buf.st_mode)) {
            // Add size of regular file
total_size += buf.st_size;
        }
        return total_size;
   // printf("%d",total_size);
        }
int main()
{
        const char *path=".";
        int n=size(path);

        printf("%d",n);
}

/Write a C program to get the number of bytes in a file named "data.bin"?
#include<stdio.h>
int main()
{
        FILE *fp=fopen("data.bin","r");
        if(fp==NULL)
        {
                perror("error");
                return 1;
        }
        fseek(fp,0,SEEK_END);
        int size=ftell(fp);
        fseek(fp,0,SEEK_SET);
        printf("%d",size);
        fclose(fp);
}

        }
}


//Develop a C program to cate a new directory named with the current timestamp in the format "YYYY-MM-DD-HH-MM-SS"?
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <sys/stat.h>
#include <sys/types.h>
int main()
{
        time_t t=time(NULL);
                struct tm *local_time=localtime(&t);
        char dir_name[100];
if (strftime(dir_name, sizeof(dir_name), "%Y-%m-%d-%H-%M-%S", local_time) == 0) {
        fprintf(stderr, "strftime failed\n");
        return 1;
    }

         if(mkdir(dir_name,0755)==0)
        {
                printf("create suc%s",dir_name);
        }
        else
        {
                perror("error craet");
        }
        printf("create directory%s",dir_name);

}
//Write a C program to create a new directory named "Documents" in the current
//directory?
#include<stdio.h>
#include<sys/stat.h>
int main()
{
        const char *name="documents";
        if(mkdir(name,0755)==0)
        {
                printf("documents created");
        }
        else
        {
                perror("not create");
        }
}

//Develop a C program to check if a file named "file.txt" exists in the current directory?
#include<stdio.h>
int main()
{
        FILE *fp=fopen("file.txt","r");
        if(fp!=NULL)
        {
                printf("file found");
        }
        else
        {
                printf("file not found");
        }
}

//Implement a C program to open a file named "data.txt" in read mode and display itscontents?
#include<stdio.h>
int main()
{
        FILE *fp;
       fp=fopen("data.txt","r");
if(fp==NULL)
{
        printf("file not");
        return 1;
}
        char ch;
while((ch=fgetc(fp))!=EOF)
{
putchar(ch);
}
}

//Develop a C program to delete a file named "delete_me.txt" from the current directory?
#include<stdio.h>
int main()
{
        const char *file="delete.txt";
        if(remove(file)==0)
        {
                printf("%s delete suc",file);
        }
        else
        {
                printf("not");
        }
}

//IImplement a C program to rename a file from "old_name.txt" to "_name.txt"?
#include<stdio.h>
int main()
{
        const char *fp="old.txt";
        const char *fp1="new.txt";
        if(rename(fp,fp1)==0)
        {
                printf("renamed");
        }
        else
        {
                perror("not");
        }
}

//Write a C program to copy the contents of one file to another?
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
        fputc(ch,fp1);
}
fclose(fp);
fclose(fp1);
}


//Develop a C program to move a file named "file.txt" to a directory named "Backup"
#include<stdio.h>
int main()
{
        const char *fp="old.txt";
        const char *fp1="backup";
        if(rename(fp,fp1)==0)
        {
                printf("renamed");
        }
        else
        {
                perror("not");
        }
}

//Implement a C program to list all files and directories in the current directory?
#include<stdio.h>
#include<dirent.h>
int main()
{
        DIR *dir=opendir(".");
        if(dir==NULL)
        {
                perror("unable to open");
                return 1;
        }
        struct dirent *entry;
        while((entry=readdir(dir))!=NULL)
        {
                printf("%s",entry->d_name);
        }
}

//Write a C program to get the size of a file named "file.txt"?
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

//Develop a C program to create a new directory named "Pictures" in the parent
//directory?
#include<stdio.h>
#include<sys/types.h>
#include<sys/stat.h>
int main()
{
        const char *direct="./pictures";
        if(mkdir(direct,0755)==0)
        {
                printf("create new dire%s",direct);
        }
        else
                printf("error");
}

//Implement a C program to count the number of lines in a file named "log.txt"?
#include<stdio.h>
int main()
{
        FILE *fp;
        int cnt=0;
        fp=fopen("log.txt","r");
        if(fp==NULL)
        {
                printf("not there");
                return 1;
        }
        char ch;
        while((ch=fgetc(fp))!=EOF)
        {
if(ch=='\n')
{
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
        FILE *fp=fopen("msg.txt","a");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        fprintf(fp,"good bye");
        fclose(fp);
}

/Write a C program to create a symbolic link named "link.txt" to a file named
//"target.txt"?
#include<stdio.h>
#include<unistd.h>
int main()
{
        const char *fp="old.txt";
        const char *fp1="link.txt";
        if(symlink(fp,fp1)==0)
        {
                printf("link created %s %s",fp,fp1);
        }
        else
        {
                perror("link not create");
        }
}

/Implement a C program to change the permissions of a file named "file.txt" to read-
//only?
#include<stdio.h>
#include<sys/types.h>
#include<sys/stat.h>
int main()
{
        const char *name="file.txt";
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
        const char *filename="file.txt";
        const char *username="hi";
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


/Write a C program to create a new text file named "notes.txt" and write multiple lines of
//text to it?
#include<stdio.h>
#include<unistd.h>
int main()
{
        FILE * fp=fopen("notes.txt","w");
        if(fp==NULL)
        {
                perror("error");
                return 1;
        }
        int n;
        char line[100];
        printf("enter num of line");
        scanf("%d",&n);
        for(int i=0;i<n;i++)
        {
                printf("entrr lene%d\n",i+1);
                fgets(line,sizeof(line),stdin );
                fputs(line,fp);
        }
}

/Develop a C program to count the number of words in a file named "essay.txt"?
#include<stdio.h>
#include<unistd.h>
int main()
{
        FILE *fp=fopen("essay.txt","r");
        int worcnt=0;
        char ch;
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
while((ch=fgetc(fp))!=EOF)
{
        if((ch==' ')||(ch=='\n'))
        {
                worcnt++;
        }
}
printf("%d",worcnt);//Write a C program to create a symbolic link named "link.txt" to a file named
//"target.txt"?
#include<stdio.h>
#include<unistd.h>
int main()
{
        const char *fp="old.txt";
        const char *fp1="link.txt";
        if(symlink(fp,fp1)==0)
        {
                printf("link created %s %s",fp,fp1);
        }
        else
        {
                perror("link not create");
        }
}

}

/Develop a C program to change the permissions of a file named "important.doc" t readand write for the owner only?
#include<stdio.h>
#include<sys/stat.h>
int main()
{
        const char *file="important.doc";
        int result=chmod(file,S_IRUSR|S_IWUSR);
        if(result==0)
        {
                printf("change permissions");

        }
        else
        {
                printf("not");
        }
}

//Develop a C program to create a new directory named with the current timestamp in the format "YYYY-MM-DD-HH-MM-SS"?
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <sys/stat.h>
#include <sys/types.h>
int main()
{
        struct stat filestat;
        if (stat("data.txt", &filestat) == -1) {
        perror("Error retrieving file status");
        return 1;
    }
                struct tm *local_time=localtime(&filestat.st_atime);
        char dir_name[100];
if (strftime(dir_name, sizeof(dir_name), "%Y-%m-%d-%H-%M-%S", local_time) == 0) {
       perror("error");
       return 1;
}
        printf("create directory%s",dir_name);

        }

/Write a C program to e/23. Implement a C program to read and display the contents of a CSV file named
//"data.csv"?
#include<stdio.h>
#include<string.h>
int main()
{
        FILE *fp=fopen("dummy.csv","r");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        char ch;
        char buf[100];
        while(fgets(buf,sizeof(buf),fp))
        {
                char *tok=strtok(buf,",");


 while(tok!=NULL)
        {

        printf("%s",tok);
tok=strtok(NULL,",");
//      fclose(fp);
}
}
}

/ Write a C program to truncate a file named "file.txt" to a specified lengt
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>
int main()
{
        const char *filename="dummy.c";
        int length=100;
        int fd=open(filename,O_RDWR);
        if(fd==-1)
        {
                perror("error");
                return 1;
        }
        if(ftruncate(fd,length)==-1)
        {
                perror("error trunc");
                return 1;

        }
        printf("file truncated %s %d bytes",filename,length);
}

/Develop a C program to search for a specific string in a file named "data.txt" and
//display the line number(s) where it occurs?
#include<stdio.h>
#include<string.h>
int main()
{
         FILE *fp;
         const char *filename="dummy.c";
         char search[100];
         char line[100];
         int linenum=0;
         printf("enter string");
         fgets(search,sizeof(search)-1,stdin);

fp=fopen(filename,"r");
if(fp==NULL)
{
        printf("not found");
        return 1;
}
while(fgets(line,sizeof(line),fp))
{
        linenum++;

if(strstr(line,search)!=NULL)
{
        printf("%d%s",linenum,line);
}
}


}

//mplement a C program to get the file type (regular file, directory, symbolic link, etc.) of
//a given path?
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <unistd.h>
int main()
{
        struct stat pathstat;
        char path[100];
        printf("enter the path");
        fgets(path,sizeof(path)-1,stdin);
        if(stat(path,&pathstat)==-1)
        {
                perror("not status");
                return 1;
        }
         if(S_ISREG(pathstat.st_mode))
        {
                printf("%s regule",path);
        }
        else if(S_ISDIR(pathstat.st_mode))
        {
                printf("%s dir",path);
        }
       else  if(S_ISLNK(pathstat.st_mode))
        {
                printf("%s link",path);
        }
        else
        {
                printf("unknown");
        }
}

/Write a C program to read and display the contents of a binary file named "binary.bin"?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        FILE *fp=fopen("dummy.bin","r");
        if(fp==NULL)
        {
                printf("not create");
                return 1;
        }
        char buf[100];
        int byte;
        while(byte=fread(buf,1,sizeof(buf),fp)>0)
        {
                for(int i=0;i<byte;i++)
                {
                printf("%02x",buf[i]);
                }
        }
}

/evelop a C program to check if a file named "config.ini" is writable?
#include<stdio.h>
int main()
{
        FILE *fp=fopen("dummy.c","r");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        printf("readable file");
        FILE *fp1=fopen("config.ini","w");
        char ch;
        while((ch=fgetc(fp))!=EOF)
        {
                fputc(ch,fp1);
        }
        if(fp1==NULL)
        {
                printf("error");
                return 1;
        }
        printf("write  file");

        fclose(fp);
        fclose(fp1);
}

/Implement a C program to read the contents of a text file named "instructions.txt" and execute the instructions as shell commands?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        FILE *fp=fopen("instructions.txt","r");
        if(fp==NULL)
        {
                printf("error");
                return 1;
        }
        //printf("readable file");
        char command[256];
        while(fgets(command,sizeof(command)-1,fp))
        {
                if(command[0]=='\0' || command[0]=='#')
                        continue;
        }
        int status=system(command);
        if(status==-1)
        {
                perror("error exe");
        }
        else
                printf("execute=%s",command);
}
/Write a C program to read and display the contents of a binary file named "binary.bin" display in hexadecimal?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        FILE *fp=fopen("dummy.bin","r");
        size_t offset=0;
        if(fp==NULL)
        {
                printf("not create");
                return 1;
        }
        char buf[100];
        int byte;
        while(byte=fread(buf,1,sizeof(buf),fp)>0)
        {
                printf("%08zx",offset);
                for(int i=0;i<byte;i++)
                {
                printf("%02x",buf[i]);
                }
        for(int i = byte; i < sizeof(buf); i++) {
            printf("   ");
        }

        printf(" |");
        for (int i = 0; i < byte; i++) {
            printf("%c", (buf[i] >= 32 && buf[i] <= 126) ? buf[i] : '.');
        }
        printf("|\n");

        offset += byte;
        }
}
~      
```

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main() {
pid_t pid;
pid = vfork();
if (pid == -1) {
perror("vfork");
return 1;
} 
else if (pid == 0) {  
printf("Child process: Hello, I'm the child!\n");
printf("Child process: My PID is %d\n", getpid());
printf("Child process: My parent's PID is %d\n", getppid()); 
_exit(0);
} 
else {  
printf("Parent process: Hello, I'm the parent!\n");
printf("Parent process: My PID is %d\n", getpid());
printf("Parent process: My child's PID is %d\n", pid);

int status;
waitpid(pid, &status, 0);
if (WIFEXITED(status)) {
printf("Parent process: Child process terminated normally.\n");
} 
else {
printf("Parent process: Child process terminated abnormally.\n");
}
}
return 0;
}



#include <stdio.h>
#include <fcntl.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>
int main()
{
int fd;
char * myfifo = "/tmp/myfifo"; 
mkfifo(myfifo, 0666);
fd = open(myfifo, O_WRONLY);
write(fd,"Hi", sizeof("Hi")); 
close(fd);
unlink(myfifo); 
return 0;
}



#include <fcntl.h>
#include <sys/stat.h>
#include <stdio.h>
#include <unistd.h>
#define MAX_BUF 1024
int main()
{
int fd;
char *myfifo = "/tmp/myfifo";
char buf[MAX_BUF];
fd = open(myfifo, O_RDONLY);
read(fd, buf, MAX_BUF);
printf("Received: %6s", buf);
close(fd);
return 0;
}






```

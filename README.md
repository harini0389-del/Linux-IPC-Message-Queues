# Linux-IPC-Message-Queues
Linux IPC-Message Queues

# AIM:
To write a C program that receives a message from message queue and display them

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux message queues API 

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## C program that receives a message from message queue and display them

```
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <string.h>

struct message
{
    long type;
    char text[100];
};

int main()
{
    key_t key = 1234;
    int msgid;
    struct message msg;

    msgid = msgget(key, IPC_CREAT | 0666);

    if (msgid == -1)
    {
        perror("msgget");
        return 1;
    }

    msg.type = 1;
    strcpy(msg.text, "Hello from Message Queue");

    if (msgsnd(msgid, &msg, sizeof(msg.text), 0) == -1)
    {
        perror("msgsnd");
        return 1;
    }

    printf("Message sent: %s\n", msg.text);

    if (msgrcv(msgid, &msg, sizeof(msg.text), 1, 0) == -1)
    {
        perror("msgrcv");
        return 1;
    }

    printf("Message received: %s\n", msg.text);

    if (msgctl(msgid, IPC_RMID, NULL) == -1)
    {
        perror("msgctl");
        return 1;
    }

    return 0;
}
```

## OUTPUT
<img width="657" height="142" alt="image" src="https://github.com/user-attachments/assets/f5a12c77-840e-4872-96ff-edfa2c0b995c" />

# RESULT:
The programs are executed successfully.

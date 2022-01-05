# 使用 C 语言中的套接字编程对数组进行排序

> 原文:[https://www . geesforgeks . org/sort-array-use-socket-programming/](https://www.geeksforgeeks.org/sort-array-using-socket-programming/)

给定一个未排序的正整数数组，使用[套接字编程](https://www.geeksforgeeks.org/socket-programming-cc/)对给定数组进行排序。

示例:

```
Input : 4 5 6 1 8 2 7 9 3 0 
Output :0 1 2 3 4 5 6 7 8 9

Input : 9 8 1 4 0
Output : 0 1 4 8 9

```

使用 **gcc** 命令(gcc client.c -o client 和 gcc server.c -o server)编译这些文件。使用**运行程序。/服务器**和**。/client** (请注意:首先要运行服务器程序，等待客户端的响应，然后是客户端代码)。

在这个程序中，客户端将获取输入并将其发送给服务器，服务器将使用冒泡排序对数组进行排序。

```
// Client code in C to sort the array
#include <arpa/inet.h>
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>

// Driver code
int main(int argc, char* argv[])
{
    int sock;
    struct sockaddr_in server;
    int server_reply[10];
    int number[10] = { 5, 4, 3, 8, 9, 1, 2, 0, 6 }, i, temp;

    // Create socket
    sock = socket(AF_INET, SOCK_STREAM, 0);
    if (sock == -1) {
        printf("Could not create socket");
    }
    puts("Socket created");

    server.sin_addr.s_addr = inet_addr("127.0.0.1");
    server.sin_family = AF_INET;
    server.sin_port = htons(8880);

    // Connect to remote server
    if (connect(sock, (struct sockaddr*)&server, sizeof(server)) < 0) {
        perror("connect failed. Error");
        return 1;
    }

    puts("Connected\n");

    if (send(sock, &number, 10 * sizeof(int), 0) < 0) {
        puts("Send failed");
        return 1;
    }

    // Receive a reply from the server
    if (recv(sock, &server_reply, 10 * sizeof(int), 0) < 0) {
        puts("recv failed");
        return 0;
    }

    puts("Server reply :\n");
    for (i = 0; i < 10; i++) {
        printf("%d\n", server_reply[i]);
    }

    // close the socket
    close(sock);
    return 0;
}
```

**注:**将上述文件保存为客户端

```
// Server code in C to sort the array
#include <arpa/inet.h>
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>

void bubble_sort(int[], int);

// Driver code
int main(int argc, char* argv[])
{
    int socket_desc, client_sock, c, read_size;
    struct sockaddr_in server, client;
    int message[10], i;

    // Create socket
    socket_desc = socket(AF_INET, SOCK_STREAM, 0);
    if (socket_desc == -1) {
        printf("Could not create socket");
    }
    puts("Socket created");

    // Prepare the sockaddr_in structure
    server.sin_family = AF_INET;
    server.sin_addr.s_addr = INADDR_ANY;
    server.sin_port = htons(8880);

    // Bind the socket
    if (bind(socket_desc, (struct sockaddr*)&server, sizeof(server)) < 0) {

        // print the error message
        perror("bind failed. Error");
        return 1;
    }
    puts("bind done");

    // lsiten to the socket
    listen(socket_desc, 3);

    puts("Waiting for incoming connections...");
    c = sizeof(struct sockaddr_in);

    // accept connection from an incoming client
    client_sock = accept(socket_desc, (struct sockaddr*)&client, (socklen_t*)&c);

    if (client_sock < 0) {
        perror("accept failed");
        return 1;
    }

    puts("Connection accepted");

    // Receive a message from client
    while ((read_size = recv(client_sock, &message, 10 * sizeof(int), 0)) > 0) {

        bubble_sort(message, 10);

        write(client_sock, &message, 10 * sizeof(int));
    }

    if (read_size == 0) {
        puts("Client disconnected");
    }
    else if (read_size == -1) {
        perror("recv failed");
    }

    return 0;
}

// Function to sort the array
void bubble_sort(int list[], int n)
{
    int c, d, t;

    for (c = 0; c < (n - 1); c++) {
        for (d = 0; d < n - c - 1; d++) {
            if (list[d] > list[d + 1]) {

                /* Swapping */
                t = list[d];
                list[d] = list[d + 1];
                list[d + 1] = t;
            }
        }
    }
}
```

**注意:**将以上文件保存为 server.c
**输出:**

```
0 1 2 3 4 5 6 7 8 9 

```
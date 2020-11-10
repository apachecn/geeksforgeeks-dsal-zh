# 使用循环调度

> 原文：[https://www.geeksforgeeks.org/calculate-server-loads-using-round-robin-scheduling/](https://www.geeksforgeeks.org/calculate-server-loads-using-round-robin-scheduling/)

计算服务器负载

给定`M`个服务器，它们处理具有无限计算能力的多个请求，并且数组**到达时间[]** 和`processTime[]`的大小为`N`，以下列方式表示到达`N`个请求的时间和加载时间：

*   每个服务器的编号从 **0** 到`M – 1`，并且以严格的时间顺序给出请求。

*   通过以下方式将每个请求`i`分配给其中一个服务器：

    *   选择第`i % m`个服务器。 如果所选服务器是空闲的，则将请求分配给服务器。

    *   否则，请选择下一个可用的服务器。 如果没有可用的服务器，则该请求将被丢弃。

考虑到每个服务器一次只能处理一个请求，因此任务是在处理所有传入请求之后查找每个服务器上的负载，因为每个服务器上的负载就是它处理的请求数。

**示例**：

> **输入**：`N = 4, M = 3, arriveTime[] = {1, 3, 6, 8}, processTime[] = {1,2,2,1}`
>
> **输出** ：
>
> ```
> 1st server -> 2
> 2nd server -> 1
> 3rd server -> 1
> ```
> 
> **说明**：
> 
> 将第一个和第四个请求分配给第一个服务器。
> 
> 将第二请求分配给第二服务器，将第三请求分配给第三服务器。
> 
> 以下是转换表：
> 
> 
> | 申请号码 | 到达时间 | 加载时间 | 时间结束 | 可用服务器 | 需求服务器 | 分配的服务器 |
> | --- | --- | --- | --- | --- | --- | --- |
> | 0 | 1 | 1 | 2 | 0, 1, 2 | 0 | 0 |
> | 1 | 3 | 2 | 5 | 0, 1, 2 | 1 | 1 |
> | 2 | 6 | 2 | 8 | 0, 1, 2 | 2 | 2 |
> | 3 | 8 | 1 | 9 | 0, 1, 2 | 1 | 1 |
> 
> 
> **输入**：`N = 4, M = 2, arriveTime[] = {1, 2, 4, 6}, processTime[] = {7, 1, 4, 4}`
> 
> **输出**：
> 
> ```
> 1st server -> 1
> 2nd server -> 2
> ```
> 
> **说明**：
> 
> 第一个请求分配给第一个服务器，第二个请求分配给第二个服务器 。
> 
> 第三个请求被分配给第二个服务器。 第三个请求的请求服务器是第一个服务器，但是由于在请求到达时它很忙，因此
>
> 因此将第二个服务器分配给它。
>
> 由于两个服务器在到达时都处于繁忙状态，因此删除了第四个请求。
>
> 以下是转换表：
> 
> 
> | 申请号码 | 到达时间 | 加载时间 | 时间结束 | 可用服务器 | 需求服务器 | 分配的服务器 |
> | --- | --- | --- | --- | --- | --- | --- |
> | 0 | 1 | 7 | 8 | 0, 1 | 0 | 0 |
> | 1 | 2 | 1 | 3 | 1 | 1 | 1 |
> | 2 | 4 | 4 | 8 | 1 | 0 | 1 |
> | 3 | 6 | 4 | 10 | – | 1 | – |


**方法**：这个想法是使用[最小优先级队列](https://www.geeksforgeeks.org/implement-min-heap-using-stl/)和[集](https://www.geeksforgeeks.org/set-in-cpp-stl/)。 [优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)保留繁忙服务器的计数，并在空闲时帮助释放它们。 [设置](https://www.geeksforgeeks.org/set-in-java/)用于维护可用服务器的数据，以将它们分配给传入的请求。 步骤如下：

*   初始化辅助数组`loadOnServer[]`，该数组将在每个服务器上存储负载。

*   通过对每个请求添加**到达时间**和**处理时间**，遍历传入的请求并找到每个请求的结束时间。

*   从结束时间已经超过当前结束时间的**优先级队列**中弹出繁忙的服务器。

*   如果可用服务器集为空，请删除当前请求。

*   现在，使用[下界函数](https://www.geeksforgeeks.org/set-lower_bound-function-in-c-stl/)搜索集合中的第`i % m`服务器，如果下界迭代器指向该集合的末尾，然后选择集合中的第一台服务器。

*   完成上述步骤后，增加所选服务器上的负载计数器。

*   完成上述步骤后，在`loadOnServer[]`中打印所有负载的存储。

下面是上述方法的实现：

## C++

```cpp

// C++ Program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print load on each server 
void printLoadOnEachServer( 
    int m, int loadOnServer[]) 
{ 
    // Traverse the loadOnServer and 
    // print each loads 
    for (int i = 0; i < m; i++) { 

        cout << i + 1 << "st Server -> "
             << loadOnServer[i] << ".\n"; 
    } 
} 

// Function for finding the load 
// on each server 
void loadBalancing(int n, int m, 
                   int arrivalTime[], 
                   int processTime[]) 
{ 
    // Stores the load on each Server 
    int loadOnServer[m]; 

    for (int i = 0; i < m; i++) { 

        // Initialize load on each 
        // server as zero 
        loadOnServer[i] = 0; 
    } 

    // Minimum priority queue for 
    // storing busy servers according 
    // to their release time 
    priority_queue<pair<int, int>, 
                   vector<pair<int, int> >, 
                   greater<pair<int, int> > > 
        busyServers; 

    // Set to store available Servers 
    set<int> availableServers; 

    for (int i = 0; i < m; i++) { 

        // Initally, all servers are free 
        availableServers.insert(i); 
    } 

    // Iterating through the requests. 
    for (int i = 0; i < n; i++) { 

        // End time of current request 
        // is the sum of arrival time 
        // and process time 
        int endTime = arrivalTime[i] 
                      + processTime[i]; 

        // Releasing all the servers which 
        // have become free by this time 
        while (!busyServers.empty() 
               && busyServers.top().first 
                      <= arrivalTime[i]) { 

            // Pop the server 
            pair<int, int> releasedServer 
                = busyServers.top(); 
            busyServers.pop(); 

            // Insert available server 
            availableServers.insert( 
                releasedServer.second); 
        } 

        // If there is no free server, 
        // the request is dropped 
        if ((int)availableServers.empty()) { 
            continue; 
        } 

        int demandedServer = i % m; 

        // Searching for demanded server 
        auto itr 
            = availableServers.lower_bound( 
                demandedServer); 

        if (itr == availableServers.end()) { 

            // If demanded Server is not free 
            // and no server is free after it, 
            // then choose first free server 
            itr = availableServers.begin(); 
        } 

        int assignedServer = *itr; 

        // Inceasing load on assigned Server 
        loadOnServer[assignedServer]++; 

        // Removing assigned server from list 
        // of assigned servers 
        availableServers.erase(assignedServer); 

        // Add assigned server in the list of 
        // busy servers with its release time 
        busyServers.push({ endTime, 
                           assignedServer }); 
    } 

    // Function to print load on each server 
    printLoadOnEachServer(m, loadOnServer); 
} 

// Driver Code 
int main() 
{ 
    // Given arrivalTime and processTime 
    int arrivalTime[] = { 1, 2, 4, 6 }; 
    int processTime[] = { 7, 1, 4, 4 }; 

    int N = sizeof(arrivalTime) 
            / sizeof(int); 

    int M = 2; 

    // Function Call 
    loadBalancing(N, M, arrivalTime, 
                  processTime); 

    return 0; 
} 

```

**输出**：

```
1st Server -> 1.
2st Server -> 2.

```

**时间复杂度**：`O(N * log M)`

**辅助空间**：`O(M)`



* * *

* * *




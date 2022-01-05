# 优先 CPU 调度程序

> 原文:[https://www . geesforgeks . org/program-for-premium-CPU-scheduling/](https://www.geeksforgeeks.org/program-for-preemptive-priority-cpu-scheduling/)

实现优先级 CPU 调度。在这个问题中，我们使用 [Min Heap](https://www.geeksforgeeks.org/binary-heap/) 作为实现优先级调度的数据结构。
**在这个问题中，较小的数字表示较高的优先级。**
下面给出的代码中使用了以下功能:

```
struct process {
   processID,
   burst time,
   response time,
   priority,
   arrival time.
} 
```

**void quicksort(进程数组[]，低，高)**–该功能用于按照进程到达时间升序排列进程。
**int partition(process array[]，int low，int high)**–该函数用于对数组进行分区排序。
**void insert(process Heap[]，process value，int *heapsize，int * current time)**–用于包含堆中所有有效且合格的进程以供执行。heapsize 根据当前时间定义正在执行的进程数 current time 记录当前 CPU 时间。
**void order(process Heap[]，int *heapsize，int start)**–用于在插入新进程后，如果有进程，则根据优先级对堆进行重新排序。
**void extractminimum(进程 Heap[]，int *heapsize，int * current time)**–此函数用于从堆中查找优先级最高的进程。它还在提取最高优先级的进程后对堆进行重新排序。
**无效调度(进程堆[]，进程数组[]，int n，int *heapsize，int * current time)**–该函数负责执行从堆[]中提取的最高优先级。
**void process(process array[]，int n)**–该功能负责根据进程到达时间管理进程到达 CPU 时的整个执行。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to implement preemptive priority scheduling
#include <bits/stdc++.h>
using namespace std;

struct Process {
    int processID;
    int burstTime;
    int tempburstTime;
    int responsetime;
    int arrivalTime;
    int priority;
    int outtime;
    int intime;
};

// It is used to include all the valid and eligible
// processes in the heap for execution. heapsize defines
// the number of processes in execution depending on
// the current time currentTime keeps a record of
// the current CPU time.
void insert(Process Heap[], Process value, int* heapsize,
            int* currentTime)
{
    int start = *heapsize, i;
    Heap[*heapsize] = value;
    if (Heap[*heapsize].intime == -1)
        Heap[*heapsize].intime = *currentTime;
    ++(*heapsize);

    // Ordering the Heap
    while (start != 0 && Heap[(start - 1) / 2].priority >
                                  Heap[start].priority) {
        Process temp = Heap[(start - 1) / 2];
        Heap[(start - 1) / 2] = Heap[start];
        Heap[start] = temp;
        start = (start - 1) / 2;
    }
}

// It is used to reorder the heap according to
// priority if the processes after insertion
// of new process.
void order(Process Heap[], int* heapsize, int start)
{
    int smallest = start;
    int left = 2 * start + 1;
    int right = 2 * start + 2;
    if (left < *heapsize && Heap[left].priority <
                            Heap[smallest].priority)
        smallest = left;
     if (right < *heapsize && Heap[right].priority <
                           Heap[smallest].priority)
        smallest = right;

    // Ordering the Heap
    if (smallest != start) {
        Process temp = Heap[smallest];
        Heap[smallest] = Heap[start];
        Heap[start] = temp;
        order(Heap, heapsize, smallest);
    }
}

// This function is used to find the process with
// highest priority from the heap. It also reorders
// the heap after extracting the highest priority process.
Process extractminimum(Process Heap[], int* heapsize,
                       int* currentTime)
{
    Process min = Heap[0];
    if (min.responsetime == -1)
        min.responsetime = *currentTime - min.arrivalTime;
    --(*heapsize);
    if (*heapsize >= 1) {
        Heap[0] = Heap[*heapsize];
        order(Heap, heapsize, 0);
    }
    return min;
}

// Compares two intervals according to starting times.
bool compare(Process p1, Process p2)
{
    return (p1.arrivalTime < p2.arrivalTime);
}

// This function is responsible for executing
// the highest priority extracted from Heap[].
void scheduling(Process Heap[], Process array[], int n,
                int* heapsize, int* currentTime)
{
    if (heapsize == 0)
        return;

    Process min = extractminimum(Heap, heapsize, currentTime);
    min.outtime = *currentTime + 1;
    --min.burstTime;
    printf("process id = %d current time = %d\n",
           min.processID, *currentTime);

    // If the process is not yet finished
    // insert it back into the Heap*/
    if (min.burstTime > 0) {
        insert(Heap, min, heapsize, currentTime);
        return;
    }

    for (int i = 0; i < n; i++)
        if (array[i].processID == min.processID) {
            array[i] = min;
            break;
        }
}

// This function is responsible for
// managing the entire execution of the
// processes as they arrive in the CPU
// according to their arrival time.
void priority(Process array[], int n)
{
    sort(array, array + n, compare);

    int totalwaitingtime = 0, totalbursttime = 0,
        totalturnaroundtime = 0, i, insertedprocess = 0,
        heapsize = 0, currentTime = array[0].arrivalTime,
        totalresponsetime = 0;

    Process Heap[4 * n];

    // Calculating the total burst time
    // of the processes
    for (int i = 0; i < n; i++) {
        totalbursttime += array[i].burstTime;
        array[i].tempburstTime = array[i].burstTime;
    }

    // Inserting the processes in Heap
    // according to arrival time
    do {
        if (insertedprocess != n) {
            for (i = 0; i < n; i++) {
                if (array[i].arrivalTime == currentTime) {
                    ++insertedprocess;
                    array[i].intime = -1;
                    array[i].responsetime = -1;
                    insert(Heap, array[i], &heapsize, ¤tTime);
                }
            }
        }
        scheduling(Heap, array, n, &heapsize, ¤tTime);
        ++currentTime;
        if (heapsize == 0 && insertedprocess == n)
            break;
    } while (1);

    for (int i = 0; i < n; i++) {
        totalresponsetime += array[i].responsetime;
        totalwaitingtime += (array[i].outtime - array[i].intime -
                                         array[i].tempburstTime);
        totalbursttime += array[i].burstTime;
    }
    printf("Average waiting time = %f\n",
           ((float)totalwaitingtime / (float)n));
    printf("Average response time =%f\n",
           ((float)totalresponsetime / (float)n));
    printf("Average turn around time = %f\n",
           ((float)(totalwaitingtime + totalbursttime) / (float)n));
}

// Driver code
int main()
{
    int n, i;
    Process a[5];
    a[0].processID = 1;
    a[0].arrivalTime = 4;
    a[0].priority = 2;
    a[0].burstTime = 6;
    a[1].processID = 4;
    a[1].arrivalTime = 5;
    a[1].priority = 1;
    a[1].burstTime = 3;
    a[2].processID = 2;
    a[2].arrivalTime = 5;
    a[2].priority = 3;
    a[2].burstTime = 1;
    a[3].processID = 3;
    a[3].arrivalTime = 1;
    a[3].priority = 4;
    a[3].burstTime = 2;
    a[4].processID = 5;
    a[4].arrivalTime = 3;
    a[4].priority = 5;
    a[4].burstTime = 4;
    priority(a, 5);
    return 0;
}
```

**Output:** 

```
process id = 3 current time = 1
process id = 3 current time = 2
process id = 5 current time = 3
process id = 1 current time = 4
process id = 4 current time = 5
process id = 4 current time = 6
process id = 4 current time = 7
process id = 1 current time = 8
process id = 1 current time = 9
process id = 1 current time = 10
process id = 1 current time = 11
process id = 1 current time = 12
process id = 2 current time = 13
process id = 5 current time = 14
process id = 5 current time = 15
process id = 5 current time = 16
Average waiting time = 4.400000
Average response time =1.600000
Average turn around time = 7.200000
```

输出显示了进程在内存中的执行顺序，还显示了每个进程的平均等待时间、平均响应时间和平均周转时间。
本文由 [**哈迪克·高尔**](https://www.linkedin.com/in/hardik-gaur-135891122/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
# 使用优先级队列实现非抢占式最短作业优先

> 原文:[https://www . geesforgeks . org/实现非抢占式最短作业优先使用优先级队列/](https://www.geeksforgeeks.org/implementation-of-non-preemptive-shortest-job-first-using-priority-queue/)

阅读此处了解相同到达时间的[最短作业优先调度算法](https://www.geeksforgeeks.org/program-for-shortest-job-first-or-sjf-cpu-scheduling-set-1-non-preemptive/)。
最短作业优先(SJF)或最短作业其次，是一种调度策略，它选择执行时间最小的等待进程来执行下一个任务。
在本文中，我们将使用优先级队列实现最短作业优先调度算法(SJF)，这样我们就可以处理不同到达时间的流程。
**例:**

```
Input:  The processes are
Process id    Arrival time    Burst time    
    p1         4                  3        
    p2         0                  8        
    p3         5                  4        
    p4         9                  2    

Output: Process scheduling according to SJF is
Process id    Arrival time    Burst time    
    p2         0                  8        
    p1         4                  3        
    p4         9                  2        
    p3         5                  4    

Input: The processes are
Process id    Arrival time    Burst time    
    p1         0                  3        
    p2         0                  8        
    p3         5                  4        
    p4         9                  2

Output: Process scheduling according to SJF is
Process id    Arrival time    Burst time    
    p1         0                  3        
    p2         0                  8        
    p4         9                  2        
    p3         5                  4    
```

在该程序中，任务是根据 SJF 调度算法调度进程，该算法规定具有最小突发时间的进程将被赋予优先级，这可以简单地通过按升序排序进程的突发时间来实现。当我们必须在不同的到达时间处理进程时，问题就出现了，那么我们就不能简单地根据突发时间对进程进行排序，因为我们需要考虑进程的到达时间，这样处理器就不会闲置。
**例:**
如果突发时间较多的进程先于突发时间较少的进程到达，那么我们必须给最先到达的进程留出处理器时间，这样处理器才不会闲置。
**进场:**
处理到达时间不同的工序，如遇 SJF 调度:

*   首先，根据到达时间对流程进行排序。
*   维护一个等待队列，使突发时间最短的进程保持在最前面。
*   保持当前运行时间，即已执行进程的突发时间总和。
    *   一个进程根据它的到达时间进入等待队列，如果一个新进程的到达时间小于
        等于当前运行时间，它将被推入等待队列。
    *   当要执行一个进程时，它会从等待队列中弹出。它的突发时间被添加到当前运行时间，它的到达时间被更新为-1，这样它就不会再次进入等待队列。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of SJF
#include <bits/stdc++.h>
using namespace std;

// number of process
#define SIZE 4

// Structure to store the
// process information
typedef struct proinfo {
    string pname; // process name
    int atime; // arrival time
    int btime; // burst time

} proinfo;

// This structure maintains the
// wait queue, using burst
// time to compare.
typedef struct cmpBtime {
    int operator()(const proinfo& a,
                   const proinfo& b)
    {
        return a.btime > b.btime;
    }
} cmpBtime;

// This function schedules the
// process according to the SJF
// scheduling algorithm.
void sjfNonpremetive(proinfo* arr)
{
    // Used to sort the processes
    // according to arrival time
    int index = 0;
    for (int i = 0; i < SIZE - 1; i++) {
        index = i;
        for (int j = i + 1; j < SIZE; j++) {
            if (arr[j].atime
                < arr[index].atime) {
                index = j;
            }
        }
        swap(arr[i], arr[index]);
    }

    // ctime stores the current run time
    int ctime = arr[0].atime;

    // priority queue, wait, is used
    // to store all the processes that
    // arrive <= ctime (current run time)
    // this is a minimum priority queue
    // that arranges values according to
    // the burst time of the processes.
    priority_queue<proinfo, vector<proinfo>,
                   cmpBtime>
        wait;

    int temp = arr[0].atime;

    // The first process is
    // pushed in the wait queue.
    wait.push(arr[0]);
    arr[0].atime = -1;

    cout << "Process id"
         << "\t";
    cout << "Arrival time"
         << "\t";
    cout << "Burst time"
         << "\t";

    cout << endl;

    while (!wait.empty()) {

        cout << "\t";
        cout << wait.top().pname << "\t\t";
        cout << wait.top().atime << "\t\t";
        cout << wait.top().btime << "\t\t";
        cout << endl;

        // ctime is increased with
        // the burst time of the
        // currently executed process.
        ctime += wait.top().btime;

        // The executed process is
        // removed from the wait queue.
        wait.pop();

        for (int i = 0; i < SIZE; i++) {
            if (arr[i].atime <= ctime
                && arr[i].atime != -1) {
                wait.push(arr[i]);

                // When the process once
                // enters the wait queue
                // its arrival time is
                // assigned to -1 so that
                // it doesn't enter again
                // int the wait queue.
                arr[i].atime = -1;
            }
        }
    }
}

// Driver Code
int main()
{
    // an array of process info structures.
    proinfo arr[SIZE];

    arr[0] = { "p1", 4, 3 };
    arr[1] = { "p2", 0, 8 };
    arr[2] = { "p3", 5, 4 };
    arr[3] = { "p4", 9, 2 };

    cout << "Process scheduling ";
    cout << "according to SJF is: \n"
         << endl;

    sjfNonpremetive(arr);
}
```

## 蟒蛇 3

```
# Python 3 implementation of SJF
import heapq as hq
# number of process
SIZE=4

# This function schedules the
# process according to the SJF
# scheduling algorithm.
def sjfNonpremetive(arr):
    # Used to sort the processes
    # according to arrival time
    index = 0
    for i in range(SIZE - 1):
        index = i
        for j in range(i + 1, SIZE) :
            if (arr[j][1] < arr[index][1]) :
                index = j

        arr[i], arr[index]=arr[index],arr[i]

    # ctime stores the current run time
    ctime = arr[0][1]

    # priority queue, wait, is used
    # to store all the processes that
    # arrive <= ctime (current run time)
    # this is a minimum priority queue
    # that arranges values according to
    # the burst time of the processes.
    wait=[]

    temp = arr[0][1]

    # The first process is
    # pushed in the wait queue.
    hq.heappush(wait,arr[0].copy())
    arr[0][1] = -1

    print("Process id",end="\t")
    print("Arrival time",end="\t")
    print("Burst time",end="\t")

    print()

    while (wait) :

        print(end="\t")
        print(wait[0][2],end= "\t\t")
        print(wait[0][1],end="\t\t")
        print(wait[0][0],end="\t\t")
        print()

        # ctime is increased with
        # the burst time of the
        # currently executed process.
        ctime += wait[0][0]

        # The executed process is
        # removed from the wait queue.
        hq.heappop(wait)

        for i in range(SIZE):
            if (arr[i][1] <= ctime
                and arr[i][1] != -1) :
                hq.heappush(wait,arr[i].copy())

                # When the process once
                # enters the wait queue
                # its arrival time is
                # assigned to -1 so that
                # it doesn't enter again
                # int the wait queue.
                arr[i][1] = -1

# Driver Code
if __name__ == '__main__':
    # an array of process info structures.
    arr=[None]*SIZE

    arr[0] =[3, 4, "p1"]
    arr[1] = [8, 0, "p2"]
    arr[2] = [4, 5, "p3"]
    arr[3] = [2, 9, "p4"]

    print("Process scheduling according to SJF is: \n")

    sjfNonpremetive(arr)
```

**Output:** 

```
Process scheduling according to SJF is: 

Process id    Arrival time    Burst time    
    p2         0                8        
    p1         4                3        
    p4         9                2        
    p3         5                4
```

**时间复杂度:** O(N^2).
**辅助空间** : O(N)。
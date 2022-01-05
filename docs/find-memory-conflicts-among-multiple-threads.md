# 发现多线程间内存冲突

> 原文:[https://www . geeksforgeeks . org/find-memory-multi-threads 冲突/](https://www.geeksforgeeks.org/find-memory-conflicts-among-multiple-threads/)

考虑一个按块组织的内存。系统上运行着多个进程。每个应用程序都会获得以下信息。

(线程 T，内存块 M，时间 T，读/写)，它本质上告诉线程 T 在时间 T 正在使用内存块 M，操作可以是读或写。

内存冲突定义为–
–同一位置的多个读取操作不会导致冲突。
–在 x+5 到 x-5 到位置 M 之间的一次写操作，将是线程在时间 x 访问位置 M 的冲突原因，其中 x 是标准时间测量单位中的某个时间。
–示例–如果线程 T1 在时间 x+1 访问了内存位置 M，并且如果线程 T2 在时间 x+6 之前访问了位置 M，那么 T1 和 T2 是冲突的候选对象，因为其中一个线程执行了写操作。

给你一个访问内存位置的线程列表，你必须找到所有的冲突。

例子

```
Input:
  (1, 512, 1, R)
  (2, 432, 2, W)
  (3, 512, 3, R)
  (4, 932, 4, R)
  (5, 512, 5, W)
  (6, 932, 6, R)
  (7, 835, 7, R)
  (8, 432, 8, R)

Output:
Thread 1 & 3 conflict with thread 5
All other operations are safe. 
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
这个想法是按内存块对所有线程进行排序，如果内存块相同，则按时间排序。一旦我们对所有线程进行了排序，我们就可以逐个遍历所有线程。对于每个被遍历的线程，我们只需要检查同一个块的先前相邻线程，因为线程是按时间排序的。

下面是这个想法的 C++实现。

```
// C++ program to find memory conflicts among threads
#include<bits/stdc++.h>
using namespace std;

/* Structure for details of thread */
struct Thread
{
    int id, memblck, time;
    char access;
};

/* Compare function needed for sorting threads
   We first sort threads on the basis of memory block,
   If they are same, then we sort on the basis of time */
bool compare(const Thread& x, const Thread& y)
{
    if (x.memblck == y.memblck)
        return x.time < y.time;
    else return x.memblck < y.memblck;
}

// Function to print all conflicts among threads
void printConflicts(Thread arr[], int n)
{
    /* Sort the threads first by memblock, then by
       time */
    sort(arr, arr+n, compare);

    /*start from second thread till last thread*/
    for (int i = 1; i < n; i++)
    {
        /* As threads are sorted, We check further
           for conflict possibility only if there
           memblock is same*/
        if(arr[i].memblck == arr[i-1].memblck)
        {

            /* As threads with same block are sorted in increasing order
               of access time. So we check possibility conflict from last
               thread to all previous threads which access the same block
               of memory such that the current thread access under the
               arr[i-1].time + 5.. and if any of them does read operation
               than conflict occurs. at any point memblock becomes different
               or current thread moves out of vulnerable time of latest
               previous processed thread, the loop breaks.
            */
            if (arr[i].time <= arr[i-1].time+5)
            {
                int j = i-1; /* start with previous thread */

                // Find all previous conflicting threads
                while (arr[i].memblck == arr[j].memblck &&
                        arr[i].time <= arr[j].time+5 &&
                        j >= 0)
                {
                    if (arr[i].access == 'W' || arr[j].access == 'W')
                    {
                        cout << "threads " << arr[j].id << " and "
                             << arr[i].id << " conflict.\n";
                    }
                    j--;
                }
            }
        }
    }

    cout << "All other operations are same\n";
}

// Driver program to test above function
int main()
{
    Thread arr[] = { {1, 512, 1, 'R'}, {2, 432, 2, 'W'},
                     {3, 512, 3, 'R'}, {4, 932, 4, 'R'},
                     {5, 512, 5, 'W'}, {6, 932, 6, 'R'},
                     {7, 835, 7, 'R'}, {8, 432, 8, 'R'}
                   };

    int n = sizeof(arr)/sizeof(arr[0]);
    printConflicts(arr, n);
    return 0;
}
```

输出:

```
threads 3 and 5 conflict.
threads 1 and 5 conflict.
All other operations are same
```

时间复杂度:上面的解决方案使用排序对线程进行排序。排序可以在 O(nLogn)时间内完成。然后打印所有冲突。打印所有冲突需要 O(n + m)个时间，其中 m 是冲突数。所以整体时间复杂度为 O(nLogn + m)。

本文由[高拉夫·阿赫瓦尔](https://www.facebook.com/COOL.DUDE.BORN.NUD3)供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
# 在有限时间内调度优先任务，最大限度减少损失

> 原文:[https://www . geesforgeks . org/scheduling-priority-tasks-limited-time-minimum-loss/](https://www.geeksforgeeks.org/scheduling-priority-tasks-limited-time-minimizing-loss/)

给定 n 个具有到达时间、优先级和所需时间单位数的任务。我们需要在单个资源上安排这些任务。目标是安排任务，以便获得最大优先级任务。目标是最小化由于时间有限而未计划的任务的优先级和剩余时间的乘积之和。这个标准仅仅意味着调度应该导致最小可能的损失。

示例:

```
Input : Total time = 3
        Task1: arrival = 1, units = 2, priority = 300
        Task2: arrival = 2, units = 2, priority = 100
Output : 100
Explanation : Two tasks are given and time to finish 
them is 3 units. First task arrives at time 1 and it
needs 2 units. Since no other task is running at that
time, we take it. 1 unit of task 1 is over. Now task 2 
arrives. The priority of task 1 is more than task 2 
(300 > 100) thus 1 more unit  of task 1 is employed. 
Now 1 unit of time is left and we have 2 units of task
2 to be done. So simply 1 unit of task 2 is done and 
the answer is ( units of task 2 left X priority of 
task 2 ) = 1 X 100 = 100

Input : Total Time = 3
        Task1: arrival = 1, units = 1, priority = 100
        Task2: arrival = 2, units = 2, priority = 300
Output : 0

```

我们使用优先级队列，一次安排一个任务单元。

1.  将总损失初始化为每个优先级和单位的总和。其思想是将结果初始化为最大值，然后逐个减去计划任务的优先级。
2.  根据到达时间对所有任务进行排序。
3.  从 1 到总时间的每个时间单位的过程。对于当前时间，选择可用的最高优先级任务。计划该任务的 1 个单元，并从总损失中减去其优先级。

下面是以上步骤的 C++实现。

```
// C++ code for task scheduling on basis
// of priority and arrival time
#include "bits/stdc++.h"
using namespace std;

// t is total time. n is number of tasks.
// arriv[] stores arrival times. units[]
// stores units of time required. prior[]
// stores priorities.
int minLoss(int n, int t, int arriv[],
            int units[],  int prior[])
{
    // Calculating maximum possible answer
    // that could be calculated. Later we
    // will subtract the tasks from it
    // accordingly.
    int ans = 0;
    for (int i = 0; i < n; i++)
        ans += prior[i] * units[i];

    // Pushing tasks in a vector so that they
    // could be sorted according with their
    // arrival time
    vector<pair<int, int> > v;
    for (int i = 0; i < n; i++)
        v.push_back({ arriv[i], i });

    // Sorting tasks in vector identified by
    // index and arrival time with respect
    // to their arrival time
    sort(v.begin(), v.end());

    // Priority queue to hold tasks to be
    // scheduled.
    priority_queue<pair<int, int> > pq;

    // Consider one unit of time at a time.
    int ptr = 0; // index in sorted vector
    for (int i = 1; i <= t; i++) {

        // Push all tasks that have arrived at
        // this time. Note that the tasks that
        // arrived earlier and could not be scheduled
        // are already in pq.
        while (ptr < n and v[ptr].x == i) {
            pq.push({ prior[v[ptr].y], units[v[ptr].y] });
            ptr++;
        }

        // Remove top priority task to be scheduled
        // at time i.
        if (!pq.empty()) {
            auto tmp = pq.top();
            pq.pop();

            // Removing 1 unit of task
            // from answer as we could
            // schedule it.
            ans -= tmp.x;
            tmp.y--;
            if (tmp.y)
                pq.push(tmp);
        }
    }

    return ans;
}

// driver code
int main()
{
    int n = 2, t = 3;
    int arriv[] = { 1, 2 };
    int units[] = { 2, 2 };
    int prior[] = { 100, 300 };

    printf("%d\n",  minLoss(n, t, arriv, units, prior));
    return 0;
}
```

输出:

```
100

```

本文由 **Parth Trehan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
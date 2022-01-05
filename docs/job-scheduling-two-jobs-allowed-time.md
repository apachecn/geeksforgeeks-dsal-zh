# 一次允许两个作业的作业调度

> 原文:[https://www . geesforgeks . org/job-scheduling-two-jobs-允许-time/](https://www.geeksforgeeks.org/job-scheduling-two-jobs-allowed-time/)

给我们 N 个工作，以及它们的开始和结束时间。在特定时刻，我们可以同时做两件事。如果一项工作在同一时刻结束，另一个节目开始，那么我们就做不到。我们需要检查是否有可能完成所有的工作。

**示例:**

```
Input :  Start and End times of Jobs
         1 2 
         2 3
         4 5 
Output : Yes
By the time third job starts, both jobs
are finished. So we can schedule third
job.

Input : Start and End times of Jobs
        1 5
        2 4
        2 6
        1 7
Output : No
All 4 jobs needs to be scheduled at time
3 which is not possible.

```

我们首先根据工作的开始时间对它们进行分类。然后我们同时开始两个作业，并检查第三个作业的开始时间是否大于前两个作业的和的结束时间。
以上思路的实现如下。

## C++

```
// CPP program to check if all jobs can be scheduled
// if two jobs are allowed at a time.
#include <bits/stdc++.h>
using namespace std;

bool checkJobs(int startin[], int endin[], int n)
{
    // making a pair of starting and ending time of job
    vector<pair<int, int> > a;
    for (int i = 0; i < n; i++)
        a.push_back(make_pair(startin[i], endin[i]));

    // sorting according to starting time of job
    sort(a.begin(), a.end());

    // starting first and second job simultaneously
    long long tv1 = a[0].second, tv2 = a[1].second;

    for (int i = 2; i < n; i++) {

        // Checking if starting time of next new job
        // is greater than ending time of currently
        // scheduled first job
        if (a[i].first >= tv1)
        {
            tv1 = tv2;
            tv2 = a[i].second;
        }

        // Checking if starting time of next new job
        // is greater than ending time of ocurrently
        // scheduled second job
        else if (a[i].first >= tv2)
            tv2 = a[i].second;

        else
            return false;
    }
    return true;
}

// Driver code
int main()
{
    int startin[] = { 1, 2, 4 }; // starting time of jobs
    int endin[] = { 2, 3, 5 }; // ending times of jobs
    int n = sizeof(startin) / sizeof(startin[0]);
    cout << checkJobs(startin, endin, n);
    return 0;
}
```
# O(n Log n)时间内的加权作业调度

> 原文:[https://www . geesforgeks . org/weighted-job-scheduling-log-n-time/](https://www.geeksforgeeks.org/weighted-job-scheduling-log-n-time/)

给定 N 个作业，每个作业由以下三个元素表示。

1.  开始时间
2.  结束时间
3.  相关利润或价值

找到工作的最大利润子集，使得子集中没有两个工作重叠。

示例:

```
Input: Number of Jobs n = 4
       Job Details {Start Time, Finish Time, Profit}
       Job 1:  {1, 2, 50} 
       Job 2:  {3, 5, 20}
       Job 3:  {6, 19, 100}
       Job 4:  {2, 100, 200}
Output: The maximum profit is 250.
We can get the maximum profit by scheduling jobs 1 and 4.
Note that there is longer schedules possible Jobs 1, 2 and 3 
but the profit with this schedule is 20+50+100 which is less than 250\.  
```

我们强烈建议参考以下文章作为先决条件。
[加权作业调度](https://www.geeksforgeeks.org/weighted-job-scheduling/)

上述问题可以用下面的递归解法解决。

```
1) First sort jobs according to finish time.
2) Now apply following recursive process. 
   // Here arr[] is array of n jobs
   findMaximumProfit(arr[], n)
   {
     a) if (n == 1) return arr[0];
     b) Return the maximum of following two profits.
         (i) Maximum profit by excluding current job, i.e., 
             findMaximumProfit(arr, n-1)
         (ii) Maximum profit by including the current job            
   }

How to find the profit including current job?
The idea is to find the latest job before the current job (in 
sorted array) that doesn't conflict with current job 'arr[n-1]'. 
Once we find such a job, we recur for all jobs till that job and
add profit of current job to result.
In the above example, "job 1" is the latest non-conflicting
for "job 4" and "job 2" is the latest non-conflicting for "job 3".
```

在[之前的文章](https://www.geeksforgeeks.org/weighted-job-scheduling/)中，我们已经讨论了基于递归和动态编程的方法。在上面的文章中讨论的实现使用线性搜索来查找先前的非冲突作业。在这篇文章中，讨论了基于二分搜索法的解决方案。基于二分搜索法的解的时间复杂度是 O(n ^ Log n)。

算法是:

1.  按非递减的完成时间对作业进行排序。
2.  对于从 1 到 n 的每个 I，根据作业的子序列[0]确定计划的最大值..我】。通过将作业[i]包含在计划中与作业[i]不包含在计划中进行比较，然后取最大值。

找到包含工作的利润。我们需要找到与工作不冲突的最新工作。这个想法是利用二分搜索法找到最新的不冲突的工作。

## C/C++

```
// C++ program for weighted job scheduling using Dynamic 
// Programming and Binary Search
#include <iostream>
#include <algorithm>
using namespace std;

// A job has start time, finish time and profit.
struct Job
{
    int start, finish, profit;
};

// A utility function that is used for sorting events
// according to finish time
bool myfunction(Job s1, Job s2)
{
    return (s1.finish < s2.finish);
}

// A Binary Search based function to find the latest job
// (before current job) that doesn't conflict with current
// job.  "index" is index of the current job.  This function
// returns -1 if all jobs before index conflict with it.
// The array jobs[] is sorted in increasing order of finish
// time.
int binarySearch(Job jobs[], int index)
{
    // Initialize 'lo' and 'hi' for Binary Search
    int lo = 0, hi = index - 1;

    // Perform binary Search iteratively
    while (lo <= hi)
    {
        int mid = (lo + hi) / 2;
        if (jobs[mid].finish <= jobs[index].start)
        {
            if (jobs[mid + 1].finish <= jobs[index].start)
                lo = mid + 1;
            else
                return mid;
        }
        else
            hi = mid - 1;
    }

    return -1;
}

// The main function that returns the maximum possible
// profit from given array of jobs
int findMaxProfit(Job arr[], int n)
{
    // Sort jobs according to finish time
    sort(arr, arr+n, myfunction);

    // Create an array to store solutions of subproblems.  table[i]
    // stores the profit for jobs till arr[i] (including arr[i])
    int *table = new int[n];
    table[0] = arr[0].profit;

    // Fill entries in table[] using recursive property
    for (int i=1; i<n; i++)
    {
        // Find profit including the current job
        int inclProf = arr[i].profit;
        int l = binarySearch(arr, i);
        if (l != -1)
            inclProf += table[l];

        // Store maximum of including and excluding
        table[i] = max(inclProf, table[i-1]);
    }

    // Store result and free dynamic memory allocated for table[]
    int result = table[n-1];
    delete[] table;

    return result;
}

// Driver program
int main()
{
    Job arr[] = {{3, 10, 20}, {1, 2, 50}, {6, 19, 100}, {2, 100, 200}};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Optimal profit is " << findMaxProfit(arr, n);
    return 0;
}
```

## 计算机编程语言

```
# Python program for weighted job scheduling using Dynamic 
# Programming and Binary Search

# Class to represent a job
class Job:
    def __init__(self, start, finish, profit):
        self.start  = start
        self.finish = finish
        self.profit  = profit

# A Binary Search based function to find the latest job
# (before current job) that doesn't conflict with current
# job.  "index" is index of the current job.  This function
# returns -1 if all jobs before index conflict with it.
# The array jobs[] is sorted in increasing order of finish
# time.
def binarySearch(job, start_index):

    # Initialize 'lo' and 'hi' for Binary Search
    lo = 0
    hi = start_index - 1

    # Perform binary Search iteratively
    while lo <= hi:
        mid = (lo + hi) // 2
        if job[mid].finish <= job[start_index].start:
            if job[mid + 1].finish <= job[start_index].start:
                lo = mid + 1
            else:
                return mid
        else:
            hi = mid - 1
    return -1

# The main function that returns the maximum possible
# profit from given array of jobs
def schedule(job):

    # Sort jobs according to finish time
    job = sorted(job, key = lambda j: j.finish)

    # Create an array to store solutions of subproblems.  table[i]
    # stores the profit for jobs till arr[i] (including arr[i])
    n = len(job) 
    table = [0 for _ in range(n)]

    table[0] = job[0].profit;

    # Fill entries in table[] using recursive property
    for i in range(1, n):

        # Find profit including the current job
        inclProf = job[i].profit
        l = binarySearch(job, i)
        if (l != -1):
            inclProf += table[l];

        # Store maximum of including and excluding
        table[i] = max(inclProf, table[i - 1])

    return table[n-1]

# Driver code to test above function
job = [Job(1, 2, 50), Job(3, 5, 20), 
      Job(6, 19, 100), Job(2, 100, 200)]
print("Optimal profit is"),
print schedule(job)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Weighted Job Scheduling in O(nLogn)
// time
import java.util.Arrays;
import java.util.Comparator;

// Class to represent a job
class Job
{
    int start, finish, profit;

    // Constructor
    Job(int start, int finish, int profit)
    {
        this.start = start;
        this.finish = finish;
        this.profit = profit;
    }
}

// Used to sort job according to finish times
class JobComparator implements Comparator<Job>
{
    public int compare(Job a, Job b)
    {
        return a.finish < b.finish ? -1 : a.finish == b.finish ? 0 : 1;
    }
}

public class WeightedIntervalScheduling
{
    /* A Binary Search based function to find the latest job
      (before current job) that doesn't conflict with current
      job.  "index" is index of the current job.  This function
      returns -1 if all jobs before index conflict with it.
      The array jobs[] is sorted in increasing order of finish
      time. */
    static public int binarySearch(Job jobs[], int index)
    {
        // Initialize 'lo' and 'hi' for Binary Search
        int lo = 0, hi = index - 1;

        // Perform binary Search iteratively
        while (lo <= hi)
        {
            int mid = (lo + hi) / 2;
            if (jobs[mid].finish <= jobs[index].start)
            {
                if (jobs[mid + 1].finish <= jobs[index].start)
                    lo = mid + 1;
                else
                    return mid;
            }
            else
                hi = mid - 1;
        }

        return -1;
    }

    // The main function that returns the maximum possible
    // profit from given array of jobs
    static public int schedule(Job jobs[])
    {
        // Sort jobs according to finish time
        Arrays.sort(jobs, new JobComparator());

        // Create an array to store solutions of subproblems.
        // table[i] stores the profit for jobs till jobs[i]
        // (including jobs[i])
        int n = jobs.length;
        int table[] = new int[n];
        table[0] = jobs[0].profit;

        // Fill entries in M[] using recursive property
        for (int i=1; i<n; i++)
        {
            // Find profit including the current job
            int inclProf = jobs[i].profit;
            int l = binarySearch(jobs, i);
            if (l != -1)
                inclProf += table[l];

            // Store maximum of including and excluding
            table[i] = Math.max(inclProf, table[i-1]);
        }

        return table[n-1];
    }

    // Driver method to test above
    public static void main(String[] args)
    {
        Job jobs[] = {new Job(1, 2, 50), new Job(3, 5, 20),
                      new Job(6, 19, 100), new Job(2, 100, 200)};

        System.out.println("Optimal profit is " + schedule(jobs));
    }
}
```

Output:

```
Optimal profit is 250
```

本文由**丹尼尔·雷**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论
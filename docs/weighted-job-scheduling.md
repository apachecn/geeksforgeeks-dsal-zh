# 加权作业调度

> 原文:[https://www.geeksforgeeks.org/weighted-job-scheduling/](https://www.geeksforgeeks.org/weighted-job-scheduling/)

给定 N 个作业，每个作业由以下三个元素表示。

1.  开始时间
2.  结束时间
3.  关联利润或价值(> = 0)

找到工作的最大利润子集，使得子集中没有两个工作重叠。

**示例:**

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
but the profit with this schedule is 20+50+100 which is less than 250.
```

这个问题的一个简单版本在这里讨论，每个工作都有相同的利润或价值。活动选择的[贪婪策略](https://www.geeksforgeeks.org/greedy-algorithms-set-1-activity-selection-problem/)在这里不起作用，因为工作越多，利润或价值就越小。

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

下面是上述朴素递归方法的实现。

## C++

```
// C++ program for weighted job scheduling using Naive Recursive Method
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
bool jobComparator(Job s1, Job s2)
{
    return (s1.finish < s2.finish);
}

// Find the latest job (in sorted array) that doesn't
// conflict with the job[i]. If there is no compatible job,
// then it returns -1.
int latestNonConflict(Job arr[], int i)
{
    for (int j=i-1; j>=0; j--)
    {
        if (arr[j].finish <= arr[i-1].start)
            return j;
    }
    return -1;
}

// A recursive function that returns the maximum possible
// profit from given array of jobs.  The array of jobs must
// be sorted according to finish time.
int findMaxProfitRec(Job arr[], int n)
{
    // Base case
    if (n == 1) return arr[n-1].profit;

    // Find profit when current job is included
    int inclProf = arr[n-1].profit;
    int i = latestNonConflict(arr, n);
    if (i != -1)
      inclProf += findMaxProfitRec(arr, i+1);

    // Find profit when current job is excluded
    int exclProf = findMaxProfitRec(arr, n-1);

    return max(inclProf,  exclProf);
}

// The main function that returns the maximum possible
// profit from given array of jobs
int findMaxProfit(Job arr[], int n)
{
    // Sort jobs according to finish time
    sort(arr, arr+n, jobComparator);

    return findMaxProfitRec(arr, n);
}

// Driver program
int main()
{
    Job arr[] = {{3, 10, 20}, {1, 2, 50}, {6, 19, 100}, {2, 100, 200}};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "The optimal profit is " << findMaxProfit(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program for weighted job scheduling using Naive Recursive Method
import java.util.*;
class GFG
{

// A job has start time, finish time and profit.
static class Job
{
    int start, finish, profit;
    Job(int start, int finish, int profit)
     {
        this.start = start;
        this.finish = finish;
        this.profit = profit;
     }
}

// Find the latest job (in sorted array) that doesn't
// conflict with the job[i]. If there is no compatible job,
// then it returns -1.
static int latestNonConflict(Job arr[], int i)
{
    for (int j = i - 1; j >= 0; j--)
    {
        if (arr[j].finish <= arr[i - 1].start)
            return j;
    }
    return -1;
}

// A recursive function that returns the maximum possible
// profit from given array of jobs. The array of jobs must
// be sorted according to finish time.
static int findMaxProfitRec(Job arr[], int n)
{
    // Base case
    if (n == 1) return arr[n-1].profit;

    // Find profit when current job is included
    int inclProf = arr[n-1].profit;
    int i = latestNonConflict(arr, n);
    if (i != -1)
    inclProf += findMaxProfitRec(arr, i+1);

    // Find profit when current job is excluded
    int exclProf = findMaxProfitRec(arr, n-1);

    return Math.max(inclProf, exclProf);
}

// The main function that returns the maximum possible
// profit from given array of jobs
static int findMaxProfit(Job arr[], int n)
{
    // Sort jobs according to finish time
    Arrays.sort(arr,new Comparator<Job>(){
       public int compare(Job j1,Job j2)
        {
           return j1.finish-j2.finish;
        }
       });

    return findMaxProfitRec(arr, n);
}

// Driver program
public static void main(String args[])
{
   int m = 4;
   Job arr[] = new Job[m];
    arr[0] = new Job(3, 10, 20);
    arr[1] = new Job(1, 2, 50);
    arr[2] = new Job(6, 19, 100);
    arr[3] = new Job(2, 100, 200);
    int n =arr.length;
    System.out.println("The optimal profit is " + findMaxProfit(arr, n));
}
}

// This code is contributed by Debojyoti Mandal
```

## 蟒蛇 3

```
# Python3 program for weighted job scheduling using
# Naive Recursive Method

# Importing the following module to sort array
# based on our custom comparison function
from functools import cmp_to_key

# A job has start time, finish time and profit
class Job:

    def __init__(self, start, finish, profit):

        self.start = start
        self.finish = finish
        self.profit = profit

# A utility function that is used for
# sorting events according to finish time
def jobComparator(s1, s2):

    return s1.finish < s2.finish

# Find the latest job (in sorted array) that
# doesn't conflict with the job[i]. If there
# is no compatible job, then it returns -1
def latestNonConflict(arr, i):

    for j in range(i - 1, -1, -1):
        if arr[j].finish <= arr[i - 1].start:
            return j

    return -1

# A recursive function that returns the
# maximum possible profit from given
# array of jobs. The array of jobs must
# be sorted according to finish time
def findMaxProfitRec(arr, n):

    # Base case
    if n == 1:
        return arr[n - 1].profit

    # Find profit when current job is included
    inclProf = arr[n - 1].profit
    i = latestNonConflict(arr, n)

    if i != -1:
        inclProf += findMaxProfitRec(arr, i + 1)

    # Find profit when current job is excluded
    exclProf = findMaxProfitRec(arr, n - 1)
    return max(inclProf, exclProf)

# The main function that returns the maximum
# possible profit from given array of jobs
def findMaxProfit(arr, n):

    # Sort jobs according to finish time
    arr = sorted(arr, key = cmp_to_key(jobComparator))
    return findMaxProfitRec(arr, n)

# Driver code
values = [ (3, 10, 20), (1, 2, 50),
           (6, 19, 100), (2, 100, 200) ]
arr = []
for i in values:
    arr.append(Job(i[0], i[1], i[2]))

n = len(arr)

print("The optimal profit is", findMaxProfit(arr, n))

# This code is code contributed by Kevin Joshi
```

**输出:**

```
The optimal profit is 250
```

上述解决方案可能包含许多重叠的子问题。例如，如果 lastinocrinction()总是返回上一个作业，那么 findmaxFurnrec(arr，n-1)将被调用两次，时间复杂度变为 O(n*2 <sup>n</sup> )。作为另一个例子，当 lastNonConflicting()返回到前一个作业之前时，有两个递归调用，用于 n-2 和 n-1。在这个例子中，递归变得和斐波那契数一样。

所以这个问题既有动态规划的性质，[最优子结构](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/)又有[重叠子问题](https://www.geeksforgeeks.org/dynamic-programming-set-1/)。
像其他动态规划问题一样，我们可以通过制作一个存储子问题解的表来解决这个问题。

下面是基于动态编程的实现。

## C++

```
// C++ program for weighted job scheduling using Dynamic Programming.
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
bool jobComparator(Job s1, Job s2)
{
    return (s1.finish < s2.finish);
}

// Find the latest job (in sorted array) that doesn't
// conflict with the job[i]
int latestNonConflict(Job arr[], int i)
{
    for (int j=i-1; j>=0; j--)
    {
        if (arr[j].finish <= arr[i].start)
            return j;
    }
    return -1;
}

// The main function that returns the maximum possible
// profit from given array of jobs
int findMaxProfit(Job arr[], int n)
{
    // Sort jobs according to finish time
    sort(arr, arr+n, jobComparator);

    // Create an array to store solutions of subproblems.  table[i]
    // stores the profit for jobs till arr[i] (including arr[i])
    int *table = new int[n];
    table[0] = arr[0].profit;

    // Fill entries in M[] using recursive property
    for (int i=1; i<n; i++)
    {
        // Find profit including the current job
        int inclProf = arr[i].profit;
        int l = latestNonConflict(arr, i);
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
    cout << "The optimal profit is " << findMaxProfit(arr, n);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for weighted job scheduling
# using Dynamic Programming

# Importing the following module to sort array
# based on our custom comparison function
from functools import cmp_to_key

# A job has start time, finish time and profit
class Job:

    def __init__(self, start, finish, profit):

        self.start = start
        self.finish = finish
        self.profit = profit

# A utility function that is used for sorting
# events according to finish time
def jobComparator(s1, s2):

    return s1.finish < s2.finish

# Find the latest job (in sorted array) that
# doesn't conflict with the job[i]. If there
# is no compatible job, then it returns -1
def latestNonConflict(arr, i):

    for j in range(i - 1, -1, -1):
        if arr[j].finish <= arr[i - 1].start:
            return j

    return -1

# The main function that returns the maximum possible
# profit from given array of jobs
def findMaxProfit(arr, n):

    # Sort jobs according to finish time
    arr = sorted(arr, key = cmp_to_key(jobComparator))

    # Create an array to store solutions of subproblems.
    # table[i] stores the profit for jobs till arr[i]
    # (including arr[i])
    table = [None] * n
    table[0] = arr[0].profit

    # Fill entries in M[] using recursive property
    for i in range(1, n):

        # Find profit including the current job
        inclProf = arr[i].profit
        l = latestNonConflict(arr, i)

        if l != -1:
            inclProf += table[l]

        # Store maximum of including and excluding
        table[i] = max(inclProf, table[i - 1])

    # Store result and free dynamic memory
    # allocated for table[]
    result = table[n - 1]

    return result

# Driver code
values = [ (3, 10, 20), (1, 2, 50),
           (6, 19, 100), (2, 100, 200) ]
arr = []
for i in values:
    arr.append(Job(i[0], i[1], i[2]))

n = len(arr)

print("The optimal profit is", findMaxProfit(arr, n))

# This code is contributed by Kevin Joshi
```

**输出:**

```
The optimal profit is 250
```

上述动态规划解的时间复杂度为 O(n <sup>2</sup> )。请注意，上面的解决方案可以使用 latestNonConflict()中的二分搜索法来优化为 O(nLogn)，而不是线性搜索。感谢加维特提出这个优化。详情请参考下面的帖子。

[O(n Log n)时间内的加权作业调度](https://www.geeksforgeeks.org/weighted-job-scheduling-log-n-time/)

**参考文献:**
[http://courses . cs . Washington . edu/courses/CSE 521/13wi/slides/06dp-sched . pdf](http://courses.cs.washington.edu/courses/cse521/13wi/slides/06dp-sched.pdf)

本文由 Shivam 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息
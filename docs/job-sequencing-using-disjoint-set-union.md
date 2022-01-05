# 作业排序问题|集合 2(使用不相交集合)

> 原文:[https://www . geeksforgeeks . org/job-sequenting-use-disjoint-set-union/](https://www.geeksforgeeks.org/job-sequencing-using-disjoint-set-union/)

给定一组 n 个作业，其中每个作业的截止日期 di >=1，利润 pi>=0。一次只能安排一个作业。每项工作需要 1 个单位的时间来完成。只有工作在最后期限前完成，我们才能获得利润。任务是找到利润最大化的工作子集。

**示例:**

```
Input: Four Jobs with following deadlines and profits
JobID Deadline Profit
   a      4      20
   b      1      10
   c      1      40
   d      1      30
Output: Following is maximum profit sequence of jobs:
       c, a

Input: Five Jobs with following deadlines and profits
JobID Deadline Profit
   a     2       100
   b     1       19
   c     2       27
   d     1       25
   e     3       15
Output: Following is maximum profit sequence of jobs:
       c, a, e
```

时间复杂度 O(n <sup>2</sup> )的贪婪解已经在[这里](https://www.geeksforgeeks.org/job-sequencing-problem-set-1-greedy-algorithm/)讨论过了。下面是简单的贪婪算法。

1.  按利润递减顺序排列所有工作。
2.  将结果序列初始化为排序作业中的第一个作业。
3.  对剩余的 n-1 个作业执行以下操作
    *   如果当前作业可以符合当前结果序列而不会错过截止日期，请将当前作业添加到结果中。否则忽略当前工作。

贪婪解决方案中代价高昂的操作是为作业分配一个空闲插槽。我们遍历一个作业的每个时隙，并分配最大可能的时隙( <deadline which="" was="" available.="">**)最大时隙是什么意思？**
假设作业 J1 的截止时间 t = 5。我们为这项工作分配了最大的空闲时间，并且少于最后期限，即 4-5 个小时。现在，另一个截止日期为 5 的作业 J2 进入，因此分配的时间段将是 3-4，因为 4-5 已经分配给作业 J1。
**为什么要给工作分配最大的时间段(空闲)？**
现在我们分配最大可能的时隙，因为如果我们分配一个比可用时隙更短的时隙，可能会有一些其他的工作错过它的最后期限。</deadline>

**示例:**
J1，截止日期 d1 = 5，利润 40
J2，截止日期 d2 = 1，利润 20
假设对于任务 J1，我们分配的时间段为 0-1。现在无法执行作业 J2，因为我们将在该时间段执行作业 J1。
**使用不相交集进行作业排序**
所有时隙最初都是单独的集。我们首先找到所有工作的最大截止日期。让最大截止时间为 m。我们创建 m+1 个单独的集合。如果一个作业被分配了一个 t 的时隙，其中 t > = 0，那么该作业被安排在[t-1，t]期间。所以一个值为 X 的集合代表时隙[X-1，X]。
我们需要记录给定的有截止日期的工作可以分配的最大可用时间。为此，我们使用不相交集合数据结构的父数组。树根总是最新的可用插槽。如果对于截止日期 d，没有可用的槽，那么根将是 0。下面是详细的步骤。
**初始化不相交集:**创建初始不相交集。

```
// m is maximum deadline of a job
parent = new int[m + 1];

// Every node is a parent of itself
for (int i = 0; i ≤ m; i++)
    parent[i] = i;
```

**查找:**查找最新的可用时隙。

```
// Returns the maximum available time slot
find(s)
{
    // Base case
    if (s == parent[s])
       return s;

    // Recursive call with path compression
    return parent[s] = find(parent[s]);
} 
```

**联合:**

```
 Merges two sets.  
// Makes u as parent of v.
union(u, v)
{
   // update the greatest available
   // free slot to u
   parent[v] = u;
} 
```

【find 怎么会返回最新的可用时隙？
最初所有的时隙都是单独的时隙。所以返回的时隙总是最大的。当我们给一项工作分配一个时间槽“t”时，我们把“t”和“t-1”结合起来，使“t-1”成为“t”的父项。为此，我们称之为联合(t-1，t)。这意味着对时隙 t 的所有未来查询现在将返回对由 t-1 表示的集合可用的最新时隙。

**实现:**
以下是上述算法的实现。

## C++

```
// C++ Program to find the maximum profit job sequence
// from a given array of jobs with deadlines and profits
#include<bits/stdc++.h>
using namespace std;

// A structure to represent various attributes of a Job
struct Job
{
    // Each job has id, deadline and profit
    char id;
    int deadLine, profit;
};

// A Simple Disjoint Set Data Structure
struct DisjointSet
{
    int *parent;

    // Constructor
    DisjointSet(int n)
    {
        parent = new int[n+1];

        // Every node is a parent of itself
        for (int i = 0; i <= n; i++)
            parent[i] = i;
    }

    // Path Compression
    int find(int s)
    {
        /* Make the parent of the nodes in the path
           from u--> parent[u] point to parent[u] */
        if (s == parent[s])
            return s;
        return parent[s] = find(parent[s]);
    }

    // Makes u as parent of v.
    void merge(int u, int v)
    {
        //update the greatest available
        //free slot to u
        parent[v] = u;
    }
};

// Used to sort in descending order on the basis
// of profit for each job
bool cmp(Job a, Job b)
{
    return (a.profit > b.profit);
}

// Functions returns the maximum deadline from the set
// of jobs
int findMaxDeadline(struct Job arr[], int n)
{
    int ans = INT_MIN;
    for (int i = 0; i < n; i++)
        ans = max(ans, arr[i].deadLine);
    return ans;
}

int printJobScheduling(Job arr[], int n)
{
    // Sort Jobs in descending order on the basis
    // of their profit
    sort(arr, arr + n, cmp);

    // Find the maximum deadline among all jobs and
    // create a disjoint set data structure with
    // maxDeadline disjoint sets initially.
    int maxDeadline = findMaxDeadline(arr, n);
    DisjointSet ds(maxDeadline);

    // Traverse through all the jobs
    for (int i = 0; i < n; i++)
    {
        // Find the maximum available free slot for
        // this job (corresponding to its deadline)
        int availableSlot = ds.find(arr[i].deadLine);

        // If maximum available free slot is greater
        // than 0, then free slot available
        if (availableSlot > 0)
        {
            // This slot is taken by this job 'i'
            // so we need to update the greatest
            // free slot. Note that, in merge, we
            // make first parameter as parent of
            // second parameter. So future queries
            // for availableSlot will return maximum
            // available slot in set of
            // "availableSlot - 1"
            ds.merge(ds.find(availableSlot - 1),
                             availableSlot);

            cout << arr[i].id << " ";
        }
    }
}

// Driver code
int main()
{
    Job arr[] =  { { 'a', 2, 100 }, { 'b', 1, 19 },
                   { 'c', 2, 27 },  { 'd', 1, 25 },
                   { 'e', 3, 15 } };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Following jobs need to be "
         << "executed for maximum profit\n";
    printJobScheduling(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum profit job sequence
// from a given array of jobs with deadlines and profits
import java.util.*;

// A Simple Disjoint Set Data Structure
class DisjointSet
{
    int parent[];

    // Constructor
    DisjointSet(int n)
    {
        parent = new int[n + 1];

        // Every node is a parent of itself
        for (int i = 0; i <= n; i++)
            parent[i] = i;
    }

    // Path Compression
    int find(int s)
    {
        /* Make the parent of the nodes in the path
           from u--> parent[u] point to parent[u] */
        if (s == parent[s])
            return s;
        return parent[s] = find(parent[s]);
    }

    // Makes u as parent of v.
    void merge(int u, int v)
    {
        //update the greatest available
        //free slot to u
        parent[v] = u;
    }
}

class Job implements Comparator<Job>
{
    // Each job has a unique-id, profit and deadline
    char id;
    int deadline, profit;

    // Constructors
    public Job() { }
    public Job(char id,int deadline,int profit)
    {
        this.id = id;
        this.deadline = deadline;
        this.profit = profit;
    }

    // Returns the maximum deadline from the set of jobs
    public static int findMaxDeadline(ArrayList<Job> arr)
    {
        int ans = Integer.MIN_VALUE;
        for (Job temp : arr)
            ans = Math.max(temp.deadline, ans);
        return ans;
    }

    // Prints optimal job sequence
    public static void printJobScheduling(ArrayList<Job> arr)
    {
        // Sort Jobs in descending order on the basis
        // of their profit
        Collections.sort(arr, new Job());

        // Find the maximum deadline among all jobs and
        // create a disjoint set data structure with
        // maxDeadline disjoint sets initially.
        int maxDeadline = findMaxDeadline(arr);
        DisjointSet dsu = new DisjointSet(maxDeadline);

        // Traverse through all the jobs
        for (Job temp : arr)
        {
            // Find the maximum available free slot for
            // this job (corresponding to its deadline)
            int availableSlot = dsu.find(temp.deadline);

            // If maximum available free slot is greater
            // than 0, then free slot available
            if (availableSlot > 0)
            {
                // This slot is taken by this job 'i'
                // so we need to update the greatest free
                // slot. Note that, in merge, we make
                // first parameter as parent of second
                // parameter.  So future queries for
                // availableSlot will return maximum slot
                // from set of "availableSlot - 1"
                dsu.merge(dsu.find(availableSlot - 1),
                                   availableSlot);
                System.out.print(temp.id + " ");
            }
        }
        System.out.println();
    }

    // Used to sort in descending order on the basis
    // of profit for each job
    public int compare(Job j1, Job j2)
    {
        return j1.profit > j2.profit? -1: 1;
    }
}

// Driver code
class Main
{
    public static void main(String args[])
    {
        ArrayList<Job> arr=new ArrayList<Job>();
        arr.add(new Job('a',2,100));
        arr.add(new Job('b',1,19));
        arr.add(new Job('c',2,27));
        arr.add(new Job('d',1,25));
        arr.add(new Job('e',3,15));
        System.out.println("Following jobs need to be "+
                           "executed for maximum profit");
        Job.printJobScheduling(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the maximum profit
# job sequence from a given array of jobs
# with deadlines and profits
import sys

class DisjointSet:
    def __init__(self, n):
        self.parent = [i for i in range(n + 1)]

    def find(self, s):

        # Make the parent of nodes in the path from
        # u --> parent[u] point to parent[u]
        if s == self.parent[s]:
            return s
        self.parent[s] = self.find(self.parent[s])
        return self.parent[s]

    # Make us as parent of v
    def merge(self, u, v):

        # Update the greatest available
        # free slot to u
        self.parent[v] = u

def cmp(a):
    return a['profit']

def findmaxdeadline(arr, n):
    """
    :param arr: Job array
    :param n: length of array
    :return: maximum deadline from the set of jobs
    """
    ans = - sys.maxsize - 1
    for i in range(n):
        ans = max(ans, arr[i]['deadline'])
    return ans

def printjobscheduling(arr, n):

    # Sort jobs in descending order on
    # basis of their profit
    arr = sorted(arr, key = cmp, reverse = True)

    """
    Find the maximum deadline among all jobs and
    create a disjoint set data structure with
    max_deadline disjoint sets initially
    """
    max_deadline = findmaxdeadline(arr, n)
    ds = DisjointSet(max_deadline)

    for i in range(n):

        # find maximum available free slot for
        # this job (corresponding to its deadline)
        available_slot = ds.find(arr[i]['deadline'])
        if available_slot > 0:

            # This slot is taken by this job 'i'
            # so we need to update the greatest free slot.
            # Note: In merge, we make first parameter
            # as parent of second parameter.
            # So future queries for available_slot will
            # return maximum available slot in set of
            # "available_slot - 1"
            ds.merge(ds.find(available_slot - 1),
                             available_slot)
            print(arr[i]['id'], end = " ")

# Driver Code
if __name__ == "__main__":
    arr = [{'id': 'a', 'deadline': 2, 'profit': 100},
           {'id': 'b', 'deadline': 1, 'profit': 19},
           {'id': 'c', 'deadline': 2, 'profit': 27},
           {'id': 'd', 'deadline': 1, 'profit': 25},
           {'id': 'e', 'deadline': 3, 'profit': 15}]
    n = len(arr)
    print("Following jobs need to be",
          "executed for maximum profit")
    printjobscheduling(arr, n)

# This code is contributed by Rajat Srivastava
```

**Output**

```
Following jobs need to be executed for maximum profit
a c e 
```

本文由 **Chirag Agarwal 供稿。**如果你喜欢 GeeksforGeeks 并想投稿，你也可以写一篇文章，把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息
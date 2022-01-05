# 找到在给定约束条件下完成所有工作的最短时间

> 原文:[https://www . geeksforgeeks . org/find-在给定约束条件下完成所有任务的最短时间/](https://www.geeksforgeeks.org/find-minimum-time-to-finish-all-jobs-with-given-constraints/)

给定一系列具有不同时间要求的工作。有 K 个相同的受托人可用，我们也被告知一个受托人做一个单位的工作需要多少时间。找出在下列限制下完成所有工作的最短时间。

*   只能向受理人分配连续的职务。例如，不能向受理人分配工作 1 和 3，但不能分配工作 2。
*   两个受让人不能共享(或共同分配)一项工作，即一项工作不能部分分配给一个受让人，部分分配给另一个受让人。

**输入:**

```
K:     Number of assignees available.
T:     Time taken by an assignee to finish one unit 
       of job
job[]: An array that represents time requirements of 
       different jobs.
```

**例:**

```
Input:  k = 2, T = 5, job[] = {4, 5, 10}
Output: 50
The minimum time required to finish all the jobs is 50.
There are 2 assignees available. We get this time by 
assigning {4, 5} to first assignee and {10} to second 
assignee.

Input:  k = 4, T = 5, job[] = {10, 7, 8, 12, 6, 8}
Output: 75
We get this time by assigning {10} {7, 8} {12} and {6, 8}
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
这个想法是利用二分搜索法。想一想，如果我们有一个函数(比如 isPossible())告诉我们是否有可能在给定的时间内完成所有工作，以及有多少个可用的受托人。我们可以通过做一个二分搜索法来解决这个问题。如果二分搜索法的中点不可能，那就在下半场找，否则就在上半场找。最小时间的二分搜索法下限可以设置为 0。上限可以通过将所有给定的作业时间相加得到。
现在如何实现 isPossible()？这个函数可以用贪婪方法实现。因为我们想知道是否有可能在给定时间内完成所有作业，所以我们遍历所有作业，并在给定时间限制内分配一个作业的同时，继续将作业逐个分配给当前受让人。当当前受理人花费的时间超过给定时间时，创建一个新的受理人，并开始为其分配作业。如果受托人的数量大于 k，则返回 false，否则返回 true。

## C++

```
// C++ program to find minimum time to finish all jobs with
// given number of assignees
#include<bits/stdc++.h>
using namespace std;

// Utility function to get maximum element in job[0..n-1]
int getMax(int arr[], int n)
{
   int result = arr[0];
   for (int i=1; i<n; i++)
      if (arr[i] > result)
         result = arr[i];
    return result;
}

// Returns true if it is possible to finish jobs[] within
// given time 'time'
bool isPossible(int time, int K, int job[], int n)
{
    // cnt is count of current assignees required for jobs
    int cnt = 1;

    int curr_time = 0; //  time assigned to current assignee

    for (int i = 0; i < n;)
    {
        // If time assigned to current assignee exceeds max,
        // increment count of assignees.
        if (curr_time + job[i] > time) {
            curr_time = 0;
            cnt++;
        }
        else { // Else add time of job to current time and move
               // to next job.
            curr_time += job[i];
            i++;
        }
    }

    // Returns true if count is smaller than k
    return (cnt <= K);
}

// Returns minimum time required to finish given array of jobs
// k --> number of assignees
// T --> Time required by every assignee to finish 1 unit
// m --> Number of jobs
int findMinTime(int K, int T, int job[], int n)
{
    // Set start and end for binary search
    // end provides an upper limit on time
    int end = 0, start = 0;
    for (int i = 0; i < n; ++i)
        end += job[i];

    int ans = end; // Initialize answer

    // Find the job that takes maximum time
    int job_max = getMax(job, n);

    // Do binary search for minimum feasible time
    while (start <= end)
    {
        int mid = (start + end) / 2;

        // If it is possible to finish jobs in mid time
        if (mid >= job_max && isPossible(mid, K, job, n))
        {
            ans = min(ans, mid);  // Update answer
            end = mid - 1;
        }
        else
            start = mid + 1;
    }

    return (ans * T);
}

// Driver program
int main()
{
    int job[] =  {10, 7, 8, 12, 6, 8};
    int n = sizeof(job)/sizeof(job[0]);
    int k = 4, T = 5;
    cout << findMinTime(k, T, job, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum time
// to finish all jobs with given
// number of assignees

class GFG
{
    // Utility function to get
    // maximum element in job[0..n-1]
    static int getMax(int arr[], int n)
    {
    int result = arr[0];
    for (int i=1; i<n; i++)
        if (arr[i] > result)
            result = arr[i];
        return result;
    }

    // Returns true if it is possible to finish jobs[]
    // within given time 'time'
    static boolean isPossible(int time, int K,
                                    int job[], int n)
    {
        // cnt is count of current
        // assignees required for jobs
        int cnt = 1;

        // time assigned to current assignee
        int curr_time = 0;

        for (int i = 0; i < n;)
        {
            // If time assigned to current assignee
            // exceeds max, increment count of assignees.
            if (curr_time + job[i] > time) {
                curr_time = 0;
                cnt++;
            }

            // Else add time of job to current
            // time and move to next job.
            else
            {
                curr_time += job[i];
                i++;
            }
        }

        // Returns true if count
        // is smaller than k
        return (cnt <= K);
    }

    // Returns minimum time required to
    // finish given array of jobs
    // k --> number of assignees
    // T --> Time required by every assignee to finish 1 unit
    // m --> Number of jobs
    static int findMinTime(int K, int T, int job[], int n)
    {
        // Set start and end for binary search
        // end provides an upper limit on time
        int end = 0, start = 0;
        for (int i = 0; i < n; ++i)
            end += job[i];

        // Initialize answer
        int ans = end;

        // Find the job that takes maximum time
        int job_max = getMax(job, n);

        // Do binary search for
        // minimum feasible time
        while (start <= end)
        {
            int mid = (start + end) / 2;

            // If it is possible to finish jobs in mid time
            if (mid >= job_max && isPossible(mid, K, job, n))
            {
                // Update answer
                ans = Math.min(ans, mid);

                end = mid - 1;
            }

            else
                start = mid + 1;
        }

        return (ans * T);
    }

    // Driver program
    public static void main(String arg[])
    {
        int job[] = {10, 7, 8, 12, 6, 8};
        int n = job.length;
        int k = 4, T = 5;
        System.out.println(findMinTime(k, T, job, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find minimum
# time to finish all jobs with
# given number of assignees

# Utility function to get maximum
# element in job[0..n-1]
def getMax(arr, n):
    result = arr[0]
    for i in range(1, n):
        if arr[i] > result:
            result = arr[i]
    return result

# Returns true if it is possible
# to finish jobs[] within given
# time 'time'
def isPossible(time, K, job, n):

    # cnt is count of current
    # assignees required for jobs
    cnt = 1

    # time assigned to current assignee
    curr_time = 0

    i = 0
    while i < n:

        # If time assigned to current
        # assignee exceeds max, increment
        # count of assignees.
        if curr_time + job[i] > time:
            curr_time = 0
            cnt += 1
        else:

            # Else add time of job to current
            # time and move to next job.
            curr_time += job[i]
            i += 1

    # Returns true if count is smaller than k
    return cnt <= K

# Returns minimum time required
# to finish given array of jobs
# k --> number of assignees
# T --> Time required by every assignee to finish 1 unit
# m --> Number of jobs
def findMinTime(K, T, job, n):

    # Set start and end for binary search
    # end provides an upper limit on time
    end = 0
    start = 0
    for i in range(n):
        end += job[i]

    ans = end # Initialize answer

    # Find the job that takes maximum time
    job_max = getMax(job, n)

    # Do binary search for minimum feasible time
    while start <= end:
        mid = int((start + end) / 2)

        # If it is possible to finish jobs in mid time
        if mid >= job_max and isPossible(mid, K, job, n):
            ans = min(ans, mid) # Update answer
            end = mid - 1
        else:
            start = mid + 1

    return ans * T

# Driver program
if __name__ == '__main__':
    job = [10, 7, 8, 12, 6, 8]
    n = len(job)
    k = 4
    T = 5
    print(findMinTime(k, T, job, n))

# this code is contributed by PranchalK
```

## C#

```
// C# program to find minimum time
// to finish all jobs with given
// number of assignees
using System;

class GFG
{
    // Utility function to get
    // maximum element in job[0..n-1]
    static int getMax(int []arr, int n)
    {
      int result = arr[0];
      for (int i=1; i<n; i++)
        if (arr[i] > result)
            result = arr[i];
        return result;
    }

    // Returns true if it is possible to
    // finish jobs[] within given time 'time'
    static bool isPossible(int time, int K,
                          int []job, int n)
    {
        // cnt is count of current
        // assignees required for jobs
        int cnt = 1;

        // time assigned to current assignee
        int curr_time = 0;

        for (int i = 0; i < n;)
        {
            // If time assigned to current assignee
            // exceeds max, increment count of assignees.
            if (curr_time + job[i] > time) {
                curr_time = 0;
                cnt++;
            }

            // Else add time of job to current
            // time and move to next job.
            else
            {
                curr_time += job[i];
                i++;
            }
        }

        // Returns true if count
        // is smaller than k
        return (cnt <= K);
    }

    // Returns minimum time required to
    // finish given array of jobs
    // k --> number of assignees
    // T --> Time required by every assignee to finish 1 unit
    // m --> Number of jobs
    static int findMinTime(int K, int T, int []job, int n)
    {
        // Set start and end for binary search
        // end provides an upper limit on time
        int end = 0, start = 0;
        for (int i = 0; i < n; ++i)
            end += job[i];

        // Initialize answer
        int ans = end;

        // Find the job that takes maximum time
        int job_max = getMax(job, n);

        // Do binary search for
        // minimum feasible time
        while (start <= end)
        {
            int mid = (start + end) / 2;

            // If it is possible to finish jobs in mid time
            if (mid >= job_max && isPossible(mid, K, job, n))
            {
                // Update answer
                ans = Math.Min(ans, mid);

                end = mid - 1;
            }

            else
                start = mid + 1;
        }

        return (ans * T);
    }

    // Driver program
    public static void Main()
    {
        int []job = {10, 7, 8, 12, 6, 8};
        int n = job.Length;
        int k = 4, T = 5;
        Console.WriteLine(findMinTime(k, T, job, n));
    }
}

// This code is contributed by Sam007.
```

## java 描述语言

```
<script>
    // Javascript program to find minimum time
    // to finish all jobs with given
    // number of assignees

    // Utility function to get
    // maximum element in job[0..n-1]
    function getMax(arr, n)
    {
      let result = arr[0];
      for (let i=1; i<n; i++)
        if (arr[i] > result)
            result = arr[i];
        return result;
    }

    // Returns true if it is possible to
    // finish jobs[] within given time 'time'
    function isPossible(time, K, job, n)
    {
        // cnt is count of current
        // assignees required for jobs
        let cnt = 1;

        // time assigned to current assignee
        let curr_time = 0;

        for (let i = 0; i < n;)
        {
            // If time assigned to current assignee
            // exceeds max, increment count of assignees.
            if (curr_time + job[i] > time) {
                curr_time = 0;
                cnt++;
            }

            // Else add time of job to current
            // time and move to next job.
            else
            {
                curr_time += job[i];
                i++;
            }
        }

        // Returns true if count
        // is smaller than k
        return (cnt <= K);
    }

    // Returns minimum time required to
    // finish given array of jobs
    // k --> number of assignees
    // T --> Time required by every assignee to finish 1 unit
    // m --> Number of jobs
    function findMinTime(K, T, job, n)
    {
        // Set start and end for binary search
        // end provides an upper limit on time
        let end = 0, start = 0;
        for (let i = 0; i < n; ++i)
            end += job[i];

        // Initialize answer
        let ans = end;

        // Find the job that takes maximum time
        let job_max = getMax(job, n);

        // Do binary search for
        // minimum feasible time
        while (start <= end)
        {
            let mid = parseInt((start + end) / 2, 10);

            // If it is possible to finish jobs in mid time
            if (mid >= job_max && isPossible(mid, K, job, n))
            {
                // Update answer
                ans = Math.min(ans, mid);

                end = mid - 1;
            }

            else
                start = mid + 1;
        }

        return (ans * T);
    }

    let job = [10, 7, 8, 12, 6, 8];
    let n = job.length;
    let k = 4, T = 5;
    document.write(findMinTime(k, T, job, n));

</script>
```

**输出:**

```
75
```

感谢 Gaurav Ahirwar 提出上述解决方案。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息
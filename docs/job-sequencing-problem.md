# 作业排序问题

> 原文:[https://www.geeksforgeeks.org/job-sequencing-problem/](https://www.geeksforgeeks.org/job-sequencing-problem/)

给定一系列工作，每个工作都有一个截止日期，如果工作在截止日期前完成，就会有相关的利润。还假设每项工作只需要一个时间单位，因此任何工作的最小可能截止时间是 1。如果一次只能安排一个工作，如何使总利润最大化？

**示例:**

```
Input: Four Jobs with following 
deadlines and profits
JobID  Deadline  Profit
  a      4        20   
  b      1        10
  c      1        40  
  d      1        30
Output: Following is maximum 
profit sequence of jobs
        c, a   

Input:  Five Jobs with following
deadlines and profits
JobID   Deadline  Profit
  a       2        100
  b       1        19
  c       2        27
  d       1        25
  e       3        15
Output: Following is maximum 
profit sequence of jobs
        c, a, e
```

一个**简单的解决方案**是生成一组给定作业的所有子集，并检查单个子集在该子集中作业的可行性。跟踪所有可行子集的最大利润。这个解的时间复杂度是指数级的。
这是标准的[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms-set-1-activity-selection-problem/)问题。

下面是算法。

> 1)按利润递减顺序对所有工作进行排序。
> 2)按照利润递减的顺序迭代工作。对于每项工作，做以下工作:
> a)找一个时间段 I，这样时间段是空的，我<的截止时间和我是最大的。将工作放入
> 这个位置，并标记该位置已满。
> b)如果没有这样的我，那就忽略这个工作。

以下是上述算法的实现。

## C++

```
// Program to find the maximum profit job sequence from a given array
// of jobs with deadlines and profits
#include<iostream>
#include<algorithm>
using namespace std;

// A structure to represent a job
struct Job
{
   char id;     // Job Id
   int dead;    // Deadline of job
   int profit;  // Profit if job is over before or on deadline
};

// This function is used for sorting all jobs according to profit
bool comparison(Job a, Job b)
{
     return (a.profit > b.profit);
}

// Returns minimum number of platforms required
void printJobScheduling(Job arr[], int n)
{
    // Sort all jobs according to decreasing order of profit
    sort(arr, arr+n, comparison);

    int result[n]; // To store result (Sequence of jobs)
    bool slot[n];  // To keep track of free time slots

    // Initialize all slots to be free
    for (int i=0; i<n; i++)
        slot[i] = false;

    // Iterate through all given jobs
    for (int i=0; i<n; i++)
    {
       // Find a free slot for this job (Note that we start
       // from the last possible slot)
       for (int j=min(n, arr[i].dead)-1; j>=0; j--)
       {
          // Free slot found
          if (slot[j]==false)
          {
             result[j] = i;  // Add this job to result
             slot[j] = true; // Make this slot occupied
             break;
          }
       }
    }

    // Print the result
    for (int i=0; i<n; i++)
       if (slot[i])
         cout << arr[result[i]].id << " ";
}

// Driver code
int main()
{
    Job arr[] = { {'a', 2, 100}, {'b', 1, 19}, {'c', 2, 27},
                   {'d', 1, 25}, {'e', 3, 15}};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Following is maximum profit sequence of jobs \n";

    // Function call
    printJobScheduling(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find the maximum profit
// job sequence from a given array
// of jobs with deadlines and profits
import java.util.*;

class Job 
{
    // Each job has a unique-id,
    // profit and deadline
    char id;
    int deadline, profit;

    // Constructors
    public Job() {}

    public Job(char id, int deadline, int profit)
    {
        this.id = id;
        this.deadline = deadline;
        this.profit = profit;
    }

    // Function to schedule the jobs take 2
    // arguments arraylist and no of jobs to schedule
    void printJobScheduling(ArrayList<Job> arr, int t)
    {
        // Length of array
        int n = arr.size();

        // Sort all jobs according to
        // decreasing order of profit
        Collections.sort(arr,
                         (a, b) -> b.profit - a.profit);

        // To keep track of free time slots
        boolean result[] = new boolean[t];

        // To store result (Sequence of jobs)
        char job[] = new char[t];

        // Iterate through all given jobs
        for (int i = 0; i < n; i++) 
        {
            // Find a free slot for this job
            // (Note that we start from the
            // last possible slot)
            for (int j
                 = Math.min(t - 1, arr.get(i).deadline - 1);
                 j >= 0; j--) {

                // Free slot found
                if (result[j] == false) 
                {
                    result[j] = true;
                    job[j] = arr.get(i).id;
                    break;
                }
            }
        }

        // Print the sequence
        for (char jb : job) 
        {
            System.out.print(jb + " ");
        }
        System.out.println();
    }

    // Driver code
    public static void main(String args[])
    {
        ArrayList<Job> arr = new ArrayList<Job>();

        arr.add(new Job('a', 2, 100));
        arr.add(new Job('b', 1, 19));
        arr.add(new Job('c', 2, 27));
        arr.add(new Job('d', 1, 25));
        arr.add(new Job('e', 3, 15));

        // Function call
        System.out.println("Following is maximum "
                           + "profit sequence of jobs");

        Job job = new Job();

        // Calling function
        job.printJobScheduling(arr, 3);
    }
}

// This code is contributed by Prateek Gupta
```

## 蟒蛇 3

```
# Program to find the maximum profit
# job sequence from a given array
# of jobs with deadlines and profits

# function to schedule the jobs take 2
# arguments array and no of jobs to schedule

def printJobScheduling(arr, t):

    # length of array
    n = len(arr)

    # Sort all jobs according to
    # decreasing order of profit
    for i in range(n):
        for j in range(n - 1 - i):
            if arr[j][2] < arr[j + 1][2]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

    # To keep track of free time slots
    result = [False] * t

    # To store result (Sequence of jobs)
    job = ['-1'] * t

    # Iterate through all given jobs
    for i in range(len(arr)):

        # Find a free slot for this job
        # (Note that we start from the
        # last possible slot)
        for j in range(min(t - 1, arr[i][1] - 1), -1, -1):

            # Free slot found
            if result[j] is False:
                result[j] = True
                job[j] = arr[i][0]
                break

    # print the sequence
    print(job)

# Driver COde
arr = [['a', 2, 100],  # Job Array
       ['b', 1, 19],
       ['c', 2, 27],
       ['d', 1, 25],
       ['e', 3, 15]]

print("Following is maximum profit sequence of jobs")

# Function Call
printJobScheduling(arr, 3) 

# This code is contributed
# by Anubhav Raj Singh
```

## C#

```
// C# Program to find the maximum profit
// job sequence from a given array
// of jobs with deadlines and profits

using System;
using System.Collections.Generic;

class GFG : IComparer<Job>
{
    public int Compare(Job x, Job y)
    {
        if (x.profit == 0 || y.profit== 0)
        {
            return 0;
        }

        // CompareTo() method
        return (y.profit).CompareTo(x.profit);

    }
}

public class Job{

    // Each job has a unique-id,
    // profit and deadline
    char id;
    public int deadline, profit;

    // Constructors
    public Job() {}

    public Job(char id, int deadline, int profit)
    {
        this.id = id;
        this.deadline = deadline;
        this.profit = profit;
    }

    // Function to schedule the jobs take 2
    // arguments arraylist and no of jobs to schedule
    void printJobScheduling(List<Job> arr, int t)
    {
        // Length of array
        int n = arr.Count;

        GFG gg = new GFG();
        // Sort all jobs according to
        // decreasing order of profit
        arr.Sort(gg);

        // To keep track of free time slots
        bool[] result = new bool[t];

        // To store result (Sequence of jobs)
        char[] job = new char[t];

        // Iterate through all given jobs
        for (int i = 0; i < n; i++)
        {
            // Find a free slot for this job
            // (Note that we start from the
            // last possible slot)
            for (int j
                 = Math.Min(t - 1, arr[i].deadline - 1);
                 j >= 0; j--) {

                // Free slot found
                if (result[j] == false)
                {
                    result[j] = true;
                    job[j] = arr[i].id;
                    break;
                }
            }
        }

        // Print the sequence
        foreach (char jb in job)
        {
            Console.Write(jb + " ");
        }
        Console.WriteLine();
    }

    // Driver code
    static public void Main ()
    {

        List<Job> arr = new List<Job>();

        arr.Add(new Job('a', 2, 100));
        arr.Add(new Job('b', 1, 19));
        arr.Add(new Job('c', 2, 27));
        arr.Add(new Job('d', 1, 25));
        arr.Add(new Job('e', 3, 15));

        // Function call
        Console.WriteLine("Following is maximum "
                           + "profit sequence of jobs");

        Job job = new Job();

        // Calling function
        job.printJobScheduling(arr, 3);

    }
}

// This code is contributed by avanitracchadiya2155.
```

## java 描述语言

```
<script>

// Program to find the maximum profit
// job sequence from a given array
// of jobs with deadlines and profits

// function to schedule the jobs take 2
// arguments array and no of jobs to schedule

function printJobScheduling(arr, t){
    // length of array
    let n = arr.length;

    // Sort all jobs according to
    // decreasing order of profit
    for(let i=0;i<n;i++){ 
        for(let j = 0;j<(n - 1 - i);j++){
            if(arr[j][2] < arr[j + 1][2]){
                let temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
         }
     }

    // To keep track of free time slots
    let result = [];

    // To store result (Sequence of jobs)
    let job = [];
    for(let i = 0;i<t;i++){
        job[i] = '-1';
        result[i] = false;
    }

    // Iterate through all given jobs
    for(let i= 0;i<arr.length;i++){
        // Find a free slot for this job
        // (Note that we start from the
        // last possible slot)
        for(let j = (t - 1, arr[i][1] - 1);j>=0;j--){
            // Free slot found
            if(result[j] == false){
                result[j] = true;
                job[j] = arr[i][0];
                break;
            }
        }
    }

    // print the sequence
    document.write(job);
}

// Driver COde
arr = [['a', 2, 100],  // Job Array
       ['b', 1, 19],
       ['c', 2, 27],
       ['d', 1, 25],
       ['e', 3, 15]];

document.write("Following is maximum profit sequence of jobs ");
document.write("<br>");

// Function Call
printJobScheduling(arr, 3) ;

</script>
```

**Output**

```
Following is maximum profit sequence of jobs 
c a e 
```

上述解的**时间复杂度**为 O(n <sup>2</sup> )。可以使用**优先级队列(最大堆)**进行优化。

算法如下:

*   根据截止日期对工作进行排序。
*   从头开始迭代，计算每两个连续截止日期之间的可用时间段。在最大堆中包含该作业的利润、截止日期和作业标识。
*   当插槽可用并且最大堆中还有作业时，请在结果中包含具有最大利润和截止日期的作业标识。
*   根据截止日期对结果数组进行排序。

下面是上述算法的实现。

## 蟒蛇 3

```
# Program to find the maximum profit
# job sequence from a given array
# of jobs with deadlines and profits
import heapq

def printJobScheduling(arr):
    n = len(arr)

    # arr[i][0] = job_id, arr[i][1] = deadline, arr[i][2] = profit

    # sorting the array on the
    # basis of their deadlines
    arr.sort(key=lambda x: x[1])

    # initialise the result array and maxHeap
    result = []
    maxHeap = []

    # starting the iteration from the end
    for i in range(n - 1, -1, -1):

        # calculate slots between two deadlines
        if i == 0:
            slots_available = arr[i][1]
        else:
            slots_available = arr[i][1] - arr[i - 1][1]

        # include the profit of job(as priority), deadline
        # and job_id in maxHeap
        # note we push negative value in maxHeap to convert
        # min heap to max heap in python
        heapq.heappush(maxHeap, (-arr[i][2], arr[i][1], arr[i][0]))

        while slots_available and maxHeap:

            # get the job with max_profit
            profit, deadline, job_id = heapq.heappop(maxHeap)

            # reduce the slots
            slots_available -= 1

            # include the job in the result array
            result.append([job_id, deadline])

    # jobs included might be shuffled
    # sort the result array by their deadlines
    result.sort(key=lambda x: x[1])

    for job in result:
        print(job[0], end=" ")
    print()

# Driver COde
arr = [['a', 2, 100],  # Job Array
       ['b', 1, 19],
       ['c', 2, 27],
       ['d', 1, 25],
       ['e', 3, 15]]

print("Following is maximum profit sequence of jobs")

# Function Call
printJobScheduling(arr)

# This code is contributed
# by Shivam Bhagat
```

**Output**

```
Following is maximum profit sequence of jobs
a c e 
```

**时间复杂度** : O(nlog(n))

**空间复杂度** : O(n)

也可以使用不相交集合数据结构进行优化。详情请参考下面的帖子。

[作业排序问题|集合 2(使用不相交集合)](https://www.geeksforgeeks.org/job-sequencing-using-disjoint-set-union/)

**来源:**
[http://OCW . MIT . edu/courses/civil-and-environmental-engineering/1-204-computer-in-algorithms-in-system-engineering-spring-2010/讲义/MIT1_204S10_lec10.pdf](http://ocw.mit.edu/courses/civil-and-environmental-engineering/1-204-computer-algorithms-in-systems-engineering-spring-2010/lecture-notes/MIT1_204S10_lec10.pdf)
本文由 **Shubham** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
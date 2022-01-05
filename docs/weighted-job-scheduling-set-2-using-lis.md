# 加权作业调度|集合 2(使用 LIS)

> 原文:[https://www . geesforgeks . org/weighted-job-scheduling-set-2-using-lis/](https://www.geeksforgeeks.org/weighted-job-scheduling-set-2-using-lis/)

给定 N 个作业，每个作业由以下三个元素表示。
1。开始时间
2。完成时间
3。利润或价值关联
找到工作的最大利润子集，使得子集中没有两个工作重叠。

**示例:**

```
Input:  
Number of Jobs n = 4
Job Details {Start Time, Finish Time, Profit}
Job 1: {1, 2, 50}
Job 2: {3, 5, 20}
Job 3: {6, 19, 100}
Job 4: {2, 100, 200}

Output:  
Job 1: {1, 2, 50}
Job 4: {2, 100, 200}

Explanation: We can get the maximum profit by 
scheduling jobs 1 and 4 and maximum profit is 250.
```

在[之前的](https://www.geeksforgeeks.org/weighted-job-scheduling/)帖子中，我们已经讨论过加权作业调度问题。我们讨论了一个 DP 解决方案，其中我们基本上包括或不包括当前的工作。在这篇文章中，讨论了另一个有趣的动态规划解决方案，我们也打印了作业。这个问题是标准[最长增加子序列(LIS)](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/) 问题的变种。我们需要稍微改变 LIS 问题的动态规划解决方案。

我们首先需要根据开始时间对工作进行分类。让作业[0..n-1]是排序后的作业数组。我们定义向量 L，使得 L[i]本身是存储作业[0]的加权作业调度的向量..那以工作结束。因此，对于索引 I，L[i]可以递归地写成–

```
L[0] = {job[0]}
L[i] = {MaxSum(L[j])} + job[i] where j < i and job[j].finish <= job[i].start
     = job[i], if there is no such j
```

例如，考虑成对{3，10，20}、{1，2，50}、{6，19，100}、{2，100，200}

```
After sorting we get, 
{1, 2, 50}, {2, 100, 200}, {3, 10, 20}, {6, 19, 100}

Therefore,
L[0]: {1, 2, 50}
L[1]: {1, 2, 50} {2, 100, 200}
L[2]: {1, 2, 50} {3, 10, 20}
L[3]: {1, 2, 50} {6, 19, 100}
```

我们选择利润最高的向量。在这种情况下，L[1]。

以下是上述想法的实现–

## C++

```
// C++ program for weighted job scheduling using LIS
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// A job has start time, finish time and profit.
struct Job
{
    int start, finish, profit;
};

// Utility function to calculate sum of all vector
// elements
int findSum(vector<Job> arr)
{
    int sum = 0;
    for (int i = 0; i < arr.size(); i++)
        sum +=  arr[i].profit;
    return sum;
}

// comparator function for sort function
int compare(Job x, Job y)
{
    return x.start < y.start;
}

// The main function that finds the maximum possible
// profit from given array of jobs
void findMaxProfit(vector<Job> &arr)
{
    // Sort arr[] by start time.
    sort(arr.begin(), arr.end(), compare);

    // L[i] stores stores Weighted Job Scheduling of
    // job[0..i] that ends with job[i]
    vector<vector<Job>> L(arr.size());

    // L[0] is equal to arr[0]
    L[0].push_back(arr[0]);

    // start from index 1
    for (int i = 1; i < arr.size(); i++)
    {
        // for every j less than i
        for (int j = 0; j < i; j++)
        {
            // L[i] = {MaxSum(L[j])} + arr[i] where j < i
            // and arr[j].finish <= arr[i].start
            if ((arr[j].finish <= arr[i].start) &&
                (findSum(L[j]) > findSum(L[i])))
                L[i] = L[j];
        }
        L[i].push_back(arr[i]);
    }

    vector<Job> maxChain;

    // find one with max profit
    for (int i = 0; i < L.size(); i++)
        if (findSum(L[i]) > findSum(maxChain))
            maxChain = L[i];

    for (int i = 0; i < maxChain.size(); i++)
        cout << "(" <<  maxChain[i].start << ", " <<
             maxChain[i].finish << ", "
             <<  maxChain[i].profit << ") ";
}

// Driver Function
int main()
{
    Job a[] = { {3, 10, 20}, {1, 2, 50}, {6, 19, 100},
                {2, 100, 200} };
    int n = sizeof(a) / sizeof(a[0]);

    vector<Job> arr(a, a + n);

    findMaxProfit(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for weighted job
// scheduling using LIS
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;

class Graph{

// A job has start time, finish time
// and profit.
static class Job
{
    int start, finish, profit;

    public Job(int start, int finish,
               int profit)
    {
        this.start = start;
        this.finish = finish;
        this.profit = profit;
    }
};

// Utility function to calculate sum of all
// ArrayList elements
static int findSum(ArrayList<Job> arr)
{
    int sum = 0;

    for(int i = 0; i < arr.size(); i++)
        sum += arr.get(i).profit;

    return sum;
}

// The main function that finds the maximum
// possible profit from given array of jobs
static void findMaxProfit(ArrayList<Job> arr)
{

    // Sort arr[] by start time.
    Collections.sort(arr, new Comparator<Job>()
    {
        @Override
        public int compare(Job x, Job y)
        {
            return x.start - y.start;
        }
    });

    // sort(arr.begin(), arr.end(), compare);

    // L[i] stores stores Weighted Job Scheduling of
    // job[0..i] that ends with job[i]
    ArrayList<ArrayList<Job>> L = new ArrayList<>();
    for(int i = 0; i < arr.size(); i++)
    {
        L.add(new ArrayList<>());
    }

    // L[0] is equal to arr[0]
    L.get(0).add(arr.get(0));

    // Start from index 1
    for(int i = 1; i < arr.size(); i++)
    {

        // For every j less than i
        for(int j = 0; j < i; j++)
        {

            // L[i] = {MaxSum(L[j])} + arr[i] where j < i
            // and arr[j].finish <= arr[i].start
            if ((arr.get(j).finish <= arr.get(i).start) &&
                (findSum(L.get(j)) > findSum(L.get(i))))
            {
                ArrayList<Job> copied = new ArrayList<>(
                    L.get(j));
                L.set(i, copied);
            }
        }
        L.get(i).add(arr.get(i));
    }

    ArrayList<Job> maxChain = new ArrayList<>();

    // Find one with max profit
    for(int i = 0; i < L.size(); i++)
        if (findSum(L.get(i)) > findSum(maxChain))
            maxChain = L.get(i);

    for(int i = 0; i < maxChain.size(); i++)
    {
        System.out.printf("(%d, %d, %d)\n",
              maxChain.get(i).start,
              maxChain.get(i).finish,
              maxChain.get(i).profit);
    }
}

// Driver code
public static void main(String[] args)
{
    Job[] a = { new Job(3, 10, 20),
                new Job(1, 2, 50),
                new Job(6, 19, 100),
                new Job(2, 100, 200) };

    ArrayList<Job> arr = new ArrayList<>(
        Arrays.asList(a));

    findMaxProfit(arr);
}
}

// This code is contributed by sanjeev2552
```

**输出:**

```
(1, 2, 50) (2, 100, 200)
```

我们可以通过移除 findSum()函数来进一步优化上述 DP 解决方案。相反，我们可以维护另一个向量/数组来存储作业 I 之前可能的最大利润之和。

**上述动态规划解的时间复杂度**为 O(n <sup>2</sup> ，其中 n 为作业数。
**程序使用的辅助空间**为 O(n <sup>2</sup> )。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
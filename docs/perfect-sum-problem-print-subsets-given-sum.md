# 完美和问题(打印给定和的所有子集)

> 原文:[https://www . geesforgeks . org/perfect-sum-问题-打印-子集-给定-sum/](https://www.geeksforgeeks.org/perfect-sum-problem-print-subsets-given-sum/)

给定一个整数数组和一个和，任务是打印给定数组的所有子集，其中和等于给定和。
示例:

```
Input : arr[] = {2, 3, 5, 6, 8, 10}
        sum = 10
Output : 5 2 3
         2 8
         10

Input : arr[] = {1, 2, 3, 4, 5}
        sum = 10
Output : 4 3 2 1 
         5 3 2 
         5 4 1 
```

在乐购问

这个问题主要是[子集和问题](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)的扩展。这里我们不仅需要找到是否有给定和的子集，还需要打印给定和的所有子集。
就像[之前的帖子](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)一样，我们构建了一个 2D 数组 dp[][]，这样 dp[i][j]就可以存储 true，前提是数组元素从 0 到 I 的和 j 是可能的。
在填充 dp[][]之后，我们从 DP[n-1][和]递归遍历它。对于被遍历的单元，我们在到达之前存储路径，并考虑元素的两种可能性。
1)电流路径中包含元素。
2)元素不包含在当前路径中。
每当和变为 0 时，我们停止递归调用并打印当前路径。
以下是上述想法的实现。

## C++

```
// C++ program to count all subsets with
// given sum.
#include <bits/stdc++.h>
using namespace std;

// dp[i][j] is going to store true if sum j is
// possible with array elements from 0 to i.
bool** dp;

void display(const vector<int>& v)
{
    for (int i = 0; i < v.size(); ++i)
        printf("%d ", v[i]);
    printf("\n");
}

// A recursive function to print all subsets with the
// help of dp[][]. Vector p[] stores current subset.
void printSubsetsRec(int arr[], int i, int sum, vector<int>& p)
{
    // If we reached end and sum is non-zero. We print
    // p[] only if arr[0] is equal to sun OR dp[0][sum]
    // is true.
    if (i == 0 && sum != 0 && dp[0][sum])
    {
        p.push_back(arr[i]);
        // Display Only when Sum of elements of p is equal to sum
          if (arr[i] == sum)
              display(p);
        return;
    }

    // If sum becomes 0
    if (i == 0 && sum == 0)
    {
        display(p);
        return;
    }

    // If given sum can be achieved after ignoring
    // current element.
    if (dp[i-1][sum])
    {
        // Create a new vector to store path
        vector<int> b = p;
        printSubsetsRec(arr, i-1, sum, b);
    }

    // If given sum can be achieved after considering
    // current element.
    if (sum >= arr[i] && dp[i-1][sum-arr[i]])
    {
        p.push_back(arr[i]);
        printSubsetsRec(arr, i-1, sum-arr[i], p);
    }
}

// Prints all subsets of arr[0..n-1] with sum 0.
void printAllSubsets(int arr[], int n, int sum)
{
    if (n == 0 || sum < 0)
       return;

    // Sum 0 can always be achieved with 0 elements
    dp = new bool*[n];
    for (int i=0; i<n; ++i)
    {
        dp[i] = new bool[sum + 1];
        dp[i][0] = true;
    }

    // Sum arr[0] can be achieved with single element
    if (arr[0] <= sum)
       dp[0][arr[0]] = true;

    // Fill rest of the entries in dp[][]
    for (int i = 1; i < n; ++i)
        for (int j = 0; j < sum + 1; ++j)
            dp[i][j] = (arr[i] <= j) ? dp[i-1][j] ||
                                       dp[i-1][j-arr[i]]
                                     : dp[i - 1][j];
    if (dp[n-1][sum] == false)
    {
        printf("There are no subsets with sum %d\n", sum);
        return;
    }

    // Now recursively traverse dp[][] to find all
    // paths from dp[n-1][sum]
    vector<int> p;
    printSubsetsRec(arr, n-1, sum, p);
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    int sum = 10;
    printAllSubsets(arr, n, sum);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to count all subsets with given sum.
import java.util.ArrayList;
public class SubSet_sum_problem
{
    // dp[i][j] is going to store true if sum j is
    // possible with array elements from 0 to i.
    static boolean[][] dp;

    static void display(ArrayList<Integer> v)
    {
       System.out.println(v);
    }

    // A recursive function to print all subsets with the
    // help of dp[][]. Vector p[] stores current subset.
    static void printSubsetsRec(int arr[], int i, int sum,
                                         ArrayList<Integer> p)
    {
        // If we reached end and sum is non-zero. We print
        // p[] only if arr[0] is equal to sun OR dp[0][sum]
        // is true.
        if (i == 0 && sum != 0 && dp[0][sum])
        {
            p.add(arr[i]);
            display(p);
            p.clear();
            return;
        }

        // If sum becomes 0
        if (i == 0 && sum == 0)
        {
            display(p);
            p.clear();
            return;
        }

        // If given sum can be achieved after ignoring
        // current element.
        if (dp[i-1][sum])
        {
            // Create a new vector to store path
            ArrayList<Integer> b = new ArrayList<>();
            b.addAll(p);
            printSubsetsRec(arr, i-1, sum, b);
        }

        // If given sum can be achieved after considering
        // current element.
        if (sum >= arr[i] && dp[i-1][sum-arr[i]])
        {
            p.add(arr[i]);
            printSubsetsRec(arr, i-1, sum-arr[i], p);
        }
    }

    // Prints all subsets of arr[0..n-1] with sum 0.
    static void printAllSubsets(int arr[], int n, int sum)
    {
        if (n == 0 || sum < 0)
           return;

        // Sum 0 can always be achieved with 0 elements
        dp = new boolean[n][sum + 1];
        for (int i=0; i<n; ++i)
        {
            dp[i][0] = true; 
        }

        // Sum arr[0] can be achieved with single element
        if (arr[0] <= sum)
           dp[0][arr[0]] = true;

        // Fill rest of the entries in dp[][]
        for (int i = 1; i < n; ++i)
            for (int j = 0; j < sum + 1; ++j)
                dp[i][j] = (arr[i] <= j) ? (dp[i-1][j] ||
                                           dp[i-1][j-arr[i]])
                                         : dp[i - 1][j];
        if (dp[n-1][sum] == false)
        {
            System.out.println("There are no subsets with" +
                                                  " sum "+ sum);
            return;
        }

        // Now recursively traverse dp[][] to find all
        // paths from dp[n-1][sum]
        ArrayList<Integer> p = new ArrayList<>();
        printSubsetsRec(arr, n-1, sum, p);
    }

    //Driver Program to test above functions
    public static void main(String args[])
    {
        int arr[] = {1, 2, 3, 4, 5};
        int n = arr.length;
        int sum = 10;
        printAllSubsets(arr, n, sum);
    }
}
//This code is contributed by Sumit Ghosh
```

**输出:**

```
4 3 2 1
5 3 2
5 4 1
```

**另一种方法:**
对于数组中的每个元素，首先决定它是否在子集内。定义一个函数来处理这一切。该函数在主函数中被调用一次。声明了将由我们的函数操作的静态类字段。每次调用时，函数都会检查字段的状态。在我们的例子中，它检查当前总和是否等于给定的总和，并相应地增加相应的类字段。如果不是，它通过接受所有案例来进行函数调用。所以函数调用的数量将等于案例的数量。因此，这里进行了两次调用——一次是取子集中的元素并增加当前总和，另一次是不取元素。
下面是实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the number of
// possible subset with given sum
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {

    static int count;
    static int sum;
    static int n;

    // Driver code
    public static void main (String[] args) {
        count = 0;
        n = 5;
        sum = 10;

        int[] pat = {2, 3, 5, 6, 8, 10};

        f(pat, 0, 0);

        System.out.println(count);
    }

    // Function to select or not the array element
    // to form a subset with given sum
    static void f(int[] pat, int i, int currSum) {
        if (currSum == sum) {
            count++;
            return;
        }
        if (currSum < sum && i < n) {
            f(pat, i+1, currSum + pat[i]);
            f(pat, i+1, currSum);
        }
    }
}
```

**输出:**

```
4 3 2 1 
5 3 2 
5 4 1 
```

本文由 **Jas Kaur** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
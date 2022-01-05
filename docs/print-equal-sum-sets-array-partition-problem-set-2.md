# 打印数组等和集(分割问题)|集 2

> 原文:[https://www . geesforgeks . org/print-equal-sum-set-array-partition-problem-set-2/](https://www.geeksforgeeks.org/print-equal-sum-sets-array-partition-problem-set-2/)

给定数组 arr[]。确定是否可以将数组分成两组，使两组中的元素之和相等。如果可能，打印两套。如果不可能，则输出-1。
**例:**

```
Input : arr = {5, 5, 1, 11}
Output : Set 1 = {5, 5, 1}, Set 2 = {11}
Sum of both the sets is 11 and equal.

Input : arr = {1, 5, 3}
Output : -1
No partitioning results in equal sum sets.
```

[Recommended: Please try your approach first on IDE and then look at the solution.](https://ide.geeksforgeeks.org) 

**先决条件:** [分区问题](https://www.geeksforgeeks.org/dynamic-programming-set-18-partition-problem/)
T5】方法:在[之前的](https://www.geeksforgeeks.org/print-equal-sum-sets-array-partition-problem/)帖子中，讨论了使用[递归](https://www.geeksforgeeks.org/recursion/)的解决方案。在这篇文章中，解释了一个使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)的解决方案。
思路是声明两个集合集 1 和集 2。要恢复解决方案，请从最终结果 dp[n][k]开始向后遍历布尔 dp 表，其中 n =元素数量，k = sum/2。集合 1 将由对总和 k 有贡献的元素组成，其他没有贡献的元素被添加到集合 2。在每个位置遵循这些步骤来恢复解决方案。

1.  检查 dp[i-1][sum]是否正确。如果为真，则当前元素对总和 k 没有贡献。将此元素添加到集合 2。用 i-1 更新指数 I，总和保持不变。

2.  如果 dp[i-1][sum]为假，则当前元素贡献 sum k。将当前元素添加到集合 1。用 i-1 和 sum-arr[i-1]更新索引 I。

重复以上步骤，直到遍历每个索引位置。
**执行:**

## C++

```
// CPP program to print equal sum sets of array.
#include <bits/stdc++.h>
using namespace std;

// Function to print equal sum
// sets of array.
void printEqualSumSets(int arr[], int n)
{
    int i, currSum;

    // Finding sum of array elements
    int sum = accumulate(arr, arr+n, 0);

    // Check sum is even or odd. If odd
    // then array cannot be partitioned.
    // Print -1 and return.
    if (sum & 1) {
        cout << "-1";
        return;
    }

    // Divide sum by 2 to find
    // sum of two possible subsets.
    int k = sum >> 1;

    // Boolean DP table to store result
    // of states.
    // dp[i][j] = true if there is a
    // subset of elements in first i elements
    // of array that has sum equal to j.
    bool dp[n + 1][k + 1];

    // If number of elements are zero, then
    // no sum can be obtained.
    for (i = 1; i <= k; i++)
        dp[0][i] = false;

    // Sum 0 can be obtained by not selecting
    // any element.
    for (i = 0; i <= n; i++)
        dp[i][0] = true;

    // Fill the DP table in bottom up manner.
    for (i = 1; i <= n; i++) {
        for (currSum = 1; currSum <= k; currSum++) {

            // Excluding current element.
            dp[i][currSum] = dp[i - 1][currSum];

            // Including current element
            if (arr[i - 1] <= currSum)
                dp[i][currSum] = dp[i][currSum] |
                  dp[i - 1][currSum - arr[i - 1]];
        }
    }

    // Required sets set1 and set2.
    vector<int> set1, set2;

    // If partition is not possible print
    // -1 and return.
    if (!dp[n][k]) {
        cout << "-1\n";
        return;
    }

    // Start from last element in dp table.
    i = n;
    currSum = k;

    while (i > 0 && currSum >= 0) {

        // If current element does not
        // contribute to k, then it belongs
        // to set 2.
        if (dp[i - 1][currSum]) {
            i--;
            set2.push_back(arr[i]);
        }

        // If current element contribute
        // to k then it belongs to set 1.
        else if (dp[i - 1][currSum - arr[i - 1]]) {
            i--;
            currSum -= arr[i];
            set1.push_back(arr[i]);
        }
    }

    // Print elements of both the sets.
    cout << "Set 1 elements: ";
    for (i = 0; i < set1.size(); i++)
        cout << set1[i] << " ";
    cout << "\nSet 2 elements: ";
    for (i = 0; i < set2.size(); i++)
        cout << set2[i] << " ";   
}

// Driver program.
int main()
{
    int arr[] = { 5, 5, 1, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printEqualSumSets(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// equal sum sets of array.
import java.io.*;
import java.util.*;

class GFG
{
    // Function to print equal
    // sum sets of array.
    static void printEqualSumSets(int []arr,
                                  int n)
    {
        int i, currSum, sum = 0;

        // Finding sum of array elements
        for (i = 0; i < arr.length; i++)
            sum += arr[i];

        // Check sum is even or odd.
        // If odd then array cannot
        // be partitioned. Print -1
        // and return.
        if ((sum & 1) == 1)
        {
            System.out.print("-1");
            return;
        }

        // Divide sum by 2 to find
        // sum of two possible subsets.
        int k = sum >> 1;

        // Boolean DP table to store
        // result of states.
        // dp[i,j] = true if there is a
        // subset of elements in first i
        // elements of array that has sum
        // equal to j.
        boolean [][]dp = new boolean[n + 1][k + 1];

        // If number of elements are zero,
        // then no sum can be obtained.
        for (i = 1; i <= k; i++)
            dp[0][i] = false;

        // Sum 0 can be obtained by
        // not selecting any element.
        for (i = 0; i <= n; i++)
            dp[i][0] = true;

        // Fill the DP table
        // in bottom up manner.
        for (i = 1; i <= n; i++)
        {
            for (currSum = 1;
                 currSum <= k;
                 currSum++)
            {

                // Excluding current element.
                dp[i][currSum] = dp[i - 1][currSum];

                // Including current element
                if (arr[i - 1] <= currSum)
                    dp[i][currSum] = dp[i][currSum] |
                    dp[i - 1][currSum - arr[i - 1]];
            }
        }

        // Required sets set1 and set2.
        List<Integer> set1 = new ArrayList<Integer>();
        List<Integer> set2 = new ArrayList<Integer>();

        // If partition is not possible
        // print -1 and return.
        if (!dp[n][k])
        {
            System.out.print("-1\n");
            return;
        }

        // Start from last
        // element in dp table.
        i = n;
        currSum = k;

        while (i > 0 && currSum >= 0)
        {

            // If current element does
            // not contribute to k, then
            // it belongs to set 2.
            if (dp[i - 1][currSum])
            {
                i--;
                set2.add(arr[i]);
            }

            // If current element contribute
            // to k then it belongs to set 1.
            else if (dp[i - 1][currSum - arr[i - 1]])
            {
                i--;
                currSum -= arr[i];
                set1.add(arr[i]);
            }
        }

        // Print elements of both the sets.
        System.out.print("Set 1 elements: ");
        for (i = 0; i < set1.size(); i++)
            System.out.print(set1.get(i) + " ");

        System.out.print("\nSet 2 elements: ");

        for (i = 0; i < set2.size(); i++)
            System.out.print(set2.get(i) + " ");
    }

    // Driver Code
    public static void main(String args[])
    {
        int []arr = new int[]{ 5, 5, 1, 11 };
        int n = arr.length;
        printEqualSumSets(arr, n);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to print equal sum
# sets of array.
import numpy as np

# Function to print equal sum
# sets of array.
def printEqualSumSets(arr, n) :

    # Finding sum of array elements
    sum_array = sum(arr)

    # Check sum is even or odd. If odd
    # then array cannot be partitioned.
    # Print -1 and return.
    if (sum_array & 1) :
        print("-1")
        return

    # Divide sum by 2 to find
    # sum of two possible subsets.
    k = sum_array >> 1

    # Boolean DP table to store result
    # of states.
    # dp[i][j] = true if there is a
    # subset of elements in first i elements
    # of array that has sum equal to j.
    dp = np.zeros((n + 1, k + 1))

    # If number of elements are zero, then
    # no sum can be obtained.
    for i in range(1, k + 1) :
        dp[0][i] = False

    # Sum 0 can be obtained by not
    # selecting any element.
    for i in range(n + 1) :
        dp[i][0] = True

    # Fill the DP table in bottom up manner.
    for i in range(1, n + 1) :
        for currSum in range(1, k + 1) :

            # Excluding current element.
            dp[i][currSum] = dp[i - 1][currSum]

            # Including current element
            if (arr[i - 1] <= currSum) :
                dp[i][currSum] = (dp[i][currSum] or
                                  dp[i - 1][currSum - arr[i - 1]])

    # Required sets set1 and set2.
    set1, set2 = [], []

    # If partition is not possible print
    # -1 and return.
    if ( not dp[n][k]) :
        print("-1")
        return

    # Start from last element in dp table.
    i = n
    currSum = k

    while (i > 0 and currSum >= 0) :

        # If current element does not
        # contribute to k, then it belongs
        # to set 2.
        if (dp[i - 1][currSum]) :
            i -= 1
            set2.append(arr[i])

        # If current element contribute
        # to k then it belongs to set 1.
        elif (dp[i - 1][currSum - arr[i - 1]]) :
            i -= 1
            currSum -= arr[i]
            set1.append(arr[i])

    # Print elements of both the sets.
    print("Set 1 elements:", end = " ")
    for i in range(len(set1)) :
        print(set1[i], end = " ")

    print("\nSet 2 elements:", end = " ")
    for i in range(len(set2)) :
        print(set2[i], end = " ")    

# Driver Code
if __name__ == "__main__" :

    arr = [ 5, 5, 1, 11 ]
    n = len(arr)
    printEqualSumSets(arr, n)

# This code is contributed by Ryuga
```

## C#

```
// C# program to print
// equal sum sets of array.
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{
    // Function to print equal
    // sum sets of array.
    static void printEqualSumSets(int []arr,
                                  int n)
    {
        int i, currSum, sum = 0;

        // Finding sum of array elements
        for (i = 0; i < arr.Length; i++)
            sum += arr[i];

        // Check sum is even or odd.
        // If odd then array cannot
        // be partitioned. Print -1
        // and return.
        if ((sum & 1) == 1)
        {
            Console.Write("-1");
            return;
        }

        // Divide sum by 2 to find
        // sum of two possible subsets.
        int k = sum >> 1;

        // Boolean DP table to store
        // result of states.
        // dp[i,j] = true if there is a
        // subset of elements in first i
        // elements of array that has sum
        // equal to j.
        bool [,]dp = new bool[n + 1, k + 1];

        // If number of elements are zero,
        // then no sum can be obtained.
        for (i = 1; i <= k; i++)
            dp[0, i] = false;

        // Sum 0 can be obtained by
        // not selecting any element.
        for (i = 0; i <= n; i++)
            dp[i, 0] = true;

        // Fill the DP table
        // in bottom up manner.
        for (i = 1; i <= n; i++)
        {
            for (currSum = 1; currSum <= k; currSum++)
            {

                // Excluding current element.
                dp[i, currSum] = dp[i - 1, currSum];

                // Including current element
                if (arr[i - 1] <= currSum)
                    dp[i, currSum] = dp[i, currSum] |
                    dp[i - 1, currSum - arr[i - 1]];
            }
        }

        // Required sets set1 and set2.
        List<int> set1 = new List<int>();
        List<int> set2 = new List<int>();

        // If partition is not possible
        // print -1 and return.
        if (!dp[n, k])
        {
            Console.Write("-1\n");
            return;
        }

        // Start from last
        // element in dp table.
        i = n;
        currSum = k;

        while (i > 0 && currSum >= 0)
        {

            // If current element does
            // not contribute to k, then
            // it belongs to set 2.
            if (dp[i - 1, currSum])
            {
                i--;
                set2.Add(arr[i]);
            }

            // If current element contribute
            // to k then it belongs to set 1.
            else if (dp[i - 1, currSum - arr[i - 1]])
            {
                i--;
                currSum -= arr[i];
                set1.Add(arr[i]);
            }
        }

        // Print elements of both the sets.
        Console.Write("Set 1 elements: ");
        for (i = 0; i < set1.Count; i++)
            Console.Write(set1[i] + " ");

        Console.Write("\nSet 2 elements: ");

        for (i = 0; i < set2.Count; i++)
            Console.Write(set2[i] + " ");
    }

    // Driver Code.
    static void Main()
    {
        int []arr = { 5, 5, 1, 11 };
        int n = arr.Length;
        printEqualSumSets(arr, n);
    }
}
// This cide is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>

// Javascript program to print equal sum sets of array.

// Function to print equal sum
// sets of array.
function printEqualSumSets(arr, n)
{
    var i, currSum;

    // Finding sum of array elements
    var sum = 0;

    for(var i =0; i< arr.length; i++)
    {
        sum+=arr[i];
    }

    // Check sum is even or odd. If odd
    // then array cannot be partitioned.
    // Print -1 and return.
    if (sum & 1) {
        document.write( "-1");
        return;
    }

    // Divide sum by 2 to find
    // sum of two possible subsets.
    var k = sum >> 1;

    // Boolean DP table to store result
    // of states.
    // dp[i][j] = true if there is a
    // subset of elements in first i elements
    // of array that has sum equal to j.
    var dp = Array.from(Array(n+1), ()=> Array(k+1));

    // If number of elements are zero, then
    // no sum can be obtained.
    for (i = 1; i <= k; i++)
        dp[0][i] = false;

    // Sum 0 can be obtained by not selecting
    // any element.
    for (i = 0; i <= n; i++)
        dp[i][0] = true;

    // Fill the DP table in bottom up manner.
    for (i = 1; i <= n; i++) {
        for (currSum = 1; currSum <= k; currSum++) {

            // Excluding current element.
            dp[i][currSum] = dp[i - 1][currSum];

            // Including current element
            if (arr[i - 1] <= currSum)
                dp[i][currSum] = dp[i][currSum] |
                  dp[i - 1][currSum - arr[i - 1]];
        }
    }

    // Required sets set1 and set2.
    var set1 = [], set2=[];

    // If partition is not possible print
    // -1 and return.
    if (!dp[n][k]) {
        document.write( "-1<br>");
        return;
    }

    // Start from last element in dp table.
    i = n;
    currSum = k;

    while (i > 0 && currSum >= 0) {

        // If current element does not
        // contribute to k, then it belongs
        // to set 2.
        if (dp[i - 1][currSum]) {
            i--;
            set2.push(arr[i]);
        }

        // If current element contribute
        // to k then it belongs to set 1.
        else if (dp[i - 1][currSum - arr[i - 1]]) {
            i--;
            currSum -= arr[i];
            set1.push(arr[i]);
        }
    }

    // Print elements of both the sets.
    document.write( "Set 1 elements: ");
    for (i = 0; i < set1.length; i++)
        document.write( set1[i] + " ");
    document.write( "<br>Set 2 elements: ");
    for (i = 0; i < set2.length; i++)
        document.write( set2[i] + " ");   
}

// Driver program.
var arr = [ 5, 5, 1, 11 ];
var n = arr.length;
printEqualSumSets(arr, n);

</script>
```

**Output :** 

```
Set 1 elements: 1 5 5 
Set 2 elements: 11
```

**时间复杂度:** O(n*k)，其中 k =和(arr) / 2
**辅助空间:** O(n*k)
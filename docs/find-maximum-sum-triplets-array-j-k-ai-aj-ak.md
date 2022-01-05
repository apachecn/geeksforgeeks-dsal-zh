# 求数组中三元组的最大和，比如 i < j < k 和 a【I】<a【j】<a【k】

> 原文:[https://www . geesforgeks . org/find-maximum-sum-triples-array-j-k-ai-aj-AK/](https://www.geeksforgeeks.org/find-maximum-sum-triplets-array-j-k-ai-aj-ak/)

给定一个 n 大小的正整数数组，求三元组(a<sub>I</sub>+a<sub>j</sub>+a<sub>k</sub>)的最大和，使得 0<=**I<j<k**T19】n 和**a<sub>I</sub>T20】a<sub>j</sub>T21】a<sub>k</sub>T15】。**

```
Input: a[] = 2 5 3 1 4 9
Output: 16

Explanation:
All possible triplets are:-
2 3 4 => sum = 9
2 5 9 => sum = 16
2 3 9 => sum = 14
3 4 9 => sum = 16
1 4 9 => sum = 14
Maximum sum = 16
```

**简单的方法**是遍历每一个带有三个嵌套‘for loops’的三元组，并逐个查找更新所有三元组的总和。这种方法的时间复杂度为 0(n<sup>3</sup>，这对于较大的“n”值是不够的。

**更好的做法**是在上述做法上做进一步的优化。我们可以遍历两个嵌套循环，而不是遍历带有三个嵌套循环的每个三元组。遍历每个数字(假设为中间元素(a <sub>j</sub> ))时，找出比它前面的一个 <sub>j</sub> 小的最大数字(a <sub>i</sub> )和比它后面的一个 <sub>j</sub> 大的最大数字(a <sub>k</sub> )。之后，用计算出的 a<sub>I</sub>+a<sub>j</sub>+a<sub>k</sub>之和更新最大答案

## C++

```
// C++ program to find maximum triplet sum
#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum triplet sum
int maxTripletSum(int arr[], int n)
{
    // Initialize the answer
    int ans = 0;

    for (int i = 1; i < n - 1; ++i) {
        int max1 = 0, max2 = 0;

        // find maximum value(less than arr[i])
        // from 0 to i-1
        for (int j = 0; j < i; ++j)
            if (arr[j] < arr[i])
                max1 = max(max1, arr[j]);

        // find maximum value(greater than arr[i])
        // from i+1 to n-1
        for (int j = i + 1; j < n; ++j)
            if (arr[j] > arr[i])
                max2 = max(max2, arr[j]);

        // store maximum answer
        if(max1 && max2)
             ans=max(ans,max1+arr[i]+max2);
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 5, 3, 1, 4, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxTripletSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum triplet sum

import java.io.*;
import java.math.*;

class GFG {

    // Function to calculate maximum triplet sum
    static int maxTripletSum(int arr[], int n)
    {
        // Initialize the answer
        int ans = 0;

        for (int i = 1; i < n - 1; ++i) {
            int max1 = 0, max2 = 0;

            // find maximum value(less than arr[i])
            // from 0 to i-1
            for (int j = 0; j < i; ++j)
                if (arr[j] < arr[i])
                    max1 = Math.max(max1, arr[j]);

            // find maximum value(greater than arr[i])
            // from i+1 to n-1
            for (int j = i + 1; j < n; ++j)
                if (arr[j] > arr[i])
                    max2 = Math.max(max2, arr[j]);

            // store maximum answer
        if(max1 > 0 && max2 > 0)
            ans = Math.max(ans, max1 + arr[i] + max2);
        }

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 2, 5, 3, 1, 4, 9 };
        int n = arr.length;
        System.out.println(maxTripletSum(arr, n));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 program to
# find maximum triplet sum

# Function to calculate
# maximum triplet sum

def maxTripletSum(arr, n):

    # Initialize the answer
    ans = 0

    for i in range(1, (n - 1)):
        max1 = 0
        max2 = 0

        # find maximum value(less than arr[i])
        # from 0 to i-1
        for j in range(0, i):
            if (arr[j] < arr[i]):
                max1 = max(max1, arr[j])

        # find maximum value(greater than arr[i])
        # from i + 1 to n-1
        for j in range((i + 1), n):
            if (arr[j] > arr[i]):
                max2 = max(max2, arr[j])

        # store maximum answer
                if (max1 > 0 and max2 >0):
                    ans = max(ans, max1 + arr[i] + max2)

    return ans

# Driver code

arr = [2, 5, 3, 1, 4, 9]
n = len(arr)
print(maxTripletSum(arr, n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to find maximum triplet sum
using System;

class GFG {

    // Function to calculate maximum triplet sum
    static int maxTripletSum(int[] arr, int n)
    {

        // Initialize the answer
        int ans = 0;

        for (int i = 1; i < n - 1; ++i)
        {
            int max1 = 0, max2 = 0;

            // find maximum value(less than
            // arr[i]) from 0 to i-1
            for (int j = 0; j < i; ++j)
                if (arr[j] < arr[i])
                    max1 = Math.Max(max1, arr[j]);

            // find maximum value(greater than
            // arr[i]) from i+1 to n-1
            for (int j = i + 1; j < n; ++j)
                if (arr[j] > arr[i])
                    max2 = Math.Max(max2, arr[j]);

            // store maximum answer
        if(max1 > 0 && max2 > 0)
            ans = Math.Max(ans, max1 + arr[i] + max2);
        }

        return ans;
    }

    // Driver code
    public static void Main()
    {

        int[] arr = { 2, 5, 3, 1, 4, 9 };
        int n = arr.Length;

        Console.WriteLine(maxTripletSum(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum triplet sum

// Function to calculate maximum triplet sum
function maxTripletSum($arr, $n)
{

    // Initialize the answer
    $ans = 0;

    for ($i = 1; $i < $n - 1; ++$i)
    {
        $max1 = 0; $max2 = 0;

        // find maximum value(less than
        // arr[i]) from 0 to i-1
        for ($j = 0; $j < $i; ++$j)
            if ($arr[$j] < $arr[$i])
                $max1 = max($max1, $arr[$j]);

        // find maximum value(greater than
        // arr[i]) from i+1 to n-1
        for ($j = $i + 1; $j < $n; ++$j)
            if ($arr[$j] > $arr[$i])
                $max2 = max($max2, $arr[$j]);

        // store maximum answer
        if($max1 && $max2)
             $ans = max($ans, $max1 + $arr[$i] + $max2);
    }

    return $ans;
}

    // Driver code
    $arr = array(2, 5, 3, 1, 4, 9);
    $n = sizeof($arr);
    echo maxTripletSum($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find maximum triplet sum

// Function to calculate maximum triplet sum
function maxTripletSum(arr, n)
{
    // Initialize the answer
    let ans = 0;

    for (let i = 1; i < n - 1; ++i) {
        let max1 = 0, max2 = 0;

        // find maximum value(less than arr[i])
        // from 0 to i-1
        for (let j = 0; j < i; ++j)
            if (arr[j] < arr[i])
                max1 = Math.max(max1, arr[j]);

        // find maximum value(greater than arr[i])
        // from i+1 to n-1
        for (let j = i + 1; j < n; ++j)
            if (arr[j] > arr[i])
                max2 = Math.max(max2, arr[j]);

        // store maximum answer
        if(max1 && max2)
            ans=Math.max(ans,max1+arr[i]+max2);
    }

    return ans;
}

// Driver code
    let arr = [ 2, 5, 3, 1, 4, 9 ];
    let n = arr.length;
    document.write(maxTripletSum(arr, n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
16
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(1)

**最佳有效的**方法是使用最大后缀-数组和二分搜索法的概念。

*   为了找到一个大于给定数的最大数，我们可以保持一个最大后缀数组，这样对于任何数(后缀 <sub>i</sub> )它都将包含索引 I 中的最大数，i+1，… n-1。后缀数组可以用 O(n)时间计算。
*   为了找到比前面给定数字小的最大数字，我们可以在给定数字之前维护一个排序的数字列表，这样我们可以简单地执行二分搜索法运算来找到比给定数字小的数字。在 C++语言中，我们可以通过使用 STL 库的[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)关联容器来实现。

## C++

```
// C++ program to find maximum triplet sum
#include <bits/stdc++.h>
using namespace std;

// Utility function to get the lower last min
// value of 'n'
int getLowValue(set<int>& lowValue, int& n)
{
    auto it = lowValue.lower_bound(n);

    // Since 'lower_bound' returns the first
    // iterator greater than 'n', thus we
    // have to decrement the pointer for
    // getting the minimum value
    --it;

    return (*it);
}

// Function to calculate maximum triplet sum
int maxTripletSum(int arr[], int n)
{
    // Initialize suffix-array
    int maxSuffArr[n + 1];

    // Set the last element
    maxSuffArr[n] = 0;

    // Calculate suffix-array containing maximum
    // value for index i, i+1, i+2, ... n-1 in
    // arr[i]
    for (int i = n - 1; i >= 0; --i)
        maxSuffArr[i] = max(maxSuffArr[i + 1], arr[i]);

    int ans = 0;

    // Initialize set container
    set<int> lowValue;

    // Insert minimum value for first comparison
    // in the set
    lowValue.insert(INT_MIN);

    for (int i = 0; i < n - 1; ++i) {
        if (maxSuffArr[i + 1] > arr[i]) {
            ans = max(ans, getLowValue(lowValue,
                                       arr[i])
                               + arr[i] + maxSuffArr[i + 1]);

            // Insert arr[i] in set<> for further
            // processing
            lowValue.insert(arr[i]);
        }
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 5, 3, 1, 4, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxTripletSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum triplet sum
import java.io.*;
import java.util.*;

class GFG{

// Function to calculate maximum triplet sum
public static int maxTripletSum(int arr[], int n)
{

    // Initialize suffix-array
    int maxSuffArr[] = new int[n + 1];

    // Set the last element
    maxSuffArr[n] = 0;

    // Calculate suffix-array containing maximum
    // value for index i, i+1, i+2, ... n-1 in
    // arr[i]
    for(int i = n - 1; i >= 0; --i)
        maxSuffArr[i] = Math.max(maxSuffArr[i + 1],
                                        arr[i]);

    int ans = 0;

    // Initialize set container
    TreeSet<Integer> lowValue = new TreeSet<Integer>();

    // Insert minimum value for first comparison
    // in the set
    lowValue.add(Integer.MIN_VALUE);

    for(int i = 0; i < n - 1; ++i)
    {
        if (maxSuffArr[i + 1] > arr[i])
        {
            ans = Math.max(ans, lowValue.lower(arr[i]) +
                           arr[i] + maxSuffArr[i + 1]);

            // Insert arr[i] in set<> for further
            // processing
            lowValue.add(arr[i]);
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 5, 3, 1, 4, 9 };
    int n = 6;

    System.out.println(maxTripletSum(arr, n));
}
}

// This code is contributed by Manu Pathria
```

**输出:**

```
16
```

**时间复杂度:**O(n * log(n))
T3】辅助空间: O(n)

本文由 [Shubham Bansal](https://www.quora.com/profile/Shubham-Bansal-209) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章，或者把你的文章发到投稿@geeksforgeeksorg。看到你的文章出现在极客主页，帮助其他极客
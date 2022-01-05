# 使用允许重复的数组元素求和到 N 的方法

> 原文:[https://www . geesforgeks . org/way-sum-n-using-array-elements-repeat-allowed/](https://www.geeksforgeeks.org/ways-sum-n-using-array-elements-repetition-allowed/)

给定一组 m 个不同的正整数和值“N”。问题是通过对数组元素求和来计算我们形成“N”的方法的总数。允许重复和不同的安排。
**例:**

```
Input : arr = {1, 5, 6}, N = 7
Output : 6

Explanation:- The different ways are:
1+1+1+1+1+1+1
1+1+5
1+5+1
5+1+1
1+6
6+1

Input : arr = {12, 3, 1, 9}, N = 14
Output : 150
```

**方法:**该方法基于动态规划的概念。

```
countWays(arr, m, N)
        Declare and initialize count[N + 1] = {0}
        count[0] = 1
        for i = 1 to N
            for j = 0 to m - 1
                if i >= arr[j]
                   count[i] += count[i - arr[j]]
        return count[N] 
```

下面是上述方法的实现。

## C++

```
// C++ implementation to count ways
// to sum up to a given value N
#include <bits/stdc++.h>

using namespace std;

// function to count the total
// number of ways to sum up to 'N'
int countWays(int arr[], int m, int N)
{
    int count[N + 1];
    memset(count, 0, sizeof(count));

    // base case
    count[0] = 1;

    // count ways for all values up
    // to 'N' and store the result
    for (int i = 1; i <= N; i++)
        for (int j = 0; j < m; j++)

            // if i >= arr[j] then
            // accumulate count for value 'i' as
            // ways to form value 'i-arr[j]'
            if (i >= arr[j])
                count[i] += count[i - arr[j]];

    // required number of ways
    return count[N];

}

// Driver code
int main()
{
    int arr[] = {1, 5, 6};
    int m = sizeof(arr) / sizeof(arr[0]);
    int N = 7;
    cout << "Total number of ways = "
        << countWays(arr, m, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count ways 
// to sum up to a given value N

class Gfg
{
    static int arr[] = {1, 5, 6};

    // method to count the total number
    // of ways to sum up to 'N'
    static int countWays(int N)
    {
        int count[] = new int[N + 1];

        // base case
        count[0] = 1;

        // count ways for all values up
        // to 'N' and store the result
        for (int i = 1; i <= N; i++)
            for (int j = 0; j < arr.length; j++)

                // if i >= arr[j] then
                // accumulate count for value 'i' as
                // ways to form value 'i-arr[j]'
                if (i >= arr[j])
                    count[i] += count[i - arr[j]];

        // required number of ways
        return count[N];

    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 7;
        System.out.println("Total number of ways = "
                                    + countWays(N));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to count
# ways to sum up to a given value N

# Function to count the total
# number of ways to sum up to 'N'
def countWays(arr, m, N):

    count = [0 for i in range(N + 1)]

    # base case
    count[0] = 1

    # Count ways for all values up
    # to 'N' and store the result
    for i in range(1, N + 1):
        for j in range(m):

            # if i >= arr[j] then
            # accumulate count for value 'i' as
            # ways to form value 'i-arr[j]'
            if (i >= arr[j]):
                count[i] += count[i - arr[j]]

    # required number of ways
    return count[N]

# Driver Code
arr = [1, 5, 6]
m = len(arr)
N = 7
print("Total number of ways = ",
           countWays(arr, m, N))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# implementation to count ways 
// to sum up to a given value N
using System;

class Gfg
{
    static int []arr = {1, 5, 6};

    // method to count the total number
    // of ways to sum up to 'N'
    static int countWays(int N)
    {
        int []count = new int[N+1];

        // base case
        count[0] = 1;

        // count ways for all values up
        // to 'N' and store the result
        for (int i = 1; i <= N; i++)
            for (int j = 0; j < arr.Length; j++)

                // if i >= arr[j] then
                // accumulate count for value 'i' as
                // ways to form value 'i-arr[j]'
                if (i >= arr[j])
                    count[i] += count[i - arr[j]];

        // required number of ways
        return count[N];

    }

    // Driver code
    public static void Main()
    {
        int N = 7;
        Console.Write("Total number of ways = "
                                    + countWays(N));
    }
}

//This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count ways
// to sum up to a given value N

// function to count the total
// number of ways to sum up to 'N'
function countWays($arr, $m, $N)
{
    $count = array_fill(0,$N + 1,0);

    // base case
    $count[0] = 1;

    // count ways for all values up
    // to 'N' and store the result
    for ($i = 1; $i <= $N; $i++)
        for ($j = 0; $j < $m; $j++)

            // if i >= arr[j] then
            // accumulate count for value 'i' as
            // ways to form value 'i-arr[j]'
            if ($i >= $arr[$j])
                $count[$i] += $count[$i - $arr[$j]];

    // required number of ways
    return $count[$N];

}

// Driver code
$arr = array(1, 5, 6);
$m =  count($arr);
$N = 7;
echo "Total number of ways = ",countWays($arr, $m, $N);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation to count ways 
    // to sum up to a given value N

    let arr = [1, 5, 6];

    // method to count the total number
    // of ways to sum up to 'N'
    function countWays(N)
    {
        let count = new Array(N+1);
        count.fill(0);

        // base case
        count[0] = 1;

        // count ways for all values up
        // to 'N' and store the result
        for (let i = 1; i <= N; i++)
            for (let j = 0; j < arr.length; j++)

                // if i >= arr[j] then
                // accumulate count for value 'i' as
                // ways to form value 'i-arr[j]'
                if (i >= arr[j])
                    count[i] += count[i - arr[j]];

        // required number of ways
        return count[N];

    }

    let N = 7;
      document.write("Total number of ways = " + countWays(N));

</script>
```

**输出:**

```
Total number of ways = 6
```

**时间复杂度:** O(N*m)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
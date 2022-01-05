# 生成 1 到 N 的排列，使得连续数的绝对差给出 K 个不同的整数

> 原文:[https://www . geeksforgeeks . org/generate-置换-1 到 n-这样-连续数的绝对差-给-k-distinct-整数/](https://www.geeksforgeeks.org/generate-permutation-of-1-to-n-such-that-absolute-difference-of-consecutive-numbers-give-k-distinct-integers/)

给定两个整数 **N** 和 **K** ，其中 **K < N** ，任务是生成从 **1** 到 **N** 的整数排列，使得所有连续整数的绝对差恰好给出 **K** 个不同的整数。

**示例:**

> **输入:** N = 3，K = 2
> **输出:**1 3 2
> | 1–3 | = 2 和| 3–2 | = 1，给出 2 个不同的整数(2 和 1)
> 
> **输入:** N = 5，K = 4
> **输出:**1 5 2 4 3
> | 1–5 | = 4，| 5–2 | = 3，| 2–4 | = 2 和| 4–3 | = 1 给出 4 个不同的整数，即 4、3、2 和 1

**做法:**简单观察就能轻松解决问题。奇数索引处放置递增序列 **1、2、3、…** ，偶数索引处放置递减序列 **N、N-1、N-2、…** 等等。
对于 **N = 10** ，连续绝对差的不同整数排列可以是 **1 10 2 9 3 8 4 7 5 6** 。连续的绝对差给出整数 **9，8，7 等等**。
所以，首先打印这样一个序列的 **K** 个整数，然后使其余的差等于 **1** 。这段代码很容易理解。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate a permutation of integers
// from 1 to N such that the absolute difference of
// all the two consecutive integers give K distinct integers
void printPermutation(int N, int K)
{
    // To store the permutation
    vector<int> res;

    int l = 1, r = N, flag = 0;

    for (int i = 0; i < K; i++) {

        if (!flag) {

            // For sequence 1 2 3...
            res.push_back(l);
            l++;
        }
        else {

            // For sequence N, N-1, N-2...
            res.push_back(r);
            r--;
        }

        // Flag is used to alternate between
        // the above if else statements
        flag ^= 1;
    }

    // Taking integers with difference 1

    // If last element added was r + 1
    if (!flag) {
        for (int i = r; i >= l; i--)
            res.push_back(i);
    }

    // If last element added was l - 1
    else {
        for (int i = l; i <= r; i++)
            res.push_back(i);
    }

    // Print the permutation
    for (auto i : res)
        cout << i << " ";
}

// Driver code
int main()
{
    int N = 10, K = 4;

    printPermutation(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Vector;

class GFG
{
    // Function to generate a permutation
    // of integers from 1 to N such that the
    // absolute difference of all the two
    // consecutive integers give K distinct integers
    static void printPermutation(int N, int K)
    {
        // To store the permutation
        Vector<Integer> res = new Vector<>();

        int l = 1, r = N, flag = 0;

        for (int i = 0; i < K; i++)
        {
            if (flag == 0)
            {
                // For sequence 1 2 3...
                res.add(l);
                l++;
            }
            else
            {
                // For sequence N, N-1, N-2...
                res.add(r);
                r--;
            }

            // Flag is used to alternate between
            // the above if else statements
            flag ^= 1;
        }

        // Taking integers with difference 1
        // If last element added was r + 1
        if (flag != 1)
        {
            for (int i = r; i >= l; i--)
            {
                res.add(i);
            }
        }
        // If last element added was l - 1
        else
        {
            for (int i = l; i <= r; i++)
            {
                res.add(i);
            }
        }

        // Print the permutation
        for (Integer i : res)
        {
            System.out.print(i + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 10, K = 4;
        printPermutation(N, K);

    }
}

// This code is contributed by
// 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to generate a permutation
# of integers from 1 to N such that the
# absolute difference of all the two
# consecutive integers give K distinct
# integers
def printPermutation(N, K):

    # To store the permutation
    res = list();

    l, r, flag = 1, N, 0

    for i in range(K):

        if flag == False:

            # For sequence 1 2 3...
            res.append(l)
            l += 1

        else:

            # For sequence N, N-1, N-2...
            res.append(r);
            r -= 1;

    # Flag is used to alternate between
    # the above if else statements
        flag = flag ^ 1;

    # Taking integers with difference 1

    # If last element added was r + 1
    if flag == False:
        for i in range(r, 2, -1):
            res.append(i)

    # If last element added was l - 1
    else:
        for i in range(l, r):
            res.append(i)

    # Print the permutation
    for i in res:
        print(i, end = " ")

# Driver code
N, K = 10, 4
printPermutation(N, K)

# This code is contributed by
# Mohit Kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;

class GFG
{
    // Function to generate a permutation
    // of integers from 1 to N such that the
    // absolute difference of all the two
    // consecutive integers give K distinct integers
    static void printPermutation(int N, int K)
    {

        // To store the permutation
        ArrayList res = new ArrayList();

        int l = 1, r = N, flag = 0;
        for (int i = 0; i < K; i++)
        {
            if (flag == 0)
            {
                // For sequence 1 2 3...
                res.Add(l);
                l++;
            }
            else
            {
                // For sequence N, N-1, N-2...
                res.Add(r);
                r--;
            }

            // Flag is used to alternate between
            // the above if else statements
            flag ^= 1;
        }

        // Taking integers with difference 1
        // If last element added was r + 1
        if (flag != 1)
        {
            for (int i = r; i >= l; i--)
            {
                res.Add(i);
            }
        }

        // If last element added was l - 1
        else
        {
            for (int i = l; i <= r; i++)
            {
                res.Add(i);
            }
        }

        // Print the permutation
        foreach (int i in res)
        {
            Console.Write(i + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int N = 10, K = 4;
        printPermutation(N, K);       
    }
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to generate a permutation
// of integers from 1 to N such that the
// absolute difference of all the two
// consecutive integers give K distinct
// integers
function printPermutation($N, $K)
{

    // To store the permutation
    $res = array();

    $l = 1;
    $r = $N;
    $flag = 0;

    for ($i = 0; $i < $K; $i++)
    {
        if (!$flag)
        {

            // For sequence 1 2 3...
            array_push($res, $l);
            $l++;
        }
        else
        {

            // For sequence N, N-1, N-2...
            array_push($res, $r);
            $r--;
        }

        // Flag is used to alternate between
        // the above if else statements
        $flag ^= 1;
    }

    // Taking integers with difference 1

    // If last element added was r + 1
    if (!$flag)
    {
        for ($i = $r; $i >= $l; $i--)
            array_push($res, $i);
    }

    // If last element added was l - 1
    else
    {
        for ($i = l; $i <= $r; $i++)
            array_push($res, $i);
    }

    // Print the permutation
    for($i = 0; $i < sizeof($res); $i++)
        echo $res[$i], " ";
}

// Driver code
$N = 10;
$K = 4;

printPermutation($N, $K);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to generate a permutation of
// integers from 1 to N such that the
// absolute difference of all the two
// consecutive integers give K distinct integers
function printPermutation(N, K)
{

    // To store the permutation
    var res = [];
    var l = 1, r = N, flag = 0;

    for(var i = 0; i < K; i++)
    {
        if (!flag)
        {

            // For sequence 1 2 3...
            res.push(l);
            l++;
        }
        else
        {

            // For sequence N, N-1, N-2...
            res.push(r);
            r--;
        }

        // Flag is used to alternate between
        // the above if else statements
        flag ^= 1;
    }

    // Taking integers with difference 1

    // If last element added was r + 1
    if (!flag)
    {
        for(var i = r; i >= l; i--)
            res.push(i);
    }

    // If last element added was l - 1
    else
    {
        for(var i = l; i <= r; i++)
            res.push(i);
    }

    // Print the permutation
    for(var i = 0; i< res.length; i++)
    {
        document.write(res[i] + " ");
    }
}

// Driver code
var N = 10, K = 4;

printPermutation(N, K);

// This code is contributed by noob2000

</script>
```

**Output:** 

```
1 10 2 9 8 7 6 5 4 3
```
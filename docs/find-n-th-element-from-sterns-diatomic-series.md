# 从斯特恩双原子系列

中找到第 n 个元素

> 原文:[https://www . geesforgeks . org/find-n-th-element-from-sterns-硅藻-series/](https://www.geeksforgeeks.org/find-n-th-element-from-sterns-diatomic-series/)

给定一个整数 n，我们必须找到斯特恩双原子级数的第 n 项。
**斯特恩双原子序列**是生成以下整数序列 0，1，1，2，1，3，2，3，1，4，3，5，2，5，3，4，…的序列。它产生于[卡尔金-威尔夫树](https://www.google.co.in/search?q=Calkin-Wilf+tree&oq=Calkin-Wilf+tree&aqs=chrome..69i57&sourceid=chrome&ie=UTF-8)。有时也称为 **fusc** 功能。
在数学术语中，斯特恩双原子级数的序列 P(n)由递推关系定义。
![\\ p(n) = p(n/2) \hspace{5.5cm} for \ n \ is \ even\\ p(n) = p((n-1)/2)+p(n+1)/2) \hspace{2cm} for \ n \ is \ odd \\ \\ where \ p(0) = 0 \ and \ p(1) = 1 \\ \\ Stern's \ Diatomic \ Series \ 0, 1, 1, 2, 1, 3, 2, 3, 1, 4, ......  ](img/55c0d4d4b478fb872ba2b4b5886b1516.png "Rendered by QuickLaTeX.com")
**例:**

```
Input : n = 7
Output : 3

Input : n = 15
Output : 4
```

**方法:**
我们用一个非常简单的动态规划概念来解决这个问题，这个概念用于寻找[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。在保存了 DP[0] = 0、DP[1] = 1 的基本情况后，我们必须简单地从 i = 2 遍历到 n，并根据斯特恩双原子级数的解释定义计算 DP[1]。最后返回 DP[n]的值。
**算法:**

```
 // SET the Base case
    DP[0] = 0;
    DP[1] = 1;

    // Traversing the array from 2nd Element to nth Element
    for (int i=2; i<=n; i++)
    {
        // Case 1: for even n
        if (i%2 == 0)
            DP[i] = DP[i/2];

        // Case 2: for odd n
        else
            DP[i] = DP[(i-1)/2] + DP[(i+1)/2];
    }
    return DP[n];
```

## C++

```
// Program to find the nth element
// of Stern's Diatomic Series
#include <bits/stdc++.h>
using namespace std;

// function to find nth stern'
// diatomic series
int findSDSFunc(int n)
{
    // Initializing the DP array
    int DP[n+1];

    // SET the Base case
    DP[0] = 0;
    DP[1] = 1;

    // Traversing the array from
    // 2nd Element to nth Element
    for (int i = 2; i <= n; i++) {

        // Case 1: for even n
        if (i % 2 == 0)
            DP[i] = DP[i / 2];

        // Case 2: for odd n
        else
            DP[i] = DP[(i - 1) / 2] +
                        DP[(i + 1) / 2];
    }
    return DP[n];
}

// Driver program
int main()
{
    int n = 15;   
    cout << findSDSFunc(n) << endl;   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the nth element
// of Stern's Diatomic Series

class GFG {

    // function to find nth stern'
    // diatomic series
    static int findSDSFunc(int n)
    {

        // Initializing the DP array
        int DP[] = new int[n+1];

        // SET the Base case
        DP[0] = 0;
        DP[1] = 1;

        // Traversing the array from
        // 2nd Element to nth Element
        for (int i = 2; i <= n; i++)
        {

            // Case 1: for even n
            if (i % 2 == 0)
                DP[i] = DP[i / 2];

            // Case 2: for odd n
            else
                DP[i] = DP[(i - 1) / 2] +
                            DP[(i + 1) / 2];
        }

        return DP[n];
    }

    // Driver program
    public static void main(String[] args)
    {
        int n = 15;

        System.out.println(findSDSFunc(n));
    }
}

// This code is contributed by Smita Semwal.
```

## 蟒蛇 3

```
# Program to find the nth element
# of Stern's Diatomic Series

# function to find nth stern'
# diatomic series
def findSDSFunc(n):

    # Initializing the DP array
    DP = [0] * (n+1)

    # SET the Base case
    DP[0] = 0
    DP[1] = 1

    # Traversing the array from
    # 2nd Element to nth Element
    for i in range(2, n+1):

        # Case 1: for even n
        if (int(i % 2) == 0):
            DP[i] = DP[int(i / 2)]

        # Case 2: for odd n
        else:
            DP[i] = (DP[int((i - 1) / 2)]
                  + DP[int((i + 1) / 2)])

    return DP[n]

# Driver program
n = 15

print(findSDSFunc(n))

# This code is contribute by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find the nth element
// of Stern's Diatomic Series
using System;

class GFG
{
    // function to find nth
    // stern' diatomic series
    static int findSDSFunc(int n)
    {

        // Initializing the DP array
        int []DP = new int[n + 1];

        // SET the Base case
        DP[0] = 0;
        DP[1] = 1;

        // Traversing the array from
        // 2nd Element to nth Element
        for (int i = 2; i <= n; i++)
        {

            // Case 1: for even n
            if (i % 2 == 0)
                DP[i] = DP[i / 2];

            // Case 2: for odd n
            else
                DP[i] = DP[(i - 1) / 2] +
                        DP[(i + 1) / 2];
        }

        return DP[n];
    }

    // Driver Code
    static public void Main ()
    {
        int n = 15;
        Console.WriteLine(findSDSFunc(n));
    }
}

// This code is contributed by aj_36
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the nth element
// of Stern's Diatomic Series

// function to find nth stern'
// diatomic series
function findSDSFunc($n)
{

    // SET the Base case
    $DP[0] = 0;
    $DP[1] = 1;

    // Traversing the array from
    // 2nd Element to nth Element
    for ($i = 2; $i <= $n; $i++)
    {

        // Case 1: for even n
        if ($i % 2 == 0)
            $DP[$i] = $DP[$i / 2];

        // Case 2: for odd n
        else
            $DP[$i] = $DP[($i - 1) / 2] +
                      $DP[($i + 1) / 2];
    }
    return $DP[$n];
}

// Driver Code
$n = 15;
echo(findSDSFunc($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the nth element
// of Stern's Diatomic Series

    // function to find nth stern'
    // diatomic series
    function findSDSFunc(n)
    {

        // Initializing the DP array
        let DP = [];

        // SET the Base case
        DP[0] = 0;
        DP[1] = 1;

        // Traversing the array from
        // 2nd Element to nth Element
        for (let i = 2; i <= n; i++)
        {

            // Case 1: for even n
            if (i % 2 == 0)
                DP[i] = DP[i / 2];

            // Case 2: for odd n
            else
                DP[i] = DP[(i - 1) / 2] +
                            DP[(i + 1) / 2];
        }
        return DP[n];
    }

// Driver code
        let n = 15;     
        document.write(findSDSFunc(n));

          // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
4
```
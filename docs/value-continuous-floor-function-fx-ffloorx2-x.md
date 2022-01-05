# 连续楼层函数的值:F(x) = F(楼层(x/2)) + x

> 原文:[https://www . geesforgeks . org/value-continuous-floor-function-FX-ffloor x2-x/](https://www.geeksforgeeks.org/value-continuous-floor-function-fx-ffloorx2-x/)

给定一个正整数数组。对于数组的每个元素 x，我们需要求定义为 **F(x) = F(floor(x/2)) + x** 的连续 floor 函数值，其中 F(0) = 0。
**例:-**

```
Input : arr[] = {6, 8}
Output : 10 15

Explanation : F(6) = 6 + F(3)
                   = 6 + 3 + F(1)
                   = 6 + 3 + 1 + F(0)
                   = 10
Similarly F(8) = 15
```

**基本方法:**对于给定的 x 值，我们可以使用简单的递归函数计算 F(x)如下:

```
int func(int x)
{
    if (x == 0) 
        return 0;
    return (x + func(floor(x/2)));
}
```

在这种方法中，如果我们有 n 个查询，那么每个查询元素需要 O(x)
一个有效的方法是使用 [**记忆**](https://www.geeksforgeeks.org/dynamic-programming-set-1/) 我们构造一个数组，它保存每个可能的 x 值的 F(x)值。否则我们就返回值。

## C++

```
// C++ program for finding value
// of continuous floor function
#include <bits/stdc++.h>

#define max 10000
using namespace std;

int dp[max];

void initDP()
    {
         for (int i = 0; i < max; i++)
             dp[i] = -1;
    }

// function to return value of F(n)
int func(int x)
    {
        if (x == 0)
            return 0;
        if (dp[x] == -1)
            dp[x] = x + func(x / 2);

        return dp[x];
    }

void printFloor(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            cout << func(arr[i]) << " ";
    }

// Driver code
int main()
    {
        // call the initDP() to fill DP array
        initDP();

        int arr[] = { 8, 6 };
        int n = sizeof(arr) / sizeof(arr[0]);

        printFloor(arr, n);

        return 0;
    }
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding value
// of continuous floor function
class GFG
{
    static final int max = 10000;
    static int dp[] = new int[max];

    static void initDP()
    {
        for (int i = 0; i < max; i++)
            dp[i] = -1;
    }

    // function to return value of F(n)
    static int func(int x)
    {
        if (x == 0)
            return 0;
        if (dp[x] == -1)
            dp[x] = x + func(x / 2);

        return dp[x];
    }

    static void printFloor(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(func(arr[i]) + " ");
    }

    // Driver code
    public static void main(String[] args)
    {

        // call the initDP() to fill DP array
        initDP();

        int arr[] = {8, 6};
        int n = arr.length;

        printFloor(arr, n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program for finding value
# of continuous floor function

max = 10000

dp = [0] * max

# function to initialize the DP array
def initDP() :

        for i in range(max) :
                dp[i] = -1

# function to return value of F(n)
def func(x) :

    if (x == 0) :
        return 0

    if (dp[x] == -1) :
        dp[x] = x + func(x // 2)

    return dp[x]

def printFloor(arr, n) :

    for i in range(n) :

        print(func(arr[i]), end = " ")

# Driver Code
if __name__ == "__main__" :

        # call the initDP() to
        # fill DP array        
        initDP()

        arr = [8, 6]
        n = len(arr)

        printFloor(arr, n)

# This code is contributed by Ryuga
```

## C#

```
// C# program for finding value
// of continuous floor function
using System;

class GFG
{
    static int max = 10000;
    static int []dp = new int[max];

    static void initDP()
    {
        for (int i = 0; i < max; i++)
            dp[i] = -1;
    }

    // function to return value of F(n)
    static int func(int x)
    {
        if (x == 0)
            return 0;
        if (dp[x] == -1)
            dp[x] = x + func(x / 2);

        return dp[x];
    }

    static void printFloor(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(func(arr[i]) + " ");
    }

    // Driver code
    public static void Main()
    {

        // call the initDP() to fill DP array
        initDP();

        int []arr = {8, 6};
        int n = arr.Length;

        printFloor(arr, n);
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding value
// of continuous floor function
$max = 10000;

$dp = array_fill(0, $max, NULL);

function initDP()
{
    global $max,$dp;
    for ($i = 0; $i < $max; $i++)
        $dp[$i] = -1;
}

// function to return value of F(n)
function func($x)
{
    global $dp;
    if ($x == 0)
        return 0;
    if ($dp[$x] == -1)
        $dp[$x] = $x + func(intval($x / 2));

    return $dp[$x];
}

function printFloor(&$arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo func($arr[$i]) . " ";
}

// Driver code

// call the initDP() to fill DP array
initDP();

$arr = array(8, 6);
$n = sizeof($arr);

printFloor($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program for finding value
// of continuous floor function
    let max = 10000;
    let dp = Array.from({length: max}, (_, i) => 0);

    function initDP()
    {
        for (let i = 0; i < max; i++)
            dp[i] = -1;
    }

    // function to return value of F(n)
    function func(x)
    {
        if (x == 0)
            return 0;
        if (dp[x] == -1)
            dp[x] = x + func(Math.floor(x / 2));

        return dp[x];
    }

    function prletFloor(arr, n)
    {
        for (let i = 0; i < n; i++)
            document.write(func(arr[i]) + " ");
    }

// driver function

        // call the initDP() to fill DP array
        initDP();

        let arr = [8, 6];
        let n = arr.length;

        prletFloor(arr, n);

   // This code is contributed by code_hunt.
</script>   
```

**输出:**

```
15 10
```

本文由[**Shivam Pradhan(anuj _ charm)**](http://www.facebook.com/ma5ter6it)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
# 将 X 和 Y 放置在 n 个位置的方法总数，这样就不会有两个 X 在一起

> 原文:[https://www . geesforgeks . org/total-number-to-place-x-and-y-at-n-places-so-no-two-x-total-number-to-place-x-to-place-x-to-n-place-n-to-two-x-to-two-x-total-to-to-place-to-to-](https://www.geeksforgeeks.org/total-number-of-ways-to-place-x-and-y-at-n-places-such-that-no-two-x-are-together/)

给定 N 个位置，任务是计算放置 X 和 Y 的方法总数，使得没有两个 X 在一起。
**例:**

```
Input: 3
Output: 5
XYX, YYX, YXY, XYY and YYY 

Input: 4
Output: 8
XYXY, XYYX, YXYX, YYYX, YYXY, YXYY, XYYY and YYYY
```

**方法:**
对于 N = 1，X 和 Y 是两种可能的方式。
对于 N = 2，XY、YX 和 YY 是 3 种可能的方式。
对于 N = 3，XYX、YYX、YXY、XYY 和 YYY 是 5 种可能的方式。
对于 N = 4，XYXY、XYYX、YYX、YYYX、YYXY、YYYY、XYYY、YYYY 是 8 种可能的方式。
在求解 N 值时，观察到一个[斐波那契](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)模式序列。
以下是上述方法的迭代实现:

## C++

```
// C++ program to find the
// number of ways Calculate
// total ways to place 'x'
// and 'y' at n places such
// that no two 'x' are together
#include <iostream>
using namespace std;

    // Function to return
    // number of ways
    int ways(int n)
    {
        // for n=1
        int first = 2;

        // for n=2
        int second = 3;
        int res = 0;

        // iterate to find
        // Fibonacci term
        for (int i = 3; i <= n; i++)
        {
            res = first + second;
            first = second;
            second = res;
        }

        return res;
    }

// Driver Code
int main()
{
    // total number of places
    int n = 7;
    cout << "Total ways are : ";
    cout << ways(n);

    return 0;
}

// This code is contributed
// by jit_t
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of ways
// Calculate total ways to place 'x' and 'y'
// at n places such that no two 'x' are together
public class GFG {

    // Function to return number of ways
    static int ways(int n)
    {
        // for n=1
        int first = 2;

        // for n=2
        int second = 3;
        int res = 0;

        // iterate to find Fibonacci term
        for (int i = 3; i <= n; i++) {
            res = first + second;
            first = second;
            second = res;
        }

        return res;
    }
    public static void main(String[] args)
    {

        // total number of places
        int n = 7;

        System.out.print("Total ways are: " + ways(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the
# number of ways Calculate
# total ways to place 'x'
# and 'y' at n places such
# that no two 'x' are together

# Function to return
# number of ways
def ways(n):

    # for n=1
    first = 2;

    # for n=2
    second = 3;
    res = 0;

    # iterate to find
    # Fibonacci term
    for i in range(3, n + 1):
        res = first + second;
        first = second;
        second = res;

    return res;

# Driver Code

# total number of places
n = 7;
print("Total ways are: " ,
                 ways(n));

# This code is contributed by mits
```

## C#

```
// C# program to find the
// number of ways. Calculate
// total ways to place 'x'
// and 'y' at n places such
// that no two 'x' are together
using System;

class GFG
{

    // Function to return
    // number of ways
    static int ways(int n)
    {
        // for n=1
        int first = 2;

        // for n=2
        int second = 3;
        int res = 0;

        // iterate to find
        // Fibonacci term
        for (int i = 3; i <= n; i++)
        {
            res = first + second;
            first = second;
            second = res;
        }

        return res;
    }

    // Driver Code
    static public void Main ()
    {

        // total number
        // of places
        int n = 7;

        Console.WriteLine("Total ways are: " +
                                     ways(n));
    }
}

//This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// number of ways Calculate
// total ways to place 'x'
// and 'y' at n places such
// that no two 'x' are together

// Function to return
// number of ways
function ways($n)
{
    // for n=1
    $first = 2;

    // for n=2
    $second = 3;
    $res = 0;

    // iterate to find
    // Fibonacci term
    for ($i = 3; $i <= $n; $i++)
    {
        $res = $first + $second;
        $first = $second;
        $second = $res;
    }

    return $res;
}
// Driver Code

// total number of places
$n = 7;
echo "Total ways are: " , ways($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript program to find the number of ways
// Calculate total ways to place 'x' and 'y'
// at n places such that no two 'x' are together

    // Function to return number of ways
    function ways(n)
    {

        // for n = 1
        var first = 2;

        // for n = 2
        var second = 3;
        var res = 0;

        // iterate to find Fibonacci term
        for (i = 3; i <= n; i++)
        {
            res = first + second;
            first = second;
            second = res;
        }
        return res;
    }

        // total number of places
        var n = 7;
        document.write("Total ways are: " + ways(n));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
Total ways are: 34
```

**时间复杂度:** O(N)
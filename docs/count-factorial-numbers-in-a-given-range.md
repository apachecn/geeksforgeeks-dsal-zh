# 计算给定范围内的阶乘数

> 原文:[https://www . geeksforgeeks . org/count-factorial-numbers-in-a-给定范围/](https://www.geeksforgeeks.org/count-factorial-numbers-in-a-given-range/)

如果存在大于等于 0 的整数，那么 F 就是阶乘数。(即 F 是 I 的阶乘)。阶乘数的例子有 1，2，6，24，120，…
编写一个程序，将两个长整数“低”和“高”作为输入，其中 0 <低<高，并在封闭区间[低，高]内计算阶乘数。
**举例:**

```
Input: 0 1 
Output: 1 //Reason: Only factorial number is 1 

Input: 12 122 
Output: 2 // Reason: factorial numbers are 24, 120 

Input: 2 720 
Output: 5 // Factorial numbers are: 2, 6, 24, 120, 720 
```

1)找出大于或等于**低**的第一个阶乘。让这个阶乘为 x！(x 的阶乘)并且这个阶乘的值是“事实”
2)保持递增 x，并且当事实小于或等于**高**时保持更新“事实”。计算循环运行的次数。
3)返回步骤 2 中计算的计数。
以下是上述算法的实现。感谢 Kartik 提出以下解决方案。

## C++

```
// Program to count factorial numbers in given range
#include <iostream>
using namespace std;

int countFact(int low, int high)
{
    // Find the first factorial number 'fact' greater than or
    // equal to 'low'
    int fact = 1, x = 1;
    while (fact < low)
    {
        fact = fact*x;
        x++;
    }

    // Count factorial numbers in range [low, high]
    int res = 0;
    while (fact <= high)
    {
        res++;
        fact = fact*x;
        x++;
    }

    // Return the count
    return res;
}

// Driver program to test above function
int main()
{
    cout << "Count is " << countFact(2, 720);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count factorial
// numbers in given range

class GFG
{
    static int countFact(int low, int high)
    {
        // Find the first factorial number
        // 'fact' greater than or equal to 'low'
        int fact = 1, x = 1;
        while (fact < low)
        {
            fact = fact * x;
            x++;
        }

        // Count factorial numbers
        // in range [low, high]
        int res = 0;
        while (fact <= high)
        {
            res++;
            fact = fact * x;
            x++;
        }

        // Return the count
        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        System.out.print("Count is "
                         + countFact(2, 720));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Program to count factorial
# numbers in given range

def countFact(low,high):

    # Find the first factorial number
    # 'fact' greater than or
    # equal to 'low'
    fact = 1
    x = 1
    while (fact < low):

        fact = fact * x
        x += 1

    # Count factorial numbers
    # in range [low, high]
    res = 0
    while (fact <= high):

        res += 1
        fact = fact * x
        x += 1

    # Return the count
    return res

# Driver code

print("Count is ", countFact(2, 720))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# Program to count factorial
// numbers in given range
using System;

public class GFG
{

    // Function to count factorial
    static int countFact(int low, int high)
    {

        // Find the first factorial number numbers
        // 'fact' greater than or equal to 'low'
        int fact = 1, x = 1;
        while (fact < low)
        {
            fact = fact * x;
            x++;
        }

        // Count factorial numbers
        // in range [low, high]
        int res = 0;
        while (fact <= high)
        {
            res++;
            fact = fact * x;
            x++;
        }

        // Return the count
        return res;
    }

    // Driver code
    public static void Main ()
    {
        Console.Write("Count is " + countFact(2, 720));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to count factorial
// numbers in given range
function countFact($low, $high)
{
    // Find the first factorial
    // number 'fact' greater
    // than or equal to 'low'
    $fact = 1; $x = 1;
    while ($fact < $low)
    {
        $fact = $fact * $x;
        $x++;
    }

    // Count factorial numbers
    // in range [low, high]
    $res = 0;
    while ($fact <= $high)
    {
        $res++;
        $fact = $fact * $x;
        $x++;
    }

    // Return the count
    return $res;
}

// Driver Code
echo "Count is " , countFact(2, 720);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript Program to count factorial
// numbers in given range
function countFact(low, high)
{

    // Find the first factorial
    // number 'fact' greater
    // than or equal to 'low'
    let fact = 1;
    let x = 1;
    while (fact < low)
    {
        fact = fact * x;
        x++;
    }

    // Count factorial numbers
    // in range [low, high]
    let res = 0;
    while (fact <= high)
    {
        res++;
        fact = fact * x;
        x++;
    }

    // Return the count
    return res;
}

// Driver Code
document.write("Count is " + countFact(2, 720));

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
Count is 5
```

本文由 Shivam 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
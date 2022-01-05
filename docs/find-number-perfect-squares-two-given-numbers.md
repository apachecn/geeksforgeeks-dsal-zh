# 两个给定数字之间的完美平方数

> 原文:[https://www . geesforgeks . org/find-number-perfect-squares-two-given-numbers/](https://www.geeksforgeeks.org/find-number-perfect-squares-two-given-numbers/)

给定两个给定的数字 a 和 b，其中 1 <=a<=b, find the number of perfect squares between a and b (a and b inclusive).
示例

```
Input :  a = 3, b = 8
Output : 1
The only perfect in given range is 4.

Input : a = 9, b = 25
Output : 3
The three squares in given range are 9, 
16 and 25
```

**方法 1** :一个比较天真的做法是检查 a 和 b(包括 a 和 b)之间的所有数字，每当我们遇到一个完美的正方形时，就增加一个计数。

以下是上述思路的实现:

## C++

```
// A Simple Method to count squares between a and b
#include <bits/stdc++.h>
using namespace std;

int countSquares(int a, int b)
{
    int cnt = 0; // Initialize result

    // Traverse through all numbers
    for (int i = a; i <= b; i++)

        // Check if current number 'i' is perfect
        // square
        for (int j = 1; j * j <= i; j++)
            if (j * j == i)
                cnt++;

    return cnt;
}

// Driver code
int main()
{
    int a = 9, b = 25;
    cout << "Count of squares is "
         << countSquares(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count squares between a and b
class CountSquares {

    static int countSquares(int a, int b)
    {
        int cnt = 0; // Initialize result

        // Traverse through all numbers
        for (int i = a; i <= b; i++)

            // Check if current number 'i' is perfect
            // square
            for (int j = 1; j * j <= i; j++)
                if (j * j == i)
                    cnt++;
        return cnt;
    }
}

// Driver Code
public class PerfectSquares {
    public static void main(String[] args)
    {
        int a = 9, b = 25;
        CountSquares obj = new CountSquares();
        System.out.print("Count of squares is " + obj.countSquares(a, b));
    }
}
```

## 计算机编程语言

```
# Python program to count squares between a and b

def CountSquares(a, b):

    cnt = 0 # initialize result

    # Traverse through all numbers
    for i in range (a, b + 1):
        j = 1;
        while j * j <= i:
            if j * j == i:
                 cnt = cnt + 1
            j = j + 1
        i = i + 1
    return cnt

# Driver Code
a = 9
b = 25
print "Count of squares is:", CountSquares(a, b)
```

## C#

```
// C# program to count squares
// between a and b
using System;

class GFG {

    // Function to count squares
    static int countSquares(int a, int b)
    {
        // Initialize result
        int cnt = 0;

        // Traverse through all numbers
        for (int i = a; i <= b; i++)

            // Check if current number
            // 'i' is perfect square
            for (int j = 1; j * j <= i; j++)
                if (j * j == i)
                    cnt++;
        return cnt;
    }

    // Driver Code
    public static void Main()
    {
        int a = 9, b = 25;
        Console.Write("Count of squares is " + countSquares(a, b));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Simple Method to count squares
//between a and b

function countSquares($a, $b)
{
    $cnt = 0; // Initialize result

    // Traverse through all numbers
    for ($i = $a; $i <= $b; $i++)

        // Check if current number
        // 'i' is perfect square
        for ($j = 1; $j * $j <= $i;
                              $j++)
            if ($j * $j == $i)
                $cnt++;

    return $cnt;
}

// Driver code

    $a = 9; $b = 25;
    echo "Count of squares is ".
              countSquares($a, $b);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// A Simple Method to count squares
//between a and b

function countSquares(a, b)
{
   let cnt = 0;

    // Traverse through all numbers
    for (let i = a; i <= b; i++)

        // Check if current number
        // 'i' is perfect square
        for (let j = 1; j * j <= i;j++)
            if (j * j == i)
                cnt++;

    return cnt;
}

// Driver code

    let a = 9;
    let b = 25;
    document.write( "Count of squares is ",
              countSquares(a, b));

// This code is contributed by sravan.
</script>
```

输出:

```
Count of squares is 3
```

这个解的时间复杂度的上界是 O((b-a) * sqrt(b))。
**方法 2(高效)**我们可以简单地取‘a’的平方根和‘b’的平方根，用
计算它们之间的完美平方

```
floor(sqrt(b)) - ceil(sqrt(a)) + 1

We take floor of sqrt(b) because we need to consider 
numbers before b.

We take ceil of sqrt(a) because we need to consider 
numbers after a.

For example, let b = 24, a = 8\.  floor(sqrt(b)) = 4, 
ceil(sqrt(a)) = 3\.  And number of squares is 4 - 3 + 1
= 2\. The two numbers are 9 and 16.
```

以下是上述思路的实现:

## C++

```
// An Efficient Method to count squares between a and b
#include <bits/stdc++.h>
using namespace std;

// An efficient solution to count square between a
// and b
int countSquares(int a, int b)
{
    return (floor(sqrt(b)) - ceil(sqrt(a)) + 1);
}

// Driver code
int main()
{
    int a = 9, b = 25;
    cout << "Count of squares is "
         << countSquares(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An Efficient method to count squares between
// a and b
class CountSquares {
    double countSquares(int a, int b)
    {
        return (Math.floor(Math.sqrt(b)) - Math.ceil(Math.sqrt(a)) + 1);
    }
}

// Driver Code
public class PerfectSquares {
    public static void main(String[] args)
    {
        int a = 9, b = 25;
        CountSquares obj = new CountSquares();
        System.out.print("Count of squares is " + (int)obj.countSquares(a, b));
    }
}
```

## 计算机编程语言

```
# An Efficient Method to count squares between a
# and b
import math
def CountSquares(a, b):
    return (math.floor(math.sqrt(b)) - math.ceil(math.sqrt(a)) + 1)

# Driver Code
a = 9
b = 25
print "Count of squares is:", int(CountSquares(a, b))
```

## C#

```
// C# program for efficient method
// to count squares between a & b
using System;

class GFG {

    // Function to count squares
    static double countSquares(int a, int b)
    {
        return (Math.Floor(Math.Sqrt(b)) - Math.Ceiling(Math.Sqrt(a)) + 1);
    }

    // Driver Code
    public static void Main()
    {
        int a = 9, b = 25;
        Console.Write("Count of squares is " + (int)countSquares(a, b));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An Efficient PHP code to count
// squares between a and b

// Method to count square
// between a and b
function countSquares($a, $b)
{
    return (floor(sqrt($b)) -
            ceil(sqrt($a)) + 1);
}

// Driver code
{
    $a = 9;
    $b = 25;
    echo "Count of squares is ",
           countSquares($a, $b);
    return 0;
}
// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// A Simple Method to count squares
//between a and b

function countSquares(a, b)
{
   return (Math.floor(Math.sqrt(b)) -  Math.ceil(Math.sqrt(a)) + 1);
}

// Driver code

    let a = 9;
    let b = 25;
    document.write( "Count of squares is ",
              countSquares(a, b));

// This code is contributed by sravan.
</script>
```

输出:

```
Count of squares is 3
```

该解决方案的时间复杂度为 0(对数 b)。数字 n 的平方根的典型实现需要的时间等于 O(Log n)[参见[本](https://www.geeksforgeeks.org/square-root-of-an-integer/)了解平方根的示例实现]

本文由**拉胡尔·阿加尔瓦尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论
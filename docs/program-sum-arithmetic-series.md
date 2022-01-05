# 算术级数求和程序

> 原文:[https://www . geesforgeks . org/program-sum-算术-series/](https://www.geeksforgeeks.org/program-sum-arithmetic-series/)

有相同共性差异的数列称为**算术数列**。系列的第一个术语是 **a** ，共同的区别是 **d** 。系列是看起来像 **a，a + d，a + 2d，a + 3d，。。。**任务是求数列的和。
示例:

```
Input : a = 1
        d = 2
        n = 4
Output : 16
1 + 3 + 5 + 7 = 16

Input : a = 2.5
        d = 1.5
        n = 20
Output : 335
```

一个**求算术级数和的简单解法**。

## C++

```
// CPP Program to find the sum of arithmetic
// series.
#include<bits/stdc++.h>
using namespace std;

// Function to find sum of series.
float sumOfAP(float a, float d, int n)
{
    float sum = 0;
    for (int i=0;i<n;i++)
    {
        sum = sum + a;
        a = a + d;
    }
    return sum;
}

// Driver function
int main()
{
    int n = 20;
    float a = 2.5, d = 1.5;
    cout<<sumOfAP(a, d, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Program to find the sum of
// arithmetic series.

class GFG{

    // Function to find sum of series.
    static float sumOfAP(float a, float d,
                                  int n)
    {
        float sum = 0;
        for (int i = 0; i < n; i++)
        {
            sum = sum + a;
            a = a + d;
        }
        return sum;
    }

    // Driver function
    public static void main(String args[])
    {
        int n = 20;
        float a = 2.5f, d = 1.5f;
        System.out.println(sumOfAP(a, d, n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 计算机编程语言

```
# Python Program to find the sum of
# arithmetic series.

# Function to find sum of series.
def sumOfAP( a, d,n) :
    sum = 0
    i = 0
    while i < n :
        sum = sum + a
        a = a + d
        i = i + 1
    return sum

# Driver function
n = 20
a = 2.5
d = 1.5
print (sumOfAP(a, d, n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Program to find the sum of
// arithmetic series.
using System;

class GFG {

    // Function to find sum of series.
    static float sumOfAP(float a, float d,
                                    int n)
    {
        float sum = 0;
        for (int i = 0; i < n; i++)
        {
            sum = sum + a;
            a = a + d;
        }

        return sum;
    }

    // Driver function
    public static void Main()
    {
        int n = 20;
        float a = 2.5f, d = 1.5f;

        Console.Write(sumOfAP(a, d, n));
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the sum 
// of arithmetic series.

// Function to find sum of series.
function sumOfAP($a, $d, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $sum = $sum + $a;
        $a = $a + $d;
    }
    return $sum;
}

// Driver Code
$n = 20;
$a = 2.5; $d = 1.5;
echo(sumOfAP($a, $d, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript Program to find the sum of arithmetic
// series.

// Function to find sum of series.
function sumOfAP(a, d, n)
{
    let sum = 0;
    for (let i=0;i<n;i++)
    {
        sum = sum + a;
        a = a + d;
    }
    return sum;
}

// Driver function

    let n = 20;
    let a = 2.5, d = 1.5;
    document.write(sumOfAP(a, d, n));

// This code is contributed by Mayank Tyagi

</script>
```

输出:

```
335
```

时间复杂度:O(n)
求算术级数和的一个**有效解**是用下面的公式。

```
Sum of arithmetic series 
           = ((n / 2) * (2 * a + (n - 1) * d))
           Where
               a - First term
               d - Common difference
               n - No of terms
```

## C++

```
// Efficient solution to find sum of arithmetic series.
#include<bits/stdc++.h>
using namespace std;

float sumOfAP(float a, float d, float n)
{
    float sum = (n / 2) * (2 * a + (n - 1) * d);
    return sum;
}

// Driver code
int main()
{
    float n = 20;
    float a = 2.5, d = 1.5;
    cout<<sumOfAP(a, d, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Efficient solution to find
// sum of arithmetic series.
class GFG
{
    static float sumOfAP(float a, float d, float n)
    {
        float sum = (n / 2) * (2 * a + (n - 1) * d);
        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        float n = 20;
        float a = 2.5f, d = 1.5f;
        System.out.print(sumOfAP(a, d, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 Efficient
# solution to find sum
# of arithmetic series.

def  sumOfAP(a,  d,  n):
    sum = (n / 2) * (2 * a + (n - 1) * d)
    return sum

# Driver code   
n = 20
a = 2.5
d = 1.5

print(sumOfAP(a, d, n))

# This code is
# contributed by sunnysingh

```

## C#

```
// C# efficient solution to find
// sum of arithmetic series.
using System;

class GFG {

    static float sumOfAP(float a,
                         float d,
                         float n)
    {
        float sum = (n / 2) *
                    (2 * a +
                    (n - 1) * d);
        return sum;
    }

    // Driver code
    static public void Main ()
    {
        float n = 20;
        float a = 2.5f, d = 1.5f;
        Console.WriteLine(sumOfAP(a, d, n));
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP code to find sum
// of arithmetic series.

// Function to find sum of series.
function sumOfAP($a, $d, $n)
{
    $sum = ($n / 2) * (2 * $a +
                ($n - 1) * $d);
    return $sum;
}

// Driver code
$n = 20;
$a = 2.5; $d = 1.5;
echo(sumOfAP($a, $d, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
// Efficient solution to find sum of arithmetic series.

function sumOfAP(a, d, n) {
    let sum = (n / 2) * (2 * a + (n - 1) * d);
    return sum;
}

// Driver code
let n = 20;
let a = 2.5, d = 1.5;
document.write(sumOfAP(a, d, n));

// This code is contributed by Ashok
```

**Output**

```
335
```

时间复杂度:O(1)
**这个公式是如何工作的？**
我们可以用数学归纳法证明这个公式。我们可以很容易地看到，这个公式适用于 n = 1 和 n = 2。假设 n = k-1 是真的。

```
Let the formula be true for n = k-1.
Sum of first k - 1 elements of geometric series is
        = (((k-1))/ 2) * (2 * a + (k - 2) * d))
We know k-th term of arithmetic series is
        = a + (k - 1)*d

Sum of first k elements = 
      = Sum of (k-1) numbers + k-th element
      = (((k-1)/2)*(2*a + (k-2)*d)) + (a + (k-1)*d)
      = [((k-1)(2a + (k-2)d) + (2a + 2kd - 2d)]/2
      = ((k / 2) * (2 * a + (k - 1) * d))
```

本文由**达曼德拉·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
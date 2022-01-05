# x 和 y 的乘积之和，使得地板(n/x) = y

> 原文:[https://www.geeksforgeeks.org/sum-product-x-y-floornx-y/](https://www.geeksforgeeks.org/sum-product-x-y-floornx-y/)

给定正整数 **n** 。任务是求 **x** 和 **y** 的乘积之和，使得 **⌊n/x⌋ = y** (整数除法)。

**示例:**

```
Input : n = 5
Output : 21
Following are the possible pairs of (x, y):
(1, 5), (2, 2), (3, 1), (4, 1), (5, 1).
So, 1*5 + 2*2 + 3*1 + 4*1 + 5*1 
   = 5 + 4 + 3 + 4 + 5 
   = 21.

Input : n = 10
Output : 87
```

**方法 1(蛮力):**
从 1 到 n 迭代 x 找到 y，然后在每次迭代中给答案加上 x*y。

下面是该方法的实现:

## C++

```
// C++ program to find sum of product of x and y
// such that n/x = y (Integer Division)
#include<bits/stdc++.h>
using namespace std;

// Return the sum of product x*y.
int sumofproduct(int n)
{
    int ans = 0;

    // Iterating x from 1 to n
    for (int x = 1; x <= n; x++)
    {
        // Finding y = n/x.
        int y = n/x;

        // Adding product of x and y to answer.
        ans += (y * x);
    }

    return ans;
}

// Driven Program
int main()
{
    int n = 10;
    cout << sumofproduct(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// product of x and y such that
// n/x = y (Integer Division)
import java.io.*;

class GFG {

// Return the sum of product x*y.
static int sumofproduct(int n)
{
    int ans = 0;

    // Iterating x from 1 to n
    for (int x = 1; x <= n; x++)
    {
        // Finding y = n/x.
        int y = n / x;

        // Adding product of x and
        // y to answer.
        ans += (y * x);
    }

    return ans;
}

    // Driver Code
    static public void main(String[] args)
    {
        int n = 10;
        System.out.println(sumofproduct(n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find sum of
# product of x and y such that
# n/x = y (Integer Division)

# Return the sum of product x*y
def sumofproduct(n):
    ans = 0

    # Iterating x from 1 to n
    for x in range(1, n + 1):

        # Finding y = n/x.
        y = int(n / x)

        # Adding product of x and y to answer.
        ans += (y * x)

    return ans

# Driven Program
n = 10
print (sumofproduct(n))

#This code is Shreyanshi Arun
```

## C#

```
// C# program to find sum of
// product of x and y such that
// n/x = y (Integer Division)
using System;

class GFG {

// Return the sum of product x*y.
static int sumofproduct(int n)
{
    int ans = 0;

    // Iterating x from 1 to n
    for (int x = 1; x <= n; x++)
    {
        // Finding y = n/x.
        int y = n / x;

        // Adding product of x and
        // y to answer.
        ans += (y * x);
    }

    return ans;
}

    // Driver Code
    static public void Main(String[] args)
    {
        int n = 10;
        Console.WriteLine(sumofproduct(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of product
// of x and y such that n/x = y
// (Integer Division)

// Return the sum of product x*y.
function sumofproduct($n)
{
    $ans = 0;

    // Iterating x from 1 to n
    for($x = 1; $x <= $n; $x++)
    {
        // Finding y = n/x.
        $y = (int)($n / $x);

        // Adding product of x
        // and y to answer.
        $ans += ($y * $x);
    }

    return $ans;
}

// Driver Code
$n = 10;
echo sumofproduct($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of
// product of x and y such that
// n/x = y (Integer Division)

// Return the sum of product x*y.
function sumofproduct(n)
{
    var ans = 0;

    // Iterating x from 1 to n
    for(x = 1; x <= n; x++)
    {

        // Finding y = n/x.
        var y = parseInt(n / x);

        // Adding product of x and
        // y to answer.
        ans += (y * x);
    }
    return ans;
}

// Driver Code
var n = 10;
document.write(sumofproduct(n));

// This code is contributed by Princi Singh

</script>
```

**输出:**

```
87
```

**时间复杂度:** O(n)
**方法二(高效途径):**
我们求解 n = 10，那么
x = 1，y = 10
x = 2，y = 5
x = 3，y = 3
x = 4，y = 2
x = 5，y = 2
x = 6，y = 1
x = 7，y = 1
x = 8，y = 1 y = 1
x = 10，y = 1
那么，我们的答案应该是 1 * 10+2 * 5+3 * 3+4 * 2+5 * 2+6 * 1+7 * 1+8 * 1+9 * 1+10 * 1。
现在，观察 y 的一些值是否重复。此外，观察它们在 x 的某个连续值范围内重复，就像 y = 1 在 x = 6 到 10 之间重复一样。

因此，不要像方法 1 中那样为 x (1 到 n)的所有值寻找 y 的值，而是尝试寻找 x 的较低值和较高值，对于这些值，y 的可能值的值像 y = 1 一样，尝试寻找 x = 6 的较低值和 x = 10 的较高值。现在，观察较低值将是(n/(y+1)) + 1，较高值将是(n/y)。求 x 范围的和，与 y 相乘，相加得出答案。
如何求 y 的可能值？

注意，当 y 小于或等于 x 时，y 具有从 1 到 sqrt(n)的所有值。因此，对于 y = 1 到 sqrt(n)，为每个 y 找到 x 的下限和上限。对于 n = 10，
y = 1，lo = 6 和 hi = 10，ans += (6 + 7 + 8 + 9 + 10)*1
y = 2，lo = 4 和 hi = 5，ans += (4 + 5)*2
y = 3，lo = 3 和 hi = 3，

对于要添加的其他值(对于 y = 10 和 n = 10 中的 5)，观察它们可以在上面的步骤中找到，对于每个 y，在答案中添加 y * (n/y)。
对于 n = 10，
y = 1，ans += 1 * (10/1)
y = 2，ans += 2 * (10/2)。

下面是该方法的实现:

## C++

```
// C++ program to find sum of product of x and y
// such that n/x = y (Integer Division)
#include<bits/stdc++.h>
using namespace std;

// Return the sum of natural number in a range.
int sumOfRange(int a, int b)
{
    // n*(n+1)/2.
    int i = (a * (a+1)) >> 1;
    int j = (b * (b+1)) >> 1;
    return (i - j);
}

// Return the sum of product x*y.
int sumofproduct(int n)
{
    int sum = 0;

    // Iterating i from 1 to sqrt(n)
    int root = sqrt(n);
    for (int i=1; i<=root; i++)
    {
        // Finding the upper limit.
        int up = n/i;

        // Finding the lower limit.
        int low = max(n/(i+1), root);

        sum += (i * sumOfRange(up, low));
        sum += (i * (n/i));
    }

    return sum;
}

// Driven Program
int main()
{
    int n = 10;
    cout << sumofproduct(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// product of x and y such that
// n / x = y (Integer Division)
import java.io.*;

class GFG {

// Return the sum of natural number in a range.
static int sumOfRange(int a, int b)
{
    // n * (n + 1) / 2.
    int i = (a * (a + 1)) >> 1;
    int j = (b * (b + 1)) >> 1;
    return (i - j);
}

// Return the sum of product x*y.
static int sumofproduct(int n)
{
    int sum = 0;

    // Iterating i from 1 to sqrt(n)
    int root = (int)Math.sqrt(n);
    for (int i = 1; i <= root; i++)
    {
        // Finding the upper limit.
        int up = n / i;

        // Finding the lower limit.
        int low = Math.max(n / (i + 1), root);

        sum += (i * sumOfRange(up, low));
        sum += (i * (n / i));
    }

    return sum;
}

    // Driver Code
    static public void main(String[] args)
    {
        int n = 10;
        System.out.println(sumofproduct(n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find sum
# of product of x and y such
# that n/x = y (Integer Division)
import math

# Return the sum of natural
# number in a range.
def sumOfRange(a, b):
    # n*(n+1)/2.
    i = (a * (a + 1)) >> 1;
    j = (b * (b + 1)) >> 1;
    return (i - j);

# Return the sum of product x*y.
def sumofproduct(n):
    sum = 0;

    # Iterating i from 1 to sqrt(n)
    root = int(math.sqrt(n));
    for i in range(1, root + 1):
        # Finding the upper limit.
        up = int(n / i);

        # Finding the lower limit.
        low = max(int(n / (i + 1)), root);

        sum += (i * sumOfRange(up, low));
        sum += (i * int(n / i));

    return sum;

# Driven Code
n = 10;
print(sumofproduct(n));

# This code is contributed by mits
```

## C#

```
// C# program to find sum of
// product of x and y such that
// n / x = y (Integer Division)
using System;

class GFG {

// Return the sum of natural number in a range.
static int sumOfRange(int a, int b)
{
    // n * (n + 1) / 2.
    int i = (a * (a + 1)) >> 1;
    int j = (b * (b + 1)) >> 1;
    return (i - j);
}

// Return the sum of product x*y.
static int sumofproduct(int n)
{
    int sum = 0;

    // Iterating i from 1 to sqrt(n)
    int root = (int)Math.Sqrt(n);
    for (int i = 1; i <= root; i++)
    {
        // Finding the upper limit.
        int up = n / i;

        // Finding the lower limit.
        int low = Math.Max(n / (i + 1), root);

        sum += (i * sumOfRange(up, low));
        sum += (i * (n / i));
    }

    return sum;
}

    // Driver Code
    static public void Main(String[] args)
    {
        int n = 10;
        Console.WriteLine(sumofproduct(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of
// product of x and y such
// that n/x = y (Integer Division)

// Return the sum of natural
// number in a range.
function sumOfRange($a, $b)
{
    // n*(n+1)/2.
    $i = ($a * ($a + 1)) >> 1;
    $j = ($b * ($b + 1)) >> 1;
    return ($i - $j);
}

// Return the sum of product x*y.
function sumofproduct($n)
{
    $sum = 0;

    // Iterating i from 1 to sqrt(n)
    $root = sqrt($n);
    for ($i = 1; $i <= $root; $i++)
    {
        // Finding the upper limit.
        $up = (int)($n / $i);

        // Finding the lower limit.
        $low = max((int)($n / ($i + 1)), $root);

        $sum += ($i * sumOfRange($up, $low));
        $sum += ($i * (int)($n / $i));
    }

    return $sum;
}

// Driven Code
$n = 10;
echo sumofproduct($n) . "\n";

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Return the sum of natural number in a range.
function sumOfRange(a, b)
{
    // n * (n + 1) / 2.
    let i = (a * (a + 1)) >> 1;
    let j = (b * (b + 1)) >> 1;
    return (i - j);
}

// Return the sum of product x*y.
function sumofproduct(n)
{
    let sum = 0;

    // Iterating i from 1 to sqrt(n)
    let root = Math.floor(Math.sqrt(n));
    for (let i = 1; i <= root; i++)
    {
        // Finding the upper limit.
        let up = Math.floor(n / i);

        // Finding the lower limit.
        let low = Math.max(Math.floor(n / (i + 1)), root);

        sum += (i * sumOfRange(up, low));
        sum += (i * Math.floor(n / i));
    }

    return sum;
}

    // Driver Code

    let n = 10;
    document.write(sumofproduct(n));

</script>
```

**输出:**

```
87
```

**时间复杂度:**O(√N)
**来源:**
[https://www . quora . com/什么是最快解决问题的方法-说明-给定一个数-N-求所有积的和-x * y-这样-N-x-y-整数除法-这里-N-想要-N-10](https://www.quora.com/What-is-the-fastest-way-to-solve-the-problem-that-states-given-a-number-N-find-the-sum-of-all-products-x*y-such-that-N-x-y-integer-division-Here-N-would-be-N-10)
本文由
供稿如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
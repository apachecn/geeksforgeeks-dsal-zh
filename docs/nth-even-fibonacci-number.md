# 第 n 个偶数斐波那契数

> 原文:[https://www.geeksforgeeks.org/nth-even-fibonacci-number/](https://www.geeksforgeeks.org/nth-even-fibonacci-number/)

给定值 n，求第 n 个偶数[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
**例:**

```
Input  : n  = 3
Output : 34

Input  : n  = 4
Output : 144

Input : n = 7
Output : 10946
```

斐波那契数列是下列整数序列中的数字。
0、1、1、2、3、5、8、13、21、34、55、89、144、…。
其中序列中的任何数字由下式给出:

```
 Fn = Fn-1 + Fn-2 
      with seed values
      F0 = 0 and F1 = 1.
```

偶数斐波那契数列是，0，2，8，34，144，610，2584…我们需要找到这个序列中的第 n 个数字。
如果我们仔细看一下斐波那契数列，可以注意到**数列中每三个数字中就有一个是偶数**，偶数的数列遵循以下递归公式。

```
Recurrence for Even Fibonacci sequence is:
     EFn = 4EFn-1 + EFn-2
with seed values
     EF0 = 0 and EF1 = 2.

EFn represents n'th term in Even Fibonacci sequence.
```

**以上公式是如何工作的？**
我们来看看原创的斐波那契公式，因为每三个斐波那契数中就有一个是偶数，所以写成了 Fn-3 和 Fn-6 的形式。

```
Fn = Fn-1 + Fn-2 [Expanding both terms]
   = Fn-2 + Fn-3 + Fn-3 + Fn-4 
   = Fn-2 + 2Fn-3 + Fn-4 [Expanding first term]
   = Fn-3 + Fn-4 + 2Fn-3 + Fn-4
   = 3Fn-3 + 2Fn-4  [Expanding one Fn-4]
   = 3Fn-3 + Fn-4 + Fn-5 + Fn-6 [Combing Fn-4 and Fn-5]
   = 4Fn-3 + Fn-6  

Since every third Fibonacci Number is even, So if Fn is 
even then Fn-3 is even and Fn-6 is also even. Let Fn be
xth even element and mark it as EFx.
If Fn is EFx, then Fn-3 is previous even number i.e. EFx-1
and Fn-6 is previous of EFx-1 i.e. EFx-2
So
Fn = 4Fn-3 + Fn-6
which means,
EFx = 4EFx-1 + EFx-2
```

## C++

```
// C++ code to find Even Fibonacci
//Series using normal Recursion
#include<iostream>
using namespace std;

// Function which return
//nth even fibonacci number
long int evenFib(int n)
{
    if (n < 1)
    return n;
    if (n == 1)
    return 2;

    // calculation of
    // Fn = 4*(Fn-1) + Fn-2
    return ((4 * evenFib(n-1)) +
             evenFib(n-2));
}

// Driver Code
int main ()
{
    int n = 7;
    cout << evenFib(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find Even Fibonacci
// Series using normal Recursion

class GFG{

// Function which return
// nth even fibonacci number
static long evenFib(int n)
{
    if (n < 1)
    return n;

    if (n == 1)
    return 2;

    // calculation of
    // Fn = 4*(Fn-1) + Fn-2
    return ((4 * evenFib(n-1)) +
                 evenFib(n-2));
}

// Driver Code
public static void main (String[] args)
{
    int n = 7;
    System.out.println(evenFib(n));
}
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 code to find Even  Fibonacci
# Series using normal Recursion

# Function which return
#nth even fibonacci number
def evenFib(n) :
    if (n < 1) :
        return n
    if (n == 1)  :
        return 2

    # calculation of
    # Fn = 4*(Fn-1) + Fn-2
    return ((4 * evenFib(n-1)) + evenFib(n-2)) 

# Driver Code
n = 7
print(evenFib(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# code to find Even Fibonacci
// Series using normal Recursion
using System;

class GFG {

// Function which return
// nth even fibonacci number
static long evenFib(int n)
{
    if (n < 1)
    return n;

    if (n == 1)
    return 2;

    // calculation of Fn = 4*(Fn-1) + Fn-2
    return ((4 * evenFib(n - 1)) +
                 evenFib(n - 2));
}

// Driver code
public static void Main ()
{
    int n = 7;
    Console.Write(evenFib(n));
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find Even Fibonacci
// Series using normal Recursion

// Function which return
// nth even fibonacci number
function evenFib($n)
{
    if ($n < 1)
        return $n;
    if ($n == 1)
        return 2;

    // calculation of
    // Fn = 4*(Fn-1) + Fn-2
    return ((4 * evenFib($n-1)) +
                 evenFib($n-2));
}

// Driver Code
$n = 7;
echo(evenFib($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript code to find Even Fibonacci
// Series using normal Recursion

// Function which return
// nth even fibonacci number
function evenFib(n)
{
    if (n < 1)
        return n;
    if (n == 1)
        return 2;

    // calculation of
    // Fn = 4*(Fn-1) + Fn-2
    return ((4 * evenFib(n-1)) +
                 evenFib(n-2));
}

// Driver Code
let n = 7;
document.write(evenFib(n));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
10946
```

上述实现的时间复杂度是指数级的。我们可以使用动态规划在线性时间内完成。我们也可以使用事实 EF <sub>n</sub> = F <sub>3n</sub> 在 O(Log n)时间内完成。请注意，我们可以在 O(Log n)时间内找到第 n 个斐波那契数(请参见这里的方法 5 和 6)。
本文由**Shivam prad Han(anuj _ charm)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
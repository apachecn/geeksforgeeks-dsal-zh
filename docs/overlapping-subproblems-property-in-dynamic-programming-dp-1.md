# 动态规划中的重叠子问题属性| DP-1

> 原文:[https://www . geesforgeks . org/overlapping-sub-problems-property-in-dynamic-programming-DP-1/](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)

动态规划是一种算法范式，它通过将给定的复杂问题分解成子问题来解决它，并存储子问题的结果，以避免再次计算相同的结果。下面是一个问题的两个主要性质，表明给定的问题可以用动态规划来解决。

在这篇文章中，我们将详细讨论第一个性质(重叠子问题)。动态规划的第二个性质将在下一篇文章中讨论，即[集合 2](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/) 。
1) **重叠子问题**T5)2)**最优子结构**

**1)重叠子问题:**
像分治法一样，动态规划结合了子问题的解决方案。动态规划主要用于反复需要同一子问题的解时。在动态编程中，子问题的计算解存储在表中，这样就不必重新计算这些解。因此，当没有共同的(重叠的)子问题时，动态规划是没有用的，因为如果不再需要解决方案，就没有必要存储它们。比如[二分搜索法](https://www.geeksforgeeks.org/binary-search/)没有共同的子问题。如果我们以遵循斐波那契数递归程序为例，有许多子问题被一次又一次地解决。

## C

```
/* a simple recursive program for Fibonacci numbers */
int fib(int n)
{
    if (n <= 1)
        return n;

    return fib(n - 1) + fib(n - 2);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
/* a simple recursive program for Fibonacci numbers */
static int fib(int n)
{
    if (n <= 1)
        return n;

    return fib(n - 1) + fib(n - 2);
}

// This code is contributed by umadevi9616
```

## 计算机编程语言

```
#  a simple recursive program for Fibonacci numbers
def fib(n):
    if n <= 1:
        return n

    return fib(n - 1) + fib(n - 2)
```

## C#

```
/* a simple recursive program for Fibonacci numbers */
static int fib(int n)
{
    if (n <= 1)
        return n;

    return fib(n - 1) + fib(n - 2);
}

// This code contributed by umadevi9616
```

## java 描述语言

```
<script>
/*package whatever //do not write package name here */
/* a simple recursive program for Fibonacci numbers */
function fib(n)
{
    if (n <= 1)
        return n;

    return fib(n - 1) + fib(n - 2);
}

// This code is contributed by gauravrajput1
</script>
```

执行 *fib(5)* 的递归树

```

                         fib(5)
                     /             \
               fib(4)                fib(3)
             /      \                /     \
         fib(3)      fib(2)         fib(2)    fib(1)
        /     \        /    \       /    \
  fib(2)   fib(1)  fib(1) fib(0) fib(1) fib(0)
  /    \
fib(1) fib(0)
```

我们可以看到函数 fib(3)被调用了 2 次。如果我们已经存储了 fib(3)的值，那么我们可以重用旧的存储值，而不是再次计算它。有以下两种不同的方法来存储这些值，以便可以重复使用:
a)记忆(自上而下)
b)制表(自下而上)

**a)记忆化(自顶向下):**一个问题的记忆化程序类似于递归版本，只是做了一点修改，在计算解决方案之前查看查找表。我们初始化一个查找数组，所有的初始值都是零。每当我们需要一个子问题的解决方案时，我们首先查看查找表。如果预先计算的值在那里，那么我们返回该值，否则，我们计算该值并将结果放在查找表中，以便以后可以重用。

以下是第 n 个斐波那契数的记忆版本。

## C++

```
/* C++ program for Memoized version
for nth Fibonacci number */
#include <bits/stdc++.h>
using namespace std;
#define NIL -1
#define MAX 100

int lookup[MAX];

/* Function to initialize NIL
values in lookup table */
void _initialize()
{
    int i;
    for (i = 0; i < MAX; i++)
        lookup[i] = NIL;
}

/* function for nth Fibonacci number */
int fib(int n)
{
    if (lookup[n] == NIL) {
        if (n <= 1)
            lookup[n] = n;
        else
            lookup[n] = fib(n - 1) + fib(n - 2);
    }

    return lookup[n];
}

// Driver code
int main()
{
    int n = 40;
    _initialize();
    cout << "Fibonacci number is " << fib(n);
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
/* C program for Memoized version for nth Fibonacci number
 */
#include <stdio.h>
#define NIL -1
#define MAX 100

int lookup[MAX];

/* Function to initialize NIL values in lookup table */
void _initialize()
{
    int i;
    for (i = 0; i < MAX; i++)
        lookup[i] = NIL;
}

/* function for nth Fibonacci number */
int fib(int n)
{
    if (lookup[n] == NIL) {
        if (n <= 1)
            lookup[n] = n;
        else
            lookup[n] = fib(n - 1) + fib(n - 2);
    }

    return lookup[n];
}

int main()
{
    int n = 40;
    _initialize();
    printf("Fibonacci number is %d ", fib(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program for Memoized version */
public class Fibonacci {
    final int MAX = 100;
    final int NIL = -1;

    int lookup[] = new int[MAX];

    /* Function to initialize NIL values in lookup table */
    void _initialize()
    {
        for (int i = 0; i < MAX; i++)
            lookup[i] = NIL;
    }

    /* function for nth Fibonacci number */
    int fib(int n)
    {
        if (lookup[n] == NIL) {
            if (n <= 1)
                lookup[n] = n;
            else
                lookup[n] = fib(n - 1) + fib(n - 2);
        }
        return lookup[n];
    }

    public static void main(String[] args)
    {
        Fibonacci f = new Fibonacci();
        int n = 40;
        f._initialize();
        System.out.println("Fibonacci number is"
                           + " " + f.fib(n));
    }
}
// This Code is Contributed by Saket Kumar
```

## 计算机编程语言

```
# a program for Memoized version of nth Fibonacci number

# function to calculate nth Fibonacci number

def fib(n, lookup):

    # base case
    if n <= 1:
        lookup[n] = n

    # if the value is not calculated previously then calculate it
    if lookup[n] is None:
        lookup[n] = fib(n-1, lookup) + fib(n-2, lookup)

    # return the value corresponding to that value of n
    return lookup[n]
# end of function

# Driver program to test the above function

def main():
    n = 34
    # Declaration of lookup table
    # Handles till n = 100
    lookup = [None] * 101
    print "Fibonacci Number is ", fib(n, lookup)

if __name__ == "__main__":
    main()

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program for Memoized versionof nth Fibonacci number
using System;

class GFG {

    static int MAX = 100;
    static int NIL = -1;
    static int[] lookup = new int[MAX];

    /* Function to initialize NIL
    values in lookup table */
    static void initialize()
    {
        for (int i = 0; i < MAX; i++)
            lookup[i] = NIL;
    }

    /* function for nth Fibonacci number */
    static int fib(int n)
    {
        if (lookup[n] == NIL) {
            if (n <= 1)
                lookup[n] = n;
            else
                lookup[n] = fib(n - 1) + fib(n - 2);
        }
        return lookup[n];
    }

    // Driver code
    public static void Main()
    {

        int n = 40;
        initialize();
        Console.Write("Fibonacci number is"
                      + " " + fib(n));
    }
}

// This Code is Contributed by Sam007
```

## java 描述语言

```
<script>

let  MAX = 100;
let NIL = -1;

let lookup = new Array(MAX);

function  _initialize()
{
    for (let i = 0; i < MAX; i++)
        lookup[i] = NIL;
}

function fib(n)
{
    if (lookup[n] == NIL)
    {
      if (n <= 1)
          lookup[n] = n;
      else
          lookup[n] = fib(n-1) + fib(n-2);
    }
    return lookup[n];
}

let n = 40;
_initialize();
document.write("Fibonacci number is" + " " + fib(n)+"<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
Fibonacci number is 102334155
```

**b)列表(自下而上):**给定问题的列表程序以自下而上的方式构建表格，并返回表格中的最后一个条目。例如，对于相同的斐波那契数，我们首先计算 fib(0)，然后 fib(1)，然后 fib(2)，然后 fib(3)，依此类推。所以从字面上看，我们正在自下而上地构建子问题的解决方案。

以下是第 n 个斐波那契数的列表版本。

## C++

```
/* C program for Tabulated version */
#include <stdio.h>
int fib(int n)
{
    int f[n + 1];
    int i;
    f[0] = 0;
    f[1] = 1;
    for (i = 2; i <= n; i++)
        f[i] = f[i - 1] + f[i - 2];

    return f[n];
}

int main()
{
    int n = 9;
    printf("Fibonacci number is %d ", fib(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program for Tabulated version */
public class Fibonacci {
    int fib(int n)
    {
        int f[] = new int[n + 1];
        f[0] = 0;
        f[1] = 1;
        for (int i = 2; i <= n; i++)
            f[i] = f[i - 1] + f[i - 2];
        return f[n];
    }

    public static void main(String[] args)
    {
        Fibonacci f = new Fibonacci();
        int n = 9;
        System.out.println("Fibonacci number is"
                           + " " + f.fib(n));
    }
}
// This Code is Contributed by Saket Kumar
```

## 计算机编程语言

```
# Python program Tabulated (bottom up) version
def fib(n):

    # array declaration
    f = [0] * (n + 1)

    # base case assignment
    f[1] = 1

    # calculating the fibonacci and storing the values
    for i in xrange(2, n + 1):
        f[i] = f[i - 1] + f[i - 2]
    return f[n]

# Driver program to test the above function

def main():
    n = 9
    print "Fibonacci number is ", fib(n)

if __name__ == "__main__":
    main()

# This code is contributed by Nikhil Kumar Singh (nickzuck_007)
```

## C#

```
// C# program for Tabulated version
using System;

class GFG {
    static int fib(int n)
    {
        int[] f = new int[n + 1];
        f[0] = 0;
        f[1] = 1;
        for (int i = 2; i <= n; i++)
            f[i] = f[i - 1] + f[i - 2];
        return f[n];
    }

    public static void Main()
    {

        int n = 9;
        Console.Write("Fibonacci number is"
                      + " " + fib(n));
    }
}

// This Code is Contributed by Sam007
```

## java 描述语言

```
<script>

// Javascript program for Tabulated version
function fib(n)
{
    var f = new Array(n + 1);
    var i;

    f[0] = 0;
    f[1] = 1;
    for(i = 2; i <= n; i++)
        f[i] = f[i - 1] + f[i - 2];

    return f[n];
}

// Driver code
var n = 9;
document.write("Fibonacci number is  " + fib(n));

// This code is contributed by akshitsaxenaa09

</script>
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Tabulated version

function fib($n)
{
    $f[$n + 1]=0;
    $i;
    $f[0] = 0;
    $f[1] = 1;
    for ($i = 2; $i <= $n; $i++)
        $f[$i] = $f[$i - 1] +
                 $f[$i - 2];

    return $f[$n];
}

// Driver Code
$n = 9;
echo("Fibonacci number is ");
echo(fib($n));

// This code is contributed by nitin mittal.
?>
```

**Output**

```
Fibonacci number is 34 
```

列表和记忆都存储子问题的解。在 Memoized 版本中，表是按需填充的，而在列表版本中，从第一个条目开始，所有条目都是逐个填充的。与列表版本不同，查找表的所有条目不一定都在 Memoized 版本中填充。例如， [LCS 问题](http://en.wikipedia.org/wiki/Longest_common_subsequence_problem)的[记忆化解决方案](https://www.ics.uci.edu/~eppstein/161/960229.html)不一定会填充所有条目。

要查看记忆化和列表化解决方案相对于基本递归解决方案所实现的优化，请查看计算第 40 个斐波那契数的以下运行所花费的时间:
[递归解决方案](https://ide.geeksforgeeks.org/vHt6ly)
[记忆化解决方案](https://ide.geeksforgeeks.org/Z94jYR)
[列表化解决方案](https://ide.geeksforgeeks.org/12C5bP)
递归方法所花费的时间比上面提到的两种动态编程技术——记忆和列表要多得多！

同样，参见[丑陋数字帖子](https://www.geeksforgeeks.org/ugly-numbers/)的方法 2，了解一个更简单的例子，其中我们有重叠的子问题，我们存储子问题的结果。

我们将在动态规划的未来帖子中讨论最优子结构属性和一些更多的示例问题。

尝试以下问题作为这篇文章的练习。
1)为 LCS 问题写一个记忆化的解。请注意，表格解决方案在《CLRS》一书中给出。
2)你会如何在记忆和制表之间做出选择？

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
参考文献:
T2http://www.youtube.com/watch?v=V5hZoJ6uK-s
# 西尔维斯特的序列

> 原文:[https://www.geeksforgeeks.org/sylvesters-sequence/](https://www.geeksforgeeks.org/sylvesters-sequence/)

在数系中，[西尔维斯特序列](https://en.wikipedia.org/wiki/Sylvester's_sequence)是一个整数序列，序列中的每个成员都是前几个成员的乘积，加 1。给定正整数 **N** 。任务是打印序列的前 N 个成员。
由于数字可能很大，使用 **%10^9 + 7** 。
示例:

```
Input : N = 6
Output : 2 3 7 43 1807 3263443

Input : N = 2
Output : 2 3
```

其思想是运行一个循环，取两个变量，并将其初始化为 1 和 2，一个存储到目前为止的乘积，另一个存储当前的数字，它只不过是第一个数字+ 1，对于每一步，都使用算术模运算相乘，即(a + b)%N = (a%N + b%N)%N，其中 N 是模数。
以下是该方法的实现:

## C++

```
// CPP program to print terms of Sylvester's sequence
#include <bits/stdc++.h>
using namespace std;
#define N 1000000007

void printSequence(int n)
{
    int a = 1; // To store the product.
    int ans = 2; // To store the current number.

    // Loop till n.
    for (int i = 1; i <= n; i++) {
        cout << ans << " ";
        ans = ((a % N) * (ans % N)) % N;
        a = ans;
        ans = (ans + 1) % N;
    }
}

// Driven Program
int main()
{
    int n = 6;
    printSequence(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Sylvester sequence
import java.util.*;

class GFG {

    public static void printSequence(int n)
    {
        int a = 1; // To store the product.
        int ans = 2; // To store the current number.
        int N = 1000000007;

        // Loop till n.
        for (int i = 1; i <= n; i++) {
           System.out.print(ans + " ");
            ans = ((a % N) * (ans % N)) % N;
            a = ans;
            ans = (ans + 1) % N;
        }
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n = 6;
        printSequence(n);

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 计算机编程语言

```
# Python Code for Sylvester sequence

def printSequence(n) :
    a = 1 # To store the product.
    ans = 2 # To store the current number.
    N = 1000000007

    # Loop till n.
    i = 1
    while i <= n :
        print ans,
        ans = ((a % N) * (ans % N)) % N
        a = ans
        ans = (ans + 1) % N
        i = i + 1

# Driver program to test above function
n = 6
printSequence(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Code for Sylvester sequence
using System;

class GFG {

    public static void printSequence(int n)
    {
         // To store the product.
        int a = 1;

        // To store the current number.
        int ans = 2;

        int N = 1000000007;

        // Loop till n.
        for (int i = 1; i <= n; i++)
        {
            Console.Write(ans + " ");
            ans = ((a % N) * (ans % N)) % N;
            a = ans;
            ans = (ans + 1) % N;
        }
    }

    // Driver program
    public static void Main()
    {
        int n = 6;
        printSequence(n);

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// terms of Sylvester's sequence

$N = 1000000007;

function printSequence($n)
{
    global $N;

    // To store
    // the product.
    $a = 1;

    // To store the
    // current number.
    $ans = 2;

    // Loop till n.
    for ($i = 1; $i <= $n; $i++)
    {
        echo $ans ," ";
        $ans = (($a % $N) * ($ans % $N)) % $N;
        $a = $ans;
        $ans = ($ans + 1) % $N;
    }
}

    // Driver Code
    $n = 6;
    printSequence($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to print
// terms of Sylvester's sequence

let N = 1000000007;

function printSequence(n)
{

    // To store
    // the product.
    let a = 1;

    // To store the
    // current number.
    let ans = 2;

    // Loop till n.
    for (let i = 1; i <= n; i++)
    {
        document.write(ans + " ");
        ans = ((a % N) * (ans % N)) % N;
        a = ans;
        ans = (ans + 1) % N;
    }
}

    // Driver Code
    let n = 6;
    printSequence(n);

// This code is contributed by gfgking.
</script>
```

输出:

```
2 3 7 43 1807 3263443
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
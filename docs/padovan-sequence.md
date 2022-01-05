# 帕多万序列

> 原文:[https://www.geeksforgeeks.org/padovan-sequence/](https://www.geeksforgeeks.org/padovan-sequence/)

[帕多万序列](https://en.wikipedia.org/wiki/Padovan_sequence)类似斐波那契序列，递归结构相似。递归公式是，

```
  P(n) = P(n-2) + P(n-3)
  P(0) = P(1) = P(2) = 1 
```

**斐波那契数列:** 0，1，1，2，3，5，8，13，21，34，55……
边长遵循斐波那契数列的正方形螺旋。

![fibonacci-tiles1](img/b632b1bc1f575aa1beba3b2b47ed1ad2.png)

**帕多万序列:** 1，1，1，2，2，3，4，5，7，9，12，16，21，28，37，…..
等边三角形螺旋，边长遵循帕多万序列。

![Padovan_triangles_(1)](img/dfe275bf9e465976bfdd2b78eb42ec54.png)

示例:

```
For Padovan Sequence:
P0 = P1 = P2 = 1 ,
P(7) = P(5) + P(4)
     = P(3) + P(2) + P(2) + P(1)
     = P(2) + P(1) + 1 + 1 + 1
     = 1 + 1 + 1 + 1 + 1 
     = 5
```

## C++

```
// C++ program to find n'th term in Padovan Sequence
// using Dynamic Programming
#include<iostream>
using namespace std;

/* Function to calculate padovan number P(n) */
int pad(int n)
{
    /* 0th ,1st and 2nd number of the series are 1*/
    int pPrevPrev = 1, pPrev = 1, pCurr = 1, pNext = 1;

    for (int i=3; i<=n; i++)
    {
        pNext = pPrevPrev + pPrev;
        pPrevPrev = pPrev;
        pPrev = pCurr;
        pCurr = pNext;
    }

    return pNext;
}

/* Driver Program */
int main()
{
    int n = 12;
    cout << pad(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n'th term
// in Padovan Sequence using
// Dynamic Programming
import java.io.*;

class GFG {

    /* Function to calculate
    padovan number P(n) */
    static int pad(int n)
    {
       int []padv=new int[n]; //create array to store padovan values
       padv[0]=padv[1]=padv[2]=1;
        for (int i = 3; i <= n; i++) {
         padv[i]=padv[i-2]+padv[i-3];  
        }
        return padv[n-1];

    }

    /* Driver Program */
    public static void main(String args[])
    {
        int n = 12;
        System.out.println(pad(n));
    }
}

/*This code is contributed by Kanjam Bhat Lidhoo.*/
```

## 计算机编程语言

```
# Python program to find n'th term in Padovan
# Sequence using Dynamic Programming

# Function to calculate padovan number P(n)
def pad(n):

    # 0th ,1st and 2nd number of the series are 1
    pPrevPrev, pPrev, pCurr, pNext = 1, 1, 1, 1

    # Find n'th Padovan number using recursive
    # formula.
    for i in range(3, n+1):
        pNext = pPrevPrev + pPrev
        pPrevPrev = pPrev
        pPrev = pCurr
        pCurr = pNext

    return pNext;

# Driver Code
print pad(12)
```

## C#

```
// C# program to find n'th term
// in Padovan Sequence using
// Dynamic Programming
using System;

class GFG {

    /* Function to calculate
    padovan number P(n) */
    static int pad(int n)
    {

        /* 0th, 1st and 2nd number
        of the series are 1*/
        int pPrevPrev = 1, pPrev = 1,
            pCurr = 1, pNext = 1;

        for (int i = 3; i <= n; i++) {
            pNext = pPrevPrev + pPrev;
            pPrevPrev = pPrev;
            pPrev = pCurr;
            pCurr = pNext;
        }

        return pNext;
    }

    /* Driver Program */
    public static void Main()
    {
        int n = 12;

        Console.WriteLine(pad(n));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n'th
// term in Padovan Sequence
// using Dynamic Programming

// Function to calculate
// padovan number P(n)
function pad($n)
{

    // 0th ,1st and 2nd number
    // of the series are 1
    $pPrevPrev = 1; $pPrev = 1;
    $pCurr = 1; $pNext = 1;

    for ($i = 3; $i <= $n; $i++)
    {
        $pNext = $pPrevPrev + $pPrev;
        $pPrevPrev = $pPrev;
        $pPrev = $pCurr;
        $pCurr = $pNext;
    }

    return $pNext;
}

// Driver Code
$n = 12;
echo(pad($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to find n'th
// term in Padovan Sequence
// using Dynamic Programming

// Function to calculate
// padovan number P(n)
function pad(n) {

    // 0th ,1st and 2nd number
    // of the series are 1
    let pPrevPrev = 1;
    let pPrev = 1;
    let pCurr = 1;
    let pNext = 1;

    for (let i = 3; i <= n; i++) {
        pNext = pPrevPrev + pPrev;
        pPrevPrev = pPrev;
        pPrev = pCurr;
        pCurr = pNext;
    }

    return pNext;
}

// Driver Code
let n = 12;
document.write(pad(n));

// This code is contributed by gfgking.
</script>
```

输出:

```
21
```

本文由**Shivam prad Han(anuj _ charm)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
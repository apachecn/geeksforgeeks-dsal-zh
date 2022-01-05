# 用严格递增顺序的数字生成 k 位数

> 原文:[https://www . geesforgeks . org/generate-k-digits-numbers-digits-严格递增顺序/](https://www.geeksforgeeks.org/generate-k-digit-numbers-digits-strictly-increasing-order/)

给定一个值 k，生成所有长度为 k 的有序数。有序意味着它应该在增加。
**例:**

```
Input : K = 7
Output :
1234567 1234568 1234569 1234578 1234579
1234589 1234678 1234679 1234689 1234789 
1235678 1235679 1235689 1235789 1236789 
1245678 1245679 1245689 1245789 1246789 
1256789 1345678 1345679 1345689 1345789 
1346789 1356789 1456789 2345678 2345679 
2345689 2345789 2346789 2356789 2456789 
3456789

Input  : K = 3
Output :
123 124 125 126 127 128 129 134 135 136 
137 138 139 145 146 147 148 149 156 157 
158 159 167 168 169 178 179 189 234 235 
236 237 238 239 245 246 247 248 249 256 
257 258 259 267 268 269 278 279 289 345 
346 347 348 349 356 357 358 359 367 368 
369 378 379 389 456 457 458 459 467 468 
469 478 479 489 567 568 569 578 579 589 
678 679 689 789 
```

这个问题非常简单，可以打印所有可能的长度为 k 的字符串，这些字符串可以由一组 n 个字符组成
**1。**循环通过 i = x 到 9。(所有挖其将从 1 到 9)。
**2。** x 将以 0 开始，每次重复调用都会递增，以确保数字格式正确。
**3。**每次重复调用时，将结果(从 0 开始)乘以 10，加上 I，使 k = k-1。
以下是上述思路的实现:

## C++

```
// C++ program to generate well
// ordered numbers with k digits.
#include<bits/stdc++.h>
using namespace std;

// number --> Current value of number.
// x --> Current digit to be considered
// k --> Remaining number of digits
void printWellOrdered(int number, 
                      int x, int k)
{
    if (k == 0)
    {
        cout << number << " ";
        return;
    }

    // Try all possible greater digits
    for (int i = (x + 1); i < 10; i++)
        printWellOrdered(number * 10 + 
                         i, i, k - 1);
}

// Generates all well ordered 
// numbers of length k.
void generateWellOrdered(int k)
{
    printWellOrdered(0, 0, k);
}

// Driver code
int main()
{
    int k = 3;
    generateWellOrdered(k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate well 
// ordered numbers with k digits.

class Generate
{
    // number --> Current value of number.
    // x --> Current digit to be considered
    // k --> Remaining number of digits
    static void printWellOrdered(int number, 
                                 int x, int k)
    {
        if (k == 0)
        {
            System.out.print(number+" ");
            return;
        }

        // Try all possible greater digits
        for (int i = (x + 1); i < 10; i++)
            printWellOrdered(number * 10 + 
                             i, i, k - 1);
    }

    // Generates all well ordered 
    // numbers of length k.
    static void generateWellOrdered(int k)
    {
        printWellOrdered(0, 0, k);
    }

    // Driver Code 
    public static void main (String[] args) 
    {
        int k = 3;
        generateWellOrdered(k);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to generate well
# ordered numbers with k digits.

# number --> Current value of number.
# x --> Current digit to be considered
# k --> Remaining number of digits
def printWellOrdered(number, x, k):

    if (k == 0):
        print(number, end = " ")
        return

    # Try all possible greater digits
    for i in range( (x + 1), 10):
        printWellOrdered(number * 10 + i,
                                i, k - 1)

# Generates all well ordered 
# numbers of length k.
def generateWellOrdered(k):
    printWellOrdered(0, 0, k)

# Driver code
if __name__ == "__main__":

    k = 3
    generateWellOrdered(k)

# This code is contributed by Ita_c
```

## C#

```
// C# program to generate well
// ordered numbers with k digits.
using System;

class GFG 
{

    // number --> Current value of number.
    // x --> Current digit to be considered
    // k --> Remaining number of digits
    static void printWellOrdered(int number, 
                                 int x, int k)
    {

        if (k == 0)
        {
            Console.Write(number + " ");
            return;
        }

        // Try all possible greater digits
        for (int i = (x + 1); i < 10; i++)
            printWellOrdered(number * 10 + 
                             i, i, k - 1);
    }

    // Generates all well ordered 
    // numbers of length k.
    static void generateWellOrdered(int k)
    {
        printWellOrdered(0, 0, k);
    }

    // Driver Code
    public static void Main () 
    {
        int k = 3;
        generateWellOrdered(k);
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate well 
// ordered numbers with k digits.

// number --> Current value of number.
// x --> Current digit to be considered
// k --> Remaining number of digits
function printWellOrdered($number, $x, $k)
{
    if ($k == 0)
    {
        echo $number, " ";
        return;
    }

    // Try all possible greater digits
    for ($i = ($x + 1); $i < 10; $i++)
        printWellOrdered($number * 10 + 
                         $i, $i, $k - 1);
}

// Generates all well ordered 
// numbers of length k
function generateWellOrdered($k)
{
    printWellOrdered(0, 0, $k);
}

// Driver code
$k = 3;
generateWellOrdered($k);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to generate well 
// ordered numbers with k digits.

    // number --> Current value of number.
    // x --> Current digit to be considered
    // k --> Remaining number of digits
    function printWellOrdered(number,x,k)
    {
        if (k == 0)
        {
            document.write(number+" ");
            return;
        }

        // Try all possible greater digits
        for (let i = (x + 1); i < 10; i++)
            printWellOrdered(number * 10 + 
                             i, i, k - 1);
    }

    // Generates all well ordered 
    // numbers of length k.
    function generateWellOrdered(k)
    {
        printWellOrdered(0, 0, k);
    }

    // Driver Code 
    let k = 3;
    generateWellOrdered(k);

    // This code is contributed by rag2127

</script>
```

**输出:**

```
123 124 125 126 127 128 129 134 135 136 137 
138 139 145 146 147 148 149 156 157 158 159 
167 168 169 178 179 189 234 235 236 237 238 
239 245 246 247 248 249 256 257 258 259 267 
268 269 278 279 289 345 346 347 348 349 356 
357 358 359 367 368 369 378 379 389 456 457 
458 459 467 468 469 478 479 489 567 568 569 
578 579 589 678 679 689 789 
```

本文由 [**拉克什·库马尔**](https://www.facebook.com/Rakesh2raj) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
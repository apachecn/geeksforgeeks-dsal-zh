# 贝尔数(分割集合的方式数)

> 原文:[https://www . geeksforgeeks . org/bell-numbers-对集合进行分区的方式数/](https://www.geeksforgeeks.org/bell-numbers-number-of-ways-to-partition-a-set/)

给定一组 n 个元素，找到许多分割它的方法。
示例:

```
Input:  n = 2
Output: Number of ways = 2
Explanation: Let the set be {1, 2}
            { {1}, {2} } 
            { {1, 2} }

Input:  n = 3
Output: Number of ways = 5
Explanation: Let the set be {1, 2, 3}
             { {1}, {2}, {3} }
             { {1}, {2, 3} }
             { {2}, {1, 3} }
             { {3}, {1, 2} }
             { {1, 2, 3} }. 
```

以上问题的解决方案是[铃号](https://en.wikipedia.org/wiki/Bell_number)。
**什么是铃号？**
设 **S(n，k)** 为 n 个元素划分成 k 个集合的总数。第 n 个贝尔数的值是 k = 1 到 n 的 S(n，k)的和，
![Bell(n) = \sum_{k=0}^{n}S(n,k)  ](img/104c52b236b52f454aa5282b4eb2abfb.png "Rendered by QuickLaTeX.com")
S(n，k)的值可以递归定义为，S(n+1，k) = k*S(n，k) + S(n，k-1)
以上递归公式是如何工作的？
当我们给 k 个分区添加第(n+1)个元素时，有两种可能。
1)作为单个元素集合添加到现有分区，即 S(n，k-1)
2)添加到每个分区的所有集合，即 k*S(n，k)
S(n，k)称为第二类[斯特林数](https://en.wikipedia.org/wiki/Stirling_numbers_of_the_second_kind)
前几个贝尔数是 1，1，2，5，15，52，203，…
一种**计算第 n 个贝尔数的简单方法**是逐个计算 k = 1 到 n 的 S(n，k)，并返回所有计算值的和。S(n，k)的计算参见[本](https://www.geeksforgeeks.org/count-number-of-ways-to-partition-a-set-into-k-subsets/)。
一个**比较好的方法**就是用[钟形三角](https://en.wikipedia.org/wiki/Bell_triangle)。下面是前几个钟形数字的钟形三角形示例。

```
1
1 2
2 3 5
5 7 10 15
15 20 27 37 52
```

三角形是用下面的公式构造的。

```
// If this is first column of current row 'i'
If j == 0
   // Then copy last entry of previous row
   // Note that i'th row has i entries
   Bell(i, j) = Bell(i-1, i-1) 

// If this is not first column of current row
Else 
   // Then this element is sum of previous element 
   // in current row and the element just above the
   // previous element
   Bell(i, j) = Bell(i-1, j-1) + Bell(i, j-1)
```

**解释**
然后 Bell(n，k)统计集合{1，2，…，n + 1}的分区数，其中元素 k + 1 是其集合中可以单独存在的最大元素。
比如 Bell(3，2)是 3，它是{1，2，3，4}的分区数的计数，其中 3 是最大的单体元素。有三个这样的分区:

```
    {1}, {2, 4}, {3}
    {1, 4}, {2}, {3}
    {1, 2, 4}, {3}. 
```

下面是基于动态规划的上述递归公式的实现。

## C++

```
// A C++ program to find n'th Bell number
#include<iostream>
using namespace std;

int bellNumber(int n)
{
   int bell[n+1][n+1];
   bell[0][0] = 1;
   for (int i=1; i<=n; i++)
   {
      // Explicitly fill for j = 0
      bell[i][0] = bell[i-1][i-1];

      // Fill for remaining values of j
      for (int j=1; j<=i; j++)
         bell[i][j] = bell[i-1][j-1] + bell[i][j-1];
   }
   return bell[n][0];
}

// Driver program
int main()
{
   for (int n=0; n<=5; n++)
      cout << "Bell Number " << n << " is "
           << bellNumber(n) << endl;
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n'th Bell number
import java.io.*;

class GFG
{
    // Function to find n'th Bell Number
    static int bellNumber(int n)
    {
        int[][] bell = new int[n+1][n+1];
        bell[0][0] = 1;

        for (int i=1; i<=n; i++)
        {
            // Explicitly fill for j = 0
            bell[i][0] = bell[i-1][i-1];

            // Fill for remaining values of j
            for (int j=1; j<=i; j++)
                bell[i][j] = bell[i-1][j-1] + bell[i][j-1];
        }

        return bell[n][0];
    }

    // Driver program
    public static void main (String[] args)
    {
        for (int n=0; n<=5; n++)
            System.out.println("Bell Number "+ n +
                            " is "+bellNumber(n));
    }
}

// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
# A Python program to find n'th Bell number

def bellNumber(n):

    bell = [[0 for i in range(n+1)] for j in range(n+1)]
    bell[0][0] = 1
    for i in range(1, n+1):

        # Explicitly fill for j = 0
        bell[i][0] = bell[i-1][i-1]

        # Fill for remaining values of j
        for j in range(1, i+1):
            bell[i][j] = bell[i-1][j-1] + bell[i][j-1]

    return bell[n][0]

# Driver program
for n in range(6):
    print('Bell Number', n, 'is', bellNumber(n))

# This code is contributed by Soumen Ghosh
```

## C#

```
// C# program to find n'th Bell number
using System;

class GFG {

    // Function to find n'th
    // Bell Number
    static int bellNumber(int n)
    {
        int[,] bell = new int[n + 1,
                              n + 1];
        bell[0, 0] = 1;

        for (int i = 1; i <= n; i++)
        {

            // Explicitly fill for j = 0
            bell[i, 0] = bell[i - 1, i - 1];

            // Fill for remaining values of j
            for (int j = 1; j <= i; j++)
                bell[i, j] = bell[i - 1, j - 1] +
                             bell[i, j - 1];
        }

        return bell[n, 0];
    }

    // Driver Code
    public static void Main ()
    {
        for (int n = 0; n <= 5; n++)
            Console.WriteLine("Bell Number "+ n +
                              " is "+bellNumber(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find
// n'th Bell number

// function that returns
// n'th bell number
function bellNumber($n)
{

    $bell[0][0] = 1;
    for ($i = 1; $i <= $n; $i++)
    {

        // Explicitly fill for j = 0
        $bell[$i][0] = $bell[$i - 1]
                            [$i - 1];

        // Fill for remaining
        // values of j
        for ($j = 1; $j <= $i; $j++)
            $bell[$i][$j] = $bell[$i - 1][$j - 1] +
                                $bell[$i][$j - 1];
    }
    return $bell[$n][0];
}

// Driver Code
for ($n = 0; $n <= 5; $n++)
echo("Bell Number " . $n . " is "
      . bellNumber($n) . "\n");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

    // Javascript program to find n'th Bell number

    // Function to find n'th Bell Number
    function bellNumber(n)
    {
        let bell = new Array(n+1);
        for(let i = 0; i < n + 1; i++)
        {
            bell[i] = new Array(n + 1);
        }
        bell[0][0] = 1;

        for (let i=1; i<=n; i++)
        {
            // Explicitly fill for j = 0
            bell[i][0] = bell[i-1][i-1];

            // Fill for remaining values of j
            for (let j=1; j<=i; j++)
                bell[i][j] = bell[i-1][j-1] + bell[i][j-1];
        }

        return bell[n][0];
    }

    for (let n=0; n<=5; n++)
            document.write("Bell Number "+ n + " is "+bellNumber(n) + "</br>");

</script>
```

**输出:**

```
Bell Number 0 is 1
Bell Number 1 is 1
Bell Number 2 is 2
Bell Number 3 is 5
Bell Number 4 is 15
Bell Number 5 is 52
```

上述解的时间复杂度为 O(n <sup>2</sup> )。我们将很快讨论计算贝尔数的其他更有效的方法。
另一个可以通过贝尔数字解决的问题。
如果一个数不能被 1 以外的正方整除，则该数为[无方](https://en.wikipedia.org/wiki/Square-free_integer)。例如，6 是一个平方自由数，但是 12 不能被 4 整除。
给定一个无平方数 x，求 x 的不同乘法分区的个数，乘法分区的个数为 Bell(n)，其中 n 为 x 的素因子个数，例如 x = 30，有 3 个 2、3、5 的素因子。所以答案是贝尔(3)，也就是 5。5 个分区分别是 1 x 30、2 x15、3 x 10、5 x 6 和 2 x 3 x 5。
**练习:**
上述实现会导致稍大的 n 值出现算术溢出。扩展上述程序，使结果在模 1000000007 下计算，以避免溢出。
**参考:**
[https://en.wikipedia.org/wiki/Bell_number](https://en.wikipedia.org/wiki/Bell_number)
[https://en.wikipedia.org/wiki/Bell_triangle](https://en.wikipedia.org/wiki/Bell_triangle)
本文由**拉杰夫·阿格沃尔**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
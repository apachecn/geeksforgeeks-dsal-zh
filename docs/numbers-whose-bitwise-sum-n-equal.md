# 按位“或”与“和”等于“N”的数字

> 原文:[https://www . geesforgeks . org/numbers-what-bitwise-sum-n-equal/](https://www.geeksforgeeks.org/numbers-whose-bitwise-sum-n-equal/)

给定一个非负整数 N，任务是找出小于或等于 N 的非负整数
的个数，其按位 or 和与 N 之和相等。
**例:**

```
Input  : N = 3
Output : 1
0 is the only number in [0, 3]
that satisfies given property.
(0 + 3) = (0 | 3)

Input  : 10
Output : 4
(0 + 10) = (0 | 10) (Both are 10)
(1 + 10) = (1 | 10) (Both are 11)
(4 + 10) = (4 | 10) (Both are 14)
(5 + 10) = (5 | 10) (Both are 15)
```

一个**简单的解决方案**是遍历从 0 到 N 的所有数字，用 N 做按位 OR 和 SUM，如果两者都是等增量计数器。
时间复杂度= 0(N)。
一个**高效的解决方案**是遵循以下步骤。
1。在 N.
2 中查找零位计数。返回功率(2，计数)。
这个想法是基于这样一个事实，即带有 N 的数 x 的按位“或”和“和”是相等的，当且仅当带有 N 的数 x 的
按位“与”将是 0

```
Let, N=10 =10102.
Bitwise AND of a number with N will be 0, if number 
contains zero bit with all respective set bit(s) of
N and either zero bit or set bit with all respective 
zero bit(s) of N (because, 0&0=1&0=0).
  e.g. 
bit     : 1   0   1   0
position: 4   3   2   1
Bitwise AND of any number with N will be 0, if the number
has following bit pattern
1st position can be  either 0 or 1 (2 ways)
2nd position can be  1 (1 way)
3rd position can be  either 0 or 1 (2 ways)
4th position can be  1 (1 way)
Total count = 2*1*2*1 = 22 = 4.
```

## C++

```
// C++ program to count numbers whose bitwise
// OR and sum with N are equal
#include <bits/stdc++.h>
using namespace std;

// Function to find total 0 bit in a number
unsigned int CountZeroBit(int n)
{
    unsigned int count = 0;
    while(n)
    {
       if (!(n & 1))
           count++;
       n >>= 1;
    }
    return count;
}

// Function to find Count of non-negative numbers
// less than or equal to N, whose bitwise OR and
// SUM with N are equal.
int CountORandSumEqual(int N )
{
    // count number of zero bit in N
    int count = CountZeroBit(N);

    // power of 2 to count
    return (1 << count);
}

// Driver code
int main()
{
   int N = 10;
   cout << CountORandSumEqual(N);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers whose bitwise
// OR and sum with N are equal
class GFG {

    // Function to find total 0 bit in a number
    static int CountZeroBit(int n)
    {
        int count = 0;

        while(n > 0)
        {
            if ((n & 1) != 0)
                count++;

            n >>= 1;
        }

        return count;
    }

    // Function to find Count of non-negative
    // numbers less than or equal to N, whose
    // bitwise OR and SUM with N are equal.
    static int CountORandSumEqual(int N )
    {

        // count number of zero bit in N
        int count = CountZeroBit(N);

        // power of 2 to count
        return (1 << count);
    }

    //Driver code
    public static void main (String[] args)
    {

        int N = 10;

        System.out.print(CountORandSumEqual(N));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to count numbers whose
# bitwise OR and sum with N are equal

# Function to find total 0 bit in a number
def CountZeroBit(n):

    count = 0
    while(n):

        if (not(n & 1)):
            count += 1
        n >>= 1

    return count

# Function to find Count of non-negative 
# numbers less than or equal to N, whose
# bitwise OR and SUM with N are equal.
def CountORandSumEqual(N):

    # count number of zero bit in N
    count = CountZeroBit(N)

    # power of 2 to count
    return (1 << count)

# Driver code
N = 10
print(CountORandSumEqual(N))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to count numbers whose
// bitwise OR and sum with N are equal
using System;

class GFG
{

    // Function to find total
    // 0 bit in a number
    static int CountZeroBit(int n)
    {
        int count = 0;
        while(n>0)
        {
            if (n%2!=0)
            count++;
            n >>= 1;
        }
        return count;
    }

    // Function to find Count of non-negative
    // numbers less than or equal to N, whose
    // bitwise OR and SUM with N are equal.
    static int CountORandSumEqual(int N )
    {

    // count number of zero bit in N
    int count = CountZeroBit(N);

    // power of 2 to count
    return (1 << count);
    }

    //Driver code
    public static void Main()
    {
        int N = 10;
        Console.Write(CountORandSumEqual(N));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// numbers whose bitwise
// OR and sum with N are equal

// Function to find total
// 0 bit in a number

function CountZeroBit($n)
{
    $count = 0;
    while($n)
    {
    if (!($n & 1))
        $count++;
    $n >>= 1;
    }
    return $count;
}

// Function to find Count of
// non-negative numbers less
// than or equal to N, whose
// bitwise OR and SUM with N
// are equal.

function CountORandSumEqual($N )
{
    // count number of
    // zero bit in N
    $count = CountZeroBit($N);

    // power of 2 to count
    return (1 << $count);
}

// Driver code
$N = 10;
echo CountORandSumEqual($N);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to count numbers whose
    // bitwise OR and sum with N are equal

    // Function to find total
    // 0 bit in a number
    function CountZeroBit(n)
    {
        let count = 0;
        while(n>0)
        {
            if (n%2!=0)
            count++;
            n >>= 1;
        }
        return count;
    }

    // Function to find Count of non-negative
    // numbers less than or equal to N, whose
    // bitwise OR and SUM with N are equal.
    function CountORandSumEqual(N)
    {

      // count number of zero bit in N
      let count = CountZeroBit(N);

      // power of 2 to count
      return (1 << count);
    }

    let N = 10;
      document.write(CountORandSumEqual(N));

</script>
```

**输出:**

```
 4
```

**上述解的总时间复杂度为 O(log <sub>2</sub> (N))。**
本文由 [**维兰占·库马尔·阿凯拉**](https://disqus.com/by/viranjankumarakela/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
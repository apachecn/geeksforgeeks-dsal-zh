# 在给定范围内其设定位最大的最小数

> 原文:[https://www . geeksforgeeks . org/最小-数-其集-位-最大-给定-范围/](https://www.geeksforgeeks.org/smallest-number-whose-set-bits-maximum-given-range/)

给定一个正整数“ **l** ”和“ **r** ”。找到最小的数字“ **n** ，使得 **l < = n < = r** 并且设置位数(二进制表示中的“1”的数量)的计数尽可能最大。

**示例:**

```
Input: 1 4
Output: 3
Explanation:
Binary representation from '1' to '4':
110 = 0012
210 = 0102
310 = 0112
110 = 1002
Thus number '3' has maximum set bits = 2

Input: 1 10
Output: 7
```

**简单的方法**是从‘l’遍历到‘r’，对每个‘x’(l<= n<= r)的设置位进行计数，并打印其中计数最大的数。这种方法的时间复杂度为 O(n*log(r))。

## C++

```
// C++ program to find number whose set
// bits are maximum among 'l' and 'r'
#include <bits/stdc++.h>
using namespace std;

// Returns smallest number whose set bits
// are maximum in given range.
int countMaxSetBits(int left, int right)
{
    // Initialize the maximum count and
    // final answer as 'num'
    int max_count = -1, num;
    for (int i = left; i <= right; ++i) {
        int temp = i, cnt = 0;

        // Traverse for every bit of 'i'
        // number
        while (temp) {
            if (temp & 1)
                ++cnt;
            temp >>= 1;
        }

        // If count is greater than previous
        // calculated max_count, update it
        if (cnt > max_count) {
            max_count = cnt;
            num = i;
        }
    }
    return num;
}

// Driver code
int main()
{
    int l = 1, r = 5;
    cout << countMaxSetBits(l, r) << "\n";

    l = 1, r = 10;
    cout << countMaxSetBits(l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number whose set
// bits are maximum among 'l' and 'r'
class gfg
{

// Returns smallest number whose set bits
// are maximum in given range.
static int countMaxSetBits(int left, int right)
{
    // Initialize the maximum count and
    // final answer as 'num'
    int max_count = -1, num = 0;
    for (int i = left; i <= right; ++i)
    {
        int temp = i, cnt = 0;

        // Traverse for every bit of 'i'
        // number
        while (temp > 0)
        {
            if (temp % 2 == 1)
                ++cnt;
            temp >>= 1;
        }

        // If count is greater than previous
        // calculated max_count, update it
        if (cnt > max_count)
        {
            max_count = cnt;
            num = i;
        }
    }
    return num;
}

// Driver code
public static void main(String[] args)
{
    int l = 1, r = 5;
    System.out.println(countMaxSetBits(l, r));

    l = 1; r = 10;
    System.out.print(countMaxSetBits(l, r));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code to find number whose set
# bits are maximum among 'l' and 'r'

def countMaxSetBits( left, right):
    max_count = -1
    for i in range(left, right+1):
        temp = i
        cnt = 0

        # Traverse for every bit of 'i'
        # number
        while temp:
            if temp & 1:
                cnt +=1
            temp = temp >> 1

        # If count is greater than previous
        # calculated max_count, update it
        if cnt > max_count:
            max_count = cnt
            num=i
    return num

# driver code
l = 1
r = 5
print(countMaxSetBits(l, r))
l = 1
r = 10
print(countMaxSetBits(l, r))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# program to find number whose set
// bits are maximum among 'l' and 'r'
using System;

class gfg
{

// Returns smallest number whose set bits
// are maximum in given range.
static int countMaxSetBits(int left, int right)
{
    // Initialize the maximum count and
    // final answer as 'num'
    int max_count = -1, num = 0;
    for (int i = left; i <= right; ++i)
    {
        int temp = i, cnt = 0;

        // Traverse for every bit of 'i'
        // number
        while (temp > 0)
        {
            if (temp % 2 == 1)
                ++cnt;
            temp >>= 1;
        }

        // If count is greater than previous
        // calculated max_count, update it
        if (cnt > max_count)
        {
            max_count = cnt;
            num = i;
        }
    }
    return num;
}

// Driver code
public static void Main(String[] args)
{
    int l = 1, r = 5;
    Console.WriteLine(countMaxSetBits(l, r));

    l = 1; r = 10;
    Console.Write(countMaxSetBits(l, r));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// whose set bits are maximum
// among 'l' and 'r'

// Returns smallest number
// whose set bits are maximum
// in given range.

function countMaxSetBits($left, $right)
{
    // Initialize the maximum
    // count and final answer
    // as 'num'
    $max_count = -1; $num;
    for ($i = $left; $i <= $right; ++$i)
    {
        $temp = $i; $cnt = 0;

        // Traverse for every
        // bit of 'i' number
        while ($temp)
        {
            if ($temp & 1)
                ++$cnt;
            $temp >>= 1;
        }

        // If count is greater than
        // previous calculated
        // max_count, update it
        if ($cnt > $max_count)
        {
            $max_count = $cnt;
            $num = $i;
        }
    }
    return $num;
}

// Driver code
$l = 1; $r = 5;
echo countMaxSetBits($l, $r), "\n";

$l = 1; $r = 10;
echo countMaxSetBits($l, $r);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find number whose set
// bits are maximum among 'l' and 'r'

// Returns smallest number whose set bits
// are maximum in given range.
function countMaxSetBits(left, right)
{

    // Initialize the maximum count and
    // final answer as 'num'
    let max_count = -1, num = 0;

    for(let i = left; i <= right; ++i)
    {
        let temp = i, cnt = 0;

        // Traverse for every bit of 'i'
        // number
        while (temp > 0)
        {
            if (temp % 2 == 1)
                ++cnt;

            temp >>= 1;
        }

        // If count is greater than previous
        // calculated max_count, update it
        if (cnt > max_count)
        {
            max_count = cnt;
            num = i;
        }
    }
    return num;
}

// Driver Code
let l = 1, r = 5;
document.write(countMaxSetBits(l, r) + "<br/>");

l = 1; r = 10;
document.write(countMaxSetBits(l, r));

// This code is contributed by code_hunt

</script>
```

**输出:**

```
3
7
```

**有效的方法**是使用位操作。不是对从“l”到“r”的每个数字进行迭代，而是仅在更新所需的数字(“num”)后进行迭代，即取具有连续数字的数字的按位“或”。例如，

```
Let l = 2, and r = 10
1\. num = 2
2\. x = num OR (num + 1)
       = 2 | 3 = 010 | 011 = 011
   num = 3(011)
3\. x = 3 | 4 = 011 | 100 = 111
   num = 7(111)
4\. x = 7 | 8 = 0111 | 1000 = 1111
   Since 15(11112) is greater than
   10, thus stop traversing for next number.
5\. Final answer = 7 
```

## C++

```
// C++ program to find number whose set
// bits are maximum among 'l' and 'r'
#include <bits/stdc++.h>
using namespace std;

// Returns smallest number whose set bits
// are maximum in given range.
int countMaxSetBits(int left, int right)
{
    while ((left | (left + 1)) <= right)
        left |= left + 1;

    return left;
}

// Driver code
int main()
{
    int l = 1, r = 5;
    cout << countMaxSetBits(l, r) << "\n";

    l = 1, r = 10;
    cout << countMaxSetBits(l, r) ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number
// whose set bits are maximum
// among 'l' and 'r'
import java.io.*;

class GFG
{

    // Returns smallest number
    // whose set bits are
    // maximum in given range.
    static int countMaxSetBits(int left,
                               int right)
    {
    while ((left | (left + 1)) <= right)
        left |= left + 1;

    return left;
    }

// Driver code
public static void main (String[] args)
{
    int l = 1;
    int r = 5;
    System.out.println(countMaxSetBits(l, r));

    l = 1;
    r = 10;
    System.out.println(countMaxSetBits(l, r));
}
}

// This code is contributed by @ajit
```

## 蟒蛇 3

```
# Python code to find number whose set
# bits are maximum among 'l' and 'r'

def countMaxSetBits( left, right):

    while(left | (left+1)) <= right:
        left |= left+1
    return left

# driver code
l = 1
r = 5
print(countMaxSetBits(l, r))
l = 1
r = 10
print(countMaxSetBits(l, r))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# program to find number
// whose set bits are maximum
// among 'l' and 'r'
using System;

class GFG
{

    // Returns smallest number
    // whose set bits are
    // maximum in given range.
    static int countMaxSetBits(int left,
                               int right)
    {
    while ((left | (left + 1)) <= right)
        left |= left + 1;

    return left;
    }

// Driver code
static public void Main ()
{
    int l = 1;
    int r = 5;
    Console.WriteLine(countMaxSetBits(l, r));

    l = 1;
    r = 10;
    Console.WriteLine(countMaxSetBits(l, r));
}
}

// This code is contributed by @ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// whose set bits are maximum
// among 'l' and 'r'

// Returns smallest number
// whose set bits are
// maximum in given range.
function countMaxSetBits($left,
                         $right)
{
    while (($left | ($left + 1)) <= $right)
        $left |= $left + 1;

    return $left;
}

// Driver code
$l = 1 ; $r = 5;
echo countMaxSetBits($l, $r) , "\n";

$l = 1; $r = 10;
echo countMaxSetBits($l, $r) ;

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to find number whose set
// bits are maximum among 'l' and 'r'

// Returns smallest number whose set bits
// are maximum in given range.
function countMaxSetBits( left, right)
{
    while ((left | (left + 1)) <= right)
        left |= left + 1;

    return left;
}

// driver code

    let l = 1, r = 5;
    document.write(countMaxSetBits(l, r) + "</br>");

    l = 1, r = 10;
    document.write(countMaxSetBits(l, r)) ;

</script>
```

**输出:**

```
3
7
```

**时间复杂度:** O(log(n))
**辅助空间:** O(1)
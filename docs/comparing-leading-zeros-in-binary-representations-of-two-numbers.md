# 比较两个数字的二进制表示中的前导零

> 原文:[https://www . geeksforgeeks . org/比较二进制数字的前导零表示/](https://www.geeksforgeeks.org/comparing-leading-zeros-in-binary-representations-of-two-numbers/)

给定两个整数 x 和 y。使用按位运算比较并打印哪一个有更多的前导零。如果两个数字的前导零数量相同，则打印“相等”。
注意:-前导零是数字二进制记数法中第一个非零数字之前的任何 0 数字。
**例:**

```
Input : 10, 16
Output :10
Explanation: If we represent the no.s using 8 bit only then 
Binary(10) = 00001010
Binary(16) = 00010000
Clearly, 10 has 4 leading zeros and 16 has 3 leading zeros

Input : 10, 12
Output : Equal
Binary(10) = 00001010
Binary(12) = 00001100
Both have equal no. of leading zeros.
```

**解决方案 1** :天真的方法是先找到数字的二进制表示，然后计算前导零的个数。
**解 2:** 找到比给定数字小的[最大二次幂，比较这些二次幂决定答案。
**解决方案 3:** 一种有效的方法是按位异或和与运算符。](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/) 

> 情况 1:如果两者都有相同数量的前导零，那么(x^y) <= (x & y) because same number of leading 0s would cause a 1 at higher position in x & y.
> 情况 2:如果我们对 y 进行求反并与 x 按位“与”,当 y 有更多数量的前导 0 时，我们会在比 y 更高的位置得到 1。
> 情况 3:否则 x 有更多的前导零

## C++

```
// CPP program to find the number with more
// leading zeroes.
#include <bits/stdc++.h>
using namespace std;

// Function to compare the no. of leading zeros
void LeadingZeros(int x, int y)
{
    // if both have same no. of leading zeros
    if ((x ^ y) <= (x & y))
        cout << "\nEqual";

    // if y has more leading zeros
    else if ((x & (~y)) > y)
        cout << y;

    else
        cout << x;
}

// Main Function
int main()
{
    int x = 10, y = 16;
    LeadingZeros(x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// with more leading zeroes.
class GFG
{
// Function to compare the no.
// of leading zeros
static void LeadingZeros(int x, int y)
{
    // if both have same no. of
    // leading zeros
    if ((x ^ y) <= (x & y))
        System.out.print("\nEqual");

    // if y has more leading zeros
    else if ((x & (~y)) > y)
        System.out.print(y);

    else
        System.out.print(x);
}

// Driver Code
public static void main (String[] args)
{
    int x = 10, y = 16;
    LeadingZeros(x, y);
}
}

// This code is contributed by Smitha
```

## 蟒蛇 3

```
# Python 3 program to find the number
# with more leading zeroes.

# Function to compare the no. of
# leading zeros
def LeadingZeros(x, y):

    # if both have same no. of
    # leading zeros
    if ((x ^ y) <= (x & y)):
        print("Equal")

    # if y has more leading zeros
    elif ((x & (~y)) > y) :
        print(y)

    else:
        print(x)

# Driver Code
if __name__ == '__main__':
    x = 10
    y = 16
    LeadingZeros(x, y)

# This code is contributed
# by Surendra_Gangwar
```

## C#

```
// C# program to find the number
// with more leading zeroes.
using System;

class GFG
{
// Function to compare the no.
// of leading zeros
static void LeadingZeros(int x, int y)
{
    // if both have same no. of
    // leading zeros
    if ((x ^ y) <= (x & y))
        Console.WriteLine("\nEqual");

    // if y has more leading zeros
    else if ((x & (~y)) > y)
        Console.WriteLine(y);

    else
        Console.WriteLine(x);
}

// Driver Code
static public void Main ()
{
    int x = 10, y = 16;
    LeadingZeros(x, y);
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number
// with more leading zeroes.

// Function to compare the no.
// of leading zeros
function LeadingZeros($x, $y)
{
    // if both have same no. of
    // leading zeros
    if (($x ^ $y) <= ($x & $y))
        echo "\nEqual";

    // if y has more leading zeros
    else if (($x & (~$y)) > $y)
        echo $y;

    else
        echo $x;
}

// Driver Code
$x = 10;
$y = 16;
LeadingZeros($x, $y);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find the number with more
// leading zeroes.

// Function to compare the no. of leading zeros
function LeadingZeros(x, y)
{
    // if both have same no. of leading zeros
    if ((x ^ y) <= (x & y))
        document.write("<br>Equal");

    // if y has more leading zeros
    else if ((x & (~y)) > y)
        document.write(y);

    else
        document.write(x);
}

// Main Function
    let x = 10, y = 16;
    LeadingZeros(x, y);

</script>
```

**Output:** 

```
10
```

**时间复杂度:**O(1)
T3】空间复杂度: O(1)
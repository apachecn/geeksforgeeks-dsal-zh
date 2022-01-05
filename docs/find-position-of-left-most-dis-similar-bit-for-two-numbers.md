# 找到两个数字最左边不相似位的位置

> 原文:[https://www . geeksforgeeks . org/find-最左侧位置-两个数字的最不相似位/](https://www.geeksforgeeks.org/find-position-of-left-most-dis-similar-bit-for-two-numbers/)

给定两个数字 **n1** 和 **n2** 。任务是从左边找到两个数的二进制表示中第一个不匹配位的位置。在使两个数字的二进制表示长度相同后，我们需要找到这个位。我们通过在较小的数字中附加 0 来使长度相同。

**注**:

*   **例如** : n1 = 1，n2 = 7。n1 和 n4 的按位表示将分别为“1”和“111”。将两个零附加到 n1，使其为 100。
*   如果 n1 等于 n2，则打印零。

**示例**:

```
Input: n1 = 12, n2 = 34
Output: 2
Binary representation of 12 is 1100 and of 34 is 100010\. 
First make both representations of the 
same length by appending 0s. 
So the first representation now becomes 11000\. 
The second bit is the different bit.

Input: n1 = 1, n2 = 2
Output: 2
```

为了找到两个数的位表示中最左边的不相似位的位置，可以进行逐位比较，也可以使用导出的公式。虽然两者的时间复杂度相同。
为了找到最左边最不相似的位，首先通过将较小的位乘以幂(2，位长差)来均衡两个数的位长。使位长相等后，取两个数的异或。现在，最左边的不相似位清楚地反映在异或值中。从给定数的位长度中减去异或值的位长度加上 1，就可以得出最左边不相似位的位置。

**算法:**

1.  找出 n1 和 n2 的位长。
2.  通过将零放在较小数字右边来均衡两个数字的比特长度(与将较小的数字乘以幂(2，比特长度差)相同)
3.  对两个数进行异或运算
4.  任何数字的位长与异或值的位长之差需要答案加 1

下面是上述方法的实现:

## C++

```
// C++ program to find the leftmost
// position of first dis-similar bit
#include <bits/stdc++.h>
using namespace std;

// Function to find first dis-similar bit
int bitPos(int n1, int n2)
{
    // return zero for equal number
    if (n1 == n2)
        return 0;

    /** find the 1st dis-similar bit **/
    // count bit length of n1 and n2
    int bitCount1 = floor(log2(n1)) + 1;
    int bitCount2 = floor(log2(n2)) + 1;

    // find bit difference and maxBit
    int bitDiff = abs(bitCount1 - bitCount2);
    int maxBitCount = max(bitCount1, bitCount2);

    if (bitCount1 > bitCount2) {
        n2 = n2 * pow(2, bitDiff);
    }
    else {
        n1 = n1 * pow(2, bitDiff);
    }

    int xorValue = n1 ^ n2;
    int bitCountXorValue = floor(log2(xorValue)) + 1;
    int disSimilarBitPosition = maxBitCount -
                                  bitCountXorValue + 1;

    return disSimilarBitPosition;
}

// Driver program
int main()
{
    int n1 = 53, n2 = 55;
    cout << bitPos(n1, n2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the leftmost position of
// first dis-similar bit

import java.io.*;

class GFG {

// Function to find first dis-similar bit
static int bitPos(int n1, int n2)
{
    // return zero for equal number
    if (n1 == n2)
        return 0;

    /** find the 1st dis-similar bit **/
    // count bit length of n1 and n2
    int bitCount1 = (int)Math.floor(Math.log(n1) /
                                    Math.log(2)) + 1;
    int bitCount2 = (int)Math.floor(Math.log(n2) /
                                    Math.log(2)) + 1;

    // find bit difference and maxBit
    int bitDiff = Math.abs(bitCount1 - bitCount2);
    int maxBitCount = Math.max(bitCount1,
                            bitCount2);

    if (bitCount1 > bitCount2)
    {
        n2 = n2 * (int)Math.pow(2, bitDiff);
    }
    else
    {
        n1 = n1 * (int)Math.pow(2, bitDiff);
    }

    int xorValue = n1 ^ n2;
    int bitCountXorValue = (int)Math.floor(Math.log(xorValue) /
                                        Math.log(2)) + 1;
    int disSimilarBitPosition = maxBitCount -
                                bitCountXorValue + 1;

    return disSimilarBitPosition;
}

// Driver Code
    public static void main (String[] args) {

        int n1 = 53, n2 = 55;
        System.out.println(bitPos(n1, n2));
}
}
// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 program to Find the leftmost
# position of first dis-similar bit

# from math lib import floor()
# and log2()
from math import floor, log2

# Function to find first
# dis-similar bit
def bitPos(n1, n2) :

    # return zero for equal number
    if n1 == n2 :
        return 0

    # find the 1st dis-similar bit
    # count bit length of n1 and n
    bitCount1 = floor(log2(n1)) + 1
    bitCount2 = floor(log2(n2)) + 1

    # find bit difference and maxBit
    bitDiff = abs(bitCount1 - bitCount2)
    maxBitCount = max(bitCount1, bitCount2)

    if (bitCount1 > bitCount2) :

        n2 *= pow(2, bitDiff)

    else :

        n1 *= pow(2, bitDiff)

    xorValue = n1 ^ n2
    bitCountXorValue = floor(log2(xorValue)) + 1
    disSimilarBitPosition = (maxBitCount -
                             bitCountXorValue + 1)

    return disSimilarBitPosition

# Driver code
if __name__ == "__main__" :

    n1, n2 = 53, 55
    print(bitPos(n1, n2))

# This code is contributed by Ryuga
```

## C#

```
// C# to find the leftmost position of
// first dis-similar bit
using System;

class GFG
{

// Function to find first dis-similar bit
static int bitPos(int n1, int n2)
{
    // return zero for equal number
    if (n1 == n2)
        return 0;

    /** find the 1st dis-similar bit **/
    // count bit length of n1 and n2
    int bitCount1 = (int)Math.Floor(Math.Log(n1) /
                                    Math.Log(2)) + 1;
    int bitCount2 = (int)Math.Floor(Math.Log(n2) /
                                    Math.Log(2)) + 1;

    // find bit difference and maxBit
    int bitDiff = Math.Abs(bitCount1 - bitCount2);
    int maxBitCount = Math.Max(bitCount1,
                               bitCount2);

    if (bitCount1 > bitCount2)
    {
        n2 = n2 * (int)Math.Pow(2, bitDiff);
    }
    else
    {
        n1 = n1 * (int)Math.Pow(2, bitDiff);
    }

    int xorValue = n1 ^ n2;
    int bitCountXorValue = (int)Math.Floor(Math.Log(xorValue) /
                                           Math.Log(2)) + 1;
    int disSimilarBitPosition = maxBitCount -
                                bitCountXorValue + 1;

    return disSimilarBitPosition;
}

// Driver Code
public static void Main()
{
    int n1 = 53, n2 = 55;
    Console.Write(bitPos(n1, n2));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the leftmost
// position of first dis-similar bit

// Function to find first dis-similar bit
function bitPos($n1, $n2)
{
    // return zero for equal number
    if ($n1 == $n2)
        return 0;

    /** find the 1st dis-similar bit **/
    // count bit length of n1 and n2
    $bitCount1 = floor(log($n1, 2)) + 1;
    $bitCount2 = floor(log($n2, 2)) + 1;

    // find bit difference and maxBit
    $bitDiff = abs($bitCount1 - $bitCount2);
    $maxBitCount = max($bitCount1, $bitCount2);

    if ($bitCount1 > $bitCount2)
    {
        $n2 = $n2 * pow(2, $bitDiff);
    }
    else {
        $n1 = $n1 * pow(2, $bitDiff);
    }

    $xorValue = $n1 ^ $n2;
    $bitCountXorValue = floor(log($xorValue, 2)) + 1;
    $disSimilarBitPosition = $maxBitCount -
                             $bitCountXorValue + 1;

    return $disSimilarBitPosition;
}

// Driver Code
$n1 = 53;
$n2 = 55;
echo bitPos($n1, $n2);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find the leftmost
// position of first dis-similar bit

// Function to find first dis-similar bit
function bitPos(n1, n2)
{

    // Return zero for equal number
    if (n1 == n2)
        return 0;

    // Find the 1st dis-similar bit
    // count bit length of n1 and n2
    let bitCount1 = Math.floor(Math.log2(n1)) + 1;
    let bitCount2 = Math.floor(Math.log2(n2)) + 1;

    // find bit difference and maxBit
    let bitDiff = Math.abs(bitCount1 - bitCount2);
    let maxBitCount = Math.max(bitCount1, bitCount2);

    if (bitCount1 > bitCount2)
    {
        n2 = n2 * Math.pow(2, bitDiff);
    }
    else
    {
        n1 = n1 * Math.pow(2, bitDiff);
    }

    let xorValue = n1 ^ n2;
    let bitCountXorValue = Math.floor(
                           Math.log2(xorValue)) + 1;
    let disSimilarBitPosition = maxBitCount -
                                bitCountXorValue + 1;

    return disSimilarBitPosition;
}

// Driver code
let n1 = 53, n2 = 55;

document.write(bitPos(n1, n2));

// This code is contributed by Manoj.

</script>
```

**Output:** 

```
5
```
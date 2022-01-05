# 范围的逐位或(或)|

> 原文:[https://www.geeksforgeeks.org/bitwise-or-or-of-a-range/](https://www.geeksforgeeks.org/bitwise-or-or-of-a-range/)

给定两个整数 L 和 R。确定范围[L，R](包括两者)内所有整数的按位或。

**示例**:

```
Input: L = 3, R = 8
Output: 15
3 | 4 | 5 | 6 | 7 | 8 = 15

Input: L = 12, R = 18
Output: 31
12 | 13 | 14 | 15 | 16 | 17 | 18 = 31 
```

一种简单的方法是遍历 L 和 R 之间的所有整数，并对所有数字进行按位或运算。

一种有效的方法是遵循以下步骤:

1.  找出最高有效位在两个数字中的位置
2.  如果两个 MSB 的位置不同，将最大值(MSB1，MSB2)的所有位(包括这个不同的位)设置为 oth 位，即在答案中为所有 0 ≤ i ≤ max(MSB1，MSB2)加上值(1 << i)。
3.  如果两个 msb 的位置相同，那么
    *   将该位设置为对应于 MSB 或在答案中添加值(1 << MSB)。
    *   从两个数字(L 和 R)中减去值(1 << MSB)。
    *   重复步骤 1、2 和 3。

下面给出的是 L = 18，R = 21 时上述算法的工作情况。

```
L = 18, R = 21
The result is initially 0.
The position of Most Significant Bit in L = 4
Position of Most Significant Bit in R = 4
Since positions are same, add value (1 << 4) i.e. 16 to the result.

Subtract (1 << 4) from L, L becomes 2.
Subtract (1 << 4) from R, R becomes 5.

Now, Position of MSB in L is 1
Position of MSB in R is 2
Since positions are different all value (1 << i) for all 
0 ≤ i ≤ max(MSB1, MSB2)
i.e. Add ((1 << 2) + (1 << 1) + (1 << 0)) = 7
Hence, final result is 16 + 7 = 23.
```

下面是上述方法的实现。

## C++

```
// C++ Program to find the bitwise
// OR of all the integers in range L-R
#include <bits/stdc++.h>
using namespace std;

// Returns the Most Significant Bit
// Position (MSB)
int MSBPosition(long long int N)
{
    int msb_p = -1;
    while (N) {
        N = N >> 1;
        msb_p++;
    }
    return msb_p;
}

// Returns the Bitwise OR of all
// integers between L and R
long long int findBitwiseOR(long long int L,
                            long long int R)
{
    long long int res = 0;

    // Find the MSB position in L
    int msb_p1 = MSBPosition(L);

    // Find the MSB position in R
    int msb_p2 = MSBPosition(R);

    while (msb_p1 == msb_p2) {
        long long int res_val = (1 << msb_p1);

        // Add this value until msb_p1 and
        // msb_p2 are same;
        res += res_val;

        L -= res_val;
        R -= res_val;

        // Calculate msb_p1 and msb_p2
        msb_p1 = MSBPosition(L);
        msb_p2 = MSBPosition(R);
    }
    // Find the max of msb_p1 and msb_p2
    msb_p1 = max(msb_p1, msb_p2);

    // Set all the bits from msb_p1 upto
    // 0th bit in the result
    for (int i = msb_p1; i >= 0; i--) {
        long long int res_val = (1 << i);
        res += res_val;
    }
    return res;
}

// Driver Code
int main()
{
    int L = 12, R = 18;
    cout << findBitwiseOR(L, R) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find
// the bitwise OR of all
// the integers in range L-R
import java.io.*;

class GFG
{

// Returns the Most Significant
// Bit Position (MSB)
static int MSBPosition(long N)
{
    int msb_p = -1;
    while (N > 0)
    {
        N = N >> 1;
        msb_p++;
    }
    return msb_p;
}

// Returns the Bitwise
// OR of all integers
// between L and R
static long findBitwiseOR(long L,
                          long R)
{
    long res = 0;

    // Find the MSB
    // position in L
    int msb_p1 = MSBPosition(L);

    // Find the MSB
    // position in R
    int msb_p2 = MSBPosition(R);

    while (msb_p1 == msb_p2)
    {
        long res_val = (1 << msb_p1);

        // Add this value until
        // msb_p1 and msb_p2 are same;
        res += res_val;

        L -= res_val;
        R -= res_val;

        // Calculate msb_p1
        // and msb_p2
        msb_p1 = MSBPosition(L);
        msb_p2 = MSBPosition(R);
    }

    // Find the max of
    // msb_p1 and msb_p2
    msb_p1 = Math.max(msb_p1,
                      msb_p2);

    // Set all the bits
    // from msb_p1 upto
    // 0th bit in the result
    for (int i = msb_p1; i >= 0; i--)
    {
        long res_val = (1 << i);
        res += res_val;
    }
    return res;
}

// Driver Code
public static void main (String[] args)
{
    int L = 12, R = 18;
    System.out.println(findBitwiseOR(L, R));
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 Program to find the bitwise
# OR of all the integers in range L-R

# Returns the Most Significant Bit
# Position (MSB)
def MSBPosition(N) :

    msb_p = -1
    while (N) :
        N = N >> 1
        msb_p += 1

    return msb_p

# Returns the Bitwise OR of all
# integers between L and R
def findBitwiseOR(L, R) :

    res = 0

    # Find the MSB position in L
    msb_p1 = MSBPosition(L)

    # Find the MSB position in R
    msb_p2 = MSBPosition(R)

    while (msb_p1 == msb_p2) :
        res_val = (1 << msb_p1)

        # Add this value until msb_p1 and
        # msb_p2 are same;
        res += res_val

        L -= res_val
        R -= res_val

        # Calculate msb_p1 and msb_p2
        msb_p1 = MSBPosition(L)
        msb_p2 = MSBPosition(R)

    # Find the max of msb_p1 and msb_p2
    msb_p1 = max(msb_p1, msb_p2)

    # Set all the bits from msb_p1 upto
    # 0th bit in the result
    for i in range(msb_p1, -1, -1) :
        res_val = (1 << i)
        res += res_val

    return res

# Driver Code
if __name__ == "__main__" :

    L , R= 12 ,18
    print(findBitwiseOR(L, R))

# This code is contributed by Ryuga
```

## C#

```
// C# Program to find
// the bitwise OR of all
// the integers in range L-R
using System;

class GFG
{

// Returns the Most Significant
// Bit Position (MSB)
static int MSBPosition(long N)
{
    int msb_p = -1;
    while (N > 0)
    {
        N = N >> 1;
        msb_p++;
    }
    return msb_p;
}

// Returns the Bitwise
// OR of all integers
// between L and R
static long findBitwiseOR(long L,
                          long R)
{
    long res = 0;

    // Find the MSB
    // position in L
    int msb_p1 = MSBPosition(L);

    // Find the MSB
    // position in R
    int msb_p2 = MSBPosition(R);

    while (msb_p1 == msb_p2)
    {
        long res_val = (1 << msb_p1);

        // Add this value until
        // msb_p1 and msb_p2 are same;
        res += res_val;

        L -= res_val;
        R -= res_val;

        // Calculate msb_p1
        // and msb_p2
        msb_p1 = MSBPosition(L);
        msb_p2 = MSBPosition(R);
    }

    // Find the max of
    // msb_p1 and msb_p2
    msb_p1 = Math.Max(msb_p1,
                      msb_p2);

    // Set all the bits
    // from msb_p1 upto
    // 0th bit in the result
    for (int i = msb_p1; i >= 0; i--)
    {
        long res_val = (1 << i);
        res += res_val;
    }
    return res;
}

// Driver Code
public static void Main ()
{
    int L = 12, R = 18;
    Console.WriteLine(findBitwiseOR(L, R));
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// bitwise OR of all the
// integers in range L-R

// Returns the Most Significant
// Bit Position (MSB)
function MSBPosition($N)
{
    $msb_p = -1;
    while ($N)
    {
        $N = $N >> 1;
        $msb_p++;
    }
    return $msb_p;
}

// Returns the Bitwise
// OR of all integers
// between L and R
function findBitwiseOR($L, $R)
{
    $res = 0;

    // Find the MSB
    // position in L
    $msb_p1 = MSBPosition($L);

    // Find the MSB
    // position in R
    $msb_p2 = MSBPosition($R);

    while ($msb_p1 == $msb_p2)
    {
        $res_val = (1 << $msb_p1);

        // Add this value until
        // msb_p1 and msb_p2 are same;
        $res += $res_val;

        $L -= $res_val;
        $R -= $res_val;

        // Calculate msb_p1
        // and msb_p2
        $msb_p1 = MSBPosition($L);
        $msb_p2 = MSBPosition($R);
    }

    // Find the max of
    // msb_p1 and msb_p2
    $msb_p1 = max($msb_p1,
                  $msb_p2);

    // Set all the bits from msb_p1
    // upto 0th bit in the result
    for ($i = $msb_p1; $i >= 0; $i--)
    {
        $res_val = (1 << $i);
        $res += $res_val;
    }
    return $res;
}

// Driver Code
$L = 12; $R = 18;
echo findBitwiseOR($L, $R);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript Program to find
    // the bitwise OR of all
    // the integers in range L-R

    // Returns the Most Significant
    // Bit Position (MSB)
    function MSBPosition(N)
    {
        let msb_p = -1;
        while (N > 0)
        {
            N = N >> 1;
            msb_p++;
        }
        return msb_p;
    }

    // Returns the Bitwise
    // OR of all integers
    // between L and R
    function findBitwiseOR(L, R)
    {
        let res = 0;

        // Find the MSB
        // position in L
        let msb_p1 = MSBPosition(L);

        // Find the MSB
        // position in R
        let msb_p2 = MSBPosition(R);

        while (msb_p1 == msb_p2)
        {
            let res_val = (1 << msb_p1);

            // Add this value until
            // msb_p1 and msb_p2 are same;
            res += res_val;

            L -= res_val;
            R -= res_val;

            // Calculate msb_p1
            // and msb_p2
            msb_p1 = MSBPosition(L);
            msb_p2 = MSBPosition(R);
        }

        // Find the max of
        // msb_p1 and msb_p2
        msb_p1 = Math.max(msb_p1,
                          msb_p2);

        // Set all the bits
        // from msb_p1 upto
        // 0th bit in the result
        for (let i = msb_p1; i >= 0; i--)
        {
            let res_val = (1 << i);
            res += res_val;
        }
        return res;
    }

    let L = 12, R = 18;
    document.write(findBitwiseOR(L, R));

</script>
```

**Output:** 

```
31
```

**时间复杂度:** O(N)，其中 N 为最高有效位。
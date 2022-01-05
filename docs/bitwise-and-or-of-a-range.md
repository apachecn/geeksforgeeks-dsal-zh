# 范围

的逐位与(或&

> 原文:[https://www.geeksforgeeks.org/bitwise-and-or-of-a-range/](https://www.geeksforgeeks.org/bitwise-and-or-of-a-range/)

给定两个非负长整数，x 和 y 给定 x <= y, the task is to find bit-wise and of all integers from x and y, i.e., we need to compute value of x & (x+1) & … & (y-1) & y.7 
**示例:**

```
Input  : x = 12, y = 15
Output : 12 
12 & 13 & 14 & 15 = 12 

Input  : x = 10, y = 20
Output : 0 
```

一个**简单的解决方案**是遍历从 x 到 y 的所有数字，并对范围内的所有数字进行逐位遍历。
一个**高效的解决方案**是遵循以下步骤。
1)找出两个数字中最高有效位的位置。
2)如果 MSB 的位置不同，则结果为 0。
3)如果位置相同。让位置为 msb _ p .
……)a)我们在结果上加 2 <sup>msb_p</sup> 。
……(b)我们从 x 和 y 中减去 2 <sup>msb_p</sup> ，
……(c)对 x 和 y 的新值重复步骤 1、2 和 3。

```
Example 1 :
x = 10, y = 20
Result is initially 0.
Position of MSB in x = 3
Position of MSB in y = 4
Since positions are different, return result.

Example 2 :
x = 17, y = 19
Result is initially 0.
Position of MSB in x = 4
Position of MSB in y = 4
Since positions are same, we compute 24.

We add 24 to result. 
Result becomes 16.

We subtract this value from x and y.
New value of x  = x - 24  = 17 - 16 = 1
New value of y  = y - 24  = 19 - 16 = 3

Position of MSB in new x = 1
Position of MSB in new y = 2
Since positions are different, we return result.
```

## C++

```
// An efficient C++ program to find bit-wise & of all
// numbers from x to y.
#include<bits/stdc++.h>
using namespace std;
typedef long long int ll;

// Find position of MSB in n. For example if n = 17,
// then position of MSB is 4\. If n = 7, value of MSB
// is 3
int msbPos(ll n)
{
    int msb_p = -1;
    while (n)
    {
        n = n>>1;
        msb_p++;
    }
    return msb_p;
}

// Function to find Bit-wise & of all numbers from x
// to y.
ll andOperator(ll x, ll y)
{
    ll res = 0; // Initialize result

    while (x && y)
    {
        // Find positions of MSB in x and y
        int msb_p1 = msbPos(x);
        int msb_p2 = msbPos(y);

        // If positions are not same, return
        if (msb_p1 != msb_p2)
            break;

        // Add 2^msb_p1 to result
        ll msb_val =  (1 << msb_p1);
        res = res + msb_val;

        // subtract 2^msb_p1 from x and y.
        x = x - msb_val;
        y = y - msb_val;
    }

    return res;
}

// Driver code
int main()
{
    ll x = 10, y = 15;
    cout << andOperator(x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient Java program to find bit-wise
// & of all numbers from x to y.
class GFG {

    // Find position of MSB in n. For example
    // if n = 17, then position of MSB is 4.
    // If n = 7, value of MSB is 3
    static int msbPos(long n)
    {

        int msb_p = -1;
        while (n > 0) {
            n = n >> 1;
            msb_p++;
        }

        return msb_p;
    }

    // Function to find Bit-wise & of all
    // numbers from x to y.
    static long andOperator(long x, long y)
    {

        long res = 0; // Initialize result

        while (x > 0 && y > 0) {

            // Find positions of MSB in x and y
            int msb_p1 = msbPos(x);
            int msb_p2 = msbPos(y);

            // If positions are not same, return
            if (msb_p1 != msb_p2)
                break;

            // Add 2^msb_p1 to result
            long msb_val = (1 << msb_p1);
            res = res + msb_val;

            // subtract 2^msb_p1 from x and y.
            x = x - msb_val;
            y = y - msb_val;
        }

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {

        long x = 10, y = 15;

        System.out.print(andOperator(x, y));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# An efficient Python program to find
# bit-wise & of all numbers from x to y.

# Find position of MSB in n. For example
# if n = 17, then position of MSB is 4.
# If n = 7, value of MSB is 3
def msbPos(n):

    msb_p = -1
    while (n > 0):

        n = n >> 1
        msb_p += 1

    return msb_p

# Function to find Bit-wise & of
# all numbers from x to y.
def andOperator(x, y):

    res = 0 # Initialize result

    while (x > 0 and y > 0):

        # Find positions of MSB in x and y
        msb_p1 = msbPos(x)
        msb_p2 = msbPos(y)

        # If positions are not same, return
        if (msb_p1 != msb_p2):
            break

        # Add 2^msb_p1 to result
        msb_val = (1 << msb_p1)
        res = res + msb_val

        # subtract 2^msb_p1 from x and y.
        x = x - msb_val
        y = y - msb_val

    return res

# Driver code
x, y = 10, 15
print(andOperator(x, y))

# This code is contributed by Anant Agarwal.
```

## C#

```
// An efficient C# program to find bit-wise & of all
// numbers from x to y.
using System;

class GFG
{
    // Find position of MSB in n.
    // For example if n = 17,
    // then position of MSB is 4.
    // If n = 7, value of MSB
    // is 3
    static int msbPos(long n)
    {
        int msb_p = -1;
        while (n > 0)
        {
            n = n >> 1;
            msb_p++;
        }
        return msb_p;
    }

    // Function to find Bit-wise
    // & of all numbers from x
    // to y.
    static long andOperator(long x, long y)
    {
        // Initialize result
        long res = 0;

        while (x > 0 && y > 0)
        {
            // Find positions of MSB in x and y
            int msb_p1 = msbPos(x);
            int msb_p2 = msbPos(y);

            // If positions are not same, return
            if (msb_p1 != msb_p2)
                break;

            // Add 2^msb_p1 to result
            long msb_val = (1 << msb_p1);
            res = res + msb_val;

            // subtract 2^msb_p1 from x and y.
            x = x - msb_val;
            y = y - msb_val;
        }

        return res;
    }

    // Driver code
    public static void Main()
    {
        long x = 10, y = 15;
        Console.WriteLine(andOperator(x, y));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An efficient C++ program
// to find bit-wise & of all
// numbers from x to y.

// Find position of MSB in n.
// For example if n = 17, then
// position of MSB is 4\. If n = 7,
// value of MSB is 3
function msbPos($n)
{
    $msb_p = -1;
    while ($n > 0)
    {
        $n = $n >> 1;
        $msb_p++;
    }
    return $msb_p;
}

// Function to find Bit-wise &
// of all numbers from x to y.
function andOperator($x, $y)
{
    $res = 0; // Initialize result

    while ($x > 0 && $y > 0)
    {
        // Find positions of
        // MSB in x and y
        $msb_p1 = msbPos($x);
        $msb_p2 = msbPos($y);

        // If positions are not
        // same, return
        if ($msb_p1 != $msb_p2)
            break;

        // Add 2^msb_p1 to result
        $msb_val = (1 << $msb_p1);
        $res = $res + $msb_val;

        // subtract 2^msb_p1
        // from x and y.
        $x = $x - $msb_val;
        $y = $y - $msb_val;
    }

    return $res;
}

// Driver code
$x = 10;
$y = 15;
echo andOperator($x, $y);

// This code is contributed
// by ihritik
?>
```

## java 描述语言

```
<script>
    // Javascript program to find bit-wise
// & of all numbers from x to y.

    // Find position of MSB in n. For example
    // if n = 17, then position of MSB is 4.
    // If n = 7, value of MSB is 3
    function msbPos(n)
    {

        let msb_p = -1;
        while (n > 0) {
            n = n >> 1;
            msb_p++;
        }

        return msb_p;
    }

    // Function to find Bit-wise & of all
    // numbers from x to y.
    function andOperator(x, y)
    {

        let res = 0; // Initialize result

        while (x > 0 && y > 0) {

            // Find positions of MSB in x and y
            let msb_p1 = msbPos(x);
            let msb_p2 = msbPos(y);

            // If positions are not same, return
            if (msb_p1 != msb_p2)
                break;

            // Add 2^msb_p1 to result
            let msb_val = (1 << msb_p1);
            res = res + msb_val;

            // subtract 2^msb_p1 from x and y.
            x = x - msb_val;
            y = y - msb_val;
        }

        return res;
    }

// Driver Code
        let x = 10, y = 15;

        document.write(andOperator(x, y));

// This code is contributed by avijitmondal1998.
</script>
```

**Output**

```
8
```

**更高效的解决方案**

1.  翻转 b 的 LSB。
2.  并检查新号码是否在范围内(a < number < b)
    *   如果大于“a”的数字再次翻转 lsb
    *   如果不是，那就是答案

## C++

```
// An efficient C++ program to find bit-wise & of all
// numbers from x to y.
#include<bits/stdc++.h>
using namespace std;
typedef long long int ll;

// Function to find Bit-wise & of all numbers from x
// to y.
ll andOperator(ll x, ll y)
{
    // Iterate over all bits of y, starting from the lsb, if it's equal to 1, flip it
    for(int i=0; i<(int)log2(y)+1;i++)
    {
        //repeat till x >= y, otherwise return the answer.
        if (y <= x) {
            return y;
        }
        if (y & (1 << i)) {
            y &= ~(1UL << i);
        }
    }
    return y;
}

// Driver code
int main()
{
    ll x = 10, y = 15;
    cout << andOperator(x, y);
    return 0;
}
```

**Output**

```
8
```

**另一种方法**

我们知道，如果一个数 num 是 2 的幂，那么(num &(num–1))等于 0。因此，如果 a 小于 2^k，b 大于或等于 2^k，那么 a 和 b 之间的所有值的&应该为零，因为(2^k &(2^k–1))等于 0。所以，如果 a 和 b 的位数相同，那么唯一的答案就不会是零。现在，在每种情况下，最后一位必然是零，因为即使 a 和 b 并列为 2，最后一位也会不同。类似地，如果 a 和 b 之间的差值大于 2，第二个最后一位将为零，并且每一位都是如此。现在，以 a = 1100(12)和 b = 1111(15)为例，那么答案的最后一位应该是零。对于第二个最后一位，我们需要检查 a/2 == b/2，因为如果它们相等，那么我们知道 b–a<= 2\. So if a/2 and b/2 is not equal then we proceed. Now, 3rd last bit should have a difference of 4 which can be checked by a/ 4 != b/4\. Hence we check every bit from last until a!=b and in every step we modify a/=2(a >> 1)和 b/=2(b >> 1)从末尾开始减少一位。

1.  运行一个和 a 一样长的 while 循环！= b 和 a > 0
2.  右移 a 1，右移 b 1
3.  增量移位计数
4.  过了一会儿，环路左转* 2^(shiftcount)

## C++

```
// An efficient C++ program to find bit-wise & of all
// numbers from x to y.
#include<bits/stdc++.h>
using namespace std;
#define int long long int

// Function to find Bit-wise & of all numbers from x
// to y.
int andOperator(int a, int b) {
      // ShiftCount variables counts till which bit every value will convert to 0
      int shiftcount = 0;
    //Iterate through every bit of a and b simultaneously
      //If a == b then we know that beyond that the and value will remain constant
      while(a != b and a > 0) {
          shiftcount++;
          a = a >> 1;
          b = b >> 1;
    }
      return int64_t(a << shiftcount);
}

// Driver code
int32_t main() {
    int a = 10, b = 15;
    cout << andOperator(a, b);
    return 0;
}
```
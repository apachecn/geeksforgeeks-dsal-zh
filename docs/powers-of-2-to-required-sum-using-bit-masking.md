# 使用位屏蔽将 2 的幂与所需的和相乘

> 原文:[https://www . geeksforgeeks . org/2 的幂与要求的和使用位屏蔽/](https://www.geeksforgeeks.org/powers-of-2-to-required-sum-using-bit-masking/)

给定一个整数 **N** ，任务是找出将 2 的[次幂相加后得出的整数 **N** 。
**举例:**](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/) 

> **输入:** N = 12345
> **输出:** 0、3、4、5、12、13
> **解释:**
> 12345 = 2^0+2^3+2^4+2^5+2^12+2^13
> **输入:** N = 10000
> **输出:** 4、8、9、10、13
> **解释:**

**进场:**

*   由于每个数字都可以表示为 2 的幂之和，因此任务是当在 **N** 的二进制表示中设置了第 i <sup>位时，打印每个 **i** 。</sup>

> **说明:**
> (29)<sub>10</sub>=(11101)<sub>2</sub>
> 因此，在 29 中，{0，2，3，4}是设置位的索引。
> 2<sup>0</sup>+2<sup>2</sup>+2<sup>3</sup>+2<sup>4</sup>+T17】= 1+4+8+16
> = 29

*   为了检查第 i <sup>位</sup>是否置位，我们只需要检查:

> if(N &(1<< i) ) == 1 
> )T1】插图:
> (29)<sub>10</sub>=(11101)<sub>2</sub>
> 0<sup>th</sup>位:11101 & 1 = 1
> 1 <sup>st</sup> 位:11101&10 = 0
> 2<sup>nd</sup>位:11101 &

下面是上述方法的实现。

## C++

```
// C++ Program to split N
// into numbers which when
// added after being raised
// to the power of 2 gives N

#include <bits/stdc++.h>
using namespace std;

// Function to print the numbers
// which raised to power of 2
// adds up to N
void PowerOfTwo(long long N)
{
    for (int i = 0; i < 64; i++) {
        long long x = 1;

        // Checking if i-th bit is
        // set in N or not by
        // shifting 1 i bits to
        // the left and performing
        // AND with N
        if (N & (x << i))
            cout << i << " ";
    }
}

// Driver Code
int main()
{

    long long N = 12345;
    PowerOfTwo(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to split N
// into numbers which when
// added after being raised
// to the power of 2 gives N
class GFG{

// Function to print the numbers
// which raised to power of 2
// adds up to N
static void PowerOfTwo(long N)
{
    for (int i = 0; i < 64; i++)
    {
        long x = 1;

        // Checking if i-th bit is
        // set in N or not by
        // shifting 1 i bits to
        // the left and performing
        // AND with N
        if ((N & (x << i)) > 0)
            System.out.print(i + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    long N = 12345;
    PowerOfTwo(N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to split N
# into numbers which when
# added after being raised
# to the power of 2 gives N

# Function to print the numbers
# which raised to power of 2
# adds up to N
def PowerOfTwo(N):

    for i in range(0, 64):
        x = 1

        # Checking if i-th bit is
        # set in N or not by
        # shifting 1 i bits to
        # the left and performing
        # AND with N
        if (N & (x << i)) > 0:
            print(i, end = " ")

# Driver Code
if __name__ == "__main__":

    # Given number
    N = 12345;

    # Function call
    PowerOfTwo(N)

# This code is contributed by rock_cool
```

## C#

```
// C# Program to split N
// into numbers which when
// added after being raised
// to the power of 2 gives N
using System;
class GFG{

// Function to print the numbers
// which raised to power of 2
// adds up to N
static void PowerOfTwo(long N)
{
    for (int i = 0; i < 64; i++)
    {
        long x = 1;

        // Checking if i-th bit is
        // set in N or not by
        // shifting 1 i bits to
        // the left and performing
        // AND with N
        if ((N & (x << i)) > 0)
            Console.Write(i + " ");
    }
}

// Driver Code
public static void Main()
{
    long N = 12345;
    PowerOfTwo(N);
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// Javascript Program to split N
// into numbers which when
// added after being raised
// to the power of 2 gives N

// Function to print the numbers
// which raised to power of 2
// adds up to N
function PowerOfTwo(N)
{
    for (var i = 0; i < 64; i++) {
        var x = 1;

        // Checking if i-th bit is
        // set in N or not by
        // shifting 1 i bits to
        // the left and performing
        // AND with N
        if ((N & (x * Math.pow(2,i))) >0)
            document.write( i + " ");
    }
}

// Driver Code
var N = 12345;
PowerOfTwo(N);

// This code is contributed by importantly.
</script>
```

**Output:** 

```
0 3 4 5 12 13
```

***时间复杂度:** O(对数 N)*
***空间复杂度:** O(1)*
如需替代方法，请参考[2 的 2 次方求和](https://www.geeksforgeeks.org/powers-2-required-sum/)
# 范围[L，R]

内所有 I 的 i * countDigits(i)^countDigits(i 之和

> 原文:[https://www . geeksforgeeks . org/I-count digitsintsi-for all-I-in-range-l-r/](https://www.geeksforgeeks.org/sum-of-i-countdigitsicountdigitsi-for-all-i-in-range-l-r/)

给定两个数字 **L，R** ，表示一个范围**【L，R】**，任务是找出所有**I∈【L，R】**的和**I * count digits(I)<sup>count digits(I)</sup>**，其中 **countDigits(i)** 是 **i** 中的位数。
**举例:**

> **输入:** L = 8，R = 11
> **输出:** 101
> **说明:**
> 对于给定的数字，我们需要找到[L，R]范围内所有数字的值。
> =>8 * 1<sup>1</sup>+9 * 1<sup>1</sup>+10 * 2<sup>2</sup>+11 * 2<sup>2</sup>T18】=>8+9+40+44
> =>101
> T21】输入: L = 98，R = 102
> **输出:**
> =>98 * 2<sup>2</sup>+99 * 2<sup>2</sup>+100 * 3<sup>3</sup>+101 * 3<sup>3</sup>+102 * 3<sup>3</sup>T41】=>8969

**进场:**思路是按照位数把区间分成段。也就是说，每个片段都包含相同位数的数字:

```
[1 - 9], [10 - 99], [100 - 999], [1000 - 9999], [10000 - 99999] ...
```

从上面的片段来看，很明显，每个片段的[L，R]都具有相同的长度。因此，该段所需的总和为:

```
countDigits(L)countDigits(L) * (L + R) * (R - L + 1) / 2
```

**证明:**

*   让**【L，R】=【10，14】**其中 **L** 和 **R** 长度相同，即 2。
*   因此，线段**【L，R】**的总和将为:

```
10 * 22 + 11 * 22 + 12 * 22 + 13 * 22 + 14 * 22
```

*   关于服用**2<sup>2</sup>T3】常见:** 

```
22 * (10 + 11 + 12 + 13 + 14) 
=> totalDigitstotalDigits * (Sum of AP)
```

*   AP 之和=(项数/ 2) *(第一项+最后一项)即**(R–L+1)*(L+R)/2**。
*   因此，所需的总和为:

```
countDigits(L)countDigits(L) * (L + R) * (R - L + 1) / 2
```

以下是上述方法的实现:

## C++

```
// C++ program to find the required sum

#include <bits/stdc++.h>
using namespace std;
#define MOD 1000000007

// Function to return the required sum
int rangeSum(int l, int r)
{
    int a = 1, b = 9, res = 0;

    // Iterating for all the number
    // of digits from 1 to 10
    for (int i = 1; i <= 10; i++) {
        int L = max(l, a);
        int R = min(r, b);

        // If the range is valid
        if (L <= R) {

            // Sum of AP
            int sum = (L + R) * (R - L + 1) / 2;
            res += pow(i, i) * (sum % MOD);
            res %= MOD;
        }

        // Computing the next minimum and maximum
        // numbers by for the (i+1)-th digit
        a = a * 10;
        b = b * 10 + 9;
    }
    return res;
}

// Driver code
int main()
{
    int l = 98, r = 102;
    cout << rangeSum(l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the required sum
import java.util.*;

class GFG{
static final int MOD = 1000000007;

// Function to return the required sum
static int rangeSum(int l, int r)
{
    int a = 1, b = 9, res = 0;

    // Iterating for all the number
    // of digits from 1 to 10
    for (int i = 1; i <= 10; i++) {
        int L = Math.max(l, a);
        int R = Math.min(r, b);

        // If the range is valid
        if (L <= R) {

            // Sum of AP
            int sum = (L + R) * (R - L + 1) / 2;
            res += Math.pow(i, i) * (sum % MOD);
            res %= MOD;
        }

        // Computing the next minimum and maximum
        // numbers by for the (i+1)-th digit
        a = a * 10;
        b = b * 10 + 9;
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    int l = 98, r = 102;
    System.out.print(rangeSum(l, r));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to find the required sum

MOD = 1000000007

# Function to return the required sum
def rangeSum(l, r):

    a = 1
    b = 9
    res = 0

    # Iterating for all the number
    # of digits from 1 to 10
    for i in range(1, 11):
        L = max(l, a)
        R = min(r, b)

        # If the range is valid
        if (L <= R):

            # Sum of AP
            sum = (L + R) * (R - L + 1) // 2
            res += pow(i, i) * (sum % MOD)
            res %= MOD

        # Computing the next minimum and maximum
        # numbers by for the (i+1)-th digit
        a = a * 10
        b = b * 10 + 9
    return res

# Driver code
if __name__ == "__main__":

    l = 98
    r = 102
    print(rangeSum(l, r))

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the required sum
using System;

class GFG{
static readonly int MOD = 1000000007;

// Function to return the required sum
static int rangeSum(int l, int r)
{
    int a = 1, b = 9, res = 0;

    // Iterating for all the number
    // of digits from 1 to 10
    for (int i = 1; i <= 10; i++) {
        int L = Math.Max(l, a);
        int R = Math.Min(r, b);

        // If the range is valid
        if (L <= R) {

            // Sum of AP
            int sum = (L + R) * (R - L + 1) / 2;
            res += (int)Math.Pow(i, i) * (sum % MOD);
            res %= MOD;
        }

        // Computing the next minimum and maximum
        // numbers by for the (i+1)-th digit
        a = a * 10;
        b = b * 10 + 9;
    }
    return res;
}

// Driver code
public static void Main(String[] args)
{
    int l = 98, r = 102;
    Console.Write(rangeSum(l, r));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find the required sum

MOD=1000000007

// Function to return the required sum
function rangeSum(l, r)
{
    var a = 1, b = 9, res = 0;

    // Iterating for all the number
    // of digits from 1 to 10
    for (var i = 1; i <= 10; i++) {
        var L = Math.max(l, a);
        var R = Math.min(r, b);

        // If the range is valid
        if (L <= R) {

            // Sum of AP
            var sum = (L + R) * (R - L + 1) / 2;
            res += Math.pow(i, i) * (sum % MOD);
            res %= MOD;
        }

        // Computing the next minimum and maximum
        // numbers by for the (i+1)-th digit
        a = a * 10;
        b = b * 10 + 9;
    }
    return res;
}

// Driver code
var l = 98, r = 102;
document.write( rangeSum(l, r));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
8969
```

时间复杂度:0(10)

辅助空间:0(1)
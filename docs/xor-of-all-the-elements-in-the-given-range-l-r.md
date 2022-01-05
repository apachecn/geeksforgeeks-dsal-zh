# 给定范围[L，R]

内所有元素的异或运算

> 原文:[https://www . geeksforgeeks . org/给定范围内所有元素的异或-l-r/](https://www.geeksforgeeks.org/xor-of-all-the-elements-in-the-given-range-l-r/)

给定一个范围**【l，r】**，任务是找出给定范围内所有整数的异或，即**(l)^(l+1)^(l+2)^…^(r)**
**示例:**

> **输入:** L = 1，R = 4
> **输出:** 4
> 1 ^ 2 ^ 3 ^ 4 = 4
> **输入:** L = 3，R = 9
> **输出:** 2

一个**简单的解决方案**是从 **L** 到 **R** 迭代求所有数字的异或。这需要线性时间。
A **更好的解决方案**是先找到整数 **R** 中的最高有效位。我们的答案不能有比“R”更大的最高有效位。对于 0 和 MSB 之间(含 0 和 MSB)的每个位“I”，我们将尝试确定 L 和 R 之间(含 0 和 MSB)的多个整数的计数的奇偶性，从而设置第“I”<sup>位。如果计数是奇数，那么我们最终答案的第 I<sup>位也将被设置。
现在真正的问题是，对于 i <sup>第</sup>位，我们如何确定计数的奇偶性？
为了一个思路，我们来看看前 16 个整数的二进制表示。</sup></sup> 

> 0:0000
> 1:0001
> 2:0010
> 3:0011
> 4:0100
> 5:0101
> 6:0110
> 7:0111
> 8:1000
> 9:1001
> 10:1010
> 11:1011
> 12:1100
> 110

很容易注意到，每 2 个 <sup>i</sup> 号后，第 i <sup>位的状态就会发生变化。我们将使用这种思想来预测整数的计数，其中第 i <sup>位设置在从 L 到 R(含)的范围内。
这里有两种情况:</sup></sup> 

1.  **案例 1(我！= 0):** 我们尝试确定 L 的第 i <sup>位</sup>是否置位。如果设置，我们试图找到 L 和 L + 2 之间的数字计数的奇偶性 <sup>i</sup> 包括在内，使得它们的 i <sup>第</sup>位被设置。如果 L 的第 I<sup>位被置位，并且 L 是奇数，那么这个计数将是奇数，否则是偶数。
    类似地，对于 R，我们尝试确定 R–2<sup>I</sup>和 R 之间的多个元素的计数的奇偶性，使得它们的 i <sup>第</sup>位被设置。如果 L 的第<sup>位被置位，并且 L 是偶数，那么这个计数将是奇数，否则是偶数。
    我们忽略其间的所有其他整数，因为它们将具有偶数个整数，且第 i <sup>位设置为</sup>。</sup></sup>
2.  **情况 2(i = 0):** 这里，我们有以下情况:
    *   如果 L 和 R 都是奇数，设置为 0 <sup>第</sup>位的整数个数的计数将是**(R–L)/2+1**
    *   在任何其他情况下，计数将是**楼层((R–L+1)/2)**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// most significant bit
int msb(int x)
{
    int ret = 0;
    while ((x >> (ret + 1)) != 0)
        ret++;
    return ret;
}

// Function to return the required XOR
int xorRange(int l, int r)
{

    // Finding the MSB
    int max_bit = msb(r);

    // Value of the current bit to be added
    int mul = 2;

    // To store the final answer
    int ans = 0;

    // Loop for case 1
    for (int i = 1; i <= max_bit; i++) {

        // Edge case when both the integers
        // lie in the same segment of continuous
        // 1s
        if ((l / mul) * mul == (r / mul) * mul) {
            if (((l & (1 << i)) != 0) && (r - l + 1) % 2 == 1)
                ans += mul;
            mul *= 2;
            continue;
        }

        // To store whether parity of count is odd
        bool odd_c = 0;

        if (((l & (1 << i)) != 0) && l % 2 == 1)
            odd_c = (odd_c ^ 1);
        if (((r & (1 << i)) != 0) && r % 2 == 0)
            odd_c = (odd_c ^ 1);

        // Updating the answer if parity is odd
        if (odd_c)
            ans += mul;

        // Updating the number to be added
        mul *= 2;
    }

    // Case 2
    int zero_bit_cnt = zero_bit_cnt = (r - l + 1) / 2;

    if (l % 2 == 1 && r % 2 == 1)
        zero_bit_cnt++;

    if (zero_bit_cnt % 2 == 1)
        ans++;

    return ans;
}

// Driver code
int main()
{
    int l = 1, r = 4;

    // Final answer
    cout << xorRange(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the
// most significant bit
static int msb(int x)
{
    int ret = 0;
    while ((x >> (ret + 1)) != 0)
        ret++;
    return ret;
}

// Function to return the required XOR
static int xorRange(int l, int r)
{

    // Finding the MSB
    int max_bit = msb(r);

    // Value of the current bit to be added
    int mul = 2;

    // To store the final answer
    int ans = 0;

    // Loop for case 1
    for (int i = 1; i <= max_bit; i++)
    {

        // Edge case when both the integers
        // lie in the same segment of continuous
        // 1s
        if ((l / mul) * mul == (r / mul) * mul)
        {
            if (((l & (1 << i)) != 0) && (r - l + 1) % 2 == 1)
                ans += mul;
            mul *= 2;
            continue;
        }

        // To store whether parity of count is odd
        int odd_c = 0;

        if (((l & (1 << i)) != 0) && l % 2 == 1)
            odd_c = (odd_c ^ 1);
        if (((r & (1 << i)) != 0) && r % 2 == 0)
            odd_c = (odd_c ^ 1);

        // Updating the answer if parity is odd
        if (odd_c!=0)
            ans += mul;

        // Updating the number to be added
        mul *= 2;
    }

    // Case 2
    int zero_bit_cnt = zero_bit_cnt = (r - l + 1) / 2;

    if (l % 2 == 1 && r % 2 == 1)
        zero_bit_cnt++;

    if (zero_bit_cnt % 2 == 1)
        ans++;

    return ans;
}

// Driver code
public static void main(String args[])
{
    int l = 1, r = 4;

    // Final answer
    System.out.print(xorRange(l, r));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the most significant bit
def msb(x) :

    ret = 0
    while ((x >> (ret + 1)) != 0) :
        ret = ret + 1
    return ret

# Function to return the required XOR
def xorRange(l, r) :

    # Finding the MSB
    max_bit = msb(r)

    # Value of the current bit to be added
    mul = 2

    # To store the final answer
    ans = 0

    # Loop for case 1
    for i in range (1, max_bit + 1) :

        # Edge case when both the integers
        # lie in the same segment of continuous
        # 1s
        if ((l // mul) * mul == (r // mul) * mul) :
            if ((((l & (1 << i)) != 0) and
                 (r - l + 1) % 2 == 1)) :
                ans = ans + mul
            mul = mul * 2
            continue

        # To store whether parity of count is odd
        odd_c = 0

        if (((l & (1 << i)) != 0) and l % 2 == 1) :
            odd_c = (odd_c ^ 1)
        if (((r & (1 << i)) != 0) and r % 2 == 0) :
            odd_c = (odd_c ^ 1)

        # Updating the answer if parity is odd
        if (odd_c) :
            ans = ans + mul

        # Updating the number to be added
        mul = mul * 2

    # Case 2
    zero_bit_cnt = (r - l + 1) // 2

    if ((l % 2 == 1 ) and (r % 2 == 1)) :
        zero_bit_cnt = zero_bit_cnt + 1

    if (zero_bit_cnt % 2 == 1):
        ans = ans + 1

    return ans

# Driver code
l = 1
r = 4

# Final answer
print(xorRange(l, r))

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the
// most significant bit
static int msb(int x)
{
    int ret = 0;
    while ((x >> (ret + 1)) != 0)
        ret++;
    return ret;
}

// Function to return the required XOR
static int xorRange(int l, int r)
{

    // Finding the MSB
    int max_bit = msb(r);

    // Value of the current bit to be added
    int mul = 2;

    // To store the final answer
    int ans = 0;

    // Loop for case 1
    for (int i = 1; i <= max_bit; i++)
    {

        // Edge case when both the integers
        // lie in the same segment of continuous
        // 1s
        if ((l / mul) * mul == (r / mul) * mul)
        {
            if (((l & (1 << i)) != 0) && (r - l + 1) % 2 == 1)
                ans += mul;
            mul *= 2;
            continue;
        }

        // To store whether parity of count is odd
        int odd_c = 0;

        if (((l & (1 << i)) != 0) && l % 2 == 1)
            odd_c = (odd_c ^ 1);
        if (((r & (1 << i)) != 0) && r % 2 == 0)
            odd_c = (odd_c ^ 1);

        // Updating the answer if parity is odd
        if (odd_c!=0)
            ans += mul;

        // Updating the number to be added
        mul *= 2;
    }

    // Case 2
    int zero_bit_cnt = zero_bit_cnt = (r - l + 1) / 2;

    if (l % 2 == 1 && r % 2 == 1)
        zero_bit_cnt++;

    if (zero_bit_cnt % 2 == 1)
        ans++;

    return ans;
}

// Driver code
public static void Main(String []args)
{
    int l = 1, r = 4;

    // Final answer
    Console.Write(xorRange(l, r));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the
// most significant bit
function msb($x)
{
    $ret = 0;
    while (($x >> ($ret + 1)) != 0)
        $ret++;
    return $ret;
}

// Function to return the required XOR
function xorRange($l, $r)
{

    // Finding the MSB
    $max_bit = msb($r);

    // Value of the current bit to be added
    $mul = 2;

    // To store the final answer
    $ans = 0;

    // Loop for case 1
    for ($i = 1; $i <= $max_bit; $i++)
    {

        // Edge case when both the integers
        // lie in the same segment of continuous
        // 1s
        if ((int)(($l / $mul) * $mul) ==
            (int)(($r / $mul) * $mul))
        {
            if ((($l & (1 << $i)) != 0) &&
                 ($r - $l + 1) % 2 == 1)
                $ans += $mul;
            $mul *= 2;
            continue;
        }

        // To store whether parity of count is odd
        $odd_c = 0;

        if ((($l & (1 << $i)) != 0) && $l % 2 == 1)
            $odd_c = ($odd_c ^ 1);
        if ((($r & (1 << $i)) != 0) && $r % 2 == 0)
            $odd_c = ($odd_c ^ 1);

        // Updating the answer if parity is odd
        if ($odd_c)
            $ans += $mul;

        // Updating the number to be added
        $mul *= 2;
    }

    // Case 2
    $zero_bit_cnt = (int)(($r - $l + 1) / 2);

    if ($l % 2 == 1 && $r % 2 == 1)
        $zero_bit_cnt++;

    if ($zero_bit_cnt % 2 == 1)
        $ans++;

    return $ans;
}

// Driver code
$l = 1;
$r = 4;

// Final answer
echo xorRange($l, $r);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the
// most significant bit
function msb(x)
{
    let ret = 0;
    while ((x >> (ret + 1)) != 0)
        ret++;
    return ret;
}

// Function to return the required XOR
function xorRange(l, r)
{

    // Finding the MSB
    let max_bit = msb(r);

    // Value of the current bit to be added
    let mul = 2;

    // To store the final answer
    let ans = 0;

    // Loop for case 1
    for (let i = 1; i <= max_bit; i++) {

        // Edge case when both the integers
        // lie in the same segment of continuous
        // 1s
        if ((parseInt(l / mul) * mul) ==
        (parseInt(r / mul) * mul))
        {
            if (((l & (1 << i)) != 0) &&
            (r - l + 1) % 2 == 1)
            ans += mul;
            mul *= 2;
            continue;
        }

        // To store whether parity of count is odd
        let odd_c = 0;

        if (((l & (1 << i)) != 0) && l % 2 == 1)
            odd_c = (odd_c ^ 1);
        if (((r & (1 << i)) != 0) && r % 2 == 0)
            odd_c = (odd_c ^ 1);

        // Updating the answer if parity is odd
        if (odd_c)
            ans += mul;

        // Updating the number to be added
        mul *= 2;
    }

    // Case 2
    let zero_bit_cnt = parseInt((r - l + 1) / 2);

    if (l % 2 == 1 && r % 2 == 1)
        zero_bit_cnt++;

    if (zero_bit_cnt % 2 == 1)
        ans++;

    return ans;
}

// Driver code
    let l = 1, r = 4;

    // Final answer
    document.write(xorRange(l, r));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(log <sub>2</sub> (R))

**辅助空间:** O(1)
**有效方法:**让 F(N)是计算所有小于或等于 n 的自然数的 XOR 的函数。因此，对于 range (L-R)，答案将是 **F(R) ^ F(L-1)** 。
如本文[所述，在 O(1)中可以找到任意给定数字的该函数值。
以下是上述方法的实施:](https://www.geeksforgeeks.org/calculate-xor-1-n/) 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required XOR
long computeXOR(const int n)
{
    // Modulus operator are expensive
    // on most of the computers.
    // n & 3 will be equivalent to n % 4
    // n % 4
    switch (n & 3) {

    // If n is a multiple of 4
    case 0:
        return n;

    // If n % 4 gives remainder 1
    case 1:
        return 1;

    // If n % 4 gives remainder 2
    case 2:
        return n + 1;

    // If n % 4 gives remainder 3
    case 3:
        return 0;
    }
}

// Driver code
int main()
{
    int l = 1, r = 4;
    cout << (computeXOR(r) ^ computeXOR(l - 1));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the required XOR
static long computeXOR(int n)
{
    // Modulus operator are expensive
    // on most of the computers.
    // n & 3 will be equivalent to n % 4
    // n % 4
    int x = n & 3;
    switch (x)
    {

        // If n is a multiple of 4
        case 0:
            return n;

        // If n % 4 gives remainder 1
        case 1:
            return 1;

        // If n % 4 gives remainder 2
        case 2:
            return n + 1;

        // If n % 4 gives remainder 3
        case 3:
            return 0;
    }
    return 0;
}

// Driver code
public static void main(String args[])
{
    int l = 1, r = 4;
    System.out.println(computeXOR(r) ^
                       computeXOR(l - 1));
}
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required XOR
def computeXOR(n) :

    # Modulus operator are expensive
    # on most of the computers.
    # n & 3 will be equivalent to n % 4
    # n % 4
    switch = {

        # If n is a multiple of 4
        0 : n,

        # If n % 4 gives remainder 1
        1 : 1,

        # If n % 4 gives remainder 2
        2: n + 1,

        # If n % 4 gives remainder 3
        3 : 0,
    }
    return switch.get( n & 3, "")

# Driver code
l = 1
r = 4
print(computeXOR(r) ^ computeXOR(l - 1))

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the required XOR
static long computeXOR(int n)
{
    // Modulus operator are expensive
    // on most of the computers.
    // n & 3 will be equivalent to n % 4
    // n % 4
    int x=n&3;
    switch (x)
    {

    // If n is a multiple of 4
    case 0:
        return n;

    // If n % 4 gives remainder 1
    case 1:
        return 1;

    // If n % 4 gives remainder 2
    case 2:
        return n + 1;

    // If n % 4 gives remainder 3
    case 3:
        return 0;
    }
    return 0;
}

// Driver code
static void Main()
{
    int l = 1, r = 4;
    Console.WriteLine(computeXOR(r) ^ computeXOR(l - 1));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the required XOR
function computeXOR($n)
{
    // Modulus operator are expensive
    // on most of the computers.
    // n & 3 will be equivalent to n % 4
    // n % 4
    $x = $n & 3;
    switch ($x)
    {

        // If n is a multiple of 4
        case 0:
            return $n;

        // If n % 4 gives remainder 1
        case 1:
            return 1;

        // If n % 4 gives remainder 2
        case 2:
            return $n + 1;

        // If n % 4 gives remainder 3
        case 3:
            return 0;
    }
    return 0;
}

// Driver code
$l = 1; $r = 4;
echo(computeXOR($r) ^ computeXOR($l - 1));

// This code is contributed by Code_Mech
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the required XOR
function computeXOR(n)
{
    // Modulus operator are expensive
    // on most of the computers.
    // n & 3 will be equivalent to n % 4
    // n % 4
    switch (n & 3) {

    // If n is a multiple of 4
    case 0:
        return n;

    // If n % 4 gives remainder 1
    case 1:
        return 1;

    // If n % 4 gives remainder 2
    case 2:
        return n + 1;

    // If n % 4 gives remainder 3
    case 3:
        return 0;
    }
}

// Driver code
    let l = 1, r = 4;
    document.write(computeXOR(r) ^ computeXOR(l - 1));

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
4
```

时间复杂度:0(1)

辅助空间:0(1)
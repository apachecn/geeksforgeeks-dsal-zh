# 检查位在给定范围内是否处于交替模式| Set-2

> 原文:[https://www . geeksforgeeks . org/check-bits-in-alternate-pattern-in-给定范围-set-2/](https://www.geeksforgeeks.org/check-whether-bits-are-in-alternate-pattern-in-the-given-range-set-2/)

给定一个非负数![N ](img/479cbec0e01453d6ddc99e257783bb88.png "Rendered by QuickLaTeX.com")和两个值![L ](img/caf69e1d4b759c8229f0240cca520d11.png "Rendered by QuickLaTeX.com")和![R ](img/e9bd86d980edb46d345fbb7b522c2d7b.png "Rendered by QuickLaTeX.com")。问题是检查 **N** 的二进制表示在 **L** 到 **R** 的范围内是否有交替模式。
这里，交替模式是指设置位和未设置位以交替顺序出现。这些位从右向左编号，即最低有效位被认为在第一个位置。
**示例** :

```
Input : N = 18, L = 1, R = 3
Output : Yes
(18)<sub>10</sub> = (10010)2
The bits in the range 1 to 3 in the
binary representation of 18 are in
alternate order.

Input : N = 22, L = 2, R = 4
Output : No
(22)<sub>10</sub> = (10110)2
The bits in the range 2 to 4 in the
binary representation of 22 are not in
alternate order.
```

**简单方法:**在[这篇文章](https://www.geeksforgeeks.org/check-whether-bits-are-in-alternate-pattern-in-the-given-range/)中已经讨论过了，它的最坏情况时间复杂度为 O(log <sub>2</sub> n)。
**高效方法:**以下是步骤:

1.  声明两个变量 **num** 和 **left_shift** 。
2.  检查 **n** 中 **rth** 位是否置位。参考[这篇](https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/)帖子。如果设置，则分配**编号** = n 和**左移位** = r，否则设置 **(r+1)第**位在 **n** 中，并将其分配给**编号**。参考[这个](https://www.geeksforgeeks.org/set-k-th-bit-given-number/)岗位。同时分配**左移** = r + 1。
3.  执行 **num** = num & ((1 < <左移)–1)。
4.  执行**num**= num>>(l–1)。
5.  最后检查位在**号**中是否为交替模式。参考[这篇](https://www.geeksforgeeks.org/check-number-bits-alternate-pattern-set-2-o1-approach/)帖子。

上述方法的全部思想是创建一个数字 **num** ，其中的位与给定范围 **n** 中的位处于相同的模式，然后检查位在 **num** 中是否处于交替模式。

## C++

```
// C++ implementation to check whether bits are in
// alternate pattern in the given range
#include <bits/stdc++.h>

using namespace std;

// function to check whether rightmost
// kth bit is set or not in 'n'
bool isKthBitSet(unsigned int n,
                 unsigned int k)
{
    if ((n >> (k - 1)) & 1)
        return true;
    return false;
}

// function to set the rightmost kth bit in 'n'
unsigned int setKthBit(unsigned int n,
                       unsigned int k)
{
    // kth bit of n is being set by this operation
    return ((1 << (k - 1)) | n);
}

// function to check if all the bits are set or not
// in the binary representation of 'n'
bool allBitsAreSet(unsigned int n)
{
    // if true, then all bits are set
    if (((n + 1) & n) == 0)
        return true;

    // else all bits are not set
    return false;
}

// function to check if a number
// has bits in alternate pattern
bool bitsAreInAltOrder(unsigned int n)
{
    unsigned int num = n ^ (n >> 1);

    // to check if all bits are set
    // in 'num'
    return allBitsAreSet(num);
}

// function to check whether bits are in
// alternate pattern in the given range
bool bitsAreInAltPatrnInGivenRange(unsigned int n,
                                   unsigned int l,
                                   unsigned int r)
{
    unsigned int num, left_shift;

    // preparing a number 'num' and 'left_shift'
    // which can be further used for the check
    // of alternate pattern in the given range
    if (isKthBitSet(n, r)) {
        num = n;
        left_shift = r;
    }
    else {
        num = setKthBit(n, (r + 1));
        left_shift = r + 1;
    }

    // unset all the bits which are left to the
    // rth bit of (r+1)th bit
    num = num & ((1 << left_shift) - 1);

    // right shift 'num' by (l-1) bits
    num = num >> (l - 1);

    return bitsAreInAltOrder(num);
}

// Driver program to test above
int main()
{
    unsigned int n = 18;
    unsigned int l = 1, r = 3;
    if (bitsAreInAltPatrnInGivenRange(n, l, r))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether bits are in
// alternate pattern in the given range
class GFG
{

// function to check whether rightmost
// kth bit is set or not in 'n'
static boolean isKthBitSet(int n,
                            int k)
{
    if ((n >> (k - 1)) == 1)
        return true;
    return false;
}

// function to set the rightmost kth bit in 'n'
static int setKthBit(int n,
                    int k)
{
    // kth bit of n is being set by this operation
    return ((1 << (k - 1)) | n);
}

// function to check if all the bits are set or not
// in the binary representation of 'n'
static boolean allBitsAreSet(int n)
{
    // if true, then all bits are set
    if (((n + 1) & n) == 0)
        return true;

    // else all bits are not set
    return false;
}

// function to check if a number
// has bits in alternate pattern
static boolean bitsAreInAltOrder(int n)
{
    int num = n ^ (n >> 1);

    // to check if all bits are set
    // in 'num'
    return allBitsAreSet(num);
}

// function to check whether bits are in
// alternate pattern in the given range
static boolean bitsAreInAltPatrnInGivenRange(int n,
                                int l, int r)
{
    int num, left_shift;

    // preparing a number 'num' and 'left_shift'
    // which can be further used for the check
    // of alternate pattern in the given range
    if (isKthBitSet(n, r))
    {
        num = n;
        left_shift = r;
    }
    else
    {
        num = setKthBit(n, (r + 1));
        left_shift = r + 1;
    }

    // unset all the bits which are left to the
    // rth bit of (r+1)th bit
    num = num & ((1 << left_shift) - 1);

    // right shift 'num' by (l-1) bits
    num = num >> (l - 1);

    return bitsAreInAltOrder(num);
}

// Driver code
public static void main(String[] args)
{
    int n = 18;
    int l = 1, r = 3;
    if (bitsAreInAltPatrnInGivenRange(n, l, r))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation to check
# whether bits are in alternate pattern
# in the given range

# function to check whether rightmost
# kth bit is set or not in 'n'
def isKthBitSet(n, k):
    if((n >> (k - 1)) & 1):
        return True
    return False

# function to set the rightmost kth bit in 'n'
def setKthBit(n, k):

    # kth bit of n is being set
    # by this operation
    return ((1 << (k - 1)) | n)

# function to check if all the bits are set or not
# in the binary representation of 'n'
def allBitsAreSet(n):

    # if true, then all bits are set
    if (((n + 1) & n) == 0):
        return True

    # else all bits are not set
    return False

# function to check if a number
# has bits in alternate pattern
def bitsAreInAltOrder(n):
    num = n ^ (n >> 1)

    # to check if all bits are set
    # in 'num'
    return allBitsAreSet(num)

# function to check whether bits are in
# alternate pattern in the given range
def bitsAreInAltPatrnInGivenRange(n, l, r):

    # preparing a number 'num' and 'left_shift'
    # which can be further used for the check
    # of alternate pattern in the given range
    if (isKthBitSet(n, r)):
        num = n
        left_shift = r

    else:
        num = setKthBit(n, (r + 1))
        left_shift = r + 1

    # unset all the bits which are left to the
    # rth bit of (r+1)th bit
    num = num & ((1 << left_shift) - 1)

    # right shift 'num' by (l-1) bits
    num = num >> (l - 1)

    return bitsAreInAltOrder(num)

# Driver Code
if __name__ == '__main__':
    n = 18
    l = 1
    r = 3
    if (bitsAreInAltPatrnInGivenRange(n, l, r)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation to check whether bits are in
// alternate pattern in the given range
using System;

class GFG
{

// function to check whether rightmost
// kth bit is set or not in 'n'
static bool isKthBitSet(int n,
                            int k)
{
    if ((n >> (k - 1)) == 1)
        return true;
    return false;
}

// function to set the rightmost kth bit in 'n'
static int setKthBit(int n,
                    int k)
{
    // kth bit of n is being set by this operation
    return ((1 << (k - 1)) | n);
}

// function to check if all the bits are set or not
// in the binary representation of 'n'
static bool allBitsAreSet(int n)
{
    // if true, then all bits are set
    if (((n + 1) & n) == 0)
        return true;

    // else all bits are not set
    return false;
}

// function to check if a number
// has bits in alternate pattern
static bool bitsAreInAltOrder(int n)
{
    int num = n ^ (n >> 1);

    // to check if all bits are set
    // in 'num'
    return allBitsAreSet(num);
}

// function to check whether bits are in
// alternate pattern in the given range
static bool bitsAreInAltPatrnInGivenRange(int n,
                                int l, int r)
{
    int num, left_shift;

    // preparing a number 'num' and 'left_shift'
    // which can be further used for the check
    // of alternate pattern in the given range
    if (isKthBitSet(n, r))
    {
        num = n;
        left_shift = r;
    }
    else
    {
        num = setKthBit(n, (r + 1));
        left_shift = r + 1;
    }

    // unset all the bits which are left to the
    // rth bit of (r+1)th bit
    num = num & ((1 << left_shift) - 1);

    // right shift 'num' by (l-1) bits
    num = num >> (l - 1);

    return bitsAreInAltOrder(num);
}

// Driver code
public static void Main()
{
    int n = 18;
    int l = 1, r = 3;
    if (bitsAreInAltPatrnInGivenRange(n, l, r))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation to check whether bits are in
// alternate pattern in the given range

// function to check whether rightmost
// kth bit is set or not in 'n'
function isKthBitSet(n, k)
{
    if ((n >> (k - 1)) & 1)
        return true;
    return false;
}

// function to set the rightmost kth bit in 'n'
function setKthBit(n, k)
{
    // kth bit of n is being set by this operation
    return ((1 << (k - 1)) | n);
}

// function to check if all the bits are set or not
// in the binary representation of 'n'
function allBitsAreSet(n)
{
    // if true, then all bits are set
    if (((n + 1) & n) == 0)
        return true;

    // else all bits are not set
    return false;
}

// function to check if a number
// has bits in alternate pattern
function bitsAreInAltOrder(n)
{
    var num = n ^ (n >> 1);

    // to check if all bits are set
    // in 'num'
    return allBitsAreSet(num);
}

// function to check whether bits are in
// alternate pattern in the given range
function bitsAreInAltPatrnInGivenRange(n,
                                   l,
                                   r)
{
    var num, left_shift;

    // preparing a number 'num' and 'left_shift'
    // which can be further used for the check
    // of alternate pattern in the given range
    if (isKthBitSet(n, r)) {
        num = n;
        left_shift = r;
    }
    else {
        num = setKthBit(n, (r + 1));
        left_shift = r + 1;
    }

    // unset all the bits which are left to the
    // rth bit of (r+1)th bit
    num = num & ((1 << left_shift) - 1);

    // right shift 'num' by (l-1) bits
    num = num >> (l - 1);

    return bitsAreInAltOrder(num);
}

// Driver program to test above
var n = 18;
var l = 1, r = 3;
if (bitsAreInAltPatrnInGivenRange(n, l, r))
    document.write( "Yes");
else
    document.write( "No");

</script>   
```

**Output:** 

```
Yes
```

**时间复杂度** : O(1)。
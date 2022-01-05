# 使用位组

计算一个范围内的设置位数

> 原文:[https://www . geeksforgeeks . org/count-使用位集计算范围内的位数/](https://www.geeksforgeeks.org/count-number-of-set-bits-in-a-range-using-bitset/)

给定一个大的二进制数。任务是在从 **L** 到 **R** 的给定范围内计算**1**的数量(基于 1 的索引)。
**举例:**

> **输入:**s =“101101011010100000111”，L = 6，R = 15
> **输出:**5
> s【L:R】=“101101010100”
> 只有 5 个设置位。
> **输入:**s =“10110”，L = 2，R = 5
> **输出:** 2

**进场:**

*   将尺寸 **len** 的字符串转换为尺寸 **N** 的位组。
*   不需要在比特组的左侧有(N–len)+(L–1)比特，在右侧有(N–R)比特。
*   使用左移位和右移位逐位运算有效地移除这些位。
*   现在 L 的左侧和 R 的右侧都是零，所以只需使用 count()函数来获取位集中 1 的计数，因为除[L，R]之外的所有位置都是“0”。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;
#define N 32

// C++ function to count
// number of 1's using bitset
int GetOne(string s, int L, int R)
{

    int len = s.length();

    // Converting the string into bitset
    bitset<N> bit(s);

    // Bitwise operations
    // Left shift
    bit <<= (N - len + L - 1);

    // Right shifts
    bit >>= (N - len + L - 1);
    bit >>= (len - R);

    // Now bit has only those bits
    // which are in range [L, R]

    // return count of one in [L, R]
    return bit.count();
}

// Driver code
int main()
{

    string s = "01010001011";

    int L = 2, R = 4;

    cout << GetOne(s, L, R);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach

N = 32

# function for converting binary
# string into integer value
def binStrToInt(binary_str):
    length = len(binary_str)
    num = 0
    for i in range(length):
        num = num + int(binary_str[i])
        num = num * 2
    return num / 2

# function to count
# number of 1's using bitset
def GetOne(s, L, R) :

    length = len(s);

    # Converting the string into bitset
    bit = s.zfill(32-len(s));

    bit = int(binStrToInt(bit))

    # Bitwise operations
    # Left shift
    bit <<= (N - length + L - 1);

    # Right shifts
    bit >>= (N - length + L - 1);
    bit >>= (length - R);

    # Now bit has only those bits
    # which are in range [L, R]

    # return count of one in [L, R]
    return bin(bit).count('1');

# Driver code
if __name__ == "__main__" :

    s = "01010001011";

    L = 2; R = 4;

    print(GetOne(s, L, R));

# This code is contributed by AnkitRai01
```

**Output:** 

```
2
```

时间复杂度:0

辅助空间:0(镜头)
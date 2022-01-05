# 比特操控(重要战术)

> 原文:[https://www . geesforgeks . org/bits-操纵-重要-战术/](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)

先决条件:[C 中的按位运算符](https://www.geeksforgeeks.org/interesting-facts-bitwise-operators-c/)、[竞争编程的按位黑客](https://www.geeksforgeeks.org/bitwise-hacks-for-competitive-programming/)、[竞争编程的位技巧](https://www.geeksforgeeks.org/bit-tricks-competitive-programming/)

1.  从 1 到 n 计算异或(直接法):

## 卡片打印处理机（Card Print Processor 的缩写）

```
// Direct XOR of all numbers from 1 to n
int computeXOR(int n)
{
    if (n % 4 == 0)
        return n;
    if (n % 4 == 1)
        return 1;
    if (n % 4 == 2)
        return n + 1;
    else
        return 0;
}
```

```
Input: 6
Output: 7
```

1.  详见[从 1 到 n 计算异或](https://www.geeksforgeeks.org/calculate-xor-1-n/)。
2.  我们可以快速计算出小于或等于和与异或相等数的组合总数。不使用循环(蛮力法)，我们可以通过数学技巧直接找到它，即

```
// Refer Equal Sum and XOR for details.
Answer = pow(2, count of zero bits)
```

1.  如何知道一个数是否是 2 的幂？

## 卡片打印处理机（Card Print Processor 的缩写）

```
//  Function to check if x is power of 2
bool isPowerOfTwo(int x)
{
     // First x in the below expression is
     // for  the case when x is 0
     return x && (!(x & (x - 1)));
}
```

1.  详见[检查一个数是否为二的幂](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)。
2.  求集合所有子集的异或。我们可以在一分钟内完成。如果给定的集合有多个元素，答案总是 0。对于具有单个元素的集合，答案是单个元素的值。详见[所有子集](https://www.geeksforgeeks.org/given-a-set-find-xor-of-the-xors-of-all-subsets/)异或的异或。
3.  我们可以使用 GCC 在 C++中快速找到整数的二进制代码中的前导零、尾随零和 1 的数量。这可以通过使用内置功能来实现，即

```
  Number of leading zeroes: builtin_clz(x)
  Number of trailing zeroes : builtin_ctz(x)
  Number of 1-bits: __builtin_popcount(x) 
```

1.  详见 [GCC 内置功能](https://www.geeksforgeeks.org/builtin-functions-gcc-compiler/)。
2.  在 C++中将二进制代码直接转换为整数。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// Conversion into Binary code//
#include <iostream>
using namespace std;

int main()
{
    auto number = 0b011;
    cout << number;
    return 0;
}
```

```
Output: 3
```

1.  交换两个号码的最快方法:

```
a ^= b;
b ^= a; 
a ^= b;
```

1.  详见[互换两个号码](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)。

2.  翻转数字位的简单方法:可以用一种简单的方法来完成，只需从所有位都等于 1 时获得的值中减去数字即可。
    例如:

```
Number : Given Number
Value  : A number with all bits set in given number.
Flipped number = Value – Number.

Example : 
Number = 23,
Binary form: 10111;
After flipping digits number will be: 01000;
Value: 11111 = 31;
```

1.  对于固定大小的整数，我们可以在 O(1)时间内找到最高有效集位。例如，下面的代码是 32 位整数。

## C

```
int setBitNumber(int n)
{     
    // Below steps set bits after
    // MSB (including MSB)

    // Suppose n is 273 (binary
    // is 100010001). It does following
    // 100010001 | 010001000 = 110011001
    n |= n>>1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set. It does following
    // 110011001 | 001100110 = 111111111
    n |= n>>2;  

    n |= n>>4; 
    n |= n>>8;
    n |= n>>16;

    // Increment n by 1 so that
    // there is only one set bit
    // which is just before original
    // MSB. n now becomes 1000000000
    n = n + 1;

    // Return original MSB after shifting.
    // n now becomes 100000000
    return (n >> 1);
}
```

1.  有关详细信息，请参考[查找数字的最高有效设置位](https://www.geeksforgeeks.org/find-significant-set-bit-number/)。

2.  我们可以快速检查一个数字中的位是否处于交替模式(如 101010)。我们计算 n ^ (n >> 1)。如果 n 具有交替模式，则 n ^ (n >> 1)运算将产生仅具有设定位的数。'^'是按位异或运算。有关详细信息，请参考[检查数字在交替模式](https://www.geeksforgeeks.org/check-number-bits-alternate-pattern-set-2-o1-approach/)中是否有位。

本文由 [**桑奇特·加尔格 1**](https://auth.geeksforgeeks.org/profile.php?user=Sanchit Garg 1) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
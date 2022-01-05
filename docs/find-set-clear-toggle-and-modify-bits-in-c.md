# 在 C

中查找、设置、清除、切换和修改位

> 原文:[https://www . geesforgeks . org/find-set-clear-toggle-and-modify-bit-in-c/](https://www.geeksforgeeks.org/find-set-clear-toggle-and-modify-bits-in-c/)

给定一个正整数 **N** ，任务是对 c 中 **N** 的二进制表示执行以下操作序列

*   [查找位:](https://www.geeksforgeeks.org/find-value-k-th-bit-binary-representation/)在 **N** 的二进制表示中查找 **K <sup>第</sup>T5】位。**
*   [设置位:](https://www.geeksforgeeks.org/set-k-th-bit-given-number/)如果**K<sup>th</sup>T5】位为 **0** ，则设置为 **1** 。否则，保持不变。**
*   [清零位:](https://www.geeksforgeeks.org/program-to-clear-k-th-bit-of-a-number-n/)如果 K <sup>第</sup>位为 **1** ，则清零至 **0** 。否则，保持不变。
*   [切换位:](https://www.geeksforgeeks.org/program-to-toggle-k-th-bit-of-a-number-n/)如果**K<sup>th</sup>T5】位为 **1** ，则将其更改为 **0** ，反之亦然。**
*   [修改位:](https://www.geeksforgeeks.org/modify-bit-given-position/)用给定位替换 **K <sup>第</sup>T5】位。**

**示例:**

> **输入:** N = 5，K = 1，P = 0
> **输出:**
> K(= 1) <sup>第</sup>位的 5 为 1。
> 设置第 K(= 1) <sup>位</sup>将 N 修改为 5
> 清除第 K(= 1) <sup>位</sup>将 N 修改为 4。
> 切换第 K(= 1)<sup>位将 N 修改为 4。
> 用 P(= 0)替换 K(= 1) <sup>第</sup>位会将 N 修改为 4</sup>
> 
> **输入** : N = 10，K = 2，P = 1
> **输出:**
> K <sup>第</sup> (= 2)位 5 为 1。
> 设置第 K(= 2)<sup>位将 N 修改为 10。
> 清除第 K(= 2)<sup>位会将 N 修改为 8。
> 切换第 K(= 2)<sup>位将 N 修改为 8。
> 将第 K(= 2) <sup>位</sup>替换为 P(= 1)会将 N 修改为 10。</sup></sup></sup>

**方法:**按照以下步骤查找、设置、清除、切换和修改 **N** 二进制表示中的第 K <sup>位</sup>位。

**找到一点:**

```
 (N >> K) & 1
```

**设置位:**

```
 N = N | (1 << K)
```

**清零位:**

```
 N = N & ~(1 << K)
```

**切换位:**

```
 N = N ^ (1 << K)
```

**修改一点:**

```
 N = N | (P << K)
```

下面是上述方法的实现:

## C

```
// C program to implement
// the above approach

#include <stdio.h>

// Function to set the kth bit of n
int setBit(int n, int k)
{
    return (n | (1 << (k - 1)));
}

// Function to clear the kth bit of n
int clearBit(int n, int k)
{
    return (n & (~(1 << (k - 1))));
}

// Function to toggle the kth bit of n
int toggleBit(int n, int k)
{
    return (n ^ (1 << (k - 1)));
}

// Function to modify k-th bit with p
int modifyBit(int n, int k, int p)
{
    return (n | (p << k));
}

// Function to find the kth bit of n
int findBit(int n, int k)
{
    return ((n >> k) & 1);
}

// Utility function to perform
// the specified Bit Operations
void bitOperations(int n, int k,
                   int p)
{

    printf("K(= %d)-th bit of %d is %d\n",
           k, n, findBit(n, k));

    printf("Setting K(= %d)th bit modifies N to %d\n",
           k, setBit(n, k));

    printf("Clearing K(= %d)th bit modifies N to %d\n",
           k, clearBit(n, k));

    printf("Toggling K(= %d)th bit modifies N to %d\n",
           k, toggleBit(n, k));

    printf("Replacing the K(= %d)<sup>th</sup> bit", k);
    printf(" with P(= %d) modifies N to 10\n",
           modifyBit(n, k, p));
}

// Driver Code
int main()
{
    int n = 5, k = 1, p = 1;
    bitOperations(n, k, p);

    return 0;
}
```

**Output:**

```
K(= 1)-th bit of 5 is 0
Setting K(= 1)th bit modifies N to 5
Clearing K(= 1)th bit modifies N to 4
Toggling K(= 1)th bit modifies N to 4
Replacing the K(= 1)th bit with P(= 7) modifies N to 10

```

***时间复杂度:** O(log(N))*
***辅助空间:** O(1)*
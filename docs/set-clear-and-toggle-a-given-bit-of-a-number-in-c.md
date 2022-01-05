# 在 C

中设置、清除和切换数字的给定位

> 原文:[https://www . geeksforgeeks . org/set-clear-and-toggle-给定的 c 位数字/](https://www.geeksforgeeks.org/set-clear-and-toggle-a-given-bit-of-a-number-in-c/)

给定一个数字 N，任务是设置、清除和切换这个数字 N 的第 K 位

*   [设置一个位](https://www.geeksforgeeks.org/set-k-th-bit-given-number/)意味着如果第 K 位是 0，那么将其设置为 1，如果是 1，那么保持不变。
*   [清零一位](https://www.geeksforgeeks.org/program-to-clear-k-th-bit-of-a-number-n/)表示如果第 K 位为 1，则清零，如果为 0，则保持不变。
*   [切换一个位](https://www.geeksforgeeks.org/program-to-toggle-k-th-bit-of-a-number-n/)意味着如果第 K 位是 1，那么将其更改为 0，如果是 0，那么将其更改为 1。

**示例:**

```
Input: N = 5, K = 1
Output: 
Setting Kth bit: 5
Clearing Kth bit: 4
Toggling Kth bit: 4
Explanation: 
5 is represented as 101 in binary
and has its first bit 1, so 
setting it will result in 101 i.e. 5.
clearing it will result in 100 i.e. 4.
toggling it will result in 100 i.e. 4.

Input: N = 7, K = 2
Output: 
Setting Kth bit: 7
Clearing Kth bit: 5
Toggling Kth bit: 5
Explanation: 
7 is represented as 111 in binary
and has its second bit 1, so 
setting it will result in 111 i.e. 7.
clearing it will result in 101 i.e. 5.
toggling it will result in 101 i.e. 5.

```

**进场:**

以下是设置、清除和切换 N 的第 Kth 位的步骤:

**设置一点**

*   因为我们都知道对具有设定位的任何位执行按位“或”会产生设定位，即

    ```
    Any bit <bitwise OR> Set bit = Set bit

    which means,
    0 | 1 = 1
    1 | 1 = 1

    ```

*   因此，对于设置位来说，用设置位对数字进行按位“或”运算是最好的方法。

    ```
    N = N | 1 << K
    OR
    N |= 1 << K

    where K is the bit that is to be set

    ```

**清零一点**

*   因为具有复位位的任何位的逐位“与”导致复位位，即

    ```
    Any bit <bitwise AND> Reset bit = Reset bit

    which means,
    0 & 0 = 0
    1 & 0 = 0

    ```

*   因此，为了清除一个位，最好对带有复位位的数字进行按位“与”运算。

    ```
    n = n & ~(1 << k)
    OR
    n &= ~(1 << k)

    where k is the bit that is to be cleared

    ```

**切换一点**

*   因为未置位和置位的异或产生置位，置位和置位的异或产生未置位。因此，执行任意位与设定位的逐位异或会导致该位的切换，即

    ```
    Any bit <bitwise XOR> Set bit = Toggle

    which means,
    0 ^ 1 = 1
    1 ^ 1 = 0

    ```

*   因此，为了切换一个位，用复位位对数字进行按位异或是最好的办法。

    ```
    n = n ^ 1 << k
    OR
    n ^= 1 << k

    where k is the bit that is to be cleared

    ```

下面是上述方法的实现:

```
// C program to set, clear and toggle a bit

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

// Driver code
int main()
{
    int n = 5, k = 1;

    printf("%d with %d-th bit Set: %d\n",
           n, k, setBit(n, k));
    printf("%d with %d-th bit Cleared: %d\n",
           n, k, clearBit(n, k));
    printf("%d with %d-th bit Toggled: %d\n",
           n, k, toggleBit(n, k));
    return 0;
}
```

**Output:**

```
5 with 1-th bit Set: 5
5 with 1-th bit Cleared: 4
5 with 1-th bit Toggled: 4

```
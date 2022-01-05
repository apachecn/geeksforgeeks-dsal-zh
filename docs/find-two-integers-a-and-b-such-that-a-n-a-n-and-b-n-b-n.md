# 求两个整数 a 和 b，使得 A ^ N = A + N 和 B ^ N = B + N

> 原文:[https://www . geesforgeks . org/find-two-integer-a-and-B- so-a-n-a-n-and-B- n-B- n/](https://www.geeksforgeeks.org/find-two-integers-a-and-b-such-that-a-n-a-n-and-b-n-b-n/)

给定一个非负整数 **N** ，任务是找出两个整数 a(小于 n 的最大整数)和(大于 n 的最小整数),使得 **A + N = A ^ N** 和 **B + N = B ^ N**
**示例:**

> **输入:** N = 5
> **输出:** A = 2 和 B = 8
> 2 + 8 = 2 ^ 8 = 10
> **输入:** N = 10
> **输出:** A = 5 和 B = 16
> 5 + 16 = 5 ^ 16 = 21

**逼近:**让我们独立找到 A 和 B。为了解决这个问题，我们必须使用属性, **x + y = x^y + 2 * (x & y)**
,因为问题指出 xor 和等于给定的和，这意味着它们的和必须为 0。

*   **求 A:** N 可以表示为 0 和 1 的一系列位。为了找到 A，我们首先要找到 N 的最高有效位。由于 A & N = 0，N 已经设置位的地方，对于那个地方，我们将使 A 的位为未设置，对于 N 已经未设置位的地方，我们将使该位为 A 设置，因为我们想要最大化 A。这将对从最高有效到最低有效的所有位进行。因此我们会得到我们的 a。
*   **找 B:** 找 B 很容易。设 I 为 1 中最左边置位的位置。我们希望 B 大于 N，也希望 B & N =0。因此使用这两个事实 B 将总是(1 < < (i+1))。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 32

// Function to find A and B
void findAB(int N)
{
    bitset<MAX> arr(N), brr(N);

    // To store the leftmost set bit in N
    int leftsetN = -1;
    for (int i = MAX - 1; i >= 0; --i) {
        if (arr[i] == 1) {
            leftsetN = i;
            break;
        }
    }

    // To store the value of A
    int A = 0;
    for (int i = leftsetN; i >= 0; --i) {

        // If the bit is unset in N
        // then  we will set it in A
        if (arr[i] == 0) {
            A |= (1 << i);
        }
    }

    // To store the value of B
    int B = 0;

    // B will be (1 << (leftsetN + 1))
    B = 1 << (leftsetN + 1);

    // Print the values of A and B
    cout << "A = " << A << " and B = " << B;
}

// Driver code
int main()
{
    int N = 5;

    findAB(N);

    return 0;
}
```

**Output:** 

```
A = 2 and B = 8
```

时间复杂度:0(最大值)

辅助空间:O(N)
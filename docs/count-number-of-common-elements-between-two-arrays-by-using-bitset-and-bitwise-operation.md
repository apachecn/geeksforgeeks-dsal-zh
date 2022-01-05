# 使用位集和按位运算

计算两个数组之间公共元素的个数

> 原文:[https://www . geesforgeks . org/count-通过使用位集和位操作计算两个数组之间的公共元素数/](https://www.geeksforgeeks.org/count-number-of-common-elements-between-two-arrays-by-using-bitset-and-bitwise-operation/)

给定两个数组 **a[]** 和 **b[]** ，任务是找出两个给定数组中公共元素的数量。**注意**两个数组都包含不同的(单独的)正整数。
**举例:**

> **输入:** a[] = {1，2，3}，b[] = {2，4，3}
> **输出:** 2
> 2 和 3 是两个数组共有的。
> **输入:** a[] = {1，4，7，2，3}，b[] = {2，11，7，4，15，20，24}
> **输出:** 3

**方法:**我们将使用 3 个相同大小的[位组](https://www.geeksforgeeks.org/c-bitset-and-its-application/)。首先，我们将遍历第一个数组，并将位 1 设置为第一个位集中的位置 **a[i]** 。
之后，我们将遍历第二个数组，并将位 1 设置为第二个位集中的位置 **b[i]** 。
最后我们将找到两个位集的按位 AND，如果结果位集的 **i <sup>th</sup>** 位置是 **1** ，那么这意味着第一和第二位集的 **i <sup>th</sup>** 位置也是 **1** 和 **i** 是两个数组中的公共元素。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 100000
bitset<MAX> bit1, bit2, bit3;

// Function to return the count of common elements
int count_common(int a[], int n, int b[], int m)
{

    // Traverse the first array
    for (int i = 0; i < n; i++) {

        // Set 1 at position a[i]
        bit1.set(a[i]);
    }

    // Traverse the second array
    for (int i = 0; i < m; i++) {

        // Set 1 at position b[i]
        bit2.set(b[i]);
    }

    // Bitwise AND of both the bitsets
    bit3 = bit1 & bit2;

    // Find the count of 1's
    int count = bit3.count();

    return count;
}

// Driver code
int main()
{

    int a[] = { 1, 4, 7, 2, 3 };
    int b[] = { 2, 11, 7, 4, 15, 20, 24 };
    int n = sizeof(a) / sizeof(a[0]);
    int m = sizeof(b) / sizeof(b[0]);

    cout << count_common(a, n, b, m);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX = 100000
bit1 , bit2, bit3 = 0, 0, 0

# Function to return the count of common elements
def count_common(a, n, b, m) :

    # Traverse the first array
    for i in range(n) :

        global bit1, bit2, bit3

        # Set 1 at (index)position a[i]
        bit1 = bit1 | (1<<a[i])

    # Traverse the second array
    for i in range(m) :

        # Set 1 at (index)position b[i]
        bit2 = bit2 | (1<<b[i])

    # Bitwise AND of both the bitsets
    bit3 = bit1 & bit2;

    # Find the count of 1's
    count = bin(bit3).count('1');

    return count;

# Driver code
if __name__ == "__main__" :

    a = [ 1, 4, 7, 2, 3 ];
    b = [ 2, 11, 7, 4, 15, 20, 24 ];
    n = len(a);
    m = len(b);

    print(count_common(a, n, b, m));

# This code is contributed by AnkitRai01
```

**Output:** 

```
3
```

时间复杂度:0(n+m)

辅助空间:0(最大)
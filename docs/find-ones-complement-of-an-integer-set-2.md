# 求整数的补码|集合 2

> 原文:[https://www . geesforgeks . org/find-one-complex-of-a-integer-set-2/](https://www.geeksforgeeks.org/find-ones-complement-of-an-integer-set-2/)

给定一个整数 **N** ，求该整数的补码。

**示例:**

> **输入:** N = 5
> **输出:** 2
> **说明:**5 的二进制表示为“101”。它的补码是“010”= 2。
> 
> **输入:**N = 255
> T3】输出: 0
> 
> **输入:**N = 26
> T3】输出: 5

**方法:**文章的[集-1 中已经提到了基于异或的方法和将数转换为二进制数的方法。这里的数字是通过翻转位并将 2 的幂加到答案上来转换的。按照下面提到的步骤来实现它:](https://www.geeksforgeeks.org/find-ones-complement-integer/)

*   求 n 的二进制表示。
*   对于每一位，对其进行补充，并将该位的贡献添加到最终答案中。
*   返回最终答案

下面是上述方法的实现。

## C++

```
// CPP program to find 1's complement of N.
#include <bits/stdc++.h>
using namespace std;

// Find the 1's complement of N
int findComplement(int num)
{
    int ans = 0;
    for (int i = 0; num > 0; i++) {
        ans += pow(2, i) * (!(num % 2));
        num /= 2;
    }

    return ans;
}

// Driver code
int main()
{
    unsigned int N = 5;
    cout << findComplement(N);
    return 0;
}
```

**Output**

```
2
```

***时间复杂度:*** O(log N)
***辅助空间:*** O(1)
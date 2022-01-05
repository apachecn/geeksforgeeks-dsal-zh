# 生成一个 N 长度阵列，其所有对的 GCD 出现在给定的 2D 阵列中

> 原文:[https://www . geeksforgeeks . org/generate-an-n-length-array-having-gcd-of-it-pairs-present-in-a-2d-array/](https://www.geeksforgeeks.org/generate-an-n-length-array-having-gcd-of-all-its-pairs-present-in-a-given-2d-array/)

给定一个由 **N*N** 正整数组成的 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[][]** ，任务是生成一个 N 长度的数组，使得该数组的所有可能对的[最大公约数(GCD)出现在数组 **arr[][]** 中。](https://www.geeksforgeeks.org/find-pair-maximum-gcd-array/)

**示例:**

> **输入:** N = 4，arr[] = {2，1，2，3，4，3，2，6，1，1，2，2，1，2，2，2，2，2，3，3，2}
> **输出:** 4，3，6，2
> **解释:**
> 将数组 A[]视为{4，3，6，2}，则下面给出该数组所有可能对的 GCD，即为给定数组 arr[]。
> {{4，1，2，2}，
> {1，3，3，1}，
> {2，3，6，2}，
> {2，1，2，2}}
> 
> **输入:** N = 1，mat = { 100 }
> T3】输出: 100

**方法:**利用原始数组中最大元素与自身的 gcd 在 arr[]中最大，去掉与该元素的 GCD 对后，可以找到下一个元素的事实，可以解决上述问题。按照以下步骤解决给定的问题:

*   初始化一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)比如说， **M** 在图 **M** 中存储数组元素的[否定频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   初始化一个变量，说 **pos** 为**(N-1)**。
*   现在，对于所有数组元素 **arr[]** 找到最大元素。
*   [穿越地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)T2
*   对于原始数组的每个元素，找到**最大**频率的元素，并存储在 ans 中。
*   找到**ans【pos】**并移除 **ans** 的 **pos+1** 到 **N-1** 的所有 [GCD](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) 。
*   将**位置**更新为**位置-1** 。
*   重复以上步骤，查找原始数组的所有元素。
*   最后打印 **ans** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
int n;

// Function to calculate GCD of two numbers
int gcd(int a, int b)
{
    return b == 0 ? a : gcd(b, a % b);
}

// Function to generate an N-length
// array having GCD of all pairs
// present in the array mat[][]
void restoreArray(vector<int> mat)
{
    map<int, int> cnt;

    // Stores the required array
    vector<int> ans(n);

    for (int i = 0; i < (n * n); ++i) {

        // Store frequencies in map
        // in decreasing order
        cnt[-mat[i]]++;
    }

    int pos = n - 1;

    for (auto it = cnt.begin();
         it != cnt.end(); ++it) {

        int x = -it->first;
        while (it->second) {

            // gcd(x, x)
            ans[pos] = x;
            --it->second;

            // Remove all GCDs for
            // indices pos + 1 -> n - 1
            for (int i = pos + 1; i < n; ++i)

                cnt[-gcd(ans[pos], ans[i])] -= 2;

            // Decreasing pos
            pos--;
        }
    }

    // Print restored array
    for (int i = 0; i < n; ++i)
        printf("%d ", ans[i]);
}

// Driver Code
int main()
{

    // Given Input
    n = 4;
    vector<int> mat{ 2, 1, 2, 3, 4, 3,
                     2, 6, 1, 1, 2,
                     2, 1, 2, 3, 2 };

    // Function Call
    restoreArray(mat);
    return 0;
}
```

**Output:**

```
2 3 4 6

```

***时间复杂度:**O(N<sup>2</sup>LogN)*
***辅助空间:** O(N <sup>2</sup> )*
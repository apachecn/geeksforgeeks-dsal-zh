# 从给定数组中找出 N-1 对(X，Y)，使得 X 和 Y 不同，并且数组中没有预设 X 模 y

> 原文:[https://www . geeksforgeeks . org/find-n-1-pairs-x-y-from-给定-array-so-x 和-y-different-and-x-modal-y-is-not-preset-in-array/](https://www.geeksforgeeks.org/find-n-1-pairs-x-y-from-given-array-such-that-x-and-y-are-different-and-x-modulo-y-is-not-preset-in-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **Arr[]** ，由 **N** 两两不同的正整数组成。任务是找到满足以下条件的**N–1**对不同的正整数 **X，Y** :

*   x≥y
*   x，Y 都属于数组。
*   X mod Y 不属于数组。

> **注:**证明 N-1 个这样的对总是存在的。

**示例:**

> **输入:** N = 4，Arr [ ] = { 2，3，4，5 }
> **输出:** (5，2)，(4，2)，(3，2)
> **解释:**4–1 = 3，因此打印了 3 个这样的对。
> 在第一对中 5 和 2 都属于数组，5 不等于 2，5 mod 2 不属于数组。
> 同样适用于所有印刷对。
> 
> **输入:** N = 2，Arr [ ] = { 1，3 }
> **输出:** 3，1
> **说明:**2–1 = 1。因此只有一对这样的。那是 3，1。

**方法:**以上问题可以用[贪心法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。在这种方法中，永远不要寻找所有可能的情况。相反，寻找我们需要的部分或数量。请按照以下步骤解决此问题:

*   将变量 **min_element** 初始化为 **Arr[0]。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:
    *   计算 **min_element** 的值作为数组 **Arr[]的[最小元素。](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:
    *   如果 **Arr[i]** 不等于 **min_element，**则打印 **Arr[i]，min_element** 作为对。

这种方法基于以下观察:

> 假设 **X** 是给定数组中的最小元素。
> Arr[I]% X 的值**永远小于 **X** ，**数组中无元素**小于 X**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the possible pairs
void find(int N, int Arr[])
{
    int min_element = Arr[0];

    // Get the minimum element
    for (int i = 0; i < N; i++) {
        if (Arr[i] < min_element) {
            min_element = Arr[i];
        }
    }

    // Pair rest N - 1 elements with
    // the minimum element and print
    for (int i = 0; i < N; i++) {
        if (Arr[i] != min_element) {
            cout << Arr[i] << " " <<
                min_element << endl;
        }
    }
}

// Driver Code
int main()
{

    // Initialize N and the Array
    int N = 4;
    int Arr[4] = { 2, 3, 4, 5 };

    find(N, Arr);

    return 0;
}
```

**Output**

```
3 2
4 2
5 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
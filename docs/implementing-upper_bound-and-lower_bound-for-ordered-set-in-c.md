# 在 C++中实现有序集的上界()和下界()

> 原文:[https://www . geeksforgeeks . org/implementing-upper _ bound-and-down _ bound-for-ordered-set-in-c/](https://www.geeksforgeeks.org/implementing-upper_bound-and-lower_bound-for-ordered-set-in-c/)

**先决条件:** [有序集和 GNU C++ PBDS](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/)
给定一个[有序集](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/) **集**和一个键 **K** ，任务是在 C++中找到**集**中元素 **K** 的[上界和下界](https://www.geeksforgeeks.org/lower-and-upper-bound-theory/)。如果元素不存在或无法计算任何一个边界，则打印 **-1** 。

> **有序集**是 g++ 中基于[策略的数据结构，它将唯一的元素保持在有序的顺序中。它以对数(n)复杂度执行由](https://www.geeksforgeeks.org/policy-based-data-structures-g/)[集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)在 [STL](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) 中执行的所有操作。除此之外，它还以 log(n)复杂度执行两个额外的操作，如:
> 1。 **order_of_key (K):** 严格小于 K 的项目数
> 2。**find _ by _ order(K):**K<sup>集合中的第</sup>个元素(从零开始计数)。

**示例:**

> **输入:** set[] = {10，20，30，40，50，60}，K = 30
> **输出:**
> 30:30 的下界
> 30:40 的上界
> **解释:**
> 元素 30 的下界位于位置 2
> 元素 30 的上界为 40 位于位置 3
> **输入:**

**进场:**

*   **上限():****上限(键)**函数返回的元素刚好大于传入参数的键。
*   **下界():****下界(键)**函数返回的元素相当于参数中传递的键。如果键不在有序集中，那么函数应该返回大于参数的元素。
*   为了实现上界和下界函数，使用 [order_of_key()](https://www.geeksforgeeks.org/order_of_key-in-c/) 函数可以找到作为参数传递的有序集中元素的索引(如果存在)。
*   现在，下限和上限都可以通过简单地比较这个索引中的元素来找到。

下面是下界()和上界()的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to implement the
// lower_bound() and upper_bound()
// using Ordered Set

#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;
using namespace std;

// Ordered Set Tree
typedef tree<int, null_type, less<int>, rb_tree_tag,
             tree_order_statistics_node_update>
    ordered_set;

ordered_set set1;

// Function that returns the lower bound
// of the element
int lower_bound(int x)
{
    // Finding the position of the element
    int pos = set1.order_of_key(x);

    // If the element is not present in the set
    if (pos == set1.size())
    {
        return -1;
    }

    // Finding the element at the position
    else
    {
        int element = *(set1.find_by_order(pos));

        return element;
    }
}

// Function that returns the upper bound
// of the element
int upper_bound(int x)
{
    // Finding the position of the element
    int pos = set1.order_of_key(x + 1);

    // If the element is not present
    if (pos == set1.size())
    {
        return -1;
    }

    // Finding the element at the position
    else
    {
        int element = *(set1.find_by_order(pos));

        return element;
    }
}

// Function to print Upper
// and Lower bound of K
// in Ordered Set
void printBound(int K)
{

    cout << "Lower Bound of " << K << ": " << lower_bound(K)
         << endl;
    cout << "Upper Bound of " << K << ": " << upper_bound(K)
         << endl;
}

// Driver's Code
int main()
{
    set1.insert(10);
    set1.insert(20);
    set1.insert(30);
    set1.insert(40);
    set1.insert(50);

    int K = 30;
    printBound(K);

    K = 60;
    printBound(K);

    return 0;
}
```

**Output**

```
Lower Bound of 30: 30
Upper Bound of 30: 40
Lower Bound of 60: -1
Upper Bound of 60: -1

```

**时间复杂度:** O(对数 N)
# 使用有序集和 GNU C++ PBDS 计算反演

> 原文:[https://www . geesforgeks . org/counting-inversion-use-ordered-set-and-GNU-c-pbds/](https://www.geeksforgeeks.org/counting-inversions-using-ordered-set-and-gnu-c-pbds/)

给定一个由 N 个整数组成的数组 **arr[]** 。任务是求逆序数。如果**arr【I】>arr【j】和 i < j** ，则两个元素**arr【I】**和**arr【j】**形成倒置。

**示例**

> **输入:** arr[] = {8，4，2，1}
> **输出:** 6
> **解释:**
> 给定数组有六个反转:
> 
> *   (8，4): arr[0] > arr[1]和 0 < 1
> *   (8，2): arr[0] > arr[2]和 0 < 2
> *   (8，1): arr[0] > arr[3]和 0 < 3
> *   (4，2): arr[1] > arr[2]和 1 < 2
> *   (4，1): arr[1] > arr[3]和 1 < 3
> *   (2，1): arr[2] > arr[3]和 2 < 3
> 
> **输入:** arr[] = {2，3}
> **输出:** 0
> **解释:**
> 不存在 arr[i] > arr[j]和 i < j.
> 这样的对

我们已经讨论了以下方法:

*   [计数数组中的反转|集合 1(使用合并排序)](https://www.geeksforgeeks.org/counting-inversions/)
*   [计数阵列中的反转|集合 2(使用自平衡 BST)](https://www.geeksforgeeks.org/count-inversions-in-an-array-set-2-using-self-balancing-bst/)
*   [使用 C++ STL 中的集合计算反转](https://www.geeksforgeeks.org/counting-inversions-using-set-in-c-stl/)
*   [计数数组中的反转|设置 3(使用位)](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit/)

在这篇文章中，我们将讨论一种使用[有序集和 GNU C++ PBDS 的方法。](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/)

**方法:**
我们将使用函数 **order_of_key(K)** ，该函数在 **log N** 时间内返回严格小于 K 的元素数。

1.  在有序集中插入数组的第一个元素。
2.  对于 **arr[]** 中的所有剩余元素，请执行以下操作:
    *   在有序集中插入当前元素。
    *   使用功能 **order_of_key(arr[i]+1)** ，在 Ordered_Set 中找到严格小于**当前元素+ 1** 的元素数。
    *   **有序集**的大小和键的顺序(当前元素+ 1)之间的差异将给出当前元素的反转计数。

**例如:**

```
arr[] = {8, 4, 2, 1}
Ordered_Set S = {8}
For remaining element in arr[]:
At index 1, the element is  4
S = {4, 8}
key = order_of_key(5) = 1
The difference between size of S and key gives the total 
number of inversion count for that current element.
inversion_count = S.size() - key =  2 - 1 = 1
Inversion Pairs are: (8, 4)

At index 2, the element is  2
S = {2, 4, 8}
key = order_of_key(3) = 1
inversion_count = S.size() - key =  3 - 1 = 2
Inversion Pairs are: (8, 2) and (4, 2)

At index 3, the element is 1
S = {1, 2, 4, 8}
key = order_of_key(2) = 1
inversion_count = S.size() - key =  4 - 1 = 3
Inversion Pairs are: (8, 1), (4, 1) and (2, 1)

Total inversion count = 1 + 2 + 3 = 6
```

下面是上述方法的实现:

## C++

```
// Ordered set in GNU C++ based
// approach for inversion count
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;
using namespace std;

// Ordered Set Tree
typedef tree<int, null_type, less_equal<int>,
             rb_tree_tag,
             tree_order_statistics_node_update>
    ordered_set;

// Returns inversion count in
// arr[0..n-1]
int getInvCount(int arr[], int n)
{
    int key;
    // Initialise the ordered_set
    ordered_set set1;

    // Insert the first
    // element in set
    set1.insert(arr[0]);

    // Initialise inversion
    // count to zero
    int invcount = 0;

    // Finding the inversion
    // count for current element
    for (int i = 1; i < n; i++) {
        set1.insert(arr[i]);

        // Number of elements strictly
        // less than arr[i]+1
        key = set1.order_of_key(arr[i] + 1);

        // Difference between set size
        // and key will give the
        // inversion count
        invcount += set1.size() - key;
    }
    return invcount;
}

// Driver's Code
int main()
{
    int arr[] = { 8, 4, 2, 1 };
    int n = sizeof(arr) / sizeof(int);

    // Function call to count
    // inversion
    cout << getInvCount(arr, n);
    return 0;
}
```

**Output:** 

```
6
```

**时间复杂度:** O(Nlog N)
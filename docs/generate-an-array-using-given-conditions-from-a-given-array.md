# 使用给定数组中的给定条件生成数组

> 原文:[https://www . geeksforgeeks . org/从给定数组中使用给定条件生成数组/](https://www.geeksforgeeks.org/generate-an-array-using-given-conditions-from-a-given-array/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是使用数组 **A** 的元素构建一个新的数组 **B[]** ，这样:

1.  如果元素不在 **B[]** 中，则将其追加到末尾。
2.  如果该元素出现在 **B[]** 中，则首先将其最左边的出现增加 1，然后将该元素追加到数组的末尾。

**例:**

> **输入:** arr[] = {1，2，1，2}
> **输出:** { 3，2，1，2 }
> **解释:**
> arr[0] = 1，B = {}。1 在 b 中不存在，所以在末尾追加。因此，B = {1}
> arr[1] = 2，B = {1}。2 在 b 中不存在，所以把它附加在最后。因此，B[] = {1，2}
> arr[2] = 1，B = {1，2}。1 已经存在于 B[]中。所以将 B[0]增加 1，并在末尾追加 1。因此 B[] = {2，2，1}
> arr[3] = 2，B = {2，2，1}。2 已经存在于 B[]中。所以将 B[0]增加 1，并在末尾追加 2。因此 B[] = {3，2，1，2}
> **输入:** arr[] = {2，5，4，2，8，4，2}
> **输出:** {3，5，5，3，8，4，2}

**天真方法:**对于数组 A 中的每个元素，检查它是否存在于数组 B 中。如果元素存在，则将最左边的匹配项增加 1。最后，在数组 B[]的末尾添加元素。
***时间复杂度:** O(N <sup>2</sup> )*
**高效方法:**思路是用一张[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储每个元素的所有指标。数组 B[]生成为:

*   对于数组 **arr[]** 中的每个元素，检查该元素是否已经存在于数组 **B[]** 中。
*   如果该元素不在数组 **B[]** 中，则该元素被添加到数组 **B[]** 中，其索引被添加到**地图**中。由于这是该元素的第一次出现，因此该索引成为该元素的**最左侧索引**。
*   如果元素已经存在于数组 **B[]** 中，则返回**最左边的**索引，并且该索引处的元素**增加**1。当该值递增时，旧值的最左侧索引将与新值的索引一起更新。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to generate an array
// from a given array under the
// given conditions

#include <bits/stdc++.h>
using namespace std;

// Function to generate an array
// from a given array under the
// given conditions
void newArray(int A[], int n)
{
    // To maintain indexes of the
    // elements in sorted order
    unordered_map<int, set<int> > idx;

    // Initialize new array B
    std::vector<int> B;

    // For every element in the given
    // array arr[]
    for (int i = 0; i < n; ++i) {

        // Check if the element is present
        // in the array B[]
        if (idx.find(A[i]) != idx.end()) {

            // Get the leftmost position
            // in the array B
            int pos = *idx[A[i]].begin();

            // Remove the leftmost position
            idx[A[i]].erase(idx[A[i]].begin());

            // Increment the value at
            // the leftmost position
            B[pos]++;

            // Insert new value position
            // in the map
            idx[B[pos]].insert(pos);
        }

        // Append arr[i] at the end
        // of the array B
        B.push_back(A[i]);

        // Insert its position in hash-map
        idx[A[i]].insert(i);
    }

    // Print the generated array
    for (int i = 0; i < n; ++i)
        cout << B[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 1, 2 };
    int n = sizeof(arr) / sizeof(int);

    newArray(arr, n);

    return 0;
}
```

**Output:** 

```
3 2 1 2
```

时间复杂度:0(n)

辅助空间:O(n)
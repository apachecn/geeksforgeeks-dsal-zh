# 检查一个数组的元素是否可以排列成一个连续差为 1 的圆

> 原文:[https://www . geeksforgeeks . org/check-if-a-array-elements-in-a-circle-in-array-in-continuous-difference-as-1/](https://www.geeksforgeeks.org/check-if-elements-of-an-array-can-be-arranged-in-a-circle-with-consecutive-difference-as-1/)

给定一组![N ](img/479cbec0e01453d6ddc99e257783bb88.png "Rendered by QuickLaTeX.com")数字。任务是检查是否有可能将所有的数字排列成一个圆，使任何两个相邻的数字相差 1。如果可能得到这样的安排，打印“是”，否则打印“否”。
**例:**

```
Input: arr[] = {1, 2, 3, 2}
Output: YES
The circle formed is:
         1
     2       2
         3   

Input: arr[] = {3, 5, 8, 4, 7, 6, 4, 7}
Output: NO
```

下面是解决这个问题的分步算法:

1.  首先在多集合中插入所有元素。
2.  移除集合的第一个元素，并将其存储在 *curr* 变量中。
3.  遍历直到多集的大小减少到 0。
    *   移除比*电流*值大 1 或小 1 的元素。
    *   如果存在差值大于 1 的值，则“不可能有圆”。
4.  检查 *curr* 变量的初始值和最终值是否相同，如果相同，则打印“是”，否则打印“否”。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to check if elements of array
// can be arranged in Circle with consecutive
// difference as 1

#include <bits/stdc++.h>
using namespace std;

// Function to check if elements of array can
// be arranged in Circle with consecutive
// difference as 1
int circlePossible(int arr[], int n)
{
    multiset<int> s;

    // Initialize the multiset with array
    // elements
    for (int i = 0; i < n; i++)
        s.insert(arr[i]);

    // Get a pointer to first element
    int cur = *s.begin();

    // Store the first element in a temp variable
    int start = cur;

    // Remove the first element
    s.erase(s.begin());

    // Traverse until multiset is non-empty
    while (s.size()) {

        // Elements which are 1 greater than the
        // current element, remove their first occurrence
        // and increment curr
        if (s.find(cur + 1) != s.end())
            s.erase(s.find(++cur));

        // Elements which are 1 less than the
        // current element, remove their first occurrence
        // and decrement curr
        else if (s.find(cur - 1) != s.end())
            s.erase(s.find(--cur));

        // If the set is non-empty and contains element
        // which differs by curr from more than 1
        // then circle is not possible return
        else {
            cout << "NO";
            return 0;
        }
    }

    // Finally, check if curr and first differs by 1
    if (abs(cur - start) == 1)
        cout << "YES";
    else
        cout << "NO";

    return 0;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 2, 2, 3 };

    int n = sizeof(arr) / sizeof(arr[0]);

    circlePossible(arr, n);

    return 0;
}
```

**Output:** 

```
YES
```
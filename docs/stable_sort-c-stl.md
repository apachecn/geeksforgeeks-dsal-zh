# c++ STL 中的 stable_sort()

> 原文:[https://www.geeksforgeeks.org/stable_sort-c-stl/](https://www.geeksforgeeks.org/stable_sort-c-stl/)

**stable_sort()** 用于对**【第一位、** **最后)**范围内的元素进行升序排序。类似于 [std::sort](https://www.geeksforgeeks.org/sort-c-stl/) ，但是 stable_sort()保持等价元素的相对顺序。它位于 **<算法>** 头文件下。

**语法:**

```
template< class RandomIterator>
void stable_sort( RandomIterator first, RandomIterator last );
```

或者

```
template< class RandomIterator, class Compare>
void stable_sort( RandomIterator first, RandomIterator last, Compare comp );
```

**参数:**

*   **第一个:**迭代器，指向范围中的第一个元素。
*   **最后:**迭代器，指向范围中过去的最后一个元素。
*   **comp:** 谓词函数，接受两个参数，如果两个参数顺序正确，则返回 true，否则返回 false。

**返回值:**不返回任何内容。

**示例:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate stable sort() in STL
#include <bits/stdc++.h>
using namespace std;

// Driver Code
int main()
{
    int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);

    stable_sort(arr, arr + n);

    cout << "Array after sorting using "
            "stable_sort is : \n";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";

    return 0;
}
```

**Output**

```
Array after sorting using stable_sort is : 
0 1 2 3 4 5 6 7 8 9 
```

### 如何使用 stable_sort()进行降序排序？

像 sort()一样，stable_sort()接受第三个参数，用于指定元素的排序顺序。我们可以通过“greater()”函数按降序排序。这个函数以一种把更大的元素放在前面的方式进行比较。

**语法:**

```
// arr is the array and n is the size
stable_sort(arr, arr + n, greater<int>());  
```

**示例:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate descending order
// stable sort using greater<>().
#include <bits/stdc++.h>
using namespace std;

// Driver Code
int main()
{
    int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);

    stable_sort(arr, arr + n, greater<int>());

    cout << "Array after sorting : \n";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";

    return 0;
}
```

**Output**

```
Array after sorting : 
9 8 7 6 5 4 3 2 1 0 
```

### 什么时候更喜欢稳定排序而不是排序()？

有时我们希望确保排序数组中相等元素的**顺序与原始数组**中相同。如果这些值与其他字段相关联，这将非常有用。例如，

*   考虑按分数对学生进行排序，如果两个学生有相同的分数，我们可能希望让他们保持与输入时相同的顺序。详见【排序算法】中的[稳定性](https://www.geeksforgeeks.org/stability-in-sorting-algorithms/)。
*   考虑我们有按结束时间排序的时间间隔，我们想按开始时间排序。此外，如果两个开始时间相同，我们希望按照结束时间对它们进行排序。sort()不能保证这一点。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A C++ program to demonstrate STL stable_sort()
// to sort intervals according to start time.
#include <bits/stdc++.h>
using namespace std;

// An interval has start time and end time
struct Interval {
    int start, end;
};

// Compares two intervals according to starting
// times.
bool compareInterval(Interval i1, Interval i2)
{
    return (i1.start < i2.start);
}

int main()
{
    // Given intervals are sorted according to end time
    Interval arr[]
        = { { 1, 3 }, { 2, 4 }, { 1, 7 }, { 2, 19 } };
    int n = sizeof(arr) / sizeof(arr[0]);

    // sort the intervals in increasing order of
    // start time such that the start time intervals
    // appear in same order as in input.
    stable_sort(arr, arr + n, compareInterval);

    cout << "Intervals sorted by start time : \n";
    for (int i = 0; i < n; i++)
        cout << "[" << arr[i].start << ", " << arr[i].end
             << "] ";

    return 0;
}
```

**Output**

```
Intervals sorted by start time : 
[1, 3] [1, 7] [2, 4] [2, 19] 
```

### 排序和稳定排序的区别()

<figure class="table">

| 

钥匙

 | 

排序()

 | 

稳定排序()

 |
| --- | --- | --- |
| **实施** | sort()函数通常使用 [Introsort](https://www.geeksforgeeks.org/introsort-or-introspective-sort/) 。因此，sort()可能会保留语义等价值的物理顺序，但不能保证。 | stable_sort()函数通常使用 [mergesort](https://www.geeksforgeeks.org/merge-sort/) 。因此，stable_sort()保持语义等价值的物理顺序及其保证。 |
| **时间复杂度** | 是 **O(n*log(n))** 。 | 是**o(n*log^2(n)**。如果与长度成线性比例的额外内存不可用。如果可用，则为 0(n * log(n))。 |

</figure>

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
# 如何在 C++中找到数组中一个数字的最后一个索引

> 原文:[https://www . geeksforgeeks . org/如何查找 c 数组中最后一个数字的索引/](https://www.geeksforgeeks.org/how-to-find-last-index-of-a-number-in-an-array-in-c/)

给定一个由 **N** 整数和数字 **K** 组成的数组 **arr[]** ，任务是在 **arr[]** 中找到最后一个出现的 **K** 。如果元素不存在，则返回 **-1** 。
**示例:**

> **输入:** arr[] = {1，3，4，2，1，8}，K = 1
> **输出:** 4
> **说明:**
> 在索引 0 和索引 4 有两次出现 1。但是最后一次出现在索引 4。
> **输入:** arr[] = {3，4，5，6，7}，K = 2
> **输出:** -1
> **解释:**
> 因为数组中不存在 2。

**方法 1:** 使用[递归](https://www.geeksforgeeks.org/recursion/)

*   从给定数组的最后一个索引递归迭代:
    *   **基本情况:**如果我们递归地到达起始索引，这意味着给定的元素 **K** 不存在于数组中。

```
if(idx < 0) {
  return -1;
}
```

*   **返回语句:**如果递归调用中的当前元素等于 **K** ，则从函数返回当前索引。

```
if(arr[idx]==K) {
   return idx;
}
```

*   **递归调用:**如果当前索引处的元素不等于 **K** ，则递归调用进行下一次迭代。

```
return recursive_function(arr, idx - 1)
```

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to find the last
// index of the given number K
int findIndex(int arr[], int idx, int K)
{

    // Base Case
    if (idx < 0)
        return -1;

    // Return Statement
    if (arr[idx] == K) {
        return idx;
    }

    // Recursive Call
    return findIndex(arr, idx - 1, K);
}

// Driver Code
int main()
{

    int arr[] = { 3, 1, 4, 4, 2, 3, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 4;

    // Function call
    cout << findIndex(arr, N - 1, K);

    return 0;
}
```

**Output:** 

```
3
```

***时间复杂度:** O(N)，其中 N 为数组长度。*
**方法二:**使用内置函数 [find()](https://www.geeksforgeeks.org/std-find-in-cpp/) 和 [find_if()](https://www.geeksforgeeks.org/stdfind_if-stdfind_if_not-in-c/) :
思路是从数组末尾找到第一个元素，从数组开头找到最后一个元素。以下是步骤:

1.  [反转给定的数组](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)。
2.  使用 [find()函数](https://www.geeksforgeeks.org/std-find-in-cpp/)找到反向数组中第一个值为 **K** 的元素。
3.  如果 find 函数返回的迭代器指向数组的末尾，则该元素不在数组中。
4.  否则使用[距离()](https://www.geeksforgeeks.org/stddistance-in-c/)功能找到 **K** 在这个反转数组中的位置(比如**位置**)。
5.  获取给定数组打印中 K 的最后一个索引的距离**(N–pos–1)**。

下面是上述方法的实现:
使用 find()

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the last index of
// the given number K
int findIndex(int arr[], int N, int K)
{

    // Reverse the given array arr[]
    reverse(arr, arr + N);

    // Find the first occurrence of K
    // in this reversed array
    auto it = find(arr, arr + N, K);

    // If the element is not present
    // then return "-1"
    if (it == arr + N) {
        return -1;
    }

    // Else return the index found
    return (N - distance(arr, it) - 1);
}

// Driver Code
int main()
{

    int arr[] = { 3, 1, 4, 4, 2, 3, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 4;

    // Function call
    cout << findIndex(arr, N, K);

    return 0;
}
```

使用 find_if()

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Comparator structure for finding
// index of element with value K
struct comparator {

    int elem;
    comparator(int const& i)
        : elem(i)
    {
    }

    bool operator()(int const& i)
    {
        return (i == elem);
    }
};

// Function to find the last index of
// the given number K
int findIndex(int arr[], int N, int K)
{

    // Reverse the given array arr[]
    reverse(arr, arr + N);

    // Find the first occurrence of K
    // in this reversed array
    auto it = find_if(arr, arr + N,
                      comparator(K));

    // If the element is not present
    // then return "-1"
    if (it == arr + N) {
        return -1;
    }

    // Else return the index found
    return (N - distance(arr, it) - 1);
}

// Driver Code
int main()
{

    int arr[] = { 3, 1, 4, 4, 2, 3, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 4;

    // Function call
    cout << findIndex(arr, N, K);

    return 0;
}
```

**Output:** 

```
3
```

**时间复杂度:** *O(N)* ，其中 N 是给定数组中元素的个数。

**方法 3:** (迭代方式)

使用循环查找最后一个位置。

下面是上述方法的实现

## C++

```
// CPP program for the above approach
#include <iostream>
using namespace std;
int findIndex(int arr[], int idx, int K)
{

    // Traversing the array from
    // last position
    for (int i = idx; i >= 0; i--) {
        if (arr[i] == K)
            return i;
    }
    return -1;
}

// Driver Code
int main()
{

    int arr[] = { 3, 1, 4, 4, 2, 3, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 4;

    // Function call
    cout << findIndex(arr, N - 1, K);
    return 0;
}
```

**输出:**

```
3
```
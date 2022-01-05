# 在 C++中对向量进行切片

> 原文:[https://www.geeksforgeeks.org/slicing-a-vector-in-c/](https://www.geeksforgeeks.org/slicing-a-vector-in-c/)

**先决条件:**[c++中的向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)
对向量进行切片意味着从给定的向量中生成一个子向量。
给定向量[中的 N 个整数](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **arr** 和正数 **X 和 Y** ，任务是将给定向量从给定向量中的索引 **X 切分到 Y** 。
**举例:**

> **输入:**向量 arr = { 1，3，4，2，4，2，1 }，X = 2，Y = 5
> **输出:**4 2 4 2
> T6】输入:向量 arr = { 1，3，4，2 }，X = 1，Y = 2
> **输出:** 3 4

**方法 1:** 思路是将这个 X 到 Y 范围内的元素复制到一个新的向量中，并返回。

1.  获取索引 X 处元素的起始迭代器为:

```
auto start = arr.begin() + X
```

2.  获取索引 Y 处元素的结束迭代器为:

```
auto end = arr.begin() + Y + 1
```

2.  使用向量中的 [copy()函数在这些迭代器之间复制这些范围内的元素。](https://www.geeksforgeeks.org/ways-copy-vector-c/)

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to slice a given vector
// from range X to Y
vector<int> slicing(vector<int>& arr,
                    int X, int Y)
{

    // Starting and Ending iterators
    auto start = arr.begin() + X;
    auto end = arr.begin() + Y + 1;

    // To store the sliced vector
    vector<int> result(Y - X + 1);

    // Copy vector using copy function()
    copy(start, end, result.begin());

    // Return the final sliced vector
    return result;
}

// Function to print the vector ans
void printResult(vector<int>& ans)
{

    // Traverse the vector ans
    for (auto& it : ans) {

        // Print elements
        cout << it << ' ';
    }
}

// Driver Code
int main()
{

    // Given vector
    vector<int> arr = { 1, 3, 4, 2,
                        4, 2, 1 };

    // Given range
    int X = 2, Y = 5;

    // Function Call
    vector<int> ans;
    ans = slicing(arr, X, Y);

    // Print the sliced vector
    printResult(ans);
}
```

**Output:** 

```
4 2 4 2
```

**方法 2:** 上述方法可以使用范围构造器来实现。以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Template class to slice a vector
// from range X to Y
template <typename T>
vector<T> slicing(vector<T> const& v,
                  int X, int Y)
{

    // Begin and End iterator
    auto first = v.begin() + X;
    auto last = v.begin() + Y + 1;

    // Copy the element
    vector<T> vector(first, last);

    // Return the results
    return vector;
}

// Template class to print the element
// in vector v
template <typename T>
void printResult(vector<T> const& v)
{

    // Traverse the vector v
    for (auto i : v) {
        cout << i << ' ';
    }
    cout << '\n';
}

// Driver Code
int main()
{

    // Given vector
    vector<int> arr = { 1, 3, 4, 2,
                        4, 2, 1 };

    // Given range
    int X = 2, Y = 5;

    // To store the sliced vector
    vector<int> ans;

    // Function Call
    ans = slicing(arr, X, Y);

    // Print the sliced vector
    printResult(ans);
}
```

**Output:** 

```
4 2 4 2
```

**方法三:**我们还可以使用 C++ STL 中的内置函数 [slice()对给定的向量进行切片。以下是上述方法的实施:](https://www.geeksforgeeks.org/stdslice-valarray-slice-selector/) 

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include "bits/stdc++.h"
#include "valarray"
using namespace std;

// Function to slice the given array
// elements from range (X, Y)
valarray<int> slicing(valarray<int> arr,
                      int X, int Y)
{

    // Return the slicing of array
    return arr[slice(X, Y - X + 1, 1)];
}

// Print the resultant array
// after slicing
void printResult(valarray<int> v)
{

    // Traverse the vector v
    for (auto i : v) {
        cout << i << ' ';
    }
    cout << '\n';
}

// Driver Code
int main()
{

    // Given vector
    valarray<int> arr = { 1, 3, 4, 2,
                          4, 2, 1 };

    // Given range
    int X = 2, Y = 5;

    // To store the sliced vector
    valarray<int> ans;

    // Function Call
    ans = slicing(arr, X, Y);

    // Print the sliced vector
    printResult(ans);
}
```

**Output:** 

```
4 2 4 2
```
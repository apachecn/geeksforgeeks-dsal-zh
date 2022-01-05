# c++中对数组下界()和上界()的实现

> 原文:[https://www . geesforgeks . org/c 对数组中下限和上限的实现/](https://www.geeksforgeeks.org/implementation-of-lower_bound-and-upper_bound-in-array-of-pairs-in-c/)

在本文中，我们将讨论在由[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)中[下界()](https://www.geeksforgeeks.org/lower_bound-in-cpp/)和[上界()](https://www.geeksforgeeks.org/stdupper_bound-in-cpp/)的实现。

*   **下界():**它返回一个迭代器，指向范围**【第一个，最后一个】**中的第一个元素，该元素的值大于或等于给定值**【瓦尔】**。但是在对数组**中，**对(x，y)** 的下界()**将返回一个迭代器，指向第一个值大于或等于 **x** 而第二个值大于或等于 **y** 的对的位置。
    如果不满足上述标准，那么它返回一个迭代器到数组对中的索引。
*   **upper_bound():** 它返回一个迭代器，指向范围**【第一个，最后一个】**中的第一个元素，该元素的值大于给定值**【瓦尔】**。但是在对数组**中，**对的上限()**(x，y)** 将返回一个迭代器，指向第一个值大于 **x** 而第二个值大于 **y** 的对的位置。
    如果不满足上述标准，那么它返回一个迭代器到数组对中的索引。

**语法:**

> //对于下界
> 下界(array_name，array_name + array_size，value，comparator _ function)；
> 
> //对于上限
> 上限(array_name，array_name + array_size，value，comparator _ function)；

**参数:**成对数组中的函数**下界()**和**上界()**接受以下参数:

1.  **数组 _ 名称&数组 _ 大小:**表示**【开始，结束】**之间间隔的数组的名称和大小。
2.  **值:**范围内要搜索的下界()/上界()的值。
3.  **comparator_function:** 二元函数，接受两个参数作为其输入，即数组中的一个类型对的元素，第二个是必须找到其下界()/上界()的值，并返回一个布尔值。

**返回类型:**返回一个迭代器，指向数组中第一个参数大于或等于值的第一个元素。

下面是演示成对数组中的[下界()和上界()](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/)的程序:

## C++

```
// C++ program to demonstrate lower_bound()
// and upper_bound() in Array of Pairs
#include <bits/stdc++.h>
using namespace std;

// Function to implement lower_bound()
void findLowerBound(pair<int, int> arr[],
                    pair<int, int>& p,
                    int n)
{
    // Given iterator points to the
    // lower_bound() of given pair
    auto low = lower_bound(arr, arr + n, p);

    cout << "lower_bound() for {2, 5}"
         << " is at index: "
         << low - arr << endl;
}

// Function to implement upper_bound()
void findUpperBound(pair<int, int> arr[],
                    pair<int, int>& p,
                    int n)
{
    // Given iterator points to the
    // lower_bound() of given pair
    auto up = upper_bound(arr, arr + n, p);

    cout << "upper_bound() for {2, 5}"
         << " is at index: "
         << up - arr << endl;
}

// Driver Code
int main()
{
    // Given sorted array of Pairs
    pair<int, int> arr[]
        = { { 1, 3 }, { 1, 7 }, { 2, 4 },
            { 2, 5 }, { 3, 8 }, { 8, 6 } };

    // Given pair {2, 5}
    pair<int, int> p = { 2, 5 };

    // Size of array
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call to find lower_bound
    // of pair p in arr
    findLowerBound(arr, p, n);

    // Function Call to find upper_bound
    // of pair p in arr
    findUpperBound(arr, p, n);
    return 0;
}
```

**Output:**

```
lower_bound() for {2, 5} is at index: 3
upper_bound() for {2, 5} is at index: 4

```
# 找出每个数组元素左边最接近的值

> 原文:[https://www . geeksforgeeks . org/find-每一个数组元素左边的最近值÷/](https://www.geeksforgeeks.org/find-the-nearest-value-present-on-the-left-of-every-array-element/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，每个数组元素的任务是找到数组中最左边的非相等值。如果没有找到这样的元素，则打印 **-1**

**示例:**

> **输入:** arr[] = { 2，1，5，8，3 }
> **输出:** -1 2 2 5 2
> **解释:**
> 【<u>2</u>】，是这个前缀中唯一的数字。因此，答案是-1。
> 【2、 <u>1</u> 】，最接近 1 的数字是 2
> 【2、1、 <u>5</u> ，最接近 5 的数字是 2
> 【2、1、5、 <u>8</u> ，最接近 8 的数字是 5
> 【2、1、5、8、 <u>3</u> ，最接近 3 的数字是 2
> 
> **输入:** arr[] = {3，3，2，4，6，5，5，1}
> **输出:**-1-1 3 4 4 4 2
> **解释:**
> 【3】，它是这个前缀中唯一的数字。因此，答案是-1。
> 【3，3】，是这个前缀中唯一的数字。因此，答案是-1
> 【3，3，2】，最接近 2 的数字是 3
> 【3，3，2，4】，最接近 4 的数字是 3
> 【3，3，2，4，6】，最接近 6 的数字是 4
> 【3，3，2，4，6，5】，最接近 5 的数字是 4
> 【3，3，2，4，6，5，5】，最接近 5 的数字是 4
> 【3，3，2

**天真方法:**最简单的想法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个**I<sup>th</sup>T7】元素，找到索引 **i** 左侧最接近的元素，该元素不等于**arr【I】**。
***时间复杂度:** O(N^2)*
***辅助空间:** O(1)***

**有效方法:**

想法是[将给定数组的元素插入](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中，这样插入的数字被排序，然后对于一个整数，找到它的位置，并将其下一个值与前一个值进行比较，并打印两个值中更接近的值。
按照以下步骤解决问题:

*   初始化一组[整数 **S** 来存储](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)[排序顺序](https://www.geeksforgeeks.org/print-elements-sorted-order-row-culumn-wise-sorted-matrix/)中的元素。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**。
*   现在，找到最近的小于和大于**arr【I】**的值，分别说 **X** 和 **Y** 。
    *   如果找不到 **X** ，打印 **Y** 。
    *   如果找不到 **Y** ，打印 **Z** 。
    *   如果 **X** 和 **Y** 都找不到，打印**-1”**。
*   之后，如果**腹肌(X–arr[I])**小于**腹肌(Y–arr[I])**，则在[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/) **S** 中添加 **arr[i]** ，并打印 **X** 。否则，打印 **Y** 。
*   对每个元素重复上述步骤。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the closest number on
// the left side of x
void printClosest(set<int>& streamNumbers, int x)
{

    // Insert the value in set and store
    // its position
    auto it = streamNumbers.insert(x).first;

    // If x is the smallest element in set
    if (it == streamNumbers.begin())
    {
        // If count of elements in the set
        // equal to 1
        if (next(it) == streamNumbers.end())
        {

            cout << "-1 ";
            return;
        }

        // Otherwise, print its
        // immediate greater element
        int rightVal = *next(it);
        cout << rightVal << " ";
        return;
    }

    // Store its immediate smaller element
    int leftVal = *prev(it);

    // If immediate greater element does not
    // exists print it's immediate
    // smaller element
    if (next(it) == streamNumbers.end()) {
        cout << leftVal << " ";
        return;
    }

    // Store the immediate
    // greater element
    int rightVal = *next(it);

    // Print the closest number
    if (x - leftVal <= rightVal - x)
        cout << leftVal << " ";
    else
        cout << rightVal << " ";
}

// Driver Code
int main()
{

    // Given array
    vector<int> arr = { 3, 3, 2, 4, 6, 5, 5, 1 };

    // Initialize set
    set<int> streamNumbers;

    // Print Answer
    for (int i = 0; i < arr.size(); i++) {

        // Function Call
        printClosest(streamNumbers, arr[i]);
    }

    return 0;
}
```

**Output**

```
-1 -1 3 3 4 4 4 2 
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*
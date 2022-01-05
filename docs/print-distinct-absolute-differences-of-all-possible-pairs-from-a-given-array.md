# 打印给定数组中所有可能对的明显绝对差异

> 原文:[https://www . geeksforgeeks . org/print-distinct-给定数组中所有可能对的绝对差异/](https://www.geeksforgeeks.org/print-distinct-absolute-differences-of-all-possible-pairs-from-a-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是找出给定数组中所有可能对的明显绝对差异。

**示例:**

> **输入:** arr[] = { 1，3，6 }
> **输出:** 2 3 5
> **解释:**T8】ABS(arr[0]–arr[1])= 2
> ABS(arr[1]–arr[2])= 3
> ABS(arr[0]–arr[2])= 5
> 
> **输入:** arr[] = { 5，6，7，8，14，19，21，22 }
> **输出:**1 2 3 5 7 8 9 11 12 13 14 15 16 17

**天真方法:**解决这个问题最简单的方法是[生成给定数组的所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)和[在一个](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中插入每对的绝对差。最后，打印集合的所有元素。
***时间复杂度:**O(N<sup>2</sup>* log(N)*
***辅助空间:** O(N <sup>2</sup> )*

**方法:**上述方法可以使用[位组](https://www.geeksforgeeks.org/c-bitset-and-its-application/)进行优化。按照以下步骤解决问题:

*   初始化一个[位组](https://www.geeksforgeeks.org/c-bitset-and-its-application/)，比如 **bset** ，其中**bset【I】**检查数组中是否存在 **i** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并将所有数组元素存储在 **bset** 中。
*   初始化一个[位集](https://www.geeksforgeeks.org/c-bitset-and-its-application/)，比如 **diff** ，其中**diff【I】**存储数组中是否存在任何值等于 **i** 的对的绝对差。
*   [找到数组中最大的元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)，说 **Max**
*   迭代范围**【0，最大】**。在每次**I<sup>th</sup>T5】迭代中，检查**bset【I】**是否为真。如果发现为真，则使用**diff = diff |(bset>>I)**插入 **i** 与所有其他数组元素的绝对差。**
*   最后，迭代范围**【0，最大】**，检查**差值【I】**是否为真。如果发现是真的，那就打印 **i** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define Max 100005

// Function to find all distinct
// absolute difference of all
// possible pairs of the array
void printUniqDif(int n, int a[])
{

    // bset[i]: Check if i is present
    // in the array or not
    bitset<Max> bset;

    // diff[i]: Check if there exists a
    // pair whose absolute difference is i
    bitset<Max> diff;

    // Traverse the array, arr[]
    for (int i = 0; i < n; i++) {

        // Add in bitset
        bset.set(a[i]);
    }

    // Iterate over the range[0, Max]
    for (int i = 0; i <= Max; i++) {

        // If i-th bit is set
        if (bset[i]) {

            // Insert the absolute difference
            // of all possible pairs whose
            // first element is arr[i]
            diff = diff | (bset >> i);
        }
    }

    // Stores count of set bits
    int X = bset.count();

    // If there is at least one
    // duplicate element in arr[]
    if (X != n) {

        cout << 0 << " ";
    }

    // Printing the distinct absolute
    // differences of all possible pairs
    for (int i = 1; i <= Max; i++) {

        // If i-th bit is set
        if (diff[i]) {
            cout << i << " ";
        }
    }
}

// Driver Code
int main()
{

    // Given array
    int a[] = { 1, 4, 6 };

    // Given size
    int n = sizeof(a) / sizeof(a[0]);

    // Function Call
    printUniqDif(n, a);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
Max = 100005

# Function to find all distinct
# absolute difference of all
# possible pairs of the array
def printUniqDif(n, a):

    # bset[i]: Check if i is present
    # in the array or not
    bset = [0 for i in range(33)]

    # diff[i]: Check if there exists a
    # pair whose absolute difference is i
    diff = 0

    # Traverse the array, arr[]
    for i in range(n):
        bset[a[i]] = 1

    # Iterate over the range[0, Max]
    d = 0

    for i in range(1,33):
        d = d | (bset[i]<<i)

    for i in range(33):

        # If i-th bit is set
        if (bset[i]):

            # Insert the absolute difference
            # of all possible pairs whose
            # first element is arr[i]
            diff = diff | d >> i
            # print(bin(diff))

    # Stores count of set bits
    X, Y = bset.count(1), str(bin(diff)[2:])

    # If there is at least one
    # duplicate element in arr[]
    if (X != n):

        print(0, end=" ")

    # Printing the distinct absolute
    # differences of all possible pairs
    for i in range(1, len(Y)):

        # If i-th bit is set
        if (Y[i] == '1'):
            print(i, end = " ")
# Driver Code
if __name__ == '__main__':

    # Given array
    a = [1, 4, 6]

    # Given size
    n = len(a)

    # Function Call
    printUniqDif(n, a)

    # This code is contributed by mohit kumar 29
```

**Output:** 

```
2 3 5
```

***时间复杂度:** O(N + Max)，其中 **Max** 是数组中最大的元素。*
***辅助空间:** O(最大)*
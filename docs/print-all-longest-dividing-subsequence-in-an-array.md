# 打印数组中所有最长的分割子序列

> 原文:[https://www . geesforgeks . org/print-all-最长除法-数组中的子序列/](https://www.geeksforgeeks.org/print-all-longest-dividing-subsequence-in-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是打印由给定数组形成的[个最长分割子序列](https://www.geeksforgeeks.org/longest-dividing-subsequence/)的所有元素。如果我们有一个以上最大长度的序列，那么打印所有的序列。

**示例:**

> **输入:** arr[] = { 2，11，16，12，36，60，71 }
> **输出:**
> 2 12 36
> 2 12 60
> **说明:**
> 有两个子序列，最大长度为 3。
> 1。2、12、36
> 2。2, 12, 60
> 
> **输入:** arr[] = { 2，4，16，32，64，60，12 }；
> **输出:**
> 2 4 16 32 64
> **解释:**
> 最大长度 5 的子序列只有一个。
> 1。2 4 16 32 64

**进场:**

1.  声明一个存储最长分割子序列的 2D 数组 **LDS[][]** 。
2.  遍历给定的数组 **arr[]** ，并使用本文[中讨论的方法找到直到当前元素的最长分割子序列。](https://www.geeksforgeeks.org/longest-dividing-subsequence/)
3.  遍历给定的 **LDS[][]** 数组，打印序列中所有长度最大的元素。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to print LDS[i] element
void printLDS(vector<int>& Max)
{

    // Traverse the Max[]
    for (auto& it : Max) {
        cout << it << ' ';
    }
}

// Function to construct and print Longest
// Dividing Subsequence
void LongestDividingSeq(int arr[], int N)
{
    // 2D vector for storing sequences
    vector<vector<int> > LDS(N);

    // Push the first element to LDS[][]
    LDS[0].push_back(arr[0]);

    // Iterate over all element
    for (int i = 1; i < N; i++) {

        // Loop for every index till i
        for (int j = 0; j < i; j++) {

            // if current elements divides
            // arr[i] and length is greater
            // than the previous index, then
            // insert the current element
            // to the sequences LDS[i]
            if ((arr[i] % arr[j] == 0)
                && (LDS[i].size() < LDS[j].size() + 1))
                LDS[i] = LDS[j];
        }

        // L[i] ends with arr[i]
        LDS[i].push_back(arr[i]);
    }

    int maxLength = 0;

    // LDS stores the sequences till
    // each element of arr[]
    // Traverse the LDS[][] to find the
    // the maximum length
    for (int i = 0; i < N; i++) {
        int x = LDS[i].size();
        maxLength = max(maxLength, x);
    }

    // Print all LDS with maximum length
    for (int i = 0; i < N; i++) {

        // Find size
        int size = LDS[i].size();

        // If size = maxLength
        if (size == maxLength) {

            // Print LDS
            printLDS(LDS[i]);
            cout << '\n';
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 11, 16, 12, 36, 60, 71 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    LongestDividingSeq(arr, N);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print LDS[i] element
def printLDS(Max):

    # Traverse the Max[]
    for it in Max:
        print(it, end = " ")

# Function to construct and print 
# Longest Dividing Subsequence
def LongestDividingSeq(arr, N):

    # 2D vector for storing sequences
    LDS = [[] for i in range(N)]

    # Push the first element to LDS[][]
    LDS[0].append(arr[0])

    # Iterate over all element
    for i in range(1, N):

        # Loop for every index till i
        for j in range(i):

            # If current elements divides
            # arr[i] and length is greater
            # than the previous index, then
            # insert the current element
            # to the sequences LDS[i]
            if ((arr[i] % arr[j] == 0) and
                (len(LDS[i]) < len(LDS[j]) + 1)):
                LDS[i] = LDS[j].copy()

        # L[i] ends with arr[i]
        LDS[i].append(arr[i])

    maxLength = 0

    # LDS stores the sequences till
    # each element of arr[]
    # Traverse the LDS[][] to find 
    # the maximum length
    for i in range(N):
        x = len(LDS[i])
        maxLength = max(maxLength, x)

    # Print all LDS with maximum length
    for i in range(N):

        # Find size
        size = len(LDS[i])

        # If size = maxLength
        if (size == maxLength):

            # Print LDS
            printLDS(LDS[i])
            print()

# Driver Code
arr = [ 2, 11, 16, 12, 36, 60, 71 ]
N = len(arr)

# Function call
LongestDividingSeq(arr, N);

# This code is contributed by ANKITKUMAR34
```

**Output:**

```
2 12 36 
2 12 60

```

 ***时间复杂度:** O(N <sup>2</sup> )
**辅助空间:** O(N <sup>2</sup> )*
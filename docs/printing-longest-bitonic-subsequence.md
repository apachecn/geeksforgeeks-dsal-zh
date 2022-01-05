# 打印最长的双音素子序列

> 原文:[https://www . geesforgeks . org/printing-long-bitonic-subsequence/](https://www.geeksforgeeks.org/printing-longest-bitonic-subsequence/)

最长双调和子序列问题是找到给定序列的最长子序列，使它先增加后减少。按递增顺序排序的序列被认为是双音素的，递减部分为空。类似地，递减顺序被认为是 Bitonic，递增部分为空。

**示例:**

```
Input:  [1, 11, 2, 10, 4, 5, 2, 1]
Output: [1, 2, 10, 4, 2, 1] OR [1, 11, 10, 5, 2, 1] 
    OR [1, 2, 4, 5, 2, 1]

Input:  [12, 11, 40, 5, 3, 1]
Output: [12, 11, 5, 3, 1] OR [12, 40, 5, 3, 1]

Input:  [80, 60, 30, 40, 20, 10]
Output: [80, 60, 30, 20, 10] OR [80, 60, 40, 20, 10]

```

在[之前的](https://www.geeksforgeeks.org/dynamic-programming-set-15-longest-bitonic-subsequence/)帖子中，我们已经讨论了最长双调和子序列问题。然而，这篇文章只涵盖了与求增子序列的最大和有关的代码，而没有涉及子序列的构造。在这篇文章中，我们将讨论如何构造最长的双调和子序列本身。

让 arr[0..n-1]是输入数组。我们定义向量 LIS 使得 LIS[i]本身是一个存储 arr[0]的最长递增子序列的向量..那以逮捕结束。因此，对于索引 I，LIS[i]可以递归地写成–

```
LIS[0] = {arr[O]}
LIS[i] = {Max(LIS[j])} + arr[i] where j < i and arr[j] < arr[i] 
       = arr[i], if there is no such j

```

我们还定义了一个向量 LDS，使得 LDS[i]本身是一个存储 arr[I]的最长递减子序列的向量..那从 arr[i]开始。因此，对于索引 I，LDS[i]可以递归地写成–

```
LDS[n] = {arr[n]}
LDS[i] = arr[i] + {Max(LDS[j])} where j > i and arr[j] < arr[i] 
       = arr[i], if there is no such j

```

例如，对于数组[1 11 2 10 4 5 2 1]，

```
LIS[0]: 1
LIS[1]: 1 11
LIS[2]: 1 2
LIS[3]: 1 2 10
LIS[4]: 1 2 4
LIS[5]: 1 2 4 5
LIS[6]: 1 2
LIS[7]: 1

```

```
LDS[0]: 1
LDS[1]: 11 10 5 2 1
LDS[2]: 2 1
LDS[3]: 10 5 2 1
LDS[4]: 4 2 1
LDS[5]: 5 2 1
LDS[6]: 2 1
LDS[7]: 1

```

因此，最长双调和子序列可以是

```
LIS[1] + LDS[1] = [1 11 10 5 2 1]        OR
LIS[3] + LDS[3] = [1 2 10 5 2 1]        OR
LIS[5] + LDS[5] = [1 2 4 5 2 1]

```

以下是上述想法的实现–

## C++

```
/* Dynamic Programming solution to print Longest
   Bitonic Subsequence */
#include <bits/stdc++.h>
using namespace std;

// Utility function to print Longest Bitonic
// Subsequence
void print(vector<int>& arr, int size)
{
    for(int i = 0; i < size; i++)
        cout << arr[i] << " ";
}

// Function to construct and print Longest
// Bitonic Subsequence
void printLBS(int arr[], int n)
{
    // LIS[i] stores the length of the longest
    // increasing subsequence ending with arr[i]
    vector<vector<int>> LIS(n);

    // initialize LIS[0] to arr[0]
    LIS[0].push_back(arr[0]);

    // Compute LIS values from left to right
    for (int i = 1; i < n; i++)
    {
        // for every j less than i
        for (int j = 0; j < i; j++)
        {
            if ((arr[j] < arr[i]) &&
                (LIS[j].size() > LIS[i].size()))
                LIS[i] = LIS[j];
        }
        LIS[i].push_back(arr[i]);
    }

    /* LIS[i] now stores Maximum Increasing
       Subsequence of arr[0..i] that ends with
       arr[i] */

    // LDS[i] stores the length of the longest
    // decreasing subsequence starting with arr[i]
    vector<vector<int>> LDS(n);

    // initialize LDS[n-1] to arr[n-1]
    LDS[n - 1].push_back(arr[n - 1]);

    // Compute LDS values from right to left
    for (int i = n - 2; i >= 0; i--)
    {
        // for every j greater than i
        for (int j = n - 1; j > i; j--)
        {
            if ((arr[j] < arr[i]) &&
                (LDS[j].size() > LDS[i].size()))
                LDS[i] = LDS[j];
        }
        LDS[i].push_back(arr[i]);
    }

    // reverse as vector as we're inserting at end
    for (int i = 0; i < n; i++)
        reverse(LDS[i].begin(), LDS[i].end());

    /* LDS[i] now stores Maximum Decreasing Subsequence
       of arr[i..n] that starts with arr[i] */

    int max = 0;
    int maxIndex = -1;

    for (int i = 0; i < n; i++)
    {
        // Find maximum value of size of LIS[i] + size
        // of LDS[i] - 1
        if (LIS[i].size() + LDS[i].size() - 1 > max)
        {
            max = LIS[i].size() + LDS[i].size() - 1;
            maxIndex = i;
        }
    }

    // print all but last element of LIS[maxIndex] vector
    print(LIS[maxIndex], LIS[maxIndex].size() - 1);

    // print all elements of LDS[maxIndex] vector
    print(LDS[maxIndex], LDS[maxIndex].size());
}

// Driver program
int main()
{
    int arr[] = { 1, 11, 2, 10, 4, 5, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printLBS(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Dynamic Programming solution to print Longest 
Bitonic Subsequence */
import java.util.*;

class GFG 
{

    // Utility function to print Longest Bitonic
    // Subsequence
    static void print(Vector<Integer> arr, int size) 
    {
        for (int i = 0; i < size; i++)
            System.out.print(arr.elementAt(i) + " ");
    }

    // Function to construct and print Longest
    // Bitonic Subsequence
    static void printLBS(int[] arr, int n) 
    {

        // LIS[i] stores the length of the longest
        // increasing subsequence ending with arr[i]
        @SuppressWarnings("unchecked")
        Vector<Integer>[] LIS = new Vector[n];

        for (int i = 0; i < n; i++)
            LIS[i] = new Vector<>();

        // initialize LIS[0] to arr[0]
        LIS[0].add(arr[0]);

        // Compute LIS values from left to right
        for (int i = 1; i < n; i++) 
        {

            // for every j less than i
            for (int j = 0; j < i; j++) 
            {

                if ((arr[i] > arr[j]) && 
                     LIS[j].size() > LIS[i].size()) 
                {
                    for (int k : LIS[j])
                        if (!LIS[i].contains(k))
                            LIS[i].add(k);
                }
            }
            LIS[i].add(arr[i]);
        }

        /*
        * LIS[i] now stores Maximum Increasing Subsequence 
        * of arr[0..i] that ends with arr[i]
        */

        // LDS[i] stores the length of the longest
        // decreasing subsequence starting with arr[i]
        @SuppressWarnings("unchecked")
        Vector<Integer>[] LDS = new Vector[n];

        for (int i = 0; i < n; i++)
            LDS[i] = new Vector<>();

        // initialize LDS[n-1] to arr[n-1]
        LDS[n - 1].add(arr[n - 1]);

        // Compute LDS values from right to left
        for (int i = n - 2; i >= 0; i--) 
        {

            // for every j greater than i
            for (int j = n - 1; j > i; j--) 
            {
                if (arr[j] < arr[i] && 
                    LDS[j].size() > LDS[i].size())
                    for (int k : LDS[j])
                        if (!LDS[i].contains(k))
                            LDS[i].add(k);
            }
            LDS[i].add(arr[i]);
        }

        // reverse as vector as we're inserting at end
        for (int i = 0; i < n; i++)
            Collections.reverse(LDS[i]);

        /*
        * LDS[i] now stores Maximum Decreasing Subsequence 
        * of arr[i..n] that starts with arr[i]
        */
        int max = 0;
        int maxIndex = -1;
        for (int i = 0; i < n; i++)
        {

            // Find maximum value of size of 
            // LIS[i] + size of LDS[i] - 1
            if (LIS[i].size() + LDS[i].size() - 1 > max)
            {
                max = LIS[i].size() + LDS[i].size() - 1;
                maxIndex = i;
            }
        }

        // print all but last element of LIS[maxIndex] vector
        print(LIS[maxIndex], LIS[maxIndex].size() - 1);

        // print all elements of LDS[maxIndex] vector
        print(LDS[maxIndex], LDS[maxIndex].size());
    }

    // Driver Code
    public static void main(String[] args) 
    {
        int[] arr = { 1, 11, 2, 10, 4, 5, 2, 1 };
        int n = arr.length;

        printLBS(arr, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Dynamic Programming solution to print Longest
# Bitonic Subsequence

def _print(arr: list, size: int):
    for i in range(size):
        print(arr[i], end=" ")

# Function to construct and print Longest
# Bitonic Subsequence
def printLBS(arr: list, n: int):

    # LIS[i] stores the length of the longest
    # increasing subsequence ending with arr[i]
    LIS = [0] * n
    for i in range(n):
        LIS[i] = []

    # initialize LIS[0] to arr[0]
    LIS[0].append(arr[0])

    # Compute LIS values from left to right
    for i in range(1, n):

        # for every j less than i
        for j in range(i):

            if ((arr[j] < arr[i]) and (len(LIS[j]) > len(LIS[i]))):
                LIS[i] = LIS[j].copy()

        LIS[i].append(arr[i])

    # LIS[i] now stores Maximum Increasing
    # Subsequence of arr[0..i] that ends with
    # arr[i]

    # LDS[i] stores the length of the longest
    # decreasing subsequence starting with arr[i]
    LDS = [0] * n
    for i in range(n):
        LDS[i] = []

    # initialize LDS[n-1] to arr[n-1]
    LDS[n - 1].append(arr[n - 1])

    # Compute LDS values from right to left
    for i in range(n - 2, -1, -1):

        # for every j greater than i
        for j in range(n - 1, i, -1):

            if ((arr[j] < arr[i]) and (len(LDS[j]) > len(LDS[i]))):
                LDS[i] = LDS[j].copy()

        LDS[i].append(arr[i])

    # reverse as vector as we're inserting at end
    for i in range(n):
        LDS[i] = list(reversed(LDS[i]))

    # LDS[i] now stores Maximum Decreasing Subsequence
    # of arr[i..n] that starts with arr[i]

    max = 0
    maxIndex = -1

    for i in range(n):

        # Find maximum value of size of LIS[i] + size
        # of LDS[i] - 1
        if (len(LIS[i]) + len(LDS[i]) - 1 > max):

            max = len(LIS[i]) + len(LDS[i]) - 1
            maxIndex = i

    # print all but last element of LIS[maxIndex] vector
    _print(LIS[maxIndex], len(LIS[maxIndex]) - 1)

    # print all elements of LDS[maxIndex] vector
    _print(LDS[maxIndex], len(LDS[maxIndex]))

# Driver Code
if __name__ == "__main__":

    arr = [1, 11, 2, 10, 4, 5, 2, 1]
    n = len(arr)

    printLBS(arr, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
/* Dynamic Programming solution to print longest 
Bitonic Subsequence */
using System;
using System.Linq;
using System.Collections.Generic;

class GFG 
{

    // Utility function to print longest Bitonic
    // Subsequence
    static void print(List<int> arr, int size) 
    {
        for (int i = 0; i < size; i++)
            Console.Write(arr[i] + " ");
    }

    // Function to construct and print longest
    // Bitonic Subsequence
    static void printLBS(int[] arr, int n) 
    {

        // LIS[i] stores the length of the longest
        // increasing subsequence ending with arr[i]
        List<int>[] LIS = new List<int>[n];

        for (int i = 0; i < n; i++)
            LIS[i] = new List<int>();

        // initialize LIS[0] to arr[0]
        LIS[0].Add(arr[0]);

        // Compute LIS values from left to right
        for (int i = 1; i < n; i++) 
        {

            // for every j less than i
            for (int j = 0; j < i; j++) 
            {

                if ((arr[i] > arr[j]) && 
                    LIS[j].Count > LIS[i].Count) 
                {
                    foreach (int k in LIS[j])
                        if (!LIS[i].Contains(k))
                            LIS[i].Add(k);
                }
            }
            LIS[i].Add(arr[i]);
        }

        /*
        * LIS[i] now stores Maximum Increasing Subsequence 
        * of arr[0..i] that ends with arr[i]
        */

        // LDS[i] stores the length of the longest
        // decreasing subsequence starting with arr[i]
        List<int>[] LDS = new List<int>[n];

        for (int i = 0; i < n; i++)
            LDS[i] = new List<int>();

        // initialize LDS[n-1] to arr[n-1]
        LDS[n - 1].Add(arr[n - 1]);

        // Compute LDS values from right to left
        for (int i = n - 2; i >= 0; i--) 
        {

            // for every j greater than i
            for (int j = n - 1; j > i; j--) 
            {
                if (arr[j] < arr[i] && 
                    LDS[j].Count > LDS[i].Count)
                    foreach (int k in LDS[j])
                        if (!LDS[i].Contains(k))
                            LDS[i].Add(k);
            }
            LDS[i].Add(arr[i]);
        }

        // reverse as vector as we're inserting at end
        for (int i = 0; i < n; i++)
            LDS[i].Reverse();

        /*
        * LDS[i] now stores Maximum Decreasing Subsequence 
        * of arr[i..n] that starts with arr[i]
        */
        int max = 0;     
        int maxIndex = -1;
        for (int i = 0; i < n; i++)
        {

            // Find maximum value of size of 
            // LIS[i] + size of LDS[i] - 1
            if (LIS[i].Count + LDS[i].Count - 1 > max)
            {
                max = LIS[i].Count + LDS[i].Count - 1;
                maxIndex = i;
            }
        }

        // print all but last element of LIS[maxIndex] vector
        print(LIS[maxIndex], LIS[maxIndex].Count - 1);

        // print all elements of LDS[maxIndex] vector
        print(LDS[maxIndex], LDS[maxIndex].Count);
    }

    // Driver Code
    public static void Main(String[] args) 
    {
        int[] arr = { 1, 11, 2, 10, 4, 5, 2, 1 };
        int n = arr.Length;

        printLBS(arr, n);
    }
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
1 11 10 5 2 1

```

以上动态规划解的**时间复杂度**为 O(n <sup>2</sup> )。
**程序使用的辅助空间**为 O(n <sup>2</sup> )。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
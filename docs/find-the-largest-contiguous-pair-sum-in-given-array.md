# 找出给定数组中最大的连续对和

> 原文:[https://www . geesforgeks . org/find-给定数组中最大的连续对和/](https://www.geeksforgeeks.org/find-the-largest-contiguous-pair-sum-in-given-array/)

给定大小为 **N** 的整数数组 **arr[]** ，任务是找到相邻的对 **{a，b}** ，使得对中两个元素的总和最大。如果有多个这样的最大和对，则打印任何这样的对。对于总和最大的多对，打印其中任何一对。
**举例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 3 4
> **解释:**
> 在这里，数组中连续的对是:
> {1，2} - > Sum 3
> {2，3} - > Sum 5
> {3，4} - > Sum 7
> Maxiumum sum 为 **7** 对是
> **输入:** arr[] = {11，-5，9，-3，2}
> **输出:** 11 -5
> 具有各自和的邻接对是:
> {11，-5} - >和 6
> {-5，9} - >和 4
> {9，-3} - >和 6
> {-3，2} - >和-1【T37】

**进场:**
按照以下步骤解决问题:

1.  逐一生成所有连续的对，并计算其总和。
2.  将每对的总和与最大总和进行比较，并相应地更新与最大总和对应的对。
3.  返回代表最大和的对。

以下是上述方法的实现:

## C++

```
// C++ program to find the
// a contiguous pair from the
// which has the largest sum
#include <bits/stdc++.h>
using namespace std;

// Function to find and return
// the largest sum contiguous pair
vector<int> largestSumpair(int arr[], int n)
{

    // Stores the contiguous pair
    vector<int> pair;

    // Initialize maximum sum
    int max_sum = INT_MIN, i;

    for (i = 1; i < n; i++) {

        // Compare sum of pair with max_sum
        if (max_sum < (arr[i] + arr[i - 1])) {
            max_sum = arr[i] + arr[i - 1];
            if (pair.empty()) {

                // Insert the pair
                pair.push_back(arr[i - 1]);
                pair.push_back(arr[i]);
            }
            else {
                pair[0] = arr[i - 1];
                pair[1] = arr[i];
            }
        }
    }
    return pair;
}

// Driver Code
int main()
{
    int arr[] = { 11, -5, 9, -3, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    vector<int> pair = largestSumpair(arr, N);
    for (auto it = pair.begin(); it != pair.end(); ++it) {
        cout << *it << ' ';
    }

    return 0;
}

// This code is contributed by shubhamsingh10
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// a contiguous pair from the
// which has the largest sum
import java.util.*;

class GFG {

    // Function to find and return
    // the largest sum contiguous pair
    public static Vector<Integer> largestSumpair(int[] arr,
                                                 int n)
    {

        // Stores the contiguous pair
        Vector<Integer> pair = new Vector<Integer>();

        // Initialize maximum sum
        int max_sum = Integer.MIN_VALUE, i;

        for (i = 1; i < n; i++) {

            // Compare sum of pair with max_sum
            if (max_sum < (arr[i] + arr[i - 1])) {
                max_sum = arr[i] + arr[i - 1];

                if (pair.isEmpty()) {

                    // Insert the pair
                    pair.add(arr[i - 1]);
                    pair.add(arr[i]);
                }
                else {
                    pair.set(0, arr[i - 1]);
                    pair.set(1, arr[i]);
                }
            }
        }
        return pair;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 11, -5, 9, -3, 2 };
        int N = arr.length;

        Vector<Integer> pair = new Vector<Integer>();
        pair = largestSumpair(arr, N);
        for (Integer it : pair) {
            System.out.print(it + " ");
        }
    }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find the
# a contiguous pair from the
# which has the largest sum

# importing sys
import sys

# Function to find and return
# the largest sum contiguous pair

def largestSumpair(arr, n):
    # Stores the contiguous pair
    pair = []

# Initialize maximum sum
    max_sum = -sys.maxsize-1

    for i in range(1, n):

        # Compare sum of pair with max_sum
        if max_sum < (arr[i] + arr[i-1]):
            max_sum = arr[i] + arr[i-1]

            if pair == []:
                # Insert the pair
                pair.append(arr[i-1])
                pair.append(arr[i])
            else:
                pair[0] = arr[i-1]
                pair[1] = arr[i]

    return pair

# Driver Code
arr = [11, -5, 9, -3, 2]
N = len(arr)
pair = largestSumpair(arr, N)
print(pair[0], end=" ")
print(pair[1], end=" ")
```

## C#

```
// C# program to find the
// a contiguous pair from the
// which has the largest sum
using System;
using System.Collections;
using System.Collections.Generic;

class GFG {

    // Function to find and return
    // the largest sum contiguous pair
    public static ArrayList largestSumpair(int[] arr, int n)
    {

        // Stores the contiguous pair
        ArrayList pair = new ArrayList();

        // Initialize maximum sum
        int max_sum = int.MinValue, i;

        for (i = 1; i < n; i++) {

            // Compare sum of pair with max_sum
            if (max_sum < (arr[i] + arr[i - 1])) {
                max_sum = arr[i] + arr[i - 1];

                if (pair.Count == 0) {

                    // Insert the pair
                    pair.Add(arr[i - 1]);
                    pair.Add(arr[i]);
                }
                else {
                    pair[0] = arr[i - 1];
                    pair[1] = arr[i];
                }
            }
        }
        return pair;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int[] arr = { 11, -5, 9, -3, 2 };
        int N = arr.Length;

        ArrayList pair = new ArrayList();
        pair = largestSumpair(arr, N);

        foreach(int it in pair) { Console.Write(it + " "); }
    }
}

// This code is contributed by rutvik_56
```

**Output:** 

```
11 -5
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*
# 生成一个由最频繁出现在每个数组元素右侧的较大元素组成的数组

> 原文:[https://www . geesforgeks . org/generate-a-array-由最频繁出现的较大元素组成-出现在每个数组元素的右侧/](https://www.geeksforgeeks.org/generate-an-array-consisting-of-most-frequent-greater-elements-present-on-the-right-side-of-each-array-element/)

给定大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **A[]** ，任务是基于以下条件生成阵列 **B[]** :

*   对于每个数组元素 **A[i]** ，找出出现在 **A[i]右侧的大于 **A[i]** 的最频繁元素。**将该元素插入 **B[]** 。
*   如果右侧存在多个这样的元素，请选择具有最小值的元素。
*   如果在 **A[i]** 、**T5】右侧没有大于 **A[i]** 的元素，则将 **-1** 插入 **B[]** 。**

最后打印得到的数组 **B[]** 。

**示例:**

> **输入:** A[] = {4，5，2，25，10，5，10，3，10，5}
> **输出:** 5，10，10，-1，-1，10，-1，5，-1，-1
> **解释:**
> **A[0] (= 4):** 大于 4 的数组元素为{5，25，10}。由于 5 出现的次数最多，因此设置 B[0] = 5。
> **A[1] (= 5):** 大于 5 的数组元素为{25，10}。由于 10 出现的次数最多，因此将 B[1] = 10。
> **A[2] (= 2):** 大于 2 的数组元素为{5，25，10}。由于 10 出现的次数最多，因此将 B[2] = 10。
> **A[3] (= 25):** 在其右侧未发现大于 A[3]的元素。因此，设置 B[3] = -1。
> **A[4] (= 10):** 在其右侧未发现大于 A[4]的元素。因此，设置 B[4] = -1。
> 同样，设置 B[5] = 10，B[6] = -1，B[7] = 5，B[8] = -1，B[9] = -1。
> 所以得到的数组是 B[] = {5，10，10，-1，-1，10，-1，5，-1，-1}。
> 
> **输入:** A[] = {1，1，3，3，2，2}
> 输出: 2，2，-1，-1，-1

**天真方法:**按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如 **V、**来存储结果数组元素。
*   [使用变量遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**A【】**，说出 **i** ，并执行以下操作:
    *   将变量**和**初始化为 **-1** ，将**频率**初始化为 **0，**存储当前索引及其频率的结果。
    *   [使用变量迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，N-1】**，比如 **j** ，并执行以下操作:
        *   如果 **A[j] ≤ A[i]** 的频率，则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
        *   否则，检查**A【j】>的频率是否为**。如果发现为真，则将 **ans** 更新为**A【j】**并将 **freq** 更新为**A【j】**的频率。
        *   否则，如果**A【j】**的频率等于 **freq** ，则更新 **ans** 为**A【j】**和 **ans** 中的较小值。
    *   将**和**的值插入到数组中， **V** 。
*   打印数组，结果为 **V** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate an array containing
// the most frequent greater element on the
// right side of each array element
void findArray(int arr[], int n)
{
    // Stores the generated array
    vector<int> v;

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {

        // Store the result for the
        // current index and its frequency
        int ans = -1, old_c = 0;

        // Iterate over the right subarray
        for (int j = i + 1; j < n; j++) {

            if (arr[j] > arr[i]) {

                // Store the frequency of
                // the current array element
                int curr_c
                    = count(&arr[j], &arr[n], arr[j]);

                // If the frequencies are equal
                if (curr_c == old_c) {

                    // Update ans to smaller
                    // of the two elements
                    if (arr[j] < ans)
                        ans = arr[j];
                }

                // If count of new element
                // is more than count of ans
                if (curr_c > old_c) {
                    ans = arr[j];
                    old_c = curr_c;
                }
            }
        }

        // Insert answer in the array
        v.push_back(ans);
    }

    // Print the resultant array
    for (int i = 0; i < v.size(); i++)
        cout << v[i] << " ";
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 4, 5, 2, 25, 10, 5,
                  10, 3, 10, 5 };
    int size = sizeof(arr)
               / sizeof(arr[0]);

    findArray(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to generate an array containing
// the most frequent greater element on the
// right side of each array element
static void findArray(int arr[], int n)
{

    // Stores the generated array
    Vector<Integer> v = new Vector<Integer>();

    // Traverse the array arr[]
    for(int i = 0; i < n; i++)
    {

        // Store the result for the
        // current index and its frequency
        int ans = -1, old_c = 0;

        // Iterate over the right subarray
        for(int j = i + 1; j < n; j++)
        {
            if (arr[j] > arr[i])
            {

                // Store the frequency of
                // the current array element
                int curr_c = 0;
                for(int k = j; k < n; k++)
                {
                    if (arr[k] == arr[j])
                    {
                        curr_c++;
                    }
                };

                // If the frequencies are equal
                if (curr_c == old_c)
                {

                    // Update ans to smaller
                    // of the two elements
                    if (arr[j] < ans)
                        ans = arr[j];
                }

                // If count of new element
                // is more than count of ans
                if (curr_c > old_c)
                {
                    ans = arr[j];
                    old_c = curr_c;
                }
            }
        }

        // Insert answer in the array
        v.add(ans);
    }

    // Print the resultant array
    for(int i = 0; i < v.size(); i++)
        System.out.print(v.get(i) + " ");
}

// Driver Code
public static void main (String[] args)
{

    // Given Input
    int arr[] = { 4, 5, 2, 25, 10,
                  5, 10, 3, 10, 5 };
    int size = arr.length;

    findArray(arr, size);
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to generate an array containing
# the most frequent greater element on the
# right side of each array element
def findArray(arr, n):

    # Stores the generated array
    v = []

    # Traverse the array arr[]
    for i in range(n):

        # Store the result for the
        # current index and its frequency
        ans = -1
        old_c = 0

        # Iterate over the right subarray
        for j in range(i + 1, n):
            if (arr[j] > arr[i]):

                # Store the frequency of
                # the current array element
                curr_c = arr[j : n + 1].count(arr[j])

                # If the frequencies are equal
                if (curr_c == old_c):

                    # Update ans to smaller
                    # of the two elements
                    if (arr[j] < ans):
                        ans = arr[j]

                # If count of new element
                # is more than count of ans
                if (curr_c > old_c):
                    ans = arr[j]
                    old_c = curr_c

        # Insert answer in the array
        v.append(ans)

    # Print the resultant array
    for i in range(len(v)):
        print(v[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ 4, 5, 2, 25, 10,
            5, 10, 3, 10, 5 ]
    size = len(arr)

    findArray(arr, size)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to generate an array containing
// the most frequent greater element on the
// right side of each array element
static void findArray(int[] arr, int n)
{

    // Stores the generated array
    List<int> v = new List<int>();

    // Traverse the array arr[]
    for(int i = 0; i < n; i++)
    {

        // Store the result for the
        // current index and its frequency
        int ans = -1, old_c = 0;

        // Iterate over the right subarray
        for(int j = i + 1; j < n; j++)
        {
            if (arr[j] > arr[i])
            {

                // Store the frequency of
                // the current array element
                int curr_c = 0;
                for(int k = j; k < n; k++)
                {
                    if (arr[k] == arr[j])
                    {
                        curr_c++;
                    }
                };

                // If the frequencies are equal
                if (curr_c == old_c)
                {

                    // Update ans to smaller
                    // of the two elements
                    if (arr[j] < ans)
                        ans = arr[j];
                }

                // If count of new element
                // is more than count of ans
                if (curr_c > old_c)
                {
                    ans = arr[j];
                    old_c = curr_c;
                }
            }
        }

        // Insert answer in the array
        v.Add(ans);
    }

    // Print the resultant array
    for(int i = 0; i < v.Count; i++)
        Console.Write(v[i] + " ");
}

// Driver Code
public static void Main()
{

    // Given Input
    int[] arr= { 4, 5, 2, 25, 10,
                 5, 10, 3, 10, 5 };
    int size = arr.Length;

    findArray(arr, size);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to generate an array containing
// the most frequent greater element on the
// right side of each array element
function findArray(arr, n) {
    // Stores the generated array
    let v = new Array();

    // Traverse the array arr[]
    for (let i = 0; i < n; i++) {

        // Store the result for the
        // current index and its frequency
        let ans = -1, old_c = 0;

        // Iterate over the right subarray
        for (let j = i + 1; j < n; j++) {

            if (arr[j] > arr[i]) {

                // Store the frequency of
                // the current array element
                // let curr_c = count(&arr[j], &arr[n], arr[j]);

                let curr_c = 0;
                arr.slice(j, n).forEach((item) => { if (item == arr[j]) { curr_c++ } })

                // If the frequencies are equal
                if (curr_c == old_c) {

                    // Update ans to smaller
                    // of the two elements
                    if (arr[j] < ans)
                        ans = arr[j];
                }

                // If count of new element
                // is more than count of ans
                if (curr_c > old_c) {
                    ans = arr[j];
                    old_c = curr_c;
                }
            }
        }

        // Insert answer in the array
        v.push(ans);
    }

    // Print the resultant array
    for (let i = 0; i < v.length; i++)
        document.write(v[i] + " ");
}

// Driver Code

// Given Input
let arr = [4, 5, 2, 25, 10, 5,
    10, 3, 10, 5];
let size = arr.length

findArray(arr, size);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
5 10 10 -1 -1 10 -1 5 -1 -1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*
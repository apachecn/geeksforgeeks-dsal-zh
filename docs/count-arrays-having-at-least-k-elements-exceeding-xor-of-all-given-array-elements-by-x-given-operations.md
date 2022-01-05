# 通过 X 个给定运算对至少有 K 个元素超过所有给定数组元素的异或运算的数组进行计数

> 原文:[https://www . geeksforgeeks . org/count-arrays-具有至少 k 个元素-超过-xor-所有给定数组元素乘以-x-给定-运算/](https://www.geeksforgeeks.org/count-arrays-having-at-least-k-elements-exceeding-xor-of-all-given-array-elements-by-x-given-operations/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算至少具有大于所有数组元素的**异或**的 **K** 元素的数组的数量，通过执行以下操作 **X** 次生成。

*   从给定数组中选择第一个或最后一个元素。
*   将所选元素增加 **1** 或删除所选元素。

**示例:**

> **输入:** arr[] = {10，2，10，5}，X = 3，K = 3
> **输出:** 1
> **解释:**
> 给定数组的异或= 7。满足该条件的唯一可能数组是{10，2，10，8}，通过将最后一个数组元素递增三次获得。
> 
> **输入:** arr[] = {3，3，4}，X = 3，K = 2
> T3】输出: 3

**方法:**思路是使用 [<u>回溯方法</u>](https://www.geeksforgeeks.org/backtracking-algorithms/) 递归尝试所有可能的走法，并在获得所需数组时递增计数。可能的移动有:

*   初始化一个变量，说**异或**，到[计算原数组](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)的异或。
*   初始化一个变量，比如**计数**，来存储所需数组的最终计数。
*   递归尝试以下四种可能性，并在获得所需数组时增加计数:
    *   删除数组的第一个元素。
    *   删除数组的最后一个元素。
    *   将第一个数组元素递增 1。
    *   将最后一个数组元素递增 1。
*   打印最终计数作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the final answer
int ans = 0;

// Utility function to count arrays
// having at least K elements exceeding
// XOR of all given array elements
void countArraysUtil(vector<int>& arr,
                     int X, int K,
                     int xorVal)
{
    // If no operations are left
    if (X == 0) {

        // Stores the count of
        // possible arrays
        int cnt = 0;

        // Count array elements are
        // greater than XOR
        for (int i = 0; i < arr.size(); i++) {

            if (arr[i] > xorVal)
                cnt++;
        }
        if (cnt >= K)
            ans++;
        return;
    }

    // Stores first element
    int temp = arr[0];

    // Delete first element
    arr.erase(arr.begin());

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Insert first element into vector
    arr.insert(arr.begin(), temp);

    // Stores the last element
    temp = arr.back();

    // Remove last element from vector
    arr.pop_back();

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Push last element into vector
    arr.push_back(temp);

    // Increment first element
    arr[0]++;

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Decrement first element
    arr[0]--;

    // Increment last element
    arr[arr.size() - 1]++;

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Decrement last element
    arr[arr.size() - 1]--;
}

// Function to find the count of
// arrays having atleast K elements
// greater than XOR of array
void countArrays(vector<int>& arr,
                 int X, int K)
{
    // Stores the XOR value
// of original array
    int xorVal = 0;

    // Traverse the vector
    for (int i = 0; i < arr.size(); i++)
        xorVal = xorVal ^ arr[i];

    countArraysUtil(arr, X, K, xorVal);

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    // Given vector
    vector<int> arr = { 10, 2, 10, 5 };

    // Given value of X & K
    int X = 3, K = 3;

    countArrays(arr, X, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
class GFG{

// Stores the final answer
static int ans = 0;

// Utility function to count arrays
// having at least K elements exceeding
// XOR of all given array elements
public static void countArraysUtil(ArrayList<Integer> arr,
                     int X, int K,
                     int xorVal)
{
    // If no operations are left
    if (X == 0) {

        // Stores the count of
        // possible arrays
        int cnt = 0;

        // Count array elements are
        // greater than XOR
        for (int i = 0; i < arr.size(); i++) {

            if (arr.get(i) > xorVal)
                cnt++;
        }
        if (cnt >= K)
            ans++;
        return;
    }

    // Stores first element
    int temp = arr.get(0);

    // Delete first element
    arr.remove(0);

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Insert first element into vector
    arr.add(0, temp);

    // Stores the last element
    temp = arr.get(arr.size() - 1);

    // Remove last element from vector
    arr.remove(arr.size() - 1);

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Push last element into vector
    arr.add(temp);

    // Increment first element
    arr.set(0, arr.get(0) + 1);

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Decrement first element
    arr.set(0, arr.get(0) - 1);

    // Increment last element
    arr.set(arr.size() - 1, arr.get(arr.size() - 1) + 1);

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Decrement last element
    arr.set(arr.size() - 1, arr.get(arr.size() - 1) - 1);

}

// Function to find the count of
// arrays having atleast K elements
// greater than XOR of array
public static void countArrays(ArrayList<Integer> arr,
                 int X, int K)
{
    // Stores the XOR value
// of original array
    int xorVal = 0;

    // Traverse the vector
    for (int i = 0; i < arr.size(); i++)
        xorVal = xorVal ^ arr.get(i);

    countArraysUtil(arr, X, K, xorVal);

    // Print the answer
    System.out.println(ans);
}

// Driver Code
public static void main(String arg[])
{

    // Given vector
    int[] input = {10, 2, 10, 5};

    // Convert the input as ArrayList
    ArrayList<Integer> arr = new ArrayList<Integer>();

    for(int i : input){
        arr.add(i);
    }

    // Given value of X & K
    int X = 3, K = 3;

    countArrays(arr, X, K);
}
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python program for the above approach

# Stores the final answer
ans = 0

# Utility function to count arrays
# having at least K elements exceeding
# XOR of all given array elements
def countArraysUtil( arr, X, K, xorVal):
    global ans

    # If no operations are left
    if (X == 0):

        # Stores the count of
        # possible arrays
        cnt = 0

        # Count array elements are
        # greater than XOR
        for i in range(len(arr)):
            if (arr[i] > xorVal):
                cnt += 1
        if (cnt >= K):
            ans += 1
        return

    # Stores first element
    temp = arr[0]

    # Delete first element
    arr.pop(0)

    # Recursive call
    countArraysUtil(arr, X - 1, K, xorVal)

    # Insert first element into vector
    arr.insert(0, temp)

    # Stores the last element
    temp = arr[-1]

    # Remove last element from vector
    arr.pop()

    # Recursive call
    countArraysUtil(arr, X - 1, K, xorVal)

    # Push last element into vector
    arr.append(temp)

    # Increment first element
    arr[0] += 1

    # Recursive call
    countArraysUtil(arr, X - 1,K, xorVal)

    # Decrement first element
    arr[0] -= 1

    # Increment last element
    arr[len(arr) - 1] += 1

    # Recursive call
    countArraysUtil(arr, X - 1, K, xorVal)

    # Decrement last element
    arr[len(arr) - 1] -= 1

# Function to find the count of
# arrays having atleast K elements
# greater than XOR of array
def countArrays(arr, X, K):

    # Stores the XOR value
    # of original array
    xorVal = 0

    # Traverse the vector
    for i in range(len(arr)):
        xorVal = xorVal ^ arr[i]
    countArraysUtil(arr, X, K, xorVal)

    # Print the answer
    print(ans)

# Driver Code
# Given vector
arr = [ 10, 2, 10, 5 ]

# Given value of X & K
X = 3
K = 3
countArrays(arr, X, K)

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Stores the final answer
    static int ans = 0;

    // Utility function to count arrays
    // having at least K elements exceeding
    // XOR of all given array elements
    static void countArraysUtil(List<int> arr, int X, int K,
                                int xorVal)
    {
        // If no operations are left
        if (X == 0) {

            // Stores the count of
            // possible arrays
            int cnt = 0;

            // Count array elements are
            // greater than XOR
            for (int i = 0; i < arr.Count; i++) {

                if (arr[i] > xorVal)
                    cnt++;
            }
            if (cnt >= K)
                ans++;
            return;
        }

        // Stores first element
        int temp = arr[0];

        // Delete first element
        arr.RemoveAt(0);

        // Recursive call
        countArraysUtil(arr, X - 1, K, xorVal);

        // Insert first element into vector
        arr.Insert(0, temp);

        // Stores the last element
        temp = arr[arr.Count - 1];

        // Remove last element from vector
        arr.RemoveAt(arr.Count - 1);

        // Recursive call
        countArraysUtil(arr, X - 1, K, xorVal);

        // Push last element into vector
        arr.Add(temp);

        // Increment first element
        arr[0]++;

        // Recursive call
        countArraysUtil(arr, X - 1, K, xorVal);

        // Decrement first element
        arr[0]--;

        // Increment last element
        arr[arr.Count - 1]++;

        // Recursive call
        countArraysUtil(arr, X - 1, K, xorVal);

        // Decrement last element
        arr[arr.Count - 1]--;
    }

    // Function to find the count of
    // arrays having atleast K elements
    // greater than XOR of array
    static void countArrays(List<int> arr, int X, int K)
    {
        // Stores the XOR value
        // of original array
        int xorVal = 0;

        // Traverse the vector
        for (int i = 0; i < arr.Count; i++)
            xorVal = xorVal ^ arr[i];

        countArraysUtil(arr, X, K, xorVal);

        // Print the answer
        Console.Write(ans);
    }

    // Driver Code
    public static void Main()
    {

        // Given vector
        List<int> arr = new List<int>() { 10, 2, 10, 5 };

        // Given value of X & K
        int X = 3, K = 3;
        countArrays(arr, X, K);
    }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Stores the final answer
let ans = 0;

// Utility function to count arrays
// having at least K elements exceeding
// XOR of all given array elements
function countArraysUtil(arr,X,K,xorVal)
{
    // If no operations are left
    if (X == 0) {

        // Stores the count of
        // possible arrays
        let cnt = 0;

        // Count array elements are
        // greater than XOR
        for (let i = 0; i < arr.length; i++) {

            if (arr[i] > xorVal)
                cnt++;
        }
        if (cnt >= K)
            ans++;
        return;
    }

    // Stores first element
    let temp = arr[0];

    // Delete first element
    arr.shift();

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Insert first element into vector
    arr.unshift(temp);

    // Stores the last element
    temp = arr[arr.length-1];

    // Remove last element from vector
    arr.pop();

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Push last element into vector
    arr.push(temp);

    // Increment first element
    arr[0]++;

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Decrement first element
    arr[0]--;

    // Increment last element
    arr[arr.length - 1]++;

    // Recursive call
    countArraysUtil(arr, X - 1,
                    K, xorVal);

    // Decrement last element
    arr[arr.length - 1]--;
}

// Function to find the count of
// arrays having atleast K elements
// greater than XOR of array
function countArrays(arr,X,K)
{
    // Stores the XOR value
// of original array
    let xorVal = 0;

    // Traverse the vector
    for (let i = 0; i < arr.length; i++)
        xorVal = xorVal ^ arr[i];

    countArraysUtil(arr, X, K, xorVal);

    // Print the answer
    document.write(ans);
}

// Driver Code
let arr=[10, 2, 10, 5];
// Given value of X & K
let X = 3, K = 3;

countArrays(arr, X, K);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(4<sup>K</sup>* N)*
***辅助空间:** O(1)*
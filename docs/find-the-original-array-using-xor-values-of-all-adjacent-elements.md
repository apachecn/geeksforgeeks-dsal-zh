# 使用所有相邻元素的异或值找到原始数组

> 原文:[https://www . geeksforgeeks . org/使用所有相邻元素的 xor 值查找原始数组/](https://www.geeksforgeeks.org/find-the-original-array-using-xor-values-of-all-adjacent-elements/)

给定一个序列**arr[]****N-1**元素，它是一个数组中所有相邻对的异或，任务是从 **arr[]** 中找到原始的**数组**。
**注:**给出 N 总是奇数，arr[]包含 N 个自然数的[排列。
**举例:**](https://www.geeksforgeeks.org/find-the-good-permutation-of-first-n-natural-numbers/) 

> **输入:** arr[] = {3，1}
> **输出:** 1 2 3
> **解释:**
> 输出数组的 XOR 将导致给定数组即:
> 1 ^ 2 = 3
> 2 ^ 3 = 1
> **输入:** arr[] = {7，5，3， 7}
> **输出:** 3 4 1 2 5
> **解释:**
> 输出数组的异或将导致给定的数组，即:
> 3 ^ 4 = 7
> 4 ^ 1 = 5
> 1 ^ 2 = 3
> 2 ^ 5 = 7

**进场:**

1.  其思想是找到 1 到 N 的所有元素的[异或](https://www.geeksforgeeks.org/tag/xor/)和给定数组的相邻元素的异或，以找到期望数组的最后一个元素。
2.  由于相邻元素的异或运算将包含除最后一个元素之外的所有元素，因此用从 1 到 N 的所有数字进行异或运算将得到预期置换的最后一个元素。
    **例如:**

```
Let's the expected array be - {a, b, c, d, e}
Then the XOR array for this array will be - 
{a^b, b^c, c^d, d^e}

Now XOR of all the element from 1 to N -
xor_all => a ^ b ^ c ^ d ^ e

XOR of the adjacent elements -
xor_adjacent => ((a ^ b) ^ (c ^ d))

Now the XOR of the both the array will be the 
last element of the expected permutation 
=> (a ^ b ^ c ^ d ^ e) ^ ((a ^ b) ^ (c ^ d))
=> As all elements are in pair except the last element.
=> (a ^ a ^ b ^ b ^ c ^ c ^ d ^ d ^ e)
=> (0 ^ 0 ^ 0 ^ 0 ^ e)
=> e
```

1.  现在对于元素的其余部分，连续地，对最后一个元素进行异或运算，我们将得到最后一个第二个元素，即 **d** 。
2.  反复更新最后一个元素，最后得到第一个元素，即 **a** 。

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// Array from the XOR array
// of the adjacent elements of array

#include <bits/stdc++.h>
using namespace std;

// XOR of all elements from 1 to N
int xor_all_elements(int n)
{

    switch (n & 3) {

    case 0:
        return n;
    case 1:
        return 1;
    case 2:
        return n + 1;
    case 3:
        return 0;
    }
}

// Function to find the Array
// from the XOR Array
vector<int> findArray(int xorr[], int n)
{
    // Take a vector to store
    // the permutation
    vector<int> arr;

    // XOR of N natural numbers
    int xor_all = xor_all_elements(n);
    int xor_adjacent = 0;

    // Loop to find the XOR of
    // adjacent elements of the XOR Array
    for (int i = 0; i < n - 1; i += 2) {
        xor_adjacent = xor_adjacent ^ xorr[i];
    }
    int last_element = xor_all ^ xor_adjacent;
    arr.push_back(last_element);

    // Loop to find the other
    // elements of the permutation
    for (int i = n - 2; i >= 0; i--) {
        // Finding the next and next elements
        last_element = xorr[i] ^ last_element;
        arr.push_back(last_element);
    }

    return arr;
}

// Driver Code
int main()
{
    vector<int> arr;

    int xorr[] = { 7, 5, 3, 7 };
    int n = 5;

    arr = findArray(xorr, n);

    // Required Permutation
    for (int i = n - 1; i >= 0; i--) {
        cout << arr[i] << " ";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Array from the XOR array
// of the adjacent elements of array
import java.util.*;

class GFG{

// XOR of all elements from 1 to N
static int xor_all_elements(int n)
{

    switch (n & 3) {

    case 0:
        return n;
    case 1:
        return 1;
    case 2:
        return n + 1;
    }
    return 0;
}

// Function to find the Array
// from the XOR Array
static Vector<Integer> findArray(int xorr[], int n)
{
    // Take a vector to store
    // the permutation
    Vector<Integer> arr = new Vector<Integer>();

    // XOR of N natural numbers
    int xor_all = xor_all_elements(n);
    int xor_adjacent = 0;

    // Loop to find the XOR of
    // adjacent elements of the XOR Array
    for (int i = 0; i < n - 1; i += 2) {
        xor_adjacent = xor_adjacent ^ xorr[i];
    }
    int last_element = xor_all ^ xor_adjacent;
    arr.add(last_element);

    // Loop to find the other
    // elements of the permutation
    for (int i = n - 2; i >= 0; i--)
    {
        // Finding the next and next elements
        last_element = xorr[i] ^ last_element;
        arr.add(last_element);
    }

    return arr;
}

// Driver Code
public static void main(String[] args)
{
    Vector<Integer> arr = new Vector<Integer>();

    int xorr[] = { 7, 5, 3, 7 };
    int n = 5;

    arr = findArray(xorr, n);

    // Required Permutation
    for (int i = n - 1; i >= 0; i--)
    {
        System.out.print(arr.get(i)+ " ");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to find the
# Array from the XOR array
# of the adjacent elements of array

# XOR of all elements from 1 to N
def xor_all_elements(n):

    if n & 3 == 0:
        return n
    elif n & 3 == 1:
        return 1
    elif n & 3 == 2:
        return n + 1
    else:
        return 0

# Function to find the Array
# from the XOR Array
def findArray(xorr, n):

    # Take a vector to store
    # the permutation
    arr = []

    # XOR of N natural numbers
    xor_all = xor_all_elements(n)
    xor_adjacent = 0

    # Loop to find the XOR of
    # adjacent elements of the XOR Array
    for i in range(0, n - 1, 2):
        xor_adjacent = xor_adjacent ^ xorr[i]

    last_element = xor_all ^ xor_adjacent
    arr.append(last_element)

    # Loop to find the other
    # elements of the permutation
    for i in range(n - 2, -1, -1):

        # Finding the next and next elements
        last_element = xorr[i] ^ last_element
        arr.append(last_element)

    return arr

# Driver Code
xorr = [7, 5, 3, 7]
n = 5

arr = findArray(xorr, n)

# Required Permutation
for i in range(n - 1, -1, -1):
    print(arr[i], end=" ")

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# implementation to find the
// Array from the XOR array
// of the adjacent elements of array
using System;
using System.Collections.Generic;

class GFG{

// XOR of all elements from 1 to N
static int xor_all_elements(int n)
{

    switch (n & 3) {

    case 0:
        return n;
    case 1:
        return 1;
    case 2:
        return n + 1;
    }
    return 0;
}

// Function to find the Array
// from the XOR Array
static List<int> findArray(int []xorr, int n)
{
    // Take a vector to store
    // the permutation
    List<int> arr = new List<int>();

    // XOR of N natural numbers
    int xor_all = xor_all_elements(n);
    int xor_adjacent = 0;

    // Loop to find the XOR of
    // adjacent elements of the XOR Array
    for (int i = 0; i < n - 1; i += 2) {
        xor_adjacent = xor_adjacent ^ xorr[i];
    }
    int last_element = xor_all ^ xor_adjacent;
    arr.Add(last_element);

    // Loop to find the other
    // elements of the permutation
    for (int i = n - 2; i >= 0; i--)
    {
        // Finding the next and next elements
        last_element = xorr[i] ^ last_element;
        arr.Add(last_element);
    }

    return arr;
}

// Driver Code
public static void Main(String[] args)
{
    List<int> arr = new List<int>();

    int []xorr = { 7, 5, 3, 7 };
    int n = 5;

    arr = findArray(xorr, n);

    // Required Permutation
    for (int i = n - 1; i >= 0; i--)
    {
        Console.Write(arr[i]+ " ");
    }
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// Array from the XOR array
// of the adjacent elements of array

// XOR of all elements from 1 to N
function xor_all_elements(n)
{

    switch (n & 3) {

    case 0:
        return n;
    case 1:
        return 1;
    case 2:
        return n + 1;
    case 3:
        return 0;
    }
}

// Function to find the Array
// from the XOR Array
function findArray(xorr, n)
{
    // Take a vector to store
    // the permutation
    let arr = [];

    // XOR of N natural numbers
    let xor_all = xor_all_elements(n);
    let xor_adjacent = 0;

    // Loop to find the XOR of
    // adjacent elements of the XOR Array
    for (let i = 0; i < n - 1; i += 2) {
        xor_adjacent = xor_adjacent ^ xorr[i];
    }
    let last_element = xor_all ^ xor_adjacent;
    arr.push(last_element);

    // Loop to find the other
    // elements of the permutation
    for (let i = n - 2; i >= 0; i--) {
        // Finding the next and next elements
        last_element = xorr[i] ^ last_element;
        arr.push(last_element);
    }

    return arr;
}

// Driver Code
    let arr = [];

    let xorr = [ 7, 5, 3, 7 ];
    let n = 5;

    arr = findArray(xorr, n);

    // Required Permutation
    for (let i = n - 1; i >= 0; i--) {
        document.write(arr[i] + " ");
    }

</script>
```

**Output:** 

```
3 4 1 2 5
```

**业绩分析:**

*   **时间复杂度:**在上面的方法中，我们迭代整个 xor 数组来寻找相邻元素的 XOR，那么最坏情况下的复杂度将是 **O(N)**
*   **空间复杂度:**在上面的方法中，有一个向量数组用来存储从 1 到 N 的数字的[排列](https://www.geeksforgeeks.org/generate-a-random-permutation-of-1-to-n/)，那么空间复杂度将是 **O(N)**
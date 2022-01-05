# 给定数组作为前缀最大数组的前 N 个自然数的排列

> 原文:[https://www . geesforgeks . org/第一个 n 个自然数的排列-以给定数组作为前缀-最大数组/](https://www.geeksforgeeks.org/permutation-of-first-n-natural-numbers-having-given-array-as-the-prefix-maximum-array/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到第一个 **N** 自然数的[排列，这样给定的数组 **arr[]** 就是该排列的](https://www.geeksforgeeks.org/find-the-good-permutation-of-first-n-natural-numbers/)[前缀最大数组](https://www.geeksforgeeks.org/maximum-prefix-sum-given-range/)。如果不存在这样的排列，则打印**-1”**。

**示例:**

> **输入:** arr[] = {1，3，4，5，5}
> **输出:** 1 3 4 5 2
> **解释:**
> 排列{1，3，4，5，2}的前缀最大数组是{1，3，4，5，5}。
> 
> **输入:** arr[] = {1，1，3，4}
> **输出:** -1

**天真方法:**解决给定问题的最简单方法是[生成前 N 个自然数](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/)的所有可能排列，并检查是否存在任何其[前缀最大数组](https://www.geeksforgeeks.org/maximum-prefix-sum-given-range/)为数组**arr【】**的排列。如果找到任何这样的排列，那么打印该排列。否则，打印**-1”**。

***时间复杂度:** O(N * N！)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以基于以下观察进行优化，即 arr【】中每个数字的[第一次出现将与所需排列中的相同位置。因此，在所有元素的正确位置填充第一个匹配项后，以升序填充剩余的数字。按照以下步骤解决问题:](https://www.geeksforgeeks.org/find-first-and-last-positions-of-an-element-in-a-sorted-array/)

*   初始化一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **ans[]** ，所有元素为 **0** 和一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **V[]** ，以存储数组中所有未访问的元素。
*   初始化一个 [HashMap](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **M** 来存储元素第一次出现的索引
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，如果 **M** 中不存在 **arr[i]** ，则将 **arr[i]** 的索引存储在 **M** 中，并将 **ans[i]** 更新为 **arr[i]** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，检查 **M** 中是否不存在 **i** ，将其存储在向量**V【】**中。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **ans[]** ，如果 **ans[i]** 的值为 **0** ，则将 **ans[i]** 更新为 **V[j]** ，并将 **j** 增加 **1** 。
*   完成上述步骤后，检查[最大元素](https://www.geeksforgeeks.org/max_element-in-cpp/)前缀数组是否与**arr【】**相同。如果发现是真的，那么[打印阵列](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)**ans【】**作为结果。否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the maximum
// prefix array of ans[] is equal
// to array arr[]
bool checkPermutation(
    int ans[], int a[], int n)
{
    // Initialize a variable, Max
    int Max = INT_MIN;

    // Traverse the array, ans[]
    for (int i = 0; i < n; i++) {

        // Store the maximum value
        // upto index i
        Max = max(Max, ans[i]);

        // If it is not equal to a[i],
        // then return false
        if (Max != a[i])
            return false;
    }

    // Otherwise return false
    return true;
}

// Function to find the permutation of
// the array whose prefix maximum array
// is same as the given array a[]
void findPermutation(int a[], int n)
{
    // Stores the required permutation
    int ans[n] = { 0 };

    // Stores the index of first
    // occurrence of elements
    unordered_map<int, int> um;

    // Traverse the array a[]
    for (int i = 0; i < n; i++) {

        // If a[i] is not present
        // in um, then store it in um
        if (um.find(a[i]) == um.end()) {

            // Update the ans[i]
            // to a[i]
            ans[i] = a[i];
            um[a[i]] = i;
        }
    }

    // Stores the unvisited numbers
    vector<int> v;
    int j = 0;

    // Fill the array, v[]
    for (int i = 1; i <= n; i++) {

        // Store the index
        if (um.find(i) == um.end()) {
            v.push_back(i);
        }
    }

    // Traverse the array, ans[]
    for (int i = 0; i < n; i++) {

        // Fill v[j] at places where
        // ans[i] is 0
        if (ans[i] == 0) {
            ans[i] = v[j];
            j++;
        }
    }

    // Check if the current permutation
    // maximum prefix array is same as
    // the given array a[]
    if (checkPermutation(ans, a, n)) {

        // If true, the print the
        // permutation
        for (int i = 0; i < n; i++) {
            cout << ans[i] << " ";
        }
    }

    // Otherwise, print -1
    else
        cout << "-1";
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 4, 5, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findPermutation(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if the maximum
// prefix array of ans[] is equal
// to array arr[]
static boolean checkPermutation(int ans[], int a[],
                                int n)
{

    // Initialize a variable, Max
    int Max = Integer.MIN_VALUE;

    // Traverse the array, ans[]
    for(int i = 0; i < n; i++)
    {

        // Store the maximum value
        // upto index i
        Max = Math.max(Max, ans[i]);

        // If it is not equal to a[i],
        // then return false
        if (Max != a[i])
            return false;
    }

    // Otherwise return false
    return true;
}

// Function to find the permutation of
// the array whose prefix maximum array
// is same as the given array a[]
static void findPermutation(int a[], int n)
{

    // Stores the required permutation
    int ans[] = new int[n];

    // Stores the index of first
    // occurrence of elements
    HashMap<Integer, Integer> um = new HashMap<>();

    // Traverse the array a[]
    for(int i = 0; i < n; i++)
    {

        // If a[i] is not present
        // in um, then store it in um
        if (!um.containsKey(a[i]))
        {

            // Update the ans[i]
            // to a[i]
            ans[i] = a[i];
            um.put(a[i], i);
        }
    }

    // Stores the unvisited numbers
    ArrayList<Integer> v = new ArrayList<>();
    int j = 0;

    // Fill the array, v[]
    for(int i = 1; i <= n; i++)
    {

        // Store the index
        if (!um.containsKey(i))
        {
            v.add(i);
        }
    }

    // Traverse the array, ans[]
    for(int i = 0; i < n; i++)
    {

        // Fill v[j] at places where
        // ans[i] is 0
        if (ans[i] == 0)
        {
            ans[i] = v.get(j);
            j++;
        }
    }

    // Check if the current permutation
    // maximum prefix array is same as
    // the given array a[]
    if (checkPermutation(ans, a, n))
    {

        // If true, the print the
        // permutation
        for(int i = 0; i < n; i++)
        {
            System.out.print(ans[i] + " ");
        }
    }

    // Otherwise, print -1
    else
        System.out.println("-1");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 4, 5, 5 };
    int N = arr.length;

    // Function Call
    findPermutation(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to check if the maximum
# prefix array of ans[] is equal
# to array arr[]
def checkPermutation(ans, a, n):

    # Initialize a variable, Max
    Max = -sys.maxsize - 1

    # Traverse the array, ans[]
    for i in range(n):

        # Store the maximum value
        # upto index i
        Max = max(Max, ans[i])

        # If it is not equal to a[i],
        # then return false
        if (Max != a[i]):
            return False

    # Otherwise return false
    return True

# Function to find the permutation of
# the array whose prefix maximum array
# is same as the given array a[]
def findPermutation(a, n):

    # Stores the required permutation
    ans = [0] * n

    # Stores the index of first
    # occurrence of elements
    um = {}

    # Traverse the array a[]
    for i in range(n):

        # If a[i] is not present
        # in um, then store it in um
        if (a[i] not in um):

            # Update the ans[i]
            # to a[i]
            ans[i] = a[i]
            um[a[i]] = i

    # Stores the unvisited numbers
    v = []
    j = 0

    # Fill the array, v[]
    for i in range(1, n + 1):

        # Store the index
        if (i not in um):
            v.append(i)

    # Traverse the array, ans[]
    for i in range(n):

        # Fill v[j] at places where
        # ans[i] is 0
        if (ans[i] == 0):
            ans[i] = v[j]
            j += 1

    # Check if the current permutation
    # maximum prefix array is same as
    # the given array a[]
    if (checkPermutation(ans, a, n)):

        # If true, the print the
        # permutation
        for i in range(n):
            print(ans[i], end = " ")

    # Otherwise, print -1
    else:
        print("-1")

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 3, 4, 5, 5 ]
    N = len(arr)

    # Function Call
    findPermutation(arr, N)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic; 

class GFG{

// Function to check if the maximum
// prefix array of ans[] is equal
// to array arr[]
static bool checkPermutation(int[] ans, int[] a,
                             int n)
{

    // Initialize a variable, Max
    int Max = Int32.MinValue;

    // Traverse the array, ans[]
    for(int i = 0; i < n; i++)
    {

        // Store the maximum value
        // upto index i
        Max = Math.Max(Max, ans[i]);

        // If it is not equal to a[i],
        // then return false
        if (Max != a[i])
            return false;
    }

    // Otherwise return false
    return true;
}

// Function to find the permutation of
// the array whose prefix maximum array
// is same as the given array a[]
static void findPermutation(int[] a, int n)
{

    // Stores the required permutation
    int[] ans = new int[n];

    // Stores the index of first
    // occurrence of elements
    Dictionary<int,
               int> um = new Dictionary<int,
                                        int>();

    // Traverse the array a[]
    for(int i = 0; i < n; i++)
    {

        // If a[i] is not present
        // in um, then store it in um
        if (!um.ContainsKey(a[i]))
        {

            // Update the ans[i]
            // to a[i]
            ans[i] = a[i];
            um[a[i]] = i;
        }
    }

    // Stores the unvisited numbers
    List<int> v = new List<int>();
    int j = 0;

    // Fill the array, v[]
    for(int i = 1; i <= n; i++)
    {

        // Store the index
        if (!um.ContainsKey(i))
        {
            v.Add(i);
        }
    }

    // Traverse the array, ans[]
    for(int i = 0; i < n; i++)
    {

        // Fill v[j] at places where
        // ans[i] is 0
        if (ans[i] == 0)
        {
            ans[i] = v[j];
            j++;
        }
    }

    // Check if the current permutation
    // maximum prefix array is same as
    // the given array a[]
    if (checkPermutation(ans, a, n))
    {

        // If true, the print the
        // permutation
        for(int i = 0; i < n; i++)
        {
            Console.Write(ans[i] + " ");
        }
    }

    // Otherwise, print -1
    else
        Console.Write("-1");
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 3, 4, 5, 5 };
    int N = arr.Length;

    // Function Call
    findPermutation(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if the maximum
// prefix array of ans[] is equal
// to array arr[]
function checkPermutation(ans,a,n)
{
    // Initialize a variable, Max
    let Max = Number.MIN_VALUE;

    // Traverse the array, ans[]
    for(let i = 0; i < n; i++)
    {

        // Store the maximum value
        // upto index i
        Max = Math.max(Max, ans[i]);

        // If it is not equal to a[i],
        // then return false
        if (Max != a[i])
            return false;
    }

    // Otherwise return false
    return true;
}

// Function to find the permutation of
// the array whose prefix maximum array
// is same as the given array a[]
function findPermutation(a,n)
{
    // Stores the required permutation
    let ans = new Array(n);
     for(let i=0;i<n;i++)
    {
        ans[i]=0;
    }
    // Stores the index of first
    // occurrence of elements
    let um = new Map();

    // Traverse the array a[]
    for(let i = 0; i < n; i++)
    {

        // If a[i] is not present
        // in um, then store it in um
        if (!um.has(a[i]))
        {

            // Update the ans[i]
            // to a[i]
            ans[i] = a[i];
            um.set(a[i], i);
        }
    }

    // Stores the unvisited numbers
    let v = [];
    let j = 0;

    // Fill the array, v[]
    for(let i = 1; i <= n; i++)
    {

        // Store the index
        if (!um.has(i))
        {
            v.push(i);
        }
    }

    // Traverse the array, ans[]
    for(let i = 0; i < n; i++)
    {

        // Fill v[j] at places where
        // ans[i] is 0
        if (ans[i] == 0)
        {
            ans[i] = v[j];
            j++;
        }
    }

    // Check if the current permutation
    // maximum prefix array is same as
    // the given array a[]
    if (checkPermutation(ans, a, n))
    {

        // If true, the print the
        // permutation
        for(let i = 0; i < n; i++)
        {
            document.write(ans[i] + " ");
        }
    }

    // Otherwise, print -1
    else
        document.write("-1");
}

// Driver Code
let arr=[1, 3, 4, 5, 5];
let N = arr.length;
// Function Call
findPermutation(arr, N);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
1 3 4 5 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
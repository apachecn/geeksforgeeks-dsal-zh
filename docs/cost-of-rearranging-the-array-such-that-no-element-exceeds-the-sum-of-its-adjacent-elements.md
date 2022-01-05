# 重新排列数组使得没有元素超过其相邻元素之和的成本

> 原文:[https://www . geeksforgeeks . org/重新排列数组的成本使得没有元素超过其相邻元素的总和/](https://www.geeksforgeeks.org/cost-of-rearranging-the-array-such-that-no-element-exceeds-the-sum-of-its-adjacent-elements/)

给定一个由 **N** 个唯一整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出将它们以循环排列的方式排列的成本，使得每个元素都小于或等于其相邻元素的总和。

> 将元素从原始数组中的索引 **i** 移动到最终排列中的索引 **j** 的成本是**| I–j |**

如果这样的安排是不可能的，那么打印 **-1** 。
**例:**

> **输入:** arr[] = {2，4，5，1，3}
> **输出:** 10
> **解释:**
> 可能的排列方式之一是{1，2，3，4，5}
> 对于指标 1，1 ≤ 4 + 2，成本= 4–1 = 3
> 对于指标 2，2 ≤ 1 + 3，成本= 3+(2–1)= 4
> 对于指标 3，3 ≤ 2 + 4， 成本= 4+(5–3)= 6
> 对于指数 4，4 ≤ 3 + 4，成本= 6+(4–2)= 8
> 对于指数 5，5 ≤ 4 + 1，成本= 8+(5–3)= 10
> **输入:** arr[] = {1，10，100，1000}
> **输出:** -1

**方法:**问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。其思想是将元素的原始索引存储在一个[散列表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)中，然后[对数组进行排序](https://www.geeksforgeeks.org/merge-sort/)。现在检查给定的条件是否满足。如果发现是真的，那么通过将当前指数和以前指数之间的差值相加来计算成本。否则，打印 **-1** 。
以下是上述方法的实施:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if given elements
// can be arranged such that sum of
// its neighbours is strictly greater
void Arrange(int arr[], int n)
{
    // Initialize the total cost
    int cost = 0;

    // Storing the original index of
    // elements in a hashmap
    unordered_map<int, int> index;

    for (int i = 0; i < n; i++) {
        index[arr[i]] = i;
    }

    // Sort the given array
    sort(arr, arr + n);

    // Check if a given condition
    // is satisfies or not
    for (int i = 0; i < n; i++) {

        // First number
        if (i == 0) {
            if (arr[i] > arr[i + 1]
                             + arr[n - 1]) {
                cout << "-1";
                return;
            }
            else {

                // Add the cost to overall cost
                cost += abs(index[arr[i]] - i);
            }
        }

        // Last number
        else if (i == n - 1) {
            if (arr[i] > arr[i - 1]
                             + arr[0]) {
                cout << "-1";
                return;
            }
            else {

                // Add the cost to
                // overall cost
                cost += abs(index[arr[i]] - i);
            }
        }

        else {
            if (arr[i] > arr[i - 1]
                             + arr[i + 1]) {
                cout << "-1";
                return;
            }
            else {

                // Add the cost to
                // overall cost
                cost += abs(index[arr[i]] - i);
            }
        }
    }

    // Printing the cost
    cout << cost;
    return;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 4, 5, 1, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    Arrange(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if given elements
// can be arranged such that sum of
// its neighbors is strictly greater
static void Arrange(int arr[], int n)
{

    // Initialize the total cost
    int cost = 0;

    // Storing the original index of
    // elements in a hashmap
    HashMap<Integer,
            Integer> index = new HashMap<Integer,
                                         Integer>();

    for(int i = 0; i < n; i++)
    {
        index.put(arr[i], i);
    }

    // Sort the given array
    Arrays.sort(arr);

    // Check if a given condition
    // is satisfies or not
    for(int i = 0; i < n; i++)
    {

        // First number
        if (i == 0)
        {
            if (arr[i] > arr[i + 1] +
                         arr[n - 1])
            {
                System.out.print("-1");
                return;
            }
            else
            {

                // Add the cost to overall cost
                cost += Math.abs(index.get(arr[i]) - i);
            }
        }

        // Last number
        else if (i == n - 1)
        {
            if (arr[i] > arr[i - 1] +
                arr[0])
            {
                System.out.print("-1");
                return;
            }
            else
            {

                // Add the cost to
                // overall cost
                cost += Math.abs(index.get(arr[i]) - i);
            }
        }

        else
        {
            if (arr[i] > arr[i - 1] +
                         arr[i + 1])
            {
                System.out.print("-1");
                return;
            }
            else
            {

                // Add the cost to
                // overall cost
                cost += Math.abs(index.get(arr[i]) - i);
            }
        }
    }

    // Printing the cost
    System.out.print(cost);
    return;
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 2, 4, 5, 1, 3 };

    int N = arr.length;

    // Function call
    Arrange(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if given elements
# can be arranged such that sum of
# its neighbours is strictly greater
def Arrange(arr, n):

    # Initialize the total cost
    cost = 0

    # Storing the original index of
    # elements in a hashmap
    index = {}

    for i in range(n):
        index[arr[i]] = i

    # Sort the given array
    arr.sort()

    # Check if a given condition
    # is satisfies or not
    for i in range(n):

        # First number
        if(i == 0):
            if(arr[i] > arr[i + 1] + arr[-1]):
                print("-1")
                return
            else:

                # Add the cost to overall cost
                cost += abs(index[arr[i]] - i)

        # Last number
        elif(i == n - 1):
            if(arr[i] > arr[i - 1] + arr[0]):
                print("-1")
                return
            else:

                # Add the cost to
                # overall cost
                cost += abs(index[arr[i]] - i)

        else:

            if(arr[i] > arr[i - 1] + arr[i + 1]):
                print("-1")
                return
            else:

                # Add the cost to
                # overall cost
                cost += abs(index[arr[i]] - i)

    # Printing the cost
    print(cost)
    return

# Driver Code

# Given array
arr = [ 2, 4, 5, 1, 3 ]

N = len(arr)

# Function call
Arrange(arr, N)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if given elements
// can be arranged such that sum of
// its neighbors is strictly greater
static void Arrange(int []arr, int n)
{

    // Initialize the total cost
    int cost = 0;

    // Storing the original index of
    // elements in a hashmap
    Dictionary<int,
               int> index = new Dictionary<int,
                                           int>();

    for(int i = 0; i < n; i++)
    {
        index.Add(arr[i], i);
    }

    // Sort the given array
    Array.Sort(arr);

    // Check if a given condition
    // is satisfies or not
    for(int i = 0; i < n; i++)
    {

        // First number
        if (i == 0)
        {
            if (arr[i] > arr[i + 1] +
                         arr[n - 1])
            {
                Console.Write("-1");
                return;
            }
            else
            {

                // Add the cost to overall cost
                cost += Math.Abs(index[arr[i]] - i);
            }
        }

        // Last number
        else if (i == n - 1)
        {
            if (arr[i] > arr[i - 1] +
                arr[0])
            {
                Console.Write("-1");
                return;
            }
            else
            {

                // Add the cost to
                // overall cost
                cost += Math.Abs(index[arr[i]] - i);
            }
        }

        else
        {
            if (arr[i] > arr[i - 1] +
                         arr[i + 1])
            {
                Console.Write("-1");
                return;
            }
            else
            {

                // Add the cost to
                // overall cost
                cost += Math.Abs(index[arr[i]] - i);
            }
        }
    }

    // Printing the cost
    Console.Write(cost);
    return;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 2, 4, 5, 1, 3 };

    int N = arr.Length;

    // Function call
    Arrange(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to check if given elements
// can be arranged such that sum of
// its neighbours is strictly greater
function Arrange(arr, n)
{
    // Initialize the total cost
    let cost = 0;

    // Storing the original index of
    // elements in a hashmap
     let index = new Map();

    for (let i = 0; i < n; i++) {
        index.set(arr[i], i)
    }

    // Sort the given array
    arr.sort();

    // Check if a given condition
    // is satisfies or not
    for (let i = 0; i < n; i++) {

        // First number
        if (i == 0) {
            if (arr[i] > arr[i + 1] + arr[n - 1]) {
                document.write("-1");
                return;
            }
            else {

                // Add the cost to overall cost
                cost += Math.abs(index.get(arr[i]) - i);
            }
        }

        // Last number
        else if (i == n - 1) {
            if (arr[i] > arr[i - 1] + arr[0]) {
                document.write("-1");
                return;
            }
            else {

                // Add the cost to
                // overall cost
                cost += Math.abs(index.get(arr[i]) - i);
            }
        }

        else {
            if (arr[i] > arr[i - 1] + arr[i + 1]) {
                document.write("-1");
                return;
            }
            else {

                // Add the cost to
                // overall cost
                cost += Math.abs(index.get(arr[i]) - i);
            }
        }
    }

    // Printing the cost
    document.write(cost);
    return;
}

// Driver Code

    // Given array
    let arr = [ 2, 4, 5, 1, 3 ];

    let N = arr.length;

    // Function call
    Arrange(arr, N);

    // This code is contributed by Dharanendra L V.

</script>
```

**输出:**

```
10
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*
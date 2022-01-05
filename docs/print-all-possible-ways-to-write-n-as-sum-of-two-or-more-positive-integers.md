# 打印将 N 写成两个或多个正整数之和的所有可能方式

> 原文:[https://www . geesforgeks . org/print-所有可能的方法-将 n 写成两个或更多正整数的和/](https://www.geeksforgeeks.org/print-all-possible-ways-to-write-n-as-sum-of-two-or-more-positive-integers/)

给定一个整数 **N** ，任务是打印所有可能的方式，其中 **N** 可以写成两个或多个正整数的和。
**例:**

> **输入:**N = 4
> T3】输出:T5】1 1 1 1
> 1 1 2
> 1 3
> 2
> T10】输入:N = 3
> T13】输出:T15】1 1 1
> 1 2

**方法:**思路是用[递归](https://www.geeksforgeeks.org/recursion/)来解决这个问题。想法是考虑从 **1 到 N** 的每一个整数，这样在每次递归调用中，和 N 可以被这个数减少，如果在任何递归调用中，N 减少到零，那么我们将打印存储在向量中的答案。以下是递归的步骤:

1.  得到数 **N** ，其和必须被分解成两个或多个正整数。
2.  递归地从值 **1 迭代到 N** 作为索引 **i** :

*   **基本情况:**如果递归调用的值是 **0** ，那么打印当前向量，因为这是将 N 分解成两个或更多正整数的方法之一。

```
if (n == 0)
    printVector(arr);
```

*   **递归调用:**如果不满足基本情况，则从**【I，N–I】**递归迭代。将当前元素 **j** 推入向量(比如 **arr** )并递归迭代下一个索引，在这个递归结束后，弹出之前插入的元素**j【T9:** 

```
for j in range[i, N]:
    arr.push_back(j);
    recursive_function(arr, j + 1, N - j);
    arr.pop_back(j);   
```

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the values stored
// in vector arr
void printVector(vector<int>& arr)
{
    if (arr.size() != 1) {

        // Traverse the vector arr
        for (int i = 0; i < arr.size(); i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
}

// Recursive function to print different
// ways in which N can be written as
// a sum of at 2 or more positive integers
void findWays(vector<int>& arr, int i, int n)
{
    // If n is zero then print this
    // ways of breaking numbers
    if (n == 0)
        printVector(arr);

    // Start from previous element
    // in the representation till n
    for (int j = i; j <= n; j++) {

        // Include current element
        // from representation
        arr.push_back(j);

        // Call function again
        // with reduced sum
        findWays(arr, j, n - j);

        // Backtrack to remove current
        // element from representation
        arr.pop_back();
    }
}

// Driver Code
int main()
{
    // Given sum N
    int n = 4;

    // To store the representation
    // of breaking N
    vector<int> arr;

    // Function Call
    findWays(arr, 1, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the values stored
// in vector arr
static void printVector(ArrayList<Integer> arr)
{
    if (arr.size() != 1)
    {

        // Traverse the vector arr
        for(int i = 0; i < arr.size(); i++)
        {
            System.out.print(arr.get(i) + " ");
        }
        System.out.println();
    }
}

// Recursive function to print different
// ways in which N can be written as
// a sum of at 2 or more positive integers
static void findWays(ArrayList<Integer> arr,
                     int i, int n)
{

    // If n is zero then print this
    // ways of breaking numbers
    if (n == 0)
        printVector(arr);

    // Start from previous element
    // in the representation till n
    for(int j = i; j <= n; j++)
    {

        // Include current element
        // from representation
        arr.add(j);

        // Call function again
        // with reduced sum
        findWays(arr, j, n - j);

        // Backtrack to remove current
        // element from representation
        arr.remove(arr.size() - 1);
    }
}

// Driver code
public static void main(String[] args)
{

    // Given sum N
    int n = 4;

    // To store the representation
    // of breaking N
    ArrayList<Integer> arr = new ArrayList<Integer>();

    // Function call
    findWays(arr, 1, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the values stored
# in vector arr
def printVector(arr):

    if (len(arr) != 1):

        # Traverse the vector arr
        for i in range(len(arr)):
            print(arr[i], end = " ")
        print()   

# Recursive function to prdifferent
# ways in which N can be written as
# a sum of at 2 or more positive integers
def findWays(arr, i, n):

    # If n is zero then prthis
    # ways of breaking numbers
    if (n == 0):
        printVector(arr)

    # Start from previous element
    # in the representation till n
    for j in range(i, n + 1):

        # Include current element
        # from representation
        arr.append(j)

        # Call function again
        # with reduced sum
        findWays(arr, j, n - j)

        # Backtrack to remove current
        # element from representation
        del arr[-1]

# Driver Code
if __name__ == '__main__':

    # Given sum N
    n = 4

    # To store the representation
    # of breaking N
    arr = []

    # Function Call
    findWays(arr, 1, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the values stored
// in vector arr
static void printList(List<int> arr)
{
    if (arr.Count != 1)
    {

        // Traverse the vector arr
        for(int i = 0; i < arr.Count; i++)
        {
            Console.Write(arr[i] + " ");
        }
        Console.WriteLine();
    }
}

// Recursive function to print different
// ways in which N can be written as
// a sum of at 2 or more positive integers
static void findWays(List<int> arr,
                     int i, int n)
{

    // If n is zero then print this
    // ways of breaking numbers
    if (n == 0)
        printList(arr);

    // Start from previous element
    // in the representation till n
    for(int j = i; j <= n; j++)
    {

        // Include current element
        // from representation
        arr.Add(j);

        // Call function again
        // with reduced sum
        findWays(arr, j, n - j);

        // Backtrack to remove current
        // element from representation
        arr.RemoveAt(arr.Count - 1);
    }
}

// Driver code
public static void Main(String[] args)
{

    // Given sum N
    int n = 4;

    // To store the representation
    // of breaking N
    List<int> arr = new List<int>();

    // Function call
    findWays(arr, 1, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the values stored
// in vector arr
function printVector(arr)
{
    if (arr.length != 1) {

        // Traverse the vector arr
        for (var i = 0; i < arr.length; i++) {
            document.write( arr[i] + " ");
        }
        document.write("<br>");
    }
}

// Recursive function to print different
// ways in which N can be written as
// a sum of at 2 or more positive integers
function findWays(arr, i, n)
{
    // If n is zero then print this
    // ways of breaking numbers
    if (n == 0)
        printVector(arr);

    // Start from previous element
    // in the representation till n
    for (var j = i; j <= n; j++) {

        // Include current element
        // from representation
        arr.push(j);

        // Call function again
        // with reduced sum
        findWays(arr, j, n - j);

        // Backtrack to remove current
        // element from representation
        arr.pop();
    }
}

// Driver Code
// Given sum N
var n = 4;
// To store the representation
// of breaking N
var arr = [];
// Function Call
findWays(arr, 1, n);

</script>
```

**Output:** 

```
1 1 1 1 
1 1 2 
1 3 
2 2
```

**时间复杂度:**O(2<sup>N</sup>)
T5】辅助空间: O(N <sup>2</sup> )
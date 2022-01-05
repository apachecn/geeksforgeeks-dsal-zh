# 给定数量的 Spt 函数或最小零件函数

> 原文:[https://www . geesforgeks . org/SPT-给定数字的功能或最小部分功能/](https://www.geeksforgeeks.org/spt-function-or-smallest-parts-function-of-a-given-number/)

给定一个整数 **N，**任务是找到数字 N 的 [Spt 函数](https://en.wikipedia.org/wiki/Spt_function)

> spt 函数(最小部分函数)是数论中的一个函数，它计算正整数的每个分区中最小部分的数量之和。它与分区函数有关。
> 例如，4 的分区是[1，1，1，1]，[1，1，2]，[2，2]，[1，3]，[4]。1 在第一个中出现 4 次，1 在第二个中出现两次，2 在第三个中出现两次，等等。；因此 spt(4) = 4 + 2 + 2 + 1 + 1 = 10。

**示例:**

> **输入:** N = 4
> **输出:** 10
> **说明:**
> 4 的分区为[1，1，1，1]，[1，1，2]，[2，2]，[1，3]，[4]。
> 1 在第一次出现 4 次，1 在第二次出现 2 次，2 在第三次出现 2 次等。
> 因此，spt(4) = 4 + 2 + 2 + 1 + 1 = 10
> 
> **输入:**5
> T3】输出: 14

**逼近**:思路是考虑从 1 到 N 的每一个整数，并将其加入到一个答案向量中，对于和减少的剩余元素再次递归。为了避免再次打印相同的制图表达，每个制图表达都将按升序构建。如果达到 **N** 的表示，我们将找到答案向量中最小元素出现的频率，并添加到 Spt 值变量中，最后打印 Spt 变量的值。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// Spt Function to given number

#include <bits/stdc++.h>
using namespace std;

// variable to store spt
// function of a number
int spt = 0;

// Function to add value
// of frequency of minimum element
// among all representations of n
void printVector(vector<int>& arr)
{
    int min_i = INT_MAX;
    for (int i = 0; i < arr.size(); i++)
        min_i = min(min_i, arr[i]);

    // find the value of frequency
    // of minimum element
    int freq = count(arr.begin(),
                     arr.end(),
                     min_i);

    // calculate spt
    spt += freq;
}

// Recursive function to find
// different ways in which
// n can be written as a sum of
// at one or more positive integers
void findWays(vector<int>& arr,
              int i, int n)
{
    // if sum becomes n,
    // consider this representation
    if (n == 0)
        printVector(arr);

    // start from previous element
    // in the representation till n
    for (int j = i; j <= n; j++) {

        // include current element
        // from representation
        arr.push_back(j);

        // call function again
        // with reduced sum
        findWays(arr, j, n - j);

        // backtrack - remove current
        // element from representation
        arr.pop_back();
    }
}

// Function to find
// the spt function
void spt_function(int n)
{

    vector<int> arr;

    // Using recurrence find
    // different ways in which
    // n can be written as a sum of
    // at 1 or more positive integers
    findWays(arr, 1, n);

    cout << spt;
}

// Driver Code
int main()
{
    int N = 4;
    spt_function(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Spt Function to given number
import java.util.*;

class GFG{

// Variable to store spt
// function of a number
static int spt = 0;

// Find the value of frequency
// of minimum element
static int count(Vector<Integer> arr, int min_i)
{
    int count = 0;

    for(int i = 0; i < arr.size(); i++)
        if(min_i == arr.get(i))
        count++;

    return count;
}

// Function to add value of
// frequency of minimum element
// among all representations of n
static void printVector(Vector<Integer> arr)
{
    int min_i = Integer.MAX_VALUE;
    for(int i = 0; i < arr.size(); i++)
        min_i = Math.min(min_i, arr.elementAt(i));

    // Find the value of frequency
    // of minimum element
    int freq = count(arr, min_i);

    // Calculate spt
    spt += freq;
}

// Recursive function to find
// different ways in which
// n can be written as a sum of
// at one or more positive integers
static void findWays(Vector<Integer> arr,
                     int i, int n)
{

    // If sum becomes n, consider
    // this representation
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

        // backtrack - remove current
        // element from representation
        arr.remove(arr.size() - 1);
    }
}

// Function to find
// the spt function
static void spt_function(int n)
{
    Vector<Integer> arr = new Vector<>();

    // Using recurrence find
    // different ways in which
    // n can be written as a sum of
    // at 1 or more positive integers
    findWays(arr, 1, n);

    System.out.print(spt);
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;

    spt_function(N);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation to find the
# Spt Function to given number
import sys

# Variable to store spt
# function of a number
spt = 0

# Function to add value
# of frequency of minimum element
# among all representations of n
def printVector(arr):

    global spt

    min_i = sys.maxsize
    for i in range(len(arr)):
        min_i = min(min_i, arr[i])

    # Find the value of frequency
    # of minimum element
    freq = arr.count(min_i)

    # Calculate spt
    spt += freq

# Recursive function to find
# different ways in which
# n can be written as a sum of
# at one or more positive integers
def findWays(arr, i, n):

    # If sum becomes n,
    # consider this representation
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

        # Backtrack - remove current
        # element from representation
        del arr[-1]

# Function to find
# the spt function
def spt_function(n):

    arr = []

    # Using recurrence find
    # different ways in which
    # n can be written as a sum of
    # at 1 or more positive integers
    findWays(arr, 1, n)

    print(spt)

# Driver Code
if __name__ == '__main__':

    N = 4
    spt_function(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the
// Spt Function to given number
using System;
using System.Collections.Generic;

class GFG{

// Variable to store spt
// function of a number
static int spt = 0;

// Find the value of frequency
// of minimum element
static int count(List<int> arr, int min_i)
{
    int count = 0;

    for(int i = 0; i < arr.Count; i++)
        if (min_i == arr[i])
            count++;

    return count;
}

// Function to add value of
// frequency of minimum element
// among all representations of n
static void printList(List<int> arr)
{
    int min_i = int.MaxValue;
    for(int i = 0; i < arr.Count; i++)
        min_i = Math.Min(min_i, arr[i]);

    // Find the value of frequency
    // of minimum element
    int freq = count(arr, min_i);

    // Calculate spt
    spt += freq;
}

// Recursive function to find
// different ways in which
// n can be written as a sum of
// at one or more positive integers
static void findWays(List<int> arr,
                          int i, int n)
{

    // If sum becomes n, consider
    // this representation
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

        // backtrack - remove current
        // element from representation
        arr.RemoveAt(arr.Count - 1);
    }
}

// Function to find
// the spt function
static void spt_function(int n)
{
    List<int> arr = new List<int>();

    // Using recurrence find
    // different ways in which
    // n can be written as a sum of
    // at 1 or more positive integers
    findWays(arr, 1, n);

    Console.Write(spt);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 4;

    spt_function(N);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// Spt Function to given number

// variable to store spt
// function of a number
var spt = 0;

// Function to add value
// of frequency of minimum element
// among all representations of n
function printVector(arr)
{
    var min_i = 1000000000;
    for (var i = 0; i < arr.length; i++)
        min_i = Math.min(min_i, arr[i]);

    // find the value of frequency
    // of minimum element
    var freq = 0;

    for(var i =0;i<arr.length; i++)
    {
       if( arr[i] == min_i)
          freq++;
    }

    // calculate spt
    spt += freq;
}

// Recursive function to find
// different ways in which
// n can be written as a sum of
// at one or more positive integers
function findWays(arr, i, n)
{
    // if sum becomes n,
    // consider this representation
    if (n == 0)
        printVector(arr);

    // start from previous element
    // in the representation till n
    for (var j = i; j <= n; j++) {

        // include current element
        // from representation
        arr.push(j);

        // call function again
        // with reduced sum
        findWays(arr, j, n - j);

        // backtrack - remove current
        // element from representation
        arr.pop();
    }
}

// Function to find
// the spt function
function spt_function( n)
{

    var arr = [];

    // Using recurrence find
    // different ways in which
    // n can be written as a sum of
    // at 1 or more positive integers
    findWays(arr, 1, n);

    document.write( spt);
}

// Driver Code
var N = 4;
spt_function(N);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
10
```
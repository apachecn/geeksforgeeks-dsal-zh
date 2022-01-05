# 数组中最大和最小的斐波那契数

> 原文:[https://www . geeksforgeeks . org/最大和最小斐波那契数列/](https://www.geeksforgeeks.org/largest-and-smallest-fibonacci-numbers-in-an-array/)

给定一个由正整数 **N** 组成的**数组 arr[]** ，任务是找出给定数组中的最小(最小)和最大(最大)斐波那契元素。
**例:**

> **输入:** arr[] = 1，2，3，4，5，6，7
> **输出:** 1，5
> **解释:**
> 数组包含 4 个斐波那契值 1，2，3 和 5。
> 因此，最大值为 5，最小值为 1。
> **输入:** arr[] = 13，3，15，6，8，11
> **输出:** 3，13
> **解释:**
> 数组包含 3 个斐波那契值 13，3 和 8。
> 因此，最大值为 13，最小值为 3。

**方法:**这种方法类似于寻找数组中的最小和最大元素。逐个遍历数组，检查是否是斐波那契数。如果是，那么在这些数字中找出最大值和最小值。
为了检查该数字是否是斐波那契数，或者不是最优的 0(1)，使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)生成数组中最大元素之前的所有斐波那契数，并将其存储在哈希表中。
**以下是上述方法的实施:**

## C++

```
// C++ program to find minimum and maximum
// fibonacci number in given array
#include <bits/stdc++.h>
using namespace std;

// Function to create hash table
// to check Fibonacci numbers
void createHash(set<int>& hash,
                int maxElement)
{
    // Insert initial two numbers
    // in the hash table
    int prev = 0, curr = 1;
    hash.insert(prev);
    hash.insert(curr);

    while (curr <= maxElement) {

        // Sum of previous two numbers
        int temp = curr + prev;

        hash.insert(temp);

        // Update the variable each time
        prev = curr;
        curr = temp;
    }
}

// Function to find minimum and maximum
// fibonacci number in given array
void fibonacci(int arr[], int n)
{

    // Find maximum value in the array
    int max_val
        = *max_element(
            arr, arr + n);

    // Creating a set containing
    // all Fibonacci numbers up to
    // maximum value in the array
    set<int> hash;
    createHash(hash, max_val);

    // For storing the Minimum
    // and Maximum Fibonacci number
    int minimum = INT_MAX;
    int maximum = INT_MIN;

    for (int i = 0; i < n; i++) {

        // Check if current element
        // is a fibonacci number
        if (hash.find(arr[i]) != hash.end()) {

            // Update the maximum and
            // minimum accordingly
            minimum = min(minimum, arr[i]);
            maximum = max(maximum, arr[i]);
        }
    }

    cout << minimum << ", "
         << maximum << endl;
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    fibonacci(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum and maximum
// fibonacci number in given array
import java.util.*;

class GFG{

// Function to create hash table
// to check Fibonacci numbers
static void createHash(HashSet<Integer> hash,
                int maxElement)
{
    // Insert initial two numbers
    // in the hash table
    int prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    while (curr <= maxElement) {

        // Sum of previous two numbers
        int temp = curr + prev;

        hash.add(temp);

        // Update the variable each time
        prev = curr;
        curr = temp;
    }
}

// Function to find minimum and maximum
// fibonacci number in given array
static void fibonacci(int arr[], int n)
{

    // Find maximum value in the array
    int max_val= Arrays.stream(arr).max().getAsInt();

    // Creating a set containing
    // all Fibonacci numbers up to
    // maximum value in the array
    HashSet<Integer> hash = new HashSet<Integer>();
    createHash(hash, max_val);

    // For storing the Minimum
    // and Maximum Fibonacci number
    int minimum = Integer.MAX_VALUE;
    int maximum = Integer.MIN_VALUE;

    for (int i = 0; i < n; i++) {

        // Check if current element
        // is a fibonacci number
        if (hash.contains(arr[i])) {

            // Update the maximum and
            // minimum accordingly
            minimum = Math.min(minimum, arr[i]);
            maximum = Math.max(maximum, arr[i]);
        }
    }

    System.out.print(minimum+ ", "
         + maximum +"\n");
}

// Driver code
public static void main(String[] args)
{

    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.length;

    fibonacci(arr, n);

}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 program to find minimum and maximum
# fibonacci number in given array

import sys

# Function to create hash table
# to check Fibonacci numbers
def createHash(hash, maxElement):
    # Insert initial two numbers
    # in the hash table
    prev = 0
    curr = 1
    hash.add(prev)
    hash.add(curr)

    while (curr <= maxElement):
        # Sum of previous two numbers
        temp = curr + prev

        hash.add(temp)
        # Update the variable each time
        prev = curr
        curr = temp

# Function to find minimum and maximum
# fibonacci number in given array
def fibonacci(arr, n):

    # Find maximum value in the array
    max_val = max(arr)

    # Creating a set containing
    # all Fibonacci numbers up to
    # maximum value in the array
    hash = set()
    createHash(hash, max_val)

    # For storing the Minimum
    # and Maximum Fibonacci number
    minimum = sys.maxsize
    maximum = -sys.maxsize-1

    for i in range(n):

        # Check if current element
        # is a fibonacci number
        if (arr[i] in hash):

            # Update the maximum and
            # minimum accordingly
            minimum = min(minimum, arr[i])
            maximum = max(maximum, arr[i])

    print(minimum,end = ", ")
    print(maximum)

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6, 7]
    n = len(arr)

    fibonacci(arr, n)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to find minimum and maximum
// fibonacci number in given array
using System;
using System.Linq;
using System.Collections.Generic;

class GFG{

// Function to create hash table
// to check Fibonacci numbers
static void createHash(HashSet<int> hash,
                int maxElement)
{
    // Insert initial two numbers
    // in the hash table
    int prev = 0, curr = 1;
    hash.Add(prev);
    hash.Add(curr);

    while (curr <= maxElement) {

        // Sum of previous two numbers
        int temp = curr + prev;

        hash.Add(temp);

        // Update the variable each time
        prev = curr;
        curr = temp;
    }
}

// Function to find minimum and maximum
// fibonacci number in given array
static void fibonacci(int []arr, int n)
{

    // Find maximum value in the array
    int max_val= arr.Max();

    // Creating a set containing
    // all Fibonacci numbers up to
    // maximum value in the array
    HashSet<int> hash = new HashSet<int>();
    createHash(hash, max_val);

    // For storing the Minimum
    // and Maximum Fibonacci number
    int minimum = int.MaxValue;
    int maximum = int.MinValue;

    for (int i = 0; i < n; i++) {

        // Check if current element
        // is a fibonacci number
        if (hash.Contains(arr[i])) {

            // Update the maximum and
            // minimum accordingly
            minimum = Math.Min(minimum, arr[i]);
            maximum = Math.Max(maximum, arr[i]);
        }
    }

    Console.Write(minimum+ ", "
        + maximum +"\n");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.Length;

    fibonacci(arr, n);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to find minimum and maximum
// fibonacci number in given array

// Function to create hash table
// to check Fibonacci numbers
function createHash(hash, maxElement)
{
    // Insert initial two numbers
    // in the hash table
    let prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    while (curr <= maxElement) {

        // Sum of previous two numbers
        let temp = curr + prev;

        hash.add(temp);

        // Update the variable each time
        prev = curr;
        curr = temp;
    }
}

// Function to find minimum and maximum
// fibonacci number in given array
function fibonacci(arr, n)
{

    // Find maximum value in the array
    let max_val= Math.max(...arr);

    // Creating a set containing
    // all Fibonacci numbers up to
    // maximum value in the array
    let hash = new Set();
    createHash(hash, max_val);

    // For storing the Minimum
    // and Maximum Fibonacci number
    let minimum = Number.MAX_VALUE;
    let maximum = Number.MIN_VALUE;

    for (let i = 0; i < n; i++) {

        // Check if current element
        // is a fibonacci number
        if (hash.has(arr[i])) {

            // Update the maximum and
            // minimum accordingly
            minimum = Math.min(minimum, arr[i]);
            maximum = Math.max(maximum, arr[i]);
        }
    }

    document.write(minimum+ ", "
         + maximum +"<br/>");
}

// Driver code

      let arr = [ 1, 2, 3, 4, 5, 6, 7 ];
    let n = arr.length;

    fibonacci(arr, n);

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
1, 5
```
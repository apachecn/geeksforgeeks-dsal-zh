# 检查数组中斐波那契元素的和是否是斐波那契数

> 原文:[https://www . geesforgeks . org/check-if-sum-of-Fibonacci-elements-in-a-a-Fibonacci-number-or-not/](https://www.geeksforgeeks.org/check-if-sum-of-fibonacci-elements-in-an-array-is-a-fibonacci-number-or-not/)

给定一个包含 **N** 元素的数组 **arr[]** ，任务是检查该数组的斐波那契元素之和是否为[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
**举例:**

> **输入:** arr[] = {2，3，7，11}
> **输出:**是
> **解释:**
> 因为数组中有两个斐波那契数，即 2 和 3。
> 所以，斐波那契数之和是 2 + 3 = 5，5 也是斐波那契数。
> **输入:** arr[] = {1，2，3}
> **输出:**否

**方法:**想法是使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)来预计算并存储[斐波那契节点](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)直到最大数量，以使检查变得容易且高效(在 O(1)时间内)。
预计算后，迭代数组的所有元素。如果这个数是斐波那契数，那么把它加到和上。最后，检查总和是否是斐波那契数。
以下是上述方法的实施:

## C++

```
// C++ program to check whether the
// sum of fibonacci elements of the
// array is a Fibonacci number or not

#include <bits/stdc++.h>
#define ll long long int
#define MAX 100005
using namespace std;

// Hash to store the Fibonacci
// numbers up to Max
set<int> fibonacci;

// Function to create the hash table
// to check Fibonacci numbers
void createHash()
{
    // Inserting the first two Fibonacci
    // numbers into the hash
    int prev = 0, curr = 1;
    fibonacci.insert(prev);
    fibonacci.insert(curr);

    // Add the remaining Fibonacci numbers
    // based on the previous two numbers
    while (curr <= MAX) {
        int temp = curr + prev;
        fibonacci.insert(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to check if the sum of
// Fibonacci numbers is Fibonacci or not
bool checkArray(int arr[], int n)
{
    // Find the sum of
    // all Fibonacci numbers
    ll sum = 0;

    // Iterating through the array
    for (int i = 0; i < n; i++)
        if (fibonacci.find(arr[i])
            != fibonacci.end())
            sum += arr[i];

    // If the sum is Fibonacci
    // then return true
    if (fibonacci.find(sum)
        != fibonacci.end())
        return true;

    return false;
}

// Driver code
int main()
{
    // array of elements
    int arr[] = { 1, 2, 4, 8, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Creating a set containing
    // all fibonacci numbers
    createHash();

    if (checkArray(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether the
// sum of fibonacci elements of the
// array is a Fibonacci number or not
import java.util.*;

class GFG{

static final int MAX = 100005;

// Hash to store the Fibonacci
// numbers up to Max
static HashSet<Integer> fibonacci = new HashSet<Integer>();

// Function to create the hash table
// to check Fibonacci numbers
static void createHash()
{
    // Inserting the first two Fibonacci
    // numbers into the hash
    int prev = 0, curr = 1;
    fibonacci.add(prev);
    fibonacci.add(curr);

    // Add the remaining Fibonacci numbers
    // based on the previous two numbers
    while (curr <= MAX) {
        int temp = curr + prev;
        fibonacci.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to check if the sum of
// Fibonacci numbers is Fibonacci or not
static boolean checkArray(int arr[], int n)
{
    // Find the sum of
    // all Fibonacci numbers
    int sum = 0;

    // Iterating through the array
    for (int i = 0; i < n; i++)
        if (fibonacci.contains(arr[i]))
            sum += arr[i];

    // If the sum is Fibonacci
    // then return true
    if (fibonacci.contains(sum))
        return true;

    return false;
}

// Driver code
public static void main(String[] args)
{
    // array of elements
    int arr[] = { 1, 2, 4, 8, 2 };
    int n = arr.length;

    // Creating a set containing
    // all fibonacci numbers
    createHash();

    if (checkArray(arr, n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to check whether the
# sum of fibonacci elements of the
# array is a Fibonacci number or not

MAX = 100005

# Hash to store the Fibonacci
# numbers up to Max
fibonacci = set()

# Function to create the hash table
# to check Fibonacci numbers
def createHash():

    global fibonacci

    # Inserting the first two Fibonacci
    # numbers into the hash
    prev , curr = 0, 1
    fibonacci.add(prev)
    fibonacci.add(curr)

    # Add the remaining Fibonacci numbers
    # based on the previous two numbers
    while (curr <= MAX):
        temp = curr + prev
        if temp <= MAX:
            fibonacci.add(temp)
        prev = curr
        curr = temp

# Function to check if the sum of
# Fibonacci numbers is Fibonacci or not
def checkArray(arr, n):

    # Find the sum of
    # all Fibonacci numbers
    sum = 0

    # Iterating through the array
    for i in range( n ):
        if (arr[i] in fibonacci):
            sum += arr[i]

    # If the sum is Fibonacci
    # then return true
    if (sum in fibonacci):
        return True

    return False

# Driver code
if __name__ == "__main__":

    # array of elements
    arr = [ 1, 2, 4, 8, 2 ]
    n = len(arr)

    # Creating a set containing
    # all fibonacci numbers
    createHash()

    if (checkArray(arr, n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by chitranayal
```

## C#

```
// C# program to check whether the
// sum of fibonacci elements of the
// array is a Fibonacci number or not
using System;
using System.Collections.Generic;

class GFG{

static readonly int MAX = 100005;

// Hash to store the Fibonacci
// numbers up to Max
static HashSet<int> fibonacci = new HashSet<int>();

// Function to create the hash table
// to check Fibonacci numbers
static void createHash()
{
    // Inserting the first two Fibonacci
    // numbers into the hash
    int prev = 0, curr = 1;
    fibonacci.Add(prev);
    fibonacci.Add(curr);

    // Add the remaining Fibonacci numbers
    // based on the previous two numbers
    while (curr <= MAX) {
        int temp = curr + prev;
        fibonacci.Add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to check if the sum of
// Fibonacci numbers is Fibonacci or not
static bool checkArray(int []arr, int n)
{
    // Find the sum of
    // all Fibonacci numbers
    int sum = 0;

    // Iterating through the array
    for (int i = 0; i < n; i++)
        if (fibonacci.Contains(arr[i]))
            sum += arr[i];

    // If the sum is Fibonacci
    // then return true
    if (fibonacci.Contains(sum))
        return true;

    return false;
}

// Driver code
public static void Main(String[] args)
{
    // array of elements
    int []arr = { 1, 2, 4, 8, 2 };
    int n = arr.Length;

    // Creating a set containing
    // all fibonacci numbers
    createHash();

    if (checkArray(arr, n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to check whether the
// sum of fibonacci elements of the
// array is a Fibonacci number or not

let MAX = 100005;

// Hash to store the Fibonacci
// numbers up to Max
let fibonacci = new Set();

// Function to create the hash table
// to check Fibonacci numbers
function createHash()
{
    // Inserting the first two Fibonacci
    // numbers into the hash
    let prev = 0, curr = 1;
    fibonacci.add(prev);
    fibonacci.add(curr);

    // Add the remaining Fibonacci numbers
    // based on the previous two numbers
    while (curr <= MAX) {
        let temp = curr + prev;
        fibonacci.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to check if the sum of
// Fibonacci numbers is Fibonacci or not
function checkArray(arr, n)
{
    // Find the sum of
    // all Fibonacci numbers
    let sum = 0;

    // Iterating through the array
    for (let i = 0; i < n; i++)
        if (fibonacci.has(arr[i]))
            sum += arr[i];

    // If the sum is Fibonacci
    // then return true
    if (fibonacci.has(sum))
        return true;

    return false;
}

// Driver code

      // array of elements
    let arr = [ 1, 2, 4, 8, 2 ];
    let n = arr.length;

    // Creating a set containing
    // all fibonacci numbers
    createHash();

    if (checkArray(arr, n))
        document.write("Yes");
    else
        document.write("No");

 // This code is contributed by sanjoy_62.                                                                              
</script>
```

**Output:** 

```
Yes
```
# 从给定数组中移除所有斐波纳契数

> 原文:[https://www . geeksforgeeks . org/从给定数组中移除所有斐波那契数/](https://www.geeksforgeeks.org/remove-all-the-fibonacci-numbers-from-the-given-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是移除数组中所有的[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
**举例:**

> **输入:** arr[] = {4，6，5，3，8，7，10，11，14，15}
> **输出:** 4 6 7 10 11 14 15
> **解释:**
> 数组包含 3 个斐波那契数据值 5，3 和 8。
> 这些值已从数组中删除。
> **输入:** arr[] = {2，4，7，8，9，11}
> **输出:** 4 7 9 11
> **解释:**
> 数组包含 2 个斐波那契数据值 2 和 8。
> 这些值已从数组中删除。

**方法:**思路是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)预先计算并存储[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，然后在 O(1)时间内检查一个节点是否包含斐波那契值。

1.  遍历数组，检查当前数字是否是斐波那契数列，或者是否使用预先计算的散列。
2.  如果是，则向左移动它后面的所有元素，以删除这个斐波那契数并减少数组长度的值。
3.  对数组的所有元素重复上述步骤。

以下是上述方法的实现:

## C++

```
// C++ program to remove all the
// fibonacci numbers from the
// given array

#include <bits/stdc++.h>
using namespace std;

const int sz = 1e3;

// Set to store all the Fibonacci numbers
set<int> fib;

// Function to generate Fibonacci numbers using
// Dynamic Programming and create hash table
// to check Fibonacci numbers
void fibonacci()
{
    // Storing the first two Fibonacci
    // numbers in the set
    int prev = 0, curr = 1, len = 2;
    fib.insert(prev);
    fib.insert(curr);

    // Compute the remaining Fibonacci numbers
    // until the max size and store them
    // in the set
    while (len <= sz) {
        int temp = curr + prev;
        fib.insert(temp);
        prev = curr;
        curr = temp;
        len++;
    }
}

// Function to print the elements of the array
void printArray(int arr[], int len)
{
    for (int i = 0; i < len; i++) {
        cout << arr[i] << ' ';
    }
}

// Function to remove all the Fibonacci numbers
// from the array
void removeFibonacci(int arr[], int len)
{
    // Creating a set containing
    // all the fibonacci numbers
    fibonacci();

    // Traverse the array
    for (int i = 0; i < len; i++) {

        // If the current element is fibonacci
        if (fib.find(arr[i]) != fib.end()) {

            // Shift all the elements on the
            // right of it to the left
            for (int j = i; j < len; j++) {
                arr[j] = arr[j + 1];
            }

            // Decrease the loop counter by 1
            // to check the shifted element
            i--;

            // Decrease the length
            len--;
        }
    }

    // Print the updated array
    printArray(arr, len);
}

// Driver code
int main()
{
    int arr[] = { 4, 6, 5, 3, 8, 7,
                  10, 11, 14, 15 };

    int len = sizeof(arr) / sizeof(int);

    removeFibonacci(arr, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove all the
// fibonacci numbers from the
// given array
import java.util.*;

class GFG{

static int sz = (int) 1e3;

// Set to store all the Fibonacci numbers
static HashSet<Integer> fib = new HashSet<Integer>();

// Function to generate Fibonacci numbers using
// Dynamic Programming and create hash table
// to check Fibonacci numbers
static void fibonacci()
{
    // Storing the first two Fibonacci
    // numbers in the set
    int prev = 0, curr = 1, len = 2;
    fib.add(prev);
    fib.add(curr);

    // Compute the remaining Fibonacci numbers
    // until the max size and store them
    // in the set
    while (len <= sz) {
        int temp = curr + prev;
        fib.add(temp);
        prev = curr;
        curr = temp;
        len++;
    }
}

// Function to print the elements of the array
static void printArray(int arr[], int len)
{
    for (int i = 0; i < len; i++) {
        System.out.print(arr[i] +" ");
    }
}

// Function to remove all the Fibonacci numbers
// from the array
static void removeFibonacci(int arr[], int len)
{
    // Creating a set containing
    // all the fibonacci numbers
    fibonacci();

    // Traverse the array
    for (int i = 0; i < len; i++) {

        // If the current element is fibonacci
        if (fib.contains(arr[i])) {

            // Shift all the elements on the
            // right of it to the left
            for (int j = i; j < len - 1; j++) {
                arr[j] = arr[j + 1];
            }

            // Decrease the loop counter by 1
            // to check the shifted element
            i--;

            // Decrease the length
            len--;
        }
    }

    // Print the updated array
    printArray(arr, len);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 6, 5, 3, 8, 7,
                  10, 11, 14, 15 };

    int len = arr.length;
    removeFibonacci(arr, len);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to remove all the
# fibonacci numbers from the
# given array

sz = 1000

# Set to store all the Fibonacci numbers
fib = set()

# Function to generate Fibonacci numbers using
# Dynamic Programming and create hash table
# to check Fibonacci numbers
def fibonacci():

    # Storing the first two Fibonacci
    # numbers in the set
    prev , curr , length = 0 , 1, 2
    fib.add(prev)
    fib.add(curr)

    # Compute the remaining Fibonacci numbers
    # until the max size and store them
    # in the set
    while (length <= sz):
        temp = curr + prev
        fib.add(temp)
        prev = curr
        curr = temp
        length += 1

# Function to print the elements of the array
def printArray( arr, length):

    for i in range(length):
        print(arr[i],end=" ")

# Function to remove all the Fibonacci numbers
# from the array
def removeFibonacci( arr, length):

    # Creating a set containing
    # all the fibonacci numbers
    fibonacci()

    # Traverse the array
    for i in fib:
        if i in arr:
            arr.remove(i)
            length -= 1

    # Print the updated array
    printArray(arr, length)

# Driver code
if __name__ == "__main__":

    arr = [ 4, 6, 5, 3, 8, 7,
                10, 11, 14, 15 ]

    length = len(arr)
    removeFibonacci(arr, length)

# This code is contributed by chitranayal
```

## C#

```
// C# program to remove all the
// fibonacci numbers from the
// given array
using System;
using System.Collections.Generic;

class GFG{

static int sz = (int) 1e3;

// Set to store all the Fibonacci numbers
static HashSet<int> fib = new HashSet<int>();

// Function to generate Fibonacci numbers using
// Dynamic Programming and create hash table
// to check Fibonacci numbers
static void fibonacci()
{
    // Storing the first two Fibonacci
    // numbers in the set
    int prev = 0, curr = 1, len = 2;
    fib.Add(prev);
    fib.Add(curr);

    // Compute the remaining Fibonacci numbers
    // until the max size and store them
    // in the set
    while (len <= sz) {
        int temp = curr + prev;
        fib.Add(temp);
        prev = curr;
        curr = temp;
        len++;
    }
}

// Function to print the elements of the array
static void printArray(int []arr, int len)
{
    for (int i = 0; i < len; i++) {
        Console.Write(arr[i] +" ");
    }
}

// Function to remove all the Fibonacci numbers
// from the array
static void removeFibonacci(int []arr, int len)
{
    // Creating a set containing
    // all the fibonacci numbers
    fibonacci();

    // Traverse the array
    for (int i = 0; i < len; i++) {

        // If the current element is fibonacci
        if (fib.Contains(arr[i])) {

            // Shift all the elements on the
            // right of it to the left
            for (int j = i; j < len - 1; j++) {
                arr[j] = arr[j + 1];
            }

            // Decrease the loop counter by 1
            // to check the shifted element
            i--;

            // Decrease the length
            len--;
        }
    }

    // Print the updated array
    printArray(arr, len);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 6, 5, 3, 8, 7,
                  10, 11, 14, 15 };

    int len = arr.Length;
    removeFibonacci(arr, len);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to remove all the
// fibonacci numbers from the
// given array

let sz = 1e3;

// Set to store all the Fibonacci numbers
let fib = new Set();

// Function to generate Fibonacci numbers using
// Dynamic Programming and create hash table
// to check Fibonacci numbers
function fibonacci()
{
    // Storing the first two Fibonacci
    // numbers in the set
    let prev = 0, curr = 1, len = 2;
    fib.add(prev);
    fib.add(curr);

    // Compute the remaining Fibonacci numbers
    // until the max size and store them
    // in the set
    while (len <= sz) {
        let temp = curr + prev;
        fib.add(temp);
        prev = curr;
        curr = temp;
        len++;
    }
}

// Function to print the elements of the array
function printArray(arr, len)
{
    for (let i = 0; i < len; i++) {
        document.write(arr[i] +" ");
    }
}

// Function to remove all the Fibonacci numbers
// from the array
function removeFibonacci(arr, len)
{
    // Creating a set containing
    // all the fibonacci numbers
    fibonacci();

    // Traverse the array
    for (let i = 0; i < len; i++) {

        // If the current element is fibonacci
        if (fib.has(arr[i])) {

            // Shift all the elements on the
            // right of it to the left
            for (let j = i; j < len - 1; j++) {
                arr[j] = arr[j + 1];
            }

            // Decrease the loop counter by 1
            // to check the shifted element
            i--;

            // Decrease the length
            len--;
        }
    }

    // Print the updated array
    printArray(arr, len);
}

// Driver code

      let arr = [ 4, 6, 5, 3, 8, 7,
                  10, 11, 14, 15 ];

    let len = arr.length;
    removeFibonacci(arr, len);

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
4 6 7 10 11 14 15
```
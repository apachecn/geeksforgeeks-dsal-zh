# 来自两个阵列的完全不同的对，这样通过反转第一个

的位可以获得第二个数

> 原文:[https://www . geeksforgeeks . org/total-distinct-pairs-from-two-array-这样-第二个数字可以通过反转第一个数字的位来获得/](https://www.geeksforgeeks.org/total-distinct-pairs-from-two-arrays-such-that-second-number-can-be-obtained-by-inverting-bits-of-first/)

给定两个数组 **arr1[]** 和 **arr2[]** ，任务是从第一个数组**(比如说 a)** 中获取一个元素，从第二个数组**(比如说 b)** 中获取一个元素。如果 **a** 的位反相形成的数等于 **b** ，则对 **(a，b)** 为有效对。
**位反转示例:**
**11** 用二进制写成 **1011** 。反转位后，得到 **0100** ，十进制为 **4** 。因此 **(11，4)** 是有效的一对，但是 **(4，11)不是**，因为 **11** 在反转 **4** 的数字后无法获得，即 **100 - > 011** ，也就是 **3** 。
**举例:**

> **输入:** arr1[] = {11，5，4}，arr2[] = {1，4，3，11}
> **输出:** 2
> (11，4)和(4，3)是唯一有效的对。
> **输入:** arr1[] = {43，7，1，99}，arr2 = {5，1，28，20}
> **输出:** 2

**进场:**

*   取两个空[套](https://www.geeksforgeeks.org/set-in-cpp-stl/) **s1** 和 **s2** 。
*   将 **arr2[]** 的所有元素插入 **s2** 中。
*   迭代第一个数组。如果第一组中不存在该元素，并且第二组中存在通过反转其位形成的数，则增加计数并将当前元素插入 **s1** 中，这样就不会再次计数。
*   最后打印**计数**的值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number formed
// by inverting bits the bits of num
int invertBits(int num)
{
    // Number of bits in num
    int x = log2(num) + 1;

    // Inverting the bits one by one
    for (int i = 0; i < x; i++)
        num = (num ^ (1 << i));

    return num;
}

// Function to return the total valid pairs
int totalPairs(int arr1[], int arr2[], int n, int m)
{

    // Set to store the elements of the arrays
    unordered_set<int> s1, s2;

    // Insert all the elements of arr2[] in the set
    for (int i = 0; i < m; i++)
        s2.insert(arr2[i]);

    // Initialize count variable to 0
    int count = 0;
    for (int i = 0; i < n; i++) {

        // Check if element of the first array
        // is not in the first set
        if (s1.find(arr1[i]) == s1.end()) {

            // Check if the element formed by inverting bits
            // is in the second set
            if (s2.find(invertBits(arr1[i])) != s2.end()) {

                // Increment the count of valid pairs and insert
                // the element in the first set so that
                // it doesn't get counted again
                count++;
                s1.insert(arr1[i]);
            }
        }
    }

    // Return the total number of pairs
    return count;
}

// Driver code
int main()
{
    int arr1[] = { 43, 7, 1, 99 };
    int arr2[] = { 5, 1, 28, 20 };
    int n = sizeof(arr1) / sizeof(arr1[0]);
    int m = sizeof(arr2) / sizeof(arr2[0]);

    cout << totalPairs(arr1, arr2, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG
{

static int log2(int N)
{
    // calculate log2 N indirectly
    // using log() method
    int result = (int)(Math.log(N) / Math.log(2));

    return result;
}

// Function to return the number formed
// by inverting bits the bits of num
static int invertBits(int num)
{
    // Number of bits in num
    int x = log2(num) + 1;

    // Inverting the bits one by one
    for (int i = 0; i < x; i++)
        num = (num ^ (1 << i));

    return num;
}

// Function to return the total valid pairs
static int totalPairs(int arr1[], int arr2[], int n, int m)
{

    // Set to store the elements of the arrays
    HashSet<Integer> s1 = new HashSet<Integer>();
    HashSet<Integer> s2 = new HashSet<Integer>();

    // add all the elements of arr2[] in the set
    for (int i = 0; i < m; i++)
        s2.add(arr2[i]);

    // Initialize count variable to 0
    int count = 0;
    for (int i = 0; i < n; i++)
    {

        // Check if element of the first array
        // is not in the first set
        if (!s1.contains(arr1[i]))
        {

            // Check if the element formed by inverting bits
            // is in the second set
            if (s2.contains(invertBits(arr1[i])))
            {

                // Increment the count of valid pairs and add
                // the element in the first set so that
                // it doesn't get counted again
                count++;
                s1.add(arr1[i]);
            }
        }
    }

    // Return the total number of pairs
    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = { 43, 7, 1, 99 };
    int arr2[] = { 5, 1, 28, 20 };
    int n = arr1.length;
    int m = arr2.length;

    System.out.println(totalPairs(arr1, arr2, n, m));
}
}

// This code is contributed by SHUBHAMSINGH10
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import log2;

# Function to return the number formed
# by inverting bits the bits of num
def invertBits(num) :

    # Number of bits in num
    x = log2(num) + 1;

    # Inverting the bits one by one
    for i in range(int(x)) :
        num = (num ^ (1 << i));

    return num;

# Function to return the total valid pairs
def totalPairs(arr1, arr2, n, m) :

    # Set to store the elements of the arrays
    s1, s2 = set(), set();

    # Insert all the elements of
    # arr2[] in the set
    for i in range(m) :
        s2.add(arr2[i]);

    # Initialize count variable to 0
    count = 0;
    for i in range(n) :

        # Check if element of the first array
        # is not in the first set
        if arr1[i] not in s1 :

            # Check if the element formed by
            # inverting bits is in the second set
            if invertBits(arr1[i]) in s2 :

                # Increment the count of valid pairs
                # and insert the element in the first
                # set so that it doesn't get counted again
                count += 1;
                s1.add(arr1[i]);

    # Return the total number of pairs
    return count;

# Driver code
if __name__ == "__main__" :

    arr1 = [ 43, 7, 1, 99 ];
    arr2 = [ 5, 1, 28, 20 ];
    n = len(arr1);
    m = len(arr2);

    print(totalPairs(arr1, arr2, n, m));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static int log2(int N)
{
    // calculate log2 N indirectly
    // using log() method
    int result = (int)(Math.Log(N) / Math.Log(2));

    return result;
}

// Function to return the number formed
// by inverting bits the bits of num
static int invertBits(int num)
{
    // Number of bits in num
    int x = log2(num) + 1;

    // Inverting the bits one by one
    for (int i = 0; i < x; i++)
        num = (num ^ (1 << i));

    return num;
}

// Function to return the total valid pairs
static int totalPairs(int []arr1, int []arr2, int n, int m)
{

    // Set to store the elements of the arrays
    HashSet<int> s1 = new HashSet<int>();
    HashSet<int> s2 = new HashSet<int>();

    // add all the elements of arr2[] in the set
    for (int i = 0; i < m; i++)
        s2.Add(arr2[i]);

    // Initialize count variable to 0
    int count = 0;
    for (int i = 0; i < n; i++)
    {

        // Check if element of the first array
        // is not in the first set
        if (!s1.Contains(arr1[i]))
        {

            // Check if the element formed by inverting bits
            // is in the second set
            if (s2.Contains(invertBits(arr1[i])))
            {

                // Increment the count of valid pairs and add
                // the element in the first set so that
                // it doesn't get counted again
                count++;
                s1.Add(arr1[i]);
            }
        }
    }

    // Return the total number of pairs
    return count;
}

// Driver code
public static void Main()
{
    int []arr1 = { 43, 7, 1, 99 };
    int []arr2 = { 5, 1, 28, 20 };
    int n = arr1.Length;
    int m = arr2.Length;

    Console.Write(totalPairs(arr1, arr2, n, m));
}
}

// This code is contribute by chitranayal
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number formed
// by inverting bits the bits of num
function invertBits(num)
{
    // Number of bits in num
    var x = parseInt(Math.log2(num)) + 1;

    // Inverting the bits one by one
    for (var i = 0; i < x; i++)
        num = (num ^ (1 << i));

    return num;
}

// Function to return the total valid pairs
function totalPairs(arr1, arr2, n, m)
{

    // Set to store the elements of the arrays
    var s1 = new Set();
    var s2 = new Set();

    // add all the elements of arr2[] in the set
    for (var i = 0; i < m; i++)
        s2.add(arr2[i]);

    // Initialize count variable to 0
    var count = 0;
    for (var i = 0; i < n; i++) {

        // Check if element of the first array
        // is not in the first set
        if (!s1.has(arr1[i]))
        {
            // Check if the element formed by inverting bits
            // is in the second set
            if (s2.has(invertBits(arr1[i]))) {

                // Increment the count of valid pairs and add
                // the element in the first set so that
                // it doesn't get counted again
                count++;
                s1.add(arr1[i]);
            }
        }
    }

    // Return the total number of pairs
    return count;
}

// Driver code
var arr1 = [43, 7, 1, 99];
var arr2 = [5, 1, 28, 20];
var n = arr1.length;
var m = arr2.length;
document.write( totalPairs(arr1, arr2, n, m));

</script>
```

**Output:** 

```
2
```
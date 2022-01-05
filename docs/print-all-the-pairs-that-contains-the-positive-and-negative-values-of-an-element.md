# 打印所有包含元素正负值的对

> 原文:[https://www . geesforgeks . org/print-all-the-pairs-in-包含元素的正负值/](https://www.geeksforgeeks.org/print-all-the-pairs-that-contains-the-positive-and-negative-values-of-an-element/)

给定一个不同整数的数组，打印该数组中所有具有正负值的数字对。
**注:**对子的顺序无关紧要。
**示例:**

```
Input: arr[] = { 1, -3, 2, 3, 6, -1 }
Output: -1 1 -3 3

Input: arr[] = { 4, 8, 9, -4, 1, -1, -8, -9 }
Output: -1 1 -4 4 -8 8 -9 9
```

一种**天真的方法**是运行两个循环，即使用外部循环考虑数组的每个元素，并使用内部循环在数组中搜索其相应的正/负值。同样，找到所有的配对。这种方法的时间复杂度为 0(n<sup>2</sup>)。
A **更好的方法**是使用**排序**，即首先对数组进行排序，然后对于每个负元素，做一个二分搜索法来找到它的对应项(+ve 数)。如果找到了，打印那一对。如果当前元素是正的，那么打破这个循环，因为在那之后将有所有的正数。

## C++

```
// CPP program to find pairs of positive
// and negative values present in an array.
#include <bits/stdc++.h>
using namespace std;

void printPairs(int arr[], int n)
{
    bool pair_exists = false;
    // Sort the array
    sort(arr, arr + n);

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // For every arr[i] < 0 element,
        // do a binary search for arr[i] > 0.
        if (arr[i] < 0) {

            // If found, print the pair.
            if (binary_search(arr, arr + n, -arr[i])) {
                cout << arr[i] << ", " << -arr[i] << endl;

                pair_exists = true;
            }
        }

        else
            break;
    }

    if (pair_exists == false)
        cout << "No such pair exists";
}

// Driver code
int main()
{
    int arr[] = { 4, 8, 9, -4, 1, -1, -8, -9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find pairs
// of positive and negative
// values present in an array.
import java.util.*;
class GFG
{
static void printPairs(int arr[], int n)
{
    boolean pair_exists = false;

    // Sort the array
    Arrays.sort(arr);

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // For every arr[i] < 0 element,
        // do a binary search for arr[i] > 0.
        if (arr[i] < 0)
        {

            // If found, print the pair.
            if (java.util.Arrays.binarySearch(arr, -arr[i])!=-1)
            {
                System.out.println(arr[i] + ", " + -arr[i] );

                pair_exists = true;
            }
        }

        else
            break;
    }

    if (pair_exists == false)
        System.out.println("No such pair exists");
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 4, 8, 9, -4, 1, -1, -8, -9 };
    int n =arr.length;

    printPairs(arr, n);
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find pairs of positive
# and negative values present in an array.

# function for binary search
def binary_search(a, x, lo=0, hi=None):
    if hi is None:
        hi = len(a)
    while lo < hi:
        mid = (lo+hi)//2
        midval = a[mid]
        if midval < x:
            lo = mid+1
        elif midval > x:
            hi = mid
        else:
            return mid
    return -1

def printPairs(arr, n):

    pair_exists = False
    # Sort the array
    arr.sort()

    # Traverse the array
    for i in range(n):

        # For every arr[i] < 0 element,
        # do a binary search for arr[i] > 0.
        if (arr[i] < 0):

            # If found, print the pair.
            if (binary_search(arr,-arr[i])):
                print(arr[i] , ", " , -arr[i])

                pair_exists = True

        else:
            break

    if (pair_exists == False):
        print("No such pair exists")

# Driver code
if __name__=='__main__':
    arr = [ 4, 8, 9, -4, 1, -1, -8, -9 ]
    n = len(arr)

    printPairs(arr, n)

# this code is contributed by ash264
```

## C#

```
// C# program to find pairs
// of positive and negative
// values present in an array.

using System;
public class GFG{

static void printPairs(int []arr, int n)
{
    bool pair_exists = false;

    // Sort the array
    Array.Sort(arr);

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // For every arr[i] < 0 element,
        // do a binary search for arr[i] > 0.
        if (arr[i] < 0)
        {

            // If found, print the pair.
            if (Array.BinarySearch(arr, -arr[i])!=-1)
            {
                Console.WriteLine(arr[i] + ", " + -arr[i] );

                pair_exists = true;
            }
        }

        else
            break;
    }

    if (pair_exists == false)
        Console.WriteLine("No such pair exists");
}

// Driver code
public static void Main()
{
    int []arr = { 4, 8, 9, -4, 1, -1, -8, -9 };
    int n =arr.Length;

    printPairs(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find pairs of positive
// and negative values present in an array.

function printPairs(arr, n) {
    let pair_exists = false;
    // Sort the array
    arr.sort((a, b) => a - b);

    // Traverse the array
    for (let i = 0; i < n; i++) {

        // For every arr[i] < 0 element,
        // do a binary search for arr[i] > 0.
        if (arr[i] < 0) {

            // If found, print the pair.
            if (arr.includes(-arr[i])) {
                document.write(arr[i] + ", " + -arr[i] + "<br>");

                pair_exists = true;
            }
        }

        else
            break;
    }

    if (pair_exists == false)
        document.write("No such pair exists");
}

// Driver code
let arr = [4, 8, 9, -4, 1, -1, -8, -9];
let n = arr.length;

printPairs(arr, n);

</script>
```

**Output:** 

```
-9, 9
-8, 8
-4, 4
-1, 1
```

**时间复杂度:** O(nlogn)
一种**高效的方法**是使用**散列**。以下是所需步骤:

*   开始遍历数组。
*   将所有粒子值存储在无序集中。
*   检查每个负元素，它们对应的正元素是否存在于集合中。
*   如果是，打印该对
*   此外，保持一个标志，检查是否不存在这样的对。

## C++

```
// CPP program to find pairs of positive
// and negative values present in an array
#include <bits/stdc++.h>
using namespace std;

// Function to print pairs of positive
// and negative values present in the array
void printPairs(int arr[], int n)
{
    unordered_set<int> pairs;
    bool pair_exists = false;

    // Store all the positive elements
    // in the unordered_set
    for (int i = 0; i < n; i++)
        if (arr[i] > 0)
            pairs.insert(arr[i]);

    // Start traversing the array
    for (int i = 0; i < n; i++) {

        // Check if the positive value of current
        // element exists in the set or not
        if (arr[i] < 0)
            if (pairs.find(-arr[i]) != pairs.end())

            { // Print that pair
                cout << arr[i] << ", " << -arr[i] << endl;

                pair_exists = true;
            }
    }

    if (pair_exists == false)
        cout << "No such pair exists";
}

// Driver code
int main()
{
    int arr[] = { 4, 8, 9, -4, 1, -1, -8, -9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find pairs of positive
// and negative values present in an array
import java.util.*;
class GFG
{

// Function to print pairs of positive
// and negative values present in the array
static void printPairs(int arr[], int n)
{
    Set<Integer> pairs = new HashSet<Integer>();
    boolean pair_exists = false;

    // Store all the positive elements
    // in the unordered_set
    for (int i = 0; i < n; i++)
        if (arr[i] > 0)
            pairs.add(arr[i]);

    // Start traversing the array
    for (int i = 0; i < n; i++)
    {

        // Check if the positive value of current
        // element exists in the set or not
        if (arr[i] < 0)
            if (pairs.contains(-arr[i]))
            {
                // Print that pair
                System.out.println(arr[i] + ", " + -arr[i]);

                pair_exists = true;
            }
    }

    if (pair_exists == false)
        System.out.println("No such pair exists");
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 4, 8, 9, -4, 1, -1, -8, -9 };
    int n = arr.length;

    printPairs(arr, n);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find pairs of positive
# and negative values present in an array

# Function to print pairs of positive
# and negative values present in the array
def printPairs(arr, n):

    pairs = set()
    pair_exists = False

    # Store all the positive elements
    # in the unordered_set
    for i in range(0, n):
        if arr[i] > 0:
            pairs.add(arr[i])

    # Start traversing the array
    for i in range(0, n):

        # Check if the positive value of current
        # element exists in the set or not
        if arr[i] < 0:
            if (-arr[i]) in pairs:

            # Print that pair
                print("{}, {}".format(arr[i], -arr[i]))
                pair_exists = True

    if pair_exists == False:
        print("No such pair exists")

# Driver code
if __name__ == "__main__":

    arr = [4, 8, 9, -4, 1, -1, -8, -9]
    n = len(arr)

    printPairs(arr, n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find pairs of positive
// and negative values present in an array
using System;
using System.Collections.Generic;

class GFG
{

// Function to print pairs of positive
// and negative values present in the array
static void printPairs(int []arr, int n)
{
    HashSet<int> pairs = new HashSet<int>();
    bool pair_exists = false;

    // Store all the positive elements
    // in the unordered_set
    for (int i = 0; i < n; i++)
        if (arr[i] > 0)
            pairs.Add(arr[i]);

    // Start traversing the array
    for (int i = 0; i < n; i++)
    {

        // Check if the positive value of current
        // element exists in the set or not
        if (arr[i] < 0)
            if (pairs.Contains(-arr[i]))
            {
                // Print that pair
                Console.WriteLine(arr[i] + ", " + -arr[i]);

                pair_exists = true;
            }
    }

    if (pair_exists == false)
        Console.WriteLine("No such pair exists");
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 4, 8, 9, -4, 1, -1, -8, -9 };
    int n = arr.Length;

    printPairs(arr, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find pairs of positive
// and negative values present in an array

// Function to print pairs of positive
// and negative values present in the array
function printPairs(arr,n)
{
    let pairs = new Set();
    let pair_exists = false;

    // Store all the positive elements
    // in the unordered_set
    for (let i = 0; i < n; i++)
        if (arr[i] > 0)
            pairs.add(arr[i]);

    // Start traversing the array
    for (let i = 0; i < n; i++)
    {

        // Check if the positive value of current
        // element exists in the set or not
        if (arr[i] < 0)
            if (pairs.has(-arr[i]))
            {
                // Print that pair
                document.write(arr[i] + ", " + -arr[i]+"<br>");

                pair_exists = true;
            }
    }

    if (pair_exists == false)
        document.write("No such pair exists");
}

// Driver code
let arr=[4, 8, 9, -4, 1, -1, -8, -9];
let n = arr.length;
printPairs(arr, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
-4, 4
-1, 1
-8, 8
-9, 9
```

**时间复杂度:** O(n)
# 打印整数数组中的所有波峰和波谷

> 原文:[https://www . geeksforgeeks . org/print-整数数组中的所有波峰和波谷/](https://www.geeksforgeeks.org/print-all-the-peaks-and-troughs-in-an-array-of-integers/)

给定一个整数数组 **arr[]** ，任务是打印数组中所有波峰的列表和所有波谷的另一个列表。峰是数组中大于其相邻元素的元素。类似地，槽是比其相邻元素小的元素。

**示例:**

> **输入:** arr[] = {5，10，5，7，4，3，5}
> **输出:**
> 峰值:10 7 5
> 谷值:5 5 3
> **输入:** arr[] = {1，2，3，4，5}
> **输出:**
> 峰值:5
> 谷值:1

**方法:**对于数组的每个元素，检查当前元素是波峰(元素必须大于其相邻元素)还是波谷(元素必须小于其相邻元素)。
**注意**数组的第一个和最后一个元素将有一个邻居。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns true if num is
// greater than both arr[i] and arr[j]
static bool isPeak(int arr[], int n, int num,
                   int i, int j)
{

    // If num is smaller than the element
    // on the left (if exists)
    if (i >= 0 && arr[i] > num)
        return false;

    // If num is smaller than the element
    // on the right (if exists)
    if (j < n && arr[j] > num)
        return false;
    return true;
}

// Function that returns true if num is
// smaller than both arr[i] and arr[j]
static bool isTrough(int arr[], int n, int num,
                     int i, int j)
{

    // If num is greater than the element
    // on the left (if exists)
    if (i >= 0 && arr[i] < num)
        return false;

    // If num is greater than the element
    // on the right (if exists)
    if (j < n && arr[j] < num)
        return false;
    return true;
}

void printPeaksTroughs(int arr[], int n)
{
    cout << "Peaks : ";

    // For every element
    for (int i = 0; i < n; i++) {

        // If the current element is a peak
        if (isPeak(arr, n, arr[i], i - 1, i + 1))
            cout << arr[i] << " ";
    }
    cout << endl;

    cout << "Troughs : ";

    // For every element
    for (int i = 0; i < n; i++) {

        // If the current element is a trough
        if (isTrough(arr, n, arr[i], i - 1, i + 1))
            cout << arr[i] << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 5, 10, 5, 7, 4, 3, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printPeaksTroughs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function that returns true if num is
    // greater than both arr[i] and arr[j]
    static boolean isPeak(int arr[], int n, int num,
                                    int i, int j)
    {

        // If num is smaller than the element
        // on the left (if exists)
        if (i >= 0 && arr[i] > num)
        {
            return false;
        }

        // If num is smaller than the element
        // on the right (if exists)
        if (j < n && arr[j] > num)
        {
            return false;
        }
        return true;
    }

    // Function that returns true if num is
    // smaller than both arr[i] and arr[j]
    static boolean isTrough(int arr[], int n, int num,
                                        int i, int j)
    {

        // If num is greater than the element
        // on the left (if exists)
        if (i >= 0 && arr[i] < num)
        {
            return false;
        }

        // If num is greater than the element
        // on the right (if exists)
        if (j < n && arr[j] < num)
        {
            return false;
        }
        return true;
    }

    static void printPeaksTroughs(int arr[], int n)
    {
        System.out.print("Peaks : ");

        // For every element
        for (int i = 0; i < n; i++)
        {

            // If the current element is a peak
            if (isPeak(arr, n, arr[i], i - 1, i + 1))
            {
                System.out.print(arr[i] + " ");
            }
        }
        System.out.println("");

        System.out.print("Troughs : ");

        // For every element
        for (int i = 0; i < n; i++)
        {

            // If the current element is a trough
            if (isTrough(arr, n, arr[i], i - 1, i + 1))
            {
                System.out.print(arr[i] + " ");
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {5, 10, 5, 7, 4, 3, 5};
        int n = arr.length;

        printPeaksTroughs(arr, n);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if num is
# greater than both arr[i] and arr[j]
def isPeak(arr, n, num, i, j):

    # If num is smaller than the element
    # on the left (if exists)
    if (i >= 0 and arr[i] > num):
        return False

    # If num is smaller than the element
    # on the right (if exists)
    if (j < n and arr[j] > num):
        return False
    return True

# Function that returns true if num is
# smaller than both arr[i] and arr[j]
def isTrough(arr, n, num, i, j):

    # If num is greater than the element
    # on the left (if exists)
    if (i >= 0 and arr[i] < num):
        return False

    # If num is greater than the element
    # on the right (if exists)
    if (j < n and arr[j] < num):
        return False
    return True

def printPeaksTroughs(arr, n):

    print("Peaks : ", end = "")

    # For every element
    for i in range(n):

        # If the current element is a peak
        if (isPeak(arr, n, arr[i], i - 1, i + 1)):
            print(arr[i], end = " ")
    print()

    print("Troughs : ", end = "")

    # For every element
    for i in range(n):

        # If the current element is a trough
        if (isTrough(arr, n, arr[i], i - 1, i + 1)):
            print(arr[i], end = " ")

# Driver code
arr = [5, 10, 5, 7, 4, 3, 5]
n = len(arr)

printPeaksTroughs(arr, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if num is
    // greater than both arr[i] and arr[j]
    static Boolean isPeak(int []arr, int n, int num,
                                    int i, int j)
    {

        // If num is smaller than the element
        // on the left (if exists)
        if (i >= 0 && arr[i] > num)
        {
            return false;
        }

        // If num is smaller than the element
        // on the right (if exists)
        if (j < n && arr[j] > num)
        {
            return false;
        }
        return true;
    }

    // Function that returns true if num is
    // smaller than both arr[i] and arr[j]
    static Boolean isTrough(int []arr, int n, int num,
                                        int i, int j)
    {

        // If num is greater than the element
        // on the left (if exists)
        if (i >= 0 && arr[i] < num)
        {
            return false;
        }

        // If num is greater than the element
        // on the right (if exists)
        if (j < n && arr[j] < num)
        {
            return false;
        }
        return true;
    }

    static void printPeaksTroughs(int []arr, int n)
    {
        Console.Write("Peaks : ");

        // For every element
        for (int i = 0; i < n; i++)
        {

            // If the current element is a peak
            if (isPeak(arr, n, arr[i], i - 1, i + 1))
            {
                Console.Write(arr[i] + " ");
            }
        }
        Console.WriteLine("");

        Console.Write("Troughs : ");

        // For every element
        for (int i = 0; i < n; i++)
        {

            // If the current element is a trough
            if (isTrough(arr, n, arr[i], i - 1, i + 1))
            {
                Console.Write(arr[i] + " ");
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {5, 10, 5, 7, 4, 3, 5};
        int n = arr.Length;

        printPeaksTroughs(arr, n);
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Function that returns true if num is
// greater than both arr[i] and arr[j]
function isPeak(arr, n, num, i,  j)
{

    // If num is smaller than the element
    // on the left (if exists)
    if (i >= 0 && arr[i] > num)
        return false;

    // If num is smaller than the element
    // on the right (if exists)
    if (j < n && arr[j] > num)
        return false;
    return true;
}

// Function that returns true if num is
// smaller than both arr[i] and arr[j]
function isTrough( arr, n,  num, i,  j)
{

    // If num is greater than the element
    // on the left (if exists)
    if (i >= 0 && arr[i] < num)
        return false;

    // If num is greater than the element
    // on the right (if exists)
    if (j < n && arr[j] < num)
        return false;
    return true;
}

function printPeaksTroughs( arr, n)
{
    document.write(  "Peaks : ");

    // For every element
    for (var i = 0; i < n; i++) {

        // If the current element is a peak
        if (isPeak(arr, n, arr[i], i - 1, i + 1))
            document.write( arr[i] + " ");
    }
    document.write( "<br>");

    document.write(  "Troughs : ");

    // For every element
    for (var i = 0; i < n; i++) {

        // If the current element is a trough
        if (isTrough(arr, n, arr[i], i - 1, i + 1))
            document.write( arr[i] + " ");
    }
}
var arr=[ 5, 10, 5, 7, 4, 3, 5 ];

    printPeaksTroughs(arr, 7);

</script>
```

**Output:** 

```
Peaks : 10 7 5 
Troughs : 5 5 3
```
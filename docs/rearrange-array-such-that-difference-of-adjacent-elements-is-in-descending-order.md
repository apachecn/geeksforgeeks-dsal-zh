# 重新排列数组，使相邻元素的差按降序排列

> 原文:[https://www . geeksforgeeks . org/rearray-array-so-相邻元素之差按降序排列/](https://www.geeksforgeeks.org/rearrange-array-such-that-difference-of-adjacent-elements-is-in-descending-order/)

给定一个具有 n 个整数的**数组 a 【】,任务是重新排列数组的元素，使相邻元素的差按降序排列。
**例:**** 

```
Input : arr[] = {1, 2, 3, 4, 5, 6} 
Output : 6 1 5 2 4 3
Explanation:
For first two elements the difference is abs(6-1)=5
For next two elements the difference is abs(1-5)=4
For next two elements the difference is abs(5-2)=3
For next two elements the difference is abs(2-4)=2
For next two elements the difference is abs(4-3)=1
Hence, difference array is 5, 4, 3, 2, 1.

Input : arr[] = {7, 10, 2, 4, 5}
Output : 10 2 7 4 5 
Explanation:
For first two elements the difference is abs(10-2)=8
For next two elements the difference is abs(2-7)=5
For next two elements the difference is abs(7-4)=3
For next two elements the difference is abs(4-5)=1
Hence, difference array is 8, 5, 3, 1.
```

**方法:**
为了解决上面提到的问题，我们必须对数组进行排序，然后按照以下顺序为偶数大小的数组打印元素:

> a[n]，a[1]，a[n-1]，a[2] …..a[(n/2)]，[(n/2)+1]

对于奇数大小的数组，我们必须按照以下顺序打印数组元素:

> a[n]，a[1]，a[n-1]，a[2] …..a[(n/2)+1]

以下是上述方法的实现:

## C++

```
// C++ implementation to Rearrange array
// such that difference of adjacent
// elements is in descending order

#include <bits/stdc++.h>
using namespace std;

// Function to print array in given order
void printArray(int* a, int n)
{
    // Sort the array
    sort(a, a + n);
    int i = 0;
    int j = n - 1;

    // Check elements till the middle index
    while (i <= j) {
        // check if length is odd
        // print the middle index at last
        if (i == j) {
            cout << a[i] << " ";
        }
        // Print the remaining elements
        // in the described order
        else {
            cout << a[j] << " ";
            cout << a[i] << " ";
        }
        i = i + 1;
        j = j - 1;
    }
    cout << endl;
}

// Driver code
int main()
{

    // array declaration
    int arr1[] = { 1, 2, 3, 4, 5, 6 };

    // size of array
    int n1 = sizeof(arr1) / sizeof(arr1[0]);

    printArray(arr1, n1);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Rearrange array
// such that difference of adjacent
// elements is in descending order
import java.util.*;

class GFG {

// Function to print array in given order
static void printArray(int []a, int n)
{

    // Sort the array
    Arrays.sort(a);

    int i = 0;
    int j = n - 1;

    // Check elements till the
    // middle index
    while (i <= j)
    {

        // Check if length is odd print
        // the middle index at last
        if (i == j)
        {
            System.out.print(a[i] + " ");
        }

        // Print the remaining elements
        // in the described order
        else
        {
            System.out.print(a[j] + " ");
            System.out.print(a[i] + " ");
        }
        i = i + 1;
        j = j - 1;
    }
    System.out.println();
}

// Driver code
public static void main (String[] args)
{

    // Array declaration
    int arr1[] = { 1, 2, 3, 4, 5, 6 };

    // Size of array
    int n1 = arr1.length;

    printArray(arr1, n1);
}   
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation to rearrange 
# array such that difference of adjacent
# elements is in descending order

# Function to print array in given order
def printArray(a, n):

    # Sort the array
    a.sort();

    i = 0;
    j = n - 1;

    # Check elements till the middle index
    while (i <= j):

        # Check if length is odd print
        # the middle index at last
        if (i == j):
            print(a[i], end = " ");

        # Print the remaining elements
        # in the described order
        else :
            print(a[j], end = " ");
            print(a[i], end = " ");

        i = i + 1;
        j = j - 1;

    print();

# Driver code
if __name__ == "__main__" :

    # Array declaration
    arr1 = [ 1, 2, 3, 4, 5, 6 ];

    # Size of array
    n1 = len(arr1);

    printArray(arr1, n1);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to rearrange array
// such that difference of adjacent
// elements is in descending order
using System;

class GFG {

// Function to print array in given order
static void printArray(int []a, int n)
{

    // Sort the array
    Array.Sort(a);

    int i = 0;
    int j = n - 1;

    // Check elements till the
    // middle index
    while (i <= j)
    {

        // Check if length is odd print
        // the middle index at last
        if (i == j)
        {
            Console.Write(a[i] + " ");
        }

        // Print the remaining elements
        // in the described order
        else
        {
            Console.Write(a[j] + " ");
            Console.Write(a[i] + " ");
        }
        i = i + 1;
        j = j - 1;
    }
    Console.WriteLine();
}

// Driver code
public static void Main (string[] args)
{

    // Array declaration
    int []arr1 = { 1, 2, 3, 4, 5, 6 };

    // Size of array
    int n1 = arr1.Length;

    printArray(arr1, n1);
}    
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

      // JavaScript implementation to Rearrange array
      // such that difference of adjacent
      // elements is in descending order

      // Function to print array in given order
      function printArray(a, n)
      {
        // Sort the array
        a.sort(function (a, b) {
          return a - b;
        });
        var i = 0;
        var j = n - 1;

        // Check elements till the middle index
        while (i <= j) {
          // check if length is odd
          // print the middle index at last
          if (i == j) {
            document.write(a[i] + "  ");
          }
          // Print the remaining elements
          // in the described order
          else {
            document.write(a[j] + "  ");
            document.write(a[i] + "  ");
          }
          i = i + 1;
          j = j - 1;
        }
        document.write("<br>");
      }

      // Driver code
      // array declaration
      var arr1 = [1, 2, 3, 4, 5, 6];

      // size of array
      var n1 = arr1.length;
      printArray(arr1, n1);

</script>
```

**Output:** 

```
6 1 5 2 4 3
```

**时间复杂度:**O(N * logN)
T3】辅助空间: O(1)
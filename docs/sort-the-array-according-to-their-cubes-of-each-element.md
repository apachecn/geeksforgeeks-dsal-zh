# 根据每个元素的立方体对数组进行排序

> 原文:[https://www . geeksforgeeks . org/根据每个元素的立方体对数组进行排序/](https://www.geeksforgeeks.org/sort-the-array-according-to-their-cubes-of-each-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是根据每个元素的立方体对数组进行排序。

**示例:**

> **输入:** arr[] = { 4，-1，0，-5，6 }
> **输出:** -5 -1 0 4 6
> 
> **输入:** arr[] = { 12，3，0，11 }
> T3】输出: 0 3 11 12

**方法:**想法是使用内置了[排序函数()](https://www.geeksforgeeks.org/sort-c-stl/)的 Comparator 函数，根据数组元素的立方体对数组进行排序。下面是使用的比较器功能:

```
bool comparator_function(int a, int b)
{
    x = pow(a, 3);
    y = pow(b, 3);
    return x < y;
}
```

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Comparator function which returns
// a^3 is less than b^3
bool cmp(int a, int b)
{
    int x = pow(a, 3);
    int y = pow(b, 3);
    return x < y;
}

// Function to sort the cubes of array
bool sortArr(int arr[], int n)
{
    // Sort the array
    sort(arr, arr + n, cmp);

    // Print the array
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 4, -1, 0, -5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    sortArr(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG {

// Function to sort the cubes of array
static void sortArr(int arr[], int n)
{
    Integer[] ar = new Integer[n];

    for (int i = 0; i < n; i++)
        ar[i] = arr[i];

    // Sort the array
    Arrays.sort(ar, new Comparator<Integer>()
    {
        public int compare(Integer a, Integer b)
        {
            int x = (int)Math.pow(a, 3);
            int y = (int)Math.pow(b, 3);
            return (x < y) ? -1 : 1;
        }
    });

    // Print the array
    for (int i = 0; i < n; i++)
    {
        System.out.print(ar[i] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    // Given array
    int arr[] = { 4, -1, 0, -5, 6 };
    int n = arr.length;

    // Function Call
    sortArr(arr, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to sort the cubes of array
def sortArr(arr, n):

    # Make a list of tuples in
    # the form(cube of (num), num)
    arr = [(i * i * i, i) for i in arr];

    # Sort the array according to
    # the their respective cubes
    arr.sort()

    # Print the array
    for i in range(n):
        print(arr[i][1], end = " ");

# Driver Code
if __name__ == "__main__" :

    # Given array
    arr = [ 4, -1, 0, -5, 6 ];
    n = len(arr);

    # Function Call
    sortArr(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class compare : IComparer
{  
    // Call CaseInsensitiveComparer.Compare
    public int Compare(Object x,
                       Object y)
    {
        return (
          new CaseInsensitiveComparer()).Compare(x,y);
    }
}

class GFG{

// Function to sort the cubes of array
static void sortArr(int []arr,
                    int n)
{
    int[] ar = new int[n];

    for (int i = 0; i < n; i++)
        ar[i] = arr[i];

    IComparer cmp = new compare();

    // Sort the array
    Array.Sort(ar, cmp);

    // Print the array
    for (int i = 0; i < n; i++)
    {
        Console.Write(ar[i] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    // Given array
    int []arr = {4, -1, 0, -5, 6};
    int n = arr.Length;

    // Function Call
    sortArr(arr, n);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
//Javascript implementation to check whether
// K times of a element is present in
// the array

// Function to sort the cubes of array
function sortArr(arr, n)
{
    // Sort the array
    arr.sort( function( a , b){
        var x = Math.pow(a,3);
        var y = Math.pow(b,3);
        if(x > y) return 1;
        if(x < y) return -1;
        return 0;
    });

    // Print the array
    for (var i = 0; i < n; i++) {
        document.write(arr[i] + " ");
    }
}

// Driver program to test above
var arr = [ 4, -1, 0, -5, 6 ];
var n = arr.length;
sortArr(arr, n);
// This code is contributed by shivani.
</script>
```

**Output:** 

```
-5 -1 0 4 6
```

**时间复杂度:** *O(N*log N)* ，其中 N 为数组中的元素个数。
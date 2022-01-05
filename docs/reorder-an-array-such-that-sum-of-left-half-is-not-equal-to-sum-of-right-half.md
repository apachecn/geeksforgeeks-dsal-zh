# 重新排列数组，使左半部分的和不等于右半部分的和

> 原文:[https://www . geesforgeks . org/对数组重新排序，这样左半部分的和不等于右半部分的和/](https://www.geeksforgeeks.org/reorder-an-array-such-that-sum-of-left-half-is-not-equal-to-sum-of-right-half/)

给定一个偶数长度的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是检查是否有可能[对数组元素](https://www.geeksforgeeks.org/reorder-a-array-according-to-given-indexes/)重新排序，使得数组左半部分的和不等于右半部分的和。如果可能，用重新排序的顺序打印**“是”**，否则打印**“否”**。
**举例:**

> **输入:** arr[] = {1，2，2，1，3，1}
> **输出:**
> 是
> 1 1 1 2 2 3
> **说明:**
> 左半部分之和= 1 + 2 + 2 = 5
> 右半部分之和= 2 + 2 + 3 = 7
> 两者之和不相等。
> **输入:** arr[] = {1，1}
> **输出:**否
> **说明:**
> 不可能有这样的安排。

**方法:**如果数组的所有元素都相等，那么我们就不能对数组元素重新排序来满足给定的条件。否则在给定数组的排序序列中，数组的左半部分和右半部分的总和将总是不相等的。
以下是上述办法的实施情况:

## C

```
// C program for the above approach
#include <stdio.h>
#include <stdlib.h>

// A comparator function used by qsort
int compare(const void * a, const void * b)
{
    return (*(int*)a - *(int*)b);
}

// Function to print the required
// reordering of array if possible
void printArr(int arr[], int n)
{

    // Sort the array in increasing order
    qsort(arr, n, sizeof(int), compare);

    // If all elements are equal, then
    // it is not possible
    if (arr[0] == arr[n - 1])
    {
        printf("No\n");
    }

    // Else print the sorted array arr[]
    else
    {
        printf("Yes\n");
        for(int i = 0; i < n; i++)
        {
            printf("%d ", arr[i]);
        }
    }
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 2, 2, 1, 3, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    printArr(arr, N);
    return 0;
}

// This code is contributed by equbalzeeshan
```

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the required
// reordering of array if possible
void printArr(int arr[], int n)
{
    // Sort the array in increasing order
    sort(arr, arr + n);

    // If all elements are equal, then
    // it is not possible
    if (arr[0] == arr[n - 1]) {
        cout << "No" << endl;
    }

    // Else print the sorted array arr[]
    else {

        cout << "Yes" << endl;
        for (int i = 0; i < n; i++) {
            cout << arr[i] << " ";
        }
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 2, 1, 3, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    printArr(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the required
// reordering of array if possible
public static void printArr(int[] arr, int n)
{

    // Sort the array in increasing order
    Arrays.sort(arr);

    // If all elements are equal, then
    // it is not possible
    if (arr[0] == arr[n - 1])
    {
        System.out.println("No");
    }

    // Else print the sorted array arr[]
    else
    {
        System.out.println("Yes");
        for(int i = 0; i < n; i++)
        {
            System.out.print(arr[i] + " ");
        }
    }
}

// Driver code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 1, 2, 2, 1, 3, 1 };

    int N = arr.length;

    // Function call
    printArr(arr, N);
}
}

// This code is contributed by equbalzeeshan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the required
# reordering of the array if possible
def printArr(arr, n):

    # Sort the array in increasing
    # order
    arr.sort()

    # If all elements are equal,
    # then it is not possible
    if(arr[0] == arr[n - 1]):
        print("No")

    # Else print the sorted
    # array arr[]
    else:
        print("Yes")
        for i in range(n):
            print(arr[i], end = " ")
        print()

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 1, 2, 2, 1, 3, 1 ]
    N = len(arr)

    # Function Call
    printArr(arr, N)

# This code is contributed by Shivam Singh
```

## C#

```
// C# code for the above approach
using System;

class GFG{

// Function to print the required
// reordering of array if possible
public static void printArr(int[] arr, int n)
{

    // Sort the array in increasing order
    Array.Sort(arr);

    // If all elements are equal, then
    // it is not possible
    if (arr[0] == arr[n - 1])
    {
        Console.Write("No\n");
    }

    // Else print the sorted array arr[]
    else
    {
        Console.Write("Yes\n");
        for(int i = 0; i < n; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }
}

// Driver code
public static void Main()
{

    // Given array
    int[] arr = new int [6]{ 1, 2, 2, 1, 3, 1 };

    int N = arr.Length;

    // Function call
    printArr(arr, N);
}
}

// This code is contributed by equbalzeeshan
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to print the required
    // reordering of array if possible
    function printArr(arr , n)
    {

        // Sort the array in increasing order
        arr.sort();

        // If all elements are equal, then
        // it is not possible
        if (arr[0] == arr[n - 1]) {
            document.write("No<br/>");
        }

        // Else print the sorted array arr
        else {
            document.write("Yes<br/>");
            for (i = 0; i < n; i++) {
                document.write(arr[i] + " ");
            }
        }
    }

    // Driver code

        // Given array
        var arr = [ 1, 2, 2, 1, 3, 1 ];

        var N = arr.length;

        // Function call
        printArr(arr, N);

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
Yes
1 1 1 2 2 3
```

**时间复杂度:** *O(N*log(N))*
# 找到数组中具有最大预变形的元素

> 原文:[https://www . geeksforgeeks . org/find-the-element-having-maximum-premutiples-in-array/](https://www.geeksforgeeks.org/find-the-element-having-maximum-premutiples-in-the-array/)

给定一个数组 **arr[]** ，任务是找到集合中具有最大预倍数的元素。对于任何索引 **i** ，预倍数是 **i** 的倍数，并且出现在数组的第 i <sup>个</sup>索引之前。另外，打印该数组中该元素的最大倍数的计数。
**举例:**

> **输入:** arr[] = {8，1，28，4，2，6，7}
> **输出:**元素= 2，预乘计数= 3
> **说明:**对于数组，arr[] = {8，1，28，4，2，6，7}数字 2 具有最大的
> 预乘数，即{8，28，4}。因此计数为 3。
> **输入:** arr[] = {8，12，5，8，17，5，28，4，3，8}
> **输出:** Element = 4，3，预乘计数= 3
> 对于数组，a[] = {8，12，5，8，17，5，6，15，4，3，8}数字 4 和 3 具有最大的预乘数
> 即{8，8 因此计数为 3。

**方法:**思路是在索引前用另一个数组存储 I 的倍数的计数。可以按照以下步骤计算结果:

1.  遍历数组的每个元素，对于每个有效的 **i** ，**计数**等于有效索引的数量 **j < i** ，这样，索引 **j** 处的元素可以被索引 **i** 处的元素整除。
2.  将元素的计数值存储在 **temp_count** 数组的索引 **i** 处。
3.  找到数组 **temp_count** []中的最大元素，并将其值存储在 **max** 中。
4.  迭代数组 **temp_count** 的每个元素，这样，如果 temp_count 的索引 **i** 处的元素等于 **max** ，则打印原始数组 **arr** 的相应 i <sup>th</sup> 元素。
5.  最后，打印 max 中存储的最大值。

以下是上述方法的实现:

## C++

```
// C++ program to find the element which has maximum
// number of premultiples and also print its count.
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000

// Function to find the elements having
// maximum number of premultiples.
void printMaxMultiple(int arr[], int n)
{

    int i, j, count, max;

    // Initialize of temp_count array with zero
    int temp_count[n] = { 0 };

    for (i = 1; i < n; i++) {
        // Initialize count with zero for
        // every ith element of arr[]
        count = 0;

        // Loop to calculate the count of multiples
        // for every ith element of arr[] before it
        for (j = 0; j < i; j++) {
            // Condition to check whether the element
            // at a[i] divides element at a[j]
            if (arr[j] % arr[i] == 0)
                count = count + 1;
        }
        temp_count[i] = count;
    }

    cout<<"Element = ";
    // To get the maximum value in temp_count[]
    max = *max_element(temp_count, temp_count + n);

    // To print all the elements having maximum
    // number of multiples before them.
    for (i = 0; i < n; i++) {
        if (temp_count[i] == max)
            cout << arr[i] << ", ";
    }
    cout << "Count of Premultiples = ";
    // To print the count of maximum number
    // of multiples
    cout << max << "\n";
}

// Driver function
int main()
{
    int arr[] = { 8, 6, 2, 5, 8, 6, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printMaxMultiple(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the element which has maximum
// number of premultiples and also print its count.
import java.io.*;
import java.util.Arrays;

class GFG{

public static int MAX = 1000;

// Function to find the elements having
// maximum number of premultiples.
public static void printMaxMultiple(int[] arr, int n)
{
    int i, j, count, max;

    // Initialize of temp_count array with zero
    int[] temp_count = new int[n];
    for(i = 0; i < temp_count.length; i++)
    {
        temp_count[i] = 0;
    }

    for(i = 1; i < n; i++)
    {
       // Initialize count with zero for
       // every ith element of arr[]
       count = 0;

       // Loop to calculate the count of multiples
       // for every ith element of arr[] before it
       for(j = 0; j < i; j++)
       {
          // Condition to check whether the element
          // at a[i] divides element at a[j]
          if (arr[j] % arr[i] == 0)
              count = count + 1;
       }
       temp_count[i] = count;
    }
    System.out.print("Element = ");

    // To get the maximum value in temp_count[]
    max = Arrays.stream(temp_count).max().getAsInt();

    // To print all the elements having maximum
    // number of multiples before them.
    for(i = 0; i < n; i++)
    {
       if (temp_count[i] == max)
           System.out.print(arr[i] + ", ");
    }
    System.out.print("Count of Premultiples = ");

    // To print the count of maximum number
    // of multiples
    System.out.println(max);
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 8, 6, 2, 5, 8, 6, 3, 4 };
    int n = arr.length;
    printMaxMultiple(arr, n);
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 program to find the element which has maximum
# number of premultiples and also print count.

MAX = 1000

# Function to find the elements having
# maximum number of premultiples.
def printMaxMultiple(arr, n):

    # Initialize of temp_count array with zero
    temp_count= [0]*n

    for i in range(1, n):

        # Initialize count with zero for
        # every ith element of arr[]
        count = 0

        # Loop to calculate the count of multiples
        # for every ith element of arr[] before it
        for j in range(i):

            # Condition to check whether the element
            # at a[i] divides element at a[j]
            if (arr[j] % arr[i] == 0):
                count = count + 1

        temp_count[i] = count

    print("Element = ",end="")
    # To get the maximum value in temp_count[]
    maxx = max(temp_count)

    # To prall the elements having maximum
    # number of multiples before them.
    for i in range(n):
        if (temp_count[i] == maxx):
            print(arr[i],end=", ",sep="")

    print("Count of Premultiples = ",end="")
    # To print the count of the maximum number
    # of multiples

    print(maxx)

# Driver function

arr = [8, 6, 2, 5, 8, 6, 3, 4 ]
n = len(arr)
printMaxMultiple(arr, n)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to find the element which has maximum
// number of premultiples and also print its count.
using System;
using System.Linq;

class GFG {

    // Function to find the elements having
    // maximum number of premultiples.
    public static void printMaxMultiple(int[] arr, int n)
    {

        int i, j, count, max;

        // Initialize of temp_count array with zero
        int[] temp_count = new int[n];
        for(i = 0; i < temp_count.Length; i++)
            temp_count[i] = 0;

        for (i = 1; i < n; i++) {

            // Initialize count with zero for
            // every ith element of arr[]
            count = 0;

            // Loop to calculate the count of multiples
            // for every ith element of arr[] before it
            for (j = 0; j < i; j++) {

                // Condition to check whether the element
                // at a[i] divides element at a[j]
                if (arr[j] % arr[i] == 0)
                    count = count + 1;
            }
            temp_count[i] = count;
        }

        Console.Write("Element = ");

        // To get the maximum value in temp_count[]
        max = temp_count.Max();;

        // To print all the elements having maximum
        // number of multiples before them.
        for (i = 0; i < n; i++) {
            if (temp_count[i] == max)
                Console.Write(arr[i]+ ", ");
        }
        Console.Write("Count of Premultiples = ");

        // To print the count of maximum
        // number of multiples
        Console.WriteLine(max);
    }

    // Driver function
    public static void Main()
    {
        int[] arr = { 8, 6, 2, 5, 8, 6, 3, 4 };
        int n = arr.Length;
        printMaxMultiple(arr, n);
    }
}

// This code is contributed by Shubhamsingh10
```

## java 描述语言

```
<script>

    // JavaScript program to find
    // the element which has maximum
    // number of premultiples and also print its count.

    // Function to find the elements having
    // maximum number of premultiples.

    function printMaxMultiple(arr,n)
    {

      let i, j, count, max;

      // Initialize of temp_count array with zero
      let temp_count = new Array(n);
      temp_count.fill(0);

      for (i = 1; i < n; i++) {
        // Initialize count with zero for
        // every ith element of arr[]
        count = 0;

        // Loop to calculate the count of multiples
        // for every ith element of arr[] before it
        for (j = 0; j < i; j++) {
          // Condition to check whether the element
          // at a[i] divides element at a[j]
          if (arr[j] % arr[i] == 0)
            count = count + 1;
        }
        temp_count[i] = count;
      }

      document.write("Element = ");
      // To get the maximum value in temp_count[]
      max = Number.MIN_VALUE;
      for (i = 0; i < n; i++)
      {
          max = Math.max(max, temp_count[i]);
      }

      // To print all the elements having maximum
      // number of multiples before them.
      for (i = 0; i < n; i++) {
        if (temp_count[i] == max)
          document.write(arr[i] + ", ");
      }
      document.write("Count of Premultiples = ");
      // To print the count of maximum number
      // of multiples
      document.write(max + "</br>");
    }

    let arr = [ 8, 6, 2, 5, 8, 6, 3, 4 ];
    let n = arr.length;
    printMaxMultiple(arr, n);

</script>
```

**Output:** 

```
Element = 2, 3, 4, Count of Premultiples = 2
```

**时间复杂度:** O(N <sup>2</sup> )
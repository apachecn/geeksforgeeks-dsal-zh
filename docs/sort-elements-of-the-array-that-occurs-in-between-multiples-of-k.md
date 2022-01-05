# 对出现在 K 的倍数之间的数组元素进行排序

> 原文:[https://www . geesforgeks . org/sort-在 k 的倍数之间出现的数组元素/](https://www.geeksforgeeks.org/sort-elements-of-the-array-that-occurs-in-between-multiples-of-k/)

给定一个数组 **arr[]** 和一个整数 **K** 。任务是对位于任意两个倍数的 **K** 之间的元素进行排序。

**示例:**

> **输入:** arr[] = {2，1，13，3，7，8，21，13，12}，K = 2
> **输出:** 2 1 3 7 13 8 13 21 12
> 数组中 2 的倍数为 2，8，12。
> 位于 2 的前两个倍数之间的元素是 1、13、3 和 7。
> 因此，这些元素按照排序顺序是 1、3、7 和 13。
> 同样，排序顺序中 8 到 12 之间的元素将是 13 和 21。
> 
> **输入:** arr[] = {11，10，9，7，4，5，12，22，13，15，17，16}，K = 3
> **输出:** 11 10 9 4 5 7 12 13 22 15 17 16

**方式:**遍历数组，跟踪 **K** 的倍数，从 **K** 的 **2 <sup>nd</sup> 倍数开始，对 **K** 的当前倍数和前一倍数之间的每个元素进行排序。在最后打印更新的数组。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Utility function to print
// the contents of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << (arr[i]) << " ";
}

// Function to sort elements
// in between multiples of k
void sortArr(int arr[], int n, int k)
{

    // To store the index of
    // previous multiple of k
    int prev = -1;
    for (int i = 0; i < n; i++)
    {
        if (arr[i] % k == 0)
        {

            // If it is not the
            // first multiple of k
            if (prev != -1)

                // Sort the elements in between
                // the previous and the current
                // multiple of k
                sort(arr + prev + 1, arr + i);

            // Update previous to be current
            prev = i;
        }
    }

    // Print the updated array
    printArr(arr, n);
}

// Driver code
int main()
{
    int arr[] = {2, 1, 13, 3, 7,
                 8, 21, 13, 12};
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    sortArr(arr, n, k);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;
class GFG {

    // Utility function to print
    // the contents of an array
    static void printArr(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Function to sort elements
    // in between multiples of k
    static void sortArr(int arr[], int n, int k)
    {

        // To store the index of
        // previous multiple of k
        int prev = -1;
        for (int i = 0; i < n; i++) {
            if (arr[i] % k == 0) {

                // If it is not the
                // first multiple of k
                if (prev != -1)

                    // Sort the elements in between
                    // the previous and the current
                    // multiple of k
                    Arrays.sort(arr, prev + 1, i);

                // Update previous to be current
                prev = i;
            }
        }

        // Print the updated array
        printArr(arr, n);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 1, 13, 3, 7, 8, 21, 13, 12 };
        int n = arr.length;
        int k = 2;
        sortArr(arr, n, k);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print
# the contents of an array
def printArr(arr, n) :
    for i in range(n) :
        print(arr[i], end = " ");

# Function to sort elements
# in between multiples of k
def sortArr(arr, n, k) :

    # To store the index of
    # previous multiple of k
    prev = -1;
    for i in range(n) :
        if (arr[i] % k == 0) :

            # If it is not the first
            # multiple of k
            if (prev != -1) :

                # Sort the elements in between
                #the previous and the current
                # multiple of k
                temp = arr[prev + 1:i];
                temp.sort();
                arr = arr[ : prev + 1] + temp + arr[i : ];

            # Update previous to be current
            prev = i;

    # Print the updated array
    printArr(arr, n);

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 1, 13, 3, 7, 8, 21, 13, 12 ];
    n = len(arr);
    k = 2;

    sortArr(arr, n, k);

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System.Collections;
using System;
class GFG {

    // Utility function to print
    // the contents of an array
    static void printArr(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Function to sort elements
    // in between multiples of k
    static void sortArr(int []arr, int n, int k)
    {

        // To store the index of
        // previous multiple of k
        int prev = -1;
        for (int i = 0; i < n; i++) {
            if (arr[i] % k == 0) {

                // If it is not the
                // first multiple of k
                if (prev != -1)

                    // Sort the elements in between
                    // the previous and the current
                    // multiple of k
                    Array.Sort(arr, prev + 1, i-(prev + 1));

                // Update previous to be current
                prev = i;
            }
        }

        // Print the updated array
        printArr(arr, n);
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 2, 1, 13, 3, 7, 8, 21, 13, 12 };
        int n = arr.Length;
        int k = 2;
        sortArr(arr, n, k);
    }
}
//contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Utility function to print
// the contents of an array
function printArr(arr, n)
{
    for (var i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Function to sort elements
// in between multiples of k
function sortArr(arr, n, k)
{

    // To store the index of
    // previous multiple of k
    var prev = -1;
    for (var i = 0; i < n; i++)
    {
        if (arr[i] % k == 0)
        {

            // If it is not the
            // first multiple of k
            if (prev != -1)

                var tmp = arr.slice(prev+1, i).sort((a,b)=> a-b);
                // Sort the elements in between
                // the previous and the current
                // multiple of k
                for(var j=prev+1; j< i; j++)
                {
                    arr[j] = tmp[j-prev-1];
                }
            // Update previous to be current
            prev = i;
        }
    }

    // Print the updated array
    printArr(arr, n);
}

// Driver code
var arr = [2, 1, 13, 3, 7,
             8, 21, 13, 12];
var n = arr.length;
var k = 2;
sortArr(arr, n, k);

</script>
```

**Output:** 

```
2 1 3 7 13 8 13 21 12
```
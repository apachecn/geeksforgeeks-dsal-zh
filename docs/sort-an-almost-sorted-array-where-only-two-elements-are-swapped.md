# 排序一个几乎排序的数组，其中只有两个元素被交换

> 原文:[https://www . geeksforgeeks . org/sort-一个几乎已排序的数组，其中只交换了两个元素/](https://www.geeksforgeeks.org/sort-an-almost-sorted-array-where-only-two-elements-are-swapped/)

给定一个几乎排序的数组，其中只有两个元素被交换，如何有效地排序数组？
**例:**

```
Input:  arr[] = {10, 20, 60, 40, 50, 30}  
// 30 and 60 are swapped
Output: arr[] = {10, 20, 30, 40, 50, 60}

Input:  arr[] = {10, 20, 40, 30, 50, 60}  
// 30 and 40 are swapped
Output: arr[] = {10, 20, 30, 40, 50, 60}

Input:   arr[] = {1, 5, 3}
// 3 and 5 are swapped
Output:  arr[] = {1, 3, 5}
```

预期的时间复杂度是 O(n)，只需要一次交换操作就可以修复阵列。

想法是从最右侧遍历并找到第一个无序元素(比前一个元素小的元素)。找到第一个元素后，通过向左侧遍历数组来找到另一个有序元素。
以下是上述思路的实现。

## C++

```
// C++ program to sort using one swap
#include<iostream>
#include<algorithm>
using namespace std;

// This function sorts an array that can be sorted
// by single swap
void sortByOneSwap(int arr[], int n)
{
    // Traverse the given array from rightmost side
    for (int i = n-1; i > 0; i--)
    {
        // Check if arr[i] is not in order
        if (arr[i] < arr[i-1])
        {
            // Find the other element to be
            // swapped with arr[i]
            int j = i-1;
            while (j>=0 && arr[i] < arr[j])
                j--;

            // Swap the pair
            swap(arr[i], arr[j+1]);
            break;
        }
    }
}

// A utility function to print an array of size n
void printArray(int arr[], int n)
{
    int i;
    for (i=0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

/* Driver program to test insertion sort */
int main()
{
    int arr[] = {10, 30, 20, 40, 50, 60, 70};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << "Given array is \n";
    printArray(arr, n);

    sortByOneSwap(arr, n);

    cout << "Sorted array is \n";
    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to
// sort using one swap
import java.io.*;

class GFG
{
// This function sorts an array
// that can be sorted by single swap
static void sortByOneSwap(int arr[],
                          int n)
{
    // Traverse the given array
    // from rightmost side
    for (int i = n - 1; i > 0; i--)
    {
        // Check if arr[i]
        // is not in order
        if (arr[i] < arr[i - 1])
        {
            // Find the other element
            // to be swapped with arr[i]
            int j = i - 1;
            while (j >= 0 && arr[i] < arr[j])
                j--;

            // Swap the pair
            int temp = arr[i];
            arr[i] = arr[j + 1];
            arr[j + 1] = temp;

            break;
        }
    }
}

// A utility function to
// print an array of size n
static void printArray(int arr[], int n)
{
    int i;
    for (i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
    System.out.println();
}

// Driver Code
public static void main(String[] args)
{
int arr[] = {10, 30, 20,
             40, 50, 60, 70};
int n = arr.length;

System.out.println("Given array is ");
printArray(arr, n);

sortByOneSwap(arr, n);

System.out.println("Sorted array is ");
printArray(arr, n);
}
}

// This code is contributed by anuj_67.
```

## C#

```
// C# program to sort using one swap
using System;

class GFG
{

// This function sorts an array
// that can be sorted by single swap
static void sortByOneSwap(int []arr,
                          int n)
{
    // Traverse the given array
    // from rightmost side
    for (int i = n - 1; i > 0; i--)
    {
        // Check if arr[i] is not in order
        if (arr[i] < arr[i - 1])
        {
            // Find the other element to be
            // swapped with arr[i]
            int j = i - 1;
            while (j >= 0 && arr[i] < arr[j])
                j--;

            // Swap the pair
            int temp = arr[i];
            arr[i] = arr[j + 1];
            arr[j + 1] = temp;

            break;
        }
    }
}

// A utility function to print an
// array of size n
static void printArray(int []arr, int n)
{
    int i;
    for (i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
    Console.WriteLine();
}

// Driver Code
public static void Main()
{
    int []arr = {10, 30, 20,
                 40, 50, 60, 70};
    int n = arr.Length;

    Console.WriteLine("Given array is ");
    printArray(arr, n);

    sortByOneSwap(arr, n);

    Console.WriteLine("Sorted array is ");
    printArray(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to sort using one swap

// This function sorts an array
// that can be sorted by single swap
function sortByOneSwap(&$arr, $n)
{
    // Traverse the given array
    // from rightmost side
    for ($i = $n - 1; $i > 0; $i--)
    {
        // Check if arr[i]
        // is not in order
        if ($arr[$i] < $arr[$i - 1])
        {
            // Find the other element
            // to be swapped with arr[i]
            $j = $i - 1;
            while ($j >= 0 && $arr[$i] < $arr[$j])
                $j--;

            // Swap the pair
            $temp = $arr[$i];
            $arr[$i] = $arr[$j + 1];
            $arr[$j + 1] = $temp;

            break;
        }
    }
}

// A utility function to
// print an array of size n
function printArray(&$arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] . " ";
    echo "\n";
}

// Driver Code
$arr = array(10, 30, 20,
        40, 50, 60, 70);
$n = sizeof($arr);

echo "Given array is " . "\n";
printArray($arr, $n);

sortByOneSwap($arr, $n);

echo "Sorted array is ". "\n";
printArray($arr, $n);

// This code is contributed by Akanksha Rai
```

## java 描述语言

```
<script>

    // Javascript program to sort using one swap

    // This function sorts an array
    // that can be sorted by single swap
    function sortByOneSwap(arr, n)
    {

        // Traverse the given array
        // from rightmost side
        for (let i = n - 1; i > 0; i--)
        {

            // Check if arr[i] is not in order
            if (arr[i] < arr[i - 1])
            {

                // Find the other element to be
                // swapped with arr[i]
                let j = i - 1;
                while (j >= 0 && arr[i] < arr[j])
                    j--;

                // Swap the pair
                let temp = arr[i];
                arr[i] = arr[j + 1];
                arr[j + 1] = temp;

                break;
            }
        }
    }

    // A utility function to print an
    // array of size n
    function printArray(arr, n)
    {
        let i;
        for (i = 0; i < n; i++)
            document.write(arr[i] + " ");
        document.write("</br>");
    }

    let arr = [10, 30, 20, 40, 50, 60, 70];
    let n = arr.length;

    document.write("Given array is " + "</br>");
    printArray(arr, n);

    sortByOneSwap(arr, n);

    document.write("Sorted array is " + "</br>");
    printArray(arr, n);

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
Given array is
10 30 20 40 50 60 70
Sorted array is
10 20 30 40 50 60 70
```

上述程序在 O(n)时间内工作，只交换一个元素。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息
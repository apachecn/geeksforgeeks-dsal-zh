# 商-余数排序

> 原文:[https://www.geeksforgeeks.org/quotient-remainder-sort/](https://www.geeksforgeeks.org/quotient-remainder-sort/)

商-余数排序是一种基于非比较的排序算法。执行商-余数排序的步骤如下所述:

1.  求数组的最小值和最大值。
2.  创建由 0 组成的 ROW*COL 矩阵，其中 ROW = MAX/MIN+1，COL = MIN。
3.  对于输入数组中的每个元素，计算商和余数，并存储在矩阵[商][余数]中
4.  对于矩阵中的每个元素，if 元素！= 0，将元素追加到排序数组

**示例:**

```
Input : 2 5 3 7 4 8   
MAX = 8, MIN = 2, ROW = 4, COL 2
matrix : 2 3  
         4 5  
         0 7  
         8 0
Output : 2 3 4 5 7 8
```

## C++

```
// CPP program to implement Quotient - Remainder
// Sort
#include <algorithm>
#include <iostream>
using namespace std;

void QRsort(int arr[], int size)
{
    // max_element finds maximum element in an array
    int MAX = *max_element(arr, arr + size);

    // min_element finds minimum element in an array
    int MIN = *min_element(arr, arr + size);

    cout << "Maximum Element found is : " << MAX << endl;
    cout << "Minimum Element found is : " << MIN << endl;

    int COL = MIN;
    int ROW = MAX / MIN + 1;

    // Creating a ROW * COL matrix of all zeros
    int matrix[ROW][COL] = { 0 };

    for (int i = 0; i < size; i++) {
        int quotient = arr[i] / MIN;
        int remainder = arr[i] % MIN;
        matrix[quotient][remainder + 1] = arr[i];
    }

    int k = 0;
    for (int i = 0; i < ROW; i++) {
        for (int j = 0; j < COL; j++) {
            if (matrix[i][j] != 0) {
                arr[k++] = matrix[i][j];
            }
        }
    }
}

void printArray(int arr[], int size)
{
    for (int i = 0; i < size; i++)
        cout << arr[i] << " ";
    cout << endl;
}

int main()
{
    int arr[] = { 5, 3, 7, 4, 8, 2, 6 };
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << "Initial Array : " << endl;
    printArray(arr, size);

    QRsort(arr, size);

    cout << "Array after sorting : " << endl;
    printArray(arr, size);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// Quotient - Remainder Sort
import java.util.*;

class GFG
{
static void QRsort(int arr[], int size)
{
    // max_element finds maximum element in an array
    int MAX = Arrays.stream(arr).max().getAsInt();

    // min_element finds minimum element in an array
    int MIN = Arrays.stream(arr).min().getAsInt();

    System.out.println("Maximum Element found is : " + MAX);
    System.out.println("Minimum Element found is : " + MIN);

    int COL = MIN;
    int ROW = MAX / MIN + 1;

    // Creating a ROW * COL matrix of all zeros
    int[][] matrix = new int[ROW][COL];

    for (int i = 0; i < size; i++)
    {
        int quotient = arr[i] / MIN;
        int remainder = arr[i] % MIN;
        matrix[quotient][remainder] = arr[i];
    }

    int k = 0;
    for (int i = 0; i < ROW; i++)
    {
        for (int j = 0; j < COL; j++)
        {
            if (matrix[i][j] != 0)
            {
                arr[k++] = matrix[i][j];
            }
        }
    }
}

static void printArray(int arr[], int size)
{
    for (int i = 0; i < size; i++)
    {
        System.out.print(arr[i] + " ");
    }
    System.out.println();
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {5, 3, 7, 4, 8, 2, 6};
    int size = arr.length;
    System.out.println("Initial Array : ");
    printArray(arr, size);

    QRsort(arr, size);

    System.out.println("Array after sorting : ");
    printArray(arr, size);
}
}

// This code is contributed by Princi Singh
```

## C#

```
// C# program to implement
// Quotient - Remainder Sort
using System;
using System.Linq;

class GFG
{
static void QRsort(int []arr, int size)
{
    // max_element finds maximum element in an array
    int MAX = arr.Max();

    // min_element finds minimum element in an array
    int MIN = arr.Min();

    Console.WriteLine("Maximum Element found is : " + MAX);
    Console.WriteLine("Minimum Element found is : " + MIN);

    int COL = MIN;
    int ROW = MAX / MIN + 1;

    // Creating a ROW * COL matrix of all zeros
    int[,] matrix = new int[ROW, COL];

    for (int i = 0; i < size; i++)
    {
        int quotient = arr[i] / MIN;
        int remainder = arr[i] % MIN;
        matrix[quotient, remainder] = arr[i];
    }

    int k = 0;
    for (int i = 0; i < ROW; i++)
    {
        for (int j = 0; j < COL; j++)
        {
            if (matrix[i, j] != 0)
            {
                arr[k++] = matrix[i, j];
            }
        }
    }
}

static void printArray(int []arr, int size)
{
    for (int i = 0; i < size; i++)
    {
        Console.Write(arr[i] + " ");
    }
    Console.WriteLine();
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {5, 3, 7, 4, 8, 2, 6};
    int size = arr.Length;
    Console.WriteLine("Initial Array : ");
    printArray(arr, size);

    QRsort(arr, size);

    Console.WriteLine("Array after sorting : ");
    printArray(arr, size);
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
Initial Array : 
5 3 7 4 8 2 6 
Maximum Element found is : 8
Minimum Element found is : 2
Array after sorting : 
2 3 4 5 6 7 8
```

**参考文献**T2【Abul Hasnat，Tanima Bhattacharyya，Atanu Dey，Santanu Halder 和 Debotosh Bhattachajee，2017。一种新的利用商和余数的排序算法。应用 Sci，12(特刊 7): 8016-8020，2017，ISSN : 1816-949X
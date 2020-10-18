# 数组上的恒定时间范围添加操作

> 原文： [https://www.geeksforgeeks.org/constant-time-range-add-operation-array/](https://www.geeksforgeeks.org/constant-time-range-add-operation-array/)

给定大小为`N`的数组，并使用全零初始化。 我们提供了许多范围添加查询，这些查询应应用于此数组。 我们需要打印最终更新的数组作为结果。

**示例**：

```
N = 6
Arr = [0, 0, 0, 0, 0, 0]
rangeUpdate1 [0, 2], add 100
Arr = [100, 100, 100, 0, 0, 0]
rangeUpdate1 [1, 5], add 100
Arr = [100, 200, 200, 100, 100, 100]
rangeUpdate1 [2, 3], add 100
Arr = [100, 200, 300, 200, 100, 100]
Which is the final updated array.

```



可以使用[段树](https://www.geeksforgeeks.org/lazy-propagation-in-segment-tree/)，并在每个查询的`O(log n)`时间中使用延迟更新来解决此问题，但是由于没有给出更新操作，因此我们可以在这里做得更好。 我们可以使用此逻辑在恒定时间内处理每个查询，当在范围`[a, b]`中给出添加`V`的查询时，如果需要，我们现在将`V`添加到`arr[a]`，将`–V`添加到`arr[b + 1]`。为了获得数组的实际值，我们将上面的数组转换为前缀和数组。 请参阅以下示例以了解，

```
Arr = [0, 0, 0, 0, 0, 0]
rangeUpdate1 [0, 2], add 100
Arr = [100, 0, 0, -100, 0, 0]
rangeUpdate1 [1, 5], add 100
Arr = [100, 100, 0, -100, 0, 0, -100]
rangeUpdate1 [2, 3], add 100
Arr = [100, 100, 100, -100, -100, 0, -100]    
Now we will convert above operation array to prefix sum array as shown below,
Arr = [100, 200, 300, 200, 100, 100]
Which is the final updated array.

```

因此，实际上，当我们向数组的特定索引添加值`V`时，它表示将`V`添加至该索引的所有元素，这就是为什么我们在`range`之后添加`–V`以在其`add`查询范围之后删除其影响。

请在下面的代码中注意，如果范围跨度到最后一个索引，则`-V`的加法被省略，因为它在数组的内存限制内。

## C++ 

```cpp

//  C++ program to get updated array after many array range 
// add operation 
#include <bits/stdc++.h> 
using namespace std; 

//  Utility method to add value val, to range [lo, hi] 
void add(int arr[], int N, int lo, int hi, int val) 
{ 
    arr[lo] += val; 
    if (hi != N - 1) 
       arr[hi + 1] -= val; 
} 

//  Utility method to get actual array from operation array 
void updateArray(int arr[], int N) 
{ 
    //  convert array into prefix sum array 
    for (int i = 1; i < N; i++) 
        arr[i] += arr[i - 1]; 
} 

//  method to print final updated array 
void printArr(int arr[], int N) 
{ 
    updateArray(arr, N); 
    for (int i = 0; i < N; i++) 
        cout << arr[i] << " "; 
    cout << endl; 
} 

//  Driver code to test above methods 
int main() 
{ 
    int N = 6; 

    int arr[N] = {0}; 

    //  Range add Queries 
    add(arr, N, 0, 2, 100); 
    add(arr, N, 1, 5, 100); 
    add(arr, N, 2, 3, 100); 

    printArr(arr, N); 
    return 0; 
} 

```

## Java

```
// Java program to get updated array after
// many array range add operation
import java.io.*;
 
class GFG {
    // Utility method to add value val,
    // to range [lo, hi]
    static void add(int arr[], int N, int lo, int hi,
                    int val)
    {
        arr[lo] += val;
        if (hi != N - 1)
            arr[hi + 1] -= val;
    }
 
    // Utility method to get actual array from
    // operation array
    static void updateArray(int arr[], int N)
    {
        // convert array into prefix sum array
        for (int i = 1; i < N; i++)
            arr[i] += arr[i - 1];
    }
 
    // method to print final updated array
    static void printArr(int arr[], int N)
    {
        updateArray(arr, N);
        for (int i = 0; i < N; i++)
            System.out.print("" + arr[i] + " ");
        System.out.print("\n");
    }
 
    // Driver code
    public static void main(String[] args)
    {
        int N = 6;
 
        int arr[] = new int[N];
 
        // Range add Queries
        add(arr, N, 0, 2, 100);
        add(arr, N, 1, 5, 100);
        add(arr, N, 2, 3, 100);
 
        printArr(arr, N);
    }
}
 
// This code is contributed by Prakriti Gupta
```

## Python3

```
# Python3 program to get updated array
# after many array range add operation
 
# Utility method to add value
# val, to range [lo, hi]
 
 
def add(arr, N, lo, hi, val):
 
    arr[lo] += val
    if (hi != N - 1):
        arr[hi + 1] -= val
 
# Utility method to get actual
# array from operation array
 
 
def updateArray(arr, N):
 
    # convert array into prefix sum array
    for i in range(1, N):
        arr[i] += arr[i - 1]
 
# method to print final updated array
 
 
def printArr(arr, N):
 
    updateArray(arr, N)
    for i in range(N):
        print(arr[i], end=" ")
    print()
 
 
# Driver code
N = 6
arr = [0 for i in range(N)]
 
# Range add Queries
add(arr, N, 0, 2, 100)
add(arr, N, 1, 5, 100)
add(arr, N, 2, 3, 100)
 
printArr(arr, N)
 
# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to get updated array after
// many array range add operation
using System;
 
class GFG {
 
    // Utility method to add value val,
    // to range [lo, hi]
    static void add(int[] arr, int N, int lo, int hi,
                    int val)
    {
        arr[lo] += val;
        if (hi != N - 1)
            arr[hi + 1] -= val;
    }
 
    // Utility method to get actual
    // array from operation array
    static void updateArray(int[] arr, int N)
    {
        // convert array into
        // prefix sum array
        for (int i = 1; i < N; i++)
            arr[i] += arr[i - 1];
    }
 
    // method to print final updated array
    static void printArr(int[] arr, int N)
    {
        updateArray(arr, N);
        for (int i = 0; i < N; i++)
            Console.Write("" + arr[i] + " ");
        Console.Write("\n");
    }
 
    // Driver code
    public static void Main()
    {
        int N = 6;
 
        int[] arr = new int[N];
 
        // Range add Queries
        add(arr, N, 0, 2, 100);
        add(arr, N, 1, 5, 100);
        add(arr, N, 2, 3, 100);
 
        printArr(arr, N);
    }
}
 
// This code is contributed by Nitin Mittal.
```

## PHP

```
<?php 
// PHP program to get updated array after 
// many array range add operation
 
// Utility method to add value val, 
// to range [lo, hi]
function add(&$arr, $N, $lo, $hi, $val)
{
    $arr[$lo] += $val;
    if ($hi != $N - 1)
    $arr[$hi + 1] -= $val;
}
 
// Utility method to get actual array
// from operation array
function updateArray(&$arr, $N)
{
    // convert array into prefix sum array
    for ($i = 1; $i < $N; $i++)
        $arr[$i] += $arr[$i - 1];
}
 
// method to print final updated array
function printArr(&$arr, $N)
{
    updateArray($arr, $N);
    for ($i = 0; $i < $N; $i++)
        echo $arr[$i] . " ";
    echo "\n";
}
 
// Driver Code
$N = 6;
$arr = array_fill(0, $N, NULL);
 
// Range add Queries
add($arr, $N, 0, 2, 100);
add($arr, $N, 1, 5, 100);
add($arr, $N, 2, 3, 100);
 
printArr($arr, $N);
 
// This code is contributed by ita_c
?>
```

输出：

```
100 200 300 200 100 100 
```


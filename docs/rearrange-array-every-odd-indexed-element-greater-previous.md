# 重新排列一个数组，使得每个奇数索引元素都大于它之前的元素

> 原文:[https://www . geesforgeks . org/rearray-array-隔奇-indexed-element-greater-previous/](https://www.geeksforgeeks.org/rearrange-array-every-odd-indexed-element-greater-previous/)

给定一个未排序的数组，重新排列数组，使奇数索引处的数字大于前一个偶数索引处的数字。可能有多个输出，我们需要打印其中一个。

**注意:**索引基于数组，所以总是从 0 开始。

**示例:**

```
Input  : arr[] = {5, 2, 3, 4}
Output : arr[] = {2, 5, 3, 4}

Input  : arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9}
Output : arr[] = {1, 3, 2, 5, 4, 7, 6, 9, 8} 
```

如果给定的数组具有偶数长度，那么它可以在一次运行中完成。对于每对邻居，将最大值放在奇数位置，最小值放在偶数位置。所以我们从一开始就开始一个循环，每两个元素进行比较。假设
6，5，4，3，2，1 会给我们 5，6，3，4，1，2
如果数组有一个奇数长度，比如 6，5，4，3，2，1，100，那么它稍微有点棘手，我们需要再次运行第二个向后循环，但是从最后一个元素开始。所以，第一个周期后的 6，5，4，3，2，1，100 将是 5，6，3，4，1，2，100，第二个周期后的 5，6，3，4，1，100，2

## C++

```
// C++ program to rearrange array such that
// odd indexed elements are greater.
#include<bits/stdc++.h>
using namespace std;

void rearrange(int arr[], int n)
{
    // Common code for odd and even lengths
    for (int i=0; i<n-1; i=i+2)
    {
        if (arr[i] > arr[i+1])
            swap(arr[i], arr[i+1]);
    }

    // If length is odd
    if (n & 1)
    {
        for (int i=n-1; i>0; i=i-2)
            if (arr[i] > arr[i-1])
                swap(arr[i], arr[i-1]);
    }
}

/* Utility that prints out an array on a line */
void printArray(int arr[], int size)
{
    for (int i=0; i < size; i++)
        printf("%d ", arr[i]);

    printf("\n");
}

/* Driver function to test above functions */
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Before rearranging\n";
    printArray(arr, n);
    rearrange(arr, n);
    cout << "After rearranging\n";
    printArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange array such that
// odd indexed elements are greater.

import java.util.Arrays;

class GFG
{
    // Utility function to Swap two variables
    public static void swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // method to rearrange array such that
    // odd indexed elements are greater.
    public static void Rearrange(int[] arr, int n)
    {
        // Common code for odd and even lengths
        for (int i = 0; i < n - 1; i = i + 2) {
            if (arr[i] > arr[i + 1])
                swap(arr, i, i + 1);
        }

        // If length is odd
        if ((n & 1) > 0) {
            for (int i = n - 1; i > 0; i = i - 2)
                if (arr[i] > arr[i - 1])
                    swap(arr, i, i - 1);
        }
    }

    // Driver Method
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

        System.out.println("Before rearranging");
        System.out.println(Arrays.toString(arr));

        Rearrange(arr, arr.length);       

        System.out.println("After rearranging");
        System.out.println(Arrays.toString(arr));
    }
}
/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python 3 program to rearrange array such
# that odd indexed elements are greater.
def rearrange(arr, n):

    # Common code for odd and even lengths
    for i in range(0, n - 1, 2):
        if (arr[i] > arr[i + 1]):
            temp = arr[i]
            arr[i] = arr[i + 1]
            arr[i + 1] = temp

    # If length is odd
    if (n & 1):
        i = n - 1
        while(i > 0):
            if (arr[i] > arr[i - 1]):
                temp = arr[i]
                arr[i] = arr[i - 1]
                arr[i - 1] = temp
            i -= 2

# Utility that prints out an
# array on a line
def printArray(arr, size):
    for i in range(0, size, 1):
        print(arr[i], end = " ")
    print("\n")

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
    n = len(arr)
    print("Before rearranging")

    printArray(arr, n)
    rearrange(arr, n)
    print("After rearranging")

    printArray(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to rearrange
// array such that odd
// indexed elements are
// greater.
using System;

class GFG
{

// Utility function to
// Swap two variables
public static void swap(int[] arr,
                        int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

// method to rearrange
// array such that odd
// indexed elements are
// greater.
public static void Rearrange(int[] arr,
                            int n)
{
    // Common code for odd
    // and even lengths
    for (int i = 0; i < n - 1; i = i + 2)
    {
        if (arr[i] > arr[i + 1])
            swap(arr, i, i + 1);
    }

    // If length is odd
    if ((n & 1) > 0)
    {
        for (int i = n - 1;
                 i > 0; i = i - 2)
            if (arr[i] > arr[i - 1])
                swap(arr, i, i - 1);
    }
}

// Driver Code
static void Main()
{
    int[] arr = {1, 2, 3, 4,
                 5, 6, 7, 8, 9};

    Console.WriteLine("Before rearranging");
    for(int i = 0; i < arr.Length; i++)
        Console.Write(arr[i] + " ");

    Rearrange(arr, arr.Length);    

    Console.WriteLine("\nAfter rearranging");
    for(int i = 0; i < arr.Length; i++)
        Console.Write(arr[i] + " ");
}
}

// This code is contributed
// by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to rearrange array such that
// odd indexed elements are greater.

function rearrange(&$arr, $n)
{
    // Common code for odd and even lengths
    for ($i = 0; $i < $n - 1; $i = $i + 2)
    {
        if ($arr[$i] > $arr[$i + 1])
        {
            $temp = $arr[$i];
            $arr[$i] = $arr[$i + 1];
            $arr[$i + 1] = $temp;
        }
    }

    // If length is odd
    if ($n & 1)
    {
        for ($i = $n - 1; $i > 0; $i = $i - 2)
            if ($arr[$i] > $arr[$i - 1])
            {
                $temp = $arr[$i];
                $arr[$i] = $arr[$i - 1];
                $arr[$i - 1] = $temp;
            }
    }
}

// Utility that prints out an array on a line
function printArray(&$arr, $size)
{
    for ($i = 0; $i < $size; $i++)
        echo $arr[$i] . " ";

    echo "\n";
}

// Driver Code
$arr = array(1, 2, 3, 4, 5, 6, 7, 8, 9);
$n = sizeof($arr);
echo "Before rearranging\n";
printArray($arr, $n);
rearrange($arr, $n);

echo "After rearranging\n";
printArray($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to rearrange array such that
// odd indexed elements are greater.

    // Utility function to Swap two variables
    function swap(arr,i,j)
    {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // method to rearrange array such that
    // odd indexed elements are greater.
    function Rearrange(arr,n)
    {
        // Common code for odd and even lengths
        for (let i = 0; i < n - 1; i = i + 2) {
            if (arr[i] > arr[i + 1])
                swap(arr, i, i + 1);
        }

        // If length is odd
        if ((n & 1) > 0) {
            for (let i = n - 1; i > 0; i = i - 2)
                if (arr[i] > arr[i - 1])
                    swap(arr, i, i - 1);
        }
    }

    // Driver Method
    let arr=[ 1, 2, 3, 4, 5, 6, 7, 8, 9 ];
    document.write("Before rearranging<br>");
    for(let i=0;i<arr.length;i++)
    {
        document.write(arr[i]+" ");
    }

    document.write("<br>")
    Rearrange(arr, arr.length); 
    document.write("After rearranging<br>");
    for(let i=0;i<arr.length;i++)
    {
        document.write(arr[i]+" ");
    }

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Before rearranging
1 2 3 4 5 6 7 8 9 
After rearranging
1 3 2 5 4 7 6 9 8 
```

***时间复杂度:** O(n)*

***辅助空间:**O(1)*T4】
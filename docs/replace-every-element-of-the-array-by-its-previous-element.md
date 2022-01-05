# 用数组的前一个元素

替换数组的每个元素

> 原文:[https://www . geeksforgeeks . org/按前一个元素替换数组中的每个元素/](https://www.geeksforgeeks.org/replace-every-element-of-the-array-by-its-previous-element/)

给定一个数组 **arr** ，任务是用出现在它前面的元素替换数组的每个元素，并用 **-1** 替换第一个元素。
**例:**

> **输入:** arr[] = {5，1，3，2，4}
> **输出:** -1 5 1 3 2
> **输入:** arr[] = {6，8，3 2，12，14，10，25 }
> **输出:** -1 6 8 32 12 14 10

**方式:**从**n–1**到 **1** 遍历数组，更新 **arr[i] = arr[i-1]** 。最后设置 **a[0] = -1** 并打印更新后数组的内容。
以下是上述方法的实施:

## C++

```
// C++ program to replace every element of the array
// with the element that appears before it
#include <bits/stdc++.h>
using namespace std;

// Function to print the array after replacing every element
// of the array with the element that appears before it
void updateArray(int arr[], int n)
{
    // Update array
    for (int i = n - 1; i > 0; i--)
        arr[i] = arr[i - 1];

    // Change the first element to -1
    arr[0] = -1;

    // Print the updated array
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver program
int main()
{
    int arr[] = { 5, 1, 3, 2, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    updateArray(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace every element
// of the array with the element that
// appears before it
class GFG
{

// Function to print the array after
// replacing every element of the
// array with the element that appears
// before it
static void updateArray(int arr[], int n)
{
    // Update array
    for (int i = n - 1; i > 0; i--)
        arr[i] = arr[i - 1];

    // Change the first element to -1
    arr[0] = -1;

    // Print the updated array
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Driver Code
public static void main(String []args)
{
    int arr[] = { 5, 1, 3, 2, 4 } ;
    int N = arr.length ;
    updateArray(arr, N);
}
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python 3 program to replace every element
# of the array with the element that appears
# before it

# Function to print the array after replacing
# every element of the array with the element
# that appears before it
def updateArray(arr, n):

    # Update array
    i = n - 1
    while(i > 0):
        arr[i] = arr[i - 1]
        i -= 1

    # Change the first element to -1
    arr[0] = -1

    # Print the updated array
    for i in range(0, n, 1):
        print(arr[i], end = " ")

# Driver Code
if __name__ == '__main__':
    arr = [5, 1, 3, 2, 4]
    N = len(arr)
    updateArray(arr, N)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to replace every element
// of the array with the element that
// appears before it
using System;

class GFG
{

// Function to print the array after
// replacing every element of the
// array with the element that appears
// before it
static void updateArray(int[] arr, int n)
{
    // Update array
    for (int i = n - 1; i > 0; i--)
        arr[i] = arr[i - 1];

    // Change the first element to -1
    arr[0] = -1;

    // Print the updated array
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Driver Code
public static void Main()
{
    int[] arr = { 5, 1, 3, 2, 4 } ;
    int N = arr.Length ;
    updateArray(arr, N);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to replace every element
// of the array with the element that
// appears before it

// Function to print the array after
// replacing every element of the array
// with the element that appears before it
function updateArray($arr, $n)
{
    // Update array
    for ($i = $n - 1; $i > 0; $i--)
        $arr[$i] = $arr[$i - 1];

    // Change the first element to -1
    $arr[0] = -1;

    // Print the updated array
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] ," ";
}

// Driver Code
$arr = array(5, 1, 3, 2, 4 );
$N = sizeof($arr);
updateArray($arr, $N);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>
// Java script program to replace every element
// of the array with the element that
// appears before it

// Function to print the array after
// replacing every element of the
// array with the element that appears
// before it
function updateArray(arr,n)
{
    // Update array
    for (let i = n - 1; i > 0; i--)
        arr[i] = arr[i - 1];

    // Change the first element to -1
    arr[0] = -1;

    // Print the updated array
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver Code

    let arr =[ 5, 1, 3, 2, 4 ];
    let N = arr.length ;
    updateArray(arr, N);

// This code is contributed by sravan kumar G
</script>
```

**Output:** 

```
-1 5 1 3 2
```

**时间复杂度:** O(n)
***辅助空间** : O(1)*
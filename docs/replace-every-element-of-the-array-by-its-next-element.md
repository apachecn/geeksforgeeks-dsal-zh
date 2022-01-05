# 用数组的下一个元素替换数组的每个元素

> 原文:[https://www . geeksforgeeks . org/按下一个元素替换数组中的每个元素/](https://www.geeksforgeeks.org/replace-every-element-of-the-array-by-its-next-element/)

给定一个数组 **arr** ，任务是用出现在它后面的元素替换数组的每个元素，并用 **-1** 替换最后一个元素。
**例:**

> **输入:** arr[] = {5，1，3，2，4}
> **输出:** 1 3 2 4 -1
> **输入:** arr[] = {6，8，3 2，12，14，10，25 }
> **输出:** 8 32 12 14 10 25 -1

**途径:**从 **0** 遍历数组到 **n-2** 并更新 **arr[i] = arr[i+1]** 。最后设置 **a[n-1] = -1** 并打印更新后数组的内容。
以下是上述方法的实施:

## C++

```
// C++ program to replace every element of the array
// with the element that appears after it
#include <bits/stdc++.h>
using namespace std;

// Function to print the array after replacing every element
// of the array with the element that appears after it
void updateArray(int arr[], int n)
{
    // Update array
    for (int i = 0; i <= n - 2; i++)
        arr[i] = arr[i + 1];

    // Change the last element to -1
    arr[n - 1] = -1;

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
// appears after it
class GFG
{

// Function to print the array after
// replacing every element of the array
// with the element that appears after it
static void updateArray(int arr[], int n)
{
    // Update array
    for (int i = 0; i <= n - 2; i++)
        arr[i] = arr[i + 1];

    // Change the last element to -1
    arr[n - 1] = -1;

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
# Python3 program to replace every
# element of the array with the
# element that appears after it

# Function to print the array after
# replacing every element of the
# array with the element that appears
# after it
def updateArray(arr, n):

    # Update array
    for i in range (n - 1):
        arr[i] = arr[i + 1]

    # Change the last element to -1
    arr[n - 1] = -1

    # Print the updated array
    for i in range( n):
        print (arr[i], end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [ 5, 1, 3, 2, 4 ]
    N = len(arr)
    updateArray(arr, N)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to replace every element
// of the array with the element that
// appears after it
using System;

class GFG
{

// Function to print the array after
// replacing every element of the array
// with the element that appears after it
static void updateArray(int[] arr, int n)
{
    // Update array
    for (int i = 0; i <= n - 2; i++)
        arr[i] = arr[i + 1];

    // Change the last element to -1
    arr[n - 1] = -1;

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
// appears after it

// Function to print the array after
// replacing every element of the
// array with the element that appears
// after it
function updateArray(&$arr, $n)
{
    // Update array
    for ($i = 0; $i <= $n - 2; $i++)
        $arr[$i] = $arr[$i + 1];

    // Change the last element to -1
    $arr[$n - 1] = -1;

    // Print the updated array
    for ($i = 0; $i < $n; $i++)
    {
        echo ($arr[$i]);
        echo (" ");
    }
}

// Driver Code
$arr = array(5, 1, 3, 2, 4 );
$N = sizeof($arr);
updateArray($arr, $N);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to replace every element of the array
// with the element that appears after it

// Function to print the array after replacing every element
// of the array with the element that appears after it
function updateArray(arr, n)
{
    // Update array
    for (let i = 0; i <= n - 2; i++)
        arr[i] = arr[i + 1];

    // Change the last element to -1
    arr[n - 1] = -1;

    // Print the updated array
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver program

    let arr = [ 5, 1, 3, 2, 4 ];
    let N = arr.length;
    updateArray(arr, N);

//This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
1 3 2 4 -1
```

**时间复杂度:** O(n)
***辅助空间** : O(1)*
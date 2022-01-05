# 以摆式排列方式打印阵列的程序

> 原文:[https://www . geesforgeks . org/program-print-array-摆锤-arrangement/](https://www.geeksforgeeks.org/program-print-array-pendulum-arrangement/)

编写一个程序，输入一个数组中的整数列表，并以类似钟摆来回移动的方式排列它们。

*   整数列表中的最小元素必须位于数组的中心位置。
*   最小数旁边的升序数字向右移动，下一个更高的数字向左移动，它继续移动。
*   当达到更高的数字时，一个人以类似钟摆的往复方式走到一边。

**示例:**

```
Input : 1   3   2   5   4
Output :5   3   1   2   4
Explanation: 
The minimum element is 1, so it is moved to the middle.
The next higher element 2  is moved to the right of the 
middle element while the next higher element 3 is 
moved to the left of the middle element and 
this process is continued.

Input : 11   12   31   14   5
Output :31   12   5   11   14
```

想法是先对数组进行排序。一旦数组被排序，使用一个辅助数组来逐个存储元素。

## C++

```
// C++ program for pendulum arrangement of numbers
#include <bits/stdc++.h>
using namespace std;

// Prints pendulum arrangement of arr[]
void pendulumArrangement(int arr[], int n)
{
    // sorting the elements
    sort(arr, arr+n);

    // Auxiliary array to store output
    int op[n];

    // calculating the middle index
    int mid = (n-1)/2;

    // storing the minimum element in the middle
    // i is index for output array and j is for
    // input array.
    int j = 1, i = 1;
    op[mid] = arr[0];
    for (i = 1; i <= mid; i++)
    {
        op[mid+i] = arr[j++];
        op[mid-i] = arr[j++];
    }

    // adjustment for when no. of elements is even
    if (n%2 == 0)
        op[mid+i] = arr[j];

    // Printing the pendulum arrangement
    cout << "Pendulum arrangement:" << endl;
    for (i = 0 ; i < n; i++)
        cout << op[i] << " ";

    cout << endl;
}

// Driver function
int main()
{
    //input Array
    int arr[] = {14, 6, 19, 21, 12};

    // calculating the length of array A
    int n = sizeof(arr)/sizeof(arr[0]);

    // calling pendulum function
    pendulumArrangement(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for pendulum arrangement of numbers

import java.util.Arrays;

class Test
{
    // Prints pendulum arrangement of arr[]
    static void pendulumArrangement(int arr[], int n)
    {
        // sorting the elements
        Arrays.sort(arr);

        // Auxiliary array to store output
        int op[] = new int[n];

        // calculating the middle index
        int mid = (n-1)/2;

        // storing the minimum element in the middle
        // i is index for output array and j is for
        // input array.
        int j = 1, i = 1;
        op[mid] = arr[0];
        for (i = 1; i <= mid; i++)
        {
            op[mid+i] = arr[j++];
            op[mid-i] = arr[j++];
        }

        // adjustment for when no. of elements is even
        if (n%2 == 0)
            op[mid+i] = arr[j];

        // Printing the pendulum arrangement
        System.out.println("Pendulum arrangement:");
        for (i = 0 ; i < n; i++)
            System.out.print(op[i] + " ");

        System.out.println();
    }

    // Driver method
    public static void main(String[] args)
    {
        //input Array
        int arr[] = {14, 6, 19, 21, 12};

        // calling pendulum function
        pendulumArrangement(arr, arr.length);
    }
}
```

## 蟒蛇 3

```
# Python 3 program for pendulum
# arrangement of numbers

# Prints pendulam arrangement of arr[]
def pendulumArrangement(arr, n):

    # sorting the elements
    arr.sort()

    # Auxiliary array to store output
    op = [0] * n

    # calculating the middle index
    mid = int((n-1)/2)

    # storing the minimum
        # element in the middle
    # i is index for output
        # array and j is for
    # input array.
    j = 1
    i = 1
    op[mid] = arr[0]
    for i in range(1,mid+1):

        op[mid+i] = arr[j]
        j+=1
        op[mid-i] = arr[j]
        j+=1

    # adjustment for when no.
        # of elements is even
    if (int(n%2) == 0):
        op[mid+i] = arr[j]

    # Printing the pendulum arrangement
    print("Pendulum arrangement:")
    for i in range(0,n):
        print(op[i],end=" ")

# Driver function
# input Array
arr = [14, 6, 19, 21, 12]

# calculating the length of array A
n = len(arr)

# calling pendulum function
pendulumArrangement(arr, n)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program for pendulum
// arrangement of numbers
using System;

class Test {

    // Prints pendulum arrangement of arr[]
    static void pendulumArrangement(int []arr,
                                    int n)
    {

        // sorting the elements
        Array.Sort(arr);

        // Auxiliary array to store output
        int []op = new int[n];

        // calculating the middle index
        int mid = (n - 1) / 2;

        // storing the minimum element in
        // the middle i is index for output
        // array and j is for input array.
        int j = 1, i = 1;
        op[mid] = arr[0];
        for (i = 1; i <= mid; i++)
        {
            op[mid + i] = arr[j++];
            op[mid - i] = arr[j++];
        }

        // adjustment for when no.
        // of elements is even
        if (n % 2 == 0)
            op[mid + i] = arr[j];

        // Printing the pendulum arrangement
        Console.Write("Pendulum arrangement:");
        for (i = 0 ; i < n; i++)
            Console.Write(op[i] + " ");

        Console.WriteLine();
    }

    // Driver code
    public static void Main()
    {

        //input Array
        int []arr = {14, 6, 19, 21, 12};

        // calling pendulum function
        pendulumArrangement(arr, arr.Length);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for pendulum
// arrangement of numbers

// Prints pendulam arrangement of arr[]
function pendulumArrangement($arr, $n)
{

    // sorting the elements
    sort($arr, $n);
    sort($arr);

    // Auxiliary array to
    // store output
    $op[$n] = NULL;

    // calculating the
    // middle index
    $mid = floor(($n - 1) / 2);

    // storing the minimum
    // element in the middle
    // i is index for output
    // array and j is for
    // input array.
    $j = 1;
    $i = 1;
    $op[$mid] = $arr[0];
    for ($i = 1; $i <= $mid; $i++)
    {
        $op[$mid + $i] = $arr[$j++];
        $op[$mid - $i] = $arr[$j++];
    }

    // adjustment for when no.
    // of elements is even
    if ($n % 2 == 0)
        $op[$mid + $i] = $arr[$j];

    // Printing the pendulum
    // arrangement
    echo "Pendulum arrangement:" ;
    for ($i = 0 ; $i < $n; $i++)
        echo $op[$i], " ";

    echo "\n";
}

    // Driver Code
    //input Array
    $arr = array(14, 6, 19, 21, 12);

    // calculating the length
    // of array A
    $n = sizeof($arr);

    // calling pendulum function
    pendulumArrangement($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
      // JavaScript program for pendulum
      // arrangement of numbers

      // Prints pendulam arrangement of arr[]
      function pendulumArrangement(arr, n)
      {

        // sorting the elements
        arr.sort(function (a, b) {
          return a - b;
        });

        // Auxiliary array to store output
        var op = [...Array(n)];

        // calculating the middle index
        var mid = parseInt((n - 1) / 2);

        // storing the minimum element in the middle
        // i is index for output array and j is for
        // input array.
        var j = 1,
          i = 1;
        op[mid] = arr[0];
        for (i = 1; i <= mid; i++) {
          op[mid + i] = arr[j++];
          op[mid - i] = arr[j++];
        }

        // adjustment for when no. of elements is even
        if (n % 2 == 0) op[mid + i] = arr[j];

        // Printing the pendulum arrangement
        document.write("Pendulum arrangement:<br>");
        for (i = 0; i < n; i++)
        document.write(op[i] + "  ");

        document.write("<br>");
      }

      // Driver function

      //input Array
      var arr = [14, 6, 19, 21, 12];

      // calculating the length of array A
      var n = arr.length;

      // calling pendulum function
      pendulumArrangement(arr, n);
    </script>
```

**输出:**

```
Pendulum arrangement:
21 14 6 12 19
```

本文由 **Nitin Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
# 打印给定数组的求和三角形的程序

> 原文:[https://www . geesforgeks . org/program-to-print-sum-triangle-for-给定数组/](https://www.geeksforgeeks.org/program-to-print-sum-triangle-for-a-given-array/)

给定一个数组，编写一个程序构造一个三角形，其中最后一行包含给定数组的元素，第二个最后一行的每个元素包含下面两个元素的和，以此类推。

**示例:**

```
Input: arr[] = {4, 7, 3, 6, 7};
Output:
81
40 41
21 19 22
11 10 9 13
4 7 3 6 7 

Input: {10, 40, 50}
Output:
140
50 90
10 40 50
```

关于输出的一个重要观察是最终值在顶部，并且需要首先打印顶部元素。因此，我们使用 2D 辅助数组以自下而上的方式构建三角形，然后打印三角形。2D 阵列的元素 tri[i][j]可以计算为 tri[i+1][j]和 tri[i+1][j+1]的和。

以下是上述想法的实现:

## C++

```
// C++ program to print sum triangle for a given array
#include <bits/stdc++.h>
using namespace std;

// prints sum triangle for arr[0..n-1]
void printTriangle(int arr[], int n)
{
    // Initialize a 2D array to store triangle
    int tri[n][n];
    memset(tri, 0, sizeof(tri));

    // Initialize last row of triangle
    for (int i = 0; i < n ; i++)
        tri[n-1][i] = arr[i];

    // Fill other rows
    for (int i = n-2; i >=0; i--)
      for (int j = 0; j <= i; j++)
        tri[i][j] = tri[i+1][j] + tri[i+1][j+1];

    // Print the triangle
    for (int i = 0; i < n; i++)
    {
        for(int j = 0; j <= i ; j++)
            cout << tri[i][j]<<" ";
        cout << endl;
    }
}

// Driver Program
int main()
{
    int arr[] = {4, 7, 3, 6, 7};
    int n = sizeof(arr)/sizeof(arr[0]);
    printTriangle(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print sum triangle for a given array
class Test{

     static int arr[] = new int[]{4, 7, 3, 6, 7};

     // prints sum triangle for arr[0..n-1]
     public static void printTriangle(int n)
     {
        // Initialize a 2D array to store triangle
        int tri[][] = new int[n][n];

        // Initialize last row of triangle
        for (int i = 0; i < n ; i++)
            tri[n-1][i] = arr[i];

        // Fill other rows
        for (int i = n-2; i >=0; i--)
            for (int j = 0; j <= i; j++)
               tri[i][j] = tri[i+1][j] + tri[i+1][j+1];

        // Print the triangle
        for (int i = 0; i < n; i++)
        {
            for(int j = 0; j <= i ; j++)
                System.out.print(tri[i][j] + " ");
            System.out.println();
        }
     }

     public static void main(String[] args)
     {
         printTriangle(arr.length);
        }
 }
```

## 蟒蛇 3

```
# Python 3 program to print sum triangle
# for a given array

# prints sum triangle for arr[0..n-1]
def printTriangle(arr, n):

    # Initialize a 2D array to store triangle
    tri = [[0 for i in range(n)]
              for i in range(n)]

    # Initialize last row of triangle
    for i in range(n):
        tri[n - 1][i] = arr[i]

    # Fill other rows
    i = n - 2
    while(i >= 0):
        for j in range(0, i + 1, 1):
            tri[i][j] = (tri[i + 1][j] +
                         tri[i + 1][j + 1])

        i -= 1

    # Print the triangle
    for i in range(0, n, 1):
        for j in range(0, i + 1, 1):
            print(tri[i][j], end = " ")
        print("\n", end = "")

# Driver Code
if __name__ == '__main__':
    arr = [4, 7, 3, 6, 7]
    n = len(arr)
    printTriangle(arr, n)

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to print sum triangle
// for a given array
using System;

class GFG {

    static int []arr = new int[]{4, 7, 3, 6, 7};

    // prints sum triangle for arr[0..n-1]
    public static void printTriangle(int n)
    {
        // Initialize a 2D array to store triangle
        int [,]tri = new int[n, n];

        // Initialize last row of triangle
        for (int i = 0; i < n ; i++)
            tri[n - 1, i] = arr[i];

        // Fill other rows
        for (int i = n - 2; i >= 0; i--)
            for (int j = 0; j <= i; j++)
            tri[i, j] = tri[i + 1, j] +
                        tri[i + 1, j + 1];

        // Print the triangle
        for (int i = 0; i < n; i++)
        {
            for(int j = 0; j <= i ; j++)
                Console.Write(tri[i, j] + " ");
                Console.WriteLine();
        }
    }

    // Driver Code
    public static void Main()
    {
        printTriangle(arr.Length);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print sum
// triangle for a given array

// prints sum triangle for arr[0..n-1]
function printTriangle($arr, $n)
{
    // Initialize a 2D array to store triangle
    $tri[$n][$n] = array(array());
    array_fill(0, count($tri), 0);

    // Initialize last row of triangle
    for ($i = 0; $i < $n ; $i++)
        $tri[$n - 1][$i] = $arr[$i];

    // Fill other rows
    for ($i = $n - 2; $i >= 0; $i--)
    for ($j = 0; $j <= $i; $j++)
        $tri[$i][$j] = $tri[$i + 1][$j] +
                       $tri[$i + 1][$j + 1];

    // Print the triangle
    for ($i = 0; $i < $n; $i++)
    {
        for( $j = 0; $j <= $i ; $j++)
            echo $tri[$i][$j] . " ";
        echo "\n";
    }
}

// Driver Code
$arr = array(4, 7, 3, 6, 7);
$n = count($arr);
printTriangle($arr, $n);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>
      // JavaScript program to print sum triangle for a given array

      // prints sum triangle for arr[0..n-1]
      function printTriangle(arr, n)
      {

        // Initialize a 2D array to store triangle
        var tri = new Array(n).fill(0).map((item) => new Array(n).fill(0));

        // Initialize last row of triangle
        for (var i = 0; i < n; i++) tri[n - 1][i] = arr[i];

        // Fill other rows
        for (var i = n - 2; i >= 0; i--)
          for (var j = 0; j <= i; j++)
            tri[i][j] = tri[i + 1][j] + tri[i + 1][j + 1];

        // Print the triangle
        for (var i = 0; i < n; i++) {
          for (var j = 0; j <= i; j++)
            document.write(tri[i][j] + "  ");
          document.write("<br>");
        }
      }

      // Driver Program
      var arr = [4, 7, 3, 6, 7];
      var n = arr.length;
      printTriangle(arr, n);

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
81
40 41
21 19 22
11 10 9 13
4 7 3 6 7

```

感谢 nish 提出这个解决方案。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息
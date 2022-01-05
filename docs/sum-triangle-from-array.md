# 对数组中的三角形求和

> 原文:[https://www.geeksforgeeks.org/sum-triangle-from-array/](https://www.geeksforgeeks.org/sum-triangle-from-array/)

给定一个整数数组，从中打印一个求和三角形，这样第一级就有了所有数组元素。从那时起，每一级的元素数量比前一级少一个，并且该级的元素是前一级中连续两个元素的总和。
**例:**

```
Input : A = {1, 2, 3, 4, 5}
Output : [48]
         [20, 28] 
         [8, 12, 16] 
         [3, 5, 7, 9] 
         [1, 2, 3, 4, 5] 

Explanation :
Here,   [48]
        [20, 28] -->(20 + 28 = 48)
        [8, 12, 16] -->(8 + 12 = 20, 12 + 16 = 28)
        [3, 5, 7, 9] -->(3 + 5 = 8, 5 + 7 = 12, 7 + 9 = 16)
        [1, 2, 3, 4, 5] -->(1 + 2 = 3, 2 + 3 = 5, 3 + 4 = 7, 4 + 5 = 9)
```

**进场:**

1.  递归是关键。在每次迭代中创建一个新的数组，该数组包含数组中连续元素的和作为参数传递。
2.  进行递归调用，并传递上一步中新创建的数组。
3.  同时反向跟踪打印阵列(以逆序打印)。

下面是执行上述方法:

## C++

```
// C++ program to create Special triangle.
#include<bits/stdc++.h>
using namespace std;

// Function to generate Special Triangle
void printTriangle(int A[] , int n)
    {
        // Base case
        if (n < 1)
            return;

        // Creating new array which contains the
        // Sum of consecutive elements in
        // the array passes as parameter.
        int temp[n - 1];
        for (int i = 0; i < n - 1; i++)
        {
            int x = A[i] + A[i + 1];
            temp[i] = x;
        }

        // Make a recursive call and pass
        // the newly created array
        printTriangle(temp, n - 1);

        // Print current array in the end so
        // that smaller arrays are printed first
        for (int i = 0; i < n ; i++)
        {
            if(i == n - 1)
                cout << A[i] << " ";
            else
            cout << A[i] << ", ";
        }

        cout << endl;
    }

    // Driver function
    int main()
    {
        int A[] = { 1, 2, 3, 4, 5 };
        int n = sizeof(A) / sizeof(A[0]);

        printTriangle(A, n);
    }

// This code is contributed by Smitha Dinesh Semwal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to create Special triangle.
import java.util.*;
import java.lang.*;

public class ConstructTriangle
{
    // Function to generate Special Triangle.
    public static void printTriangle(int[] A)
    {
        // Base case
        if (A.length < 1)
            return;

        // Creating new array which contains the
        // Sum of consecutive elements in
        // the array passes as parameter.
        int[] temp = new int[A.length - 1];
        for (int i = 0; i < A.length - 1; i++)
        {
            int x = A[i] + A[i + 1];
            temp[i] = x;
        }

        // Make a recursive call and pass
        // the newly created array
        printTriangle(temp);

        // Print current array in the end so
        // that smaller arrays are printed first
        System.out.println(Arrays.toString(A));
    }

    // Driver function
    public static void main(String[] args)
    {
        int[] A = { 1, 2, 3, 4, 5 };
        printTriangle(A);
    }
}
```

## 蟒蛇 3

```
# Python3 program to create Special triangle.
# Function to generate Special Triangle.
def printTriangle(A):

        # Base case
        if (len(A) < 1):
            return

        # Creating new array which contains the
        # Sum of consecutive elements in
        # the array passes as parameter.
        temp = [0] * (len(A) - 1)
        for i in range( 0, len(A) - 1):

            x = A[i] + A[i + 1]
            temp[i] = x

        # Make a recursive call and pass
        # the newly created array
        printTriangle(temp)

        # Print current array in the end so
        # that smaller arrays are printed first
        print(A)

# Driver function
A = [ 1, 2, 3, 4, 5 ]
printTriangle(A)

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to create Special triangle.

using System;

public class ConstructTriangle
{
// Function to generate Special Triangle
static void printTriangle(int []A, int n)
    {
        // Base case
        if (n < 1)
            return;

        // Creating new array which contains the
        // Sum of consecutive elements in
        // the array passes as parameter.
        int []temp = new int[n - 1];
        for (int i = 0; i < n - 1; i++)
        {
            int x = A[i] + A[i + 1];
            temp[i] = x;
        }

        // Make a recursive call and pass
        // the newly created array
        printTriangle(temp, n - 1);

        // Print current array in the end so
        // that smaller arrays are printed first
        for (int i = 0; i < n ; i++)
        {
            if(i == n - 1)
                Console.Write(A[i] + " ");
            else
            Console.Write(A[i] + ", ");
        }

        Console.WriteLine();
    }

    // Driver function
    public static void Main()
    {
        int[] A = { 1, 2, 3, 4, 5 };
        int n = A.Length;
        printTriangle(A,n);
    }
}

//This code contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to create
// Special triangle.

// Function to generate
// Special Triangle
function printTriangle($A , $n)
    {

        // Base case
        if ($n < 1)
            return;

        // Creating new array which
        // contains the Sum of
        // consecutive elements in
        // the array passes as parameter.
        $temp[$n - 1] = 0;
        for ($i = 0; $i < $n - 1; $i++)
        {
            $x = $A[$i] + $A[$i + 1];
            $temp[$i] = $x;
        }

        // Make a recursive call and
        // pass the newly created array
        printTriangle($temp, $n - 1);

        // Print current array in the
        // end so that smaller arrays
        // are printed first
        for ($i = 0; $i < $n ; $i++)
        {
            if($i == $n - 1)
                echo $A[$i] , " ";
            else
            echo $A[$i] , ", ";
        }

        echo "\n";
    }

// Driver Code
$A = array( 1, 2, 3, 4, 5 );
$n = sizeof($A);

printTriangle($A, $n);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to create Special triangle.

// Function to generate Special Triangle
 function printTriangle(A,  n)
    {
        // Base case
        if (n < 1)
            return;

        // Creating new array which contains the
        // Sum of consecutive elements in
        // the array passes as parameter.
        var temp = new Array(n - 1);
        for (var i = 0; i < n - 1; i++)
        {
            var x = A[i] + A[i + 1];
            temp[i] = x;
        }

        // Make a recursive call and pass
        // the newly created array
        printTriangle(temp, n - 1);

        // Print current array in the end so
        // that smaller arrays are printed first
        for (var i = 0; i < n ; i++)
        {
            if(i == n - 1)
                document.write( A[i]  + " ");
            else
            document.write( A[i]  + ", ");
        }

        document.write("<br>");
    }

    // Driver function

         var A = [ 1, 2, 3, 4, 5 ];
        var n = A.length;
        printTriangle(A,n);

</script>
```

**输出:**

```
48
20, 28
8, 12, 16
3, 5, 7, 9
1, 2, 3, 4, 5
```
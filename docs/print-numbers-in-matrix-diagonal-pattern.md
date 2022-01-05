# 以矩阵对角线模式打印数字

> 原文:[https://www . geesforgeks . org/print-numbers-in-matrix-对角线-pattern/](https://www.geeksforgeeks.org/print-numbers-in-matrix-diagonal-pattern/)

给定一个整数 **N** ，任务是打印给定的图案。
**例:**

```
Input: 3
Output:
1 2 4 
3 5 7 
6 8 9

Input: 4
Output:
1 2 4 7 
3 5 8 11 
6 9 12 14 
10 13 15 16
```

**进场:**

*   创建一个大小为 **N X N** 的矩阵，该矩阵将在打印前存储图案。
*   将元素存储在图案的上部三角形中。正如所观察到的，当您向下移动对角线时，行索引增加 1，列索引减少 1。
*   一旦上三角形完成，则以与上三角形类似的方式存储下三角形的元素，即当您沿对角线向下移动时，行索引增加 1，列索引减少 1。

以下是上述方法的实现:

## C++

```
// C++ program to print the required pattern
#include <bits/stdc++.h>
using namespace std;

// Function to print the required pattern
void printPattern(int n)
{
    // arr[][] will store the pattern matrix
    int arr[n][n], k, i, j, p = 1, f;

    // Store the values for upper triangle
    // of the pattern
    for (k = 0; k < n; k++) {
        j = k;
        i = 0;
        while (j >= 0) {
            arr[i][j] = p;
            p++;
            i = i + 1;
            j = j - 1;
        }
    }

    // Store the values for lower triangle
    // of the pattern
    for (k = 1; k < n; k++) {
        i = k;
        j = n - 1;
        f = k;
        while (j >= f) {
            arr[i][j] = p;
            p++;
            i = i + 1;
            j = j - 1;
        }
    }

    // Print the pattern
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    int n = 3;

    printPattern(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the required pattern

public class GFG{

    // Function to print the required pattern
    static void printPattern(int n)
    {
        // arr[][] will store the pattern matrix
        int arr[][] = new int[n][n] ;
        int k, i, j, p = 1, f ;

        // Store the values for upper triangle
        // of the pattern
        for (k = 0; k < n; k++) {
            j = k;
            i = 0;
            while (j >= 0) {
                arr[i][j] = p;
                p++;
                i = i + 1;
                j = j - 1;
            }
        }

        // Store the values for lower triangle
        // of the pattern
        for (k = 1; k < n; k++) {
            i = k;
            j = n - 1;
            f = k;
            while (j >= f) {
                arr[i][j] = p;
                p++;
                i = i + 1;
                j = j - 1;
            }
        }

        // Print the pattern
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                System.out.print(arr[i][j] + " ") ;
            }
            System.out.println() ;
        }
    }

    // Driver code
    public static void main(String []args)
    {
        int n = 3;

        printPattern(n);
    }
    // This code is contributed by Ryuga

}
```

## 蟒蛇 3

```
# Python 3 program to print the
# required pattern

# Function to print the required pattern
def printPattern(n):

    # arr[][] will store the pattern matrix
    arr = [[0 for i in range(n)]
              for j in range(n)]
    p = 1

    # Store the values for upper
    # triangle of the pattern
    for k in range(n):
        j = k
        i = 0
        while (j >= 0):
            arr[i][j] = p
            p += 1
            i = i + 1
            j = j - 1

    # Store the values for lower triangle
    # of the pattern
    for k in range(1, n, 1):
        i = k
        j = n - 1
        f = k
        while (j >= f):
            arr[i][j] = p
            p += 1
            i = i + 1
            j = j - 1

    # Print the pattern
    for i in range(0, n, 1):
        for j in range(0, n, 1):
            print(arr[i][j], end = " ")

        print("\n", end = "")

# Driver code
if __name__ == '__main__':
    n = 3

    printPattern(n)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to print the required pattern
using System;

public class GFG{

    // Function to print the required pattern
    static void printPattern(int n)
    {
        // arr[][] will store the pattern matrix
        int [,]arr = new int[n,n] ;
        int k, i, j, p = 1, f ;

        // Store the values for upper triangle
        // of the pattern
        for (k = 0; k < n; k++) {
            j = k;
            i = 0;
            while (j >= 0) {
                arr[i,j] = p;
                p++;
                i = i + 1;
                j = j - 1;
            }
        }

        // Store the values for lower triangle
        // of the pattern
        for (k = 1; k < n; k++) {
            i = k;
            j = n - 1;
            f = k;
            while (j >= f) {
                arr[i,j] = p;
                p++;
                i = i + 1;
                j = j - 1;
            }
        }

        // Print the pattern
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                Console.Write(arr[i,j] + " ") ;
            }
            Console.WriteLine() ;
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 3;

        printPattern(n);
    }
    // This code is contributed by inder_verma..

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the required pattern

// Function to print the required pattern
function printPattern($n)
{
    // arr[][] will store the pattern matrix
    $arr[][] = array($n, $n);
    $k; $i; $j; $p = 1; $f;

    // Store the values for upper
    // triangle of the pattern
    for ($k = 0; $k < $n; $k++)
    {
        $j = $k;
        $i = 0;
        while ($j >= 0)
        {
            $arr[$i][$j] = $p;
            $p++;
            $i = $i + 1;
            $j = $j - 1;
        }
    }

    // Store the values for lower
    // triangle of the pattern
    for ($k = 1; $k < $n; $k++)
    {
        $i = $k;
        $j = $n - 1;
        $f = $k;
        while ($j >= $f)
        {
            $arr[$i][$j] = $p;
            $p++;
            $i = $i + 1;
            $j = $j - 1;
        }
    }

    // Print the pattern
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            echo($arr[$i][$j] . " ");
        }
        echo("\n");
    }
}

// Driver code
$n = 3;

printPattern($n);

// This code is contributed
// by Mukul Singh
?>
```

## java 描述语言

```
<script>
    // Javascript program to print the required pattern

    // Function to print the required pattern
    function printPattern(n)
    {
        // arr[][] will store the pattern matrix
        let arr = new Array(n);
        for(let i = 0; i < n; i++)
        {
            arr[i] = new Array(n);
            for(let j = 0; j < n; j++)
            {
                arr[i][j] = 0;
            }
        }
        let k, i, j, p = 1, f ;

        // Store the values for upper triangle
        // of the pattern
        for (k = 0; k < n; k++) {
            j = k;
            i = 0;
            while (j >= 0) {
                arr[i][j] = p;
                p++;
                i = i + 1;
                j = j - 1;
            }
        }

        // Store the values for lower triangle
        // of the pattern
        for (k = 1; k < n; k++) {
            i = k;
            j = n - 1;
            f = k;
            while (j >= f) {
                arr[i][j] = p;
                p++;
                i = i + 1;
                j = j - 1;
            }
        }

        // Print the pattern
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                document.write(arr[i][j] + " ") ;
            }
            document.write("<br>") ;
        }
    }

    let n = 3;      
      printPattern(n);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
1 2 4 
3 5 7 
6 8 9
```
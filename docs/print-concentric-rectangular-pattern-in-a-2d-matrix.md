# 以 2d 矩阵打印同心矩形图案

> 原文:[https://www . geeksforgeeks . org/print-同心圆-矩形-二维矩阵图案/](https://www.geeksforgeeks.org/print-concentric-rectangular-pattern-in-a-2d-matrix/)

给定一个正整数 **n** ，打印填充矩形图案的矩阵如下图:
T3【a a a a a a a aT5**a b b b b a**T8**a b c b a**T11**a b b b b a**T14**a a a a**T17】其中 a = n，b = n–1，c = n–2 以此类推。

**示例:**

```
Input : n = 4
Output :
4 4 4 4 4 4 4 
4 3 3 3 3 3 4 
4 3 2 2 2 3 4 
4 3 2 1 2 3 4 
4 3 2 2 2 3 4 
4 3 3 3 3 3 4 
4 4 4 4 4 4 4 

Input : n = 3
Output :
3 3 3 3 3 
3 2 2 2 3 
3 2 1 2 3 
3 2 2 2 3 
3 3 3 3 3 
```

对于给定的 **n** ，要打印的行数或列数为 2 * n–1。我们将把矩阵打印成两部分。我们将首先从 0 到楼层((2 * n–1)/2)的行打印上半部分，然后从楼层((2 * n–1)/2)+1 到 2 * n–2 打印下半部分。
现在对于每一行，我们将分三部分打印。第一部分是递减序列，从 n 开始，每次迭代递减 1。迭代次数等于行号，第二部分是常数序列，其中常数为 n–I，打印 2 * n–1–2 *行号，第三部分是递增序列，与第一个序列相反。
下半部分，观察，是上半部分(不含中排)的镜像。因此，只需运行上半部分从(2 * n–1)/2 到 0 的循环。

下面是这种方法的基本实现:

## C++

```
// C++ program for printing
// the rectangular pattern
#include <bits/stdc++.h>
using namespace std;

// Function to print the pattern
void printPattern(int n)
{
    // number of rows and columns to be printed
    int s = 2 * n - 1;

    // Upper Half
    for (int i = 0; i < (s / 2) + 1; i++) {

        int m = n;

        // Decreasing part
        for (int j = 0; j < i; j++) {
            cout << m << " ";
            m--;
        }

        // Constant Part
        for (int k = 0; k < s - 2 * i; k++) {
            cout << n - i << " ";
        }

        // Increasing part.
        m = n - i + 1;
        for (int l = 0; l < i; l++) {
            cout << m << " ";
            m++;
        }

        cout << endl;
    }

    // Lower Half
    for (int i = s / 2 - 1; i >= 0; i--) {

        // Decreasing Part
        int m = n;
        for (int j = 0; j < i; j++) {
            cout << m << " ";
            m--;
        }

        // Constant Part.
        for (int k = 0; k < s - 2 * i; k++) {
            cout << n - i << " ";
        }

        // Decreasing Part
        m = n - i + 1;
        for (int l = 0; l < i; l++) {
            cout << m << " ";
            m++;
        }
        cout << endl;
    }
}
// Driven Program
int main()
{
    int n = 3;

    printPattern(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for printing
// the rectangular pattern
import java.io.*;

class GFG
{

// Function to
// print the pattern
static void printPattern(int n)
{
    // number of rows and
    // columns to be printed
    int s = 2 * n - 1;

    // Upper Half
    for (int i = 0;
             i < (s / 2) + 1; i++)
    {
        int m = n;

        // Decreasing part
        for (int j = 0; j < i; j++)
        {
            System.out.print(m + " ");
            m--;
        }

        // Constant Part
        for (int k = 0;
                 k < s - 2 * i; k++)
        {
            System.out.print(n - i + " ");
        }

        // Increasing part.
        m = n - i + 1;
        for (int l = 0; l < i; l++)
        {
            System.out.print(m + " ");
            m++;
        }

        System.out.println();
    }

    // Lower Half
    for (int i = s / 2 - 1;
             i >= 0; i--)
    {

        // Decreasing Part
        int m = n;
        for (int j = 0; j < i; j++)
        {
            System.out.print(m + " ");
            m--;
        }

        // Constant Part.
        for (int k = 0;
                 k < s - 2 * i; k++)
        {
            System.out.print(n - i + " ");
        }

        // Decreasing Part
        m = n - i + 1;
        for (int l = 0; l < i; l++)
        {
            System.out.print(m + " ");
            m++;
        }
        System.out.println();
    }
}
// Driver Code
public static void main (String[] args)
{
    int n = 3;

    printPattern(n);
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 program for printing
# the rectangular pattern

# Function to print the pattern
def printPattern(n) :

    # number of rows and columns to be printed
    s = 2 * n - 1

    # Upper Half
    for i in range(0, int(s / 2) + 1):

        m = n

        # Decreasing part
        for j in range(0, i):
            print(m ,end= " " )
            m-=1

        # Constant Part
        for k in range(0, s - 2 * i):
            print(n-i ,end= " " )

        # Increasing part.
        m = n - i + 1
        for l in range(0, i):
            print(m ,end= " " )
            m+=1

        print("")

    # Lower Half
    for i in range(int(s / 2),-1,-1):

        # Decreasing Part
        m = n
        for j in range(0, i):
            print(m ,end= " " )
            m-=1

        # Constant Part.
        for k in range(0, s - 2 * i):
            print(n-i ,end= " " )

        # Decreasing Part
        m = n - i + 1
        for l in range(0, i):
            print(m ,end= " " )
            m+=1

        print("")

# Driven Program
if __name__=='__main__':
    n = 3
    printPattern(n)

# this code is contributed by Smitha Dinesh
# Semwal
```

## C#

```
// C# program for printing
// the rectangular pattern
using System;

class GFG
{

// Function to
// print the pattern
static void printPattern(int n)
{
    // number of rows and
    // columns to be printed
    int s = 2 * n - 1;

    // Upper Half
    for (int i = 0;
             i < (s / 2) + 1; i++)
    {
        int m = n;

        // Decreasing part
        for (int j = 0; j < i; j++)
        {
            Console.Write(m + " ");
            m--;
        }

        // Constant Part
        for (int k = 0;
                 k < s - 2 * i; k++)
        {
            Console.Write(n - i + " ");
        }

        // Increasing part.
        m = n - i + 1;
        for (int l = 0; l < i; l++)
        {
            Console.Write(m + " ");
            m++;
        }

        Console.WriteLine();
    }

    // Lower Half
    for (int i = s / 2 - 1;
             i >= 0; i--)
    {

        // Decreasing Part
        int m = n;
        for (int j = 0; j < i; j++)
        {
            Console.Write(m + " ");
            m--;
        }

        // Constant Part.
        for (int k = 0;
                 k < s - 2 * i; k++)
        {
            Console.Write(n - i + " ");
        }

        // Decreasing Part
        m = n - i + 1;
        for (int l = 0; l < i; l++)
        {
            Console.Write(m + " ");
            m++;
        }
        Console.WriteLine();
    }
}
// Driver Code
public static void Main ()
{
    int n = 3;

    printPattern(n);
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for printing
// the rectangular pattern

// Function to print the pattern
function printPattern($n)
{
    // number of rows and columns
    // to be printed
    $s = 2 * $n - 1;

    // Upper Half
    for ($i = 0;
         $i < (int)($s / 2) + 1; $i++)
    {

        $m = $n;

        // Decreasing part
        for ($j = 0; $j < $i; $j++)
        {
            echo $m , " ";
            $m--;
        }

        // Constant Part
        for ($k = 0; $k < $s - 2 * $i; $k++)
        {
            echo ($n - $i) , " ";
        }

        // Increasing part.
        $m = $n - $i + 1;
        for ($l = 0; $l < $i; $l++)
        {
            echo $m , " ";
            $m++;
        }

        echo "\n";
    }

    // Lower Half
    for ($i = (int)($s / 2 - 1);
         $i >= 0; $i--)
    {

        // Decreasing Part
        $m = $n;
        for ($j = 0; $j < $i; $j++)
        {
            echo $m, " ";
            $m--;
        }

        // Constant Part.
        for ($k = 0; $k < $s - 2 * $i; $k++)
        {
            echo $n - $i , " ";
        }

        // Decreasing Part
        $m = $n - $i + 1;
        for ($l = 0; $l < $i; $l++)
        {
            echo $m , " ";
            $m++;
        }
        echo "\n";
    }
}

// Driver Code
$n = 3;
printPattern($n);

// This code is contributed
// by Sach_Code   
?>
```

## java 描述语言

```
<script>

// Javascript program for printing
// the rectangular pattern

// Function to
// print the pattern
function printPattern(n)
{
    // number of rows and
    // columns to be printed
    let s = 2 * n - 1;

    // Upper Half
    for (let i = 0;
             i < Math.floor(s / 2) + 1; i++)
    {
        let m = n;

        // Decreasing part
        for (let j = 0; j < i; j++)
        {
            document.write(m + " ");
            m--;
        }

        // Constant Part
        for (let k = 0;
                 k < s - 2 * i; k++)
        {
            document.write(n - i + " ");
        }

        // Increasing part.
        m = n - i + 1;
        for (let l = 0; l < i; l++)
        {
            document.write(m + " ");
            m++;
        }

        document.write("<br/>");
    }

    // Lower Half
    for (let i = Math.floor(s / 2) - 1;
             i >= 0; i--)
    {

        // Decreasing Part
        let m = n;
        for (let j = 0; j < i; j++)
        {
            document.write(m + " ");
            m--;
        }

        // Constant Part.
        for (let k = 0;
                 k < s - 2 * i; k++)
        {
            document.write(n - i + " ");
        }

        // Decreasing Part
        m = n - i + 1;
        for (let l = 0; l < i; l++)
        {
            document.write(m + " ");
            m++;
        }
        document.write("<br/>");
    }
}

// Driver Code

      let n = 3;

    printPattern(n);

</script>
```

**输出**

```
3 3 3 3 3 
3 2 2 2 3 
3 2 1 2 3 
3 2 2 2 3 
3 3 3 3 3  
```

**另一种方法:**

## C++

```
// C++ program for printing
// the rectangular pattern
#include<bits/stdc++.h>
using namespace std;

// Function to print the pattern
void printPattern(int n)
{
    int arraySize = n * 2 - 1;
    int result[arraySize][arraySize];

    // Fill the values
    for(int i = 0; i < arraySize; i++)
    {
        for(int j = 0; j < arraySize; j++)
        {
            if(abs(i - arraySize / 2) > abs(j - arraySize / 2))
                result[i][j] = abs(i - arraySize / 2) + 1;
            else
                result[i][j] = (abs(j-arraySize / 2) + 1);

        }
    }

    // Print the array
    for(int i = 0; i < arraySize; i++)
    {
        for(int j = 0; j < arraySize; j++)
        {
            cout << result[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    int n = 3;

    printPattern(n);
    return 0;
}

// This code is contributed
// by Rajput-Ji.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for printing
// the rectangular pattern
import java.io.*;

class GFG
{

// Function to print the pattern
static void printPattern(int n)
{
        int arraySize = n * 2 - 1;
        int[][] result = new int[arraySize][arraySize];

        //Fill the values
        for(int i = 0; i < arraySize; i++)
        {
            for(int j = 0; j < arraySize; j++)
            {
                result[i][j] = Math.max(Math.abs(i-arraySize/2),
                                    Math.abs(j-arraySize/2))+1;
            }
        }

        //Print the array
        for(int i = 0; i < arraySize; i++)
        {
            for(int j = 0; j < arraySize; j++)
            {
            System.out.print(result[i][j]);
            }
            System.out.println();
        }
}
// Driver Code
public static void main (String[] args)
{
    int n = 3;

    printPattern(n);
}
}

// This code is contributed
// by MohitSharma23.
```

## 蟒蛇 3

```
# Python3 program for printing
# the rectangular pattern

# Function to print the pattern
def printPattern(n):

    arraySize = n * 2 - 1;
    result = [[0 for x in range(arraySize)]
                 for y in range(arraySize)];

    # Fill the values
    for i in range(arraySize):
        for j in range(arraySize):
            if(abs(i - (arraySize // 2)) >
               abs(j - (arraySize // 2))):
                result[i][j] = abs(i - (arraySize // 2)) + 1;
            else:
                result[i][j] = abs(j - (arraySize // 2)) + 1;

    # Print the array
    for i in range(arraySize):
        for j in range(arraySize):
            print(result[i][j], end = " ");
        print("");

# Driver Code
n = 3;

printPattern(n);

# This code is contributed by mits
```

## C#

```
// C# program for printing
// the rectangular pattern
using System;

class GFG
{

// Function to print the pattern
static void printPattern(int n)
{
        int arraySize = n * 2 - 1;
        int[,] result = new int[arraySize,arraySize];

        // Fill the values
        for(int i = 0; i < arraySize; i++)
        {
            for(int j = 0; j < arraySize; j++)
            {
                result[i,j] = Math.Max(Math.Abs(i-arraySize/2),
                                    Math.Abs(j-arraySize/2))+1;
            }
        }

        // Print the array
        for(int i = 0; i < arraySize; i++)
        {
            for(int j = 0; j < arraySize; j++)
            {
                Console.Write(result[i,j]+" ");
            }
            Console.WriteLine();
        }
}

// Driver Code
public static void Main (String[] args)
{
    int n = 3;

    printPattern(n);
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for printing
// the rectangular pattern

// Function to print the pattern
function printPattern($n)
{
    $arraySize = $n * 2 - 1;
    $result=array_fill(0,$arraySize,array_fill(0,$arraySize,0));

    // Fill the values
    for($i = 0; $i < $arraySize; $i++)
    {
        for($j = 0; $j < $arraySize; $j++)
        {
            if(abs($i - (int)($arraySize / 2)) >
                    abs($j - (int)($arraySize / 2)))
                $result[$i][$j] = abs($i -
                        (int)($arraySize / 2)) + 1;
            else
                $result[$i][$j] = (abs($j-(int)
                                ($arraySize / 2)) + 1);

        }
    }

    // Print the array
    for($i = 0; $i < $arraySize; $i++)
    {
        for($j = 0; $j < $arraySize; $j++)
        {
            echo $result[$i][$j]." ";
        }
        echo "\n";
    }
}

// Driver Code

    $n = 3;

    printPattern($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program for printing the rectangular pattern

    // Function to print the pattern
    function printPattern(n)
    {
            let arraySize = n * 2 - 1;
            let result = new Array(arraySize);

            // Fill the values
            for(let i = 0; i < arraySize; i++)
            {
                result[i] = new Array(arraySize);
                for(let j = 0; j < arraySize; j++)
                {
                    result[i][j] = Math.max(Math.abs(i-parseInt(arraySize/2, 10)),
                                        Math.abs(j-parseInt(arraySize/2, 10)))+1;
                }
            }

            // Print the array
            for(let i = 0; i < arraySize; i++)
            {
                for(let j = 0; j < arraySize; j++)
                {
                    document.write(result[i][j] + " ");
                }
                  document.write("</br>");
            }
    }

    let n = 3;

    printPattern(n);

// This code is contributed by divyeshrabadiya07.
</script>
```

**输出**

```
3 3 3 3 3 
3 2 2 2 3 
3 2 1 2 3 
3 2 2 2 3 
3 3 3 3 3  
```
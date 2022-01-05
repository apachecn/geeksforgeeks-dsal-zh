# 拉丁方

> 原文:[https://www.geeksforgeeks.org/latin-square/](https://www.geeksforgeeks.org/latin-square/)

拉丁方是一个 n×n 的网格，由 n 个不同的数字填充，每一行和每一列恰好出现一次。给定一个输入 n，我们必须打印一个 n×n 矩阵，该矩阵由从 1 到 n 的数字组成，每行和每列恰好出现一次。
**例:**

```
Input: 3
Output:  1 2 3
         3 1 2 
         2 3 1

Input: 5
Output:  1 2 3 4 5
         5 1 2 3 4
         4 5 1 2 3 
         3 4 5 1 2
         2 3 4 5 1
```

你发现数字存储在拉丁方块中的模式了吗？

*   在第一行中，数字从 1 到 n 连续存储。
*   在第二行，数字向右移动一列。即 1 现在存储在第二列，以此类推。
*   在第三行，数字向右移动两列。即 1 现在存储在第 3 列，以此类推。
*   我们对其余的行继续同样的方法。

**注**:n×n 拉丁方可能有多种可能的配置。

## C++

```
// C++ program to print Latin Square
#include<stdio.h>

// Function to print n x n Latin Square
void printLatin(int n)
{
    // A variable to control the rotation
    // point.
    int k = n+1;

    // Loop to print rows
    for (int i=1; i<=n; i++)
    {
        // This loops runs only after first
        // iteration of outer loop. It prints
        // numbers from n to k
        int temp = k;
        while (temp <= n)
        {
            printf("%d ", temp);
            temp++;
        }

        // This loop prints numbers from 1 to k-1.
        for (int j=1; j<k; j++)
            printf("%d ", j);

        k--;
        printf("\n");
    }
}

// Driver program to test above function
int main(void)
{
    int n = 5;

    // Invoking printLatin function
    printLatin(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print Latin Square
class GFG {

    // Function to print n x n Latin Square
    static void printLatin(int n)
    {

        // A variable to control the
        // rotation point.
        int k = n+1;

        // Loop to print rows
        for (int i = 1; i <= n; i++)
        {

            // This loops runs only after
            // first iteration of outer
            // loop. It prints
            // numbers from n to k
            int temp = k;

            while (temp <= n)
            {
                System.out.print(temp + " ");
                temp++;
            }

            // This loop prints numbers from
            // 1 to k-1.
            for (int j = 1; j < k; j++)
                System.out.print(j + " ");

            k--;
            System.out.println();
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 5;

        // Invoking printLatin function
        printLatin(n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program to print Latin Square

# Function to prn x n Latin Square
def printLatin(n):

    # A variable to control the
    # rotation point.
    k = n + 1

    # Loop to prrows
    for i in range(1, n + 1, 1):

        # This loops runs only after first
        # iteration of outer loop. It prints
        # numbers from n to k
        temp = k
        while (temp <= n) :
            print(temp, end = " ")
            temp += 1

        # This loop prints numbers
        # from 1 to k-1.
        for j in range(1, k):
            print(j, end = " ")

        k -= 1
        print()

# Driver Code
n = 5

# Invoking printLatin function
printLatin(n)

# This code is contributed by R_Raj
```

## C#

```
// C# program to print Latin Square
using System;

class GFG {

    // Function to print n x n
    // Latin Square
    static void printLatin(int n)
    {

        // A variable to control the
        // rotation point.
        int k = n + 1;

        // Loop to print rows
        for (int i = 1; i <= n; i++)
        {

            // This loops runs only after
            // first iteration of outer
            // loop. It prints numbers
            // from n to k
            int temp = k;

            while (temp <= n)
            {
                Console.Write(temp + " ");
                temp++;
            }

            // This loop prints numbers from
            // 1 to k-1.
            for (int j = 1; j < k; j++)
                Console.Write(j + " ");

            k--;
            Console.WriteLine();
        }
    }

    // Driver code
    public static void Main ()
    {
        int n = 5;

        // Invoking printLatin function
        printLatin(n);
    }
}

// This code is contributed by KRV.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print Latin Square

// Function to print n x n Latin Square
function printLatin( $n)
{
    // A variable to control
    // the rotation point.
    $k = $n + 1;

    // Loop to print rows
    for ( $i = 1; $i <= $n; $i++)
    {
        // This loops runs only after
        // first iteration of outer loop.
        // It prints numbers from n to k
        $temp = $k;
        while ($temp <= $n)
        {
            echo $temp," ";
            $temp++;
        }

        // This loop prints numbers
        // from 1 to k-1.
        for ($j = 1; $j < $k; $j++)
            echo $j, " ";

        $k--;
        echo "\n";
    }
}

// Driver Code
$n = 5;

// Invoking printLatin function
printLatin($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // Javascript program to print Latin Square

    // Function to print n x n
    // Latin Square
    function printLatin(n)
    {

        // A variable to control the
        // rotation point.
        let k = n + 1;

        // Loop to print rows
        for (let i = 1; i <= n; i++)
        {

            // This loops runs only after
            // first iteration of outer
            // loop. It prints numbers
            // from n to k
            let temp = k;

            while (temp <= n)
            {
                document.write(temp + " ");
                temp++;
            }

            // This loop prints numbers from
            // 1 to k-1.
            for (let j = 1; j < k; j++)
                document.write(j + " ");

            k--;
            document.write("</br>");
        }
    }

    let n = 5;

    // Invoking printLatin function
    printLatin(n);

</script>
```

**输出:**

```
1 2 3 4 5 
5 1 2 3 4 
4 5 1 2 3 
3 4 5 1 2 
2 3 4 5 1 
```

**参考:**
[【https://en.wikipedia.org/wiki/Latin_square】](https://en.wikipedia.org/wiki/Latin_square)
本文由 [**Pratik Agarwal**](https://www.facebook.com/Pratik.Agarwal01) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
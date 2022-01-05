# 通过改变符号打印 N 个元素的所有组合，使得它们的总和可以被 M 整除

> 原文:[https://www . geeksforgeeks . org/print-n 元素的所有组合-通过改变符号-这样-它们的总和可以被 m 整除/](https://www.geeksforgeeks.org/print-all-the-combinations-of-n-elements-by-changing-sign-such-that-their-sum-is-divisible-by-m/)

给定一个由 N 个整数和 m 个整数组成的数组。您可以更改数组中任何元素的符号(正或负)。任务是打印数组元素的所有可能的组合，这些组合可以通过改变元素的符号来获得，这样它们的总和可以被 m 整除。

**注意**:你必须获取每个组合中的所有数组元素，并且与数组中的元素顺序相同。但是，您可以更改元素的符号。

**示例:**

> **输入:** a[] = {5，6，7}，M = 3
> **输出:**
> -5-6-7
> +5-6+7
> -5+6-7
> +5+6+7
> 
> **输入:** a[] = {3，5，6，8}，M = 5
> **输出:**
> -3-5+6-8
> -3+5+6-8
> +3-5-6+8
> +3+5-6+8

**方法:**这里使用[动力集](https://www.geeksforgeeks.org/power-set/)的概念来解决这个问题。使用幂集生成可应用于元素数组的所有可能的符号组合。如果得到的和能被 M 整除，那么打印组合。以下是步骤:

*   使用[功率设置](https://www.geeksforgeeks.org/power-set/)迭代所有可能的“+”和“-”组合。
*   迭代数组元素，如果左边第 j 位被设置，那么假设数组元素为正，如果该位没有被设置，那么假设数组元素为负。请参考此处的检查是否设置了位索引。
*   如果总和可被 M 整除，则再次遍历数组元素，并将它们与符号(“+”或“-”)一起打印出来。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to print all the combinations
void printCombinations(int a[], int n, int m)
{

    // Iterate for all combinations
    for (int i = 0; i < (1 << n); i++) {
        int sum = 0;

        // Initially 100 in binary if n is 3
        // as 1<<(3-1) = 100 in binary
        int num = 1 << (n - 1);

        // Iterate in the array and assign signs
        // to the array elements
        for (int j = 0; j < n; j++) {

            // If the j-th bit from left is set
            // take '+' sign
            if (i & num)
                sum += a[j];
            else
                sum += (-1 * a[j]);

            // Right shift to check if
            // jth bit is set or not
            num = num >> 1;
        }

        if (sum % m == 0) {

            // re-initialize
            num = 1 << (n - 1);

            // Iterate in the array elements
            for (int j = 0; j < n; j++) {

                // If the jth from left is set
                if ((i & num))
                    cout << "+" << a[j] << " ";
                else
                    cout << "-" << a[j] << " ";

                // right shift
                num = num >> 1;
            }
            cout << endl;
        }
    }
}

// Driver Code
int main()
{
    int a[] = { 3, 5, 6, 8 };
    int n = sizeof(a) / sizeof(a[0]);
    int m = 5;

    printCombinations(a, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG
{

// Function to print
// all the combinations
static void printCombinations(int a[],
                              int n, int m)
{

    // Iterate for all
    // combinations
    for (int i = 0;
             i < (1 << n); i++)
    {
        int sum = 0;

        // Initially 100 in binary
        // if n is 3 as
        // 1<<(3-1) = 100 in binary
        int num = 1 << (n - 1);

        // Iterate in the array
        // and assign signs to
        // the array elements
        for (int j = 0; j < n; j++)
        {

            // If the j-th bit
            // from left is set
            // take '+' sign
            if ((i & num) > 0)
                sum += a[j];
            else
                sum += (-1 * a[j]);

            // Right shift to check if
            // jth bit is set or not
            num = num >> 1;
        }

        if (sum % m == 0)
        {

            // re-initialize
            num = 1 << (n - 1);

            // Iterate in the
            // array elements
            for (int j = 0; j < n; j++)
            {

                // If the jth from
                // left is set
                if ((i & num) > 0)
                    System.out.print("+" +
                                     a[j] + " ");
                else
                    System.out.print("-" +
                                     a[j] + " ");

                // right shift
                num = num >> 1;
            }

        System.out.println();
        }
    }
}

// Driver code
public static void main(String args[])
{
    int a[] = { 3, 5, 6, 8 };
    int n = a.length;
    int m = 5;

    printCombinations(a, n, m);
}
}

// This code is contributed
// by inder_verma.
```

## 蟒蛇 3

```
# Function to print
# all the combinations
def printCombinations(a, n, m):

    # Iterate for all
    # combinations
    for i in range(0, (1 << n)):

        sum = 0

        # Initially 100 in binary
        # if n is 3 as
        # 1<<(3-1) = 100 in binary
        num = 1 << (n - 1)

        # Iterate in the array
        # and assign signs to
        # the array elements
        for j in range(0, n):

            # If the j-th bit
            # from left is set
            # take '+' sign
            if ((i & num) > 0):
                sum += a[j]
            else:
                sum += (-1 * a[j])

            # Right shift to check if
            # jth bit is set or not
            num = num >> 1

        if (sum % m == 0):

            # re-initialize
            num = 1 << (n - 1)

            # Iterate in the
            # array elements
            for j in range(0, n):

                # If the jth from
                # left is set
                if ((i & num) > 0):
                    print("+", a[j], end = " ",
                                     sep = "")
                else:
                    print("-", a[j], end = " ",
                                     sep = "")

                # right shift
                num = num >> 1
            print("")

# Driver code
a = [ 3, 5, 6, 8 ]
n = len(a)
m = 5
printCombinations(a, n, m)

# This code is contributed
# by smita.
```

## C#

```
// Print all the combinations
// of N elements by changing
// sign such that their sum
// is divisible by M
using System;

class GFG
{

// Function to print
// all the combinations
static void printCombinations(int []a,
                              int n, int m)
{

    // Iterate for all
    // combinations
    for (int i = 0;
             i < (1 << n); i++)
    {
        int sum = 0;

        // Initially 100 in binary
        // if n is 3 as
        // 1<<(3-1) = 100 in binary
        int num = 1 << (n - 1);

        // Iterate in the array
        // and assign signs to
        // the array elements
        for (int j = 0; j < n; j++)
        {

            // If the j-th bit
            // from left is set
            // take '+' sign
            if ((i & num) > 0)
                sum += a[j];
            else
                sum += (-1 * a[j]);

            // Right shift to check if
            // jth bit is set or not
            num = num >> 1;
        }

        if (sum % m == 0)
        {

            // re-initialize
            num = 1 << (n - 1);

            // Iterate in the
            // array elements
            for (int j = 0; j < n; j++)
            {

                // If the jth from
                // left is set
                if ((i & num) > 0)
                    Console.Write("+" +
                              a[j] + " ");
                else
                    Console.Write("-" +
                              a[j] + " ");

                // right shift
                num = num >> 1;
            }

        Console.Write("\n");
        }
    }
}

// Driver code
public static void Main()
{
    int []a = { 3, 5, 6, 8 };
    int n = a.Length;
    int m = 5;

    printCombinations(a, n, m);
}
}

// This code is contributed
// by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to print all the combinations
function printCombinations($a, $n, $m)
{

    // Iterate for all combinations
    for ($i = 0; $i < (1 << $n); $i++)
    {
        $sum = 0;

        // Initially 100 in binary if n 
        // is 3 as 1<<(3-1) = 100 in binary
        $num = 1 << ($n - 1);

        // Iterate in the array and assign
        // signs to the array elements
        for ($j = 0; $j < $n; $j++)
        {

            // If the j-th bit from left
            // is set take '+' sign
            if ($i & $num)
                $sum += $a[$j];
            else
                $sum += (-1 * $a[$j]);

            // Right shift to check if
            // jth bit is set or not
            $num = $num >> 1;
        }

        if ($sum % $m == 0)
        {

            // re-initialize
            $num = 1 << ($n - 1);

            // Iterate in the array elements
            for ($j = 0; $j < $n; $j++)
            {

                // If the jth from left is set
                if (($i & $num))
                    echo "+" , $a[$j] , " ";
                else
                    echo "-" , $a[$j] , " ";

                // right shift
                $num = $num >> 1;
            }
        echo "\n";
        }
    }
}

// Driver Code
$a = array( 3, 5, 6, 8 );
$n = sizeof($a);
$m = 5;

printCombinations($a, $n, $m);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Function to print
// all the combinations
function printCombinations(a, n, m)
{

    // Iterate for all
    // combinations
    for(let i = 0; i < (1 << n); i++)
    {
        let sum = 0;

        // Initially 100 in binary
        // if n is 3 as
        // 1<<(3-1) = 100 in binary
        let num = 1 << (n - 1);

        // Iterate in the array
        // and assign signs to
        // the array elements
        for(let j = 0; j < n; j++)
        {

            // If the j-th bit
            // from left is set
            // take '+' sign
            if ((i & num) > 0)
                sum += a[j];
            else
                sum += (-1 * a[j]);

            // Right shift to check if
            // jth bit is set or not
            num = num >> 1;
        }

        if (sum % m == 0)
        {

            // Re-initialize
            num = 1 << (n - 1);

            // Iterate in the
            // array elements
            for(let j = 0; j < n; j++)
            {

                // If the jth from
                // left is set
                if ((i & num) > 0)
                    document.write("+" + a[j] + " ");
                else
                    document.write("-" + a[j] + " ");

                // Right shift
                num = num >> 1;
            }
            document.write("</br>");
        }
    }
}

// Driver code
let a = [ 3, 5, 6, 8 ];
let n = a.length;
let m = 5;

printCombinations(a, n, m);

// This code is contributed by mukesh07 

</script>
```

**Output:** 

```
-3 -5 +6 -8 
-3 +5 +6 -8 
+3 -5 -6 +8 
+3 +5 -6 +8
```

**时间复杂度:** O(2 <sup>N</sup> * N)，其中 N 为元素个数。
# 求[1，n]

范围内所有数的除数

> 原文:[https://www . geeksforgeeks . org/find-范围内所有数字的除数-1-n/](https://www.geeksforgeeks.org/find-the-number-of-divisors-of-all-numbers-in-the-range-1-n/)

给定一个整数 **N** 。任务是找出**【1，N】**范围内所有数字的除数。

**示例:**

> **输入:** N = 5
> **输出:** 1 2 2 3 2
> 除数(1) = 1
> 除数(2) = 1 和 2
> 除数(3) = 1 和 3
> 除数(4) = 1、2 和 4
> 除数(5) = 1 和 5
> 
> **输入:** N = 10
> **输出:**1 2 2 3 4 2 4 3 4

**方法:**创建一个大小为 **(N + 1)** 的数组 **arr[]** ，其中 **arr[i]** 存储 **i** 的除数。现在，对于范围**【1，N】**中的每一个 **j** ，递增所有可被 **j** 整除的元素。
例如，如果 **j = 3** 则更新 **arr[3]、arr[6]、arr[9]，…**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of divisors
// of all numbers in the range [1, n]
void findDivisors(int n)
{

    // Array to store the count
    // of divisors
    int div[n + 1];
    memset(div, 0, sizeof div);

    // For every number from 1 to n
    for (int i = 1; i <= n; i++) {

        // Increase divisors count for
        // every number divisible by i
        for (int j = 1; j * i <= n; j++)
            div[i * j]++;
    }

    // Print the divisors
    for (int i = 1; i <= n; i++)
        cout << div[i] << " ";
}

// Driver code
int main()
{
    int n = 10;
    findDivisors(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function to find the number of divisors
    // of all numbers in the range [1, n]
    static void findDivisors(int n)
    {

        // Array to store the count
        // of divisors
        int[] div = new int[n + 1];

        // For every number from 1 to n
        for (int i = 1; i <= n; i++)
        {

            // Increase divisors count for
            // every number divisible by i
            for (int j = 1; j * i <= n; j++)
                div[i * j]++;
        }

        // Print the divisors
        for (int i = 1; i <= n; i++)
            System.out.print(div[i]+" ");
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 10;
        findDivisors(n);
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 implementation of the approach
# Function to find the number of divisors
# of all numbers in the range [1,n]
def findDivisors(n):

    # List to store the count
    # of divisors
    div = [0 for i in range(n + 1)]

    # For every number from 1 to n
    for i in range(1, n + 1):

        # Increase divisors count for
        # every number divisible by i
        for j in range(1, n + 1):
            if j * i <= n:
                div[i * j] += 1

    # Print the divisors
    for i in range(1, n + 1):
        print(div[i], end = " ")

# Driver Code
if __name__ == "__main__":
    n = 10
    findDivisors(n)

# This code is contributed by
# Vivek Kumar Singh
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the number of divisors
// of all numbers in the range [1, n]
static void findDivisors(int n)
{

    // Array to store the count
    // of divisors
    int[] div = new int[n + 1];

    // For every number from 1 to n
    for (int i = 1; i <= n; i++)
    {

        // Increase divisors count for
        // every number divisible by i
        for (int j = 1; j * i <= n; j++)
            div[i * j]++;
    }

    // Print the divisors
    for (int i = 1; i <= n; i++)
        Console.Write(div[i]+" ");
}

// Driver code
static void Main()
{
    int n = 10;
    findDivisors(n);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to find the number of divisors
// of all numbers in the range [1, n]
function findDivisors($n)
{

    // Array to store the count
    // of divisors
    $div = array_fill(0, $n + 2, 0);

    // For every number from 1 to n
    for ($i = 1; $i <= $n; $i++)
    {

        // Increase divisors count for
        // every number divisible by i
        for ($j = 1; $j * $i <= $n; $j++)
            $div[$i * $j]++;
    }

    // Print the divisors
    for ($i = 1; $i <= $n; $i++)
        echo $div[$i], " ";
}

// Driver code
$n = 10;
findDivisors($n);

// This code is contributed
// by Arnab Kundu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the number of divisors
// of all numbers in the range [1, n]
function findDivisors(n)
{

    // Array to store the count
    // of divisors
    let div = new Array(n + 1).fill(0);

    // For every number from 1 to n
    for(let i = 1; i <= n; i++)
    {

        // Increase divisors count for
        // every number divisible by i
        for(let j = 1; j * i <= n; j++)
            div[i * j]++;
    }

    // Print the divisors
    for(let i = 1; i <= n; i++)
        document.write(div[i] + " ");
}

// Driver code
let n = 10;
findDivisors(n);

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
1 2 2 3 2 4 2 4 3 4
```
# 检查一个数是否可以表示为 K 个不同正整数的和

> 原文:[https://www . geesforgeks . org/check-一个数字是否可以表示为 k 个不同正整数的和/](https://www.geeksforgeeks.org/check-whether-a-number-can-be-represented-as-sum-of-k-distinct-positive-integers/)

给定两个整数 **N** 和 **K** ，任务是检查 **N** 是否可以表示为 **K** 个不同正整数的和。

**示例:**

> **输入:** N = 12，K = 4
> **输出:**是
> N = 1 + 2 + 4 + 5 = 12 (12 为 4 个不同整数之和)
> 
> **输入:** N = 8，K = 4
> T3】输出:否

**方法:**考虑系列 **1 + 2 + 3 + … + K** ，其正好具有 **K** 个具有最小可能和的不同整数，即**和=(K *(K–1))/2**。现在，如果 **N < Sum** 则不能将 **N** 表示为 **K** 个不同正整数的和，但是如果 **N ≥ Sum** 则可以将任意整数如 **X ≥ 0** 加到 **Sum** 上，生成等于 **N** 的和，即**1+2+3+……+(K–1)+)**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns true if n
// can be represented as the sum of
// exactly k distinct positive integers
bool solve(int n, int k)
{
    // If n can be represented as
    // 1 + 2 + 3 + ... + (k - 1) + (k + x)
    if (n >= (k * (k + 1)) / 2) {
        return true;
    }

    return false;
}

// Driver code
int main()
{
    int n = 12, k = 4;

    if (solve(n, k))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG {

    // Function that returns true if n
    // can be represented as the sum of
    // exactly k distinct positive integers
    static boolean solve(int n, int k)
    {
        // If n can be represented as
        // 1 + 2 + 3 + ... + (k - 1) + (k + x)
        if (n >= (k * (k + 1)) / 2) {
            return true;
        }

        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 12, k = 4;

        if (solve(n, k))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if n
# can be represented as the sum of
# exactly k distinct positive integers
def solve(n,k):
    # If n can be represented as
    # 1 + 2 + 3 + ... + (k - 1) + (k + x)
    if (n >= (k * (k + 1)) // 2):
        return True

    return False

# Driver code
if __name__ == '__main__':
    n = 12
    k = 4

    if (solve(n, k)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function that returns true if n
    // can be represented as the sum of
    // exactly k distinct positive integers
    static bool solve(int n, int k)
    {
        // If n can be represented as
        // 1 + 2 + 3 + ... + (k - 1) + (k + x)
        if (n >= (k * (k + 1)) / 2) {
            return true;
        }

        return false;
    }

    // Driver code
    static public void Main ()
    {
        int n = 12, k = 4;

        if (solve(n, k))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the approach

// Function that returns true if n
// can be represented as the sum of
// exactly k distinct positive integers
function solve($n, $k)
{
    // If n can be represented as
    // 1 + 2 + 3 + ... + (k - 1) + (k + x)
    if ($n >= ($k * ($k + 1)) / 2) {
        return true;
    }

    return false;
}

// Driver code

$n = 12;
$k = 4;

if (solve($n, $k))
    echo  "Yes";
else
    echo  "No";

// This code is contributed by ihritik

?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if n
// can be represented as the sum of
// exactly k distinct positive integers
function solve(n, k)
{

    // If n can be represented as
    // 1 + 2 + 3 + ... + (k - 1) + (k + x)
    if (n >= (k * (k + 1)) / 2)
    {
        return true;
    }
    return false;
}

// Driver code
var n = 12, k = 4;

if (solve(n, k))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
Yes
```
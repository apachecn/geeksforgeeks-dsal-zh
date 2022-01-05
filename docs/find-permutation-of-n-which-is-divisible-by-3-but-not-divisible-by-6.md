# 求能被 3 整除但不能被 6 整除的 n 的排列

> 原文:[https://www . geeksforgeeks . org/find-n 的排列可被 3 整除但不能被 6 整除/](https://www.geeksforgeeks.org/find-permutation-of-n-which-is-divisible-by-3-but-not-divisible-by-6/)

给定一个整数![n     ](img/fa0f9698e6e59ce8e3e999505a99dbbe.png "Rendered by QuickLaTeX.com")。任务是找到另一个整数，它是 n 的排列，可被 3 整除但不能被 6 整除。假设 n 能被 6 整除。如果没有这样的排列，打印-1。

**示例**:

```
Input: n = 336
Output: 363

Input: n = 48
Output: -1
```

一个数要能被 6 整除，它必须能被 3 整除，也能被 2 整除，这意味着每个能被 3 整除的偶数都能被 6 整除。所以，能被 3 整除但不能被 6 整除的整数是能被 3 整除的奇数。
因此，如果整数 n 包含任何奇数，那么存在可被 3 整除但不能被 6 整除的置换，否则不存在这样的置换。

**算法**:

1.  设 LEN 为整数长度(即 ceil(log10(n))。
2.  迭代 LEN，检查 n 是偶数还是奇数。
    *   如果 n 是奇数，返回 n
    *   否则向右旋转 n 次。然后继续。
3.  如果 LEN 超过返回-1

下面是上述方法的实现:

## C++

```
// C++ program to find permutation of n
// which is divisible by 3 but not
// divisible by 6

#include <bits/stdc++.h>
using namespace std;

// Function to find the permutation
int findPermutation(int n)
{
    // length of integer
    int len = ceil(log10(n));

    for (int i = 0; i < len; i++) {
        // if integer is even
        if (n % 2 != 0) {
            // return odd integer
            return n;
        }
        else {
            // rotate integer
            n = (n / 10) + (n % 10) * pow(10, len - i - 1);
            continue;
        }
    }

    // return -1 in case no required
    // permutation exists
    return -1;
}

// Driver Code
int main()
{
    int n = 132;

    cout << findPermutation(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find permutation
// of n which is divisible by 3
// but not divisible by 6
import java.lang.*;
import java.util.*;

class GFG
{
// Function to find the permutation
static int findPermutation(int n)
{
    // length of integer
    int len = (int)Math.ceil(Math.log10(n));

    for (int i = 0; i < len; i++)
    {
        // if integer is even
        if (n % 2 != 0)
        {
            // return odd integer
            return n;
        }
        else
        {
            // rotate integer
            n = (n / 10) + (n % 10) *
                (int)Math.pow(10, len - i - 1);
            continue;
        }
    }

    // return -1 in case no required
    // permutation exists
    return -1;
}

// Driver Code
public static void main(String args[])
{
    int n = 132;

    System.out.println(findPermutation(n));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 program to find permutation
# of n which is divisible by 3 but
# not divisible by 6
from math import log10, ceil, pow

# Function to find the permutation
def findPermutation(n):

    # length of integer
    len = ceil(log10(n))

    for i in range(0, len, 1):

        # if integer is even
        if n % 2 != 0:

            # return odd integer
            return n
        else:

            # rotate integer
            n = ((n / 10) + (n % 10) *
                  pow(10, len - i - 1))
            continue

    # return -1 in case no required
    # permutation exists
    return -1

# Driver Code
if __name__ == '__main__':
    n = 132

    print(int(findPermutation(n)))

# This code is contributed
# by Surendra_Gangwar
```

## C#

```
// C# program to find permutation
// of n which is divisible by 3
// but not divisible by 6
using System;

class GFG
{
// Function to find the permutation
static int findPermutation(int n)
{
    // length of integer
    int len = (int)Math.Ceiling(Math.Log10(n));

    for (int i = 0; i < len; i++)
    {
        // if integer is even
        if (n % 2 != 0)
        {
            // return odd integer
            return n;
        }
        else
        {
            // rotate integer
            n = (n / 10) + (n % 10) *
                (int)Math.Pow(10, len - i - 1);
            continue;
        }
    }

    // return -1 in case no required
    // permutation exists
    return -1;
}

// Driver Code
public static void Main()
{
    int n = 132;

    Console.WriteLine(findPermutation(n));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find permutation
// of n which is divisible by 3 but
// not divisible by 6

// Function to find the permutation
function findPermutation($n)
{
    // length of integer
    $len = ceil(log10($n));

    for ($i = 0; $i < $len; $i++)
    {
        // if integer is even
        if ($n % 2 != 0)
        {
            // return odd integer
            return (int)$n;
        }
        else
        {
            // rotate integer
            $n = ($n / 10) + ($n % 10) *
                  pow(10, $len - $i - 1);
            continue;
        }
    }

    // return -1 in case no required
    // permutation exists
    return -1;
}

// Driver Code
$n = 132;

echo findPermutation($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// java script  program to find permutation
// of n which is divisible by 3 but
// not divisible by 6

// Function to find the permutation
function findPermutation(n)
{

    // length of integer
    let len = Math.ceil(Math.log10(n));

    for (let i = 0; i < len; i++)
    {

        // if integer is even
        if (n % 2 != 0)
        {

            // return odd integer
            return parseInt(n);
        }
        else
        {

            // rotate integer
            n = (n / 10) + (n % 10) *
                Math.pow(10, len - i - 1);
            continue;
        }
    }

    // return -1 in case no required
    // permutation exists
    return -1;
}

// Driver Code
let n = 132;

document.write( findPermutation(n));

// This code is contributed by sravan kumar (vignan)
</script>
```

**Output:** 

```
213
```
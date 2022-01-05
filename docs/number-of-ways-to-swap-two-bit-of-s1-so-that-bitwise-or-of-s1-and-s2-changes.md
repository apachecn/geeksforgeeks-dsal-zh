# 交换 s1 的两位以便 s1 和 s2 的按位“或”改变的方式数

> 原文:[https://www . geeksforgeeks . org/交换 s1 和 s2 的两位“按位或”更改的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-swap-two-bit-of-s1-so-that-bitwise-or-of-s1-and-s2-changes/)

给定两个长度为![N       ](img/ae8820e7c86d7e5688cd7d5335fa4d5f.png "Rendered by QuickLaTeX.com")的二进制数字串![s1       ](img/37fb1b4e0d7f341a55b4e1cd1d3e1d2b.png "Rendered by QuickLaTeX.com")和![s2       ](img/4da8ccf35c30750091c546aade3fceee.png "Rendered by QuickLaTeX.com")。找出 s1 中交换两位的方式数(仅 s1 而非 s2)，以便这两个数字的逐位“或”发生变化 **s1** 和 **s2** 。

**注意:**两个字符串的长度必须相等，长度不同时可以取前导零。

**示例:**

```
Input: s1 = "01011", s2 = "11001"
Output: 4
Explanation:
You can swap the bit of s1 at indexed:
(1, 4), (2, 3), (3, 4) and (3, 5)
there are 4 ways possible.

Input: s1 = "011000", s2 = "010011"
Output: 6
```

**方法:**将变量**结果**初始化为零，该变量存储交换 s1 位的方式数，以便 s1 和 s2 的按位“或”发生变化。将四个变量![a       ](img/52bc59826aafbb34ac7c40efc202e06a.png "Rendered by QuickLaTeX.com")、![b       ](img/a54f2ddff94c305c1eda8909719a86bd.png "Rendered by QuickLaTeX.com")、![c       ](img/fd8fbe40683b28d605e6a44f922cd3b2.png "Rendered by QuickLaTeX.com")、![d       ](img/5ccf383910b5eb473ae7dd80801fb145.png "Rendered by QuickLaTeX.com")初始化为零。

从左侧遍历两个字符串，并检查以下条件，以增加上面声明的
变量的值:

*   如果 s1 和 s2 的当前位都为零，则递增 c。
*   如果 s2 的当前位为零，s1 为 1，则递增 d。
*   如果 s2 的当前位为 1，s1 为零，则递增 a。
*   如果 s1 和 s2 的当前位都为 1，则递增 b。

通过 **(a*d) + (b*c) + (c*d)** 更新结果并返回结果。

下面是上述方法的实现:

## C++

```
// C++ program to find no of ways
// to swap bits of s1 so that
// bitwise OR of s1 and s2 changes
#include <iostream>
using namespace std;

// Function to find number of ways
int countWays(string s1, string s2, int n)
{

    int a, b, c, d;
    a = b = c = d = 0;

    // initialise result that store
    // No. of swaps required
    int result = 0;

    // Traverse both strings and check
    // the bits as explained
    for (int i = 0; i < n; i++) {
        if (s2[i] == '0') {
            if (s1[i] == '0') {
                c++;
            }
            else {
                d++;
            }
        }
        else {
            if (s1[i] == '0') {
                a++;
            }
            else {
                b++;
            }
        }
    }

    // calculate result
    result = a * d + b * c + c * d;

    return result;
}

// Driver code
int main()
{
    int n = 5;
    string s1 = "01011";
    string s2 = "11001";

    cout << countWays(s1, s2, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find no of ways
// to swap bits of s1 so that
// bitwise OR of s1 and s2 changes
import java.io.*;

class GFG {

// Function to find number of ways
static int countWays(String s1, String s2, int n)
{

    int a, b, c, d;
    a = b = c = d = 0;

    // initialise result that store
    // No. of swaps required
    int result = 0;

    // Traverse both strings and check
    // the bits as explained
    for (int i = 0; i < n; i++) {
        if (s2.charAt(i) == '0') {
            if (s1.charAt(i) == '0') {
                c++;
            }
            else {
                d++;
            }
        }
        else {
            if (s1.charAt(i) == '0') {
                a++;
            }
            else {
                b++;
            }
        }
    }

    // calculate result
    result = a * d + b * c + c * d;

    return result;
}

// Driver code

    public static void main (String[] args) {
        int n = 5;
    String s1 = "01011";
    String s2 = "11001";

    System.out.println(countWays(s1, s2, n));
    }
}
// This code is contributed by shs..
```

## 蟒蛇 3

```
# Python 3 program to find no of ways
# to swap bits of s1 so that
# bitwise OR of s1 and s2 changes

# Function to find number of ways
def countWays(s1, s2, n):
    a = b = c = d = 0

    # initialise result that store
    # No. of swaps required
    result = 0;

    # Traverse both strings and check
    # the bits as explained
    for i in range(0, n, 1):
        if (s2[i] == '0'):
            if (s1[i] == '0'):
                c += 1;

            else:
                d += 1
        else:
            if (s1[i] == '0'):
                a += 1

            else:
                b += 1

    # calculate result
    result = a * d + b * c + c * d

    return result

# Driver code
if __name__ == '__main__':
    n = 5
    s1 = "01011"
    s2 = "11001"

    print(countWays(s1, s2, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find no of ways
// to swap bits of s1 so that
// bitwise OR of s1 and s2 changes
using System;

class GFG {

// Function to find number of ways
static int countWays(string s1, string s2, int n)
{

    int a, b, c, d;
    a = b = c = d = 0;

    // initialise result that store
    // No. of swaps required
    int result = 0;

    // Traverse both strings and check
    // the bits as explained
    for (int i = 0; i < n; i++) {
        if (s2[i] == '0') {
            if (s1[i] == '0') {
                c++;
            }
            else {
                d++;
            }
        }
        else {
            if (s1[i] == '0') {
                a++;
            }
            else {
                b++;
            }
        }
    }

    // calculate result
    result = a * d + b * c + c * d;

    return result;
}

// Driver code

    public static void Main () {
        int n = 5;
    string s1 = "01011";
    string s2 = "11001";

    Console.WriteLine(countWays(s1, s2, n));
    }
}
// This code is contributed by shs..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find no of ways
// to swap bits of s1 so that
// bitwise OR of s1 and s2 changes

// Function to find number of ways
function countWays($s1, $s2, $n)
{
    $a = $b = $c = $d = 0;

    // initialise result that store
    // No. of swaps required
    $result = 0;

    // Traverse both strings and check
    // the bits as explained
    for ($i = 0; $i < $n; $i++)
    {
        if ($s2[$i] == '0')
        {
            if ($s1[$i] == '0')
            {
                $c++;
            }
            else
            {
                $d++;
            }
        }
        else
        {
            if ($s1[$i] == '0')
            {
                $a++;
            }
            else
            {
                $b++;
            }
        }
    }

    // calculate result
    $result = $a * $d + $b *
              $c + $c * $d;

    return $result;
}

// Driver code
$n = 5;
$s1 = "01011";
$s2 = "11001";
echo countWays($s1, $s2, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript program to find no of ways
// to swap bits of s1 so that
// bitwise OR of s1 and s2 changes
 // Function to find number of ways
function countWays(s1, s2 , n)
{

    var a, b, c, d;
    a = b = c = d = 0;

    // initialise result that store
    // No. of swaps required
    var result = 0;

    // Traverse both strings and check
    // the bits as explained
    for (i = 0; i < n; i++) {
        if (s2.charAt(i) == '0') {
            if (s1.charAt(i) == '0') {
                c++;
            }
            else {
                d++;
            }
        }
        else {
            if (s1.charAt(i) == '0') {
                a++;
            }
            else {
                b++;
            }
        }
    }

    // calculate result
    result = a * d + b * c + c * d;

    return result;
}

// Driver code
var n = 5;
var s1 = "01011";
var s2 = "11001";

document.write(countWays(s1, s2, n));

// This code is contributed by Princi Singh
</script>
```

**Output**

```
4
```

**时间复杂度:** O(N)

**辅助空间:** O(1)
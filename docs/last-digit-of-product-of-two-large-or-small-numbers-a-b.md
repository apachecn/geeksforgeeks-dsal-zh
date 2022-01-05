# 两个大数字或小数字乘积的最后一位数字(a * b)

> 原文:[https://www . geesforgeks . org/两个大数字或小数字乘积的最后一位数字-a-b/](https://www.geeksforgeeks.org/last-digit-of-product-of-two-large-or-small-numbers-a-b/)

给定两个或大或小的数字，任务是找到这两个数字乘积的最后一位数字。
**例:**

```
Input: a = 1234567891233789, b = 567891233156156
Output: 4

Input: a = 123, b = 456
Output: 8
```

**逼近:**一般来说，2 个数 a 和 b 相乘的最后一位是这两个数的 LSB 乘积的最后一位。
例如:a = 123，b = 456，
a * b 的最后一位
=的最后一位((a 的 LSB)*(b 的 LSB))
=的最后一位((3)*(6))
=的最后一位(18)
= 8
下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print last digit of product a * b
void lastDigit(string a, string b)
{
    int lastDig = (a[a.length() - 1] - '0')
                  * (b[b.length() - 1] - '0');
    cout << lastDig % 10;
}

// Driver code
int main()
{
    string a = "1234567891233", b = "1234567891233156";
    lastDigit(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class Solution {

    // Function to print last digit of product a * b
    public static void lastDigit(String a, String b)
    {
        int lastDig = (a.charAt(a.length() - 1) - '0')
                      * (b.charAt(b.length() - 1) - '0');
        System.out.println(lastDig % 10);
    }

    // Driver code
    public static void main(String[] args)
    {
        String a = "1234567891233", b = "1234567891233156";
        lastDigit(a, b);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to print the last digit
# of product a * b
def lastDigit(a, b):
    lastDig = ((int(a[len(a) - 1]) - int('0')) *
               (int(b[len(b) - 1]) - int('0')))
    print(lastDig % 10)

# Driver code
if __name__ == '__main__':
    a, b = "1234567891233", "1234567891233156"
    lastDigit(a, b)

# This code has been contributed
# by 29AjayKumar
```

## C#

```
// CSharp implementation of the above approach

using System;
class Solution {

    // Function to print last digit of product a * b
    public static void lastDigit(String a, String b)
    {
        int lastDig = (a[a.Length - 1] - '0')
                      * (b[b.Length - 1] - '0');

        Console.Write(lastDig % 10);
    }

    // Driver code
    public static void Main()
    {
        String a = "1234567891233", b = "1234567891233156";
        lastDigit(a, b);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to print last digit of product a * b
function lastDigit($a, $b)
{
    $lastDig = (ord($a[strlen($a) - 1]) - 48) *
               (ord($b[strlen($b) - 1]) - 48);
    echo $lastDig % 10;
}

// Driver code
$a = "1234567891233";
$b = "1234567891233156";
lastDigit($a, $b);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
  <script>
    // Javascript implementation of the above approach

    // Function to print last digit of product a * b
    function lastDigit(a, b) {
      var lastDig = (a[a.length - 1] - '0')
        * (b[b.length - 1] - '0');
      document.write(lastDig % 10);
    }

    // Driver code
    var a = "1234567891233", b = "1234567891233156";
    lastDigit(a, b);

// This code is contributed by rrrtnx.
  </script>
```

**Output:** 

```
8
```

**时间复杂度:** O(1)。
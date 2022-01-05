# 求 N 的大值 N % 4(余数为 4)

> 原文:[https://www . geesforgeks . org/find-n-4-n 大值 4 的余数/](https://www.geeksforgeeks.org/find-n-4-remainder-with-4-for-a-large-value-of-n/)

给定一个代表大整数的字符串 **str** ，任务是找到 **N % 4** 的结果。
**例:**

> **输入:** N = 81
> **输出:** 1
> **输入:**N = 46234624362346435768440
> **输出:** 0

**方法:**除以 4 的余数只依赖于一个数的最后 2 位数字，所以我们不除 N，而是只除 N 的最后两位数字，求余数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return s % n
int findMod4(string s, int n)
{

    // To store the number formed by
    // the last two digits
    int k;

    // If it contains a single digit
    if (n == 1)
        k = s[0] - '0';

    // Take last 2 digits
    else
        k = (s[n - 2] - '0') * 10
            + s[n - 1] - '0';

    return (k % 4);
}

// Driver code
int main()
{
    string s = "81";
    int n = s.length();
    cout << findMod4(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return s % n
static int findMod4(String s, int n)
{

    // To store the number formed by
    // the last two digits
    int k;

    // If it contains a single digit
    if (n == 1)
        k = s.charAt(0) - '0';

    // Take last 2 digits
    else
        k = (s.charAt(n - 2) - '0') * 10
            + s.charAt(n - 1) - '0';

    return (k % 4);
}

// Driver code
public static void main(String[] args)
{
    String s = "81";
    int n = s.length();
    System.out.println(findMod4(s, n));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return s % n
def findMod4(s, n):

    # To store the number formed by
    # the last two digits

    # If it contains a single digit
    if (n == 1):
        k = ord(s[0]) - ord('0')

    # Take last 2 digits
    else:
        k = ((ord(s[n - 2]) - ord('0')) * 10 +
              ord(s[n - 1]) - ord('0'))

    return (k % 4)

# Driver code
if __name__ == '__main__':
    s = "81"
    n = len(s)
    print(findMod4(s, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return s % n
static int findMod4(string s, int n)
{

    // To store the number formed by
    // the last two digits
    int k;

    // If it contains a single digit
    if (n == 1)
        k = s[0] - '0';

    // Take last 2 digits
    else
        k = (s[n - 2]- '0') * 10
            + s[n - 1] - '0';

    return (k % 4);
}

// Driver code
public static void Main()
{
    string s = "81";
    int n = s.Length;
    Console.WriteLine(findMod4(s, n));
}
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the approach
// Function to return s % n
function findMod4($s, $n)
{

    // To store the number formed by
    // the last two digits
    $k;

    // If it contains a single digit
    if ($n == 1)
        $k = $s[0] - '0';

    // Take last 2 digits
    else
        $k = ($s[$n - 2] - '0') * 10
            + $s[$n - 1] - '0';

    return ($k % 4);
}

// Driver code
{
    $s = "81";
    $n = strlen($s);
    echo(findMod4($s, $n));
}

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return s % n
function findMod4(s, n)
{

    // To store the number formed by
    // the last two digits
    var k=0;

    // If it contains a single digit
    if (n == 1)
        k = s[0] - '0';

    // Take last 2 digits
    else
        k = (s[n - 2] - '0') * 10
            + s[n - 1] - '0';

    return (k % 4);
}

// Driver code
var s = "81";
var n = s.length;
document.write(findMod4(s, n));

// This code is contributed by nood2000.
</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(1)
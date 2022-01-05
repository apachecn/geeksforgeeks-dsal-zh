# 检查号码是否只设置了第一位和最后一位|设置 2

> 原文:[https://www . geesforgeks . org/check-number-with-first-and-last-bits-set-2/](https://www.geeksforgeeks.org/check-whether-the-number-has-only-first-and-last-bits-set-set-2/)

给定一个正整数 n，检查 n 的二进制表示中是否只设置了第一位和最后一位。打印“是”或“否”。
**例:**

> 输入:9
> 输出:是
> (9)10 = (1001)2，只设置第一位和
> 最后一位。
> 输入:15
> 输出:否
> (15)10 = (1111)2，除了第一个和最后一个
> 之外，还有其他设置的位。

我们已经在这里讨论了一个解决方案。
在这篇文章中，讨论了一个更简单的解决方案。

## C++

```
// C++ to check whether the number has only
// first and last bits set
#include <bits/stdc++.h>
using namespace std;

// function to check whether the number has only
// first and last bits set
bool onlyFirstAndLastAreSet(unsigned int n)
{
    if (n == 1)
        return true;
    if (n == 2)
        return false;
    return (((n - 1) & (n - 2)) == 0);
}

// Driver program to test above
int main()
{
    unsigned int n = 9;
    if (onlyFirstAndLastAreSet(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java to check whether
// the number has only
// first and last bits set

class GFG
{
// function to check whether
// the number has only
// first and last bits set
static boolean onlyFirstAndLastAreSet(int n)
{
    if (n == 1)
        return true;
    if (n == 2)
        return false;
    return (((n - 1) &
             (n - 2)) == 0);
}

// Driver Code
public static void main(String[] args)
{
    int n = 9;
    if (onlyFirstAndLastAreSet(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed
// by Smitha
```

## 蟒蛇 3

```
# Python 3 to check whether
# the number has only
# first and last bits set

# function to check whether
# the number has only
# first and last bits set
def onlyFirstAndLastAreSet(n):

    if (n == 1):
        return True
    if (n == 2):
        return False

    return (((n - 1) &
             (n - 2)) == 0)

# Driver Code
n = 9
if (onlyFirstAndLastAreSet(n)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Smitha
```

## C#

```
// C# to check whether
// the number has only
// first and last bits set
using System;

class GFG
{
// function to check whether
// the number has only
// first and last bits set
static bool onlyFirstAndLastAreSet(int n)
{
    if (n == 1)
        return true;
    if (n == 2)
        return false;
    return (((n - 1) &
             (n - 2)) == 0);
}

// Driver Code
public static void Main()
{
    int n = 9;
    if (onlyFirstAndLastAreSet(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed
// by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP to check whether the
// number has only first and
// last bits set

// function to check whether
// the number has only first
// and last bits set
function onlyFirstAndLastAreSet($n)
{
    if ($n == 1)
        return true;
    if ($n == 2)
        return false;
    return ((($n - 1) &
             ($n - 2)) == 0);
}

// Driver Code
$n = 9;
if (onlyFirstAndLastAreSet($n))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Smitha
?>
```

## java 描述语言

```
<script>

// javascript to check whether
// the number has only
// first and last bits set

// function to check whether
// the number has only
// first and last bits set
function onlyFirstAndLastAreSet(n)
{
    if (n == 1)
        return true;
    if (n == 2)
        return false;
    return (((n - 1) &
             (n - 2)) == 0);
}

// Driver Code

var n = 9;
if (onlyFirstAndLastAreSet(n))
    document.write("Yes");
else
    document.write("No");

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
Yes
```
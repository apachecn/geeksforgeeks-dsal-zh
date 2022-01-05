# 检查字符串是否有 m 个连续的 1 或 0

> 原文:[https://www . geesforgeks . org/check-if-a-string-has-m-continuous-1s-or-0s/](https://www.geeksforgeeks.org/check-if-a-string-has-m-consecutive-1s-or-0s/)

给定二进制字符串和数字 m，任务是检查该字符串是否有 m 个连续的 1 或 0。

**示例:**

> **输入:** str = "001001 "，m = 2
> **输出:**是
> 
> **输入:** str = "1000000001 "，m = 10
> T3】输出:否

**方法**是通过遍历二进制字符串来计数连续的 1 或 0。遍历二进制字符串时，记录连续出现的 1 或 0 的数量。如果有 M 个连续的 1 或 0，返回**真**，否则返回**假**。

下面给出了上述方法的实现:

## C++

```
// Program to check if the binary string
// contains m consecutive 1's or 0's
#include <bits/stdc++.h>
#include <stdio.h>
using namespace std;

// Function that checks if
// the binary string contains m
// consecutive 1's or 0's
bool check(string s, int m)
{
    // length of binary string
    int l = s.length();

    // counts zeros
    int c1 = 0;

    // counts 1's
    int c2 = 0;

    for (int i = 0; i < l; i++) {

        if (s[i] == '0') {
            c2 = 0;

           // count consecutive 0's
            c1++;
        }
        else {
            c1 = 0;

            // count consecutive 1's
            c2++;
        }
        if (c1 == m || c2 == m)
            return true;
    }
    return false;
}

// Drivers Code
int main()
{
    string s = "001001";
    int m = 2;

    // function call
    if (check(s, m))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to check if the
// binary string contains
// m consecutive 1's or 0's
import java.io.*;

class GFG
{

// Function that checks if
// the binary string contains m
// consecutive 1's or 0's
static boolean check(String s,
                     int m)
{
    // length of binary string
    int l = s.length();

    // counts zeros
    int c1 = 0;

    // counts 1's
    int c2 = 0;

    for (int i = 0; i < l; i++)
    {

        if (s.charAt(i) == '0')
        {
            c2 = 0;

        // count consecutive 0's
            c1++;
        }
        else
        {
            c1 = 0;

            // count consecutive 1's
            c2++;
        }
        if (c1 == m || c2 == m)
            return true;
    }
    return false;
}

// Drivers Code

public static void main (String[] args)
{
    String s = "001001";
    int m = 2;

    // function call
    if (check(s, m))
        System.out.println( "YES");
    else
        System.out.println( "NO");
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Program to check if the binary string
# contains m consecutive 1's or 0's

# Function that checks if
# the binary string contains m
# consecutive 1's or 0's
def check(s, m):

    # length of binary string
    l = len(s);

    # counts zeros
    c1 = 0;

    # counts 1's
    c2 = 0;

    for i in range(0, l - 1):

        if (s[i] == '0'):
            c2 = 0;

        # count consecutive 0's
            c1 = c1 + 1;

        else :
            c1 = 0;

            # count consecutive 1's
            c2 = c2 + 1;

        if (c1 == m or c2 == m):
            return True;

    return False;

# Driver Code
s = "001001";
m = 2;

# function call
if (check(s, m)):
    print("YES");
else :
    print("NO");

# This code is contributed
# by Shivi_Agggarwal
```

## C#

```
// Program to check if the
// binary string contains
// m consecutive 1's or 0's
using System;

class GFG
{

// Function that checks if
// the binary string contains
// m consecutive 1's or 0's
static bool check(string s,
                  int m)
{
    // length of
    // binary string
    int l = s.Length;

    // counts zeros
    int c1 = 0;

    // counts 1's
    int c2 = 0;

    for (int i = 0; i < l; i++)
    {

        if (s[i] == '0')
        {
            c2 = 0;

            // count consecutive
            // 0's
            c1++;
        }
        else
        {
            c1 = 0;

            // count consecutive
            // 1's
            c2++;
        }
        if (c1 == m || c2 == m)
            return true;
    }
    return false;
}

// Driver Code
public static void Main ()
{
    String s = "001001";
    int m = 2;

    // function call
    if (check(s, m))
        Console.WriteLine( "YES");
    else
        Console.WriteLine( "NO");
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to check if the
// binary string contains m
// consecutive 1's or 0's

// Function that checks if
// the binary string contains
// m consecutive 1's or 0's
function check($s, $m)
{
    // length of binary
    // string
    $l = count($s);

    // counts zeros
    $c1 = 0;

    // counts 1's
    $c2 = 0;

    for ($i = 0; $i <= $l; $i++)
    {

        if ($s[$i] == '0')
        {
            $c2 = 0;

            // count consecutive
            // 0's
            $c1++;
        }
        else
        {
            $c1 = 0;

            // count consecutive 1's
            $c2++;
        }
        if ($c1 == $m or
            $c2 == $m)
            return true;
    }
    return false;
}

// Driver Code
$s = "001001";
$m = 2;

// function call
if (check($s, $m))
    echo "YES";
else
    echo "NO";

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Program to check if the
    // binary string contains
    // m consecutive 1's or 0's

    // Function that checks if
    // the binary string contains
    // m consecutive 1's or 0's
    function check(s, m)
    {
        // length of
        // binary string
        let l = s.length;

        // counts zeros
        let c1 = 0;

        // counts 1's
        let c2 = 0;

        for (let i = 0; i < l; i++)
        {

            if (s[i] == '0')
            {
                c2 = 0;

                // count consecutive
                // 0's
                c1++;
            }
            else
            {
                c1 = 0;

                // count consecutive
                // 1's
                c2++;
            }
            if (c1 == m || c2 == m)
                return true;
        }
        return false;
    }

    let s = "001001";
    let m = 2;

    // function call
    if (check(s, m))
        document.write( "YES");
    else
        document.write( "NO");

</script>
```

**Output :** 

```
YES
```

**时间复杂度:** O(N)，其中 N 为二进制字符串的长度。
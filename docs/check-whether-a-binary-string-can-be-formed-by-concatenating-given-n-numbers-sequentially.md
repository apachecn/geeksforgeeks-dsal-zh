# 检查一个二进制串是否可以由给定的 N 个数字顺序串接而成

> 原文:[https://www . geesforgeks . org/check-一个二进制字符串是否可以通过按顺序连接给定的 n 个数字来形成/](https://www.geeksforgeeks.org/check-whether-a-binary-string-can-be-formed-by-concatenating-given-n-numbers-sequentially/)

给定一个“n”个数字的序列(没有前导零)，任务是找出是否有可能通过按顺序连接这些数字来创建一个二进制字符串。
如果可能，则打印形成的二进制字符串，否则打印“-1”。
**例:**

> **输入:** arr[] = {10，11，1，0，10}
> **输出:** 10111010
> 所有数字只包含数字‘1’和‘0’。因此，可以通过将
> 这些数字按顺序串联起来形成一个二进制字符串，即 10111010。
> **输入:** arr[] = {1，2，11，10}
> **输出:** -1
> 其中一个数字包含数字“2”，该数字不能是任何二进制字符串的一部分。
> 所以，输出为-1。

**方法:**主要观察的是，我们只能连接那些只包含数字‘1’和‘0’的数字。否则，不可能形成二进制字符串。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns false if
// the number passed as argument contains
// digit(s) other than '0' or '1'
bool isBinary(int n)
{
    while (n != 0) {
        int temp = n % 10;
        if (temp != 0 && temp != 1) {
            return false;
        }
        n = n / 10;
    }
    return true;
}

//Function that checks whether the
//binary string can be formed or not
void formBinaryStr(int n, int a[])
{
    bool flag = true;

    // Empty string for storing
    // the binary number
    string s = "";

    for (int i = 0; i < n; i++) {

        // check if a[i] can be a
        // part of the binary string
        if (isBinary(a[i]))

            // Conversion of int into string
            s += to_string(a[i]);
        else {

            // if a[i] can't be a part
            // then break the loop
            flag = false;
            break;
        }
    }

    // possible to create binary string
    if (flag)
        cout << s << "\n";

    // impossible to create binary string
    else
        cout << "-1\n";
}

// Driver code
int main()
{

    int a[] = { 10, 1, 0, 11, 10 };
    int N = sizeof(a) / sizeof(a[0]);

    formBinaryStr(N, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  implementation of the approach
import java.util.*;
class Solution
{
// Function that returns false if
// the number passed as argument contains
// digit(s) other than '0' or '1'
static boolean isBinary(int n)
{
    while (n != 0) {
        int temp = n % 10;
        if (temp != 0 && temp != 1) {
            return false;
        }
        n = n / 10;
    }
    return true;
}

//Function that checks whether the
//binary String can be formed or not
static void formBinaryStr(int n, int a[])
{
    boolean flag = true;

    // Empty String for storing
    // the binary number
    String s = "";

    for (int i = 0; i < n; i++) {

        // check if a[i] can be a
        // part of the binary String
        if (isBinary(a[i]))

            // Conversion of int into String
            s += ""+a[i];
        else {

            // if a[i] can't be a part
            // then break the loop
            flag = false;
            break;
        }
    }

    // possible to create binary String
    if (flag)
        System.out.print( s + "\n");

    // impossible to create binary String
    else
        System.out.print( "-1\n");
}

// Driver code
public static void main(String args[])
{

    int a[] = { 10, 1, 0, 11, 10 };
    int N = a.length;

    formBinaryStr(N, a);
}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns false if the
# number passed as argument contains
# digit(s) other than '0' or '1'
def isBinary(n):

    while n != 0:
        temp = n % 10
        if temp != 0 and temp != 1:
            return False

        n = n // 10

    return True

# Function that checks whether the
# binary string can be formed or not
def formBinaryStr(n, a):

    flag = True

    # Empty string for storing
    # the binary number
    s = ""
    for i in range(0, n):

        # check if a[i] can be a
        # part of the binary string
        if isBinary(a[i]) == True:

            # Conversion of int into string
            s += str(a[i])

        else:
            # if a[i] can't be a part
            # then break the loop
            flag = False
            break

    # possible to create binary string
    if flag == True:
        print(s)

    # impossible to create binary string
    else:
        cout << "-1\n"

# Driver code
if __name__ == "__main__":

    a = [10, 1, 0, 11, 10]
    N = len(a)

    formBinaryStr(N, a)

# This code is contributed by Rituraj Jain
```

## C#

```
// C#  implementation of the approach
using System;

public class Solution
{
// Function that returns false if
// the number passed as argument contains
// digit(s) other than '0' or '1'
public static bool isBinary(int n)
{
    while (n != 0)
    {
        int temp = n % 10;
        if (temp != 0 && temp != 1)
        {
            return false;
        }
        n = n / 10;
    }
    return true;
}

//Function that checks whether the 
//binary String can be formed or not
public static void formBinaryStr(int n, int[] a)
{
    bool flag = true;

    // Empty String for storing
    // the binary number
    string s = "";

    for (int i = 0; i < n; i++)
    {

        // check if a[i] can be a
        // part of the binary String
        if (isBinary(a[i]))
        {

            // Conversion of int into String
            s += "" + a[i];
        }
        else
        {

            // if a[i] can't be a part
            // then break the loop
            flag = false;
            break;
        }
    }

    // possible to create binary String
    if (flag)
    {
        Console.Write(s + "\n");
    }

    // impossible to create binary String
    else
    {
        Console.Write("-1\n");
    }
}

// Driver code
public static void Main(string[] args)
{

    int[] a = new int[] {10, 1, 0, 11, 10};
    int N = a.Length;

    formBinaryStr(N, a);
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns false if the
// number passed as argument contains
// digit(s) other than '0' or '1'
function isBinary($n)
{
    while ($n != 0)
    {
        $temp = $n % 10;
        if ($temp != 0 && $temp != 1)
        {
            return false;
        }
        $n = intval($n / 10);
    }
    return true;
}

// Function that checks whether the
// binary string can be formed or not
function formBinaryStr($n, &$a)
{
    $flag = true;

    // Empty string for storing
    // the binary number
    $s = "";

    for ($i = 0; $i < $n; $i++)
    {

        // check if a[i] can be a
        // part of the binary string
        if (isBinary($a[$i]))

            // Conversion of int into string
            $s = $s.strval($a[$i]);
        else
        {

            // if a[i] can't be a part
            // then break the loop
            $flag = false;
            break;
        }
    }

    // possible to create binary string
    if ($flag)
        echo $s . "\n";

    // impossible to create binary string
    else
        echo "-1\n";
}

// Driver code
$a = array( 10, 1, 0, 11, 10 );
$N = sizeof($a) / sizeof($a[0]);

formBinaryStr($N, $a);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript  implementation of the approach

    // Function that returns false if
    // the number passed as argument contains
    // digit(s) other than '0' or '1'
    function isBinary(n)
    {
        while (n != 0) {
            var temp = n % 10;
            if (temp != 0 && temp != 1) {
                return false;
            }
            n = parseInt(n / 10);
        }
        return true;
    }

    // Function that checks whether the
    // binary String can be formed or not
    function formBinaryStr(n , a) {
        var flag = true;

        // Empty String for storing
        // the binary number
        var s = "";

        for (i = 0; i < n; i++) {

            // check if a[i] can be a
            // part of the binary String
            if (isBinary(a[i]))

                // Conversion of var into String
                s += "" + a[i];
            else {

                // if a[i] can't be a part
                // then break the loop
                flag = false;
                break;
            }
        }

        // possible to create binary String
        if (flag)
            document.write(s + "\n");

        // impossible to create binary String
        else
            document.write("-1\n");
    }

    // Driver code

        var a = [ 10, 1, 0, 11, 10 ];
        var N = a.length;

        formBinaryStr(N, a);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
10101110
```
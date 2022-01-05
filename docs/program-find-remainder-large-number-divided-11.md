# 当大数除以 11 时求余数的程序

> 原文:[https://www . geesforgeks . org/program-find-余数-大数-除数-11/](https://www.geeksforgeeks.org/program-find-remainder-large-number-divided-11/)

给定一个数 n，任务是当 n 除以 11 时求余数。数字的输入可能非常大。
示例:

```
Input : str = 13589234356546756
Output : 6

Input : str = 3435346456547566345436457867978
Output : 4
```

因为给定的数字可能非常大，所以我们不能使用 n % 11。需要使用一些步骤来查找余数:

```
1\. Store number in string.
2\. Count length of number string.
3\. Convert string character one by one 
into digit and check if it's less than
11\. Then continue for next character 
otherwise take remainder and use 
remainder for next number.
4\. We get remainder.

Ex. str = "1345"
    len = 4
    rem = 3
```

## C++

```
// CPP implementation to find remainder
// when a large number is divided by 11
#include <bits/stdc++.h>
using namespace std;

// Function to return remainder
int remainder(string str)
{
    // len is variable to store the
    // length of number string.
    int len = str.length();

    int num, rem = 0;

    // loop that find remainder
    for (int i = 0; i < len; i++) {
        num = rem * 10 + (str[i] - '0');
        rem = num % 11;
    }

    return rem;
}

// Driver code
int main()
{
    string str = "3435346456547566345436457867978";
    cout << remainder(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation to find remainder
// when a large number is divided by 11
import java.io.*;

class GFG{

    // Function to return remainder
    static int remainder(String str)
    {
        // len is variable to store the
        // length of number string.
        int len = str.length();

        int num, rem = 0;

        // loop that find remainder
        for (int i = 0; i < len; i++) {
            num = rem * 10 + (str.charAt(i) - '0');
            rem = num % 11;
        }

        return rem;
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "3435346456547566345436457867978";
        System.out.println(remainder(str));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 implementation to find remainder
# when a large number is divided by 11

# Function to return remainder
def remainder(st) :

    # len is variable to store the
    # length of number string.
    ln = len(st)

    rem = 0

    # loop that find remainder
    for i in range(0, ln) :
        num = rem * 10 + (int)(st[i])
        rem = num % 11

    return rem

# Driver code
st = "3435346456547566345436457867978"
print(remainder(st))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# implementation to find remainder
// when a large number is divided by 11
using System;

class GFG
{

    // Function to return remainder
    static int remainder(string str)
    {

        // len is variable to store the
        // length of number string.
        int len = str.Length;

        int num, rem = 0;

        // loop that find remainder
        for (int i = 0; i < len; i++)
        {
            num = rem * 10 + (str[i] - '0');
            rem = num % 11;
        }

        return rem;
    }

    // Driver code
    public static void Main()
    {
        string str = "3435346456547566345436457867978";
        Console.WriteLine(remainder(str));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find remainder
// when a large number is divided by 11

// Function to return remainder
function remainder($str)
{

    // len is variable to store the
    // length of number string.
    $len = strlen($str);

    $num; $rem = 0;

    // loop that find remainder
    for ($i = 0; $i < $len; $i++)
    {
        $num = $rem * 10 +
               ($str[$i] - '0');
        $rem = $num % 11;
    }

    return $rem;
}

// Driver code
$str = "3435346456547566345436457867978";
echo(remainder($str));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript implementation to find remainder
// when a large number is divided by 11

// Function to return remainder
function remainder(str)
{

    // len is variable to store the
    // length of number string.
    let len = str.length;

    let num;
    let rem = 0;

    // loop that find remainder
    for (let i = 0; i < len; i++)
    {
        num = rem * 10 +
               (str[i] - '0');
        rem = num % 11;
    }

    return rem;
}

// Driver code
let str = "3435346456547566345436457867978";
document.write(remainder(str));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
4
```

**时间复杂度:** O(L)，其中 L 是字符串的长度

**辅助空间:** O(L)
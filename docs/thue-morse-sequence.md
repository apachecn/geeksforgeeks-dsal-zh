# 图-莫尔斯序列

> 原文:[https://www.geeksforgeeks.org/thue-morse-sequence/](https://www.geeksforgeeks.org/thue-morse-sequence/)

[Thue–Morse 序列，或称普劳特–Thue–Morse 序列](https://en.wikipedia.org/wiki/Thue%E2%80%93Morse_sequence)，是一个由 0 和 1 组成的无限二进制序列。该序列是通过从 0 开始并连续追加到目前为止获得的序列的布尔补码而获得的。
前几步:

> 从 0 开始
> 追加补 0，我们得到 01
> 追加补 01，我们得到 0110
> 追加补 0110，我们得到 01101001

给定一个整数 **n** 。任务是找到由 Thue-Morse 序列构成的第 n 个字符串，即 Thue-Morse 序列的长度为 2 <sup>n-1</sup> 的前缀。
**例:**

```
Input : n = 4
Output : 01101001
We get 0, 01, 0110 and 01101001
in fourth iteration.

Input : n = 3
Output : 0110
```

其思想是用 0 初始化输出字符串，然后运行 n-1 次循环，每次迭代找到字符串的补码并将其附加到字符串中。
以下是该方法的实施:

## C++

```
// CPP Program to find nth term of Thue-Morse sequence.
#include <bits/stdc++.h>
using namespace std;

// Return the complement of the binary string.
string complement(string s)
{
    string comps;

    // finding the complement of the string.
    for (int i = 0; i < s.length(); i++) {

        // if character is 0, append 1
        if (s.at(i) == '0')
            comps += '1';

        // if character is 1, append 0.
        else
            comps += '0';
    }

    return comps;
}

// Return the nth term of Thue-Morse sequence.
string nthTerm(int n)
{
    // Initialing the string to 0
    string s = "0";

    // Running the loop for n - 1 time.
    for (int i = 1; i < n; i++)

        // appending the complement of
        // the string to the string.
        s += complement(s);

    return s;
}
// Driven Program
int main()
{
    int n = 4;
    cout << nthTerm(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find nth
// term of Thue-Morse sequence.

class GFG
{
    // Return the complement
    // of the binary String.
    static String complement(String s)
    {
        String comps = "";

        // finding the complement
        // of the String.
        for (int i = 0; i < s.length(); i++)
        {

            // if character is 0,
            // append 1
            if (s.charAt(i) == '0')
                comps += '1';

            // if character is 1,
            // append 0.
            else
                comps += '0';
        }

        return comps;
    }

    // Return the nth term
    // of Thue-Morse sequence.
    static String nthTerm(int n)
    {
        // Initialing the
        // String to 0
        String s = "0";

        // Running the loop
        // for n - 1 time.
        for (int i = 1; i < n; i++)

            // appending the complement of
            // the String to the String.
            s += complement(s);

        return s;
    }

    // Driven Code
public static void main(String[] args)
    {
        int n = 4;
        System.out.print(nthTerm(n));
    }
}

// This code is contributed by
// mits
```

## 蟒蛇 3

```
# Python3 Program to find nth term of
# Thue-Morse sequence.

# Return the complement of the
# binary string.
def complement(s):
    comps = "";

    # finding the complement
    # of the string.
    for i in range(len(s)):

        # if character is 0, append 1
        if (s[i] == '0'):
            comps += '1';

        # if character is 1, append 0.
        else:
            comps += '0';

    return comps;

# Return the nth term of
# Thue-Morse sequence.
def nthTerm(n):

    # Initialing the string to 0
    s = "0";

    # Running the loop for n - 1 time.
    for i in range(1, n):

        # appending the complement of
        # the string to the string.
        s += complement(s);

    return s;

# Driver Code
n = 4;
print(nthTerm(n));

# This code is contributed
# by mits
```

## C#

```
// C# Program to find nth
// term of Thue-Morse sequence.
using System;

class GFG
{
    // Return the complement
    // of the binary string.
    static string complement(string s)
    {
        string comps = "";

        // finding the complement
        // of the string.
        for (int i = 0; i < s.Length; i++)
        {

            // if character is 0,
            // append 1
            if (s[i] == '0')
                comps += '1';

            // if character is 1,
            // append 0.
            else
                comps += '0';
        }

        return comps;
    }

    // Return the nth term
    // of Thue-Morse sequence.
    static string nthTerm(int n)
    {
        // Initialing the
        // string to 0
        string s = "0";

        // Running the loop
        // for n - 1 time.
        for (int i = 1; i < n; i++)

            // appending the complement of
            // the string to the string.
            s += complement(s);

        return s;
    }

    // Driven Code
    static void Main()
    {
        int n = 4;
        Console.Write(nthTerm(n));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find nth
// term of Thue-Morse sequence.

// Return the complement
// of the binary string.
function complement($s)
{
    $comps = "";

    // finding the complement
    // of the string.
    for ($i = 0;
         $i < strlen($s); $i++)
    {

        // if character is
        // 0, append 1
        if ($s[$i] == '0')
            $comps .= '1';

        // if character is
        // 1, append 0.
        else
            $comps .= '0';
    }

    return $comps;
}

// Return the nth term
// of Thue-Morse sequence.
function nthTerm($n)
{
    // Initialing the
    // string to 0
    $s = "0";

    // Running the loop
    // for n - 1 time.
    for ($i = 1; $i < $n; $i++)

        // appending the complement of
        // the string to the string.
        $s .= complement($s);

    return $s;
}

// Driven Code
$n = 4;
echo nthTerm($n);

// This code is contributed
// by mits
?>
```

## C++

```
#include <iostream>
using namespace std;

int main() {

    cout<<"GFG!";
    return 0;
}
```

## java 描述语言

```
<script>

// JavaScript Program to find nth
// term of Thue-Morse sequence.

    // Return the complement
    // of the binary string.
    function complement(s)
    {
        let comps = "";

        // finding the complement
        // of the string.
        for (let i = 0; i < s.length; i++)
        {

            // if character is 0,
            // append 1
            if (s[i] == '0')
                comps += '1';

            // if character is 1,
            // append 0.
            else
                comps += '0';
        }

        return comps;
    }

    // Return the nth term
    // of Thue-Morse sequence.
    function nthTerm(n)
    {
        // Initialing the
        // string to 0
        let s = "0";

        // Running the loop
        // for n - 1 time.
        for (let i = 1; i < n; i++)

            // appending the complement of
            // the string to the string.
            s += complement(s);

        return s;
    }

// Driver program

        let n = 4;
        document.write(nthTerm(n));

        // This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
01101001
```
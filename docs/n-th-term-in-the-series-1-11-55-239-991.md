# 系列 1、11、55、239、991、…。

> 原文:[https://www . geesforgeks . org/n-th-系列术语-1-11-55-239-991/](https://www.geeksforgeeks.org/n-th-term-in-the-series-1-11-55-239-991/)

给定一个数字 N，任务是编写一个程序来寻找数列中的第 N 项:

> **1，11，55，239，991，…**

**示例** :

```
Input: N = 3
Output: 55

Input: N = 4 
Output: 239 
```

**方法-1:** 写下给定数字的二进制表示时，可以观察到一种模式。

> **1 = 1**
> **11 = 1011**
> **55 = 110111**
> **239 = 11101111**
> **。**
> **。**
> **。**

因此，对于 N = 1，答案永远是 1。对于第 N 项，二进制字符串将是 **(n-1)*1 + (0) + (n)*1** ，其被[转换为十进制值](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)以获得答案。
以下是上述方法的实施:

## C++

```
// C++ program to find the N-th term
// in 1, 11, 55, 239, 991, ....
#include <bits/stdc++.h>
using namespace std;

// Function to return the decimal value
// of a binary number
int binaryToDecimal(string n)
{
    string num = n;
    int dec_value = 0;

    // Initializing base value to 1, i.e 2^0
    int base = 1;

    int len = num.length();
    for (int i = len - 1; i >= 0; i--) {
        if (num[i] == '1')
            dec_value += base;
        base = base * 2;
    }

    return dec_value;
}

// find the binary representation
// of the N-th number in sequence
int numberSequence(int n)
{
    // base case
    if (n == 1)
        return 1;

    // answer string
    string s = "";

    // add n-1 1's
    for (int i = 1; i < n; i++)
        s += '1';

    // add 0
    s += '0';

    // add n 1's at end
    for (int i = 1; i <= n; i++)
        s += '1';

    int num = binaryToDecimal(s);

    return num;
}

// Driver Code
int main()
{
    int n = 4;

    cout << numberSequence(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the N-th
// term in 1, 11, 55, 239, 991, ....
import java.util.*;

class GFG
{

// Function to return the decimal
// value of a binary number
static int binaryToDecimal(String n)
{
    String num = n;
    int dec_value = 0;

    // Initializing base
    // value to 1, i.e 2^0
    int base = 1;

    int len = num.length();
    for (int i = len - 1; i >= 0; i--)
    {
        if (num.charAt(i) == '1')
            dec_value += base;
        base = base * 2;
    }

    return dec_value;
}

// find the binary representation
// of the N-th number in sequence
static int numberSequence(int n)
{
    // base case
    if (n == 1)
        return 1;

    // answer string
    String s = "";

    // add n-1 1's
    for (int i = 1; i < n; i++)
        s += '1';

    // add 0
    s += '0';

    // add n 1's at end
    for (int i = 1; i <= n; i++)
        s += '1';

    int num = binaryToDecimal(s);

    return num;
}

// Driver Code
public static void main(String args[])
{
    int n = 4;

    System.out.println(numberSequence(n));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to find the N-th term
# in 1, 11, 55, 239, 991, ....

# Function to return the decimal value
# of a binary number
def binaryToDecimal(n):

    num = n
    dec_value = 0

    # Initializing base value to 1, i.e 2^0
    base = 1

    l = len(num)
    for i in range(l - 1,-1, -1):
        if (num[i] == '1'):
            dec_value += base
        base = base * 2

    return dec_value

# find the binary representation
# of the N-th number in sequence
def numberSequence(n):

    # base case
    if (n == 1):
        return 1

    # answer string
    s = ""

    # add n-1 1's
    for i in range(1, n):
        s += '1'

    # add 0
    s += '0'

    # add n 1's at end
    for i in range(1,n+1):
        s += '1'

    num = binaryToDecimal(s)

    return num

# Driver Code
if __name__ == "__main__":

    n = 4

    print(numberSequence(n))

# this code is contributed by ChitraNayal
```

## C#

```
// C# program to find the N-th
// term in 1, 11, 55, 239, 991, ....
using System;

class GFG
{

// Function to return the decimal
// value of a binary number
static int binaryToDecimal(String n)
{
    String num = n;
    int dec_value = 0;

    // Initializing base
    // value to 1, i.e 2^0
    int base_ = 1;

    int len = num.Length;
    for (int i = len - 1; i >= 0; i--)
    {
        if (num[i] == '1')
            dec_value += base_;
        base_ = base_ * 2;
    }

    return dec_value;
}

// find the binary representation
// of the N-th number in sequence
static int numberSequence(int n)
{
    // base case
    if (n == 1)
        return 1;

    // answer string
    String s = "";

    // add n-1 1's
    for (int i = 1; i < n; i++)
        s += '1';

    // add 0
    s += '0';

    // add n 1's at end
    for (int i = 1; i <= n; i++)
        s += '1';

    int num = binaryToDecimal(s);

    return num;
}

// Driver Code
public static void Main()
{
    int n = 4;

    Console.WriteLine(numberSequence(n));
}
}

// This code is contributed
// by Subhadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the N-th term
// in 1, 11, 55, 239, 991, ....

// Function to return the decimal
// value of a binary number
function binaryToDecimal($n)
{
    $num = $n;
    $dec_value = 0;

    // Initializing base value
    // to 1, i.e 2^0
    $base = 1;

    $len = strlen($num);
    for ($i = $len - 1; $i >= 0; $i--)
    {
        if ($num[$i] == '1')
            $dec_value += $base;
        $base = $base * 2;
    }

    return $dec_value;
}

// find the binary representation
// of the N-th number in sequence
function numberSequence($n)
{
    // base case
    if ($n == 1)
        return 1;

    // answer string
    $s = "";

    // add n-1 1's
    for ($i = 1; $i < $n; $i++)
        $s .= '1';

    // add 0
    $s .= '0';

    // add n 1's at end
    for ($i = 1; $i <= $n; $i++)
        $s .= '1';

    $num = binaryToDecimal($s);

    return $num;
}

// Driver Code
$n = 4;

echo numberSequence($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find the N-th term
// in 1, 11, 55, 239, 991, ....

// Function to return the decimal value
// of a binary number
function binaryToDecimal(n)
{
    let num = n;
    let dec_value = 0;

    // Initializing base value to 1, i.e 2^0
    let base = 1;

    let len = num.length;
    for (let i = len - 1; i >= 0; i--) {
        if (num[i] == '1')
            dec_value += base;
        base = base * 2;
    }

    return dec_value;
}

// find the binary representation
// of the N-th number in sequence
function numberSequence(n)
{
    // base case
    if (n == 1)
        return 1;

    // answer string
    let s = "";

    // add n-1 1's
    for (let i = 1; i < n; i++)
        s += '1';

    // add 0
    s += '0';

    // add n 1's at end
    for (let i = 1; i <= n; i++)
        s += '1';

    let num = binaryToDecimal(s);

    return num;
}

// Driver Code
let n = 4;

document.write(numberSequence(n));

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
239
```

**逼近-2:** 级数有一个通式 **4 <sup>N</sup> -2 <sup>N</sup> -1** ，用来得到级数的第 N 项。
以下是上述方法的实施:

## C++

```
// C++ program to find the N-th term
// in 1, 11, 55, 239, 991, ....
#include <bits/stdc++.h>
using namespace std;

// Function to find the N-th term
int numberSequence(int n)
{
    // calculates the N-th term
    int num = pow(4, n) - pow(2, n) - 1;

    return num;
}

// Driver Code
int main()
{
    int n = 4;

    cout << numberSequence(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the N-th
// term in 1, 11, 55, 239, 991, ....
class GFG
{
// Function to find the N-th term
static int numberSequence(int n)
{
    // calculates the N-th term
    int num = (int)(Math.pow(4, n) -
                    Math.pow(2, n)) - 1;

    return num;
}

// Driver Code
public static void main(String args[])
{
    int n = 4;

    System.out.println(numberSequence(n));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to find N-th term
# in 1, 11, 55, 239, 991, ....

# calculate Nth term of series
def numberSequence(n) :

    # calculates the N-th term
    num = pow(4, n) - pow(2, n) - 1

    return num

# Driver Code
if __name__ == "__main__" :

    n = 4

    print(numberSequence(n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find the N-th
// term in 1, 11, 55, 239, 991, ....
using System;

class GFG
{
// Function to find the N-th term
static int numberSequence(int n)
{
    // calculates the N-th term
    int num = (int)(Math.Pow(4, n) -
                    Math.Pow(2, n)) - 1;

    return num;
}

// Driver Code
public static void Main()
{
    int n = 4;

    Console.WriteLine(numberSequence(n));
}
}

// This code is contributed
// by chandan_jnu.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the N-th term
// in 1, 11, 55, 239, 991, ....

// Function to find the N-th term
function numberSequence($n)
{
    // calculates the N-th term
    $num = pow(4, $n) -
           pow(2, $n) - 1;

    return $num;
}

// Driver Code
$n = 4;

echo numberSequence($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the N-th term
// in 1, 11, 55, 239, 991, ....

// Function to find the N-th term
function numberSequence(n)
{
    // calculates the N-th term
    let num = Math.pow(4, n) - Math.pow(2, n) - 1;

    return num;
}

// Driver Code
let n = 4;

document.write(numberSequence(n));

</script>
```

**Output:** 

```
239
```
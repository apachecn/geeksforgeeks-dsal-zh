# 最大偶数不大于 N

> 原文:[https://www . geesforgeks . org/最大偶数-数字-不大于-n/](https://www.geeksforgeeks.org/largest-even-digit-number-not-greater-n/)

给定一个数字 N，我们需要写一个程序来寻找最大的不大于 N 的数字，它的所有数字都是偶数。
**例:**

```
Input: N = 23
Output: 22 
Explanation: 22 is the largest number not 
greater then N which has all digits even. 

Input: N = 236
Output: 228 
Explanation: 228 is the largest number not 
greater than N which has all digits even. 
```

**天真法**:天真法是从 N 到 0 迭代，找到第一个所有数字都是偶数的数字。
以下是上述办法的实施情况:

## C++

```
// CPP program to print the largest
// integer not greater than N with all even digits
#include <bits/stdc++.h>
using namespace std;

// function to check if all digits
// are even of a given number
int checkDigits(int n)
{
    // iterate for all digits
    while (n) {
        if ((n % 10) % 2) // if digit is odd
            return 0;

        n /= 10;
    }

    // all digits are even
    return 1;
}

// function to return the largest number
// with all digits even
int largestNumber(int n)
{
    // iterate till we find a
    // number with all digits even
    for (int i = n;; i--)
        if (checkDigits(i))
            return i;
}

// Driver Code
int main()
{
    int N = 23;   
    cout << largestNumber(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the largest
// integer not greater than N with
// all even digits
import java .io.*;

public class GFG {

// function to check if all digits
// are even of a given number
static int checkDigits(int n)
{

    // iterate for all digits
    while (n > 0)
    {

        // if digit is odd
        if (((n % 10) % 2) > 0)
            return 0;

        n /= 10;
    }

    // all digits are even
    return 1;
}

// function to return the largest
// number with all digits even
static int largestNumber(int n)
{

    // iterate till we find a
    // number with all digits even
    for (int i = n;; i--)
        if (checkDigits(i) > 0)
            return i;
}

    // Driver Code
    static public void main (String[] args)
    {
        int N = 23;
        System.out.println(largestNumber(N));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to print the largest
# integer not greater than N with
# all even digits

# function to check if all digits
# are even of a given number
def checkDigits(n):

    # iterate for all digits
    while (n>0):
        # if digit is odd
        if ((n % 10) % 2):
            return False;

        n =int(n/10);

    # all digits are even
    return True;

# function to return the
# largest number with
# all digits even
def largestNumber(n):

    # Iterate till we find a
    # number with all digits even
    for i in range(n,-1,-1):
        if (checkDigits(i)):
            return i;

# Driver Code
N = 23;
print(largestNumber(N));

# This code is contributed by mits
```

## C#

```
// C# program to print the largest
// integer not greater than N with
// all even digits
using System;

public class GFG {

// function to check if all digits
// are even of a given number
static int checkDigits(int n)
{

    // iterate for all digits
    while (n > 0)
    {

        // if digit is odd
        if (((n % 10) % 2) > 0)
            return 0;

        n /= 10;
    }

    // all digits are even
    return 1;
}

// function to return the largest
// number with all digits even
static int largestNumber(int n)
{

    // iterate till we find a
    // number with all digits even
    for (int i = n;; i--)
        if (checkDigits(i) > 0)
            return i;
}

    // Driver Code
    static public void Main ()
    {
        int N = 23;
        Console.WriteLine(largestNumber(N));
    }
}

// This code is contributed by aunj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the largest
// integer not greater than N with
// all even digits

// function to check if all digits
// are even of a given number
function checkDigits($n)
{

    // iterate for all digits
    while ($n)
    {
        // if digit is odd
        if (($n % 10) % 2)
            return 0;

        $n /= 10;
    }

    // all digits are even
    return 1;
}

// function to return the
// largest number with
// all digits even
function largestNumber($n)
{

    // Iterate till we find a
    // number with all digits even
    for ($i = $n; ; $i--)
        if (checkDigits($i))
            return $i;
}

// Driver Code
$N = 23;
echo(largestNumber($N));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// javascript program to print the largest
// integer not greater than N with
// all even digits

// function to check if all digits
// are even of a given number
function checkDigits(n)
{

    // iterate for all digits
    while (n > 0)
    {

        // if digit is odd
        if (((n % 10) % 2) > 0)
            return 0;

        n = parseInt(n/ 10);
    }

    // all digits are even
    return 1;
}

// function to return the largest
// number with all digits even
function largestNumber(n)
{

    // iterate till we find a
    // number with all digits even
    for (i = n;; i--)
        if (checkDigits(i) > 0)
            return i;
}

// Driver Code
var N = 23;
document.write(largestNumber(N));

// This code is contributed by shikhasingrajput
</script>
```

**输出:**

```
22
```

**时间复杂度:** O(N)
**高效方法:**我们可以通过将 N 中的第一个奇数数字减 1，然后用最大的偶数数字(即 8)替换该奇数数字右侧的所有数字来获得所需的数字。例如，如果 N = 24578，那么 X = 24488。在某些情况下，这种方法可以创建一个前导 0，在这种情况下，我们可以简单地丢弃前导 0。例如，如果 N = 1334，那么 X = 0888。所以，我们的答案将是 X = 888。如果 N 中没有奇数，那么 N 就是数字本身。
以下是上述方法的实施:

## C++

```
// CPP program to print the largest
// integer not greater than N with all even digits
#include <bits/stdc++.h>
using namespace std;

// function to return the largest number
// with all digits even
int largestNumber(int n)
{
    string s = "";
    int duplicate = n;

    // convert the number to a string for
    // easy operations
    while (n) {
        s = char(n % 10 + 48) + s;
        n /= 10;
    }

    int index = -1;

    // find first odd digit
    for (int i = 0; i < s.length(); i++) {
        if ((s[i] - '0') % 2 & 1) {
            index = i;
            break;
        }
    }

    // if no digit, then N is the answer
    if (index == -1)
        return duplicate;

    int num = 0;

    // till first odd digit, add all even numbers
    for (int i = 0; i < index; i++)
        num = num * 10 + (s[i] - '0');

    // decrease 1 from the odd digit
    num = num * 10 + (s[index] - '0' - 1);

    // add 0 in the rest of the digits
    for (int i = index + 1; i < s.length(); i++)
        num = num * 10 + 8;

    return num;
}

// Driver Code
int main()
{
    int N = 24578;

    cout << largestNumber(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the largest
// integer not greater than N with all even digits
class GFG
{

// function to return the largest number
// with all digits even
static int largestNumber(int n)
{
    String s = "";
    int duplicate = n;

    // convert the number to a string for
    // easy operations
    while (n > 0)
    {
        s = (char)(n % 10 + 48) + s;
        n /= 10;
    }

    int index = -1;

    // find first odd digit
    for (int i = 0; i < s.length(); i++)
    {
        if ((((int)(s.charAt(i) - '0') % 2) & 1) > 0)
        {
            index = i;
            break;
        }
    }

    // if no digit, then N is the answer
    if (index == -1)
        return duplicate;

    int num = 0;

    // till first odd digit, add all even numbers
    for (int i = 0; i < index; i++)
        num = num * 10 + (int)(s.charAt(i) - '0');

    // decrease 1 from the odd digit
    num = num * 10 + ((int)s.charAt(index) - (int)('0') - 1);

    // add 0 in the rest of the digits
    for (int i = index + 1; i < s.length(); i++)
        num = num * 10 + 8;

    return num;
}

// Driver Code
public static void main (String[] args)
{
    int N = 24578;

    System.out.println(largestNumber(N));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to print the largest
# integer not greater than N with
# all even digits
import math as mt

# function to return the largest
# number with all digits even
def largestNumber(n):

    s = ""
    duplicate = n

    # convert the number to a string
    # for easy operations
    while (n > 0):
        s = chr(n % 10 + 48) + s
        n = n // 10

    index = -1

    # find first odd digit
    for i in range(len(s)):
        if ((ord(s[i]) - ord('0')) % 2 & 1):
            index = i
            break

    # if no digit, then N is the answer
    if (index == -1):
        return duplicate

    num = 0

    # till first odd digit, add all
    # even numbers
    for i in range(index):
        num = num * 10 + (ord(s[i]) - ord('0'))

    # decrease 1 from the odd digit
    num = num * 10 + (ord(s[index]) -  
                      ord('0') - 1)

    # add 0 in the rest of the digits
    for i in range(index+1,len(s)):
        num = num * 10 + 8

    return num

# Driver Code
N = 24578

print(largestNumber(N))

# This code is contributed
# by Mohit kumar 29

```

## C#

```
// C# program to print the largest
// integer not greater than N with all even digits
using System;

class GFG
{

// function to return the largest number
// with all digits even
static int largestNumber(int n)
{
    string s = "";
    int duplicate = n;

    // convert the number to a string for
    // easy operations
    while (n > 0)
    {
        s = (char)(n % 10 + 48) + s;
        n /= 10;
    }

    int index = -1;

    // find first odd digit
    for (int i = 0; i < s.Length; i++)
    {
        if ((((int)(s[i] - '0') % 2) & 1) > 0)
        {
            index = i;
            break;
        }
    }

    // if no digit, then N is the answer
    if (index == -1)
        return duplicate;

    int num = 0;

    // till first odd digit, add all even numbers
    for (int i = 0; i < index; i++)
        num = num * 10 + (int)(s[i] - '0');

    // decrease 1 from the odd digit
    num = num * 10 + ((int)s[index] - (int)('0') - 1);

    // add 0 in the rest of the digits
    for (int i = index + 1; i < s.Length; i++)
        num = num * 10 + 8;

    return num;
}

// Driver Code
static void Main()
{
    int N = 24578;

    Console.WriteLine(largestNumber(N));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the largest
// integer not greater than N with all even digits

// function to return the largest number
// with all digits even
function largestNumber($n)
{
    $s = "";
    $duplicate = $n;

    // convert the number to a string for
    // easy operations
    while ($n)
    {
        $s = chr($n % 10 + 48).$s;
        $n =(int)($n/10);
    }

    $index = -1;

    // find first odd digit
    for ($i = 0; $i < strlen($s); $i++)
    {
        if (ord($s[$i] - '0') % 2 & 1)
        {
            $index = $i;
            break;
        }
    }

    // if no digit, then N is the answer
    if ($index == -1)
        return $duplicate;

    $num = 0;

    // till first odd digit, add all even numbers
    for ($i = 0; $i < $index; $i++)
        $num = $num * 10 + (ord($s[$i]) - ord('0'));

    // decrease 1 from the odd digit
    $num = $num * 10 + ((ord($s[$i]) - ord('0')) - 1);

    // add 0 in the rest of the digits
    for ($i = $index + 1; $i < strlen($s); $i++)
        $num = $num * 10 + 8;

    return $num;
}

// Driver Code
    $N = 24578;

    echo largestNumber($N);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to print the largest
// integer not greater than N with all even digits

// function to return the largest number
// with all digits even
function largestNumber(n)
{
    var s = "";
    var duplicate = n;

    // convert the number to a string for
    // easy operations
    while (n > 0)
    {
        s = String.fromCharCode(n % 10 + 48) + s;
        n = parseInt(n/10);
    }

    var index = -1;

    // find first odd digit
    for (i = 0; i < s.length; i++)
    {
        if ((((s.charAt(i).charCodeAt(0) - '0'.charCodeAt(0)) % 2) & 1) > 0)
        {
            index = i;
            break;
        }
    }

    // if no digit, then N is the answer
    if (index == -1)
        return duplicate;

    var num = 0;

    // till first odd digit, add all even numbers
    for (i = 0; i < index; i++)
        num = num * 10 + (s.charAt(i).charCodeAt(0) - '0'.charCodeAt(0));

    // decrease 1 from the odd digit
    num = num * 10 + (s.charAt(index).charCodeAt(0) - ('0').charCodeAt(0) - 1);

    // add 0 in the rest of the digits
    for (i = index + 1; i < s.length; i++)
        num = num * 10 + 8;

    return num;
}

// Driver Code
var N = 24578;

document.write(largestNumber(N));

// This code contributed by shikhasingrajput
</script>
```

**输出:**

```
24488
```

**时间复杂度:** O(M)，其中 M 为位数
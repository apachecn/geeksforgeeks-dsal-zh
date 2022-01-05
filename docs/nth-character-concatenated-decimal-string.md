# 串联十进制字符串中的第 n 个字符

> 原文:[https://www . geeksforgeeks . org/n-字符连接-十进制-字符串/](https://www.geeksforgeeks.org/nth-character-concatenated-decimal-string/)

如果所有的十进制数都连接在一个字符串中，那么我们将得到一个看起来像字符串 P 的字符串，如下所示。我们需要告诉这个字符串的第 n 个字符。
P = " 12345678910111213141516171819202122232425262728293031…"

**示例:**

```
N = 10    10th character is 1
N = 11    11th character is 0
N = 50    50th character is 3
N = 190    190th character is 1
```

我们可以通过按长度断开字符串来解决这个问题。我们知道在十进制中，9 个数字的长度是 1，90 个数字的长度是 2，900 个数字的长度是 3，以此类推，所以我们可以根据给定的 N 跳过这些数字，就可以得到想要的字符。

```
Processing for N = 190 is explained below,
P[184..195] = “979899100101” 
First getting length of number at N,
190 – 9 = 181        number length is more than 1
181 – 90*2 = 1       number length is more than 2
1 – 900*3 < 0        number length is 3
Now getting actual character at N,
1 character after maximum 2 length number(99) is,  1

Processing for N = 251 is explained below,
P[250..255] = “120121”
First getting length of number at N,
251 - 9 = 242             number length is more than 1
242 – 90*2 = 62           number length is more than 2
62 – 900*3 < 0            number length is 3
Now getting actual character at N,
62 characters after maximum 2 length number(99) is,
Ceil(62/3) = 21,  99 + 21 = 120 
120 is the number at N, now getting actual digit,
62%3 = 2,
2nd digit of 120 is 2, so our answer will be 2 only.
```

请参见下面的代码，以便更好地理解，

## C++

```
// C++ program to get Nth character in
// concatenated Decimal String
#include <bits/stdc++.h>
using namespace std;

// Utility method to get dth digit of number N
char getDigit(int N, int d)
{
    string str;
    stringstream ss;
    ss << N;
    ss >> str;
    return str[d - 1];
}

// Method to return Nth character in concatenated
// decimal string
char getNthChar(int N)
{
    // sum will store character escaped till now
    int sum = 0, nine = 9;

    // dist will store numbers escaped till now
    int dist = 0, len;

    // loop for number lengths
    for (len = 1; ; len++)
    {
        // nine*len will be incremented characters
        // and nine will be incremented numbers
        sum += nine*len;
        dist += nine;

        if (sum >= N)
        {
            // restore variables to previous correct state
            sum -= nine*len;
            dist -= nine;
            N -= sum;
            break;
        }
        nine *= 10;
    }

    // get distance from last one digit less maximum
    // number
    int diff = ceil((double)N / len);

    // d will store dth digit of current number
    int d = N % len;
    if (d == 0)
        d = len;

    // method will return dth numbered digit
    // of (dist + diff) number
    return getDigit(dist + diff, d);
}

// Driver code to test above methods
int main()
{
    int N = 251;
    cout << getNthChar(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get Nth character in
// concatenated Decimal String

class GFG
{

// Utility method to get dth digit of number N
static char getDigit(int N, int d)
{
    String str=Integer.toString(N);
    return str.charAt(d - 1);
}

// Method to return Nth character in concatenated
// decimal string
static char getNthChar(int N)
{
    // sum will store character escaped till now
    int sum = 0, nine = 9;

    // dist will store numbers escaped till now
    int dist = 0, len;

    // loop for number lengths
    for (len = 1; ; len++)
    {
        // nine*len will be incremented characters
        // and nine will be incremented numbers
        sum += nine * len;
        dist += nine;

        if (sum >= N)
        {
            // restore variables to previous correct state
            sum -= nine * len;
            dist -= nine;
            N -= sum;
            break;
        }
        nine *= 10;
    }

    // get distance from last one digit
    // less maximum number
    int diff = (int)(Math.ceil((double)(N) / (double)(len)));

    // d will store dth digit of current number
    int d = N % len;
    if (d == 0)
        d = len;

    // method will return dth numbered digit
    // of (dist + diff) number
    return getDigit(dist + diff, d);
}

// Driver code
public static void main (String[] args)
{
    int N = 251;
    System.out.println(getNthChar(N));
}
}

// This code is contributed by mits
```

## 计算机编程语言

```
# Python program to get Nth character in
# concatenated Decimal String

# Method to get dth digit of number N
def getDigit(N, d):
    string = str(N)
    return string[d-1];

# Method to return Nth character in concatenated
# decimal string
def getNthChar(N):

    #  sum will store character escaped till now
    sum = 0
    nine = 9

    #  dist will store numbers escaped till now
    dist = 0

    #  loop for number lengths
    for len in range(1,N):

        # nine*len will be incremented characters
        # and nine will be incremented numbers
        sum += nine*len
        dist += nine
        if (sum >= N):

            #  restore variables to previous correct state
            sum -= nine*len
            dist -= nine
            N -= sum
            break

        nine *= 10

    # get distance from last one digit less maximum
    # number
    diff = (N / len) + 1

    # d will store dth digit of current number
    d = N % len
    if (d == 0):
        d = len

    # method will return dth numbered digit
    # of (dist + diff) number
    return getDigit(dist + diff, d);

#  Driver code to test above methods
N = 251
print getNthChar(N)

# Contributed by Afzal_Saan
```

## C#

```
// C# program to get Nth character in
// concatenated Decimal String
using System;

class GFG
{

// Utility method to get dth digit of number N
static char getDigit(int N, int d)
{
    string str = Convert.ToString(N);
    return str[d - 1];
}

// Method to return Nth character in
// concatenated decimal string
static char getNthChar(int N)
{
    // sum will store character
    // escaped till now
    int sum = 0, nine = 9;

    // dist will store numbers
    // escaped till now
    int dist = 0, len;

    // loop for number lengths
    for (len = 1; ; len++)
    {
        // nine*len will be incremented characters
        // and nine will be incremented numbers
        sum += nine * len;
        dist += nine;

        if (sum >= N)
        {
            // restore variables to previous
            // correct state
            sum -= nine * len;
            dist -= nine;
            N -= sum;
            break;
        }
        nine *= 10;
    }

    // get distance from last one digit
    // less maximum number
    int diff = (int)(Math.Ceiling((double)(N) /
                                  (double)(len)));

    // d will store dth digit of
    // current number
    int d = N % len;
    if (d == 0)
        d = len;

    // method will return dth numbered
    // digit of (dist + diff) number
    return getDigit(dist + diff, d);
}

// Driver code
static void Main()
{
    int N = 251;
    Console.WriteLine(getNthChar(N));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get Nth character
// in concatenated Decimal String

// Method to get dth digit
// of number N
function getDigit($N, $d)
{
    $string = strval($N);
    return $string[$d - 1];
}

// Method to return Nth character
// in concatenated decimal string
function getNthChar($N)
{
    // sum will store character
    // escaped till now
    $sum = 0;
    $nine = 9;

    // dist will store numbers
    // escaped till now
    $dist = 0;

    // loop for number lengths
    for($len = 1; $len < $N; $len++)
    {

        // nine*len will be incremented characters
        // and nine will be incremented numbers
        $sum += $nine * $len;
        $dist += $nine;
        if ($sum >= $N)
        {
            // restore variables to
            // previous correct state
            $sum -= $nine * $len;
            $dist -= $nine;
            $N -= $sum;
            break;
        }
        $nine *= 10;
    }

    // get distance from last one
    // digit less maximum number
    $diff = ($N / $len) + 1;

    // d will store dth digit
    // of current number
    $d = $N % $len;
    if ($d == 0)
        $d = $len;

    // method will return dth numbered
    // digit of (dist + diff) number
    return getDigit($dist + $diff, $d);
}

// Driver code
$N = 251;
echo getNthChar($N);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to get Nth
// character in concatenated
// Decimal String

// Utility method to get dth
// digit of number N
function getDigit(N, d)
{
    let str = N.toString();
    return str[d - 1];
}

// Method to return Nth character in
// concatenated decimal string
function getNthChar(N)
{

    // Sum will store character
    // escaped till now
    let sum = 0, nine = 9;

    // dist will store numbers
    // escaped till now
    let dist = 0, len;

    // Loop for number lengths
    for(len = 1; ; len++)
    {

        // nine*len will be incremented
        // characters and nine will be
        // incremented numbers
        sum += nine * len;
        dist += nine;

        if (sum >= N)
        {

            // Restore variables to
            // previous correct state
            sum -= nine * len;
            dist -= nine;
            N -= sum;
            break;
        }
        nine *= 10;
    }

    // Get distance from last one digit
    // less maximum number
    let diff = (Math.ceil((N) / (len)));

    // d will store dth digit
    // of current number
    let d = N % len;

    if (d == 0)
        d = len;

    // Method will return dth numbered digit
    // of (dist + diff) number
    return getDigit(dist + diff, d);
}

// Driver Code
let N = 251;

document.write(getNthChar(N));

// This code is contributed by code_hunt

</script>
```

**输出:**

```
2
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
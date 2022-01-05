# 最小偶数位数不小于 N

> 原文:[https://www . geesforgeks . org/最小-偶数-数字-不小于-n/](https://www.geeksforgeeks.org/smallest-even-digits-number-not-less-than-n/)

给定一个数字 N，我们需要编写一个程序来寻找不小于 N 的最小数字，它的所有数字都是偶数。
**例:**

```
Input: N = 1345  
Output: 2000
Explanation: 2000 is the smallest number not 
less than N, whose all digits are even. 

Input : N = 2397 
Output : 2400 
Explanation: 2400 is the smallest number not 
less than N, whose all digits are even.
```

**天真的方法**:天真的方法是从 N 开始不断迭代，直到我们找到一个所有数字都是偶数的数字。
以下是上述办法的实施:

## C++

```
// CPP program to print the smallest
// integer not less than N with all even digits
#include <bits/stdc++.h>
using namespace std;

// function to check if all digits
// are even of a given number
int check_digits(int n)
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

// function to return the smallest number
// with all digits even
int smallest_number(int n)
{
    // iterate till we find a
    // number with all digits even
    for (int i = n;; i++)
        if (check_digits(i))
            return i;
}

// Driver Code
int main()
{
    int N = 2397;
    cout << smallest_number(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the smallest
// integer not less than N with all
// even digits
class GFG {

    // function to check if all digits
    // are even of a given number
    static int check_digits(int n)
    {

        // iterate for all digits
        while (n != 0) {

            // if digit is odd
            if ((n % 10) % 2 != 0)
                return 0;

            n /= 10;
        }

        // all digits are even
        return 1;
    }

    // function to return the smallest
    // number with all digits even
    static int smallest_number(int n)
    {

        // iterate till we find a
        // number with all digits even
        for (int i = n; ; i++)
            if (check_digits(i) != 0)
                return i;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 2397;

        System.out.println(smallest_number(N));
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 program to print the smallest
# integer not less than N with
# all even digits

# function to check if all digits
# are even of a given number
def check_digits(n) :

    # iterate for all digits
    while (n) :

        # if digit is odd
        if ((n % 10) % 2) :
            return 0

        n = int(n / 10)

    # all digits are even
    return 1

# function to return the
# smallest number with
# all digits even
def smallest_number(n) :

    # iterate till we find a
    # number with all digits even
    for i in range(n, 2401) :
        if (check_digits(i) == 1) :
            return (i)

# Driver Code
N = 2397
print (str(smallest_number(N)))

# This code is contributed by
# Manish Shaw (manishshaw1)
```

## C#

```
// C# program to print the smallest
// integer not less than N with all
// even digits
using System;
class GFG {

    // function to check if all digits
    // are even of a given number
    static int check_digits(int n)
    {

        // iterate for all digits
        while (n != 0) {

            // if digit is odd
            if ((n % 10) % 2 != 0)
                return 0;

            n /= 10;
        }

        // all digits are even
        return 1;
    }

    // function to return the smallest
    // number with all digits even
    static int smallest_number(int n)
    {

        // iterate till we find a
        // number with all digits even
        for (int i = n; ; i++)
            if (check_digits(i) != 0)
                return i;
    }

    // Driver Code
    public static void Main()
    {
        int N = 2397;

    Console.WriteLine(smallest_number(N));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the smallest
// integer not less than N with
// all even digits

// function to check if all digits
// are even of a given number
function check_digits($n)
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
// smallest number with
// all digits even
function smallest_number( $n)
{

    // iterate till we find a
    // number with all digits even
    for ($i = $n; ; $i++)
        if (check_digits($i))
            return $i;
}

    // Driver Code
    $N = 2397;
    echo smallest_number($N);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// Javascript program to prvar the smallest
// integer not less than N with all
// even digits

// function to check if all digits
// are even of a given number
function check_digits(n)
{

    // iterate for all digits
    while (n != 0) {

        // if digit is odd
        if ((n % 10) % 2 != 0)
            return 0;

        n = parseInt(n/10);
    }

    // all digits are even
    return 1;
}

// function to return the smallest
// number with all digits even
function smallest_number(n)
{

    // iterate till we find a
    // number with all digits even
    for (i = n; ; i++)
        if (check_digits(i) != 0)
            return i;
}

// Driver Code
var N = 2397;

document.write(smallest_number(N));

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
2400
```

**时间复杂度:** O(N)
**高效方法:**我们可以通过将 N 中的第一个奇数数字增加 1，并用最小的偶数数字(即 0)替换该奇数数字右侧的所有数字来找到该数字。如果 N 中没有奇数，那么 N 本身就是最小的数。例如，考虑 N = 213。递增 N 中的第一个奇数位，即 1 到 2，并用 0 替换它右边的所有数字。所以，我们需要的号码是 220。
**棘手案例:**

*   如果 N 中的第一个奇数是 9，那么我们必须用下一个偶数替换那个奇数左边的数字。例如，如果 N=44934，那么最小的数=46000。
*   另一个棘手的情况是，第一个奇数位是 9，第一个奇数位左边的数字是 8。在这种情况下，我们必须用 0 直接替换第一个奇数左边的数字，用下一个偶数替换这个数字左边的数字，并一直这样做，直到找到 8 以外的数字。例如，如果 N=86891，那么 Y=88000。最后，如果左边的所有数字继续是 8，直到我们到达最左边的数字，或者如果 N 的第一个数字是 9，那么我们必须添加最小的非零偶数(即 2)作为左边的新数字。例如，如果 N=891 或 N=910，那么 Y=2000。

下面是高效方法的实现:

## C++

```
// CPP program to print the smallest
// integer not less than N with all even digits
#include <bits/stdc++.h>
using namespace std;

// function to return the answer when the
// first odd digit is 9
int trickyCase(string s, int index)
{

    int index1 = -1;

    // traverse towwars the left to find the non-8 digit
    for (int i = index - 1; i >= 0; i--) {
        // index digit
        int digit = s[i] - '0';

        // if digit is not 8, then break
        if (digit != 8) {
            index1 = i;
            break;
        }
    }
    // if on the left side of the '9', no 8
    // is found then we return by adding a 2 and 0's
    if (index1 == -1)
        return 2 * pow(10, s.length());

    int num = 0;

    // till non-8 digit add all numbers
    for (int i = 0; i < index1; i++)
        num = num * 10 + (s[i] - '0');

    // if non-8 is even or odd than add the next even.
    if (s[index1] % 2 == 0)
        num = num * 10 + (s[index1] - '0' + 2);
    else
        num = num * 10 + (s[index1] - '0' + 1);

    // add 0 to right of 9
    for (int i = index1 + 1; i < s.length(); i++)
        num = num * 10;

    return num;
}

// function to return the smallest number
// with all digits even
int smallestNumber(int n)
{
    int num = 0;
    string s = "";

    int duplicate = n;
    // convert the number to string to
    // perform operations
    while (n) {
        s = char(n % 10 + 48) + s;
        n /= 10;
    }

    int index = -1;

    // find out the first odd number
    for (int i = 0; i < s.length(); i++) {
        int digit = s[i] - '0';
        if (digit & 1) {
            index = i;
            break;
        }
    }

    // if no odd numbers are there, than n is the answer
    if (index == -1)
        return duplicate;

    // if the odd number is 9,
    // than tricky case handles it
    if (s[index] == '9') {
        num = trickyCase(s, index);
        return num;
    }

    // add all digits till first odd
    for (int i = 0; i < index; i++)
        num = num * 10 + (s[i] - '0');

    // increase the odd digit by 1
    num = num * 10 + (s[index] - '0' + 1);

    // add 0 to the right of the odd number
    for (int i = index + 1; i < s.length(); i++)
        num = num * 10;

    return num;
}

// Driver Code
int main()
{
    int N = 2397;
    cout << smallestNumber(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// smallest integer not less
// than N with all even digits
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{
// function to return
// the answer when the
// first odd digit is 9
static int trickyCase(String s,
                      int index)
{

    int index1 = -1;

    // traverse towwars the left
    // to find the non-8 digit
    for (int i = index - 1; i >= 0; i--)
    {
        // index digit
        int digit = s.charAt(i) - '0';

        // if digit is not 8,
        // then break
        if (digit != 8)
        {
            index1 = i;
            break;
        }
    }

    // if on the left side of the
    // '9', no 8 is found then we
    // return by adding a 2 and 0's
    if (index1 == -1)
        return 2 * (int)Math.pow(10, s.length());

    int num = 0;

    // till non-8 digit
    // add all numbers
    for (int i = 0; i < index1; i++)
        num = num * 10 + (s.charAt(i) - '0');

    // if non-8 is even or odd
    // than add the next even.
    if (s.charAt(index1) % 2 == 0)
        num = num * 10 +
            (s.charAt(index1) - '0' + 2);
    else
        num = num * 10 +
            (s.charAt(index1) - '0' + 1);

    // add 0 to right of 9
    for (int i = index1 + 1;
            i < s.length(); i++)
        num = num * 10;

    return num;
}

// function to return
// the smallest number
// with all digits even
static int smallestNumber(int n)
{
    int num = 0;
    String s = "";

    int duplicate = n;

    // convert the number to
    // string to perform operations
    while (n > 0)
    {
        s = (char)(n % 10 + 48) + s;
        n /= 10;
    }

    int index = -1;

    // find out the
    // first odd number
    for (int i = 0; i < s.length(); i++)
    {
        int digit = s.charAt(i) - '0';
        int val = digit & 1;
        if (val == 1)
        {
            index = i;
            break;
        }
    }

    // if no odd numbers are there,
    // than n is the answer
    if (index == -1)
        return duplicate;

    // if the odd number is 9,
    // than tricky case handles it
    if (s.charAt(index) == '9')
    {
        num = trickyCase(s, index);
        return num;
    }

    // add all digits till first odd
    for (int i = 0; i < index; i++)
        num = num * 10 +
             (s.charAt(i) - '0');

    // increase the
    // odd digit by 1
    num = num * 10 +
        (s.charAt(index) - '0' + 1);

    // add 0 to the right
    // of the odd number
    for (int i = index + 1;
             i < s.length(); i++)
        num = num * 10;

    return num;
}

// Driver Code
public static void main(String args[])
{
    int N = 2397;
    System.out.print(smallestNumber(N));
}
}

// This code is contributed
// by Akanksha rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 program to print the smallest
# integer not less than N with all even digits

# Function to return the answer when the
# first odd digit is 9
def trickyCase(s, index):
    index1 = -1;

    # traverse towwars the left to find
    # the non-8 digit
    for i in range(index - 1, -1, -1):

        # index digit
        digit = s[i] - '0';

        # if digit is not 8, then break
        if (digit != 8):
            index1 = i;
            break;

    # if on the left side of the '9',
    # no 8 is found then we return by
    # adding a 2 and 0's
    if (index1 == -1):
        return 2 * pow(10, len(s));

    num = 0;

    # till non-8 digit add all numbers
    for i in range(index1):
        num = num * 10 + (s[i] - '0');

    # if non-8 is even or odd
    # than add the next even.
    if (s[index1] % 2 == 0):
        num = num * 10 + (s[index1] - '0' + 2);
    else:
        num = num * 10 + (s[index1] - '0' + 1);

    # add 0 to right of 9
    for i in range(index1 + 1, len(s)):
        num = num * 10;

    return num;

# function to return the smallest
# number with all digits even
def smallestNumber(n):

    num = 0;
    s = "";

    duplicate = n;

    # convert the number to string to
    # perform operations
    while (n):
        s = chr(n % 10 + 48) + s;
        n = int(n / 10);

    index = -1;

    # find out the first odd number
    for i in range(len(s)):
        digit = ord(s[i]) - ord('0');
        if (digit & 1):
            index = i;
            break;

    # if no odd numbers are
    # there, than n is the answer
    if (index == -1):
        return duplicate;

    # if the odd number is 9, than
    # tricky case handles it
    if (s[index] == '9'):
        num = trickyCase(s, index);
        return num;

    # add all digits till first odd
    for i in range(index):
        num = num * 10 + ord(s[i]) - ord('0');

    # increase the odd digit by 1
    num = num * 10 + (ord(s[index]) -
                      ord('0') + 1);

    # add 0 to the right of the odd number
    for i in range(index + 1, len(s)):
        num = num * 10;

    return num;

# Driver Code
N = 2397;
print(smallestNumber(N));

# This code is contributed
# by mits
```

## C#

```
// C# program to print the smallest integer
// not less than N with all even digits
using System;

class GFG
{
// function to return the answer when
// the first odd digit is 9
static int trickyCase(string s,
                      int index)
{
    int index1 = -1;

    // traverse towwars the left
    // to find the non-8 digit
    for (int i = index - 1; i >= 0; i--)
    {
        // index digit
        int digit = s[i] - '0';

        // if digit is not 8, then break
        if (digit != 8)
        {
            index1 = i;
            break;
        }
    }

    // if on the left side of the
    // '9', no 8 is found then we
    // return by adding a 2 and 0's
    if (index1 == -1)
        return 2 * (int)Math.Pow(10, s.Length);

    int num = 0;

    // till non-8 digit add all numbers
    for (int i = 0; i < index1; i++)
        num = num * 10 + (s[i] - '0');

    // if non-8 is even or odd
    // than add the next even.
    if (s[index1] % 2 == 0)
        num = num * 10 +
            (s[index1] - '0' + 2);
    else
        num = num * 10 +
             (s[index1] - '0' + 1);

    // add 0 to right of 9
    for (int i = index1 + 1;
            i < s.Length; i++)
        num = num * 10;

    return num;
}

// function to return the smallest number
// with all digits even
static int smallestNumber(int n)
{
    int num = 0;
    string s = "";

    int duplicate = n;

    // convert the number to
    // string to perform operations
    while (n > 0)
    {
        s = (char)(n % 10 + 48) + s;
        n /= 10;
    }

    int index = -1;

    // find out the first odd number
    for (int i = 0; i < s.Length; i++)
    {
        int digit = s[i] - '0';
        int val = digit & 1;
        if (val == 1)
        {
            index = i;
            break;
        }
    }

    // if no odd numbers are there,
    // than n is the answer
    if (index == -1)
        return duplicate;

    // if the odd number is 9,
    // than tricky case handles it
    if (s[index] == '9')
    {
        num = trickyCase(s, index);
        return num;
    }

    // add all digits till first odd
    for (int i = 0; i < index; i++)
        num = num * 10 +
            (s[i] - '0');

    // increase the odd digit by 1
    num = num * 10 +
        (s[index] - '0' + 1);

    // add 0 to the right of the odd number
    for (int i = index + 1;
            i < s.Length; i++)
        num = num * 10;

    return num;
}

// Driver Code
public static void Main()
{
    int N = 2397;
    Console.Write(smallestNumber(N));
}
}

// This code is contributed
// by Akanksha Rai
?>
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// the smallest integer
// not less than N with
// all even digits

// function to return
// the answer when the
// first odd digit is 9
function trickyCase($s, $index)
{
    $index1 = -1;

    // traverse towwars the
    // left to find the
    // non-8 digit
    for ($i = $index - 1;
         $i >= 0; $i--)
    {
        // index digit
        $digit = $s[$i] - '0';

        // if digit is not
        // 8, then break
        if ($digit != 8)
        {
            $index1 = $i;
            break;
        }
    }

    // if on the left side
    // of the '9', no 8
    // is found then we
    // return by adding a 2
    // and 0's
    if ($index1 == -1)
        return 2 * pow(10,
              strlen($s));

    $num = 0;

    // till non-8 digit
    // add all numbers
    for ($i = 0; $i < $index1; $i++)
        $num = $num * 10 +
              ($s[$i] - '0');

    // if non-8 is even or
    // odd than add the next even.
    if ($s[$index1] % 2 == 0)
        $num = $num * 10 +
              ($s[$index1] - '0' + 2);
    else
        $num = $num * 10 +
              ($s[$index1] - '0' + 1);

    // add 0 to right of 9
    for ($i = $index1 + 1;
         $i < strlen($s); $i++)
        $num = $num * 10;

    return $num;
}

// function to return
// the smallest number
// with all digits even
function smallestNumber($n)
{
    $num = 0;
    $s = "";

    $duplicate = $n;

    // convert the number
    // to string to perform
    // operations
    while ($n)
    {
        $s = chr($n % 10 + 48) . $s;
        $n = (int)($n / 10);
    }

    $index = -1;

    // find out the
    // first odd number
    for ($i = 0;
         $i < strlen($s); $i++)
    {
        $digit = $s[$i] - '0';
        if ($digit & 1)
        {
            $index = $i;
            break;
        }
    }

    // if no odd numbers are
    // there, than n is the answer
    if ($index == -1)
        return $duplicate;

    // if the odd number
    // is 9, than tricky
    // case handles it
    if ($s[$index] == '9')
    {
        $num = trickyCase($s, $index);
        return $num;
    }

    // add all digits
    // till first odd
    for ($i = 0; $i < $index; $i++)
        $num = $num * 10 +
              ($s[$i] - '0');

    // increase the
    // odd digit by 1
    $num = $num * 10 +
          ($s[$index] - '0' + 1);

    // add 0 to the right
    // of the odd number
    for ($i = $index + 1;
         $i < strlen($s); $i++)
        $num = $num * 10;

    return $num;
}

// Driver Code
$N = 2397;
echo smallestNumber($N);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program to print the smallest integer
    // not less than N with all even digits

    // function to return the answer when
    // the first odd digit is 9
    function trickyCase(s, index)
    {
        let index1 = -1;

        // traverse towwars the left
        // to find the non-8 digit
        for (let i = index - 1; i >= 0; i--)
        {
            // index digit
            let digit = s[i].charCodeAt() - '0'.charCodeAt();

            // if digit is not 8, then break
            if (digit != 8)
            {
                index1 = i;
                break;
            }
        }

        // if on the left side of the
        // '9', no 8 is found then we
        // return by adding a 2 and 0's
        if (index1 == -1)
            return 2 * Math.pow(10, s.length);

        let num = 0;

        // till non-8 digit add all numbers
        for (let i = 0; i < index1; i++)
            num = num * 10 + (s[i].charCodeAt() - '0'.charCodeAt());

        // if non-8 is even or odd
        // than add the next even.
        if (s[index1].charCodeAt() % 2 == 0)
            num = num * 10 +
                (s[index1].charCodeAt() - '0'.charCodeAt() + 2);
        else
            num = num * 10 +
                 (s[index1].charCodeAt() - '0'.charCodeAt() + 1);

        // add 0 to right of 9
        for (let i = index1 + 1;
                i < s.length; i++)
            num = num * 10;

        return num;
    }

    // function to return the smallest number
    // with all digits even
    function smallestNumber(n)
    {
        let num = 0;
        let s = "";

        let duplicate = n;

        // convert the number to
        // string to perform operations
        while (n > 0)
        {
            s = String.fromCharCode(n % 10 + 48) + s;
            n = parseInt(n / 10, 10);
        }

        let index = -1;

        // find out the first odd number
        for (let i = 0; i < s.length; i++)
        {
            let digit = s[i].charCodeAt() - '0'.charCodeAt();
            let val = digit & 1;
            if (val == 1)
            {
                index = i;
                break;
            }
        }

        // if no odd numbers are there,
        // than n is the answer
        if (index == -1)
            return duplicate;

        // if the odd number is 9,
        // than tricky case handles it
        if (s[index] == '9')
        {
            num = trickyCase(s, index);
            return num;
        }

        // add all digits till first odd
        for (let i = 0; i < index; i++)
            num = num * 10 +
                (s[i].charCodeAt() - '0'.charCodeAt());

        // increase the odd digit by 1
        num = num * 10 +
            (s[index].charCodeAt() - '0'.charCodeAt() + 1);

        // add 0 to the right of the odd number
        for (let i = index + 1;
                i < s.length; i++)
            num = num * 10;

        return num;
    }

    let N = 2397;
    document.write(smallestNumber(N));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
2400
```

**时间复杂度:** O(M)，其中 M 为 n 中的位数
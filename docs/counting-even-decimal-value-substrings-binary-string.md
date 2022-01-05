# 计算二进制字符串中的偶数十进制值子字符串

> 原文:[https://www . geesforgeks . org/counting-偶数-十进制-值-子字符串-二进制-字符串/](https://www.geeksforgeeks.org/counting-even-decimal-value-substrings-binary-string/)

给定大小为 n 的二进制字符串。考虑从左到右的二进制到十进制转换，计算所有具有偶数十进制值的子字符串(例如，子字符串“1011”被视为 13)
**示例:**

```
Input :  101
Output : 2
Explanation : 
Substring are   : 1, 10, 101, 0, 01, 1 
In decimal form : 1,  1,  3, 0,  2, 1 
There are only 2 even decimal value substring.  

Input : 10010
Output : 8 
```

**简单的解决方法**是逐个[生成所有子串](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)并计算它们的十进制值。至少，返回偶数十进制值子串的计数。
下面是上面想法的实现。

## C++

```
// C++ code to generate all possible substring
// and count even decimal value substring.
#include <bits/stdc++.h>
using namespace std;

// generate all substring in arr[0..n-1]
int evenDecimalValue(string str, int n)
{
    // store the count
    int result = 0;

    // Pick starting point
    for (int i = 0; i < n; i++) {

        // Pick ending point
        for (int j = i; j < n; j++) {

            int decimalValue = 0;
            int powerOf2 = 1;

            // substring between current starting
            // and ending points
            for (int k = i; k <= j; k++) {
                decimalValue += ((str[k] - '0') * powerOf2);

                // increment power of 2 by one
                powerOf2 *= 2;
            }

            if (decimalValue % 2 == 0)
                result++;
        }
    }
    return result;
}

// Driver program
int main()
{
    string str = "10010";
    int n = 5;
    cout << evenDecimalValue(str, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count all even
// decimal value substring .
import java.io.*;

class GFG
{
    // generate all substring in arr[0..n-1]
    static int evenDecimalValue(String str, int n)
    {
       // store the count
       int result = 0;

       // Pick starting point
       for (int i = 0; i < n; i++)
       {

          // Pick ending point
          for (int j = i; j < n; j++)
          {

            int decimalValue = 0;
            int powerOf2 = 1;

            // substring between current
            // starting and ending points
            for (int k = i; k <= j; k++)
            {
                decimalValue += ((str.charAt(k) -
                                 '0') * powerOf2);

                // increment power of 2 by one
                powerOf2 *= 2;
            }

            if (decimalValue % 2 == 0)
                result++;
          }
      }
      return result;
    }

    // Driver code
    public static void main (String[] args)
    {
       String str = "10010";
       int n = 5;
       System.out.println(evenDecimalValue(str, n));

    }
}

//This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 Program to count all even
# decimal value substring
import math

# Generate all substring in arr[0..n-1]
def evenDecimalValue(str, n) :

    # Store the count
    result = 0

    # Pick starting point
    for i in range(0, n) :

        # Pick ending point
        for j in range(i, n):

            decimalValue = 0;
            powerOf2 = 1;

            # Substring between current
            # starting and ending points
            for k in range(i, j + 1) :
                decimalValue += ((int(str[k])- 0) * powerOf2)

                # increment power of 2 by one
                powerOf2 *= 2

            if (decimalValue % 2 == 0):
                result += 1

    return result

# Driver code
str = "10010"
n = 5
print (evenDecimalValue(str, n))

# This code is contributed by Gitanjali.
```

## C#

```
// C# Program to count all even
// decimal value substring .
using System;

class GFG
{
    // generate all substring in arr[0..n-1]
    static int evenDecimalValue(string str, int n)
    {
        // store the count
        int result = 0;

        // Pick starting point
        for (int i = 0; i < n; i++)
        {

            // Pick ending point
            for (int j = i; j < n; j++)
            {

                int decimalValue = 0;
                int powerOf2 = 1;

                // substring between current
                // starting and ending points
                for (int k = i; k <= j; k++)
                {
                    decimalValue += ((str[k] -
                                    '0') * powerOf2);

                    // increment power of 2 by one
                    powerOf2 *= 2;
                }

                if (decimalValue % 2 == 0)
                    result++;
            }
        }
        return result;
    }

    // Driver code
    public static void Main ()
    {
        String str = "10010";
        int n = 5;
        Console.WriteLine(evenDecimalValue(str, n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to generate all
// possible substring and
// count even decimal value
// substring

// generate all substring
// in arr[0..n-1]
function evenDecimalValue( $str, $n)
{
    // store the count
    $result = 0;

    // Pick starting point
    for ( $i = 0; $i < $n; $i++)
    {

        // Pick ending point
        for ($j = $i; $j < $n; $j++)
        {

            $decimalValue = 0;
            $powerOf2 = 1;

            // substring between current
            // starting and ending points
            for ( $k = $i; $k <= $j; $k++)
            {
                $decimalValue += (($str[$k] - '0') *
                                   $powerOf2);

                // increment power of 2 by one
                $powerOf2 *= 2;
            }

            if ($decimalValue % 2 == 0)
                $result++;
        }
    }
    return $result;
}

// Driver Code
$str = "10010";
$n = 5;
echo evenDecimalValue($str, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// javascript code to generate all possible substring
// and count even decimal value substring.

// generate all substring in arr[0..n-1]
function evenDecimalValue(str, n)
{
    // store the count
    var result = 0;

    // Pick starting point
    for (var i = 0; i < n; i++) {

        // Pick ending point
        for (var j = i; j < n; j++) {

            var decimalValue = 0;
            var powerOf2 = 1;

            // substring between current starting
            // and ending points
            for (var k = i; k <= j; k++) {
                decimalValue += ((str[k] - '0') * powerOf2);

                // increment power of 2 by one
                powerOf2 *= 2;
            }

            if (decimalValue % 2 == 0)
                result++;
        }
    }
    return result;
}

// Driver program
var str = "10010";
var n = 5;
document.write( evenDecimalValue(str, n) );

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
8
```

**时间复杂度:** O(n <sup>3</sup> )
**高效解**是基于起始值为‘0’的子串总是产生偶数小数值。所以我们简单地从左到右遍历一个循环，统计所有起始值为零的子串。
以下是上述思路的实现。

## C++

```
// Program to count all even decimal value substring .
#include <bits/stdc++.h>
using namespace std;

// function return count of even decimal
// value substring
int evenDecimalValue(string str, int n)
{
    // store the count of even decimal value substring
    int result = 0;
    for (int i = 0; i < n; i++) {

        // substring started with '0'
        if (str[i] == '0') {

            // increment result by (n-i)
            // because all substring which are generate by
            // this character produce even decimal value.
            result += (n - i);
        }
    }
    return result;
}

// Driver program
int main()
{
    string str = "10010";
    int n = 5;
    cout << evenDecimalValue(str, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count all even
// decimal value substring .
import java.io.*;

class GFG
{
    // function return count of
    // even decimal value substring
    static int evenDecimalValue(String str, int n)
    {
        // store the count of even
        // decimal value substring
        int result = 0;
        for (int i = 0; i < n; i++)
        {

            // substring started with '0'
            if (str.charAt(i) == '0')
            {

                // increment result by (n-i)
                // because all substring which
                // are generate by this character
                // produce even decimal value.
                result += (n - i);
            }
        }
        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "10010";
        int n = 5;
        System.out.println(evenDecimalValue(str, n));
    }
}
// This code is contributed
// by Gitanjali.
```

## 蟒蛇 3

```
# Python Program to count all even
# decimal value substring

# Function return count of even
# decimal value substring
def evenDecimalValue(str, n) :

    # Store the count of even
    # decimal value substring
    result = 0
    for i in range(0, n):

        # substring started with '0'
        if (str[i] == '0'):

            # increment result by (n-i)
            # because all substring which are generate by
            # this character produce even decimal value.
            result += (n - i)

    return result

# Driver code
str = "10010"
n = 5
print (evenDecimalValue(str, n))

# This code is contributed by Gitanjali.
```

## C#

```
// C# Program to count all even
// decimal value substring .
using System;

class GFG
{
    // function return count of
    // even decimal value substring
    static int evenDecimalValue(string str, int n)
    {
        // store the count of even
        // decimal value substring
        int result = 0;
        for (int i = 0; i < n; i++)
        {

            // substring started with '0'
            if (str[i] == '0')
            {

                // increment result by (n-i)
                // because all substring which
                // are generate by this character
                // produce even decimal value.
                result += (n - i);
            }
        }
        return result;
    }

    // Driver code
    public static void Main()
    {
        string str = "10010";
        int n = 5;
        Console.WriteLine(evenDecimalValue(str, n));
    }
}
// This code is contributed
// by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to count all
// even decimal value substring .

// function return count of
// even decimal value substring
function evenDecimalValue($str, $n)
{
    // store the count of even
    // decimal value substring
    $result = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // substring started with '0'
        if ($str[$i] == '0')
        {

            // increment result by (n-i)
            // because all substring which
            // are generated by this character
            // produce even decimal value.
            $result += ($n - $i);
        }
    }
    return $result;
}

// Driver Code
$str = "10010";
$n = 5;
echo evenDecimalValue($str, $n) ;
return 0;

// This code is contributed by SanjuTomar.
?>
```

## java 描述语言

```
<script>
    // Javascript Program to count all even
    // decimal value substring .

    // function return count of
    // even decimal value substring
    function evenDecimalValue(str, n)
    {
        // store the count of even
        // decimal value substring
        let result = 0;
        for (let i = 0; i < n; i++)
        {

            // substring started with '0'
            if (str[i] == '0')
            {

                // increment result by (n-i)
                // because all substring which
                // are generate by this character
                // produce even decimal value.
                result += (n - i);
            }
        }
        return result;
    }

    let str = "10010";
    let n = 5;
    document.write(evenDecimalValue(str, n));

    // This code is contributed by divyeshrabadiya07.
</script>
```

】
**输出:**

```
8
```

**时间复杂度:**O(n)
T3】空间复杂度: O(1)
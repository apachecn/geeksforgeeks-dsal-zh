# 不使用/和%运算符检查数字是否为 5 的倍数

> 原文:[https://www . geesforgeks . org/check-如果一个数字是 5 的倍数，不使用 and-operator/](https://www.geeksforgeeks.org/check-if-a-number-is-multiple-of-5-without-using-and-operators/)

给定一个正数 n，编写一个函数 is multiplief5(int n)，如果 n 是 5 的倍数，则返回 true，否则返回 false。**不允许使用%和/运算符**。
**方法 1(重复从 n 中减去 5)**
运行一个循环，当 n 大于 0 时，在循环中从 n 中减去 5。循环结束后，检查 n 是否为 0。如果 n 变成 0，则 n 是 5 的倍数，否则不是。

## C++

```
#include <iostream>
using namespace std;

// assumes that n is a positive integer
bool isMultipleof5 (int n)
{
    while ( n > 0 )
        n = n - 5;

    if ( n == 0 )
        return true;

    return false;
}

// Driver Code
int main()
{
    int n = 19;
    if ( isMultipleof5(n) == true )
        cout << n <<" is multiple of 5";
    else
        cout << n << " is not a multiple of 5";

    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
#include<stdio.h>

// assumes that n is a positive integer
bool isMultipleof5 (int n)
{
    while ( n > 0 )
        n = n - 5;

    if ( n == 0 )
        return true;

    return false;
}

// Driver Code
int main()
{
    int n = 19;
    if ( isMultipleof5(n) == true )
        printf("%d is multiple of 5\n", n);
    else
        printf("%d is not a multiple of 5\n", n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a number
// is multiple of 5 without using
// '/' and '%' operators
class GFG
{

// assumes that n is a positive integer
static boolean isMultipleof5 (int n)
{
    while (n > 0)
        n = n - 5;

    if (n == 0)
        return true;

    return false;
}

// Driver Code
public static void main(String[] args)
{
    int n = 19;
    if (isMultipleof5(n) == true)
        System.out.printf("%d is multiple of 5\n", n);
    else
        System.out.printf("%d is not a multiple of 5\n", n);
}
}

// This code is contributed by Smitha DInesh Semwal
```

## 蟒蛇 3

```
# Python code to check
# if a number is multiple of
# 5 without using / and %

# Assumes that n is a positive integer
def isMultipleof5(n):

    while ( n > 0 ):
        n = n - 5

    if ( n == 0 ):
        return 1

    return 0

# Driver Code
i = 19
if ( isMultipleof5(i) == 1 ):
    print (i, "is multiple of 5")
else:
    print (i, "is not a multiple of 5")

# This code is contributed
# by Sumit Sudhakar
```

## C#

```
// C# code to check if a number
// is multiple of 5 without using /
// and % operators
using System;

class GFG
{

// assumes that n is a positive integer
static bool isMultipleof5 (int n)
{
    while (n > 0)
        n = n - 5;

    if (n == 0)
        return true;

    return false;
}

// Driver Code
public static void Main()
{
    int n = 19;
    if (isMultipleof5(n) == true)
        Console.Write(n + " is multiple of 5\n");
    else
        Console.Write(n + " is not a multiple of 5\n");
}
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// assumes that n is a positive integer
function isMultipleof5 ($n)
{
    while ( $n > 0 )
        $n = $n - 5;

    if ( $n == 0 )
        return true;

    return false;
}

// Driver Code
    $n = 19;
    if ( isMultipleof5($n) == true )
        echo("$n is multiple of 5");
    else
        echo("$n is not a multiple of 5" );

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// assumes that n is a positive integer
function isMultipleof5 (n)
{
    while (n > 0)
        n = n - 5;

    if (n == 0)
        return true;

    return false;
}

// Driver Code
    let n = 19;
    if (isMultipleof5(n) == true)
        document.write(n + " is multiple of 5\n");
    else
        document.write(n + " is not a multiple of 5\n");

</script>
```

**输出:**

```
19 is not a multiple of 5
```

***时间复杂度:** O(n / 5)*

***辅助空间:** O(1)*

**方法 2(转换为字符串并检查最后一个字符)**
将 n 转换为字符串并检查字符串的最后一个字符。如果最后一个字符是“5”或“0”，则 n 是 5 的倍数，否则不是。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Assuming that integer takes 4 bytes, there
// can be maximum 10 digits in a integer
# define MAX 11

bool isMultipleof5(int n)
{
    char str[MAX];
    int len = strlen(str);

    // Check the last character of string
    if ( str[len - 1] == '5' ||
        str[len - 1] == '0' )

        return true;

    return false;
}

// Driver Code
int main()
{
    int n = 19;
    if ( isMultipleof5(n) == true )
        cout << n <<" is multiple of 5" <<endl;
    else
        cout << n <<" is not multiple of 5" <<endl;

    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

// Assuming that integer takes 4 bytes, there
// can be maximum 10 digits in a integer
# define MAX 11

bool isMultipleof5(int n)
{
    char str[MAX];
    int len = strlen(str);

    // Check the last character of string
    if ( str[len - 1] == '5' ||
         str[len - 1] == '0' )

        return true;

    return false;
}

// Driver Code
int main()
{
    int n = 19;
    if ( isMultipleof5(n) == true )
        printf("%d is multiple of 5\n", n);
    else
        printf("%d is not a multiple of 5\n", n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Assuming that integer
// takes 4 bytes, there
// can be maximum 10
// digits in a integer
class GFG
{
static int MAX = 11;

static boolean isMultipleof5(int n)
{
    char str[] = new char[MAX];
    int len = str.length;

    // Check the last
    // character of string
    if (str[len - 1] == '5' ||
        str[len - 1] == '0' )

        return true;

    return false;
}

// Driver Code
public static void main(String[] args)
{
    int n = 19;
    if ( isMultipleof5(n) == true )
        System.out.println(n +" is multiple " +
                                       "of 5");
    else
        System.out.println(n +" is not a " +
                           "multiple of 5");
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Assuming that integer
# takes 4 bytes, there
# can be maximum 10
# digits in a integer
MAX = 11;

def isMultipleof5(n):
    s = str(n);
    l = len(s);

    # Check the last
    # character of string
    if (s[l - 1] == '5' or
        s[l - 1] == '0'):
        return True;
    return False;

# Driver Code
n = 19;
if (isMultipleof5(n) == True ):
    print(n, "is multiple of 5");
else:
    print(n, "is not a multiple of 5");

# This code is contributed by mits
```

## C#

```
using System;

// Assuming that integer
// takes 4 bytes, there
// can be maximum 10
// digits in a integer
class GFG
{
static int MAX = 11;

static bool isMultipleof5(int n)
{
    char[] str = new char[MAX];
    int len = str.Length;

    // Check the last
    // character of string
    if (str[len - 1] == '5' ||
        str[len - 1] == '0' )

        return true;

    return false;
}

// Driver Code
static void Main()
{
    int n = 19;
    if ( isMultipleof5(n) == true )
        Console.WriteLine("{0} is " +
                          "multiple of 5", n);
    else
        Console.WriteLine("{0} is not a " +
                          "multiple of 5", n);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Assuming that integre
// takes 4 bytes, there
// can be maximum 10
// digits in a integer
$MAX = 11;

function isMultipleof5($n)
{
    global $MAX;
    $str = (string)$n;
    $len = strlen($str);

    // Check the last
    // character of string
    if ($str[$len - 1] == '5' ||
        $str[$len - 1] == '0')

        return true;

    return false;
}

// Driver Code
$n = 19;
if (isMultipleof5($n) == true )
    echo "$n is multiple of 5";
else
    echo "$n is not a multiple of 5";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Assuming that integer
// takes 4 bytes, there
// can be maximum 10
// digits in a integer
MAX = 11;

function isMultipleof5(n)
{
    str = Array(n).fill('');
    var len = str.length;

    // Check the last
    // character of string
    if (str[len - 1] == '5' ||
        str[len - 1] == '0' ) 
        return true;

    return false;
}

// Driver Code
var n = 19;
if ( isMultipleof5(n) == true )
    document.write(n +" is multiple " +
                                   "of 5");
else
    document.write(n +" is not a " +
                       "multiple of 5");

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
19 is not a multiple of 5
```

***时间复杂度:** O(1)*

***辅助空间:** O(MAX)*

感谢 Baban_Rathore 提出这个方法。
**方法 3(将最后一位数字设置为 0，并使用浮点技巧)**
在两种情况下，数字 n 可以是 5 的倍数。当 n 的最后一位是 5 或 10 时。如果设置了 n 的二进制等价物中的最后一位(当最后一位是 5 时可能是这种情况)，那么我们使用 n < < =1 乘以 2，以确保如果数字是 5 的倍数，那么我们将最后一位作为 0。一旦我们做到了这一点，我们的工作就是检查最后一个数字是否为 0，这可以使用浮点和整数比较技巧来完成。

## C++

```
#include <iostream>
using namespace std;
bool isMultipleof5(int n)
{
    // If n is a multiple of 5 then we
    // make sure that last digit of n is 0
    if ( (n & 1) == 1 )
        n <<= 1;

    float x = n;
    x = ( (int)(x * 0.1) ) * 10;

    // If last digit of n is 0 then n
    // will be equal to (int)x
    if ( (int)x == n )
        return true;

    return false;
}

// Driver Code
int main()
{
    int i = 19;
    if ( isMultipleof5(i) == true )
        cout << i <<" is multiple of 5\n";
    else
        cout << i << " is not a multiple of 5\n";

    getchar();
    return 0;
}

// This code is contributed by shubhamsingh10
```

## C

```
#include<stdio.h>

bool isMultipleof5(int n)
{
    // If n is a multiple of 5 then we
    // make sure that last digit of n is 0
    if ( (n & 1) == 1 )
        n <<= 1;

    float x = n;
    x = ( (int)(x * 0.1) ) * 10;

    // If last digit of n is 0 then n
    // will be equal to (int)x
    if ( (int)x == n )
        return true;

    return false;
}

// Driver Code
int main()
{
    int i = 19;
    if ( isMultipleof5(i) == true )
        printf("%d is multiple of 5\n", i);
    else
        printf("%d is not a multiple of 5\n", i);

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if
// a number is multiple of
// 5 without using / and %
class GFG
{
static boolean isMultipleof5(int n)
{
    // If n is a multiple of 5
    // then we make sure that
    // last digit of n is 0
    if ((n & 1) == 1)
        n <<= 1;

    float x = n;
    x = ((int)(x * 0.1)) * 10;

    // If last digit of n is
    // 0 then n will be equal
    // to (int)x
    if ((int)x == n)
        return true;

    return false;
}

// Driver Code
public static void main(String[] args)
{
    int i = 19;
    if (isMultipleof5(i) == true)
        System.out.println(i + "is multiple of 5");
    else
        System.out.println(i + " is not a " +
                            "multiple of 5");
}
}

// This code is contributed
// by mits
```

## 蟒蛇 3

```
# Python code to check
# if a number is multiple of
# 5 without using / and %

def isMultipleof5(n):

    # If n is a multiple of 5 then we
    # make sure that last digit of n is 0
    if ( (n & 1) == 1 ):
        n <<= 1;

    x = n
    x = ( (int)(x * 0.1) ) * 10

    # If last digit of n is 0
    # then n will be equal to x
    if ( x == n ):
        return 1

    return 0

# Driver Code
i = 19
if ( isMultipleof5(i) == 1 ):
    print (i, "is multiple of 5")
else:
    print (i, "is not a multiple of 5")

# This code is contributed
# by Sumit Sudhakar
```

## C#

```
// C# code to check if
// a number is multiple of
// 5 without using / and %
class GFG
{
static bool isMultipleof5(int n)
{
    // If n is a multiple of 5
    // then we make sure that
    // last digit of n is 0
    if ((n & 1) == 1)
        n <<= 1;

    float x = n;
    x = ((int)(x * 0.1)) * 10;

    // If last digit of n is
    // 0 then n will be equal
    // to (int)x
    if ((int)x == n)
        return true;

    return false;
}

// Driver Code
public static void Main()
{
    int i = 19;
    if (isMultipleof5(i) == true)
        System.Console.WriteLine(i + "is multiple of 5");
    else
        System.Console.WriteLine(i + " is not a " +
                                   "multiple of 5");
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
function isMultipleof5($n)
{
    // If n is a multiple of 5
    // then we make sure that
    // last digit of n is 0
    if (($n & 1) == 1 )
        $n <<= 1;

    $x = $n;
    $x = ((int)($x * 0.1)) * 10;

    // If last digit of n
    // is 0 then n will be
    // equal to (int)x
    if ( (int)($x) == $n )
        return true;

    return false;
}

// Driver Code
$i = 19;
if ( isMultipleof5($i) == true )
    echo "$i is multiple of 5\n";
else
    echo "$i is not a multiple of 5\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// JavaScript code to check if
// a number is multiple of
// 5 without using / and %
function isMultipleof5( n)
{    

    // If n is a multiple of 5 then we
    // make sure that last digit of n is 0
    if ( (n & 1) == 1 )
        n <<= 1;

    x = ( (int)(x * 0.1) ) * 10;

    // If last digit of n is 0 then n
    // will be equal to (int)x
    if ( (int)(x == n))
        return true;

    return false;
}

// Driver Code
      i = 19;
    if ( isMultipleof5 == true)
        document.write( i + " is multiple of 5\n");
    else
        document.write( i + " is not a multiple of 5\n");

      // This code is contributed by simranarora5sos
    </script>
```

**输出:**

```
19 is not a multiple of 5
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

感谢黑王子提出这个方法。
如果发现以上代码/算法不正确，请写评论，或者找其他方法解决同样的问题。
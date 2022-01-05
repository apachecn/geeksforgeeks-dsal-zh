# 检查一个数字是否在给定的基数内

> 原文:[https://www . geesforgeks . org/check-a-number-in-given-base-or-not/](https://www.geeksforgeeks.org/check-if-a-number-is-in-given-base-or-not/)

给定一个数字作为字符串和基数，检查给定的数字是否在给定的基数内。
**例:**

```
Input : str = "1010", base = 2
Output : Yes

Input : str = "1015", base = 2
Output : No

Input : str = "AF87", base = 16
Output : Yes
```

想法是逐一检查所有数字是否都在给定的基本范围内。如果是，返回真，否则返回假。

## C++

```
// CPP program to check if given
// number is in given base or not.
#include <cstring>
#include <iostream>
using namespace std;

bool isInGivenBase(string str, int base)
{
    // Allowed bases are till 16 (Hexadecimal)
    if (base > 16)
    return false;

    // If base is below or equal to 10, then all
    // digits should be from 0 to 9.
    else if (base <= 10)
    {
    for (int i = 0; i < str.length(); i++)
        if (!(str[i] >= '0' and
             str[i] < ('0' + base)))
            return false;
    }

    // If base is below or equal to 16, then all
    // digits should be from 0 to 9 or from 'A'
    else
    {
    for (int i = 0; i < str.length(); i++)
        if (! ((str[i] >= '0' &&
                str[i] < ('0' + base)) ||                                
                (str[i] >= 'A' &&
                 str[i] < ('A' + base - 10))
            ))                
            return false;
    }
    return true;
}

// Driver code
int main()
{
    string str = "AF87";
    if (isInGivenBase(str, 16))
    cout << "Yes";
    else
    cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if given
// number is in given base or not.
class Geeks {

static boolean isInGivenBase(String str, int base)
{

    // Allowed bases are till 16 (Hexadecimal)
    if (base > 16)
    return false;

    // If base is below or equal to 10, then all
    // digits should be from 0 to 9.
    else if (base <= 10)
    {
    for (int i = 0; i < str.length(); i++)
        if (!(str.charAt(i) >= '0' &&
              str.charAt(i) < ('0' + base)))
            return false;
    }

    // If base is below or equal to 16, then all
    // digits should be from 0 to 9 or from 'A'
    else
    {
    for (int i = 0; i < str.length(); i++)
        if (! ((str.charAt(i) >= '0' &&
                str.charAt(i) < ('0' + base)) ||                            
                (str.charAt(i) >= 'A' &&
                 str.charAt(i) < ('A' + base - 10))
            ))            
            return false;
    }
    return true;
}

// Driver Class
public static void main(String args[])

{
    String str = "AF87";
    if (isInGivenBase(str, 16) == true)
    System.out.println("Yes");
    else
    System.out.println("No");

}
}

// This code is contributed by ankita_saini
```

## 蟒蛇 3

```
# Python3 program to check if given
# number is in given base or not.

def isInGivenBase(Str, base):

    # Allowed bases are till 16 (Hexadecimal)
    if (base > 16):
        return False

    # If base is below or equal to 10,
    # then all digits should be from 0 to 9.
    elif (base <= 10):
        for i in range(len(Str)):
            if (Str[i].isnumeric() and
               (ord(Str[i]) >= ord('0') and
                ord(Str[i]) < (ord('0') + base)) == False):
                return False

    # If base is below or equal to 16, then all
    # digits should be from 0 to 9 or from 'A'
    else:
        for i in range(len(Str)):
            if (Str[i].isnumeric() and
               ((ord(Str[i]) >= ord('0') and
                 ord(Str[i]) < (ord('0') + base)) or
                (ord(Str[i]) >= ord('A') and
                 ord(Str[i]) < (ord('A') + base - 10))) == False):
                return False

    return True

# Driver code
Str = "AF87"
if (isInGivenBase(Str, 16)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to check if given
// number is in given base or not.
using System;

class GFG
{
static bool isInGivenBase(String str,
                          int bas)
{

    // Allowed base are
    // till 16 (Hexadecimal)
    if (bas > 16)
    return false;

    // If bas is below or equal
    // to 10, then all digits
    // should be from 0 to 9.
    else if (bas <= 10)
    {
    for (int i = 0; i < str.Length; i++)
        if (!(str[i] >= '0' &&
              str[i] < ('0' + bas)))
            return false;
    }

    // If base is below or equal
    // to 16, then all digits should
    // be from 0 to 9 or from 'A'
    else
    {
    for (int i = 0; i < str.Length; i++)
        if (! ((str[i] >= '0' &&
                str[i] < ('0' + bas)) ||                        
               (str[i] >= 'A' &&
                str[i] < ('A' + bas - 10))
            ))        
            return false;
    }
    return true;
}

// Driver Code
public static void Main(String []args)
{
    String str = "AF87";
    if (isInGivenBase(str, 16) == true)
    Console.WriteLine("Yes");
    else
    Console.WriteLine("No");
}
}

// This code is contributed
// by ankita_saini
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if given
// number is in given base or not.

function isInGivenBase($str, $base)
{
    // Allowed bases are till
    // 16 (Hexadecimal)
    if ($base > 16)
    return false;

    // If base is below or equal to
    // 10, then all digits should
    // be from 0 to 9.
    else if ($base <= 10)
    {
    for ($i = 0; $i < strlen($str); $i++)
        if (!($str[$i] >= '0' and
            $str[$i] < ('0' + $base)))
            return false;
    }

    // If base is below or equal to 16,
    // then all digits should be from
    // 0 to 9 or from 'A'
    else
    {
    for ($i = 0; $i < strlen($str); $i++)
        if (! (($str[$i] >= '0' &&
                $str[$i] < ('0' + $base)) ||                            
               ($str[$i] >= 'A' &&
                $str[$i] < ('A' + $base - 10))
            ))            
            return false;
    }
    return true;
}

// Driver code
$str = "AF87";

if (isInGivenBase($str, 16))
    echo "Yes";
else
    echo "No";

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

    // Javascript program to check if given
    // number is in given base or not.

    function isInGivenBase(str, bas)
    {

        // Allowed base are
        // till 16 (Hexadecimal)
        if (bas > 16)
            return false;

        // If bas is below or equal
        // to 10, then all digits
        // should be from 0 to 9.
        else if (bas <= 10)
        {
          for (let i = 0; i < str.length; i++)
              if (!(str[i].charCodeAt() >=
              '0'.charCodeAt() &&
               str[i].charCodeAt() <
               ('0'.charCodeAt() + bas)))
                  return false;
        }

        // If base is below or equal
        // to 16, then all digits should
        // be from 0 to 9 or from 'A'
        else
        {
          for (let i = 0; i < str.length; i++)
              if (! ((str[i].charCodeAt() >=
              '0'.charCodeAt() &&
               str[i].charCodeAt() <
               ('0'.charCodeAt() + bas)) ||                        
               (str[i].charCodeAt() >=
               'A'.charCodeAt() &&
                str[i].charCodeAt() <
                ('A'.charCodeAt() + bas - 10))
                  ))        
                  return false;
        }
        return true;
    }

    let str = "AF87";
    if (isInGivenBase(str, 16) == true)
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```
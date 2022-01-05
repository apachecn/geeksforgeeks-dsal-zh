# 给定一个巨大的数字，检查它是否是 2 的幂。

> 原文:[https://www . geesforgeks . org/given-巨额-数字-校验-幂-二/](https://www.geeksforgeeks.org/given-huge-number-check-power-two/)

找出一个给定的数，**数**是否为 2 的幂。更具体地说，找出给定的数字是否可以表示为 2^k，其中 k > = 1。如果数字是 2 的幂，返回 1，否则返回 0
**注:**

*   给定数字的位数(即数字)可以大于 100。
*   非零数字前没有前导零。例如 0000128 不在输入中。/li >

**示例:**

```
Input : 3 
Output : 0
2^0 = 1 where as k >= 1

Input : 128
Output : 1
```

**方法一:使用字符串**
思路是将大数(表示为字符串)重复除以 2。为了执行除法，我们从右向左遍历数字。如果最后一个数字本身不能被 2 整除，我们返回 0。否则我们遵循学校的划分方法。

## C

```
/*  C program to find whether a number is power of
    2 or not */
#include <stdio.h>
#include <string.h>

// returns 1 when str is power of 2
// return 0 when str is not a power of 2
int isPowerOf2(char* str)
{
    int len_str = strlen(str);

    // sum stores the intermediate dividend while
    // dividing.
    int num = 0;

    // if the input is "1" then return 0
    // because 2^k = 1 where k >= 1 and here k = 0
    if (len_str == 1 && str[len_str - 1] == '1')
        return 0;

    // Divide the number until it gets reduced to 1
    // if we are successfully able to reduce the number
    // to 1 it means input string is power of two if in
    // between an odd number appears at the end it means
    // string is not divisible by two hence not a power
    // of 2.
    while (len_str != 1 || str[len_str - 1] != '1') {

        // if the last digit is odd then string is not
        // divisible by 2 hence not a power of two
        // return 0.
        if ((str[len_str - 1] - '0') % 2 == 1)
            return 0;

        // divide the whole string by 2\. i is used to
        // track index in current number. j is used to
        // track index for next iteration.
        for (int i = 0, j = 0; i < len_str; i++) {
            num = num * 10 + str[i] - '0';

            // if num < 2 then we have to take another digit
            // to the right of A[i] to make it bigger than
            // A[i]. E. g. 214 / 2 --> 107
            if (num < 2) {

                // if it's not the first index. E.g 214
                // then we have to include 0.
                if (i != 0)
                    str[j++] = '0';               

                // for eg. "124" we will not write 064
                // so if it is the first index just ignore
                continue;
            }

            str[j++] = (int)(num / 2) + '0';
            num = (num) - (num / 2) * 2;
        }

        str[j] = '\0';

        // After every division by 2 the
        // length of string is changed.
        len_str = j;
    }

    // if the string reaches to 1 then the str is
    // a power of 2.
    return 1;
}

// Driver code.
int main()
{
    char str1[] = "12468462246684202468024"
                     "6842024662202000002";
    char str2[] = "1";
    char str3[] = "128";

    printf("%d\n%d\n%d", isPowerOf2(str1),
           isPowerOf2(str2), isPowerOf2(str3));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to find whether a number 
    is power of 2 or not */
import java.util.*;

class GFG
{

// returns 1 when str is power of 2
// return 0 when str is not a power of 2
static int isPowerOf2(String s)
{
    char []str = s.toCharArray();
    int len_str = s.length();

    // sum stores the intermediate dividend while
    // dividing.
    int num = 0;

    // if the input is "1" then return 0
    // because 2^k = 1 where k >= 1 and here k = 0
    if (len_str == 1 && str[len_str - 1] == '1')
        return 0;

    // Divide the number until it gets reduced to 1
    // if we are successfully able to reduce the number
    // to 1 it means input string is power of two if in
    // between an odd number appears at the end it means
    // string is not divisible by two hence not a power
    // of 2.
    while (len_str != 1 || str[len_str - 1] != '1')
    {

        // if the last digit is odd then string is not
        // divisible by 2 hence not a power of two
        // return 0.
        if ((str[len_str - 1] - '0') % 2 == 1)
            return 0;

        // divide the whole string by 2\. i is used to
        // track index in current number. j is used to
        // track index for next iteration.
        int j = 0;
        for (int i = 0; i < len_str; i++)
        {
            num = num * 10 + (int)str[i] - (int)'0';

            // if num < 2 then we have to take another digit
            // to the right of A[i] to make it bigger than
            // A[i]. E. g. 214 / 2 --> 107
            if (num < 2)
            {

                // if it's not the first index. E.g 214
                // then we have to include 0.
                if (i != 0)
                    str[j++] = '0';    

                // for eg. "124" we will not write 064
                // so if it is the first index just ignore
                continue;
            }

            str[j++] = (char)((int)(num / 2) + (int)'0');
            num = (num) - (num / 2) * 2;
        }

        str[j] = '\0';

        // After every division by 2 the
        // length of string is changed.
        len_str = j;
    }

    // if the string reaches to 1 then the str is
    // a power of 2.
    return 1;
}

// Driver code.
public static void main (String[] args)
{
    String str1 = "124684622466842024680246842024662202000002";
    String str2 = "1";
    String str3 = "128";

    System.out.println(isPowerOf2(str1) +
                "\n"+isPowerOf2(str2) +
                "\n"+isPowerOf2(str3));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find whether a number
# is power of 2 or not

# returns 1 when str is power of 2
# return 0 when str is not a power of 2
def isPowerOf2(sttr):

    len_str = len(sttr);
    sttr=list(sttr);

    # sum stores the intermediate dividend
    # while dividing.
    num = 0;

    # if the input is "1" then return 0
    # because 2^k = 1 where k >= 1 and here k = 0
    if (len_str == 1 and sttr[len_str - 1] == '1'):
        return 0;

    # Divide the number until it gets reduced to 1
    # if we are successfully able to reduce the number
    # to 1 it means input string is power of two if in
    # between an odd number appears at the end it means
    # string is not divisible by two hence not a power
    # of 2.
    while (len_str != 1 or sttr[len_str - 1] != '1'):

        # if the last digit is odd then string is not
        # divisible by 2 hence not a power of two
        # return 0.
        if ((ord(sttr[len_str - 1]) - ord('0')) % 2 == 1):
            return 0;

        # divide the whole string by 2\. i is used to
        # track index in current number. j is used to
        # track index for next iteration.
        j = 0;
        for i in range(len_str):
            num = num * 10 + (ord(sttr[i]) - ord('0'));

            # if num < 2 then we have to take another digit
            # to the right of A[i] to make it bigger than
            # A[i]. E. g. 214 / 2 --> 107
            if (num < 2):

                # if it's not the first index. E.g 214
                # then we have to include 0.
                if (i != 0):
                    sttr[j] = '0';
                    j += 1;

                # for eg. "124" we will not write 064
                # so if it is the first index just ignore
                continue;

            sttr[j] = chr((num // 2) + ord('0'));
            j += 1;
            num = (num) - (num // 2) * 2;

        # After every division by 2 the
        # length of string is changed.
        len_str = j;

    # if the string reaches to 1 then the
    # str is a power of 2.
    return 1;

# Driver code.
str1 = "124684622466842024680246842024662202000002";
str2 = "1";
str3 = "128";

print("", isPowerOf2(str1), "\n",
          isPowerOf2(str2), "\n",
          isPowerOf2(str3));

# This code is contributed by mits
```

## C#

```
/* C# program to find whether a number is power of
    2 or not */
using System;

class GFG
{

// returns 1 when str is power of 2
// return 0 when str is not a power of 2
static int isPowerOf2(string s)
{
    char []str = s.ToCharArray();
    int len_str = str.Length;

    // sum stores the intermediate dividend while
    // dividing.
    int num = 0;

    // if the input is "1" then return 0
    // because 2^k = 1 where k >= 1 and here k = 0
    if (len_str == 1 && str[len_str - 1] == '1')
        return 0;

    // Divide the number until it gets reduced to 1
    // if we are successfully able to reduce the number
    // to 1 it means input string is power of two if in
    // between an odd number appears at the end it means
    // string is not divisible by two hence not a power
    // of 2.
    while (len_str != 1 || str[len_str - 1] != '1')
    {

        // if the last digit is odd then string is not
        // divisible by 2 hence not a power of two
        // return 0.
        if ((str[len_str - 1] - '0') % 2 == 1)
            return 0;

        // divide the whole string by 2\. i is used to
        // track index in current number. j is used to
        // track index for next iteration.
        int j = 0;
        for (int i = 0; i < len_str; i++)
        {
            num = num * 10 + (int)str[i] - (int)'0';

            // if num < 2 then we have to take another digit
            // to the right of A[i] to make it bigger than
            // A[i]. E. g. 214 / 2 --> 107
            if (num < 2)
            {

                // if it's not the first index. E.g 214
                // then we have to include 0.
                if (i != 0)
                    str[j++] = '0';        

                // for eg. "124" we will not write 064
                // so if it is the first index just ignore
                continue;
            }

            str[j++] = (char)((int)(num / 2) + (int)'0');
            num = (num) - (num / 2) * 2;
        }

        str[j] = '\0';

        // After every division by 2 the
        // length of string is changed.
        len_str = j;
    }

    // if the string reaches to 1 then the str is
    // a power of 2.
    return 1;
}

// Driver code.
static void Main()
{
    string str1 = "124684622466842024680246842024662202000002";
    string str2 = "1";
    string str3 = "128";

    Console.Write(isPowerOf2(str1) +
                "\n"+isPowerOf2(str2) +
                "\n"+isPowerOf2(str3));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
/* PHP program to find whether a number is power of
    2 or not */

// returns 1 when str is power of 2
// return 0 when str is not a power of 2
function isPowerOf2($str)
{
    $len_str = strlen($str);

    // sum stores the intermediate dividend while
    // dividing.
    $num = 0;

    // if the input is "1" then return 0
    // because 2^k = 1 where k >= 1 and here k = 0
    if ($len_str == 1 && $str[$len_str - 1] == '1')
        return 0;

    // Divide the number until it gets reduced to 1
    // if we are successfully able to reduce the number
    // to 1 it means input string is power of two if in
    // between an odd number appears at the end it means
    // string is not divisible by two hence not a power
    // of 2.
    while ($len_str != 1 || $str[$len_str - 1] != '1')
    {

        // if the last digit is odd then string is not
        // divisible by 2 hence not a power of two
        // return 0.
        if (ord($str[$len_str - 1] - '0') % 2 == 1)
            return 0;

        // divide the whole string by 2\. i is used to
        // track index in current number. j is used to
        // track index for next iteration.
        $j=0;
        for ($i = 0; $i < $len_str; $i++)
        {
            $num = $num * 10 + (ord($str[$i]) - ord('0'));

            // if num < 2 then we have to take another digit
            // to the right of A[i] to make it bigger than
            // A[i]. E. g. 214 / 2 --> 107
            if ($num < 2)
            {

                // if it's not the first index. E.g 214
                // then we have to include 0.
                if ($i != 0)
                    $str[$j++] = '0';        

                // for eg. "124" we will not write 064
                // so if it is the first index just ignore
                continue;
            }

            $str[$j++] = chr((int)($num / 2) + ord('0'));
            $num = ($num) - (int)($num / 2) * 2;
        }

        // After every division by 2 the
        // length of string is changed.
        $len_str = $j;
    }

    // if the string reaches to 1 then the str is
    // a power of 2.
    return 1;
}

    // Driver code.
    $str1 = "124684622466842024680246842024662202000002";
    $str2 = "1";
    $str3 = "128";

    print(isPowerOf2($str1)."\n".isPowerOf2($str2)."\n".isPowerOf2($str3));

// This code is contributed by mits
?>

?>
```

**输出:**

```
0
0
1
```

**时间复杂度:** O(N^2)其中 n 是给定数字中的位数。

**方法 2:使用 boost 库**
Boost 库旨在广泛使用，并可用于广泛的应用领域。例如，在 C++中，它们有助于处理范围超过长双数据类型(264)的大数。

1.  将输入作为提升整数。
2.  使用位操作检查它是否是 2 的幂。

## C++

```
// C++ program to find whether a number
// is power of 2 or not
#include <bits/stdc++.h>
#include <boost/multiprecision/cpp_int.hpp>

using namespace std;
using namespace boost::multiprecision;

// Function to check whether a
// number is power of 2 or not
bool ispowerof2 ( cpp_int num )
{
    if ( ( num & ( num - 1 ) ) == 0 )
        return 1;
    return 0;   
}

// Driver function
int main()
{
    cpp_int num = 549755813888;
    cout << ispowerof2 ( num ) << endl;
    return 0;
} 

// This code is contributed by  Aditya Gupta 4
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// whether a number
// is power of 2 or not
class GfG
{

// Function to check whether a
// number is power of 2 or not
static long ispowerof2 ( long num )
{
    if ((num & (num - 1)) == 0)
        return 1;
    return 0;
}

// Driver code
public static void main(String[] args)
{
    long num = 549755813888L;
    System.out.println(ispowerof2(num));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find whether a number
# is power of 2 or not

# Function to check whether a
# number is power of 2 or not
def ispowerof2(num):

    if((num & (num - 1)) == 0):
        return 1
    return 0

# Driver function
if __name__=='__main__':
    num = 549755813888
    print(ispowerof2(num))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find
// whether a number
// is power of 2 or not
class GFG{
// Function to check whether a
// number is power of 2 or not
static long ispowerof2 ( long num )
{
    if ((num&(num-1)) == 0)
        return 1;
    return 0;
}

// Driver Code
public static void Main()
{
long num = 549755813888;
System.Console.WriteLine(ispowerof2(num));
}
}
// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// whether a number
// is power of 2 or not

// Function to check whether a
// number is power of 2 or not
function ispowerof2 ( $num )
{
    if (($num & ($num - 1 )) == 0)
        return 1;
    return 0;
}

// Driver Code
$num = 549755813888;
echo ispowerof2($num);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// whether a number
// is power of 2 or not

// Function to check whether a
// number is power of 2 or not
function ispowerof2(num)
{
    if ((num & (num - 1)) == 0)
        return 1;

    return 0;
}

// Driver code
var num = 549755813888;

document.write(ispowerof2(num));

// This code is contributed by Princi Singh

</script>
```

**输出:**

```
1
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*
**参考:**[https://www . boost . org/doc/libs/1 _ 61 _ 0/libs/multi precision/doc/html/index . html](https://www.boost.org/doc/libs/1_61_0/libs/multiprecision/doc/html/index.html)
如发现有不正确的地方，或想分享更多关于以上讨论话题的信息，请写评论。
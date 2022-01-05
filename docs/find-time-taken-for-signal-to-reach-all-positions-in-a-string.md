# 查找信号到达一个字符串中所有位置所需的时间

> 原文:[https://www . geesforgeks . org/find-信号到达字符串中所有位置所需的时间/](https://www.geeksforgeeks.org/find-time-taken-for-signal-to-reach-all-positions-in-a-string/)

给定一个由“x”和“o”组成的字符串。从每个“x”发出一个双向传播的信号。信号传输到下一个小区需要一个时间单位。如果一个单元格包含“o”，信号会将其更改为“x”。任务是计算将数组转换成信号串所需的时间。
一串信号中只包含‘x’。
**例:**

> 输入:s =“ooxooooo”
> 输出:3
> 输入:s =“ooxooooo”
> 输出:4

**来源** : [OYO 客房采访集 2](https://www.geeksforgeeks.org/oyo-rooms-interview-experience-set-2-for-fresher/)
想法是找出最长的连片‘o’的长度。还要检查，如果“x”出现在连续“o”的右侧和左侧，则时间周期将减少到最大长度的一半，否则时间周期将等于最大长度。
以下是上述方法的实施。

## C++

```
// C++ program to Find time taken for signal
// to reach all positions in a string
#include <bits/stdc++.h>
using namespace std;

// Returns time needed for signal to traverse
// through complete string.
int maxLength(string s, int n)
{
    int right = 0, left = 0;
    int coun = 0, max_length = INT_MIN;

    s = s + '1'; // for the calculation of last index
    // for strings like oxoooo, xoxxoooo ..

    for (int i = 0; i <= n; i++) {
        if (s[i] == 'o')
            coun++;

        else {

            // if coun is greater than max_length
            if (coun > max_length) {

                right = 0;
                left = 0;

                // if 'x' is present at the right side
                // of max_length
                if (s[i] == 'x')
                    right = 1;

                // if 'x' is present at left side of
                // max_length
                if (((i - coun) > 0) && (s[i - coun - 1] == 'x'))
                    left = 1;

                // We use ceiling function to handle odd
                // number 'o's
                coun = ceil((double)coun / (right + left));

                max_length = max(max_length, coun);
            }
            coun = 0;
        }
    }

    return max_length;
}

// Driver code
int main()
{
    string s = "oooxoooooooooxooo";
    int n = s.size();
    cout << maxLength(s, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find time taken for signal
// to reach all positions in a string
public class GFG {

    // Returns time needed for signal to traverse
    // through complete string.
    static int maxLength(String s, int n)
    {
        int right = 0, left = 0;
        int coun = 0, max_length = Integer.MIN_VALUE;

        s = s + '1'; // for the calculation of last index
        // for strings like oxoooo, xoxxoooo ..

        for (int i = 0; i <= n; i++) {
            if (s.charAt(i) == 'o')
                coun++;

            else {

                // if coun is greater than max_length
                if (coun > max_length) {

                    right = 0;
                    left = 0;

                    // if 'x' is present at the right side
                    // of max_length
                    if (s.charAt(i) == 'x')
                        right = 1;

                    // if 'x' is present at left side of
                    // max_length
                    if (((i - coun) > 0) && (s.charAt(i - coun - 1) == 'x'))
                        left = 1;

                    // We use ceiling function to handle odd
                    // number 'o's
                    coun = (int)Math.ceil((double)coun / (right + left));

                    max_length = Math.max(max_length, coun);
                }
                coun = 0;
            }
        }

        return max_length;
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "oooxoooooooooxooo";
        int n = s.length();
        System.out.println(maxLength(s, n));
    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 program to Find time taken for signal
# to reach all positions in a string
import sys
import math

# Returns time needed for signal
# to traverse through complete string.
def maxLength(s, n):
    right = 0
    left = 0
    coun = 0
    max_length = -(sys.maxsize-1)

    # for the calculation of last index
    s = s+'1'

    # for strings like oxoooo, xoxxoooo 
    for i in range(0, n + 1):
        if s[i]=='o':
            coun+= 1
        else:

            # if coun is greater than
            # max_length
            if coun>max_length:
                right = 0
                left = 0

                # if 'x' is present at the right side
                # of max_length
                if s[i]=='x':
                    right = 1

                # if 'x' is present at left side of
                # max_length
                if i-coun>0 and s[i-coun-1] == 'x':
                    left = 1

                # We use ceiling function to handle odd
                # number 'o's
                coun = math.ceil(float(coun/(right + left)))
                max_length = max(max_length, coun)
            coun = 0

    return max_length

# Driver code
if __name__=='__main__':
    s = "oooxoooooooooxooo"
    n = len(s)
    print(maxLength(s, n))

# This code is contributed by
# Shrikant13
```

## C#

```
// C# program to Find time taken
// for signal to reach all
// positions in a string
using System;

class GFG {

    // Returns time needed for signal
    // to traverse through complete string.
    static int maxLength(string s, int n)
    {
        int right = 0, left = 0;
        int coun = 0, max_length = int.MinValue;

        s = s + '1'; // for the calculation of last index

        // for strings like oxoooo, xoxxoooo ..
        for (int i = 0; i <= n; i++) {
            if (s[i] == 'o')
                coun++;

            else {

                // if coun is greater than max_length
                if (coun > max_length) {
                    right = 0;
                    left = 0;

                    // if 'x' is present at the right
                    // side of max_length
                    if (s[i] == 'x')
                        right = 1;

                    // if 'x' is present at left side
                    // of max_length
                    if (((i - coun) > 0) && (s[i - coun - 1] == 'x'))
                        left = 1;

                    // We use ceiling function to
                    // handle odd number 'o's
                    coun = (int)Math.Ceiling((double)coun / (right + left));

                    max_length = Math.Max(max_length, coun);
                }
                coun = 0;
            }
        }

        return max_length;
    }

    // Driver code
    public static void Main()
    {
        string s = "oooxoooooooooxooo";
        int n = s.Length;
        Console.Write(maxLength(s, n));
    }
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Find time taken for signal
// to reach all positions in a string

// Returns time needed for signal
// to traverse through complete string.
function maxLength($s, $n)
{
    $right = 0; $left = 0;
    $coun = 0;
    $max_length = PHP_INT_MIN;

    $s = $s . '1'; // for the calculation of last index
                   // for strings like oxoooo, xoxxoooo ..

    for ($i = 0; $i <= $n; $i++)
    {
        if ($s[$i] == 'o')
            $coun++;

        else
        {

            // if coun is greater than max_length
            if ($coun > $max_length)
            {

                $right = 0;
                $left = 0;

                // if 'x' is present at the right side
                // of max_length
                if ($s[$i] == 'x')
                    $right = 1;

                // if 'x' is present at left side of
                // max_length
                if ((($i - $coun) > 0) &&
                    ($s[$i - $coun - 1] == 'x'))
                    $left = 1;

                // We use ceiling function to handle odd
                // number 'o's
                $coun = (int)ceil((double)$coun / ($right +
                                                   $left));

                $max_length = max($max_length, $coun);
            }
            $coun = 0;
        }
    }

    return $max_length;
}

// Driver code
$s = "oooxoooooooooxooo";
$n = strlen($s);
echo(maxLength($s, $n));

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript program to Find time taken for signal
// to reach all positions in a string

// Returns time needed for signal to traverse
// through complete string.
function maxLength( s, n)
{
    var right = 0, left = 0;
    var coun = 0, max_length = Number.MIN_VALUE;

    s = s + '1'; // for the calculation of last index
    // for strings like oxoooo, xoxxoooo ..

    for (var i = 0; i <= n; i++) {
        if (s[i] == 'o')
            coun++;

        else {

            // if coun is greater than max_length
            if (coun > max_length) {

                right = 0;
                left = 0;

                // if 'x' is present at the right side
                // of max_length
                if (s[i] == 'x')
                    right = 1;

                // if 'x' is present at left side of
                // max_length
                if (((i - coun) > 0) && (s[i - coun - 1] == 'x'))
                    left = 1;

                // We use ceiling function to handle odd
                // number 'o's
                coun = Math.ceil(coun / (right + left));

                max_length = Math.max(max_length, coun);
            }
            coun = 0;
        }
    }

    return max_length;
}

var s = "oooxoooooooooxooo";
var n = s.length;
document.write( maxLength(s, n));

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
5
```
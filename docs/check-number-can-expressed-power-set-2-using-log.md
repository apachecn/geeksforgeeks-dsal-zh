# 检查一个数字是否可以用幂表示|设置 2(使用对数)

> 原文:[https://www . geesforgeks . org/check-number-can-expressed-power-set-2-use-log/](https://www.geeksforgeeks.org/check-number-can-expressed-power-set-2-using-log/)

检查给定一个正整数 n，一个数是否可以表示为 x^y (x 升到 y 的幂)
，找出它是否可以表示为 x^y，其中 y > 1 和 x > 0。x 和 y 都是整数。
**例:**

```
Input:  n = 8
Output: true
8 can be expressed as 2^3

Input:  n = 49
Output: true
49 can be expressed as 7^2

Input:  n = 48
Output: false
48 can't be expressed as x^y
```

我们在下面的帖子中讨论了两种不同的方法。
[检查一个数是否可以表示为 x^y (x 的幂为 y)](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-xy-x-raised-to-power-y/) 。
思路是从 2 到 n 的平方根在不同的基数上求 Log n，如果一个基数的 Log n 变成整数，那么结果为真，否则结果为假。

## C++

```
// CPP program to find if a number
// can be expressed as x raised to
// power y.
#include <bits/stdc++.h>
using namespace std;

bool isPower(unsigned int n)
{
    // Find Log n in different bases
    // and check if the value is an
    // integer
    for (int x=2; x<=sqrt(n); x++) {
        float f = log(n) / log(x);
        if ((f - (int)f) == 0.0)
            return true;       
    }
    return false;
}

// Driver code
int main()
{
    for (int i = 2; i < 100; i++)
        if (isPower(i))
            cout << i << "  ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number
// can be expressed as x raised to
// power y.
class GFG {

    static boolean isPower(int n)
    {
        // Find Log n in different
        // bases and check if the
        // value is an integer
        for (int x = 2; x <=
               (int)Math.sqrt(n); x++)
        {
            float f = (float)Math.log(n) /
                      (float) Math.log(x);

            if ((f - (int)f) == 0.0)
                return true;    
        }
        return false;
    }

    // Driver code
    public static void main(String args[])
    {
        for (int i = 2; i < 100; i++)
            if (isPower(i))
                System.out.print( i + " ");
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python3 program to find if a number
# can be expressed as x raised to
# power y.
import math

def isPower(n):

    # Find Log n in different
    # bases and check if the
    # value is an integer
    for x in range(2,int(math.sqrt(n)) + 1):

        f = math.log(n) / math.log(x);
        if ((f - int(f)) == 0.0):
            return True;    

    return False;

# Driver code
for i in range(2, 100):
    if (isPower(i)):
        print(i, end = " ");

# This code is contributed by mits
```

## C#

```
// C# program to find if a number
// can be expressed as x raised to
// power y.
using System;

class GFG
{
    static bool isPower(int n)
    {
        // Find Log n in different
        // bases and check if the
        // value is an integer
        for (int x = 2;
                 x <= (int)Math.Sqrt(n); x++)
        {
            float f = (float)Math.Log(n) /
                      (float) Math.Log(x);
            if ((f - (int)f) == 0.0)
                return true;    
        }
        return false;
    }
    // Driver Code
    public static void Main()
    {
        for (int i = 2; i < 100; i++)
            if (isPower(i))
                Console.Write( i + " ");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a number
// can be expressed as x raised to
// power y.

function isPower($n)
{
    // Find Log n in different
    // bases and check if the
    // value is an integer
    for ($x = 2; $x <= sqrt($n); $x++)
    {
        $f = log($n) / log($x);
        if (($f - (int)$f) == 0.0)
            return true;    
    }
    return false;
}

// Driver code
for ($i = 2; $i < 100; $i++)
    if (isPower((int)$i))
        echo $i." ";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// javascript program to find if a number
// can be expressed as x raised to
// power y.
function isPower(n) {
        // Find Log n in different
        // bases and check if the
        // value is an integer
        for (x = 2; x <= parseInt( Math.sqrt(n)); x++)
        {
            var f =  Math.log(n) /  Math.log(x);

            if ((f - parseInt( f)) == 0.0)
                return true;
        }
        return false;
    }

    // Driver code

        for (i = 2; i < 100; i++)
            if (isPower(i))
                document.write(i + " ");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
4  8  9  16  25  27  32  36  49  64  81
```
# 起伏的数字

> 原文:[https://www.geeksforgeeks.org/undulating-numbers/](https://www.geeksforgeeks.org/undulating-numbers/)

一个[起伏数字](https://en.wikipedia.org/wiki/Undulating_number)是一个只有两种数字类型且交替数字相同的数字，也就是说，它的形式是“ababab…”。有时仅限于非平凡起伏的数字，要求至少有 3 位数字，a 不等于 b。

> 前几个这样的数字是:101、121、131、141、151、161、171、181、191、202、212、232、242、252、262、272、282、292、303、313、323、343、353、363、373、383、393、404、414、424

1.  对于任意 n >= 3，有 9 × 9 = 81 个非平凡的 n 位起伏数字，因为第一个数字可以有 9 个值(不能是 0)，当第二个数字必须不同于第一个数字时，它可以有 9 个值。

给定一个数字，考虑到交替数字的定义，检查它是否是波动数字，至少 3 个数字和相邻数字不相同。
示例:

```
Input : n = 121
Output : Yes

Input : n = 1991
Output : No
```

## C++

```
// C++ program to check whether a number
// is undulating or not
#include <bits/stdc++.h>
using namespace std;

bool isUndulating(string n)
{
    // Considering the definition
    // with restriction that there
    // should be at least 3 digits
    if (n.length() <= 2)
       return false;

    // Check if all alternate digits are
    // same or not.
    for (int i = 2; i < n.length(); i++)
        if (n[i - 2] != n[i])
           false;

    return true;
}

int main()
{
    string n = "1212121";
    if (isUndulating(n))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether a number
// is undulating or not
import java.util.*;

class GFG {

    public static boolean isUndulating(String n)
    {

        // Considering the definition
        // with restriction that there
        // should be at least 3 digits
            if (n.length() <= 2)
                return false;

        // Check if all alternate digits are
        // same or not.
        for (int i = 2; i < n.length(); i++)
            if (n.charAt(i-2) != n.charAt(i))
                return false;

        return true;
    }

    // Driver code
    public static void main (String[] args)
    {

        String n = "1212121";

        if (isUndulating(n)==true)
            System.out.println("yes");
        else
            System.out.println("no");
    }
}

// This code is contributed by akash1295.
```

## 蟒蛇 3

```
# Python3 program to check whether a
# number is undulating or not

def isUndulating(n):

    # Considering the definition
    # with restriction that there
    # should be at least 3 digits
    if (len(n) <= 2):
        return False

    # Check if all alternate digits
    # are same or not.
    for i in range(2, len(n)):
        if (n[i - 2] != n[i]):
            return False

    return True

# Driver Code
n = "1212121"
if (isUndulating(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to check whether a number
// is undulating or not
using System;

class GFG {

    public static bool isUndulating(string n)
    {

        // Considering the definition
        // with restriction that there
        // should be at least 3 digits
            if (n.Length <= 2)
                return false;

        // Check if all alternate digits are
        // same or not.
        for (int i = 2; i < n.Length; i++)
            if (n[i-2] != n[i])
                return false;

        return true;
    }

    // Driver code
    public static void Main ()
    {

        string n = "1212121";

        if (isUndulating(n)==true)
            Console.WriteLine("yes");
        else
            Console.WriteLine("no");
    }
}

// This code is contributed by Vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether a
// number is undulating or not

function isUndulating($n)
{

    // Considering the definition
    // with restriction that there
    // should be at least 3 digits
    if (strlen($n) <= 2)
        return false;

    // Check if all alternate
    // digits are same or not.
    for ($i = 2; $i < strlen($n); $i++)
        if ($n[$i - 2] != $n[$i])
            false;

    return true;
}

// Driver code
$n = "1212121";
if (isUndulating($n))
    echo("Yes");
else
    echo("No");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program tto check whether a number
// is undulating or not

    function isUndulating(n)
    {

        // Considering the definition
        // with restriction that there
        // should be at least 3 digits
            if (n.length <= 2)
                return false;

        // Check if all alternate digits are
        // same or not.
        for (let i = 2; i < n.length; i++)
            if (n[i-2] != n[i])
                return false;

        return true;
    }

// Driver Code

        let n = "1212121";

        if (isUndulating(n)==true)
            document.write("Yes");
        else
            document.write("No");

</script>
```

**Output:** 

```
Yes
```
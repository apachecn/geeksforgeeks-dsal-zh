# 检查给定数的所有旋转是否大于或等于给定数

> 原文:[https://www . geesforgeks . org/check-给定数字的所有旋转是否大于或等于给定数字/](https://www.geeksforgeeks.org/check-whether-all-the-rotations-of-a-given-number-is-greater-than-or-equal-to-the-given-number-or-not/)

给定一个整数 *x* ，任务是找出元素上的每个 k 周期移位是否产生一个大于或等于同一元素的数。
整数 *x* 的 k 循环移位是一个移除 *x* 的最后一个 *k* 位并将它们插入其开头的函数。
例如 *123* 的 k-循环移位为 *k=1* 的 *312* 和 *k=2* 的 *231* 。如果满足给定条件，则打印*是*，否则打印*否*。
**举例:**

> **输入:** x = 123
> **输出:**是
> k = 1 时 123 的 k-循环位移为 312，k=2 时为 231。
> 312 和 231 都大于 123。
> **输入:** 2214
> **输出:**否
> k = 2 时 2214 的 k-循环移位为 1422，小于 2214

**方法:**只需找出该数所有可能的 k 次循环移位，检查是否都大于给定数。
以下是上述办法的实施情况:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

void CheckKCycles(int n, string s)
{
    bool ff = true;
    int x = 0;
    for (int i = 1; i < n; i++)
    {

        // Splitting the number at index i
        // and adding to the front
        x = (s.substr(i) + s.substr(0, i)).length();

        // Checking if the value is greater than
        // or equal to the given value
        if (x >= s.length())
        {
            continue;
        }
        ff = false;
        break;
    }
    if (ff)
    {
        cout << ("Yes");
    }
    else
    {
        cout << ("No");
    }
}

// Driver code
int main()
{
    int n = 3;
    string s = "123";
    CheckKCycles(n, s);
    return 0;
}

/* This code contributed by Rajput-Ji */
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static void CheckKCycles(int n, String s)
    {
        boolean ff = true;
        int x = 0;
        for (int i = 1; i < n; i++)
        {

            // Splitting the number at index i
            // and adding to the front
            x = (s.substring(i) + s.substring(0, i)).length();

            // Checking if the value is greater than
            // or equal to the given value
            if (x >= s.length())
            {
                continue;
            }
            ff = false;
            break;
        }
        if (ff)
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }

    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3;
        String s = "123";
        CheckKCycles(n, s);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 计算机编程语言

```
# Python3 implementation of the approach
def CheckKCycles(n, s):
    ff = True
    for i in range(1, n):

        # Splitting the number at index i
        # and adding to the front
        x = int(s[i:] + s[0:i])

        # Checking if the value is greater than
        # or equal to the given value
        if (x >= int(s)):
            continue
        ff = False
        break
    if (ff):
        print("Yes")
    else:
        print("No")

n = 3
s = "123"
CheckKCycles(n, s)
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static void CheckKCycles(int n, String s)
    {
        bool ff = true;
        int x = 0;
        for (int i = 1; i < n; i++)
        {

            // Splitting the number at index i
            // and adding to the front
            x = (s.Substring(i) + s.Substring(0, i)).Length;

            // Checking if the value is greater than
            // or equal to the given value
            if (x >= s.Length)
            {
                continue;
            }
            ff = false;
            break;
        }
        if (ff)
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }

    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 3;
        String s = "123";
        CheckKCycles(n, s);
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

function CheckKCycles($n, $s)
{
    $ff = true;
    $x = 0;
    for ($i = 1; $i < $n; $i++)
    {

        // Splitting the number at index i
        // and adding to the front
        $x = strlen(substr($s, $i).substr($s, 0, $i));

        // Checking if the value is greater than
        // or equal to the given value
        if ($x >= strlen($s))
        {
            continue;
        }
        $ff = false;
        break;
    }
    if ($ff)
    {
        print("Yes");
    }
    else
    {
        print("No");
    }
}

// Driver code
$n = 3;
$s = "123";
CheckKCycles($n, $s);

// This code contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript implementation of the approach
function CheckKCycles(n, s)
{
    var ff = true;
    var x = 0;
    for (i = 1; i < n; i++)
    {

        // Splitting the number at index i
        // and adding to the front
        x = (s.substring(i) + s.substring(0, i)).length;

        // Checking if the value is greater than
        // or equal to the given value
        if (x >= s.length)
        {
            continue;
        }
        ff = false;
        break;
    }
    if (ff)
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }
}

// Driver code
    var n = 3;
    var s = "123";
    CheckKCycles(n, s);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
Yes
```
# 检查给定的浮点数是偶数还是奇数

> 原文:[https://www . geesforgeks . org/check-是否给定-浮点数-偶数-奇数/](https://www.geeksforgeeks.org/check-whether-given-floating-point-number-even-odd/)

给定一个浮点数，检查它是偶数还是奇数。
我们可以通过最后一位数字除以 2 来检查一个整数是偶数还是奇数。但是在浮点数的情况下，我们不能仅仅通过将其最后一个数字除以 2 来检查给定的数字是偶数还是奇数。例如，100.70 是一个奇数，但是它的最后一个数字可以被 2 整除。
示例:

```
Input : 100.7
Output : odd

Input : 98.8
Output : even

Input : 100.70
Output : odd
Trailing 0s after dot do not matter.
```

**进场:**

*   我们从一个数字的最低有效位开始遍历它，直到得到一个非零数字或“.”
*   如果这个数能被 2 整除，它就是偶数，否则就是奇数
*   如果是“.”这意味着数字的小数部分被遍历，现在我们可以通过将数字除以 2 来检查数字是偶数还是奇数，无论它是 0 还是非零数字。

下面是上述方法的实现:

## C++

```
// CPP program to check whether given floating
// point number is even or odd
#include <bits/stdc++.h>
using namespace std;

// Function to check even or odd.
bool isEven(string s)
{
    int l = s.length();

    // Loop to traverse number from LSB
    bool dotSeen = false;
    for (int i = l - 1; i >= 0; i--) {

        // We ignore trailing 0s after dot
        if (s[i] == '0' && dotSeen == false)
            continue;

        // If it is '.' we will check next digit and it
        // means decimal part is traversed.
        if (s[i] == '.') {
            dotSeen = true;
            continue;
        }

        // If digit is divisible by 2
        // means even number.
        if ((s[i] - '0') % 2 == 0)
            return true;

        return false;
    }
}

// Driver Function
int main()
{
    string s = "100.70";
    if (isEven(s))
        cout << "Even";
    else
        cout << "Odd";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether given floating
// point number is even or odd
import java.util.*;
import java.lang.*;

public class GfG {

    // Function to check even or odd.
    public static boolean isEven(String s1)
    {
        int l = s1.length();
        char[] s = s1.toCharArray();

        // Loop to traverse number from LSB
        boolean dotSeen = false;
        for (int i = l - 1; i >= 0; i--) {

            // We ignore trailing 0s after dot
            if (s[i] == '0' && dotSeen == false)
                continue;

            // If it is '.' we will check next digit and it
            // means decimal part is traversed.
            if (s[i] == '.') {
                dotSeen = true;
                continue;
            }

            // If digit is divisible by 2
            // means even number.
            if ((s[i] - '0') % 2 == 0)
                return true;

            return false;
        }

        return false;
    }

    // Driver function
    public static void main(String argc[])
    {
        String s = "100.70";
        if (isEven(s))
            System.out.println("Even");
        else
            System.out.println("Odd");
    }
}
/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# Python 3 program to check
# whether given floating
# point number is even or odd

# Function to check
# even or odd.
def isEven(s) :

    l = len(s)

    # Loop to traverse
    # number from LSB
    dotSeen = False
    for i in range(l - 1, -1, -1 ) :

        # We ignore trailing
        # 0s after dot
        if (s[i] == '0'
           and dotSeen == False) :
             continue

        # If it is '.' we will
        # check next digit and it
        # means decimal part is
        # traversed.
        if (s[i] == '.') :
            dotSeen = True
              continue

        # If digit is
        # divisible by 2
        # means even number.
        if ((int)(s[i]) % 2 == 0) :
              return True

        return False     

# Driver Function
s = "100.70"
if (isEven(s)) :
    print("Even")
else :
    print("Odd")

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to check whether given floating
// point number is even or odd
using System;

public class GfG {

    // Function to check even or odd.
    public static bool isEven(string s1)
    {
        int l = s1.Length;

        // char[] s = s1.toCharArray();

        // Loop to traverse number from LSB
        bool dotSeen = false;
        for (int i = l - 1; i >= 0; i--) {

            // We ignore trailing 0s after dot
            if (s1[i] == '0' && dotSeen == false)
                continue;

            // If it is '.' we will check next
            // digit and it means decimal part
            // is traversed.
            if (s1[i] == '.') {
                dotSeen = true;
                continue;
            }

            // If digit is divisible by 2
            // means even number.
            if ((s1[i] - '0') % 2 == 0)
                return true;

            return false;
        }

        return false;
    }

    // Driver function
    public static void Main()
    {
        string s1 = "100.70";

        if (isEven(s1))
            Console.WriteLine("Even");
        else
            Console.WriteLine("Odd");
    }
}

/* This code is contributed by Vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// whether given floating
// point number is even or odd

// Function to check
// even or odd.
function isEven($s)
{
    $l = strlen($s);

    // Loop to traverse
    // number from LSB
    $dotSeen = false;
    for ($i = $l - 1; $i >= 0; $i--)
    {

        // We ignore trailing
        // 0s after dot
        if ($s[$i] == '0' && $dotSeen == false)
        continue;

        // If it is '.' we will
        // check next digit and it
        // means decimal part is
        // traversed.
        if ($s[$i] == '.')
        {
            $dotSeen = true;
            continue;
        }

        // If digit is divisible by 2
        // means even number.
        if (($s[$i] - '0') % 2 == 0)
            return true;

        return false;    
    }
}

    // Driver Code
    $s = "100.70";
    if (isEven($s))
    echo "Even";
    else
    echo "Odd";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to check
// whether given floating
// point number is even or odd

// Function to check
// even or odd.
function isEven(s)
{
    let l = s.length;

    // Loop to traverse
    // number from LSB
    let dotSeen = false;
    for (let i = l - 1; i >= 0; i--)
    {

        // We ignore trailing
        // 0s after dot
        if (s[i] == '0' && dotSeen == false)
        continue;

        // If it is '.' we will
        // check next digit and it
        // means decimal part is
        // traversed.
        if (s[i] == '.')
        {
            dotSeen = true;
            continue;
        }

        // If digit is divisible by 2
        // means even number.
        if ((s[i] - '0') % 2 == 0)
            return true;

        return false;   
    }
}

    // Driver Code
    let s = "100.70";
    if (isEven(s))
    document.write("Even");
    else
    document.write("Odd");

// This code is contributed by gfgking

</script>
```

**输出:**

```
odd
```

***时间复杂度:** O(|s|)*

***辅助空间:** O(1)*
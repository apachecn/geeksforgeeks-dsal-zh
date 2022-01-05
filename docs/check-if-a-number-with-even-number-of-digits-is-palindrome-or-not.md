# 检查偶数位数的数字是否回文

> 原文:[https://www . geesforgeks . org/check-if-a-number-with-number-of-digits-is-回文-or-not/](https://www.geeksforgeeks.org/check-if-a-number-with-even-number-of-digits-is-palindrome-or-not/)

给定一个包含偶数位数的数字 **N** 。任务是检查那个数字是否是[回文](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)。
**举例:**

```
Input: N = 123321
Output: Palindrome

Input: 1234
Output: Not palindrome
```

一种**天真的方法**是从该数字的前后遍历，并在它们不匹配的地方停止。
一个**有效的方法**是使用下面的事实:

> **位数为**偶数**的回文数字**总是能被 11 整除。

假设数字为 **d1 d2 d3 d4…dn** ，其中 **d1，d2，d3..**是数字的**位**。如果是回文，那么 d1 = dn，d2 = dn-1，d3 = dn-2…..等等。现在由于 11 的**可除性规定一个数字**的交替数字之和的**差应该是**零**，并且在回文有偶数个数字的情况下也是一样的，即** 

> D1+D3++dn-1 = D2+D4+D6++dn

所以，一个**数字**的**偶数**的**回文数字**总是可以被 11 整除的**。**

## C++

```
// C++ program to find number is palindrome
// or not without using any extra space
#include <bits/stdc++.h>
using namespace std;

// Function to check if the number is palindrome
bool isPalindrome(int n)
{
    // if divisible by 11 then true
    if (n % 11 == 0) {
        return true;
    }

    // if not divisible by 11
    return false;
}

// Driver code
int main()
{
    isPalindrome(123321) ? cout << "Palindrome"
                         : cout << "Not Palindrome";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number
// is palindrome or not without
// using any extra space
class GFG
{
    // Function to check if the
    // number is palindrome
    static boolean isPalindrome(int n)
    {
        // if divisible by 11 then true
        if (n % 11 == 0)
        {
            return true;
        }

        // if not divisible by 11
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        System.out.println(isPalindrome(123321) ?
                                   "Palindrome" :
                               "Not Palindrome");
    }
}

// This code is contributed by Bilal
```

## 蟒蛇 3

```
# Python 3 program to find number is palindrome
# or not without using any extra space.

# Function to check if the number is palindrome
def isPalindrome(n) :

    # if divisible by 11 then return True
    if n % 11 == 0 :
        return True

    # if not divisible by 11 then return False
    return False

# Driver code
if __name__ == "__main__" :

    n = 123321

    if isPalindrome(n) :
        print("Palindrome")
    else :
        print("Not Palindrome")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find number
// is palindrome or not without
// using any extra space
using System;

class GFG
{
    // Function to check if the
    // number is palindrome
    static bool isPalindrome(int n)
    {
        // if divisible by
        // 11 then true
        if (n % 11 == 0)
        {
            return true;
        }

        // if not divisible by 11
        return false;
    }

    // Driver code
    public static void Main()
    {
        Console.Write(isPalindrome(123321) ?
                              "Palindrome" :
                          "Not Palindrome");
    }
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// is palindrome or not without
// using any extra space

// Function to check if the
// number is palindrome
function isPalindrome($n)
{
    // if divisible by
    // 11 then true
    if ($n % 11 == 0)
    {
        return true;
    }

    // if not divisible by 11
    return false;
}

// Driver code
echo isPalindrome(123321) ?
             "Palindrome" :
          "Not Palindrome";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find number
// is palindrome or not without
// using any extra space

    // Function to check if the
    // number is palindrome
    function isPalindrome(n)
    {
        // if divisible by 11 then true
        if (n % 11 == 0)
        {
            return true;
        }

        // if not divisible by 11
        return false;
    }

    // Driver code
    document.write(isPalindrome(123321) ?
            "Palindrome" :
        "Not Palindrome");

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
Palindrome
```
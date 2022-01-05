# 检查一个号码是否为鸭号

> 原文:[https://www . geesforgeks . org/check-what-number-duck-number-not/](https://www.geeksforgeeks.org/check-whether-number-duck-number-not/)

鸭号是一个正数，其中有零，例如 3210，8050896，70709 都是鸭号。请注意，只有前导 0 的数字不被视为鸭号。例如，像 035 或 0012 这样的数字不被认为是鸭号。像 01203 这样的数字被认为是 Duck，因为其中有一个非前导 0。

**示例:**

> 输入:707069
> 输出:是鸭号。
> 说明:707069 开头不含零。
> 
> 输入:02364
> 输出:不是鸭号。
> 说明:02364 中，数字的开头有一个零。

## C++

```
// C++ Program to check whether
// a number is Duck Number or not.
#include <iostream>
using namespace std;

// Function to check whether
// given number is duck number or not.
bool check_duck(string num)
{
    // Ignore leading 0s
    int i = 0, n = num.length();
    while (i < n && num[i] == '0')
        i++;

    // Check remaining digits
    while (i < n) {
        if (num[i] == '0')
            return true;
        i++;
    }

    return false;
}

// Driver Method
int main(void)
{
    string num = "1023";
    if (check_duck(num))
        cout << "It is a duck number\n";
    else
        cout << "It is not a duck number\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check whether a
// number is Duck Number or not.

import java.io.*;
class GFG {

    // Function to check whether
    // the given number is duck number or not.
    static boolean check_duck(String num)
    {
        // Ignore leading 0s
        int i = 0, n = num.length();
        while (i < n && num.charAt(i) == '0')
            i++;

        // Check remaining digits
        while (i < n) {
            if (num.charAt(i) == '0')
                return true;
            i++;
        }

        return false;
    }

    // Driver Method
    public static void main(String args[]) throws IOException
    {
        String num = "1023";
        if (check_duck(num))
            System.out.println("It is a duck number");
        else
            System.out.println("It is not a duck number");
    }
}
```

## 计算机编程语言

```
# Python program to check whether a number is Duck Number or not.

# Function to check whether
# the given number is duck number or not.
def check_duck(num) :

    # Length of the number(number of digits)
    n = len(num)

    # Ignore leading 0s
    i = 0
    while (i < n and num[i] == '0') :
        i = i + 1

    # Check remaining digits
    while (i < n) :
        if (num[i] == "0") :
            return True
        i = i + 1

    return False

# Driver Method
num1 = "1023"
if(check_duck(num1)) :
    print "It is a duck number"
else :
    print "It is not a duck number"

# Write Python3 code here
```

## C#

```
// C# Program to check whether a
// number is Duck Number or not.
using System;

class GFG {

    // Function to check whether
    // the given number is duck
    // number or not.
    static bool check_duck( String num)
    {

        // Ignore leading 0s
        int i = 0, n = num.Length;
        while (i < n && num[i] == '0')
            i++;

        // Check remaining digits
        while (i < n) {
            if (num[i] == '0')
                return true;
            i++;
        }

        return false;
    }

    // Driver Method
    public static void Main()
    {

        String num1 = "1023";

        // checking number1
        if( check_duck(num1))
            Console.Write("It is a "
                      + "duck number");
        else
            Console.Write("It is not "
                    + "a duck number");
    }
}

// This code is contributed by
// nitin mittal.
```

## java 描述语言

```
<script>

// Javascript program to check whether
// a number is Duck Number or not.

// Function to check whether
// given number is duck number or not.
function check_duck(num)
{

    // Ignore leading 0s
    let i = 0, n = num.length;
    while (i < n && num[i] == '0')
        i++;

    // Check remaining digits
    while (i < n)
    {
        if (num[i] == '0')
            return true;

        i++;
    }
    return false;
}

// Driver code
let num = "1023";

if (check_duck(num))
    document.write("It is a duck number");
else
    document.write("It is not a duck number");

// This code is contributed by rishavmahato348

</script>
```

**输出:**

```
It is a duck number.
```

本文由**尼基塔·蒂瓦里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
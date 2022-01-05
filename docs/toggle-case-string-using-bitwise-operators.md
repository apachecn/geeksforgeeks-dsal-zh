# 使用按位运算符切换字符串的大小写

> 原文:[https://www . geeksforgeeks . org/toggle-case-string-use-bitwise-operator/](https://www.geeksforgeeks.org/toggle-case-string-using-bitwise-operators/)

给定一个字符串，编写一个函数，使用按位运算符返回字符串的切换大小写。
在 [ASCII](http://www.asciitable.com/) 代码中，字符‘A’是整数 65 = (0100 0001)2，而字符‘A’是整数 97 = (0110 0001)2。同样，字符“D”是整数 68 = (0100 0100)2，而字符“D”是整数 100 = (0110 0100)2。

我们可以看到，在“A”和“A”的 ASCII 码中，只有第六个最低有效位不同。类似的行为可以在“D”和“D”的 ASCII 代码中看到。因此，我们需要切换该位来切换大小写。

**示例:**

```
Input : "GeekSfOrgEEKs"
Output : "gEEKsFoRGeekS"                  

Input : "StRinG"
Output : "sTrINg"
```

[ASCII 表](http://www.asciitable.com/)的构造方式是小写字母的二进制表示与大写字母的二进制表示几乎相同。

**切换情况**
第 6 个 LSB 为 1 的整数为 32 (0010 0000)。因此，字符 32 的按位 XORing 将切换字符的第 6 个 LSB，从而切换其大小写。如果字符是大写，它将被转换成小写，反之亦然。

## C++

```
// C++ program to get toggle case of a string
#include <bits/stdc++.h>
using namespace std;

// tOGGLE cASE = swaps CAPS to lower
// case and lower case to CAPS
char *toggleCase(char *a)
{
    for(int i = 0; a[i] != '\0'; i++)
    {

        // Bitwise EXOR with 32
        a[i] ^= 32;
    }
    return a;
}

// Driver Code
int main()
{
    char str[] = "CheRrY";
    cout << "Toggle case: "
         << toggleCase(str) << endl;
    cout << "Original string: "
         << toggleCase(str) << endl;
    return 0;
}

// This code is contributed by noob2000
```

## C

```
// C program to get toggle case of a string
#include <stdio.h>

// tOGGLE cASE = swaps CAPS to lower
// case and lower case to CAPS
char *toggleCase(char *a)
{
    for (int i=0; a[i]!='\0'; i++) {

        // Bitwise EXOR with 32
        a[i] ^= 32;
    }

    return a;
}

// Driver Code
int main()
{
    char str[] = "CheRrY";
    printf("Toggle case: %s\n", toggleCase(str));
    printf("Original string: %s", toggleCase(str));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// program to get toggle case of a string

public class Test
{

    static int x=32;

    // tOGGLE cASE = swaps CAPS to lower
    // case and lower case to CAPS
    static String toggleCase(char[] a)
    {
        for (int i=0; i<a.length; i++) {

            // Bitwise EXOR with 32
            a[i]^=32;
        }
        return new String(a);
    }

    /* Driver program */
    public static void main(String[] args)
    {
        String str = "CheRrY";
        System.out.print("Toggle case: ");
        str = toggleCase(str.toCharArray());
        System.out.println(str);

        System.out.print("Original string: ");
        str = toggleCase(str.toCharArray());
        System.out.println(str);   
    }
}
```

## 蟒蛇 3

```
# Python3 program to get toggle case of a string
x = 32;

# tOGGLE cASE = swaps CAPS to lower
# case and lower case to CAPS
def toggleCase(a):

    for i in range(len(a)):

        # Bitwise EXOR with 32
        a = a[:i] + chr(ord(a[i]) ^ 32) + a[i + 1:];
    return a;

# Driver Code
str = "CheRrY";
print("Toggle case: ", end = "");
str = toggleCase(str);
print(str);

print("Original string: ", end = "");
str = toggleCase(str);
print(str);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to get toggle case of a string
using System;

class GFG {

    // tOGGLE cASE = swaps CAPS to lower
    // case and lower case to CAPS
    static string toggleCase(char []a)
    {
        for (int i = 0; i < a.Length; i++)
        {

            // Bitwise EXOR with 32
            a[i] ^= (char)32;
        }

        return new string(a);
    }

    /* Driver program */
    public static void Main()
    {
        string str = "CheRrY";
        Console.Write("Toggle case: ");
        str = toggleCase(str.ToCharArray());
        Console.WriteLine(str);

        Console.Write("Original string: ");
        str = toggleCase(str.ToCharArray());
        Console.Write(str);
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>
// program to get toggle case of a string 
x = 32;

// tOGGLE cASE = swaps CAPS to lower
// case and lower case to CAPS
function toggleCase(a)
{
    for (i = 0; i < a.length; i++)
    {

        // Bitwise EXOR with 32
        a[i] = String.fromCharCode(a[i].charCodeAt(0)^32);
    }
    return a.join("");;
}

/* Driver program */
var str = "CheRrY";
document.write("Toggle case: ");
str = toggleCase(str.split(''));
document.write(str);

document.write("<br>Original string: ");
str = toggleCase(str.split(''));
document.write(str); 

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
Toggle case: cHErRy
Original string: CheRrY
```

感谢库马尔·高拉夫改进了解决方案。
**类似文章:**
[**在 C/C++**](https://www.geeksforgeeks.org/case-conversion-lower-upper-vice-versa-string-using-bitwise-operators-cc/)
中使用 BitWise 运算符进行字符串的 Case 转换本文由[**Sanjay Kumar Ulsha**](https://www.linkedin.com/in/sanjayulsha)来自 [**海得拉巴 JNTUH 工程学院**](http://jntuhceh.ac.in/) 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
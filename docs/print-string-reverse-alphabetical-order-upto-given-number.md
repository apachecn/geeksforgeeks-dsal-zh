# 找到一个字符串，使得每个字符在字典上大于它紧接的下一个字符

> 原文:[https://www . geesforgeks . org/print-string-reverse-字母顺序-up-给定-number/](https://www.geeksforgeeks.org/print-string-reverse-alphabetical-order-upto-given-number/)

给定一个整数 N，任务是找到一个长度为(N+1)的字符串(仅考虑小写字符)，使得任意位置的字符在字典上应大于其紧接的下一个字符。
**例:**

```
Input: 2
Output: cba
c is greater than b and
b is greater than a

Input: 5
Output: fedcba
```

**进场:**

1.  以相反的顺序声明一个包含所有字母的字符串。
2.  用 26 取给定数的模。因此，如果该值小于 26，运行从**26 –(模数值+ 1)** 到 25 的循环，转到字符串的索引并打印该索引。
3.  如果模数值大于 0，则用 26 除模数值，然后循环到 0 到 25，并根据给定的计算值打印字符串的每个元素。

以下是上述方法的实现:

## C++

```
// C++ program to print a string in reverse
// alphabetical order upto given number
#include <bits/stdc++.h>
using namespace std;

// Function that prints the required string
string printString(int n, string str)
{
    string str2 = "";

    // Find modulus with 26
    int extraChar = n % 26;

    // Print extra characters required
    if (extraChar >= 1) {
        for (int i = 26 - (extraChar + 1); i <= 25; i++)
            str2 += str[i];
    }
    int countOfStr = n / 26;

    // Print the given reverse string countOfStr times
    for (int i = 1; i <= countOfStr; i++) {
        for (int j = 0; j < 26; j++)
            str2 += str[j];
    }
    return str2;
}

// Driver Code
int main()
{
    int n = 30;

    // Initialize a string in reverse order
    string str = "zyxwvutsrqponmlkjihgfedcba";

    cout << printString(n, str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print a String in reverse
// alphabetical order upto given number

class GFG {

// Function that prints the required String
    static String printString(int n, String str) {
        String str2 = "";

        // Find modulus with 26
        int extraChar = n % 26;

        // Print extra characters required
        if (extraChar >= 1) {
            for (int i = 26 - (extraChar + 1); i <= 25; i++) {
                str2 += str.charAt(i);
            }
        }
        int countOfStr = n / 26;

        // Print the given reverse String countOfStr times
        for (int i = 1; i <= countOfStr; i++) {
            for (int j = 0; j < 26; j++) {
                str2 += str.charAt(j);
            }
        }
        return str2;
    }

// Driver Code
    public static void main(String[] args) {
        int n = 30;

        // Initialize a String in reverse order
        String str = "zyxwvutsrqponmlkjihgfedcba";
        System.out.println(printString(n, str));
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python 3 program to print a
# string in reverse alphabetical
# order upto given number

# Function that prints the
# required string
def printString(n, str):

    str2 = ""

    # Find modulus with 26
    extraChar = n % 26

    # Print extra characters required
    if (extraChar >= 1) :
        for i in range( 26 - (extraChar + 1), 26):
            str2 += str[i]

    countOfStr = n // 26

    # Print the given reverse
    # string countOfStr times
    for i in range(1, countOfStr + 1) :
        for j in range(26):
            str2 += str[j]
    return str2

# Driver Code
if __name__ == "__main__":
    n = 30

    # Initialize a string in
    # reverse order
    str = "zyxwvutsrqponmlkjihgfedcba"

    print(printString(n, str))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to print a String in reverse
// alphabetical order upto given number
using System;
public class GFG {

// Function that prints the required String
    static String printString(int n, String str) {
        String str2 = "";

        // Find modulus with 26
        int extraChar = n % 26;

        // Print extra characters required
        if (extraChar >= 1) {
            for (int i = 26 - (extraChar + 1); i <= 25; i++) {
                str2 += str[i];
            }
        }
        int countOfStr = n / 26;

        // Print the given reverse String countOfStr times
        for (int i = 1; i <= countOfStr; i++) {
            for (int j = 0; j < 26; j++) {
                str2 += str[j];
            }
        }
        return str2;
    }

// Driver Code
    public static void Main() {
        int n = 30;

        // Initialize a String in reverse order
        String str = "zyxwvutsrqponmlkjihgfedcba";
        Console.Write(printString(n, str));
    }
}

// This code is contributed by Rajput-JI
```

## java 描述语言

```
<script>
      // JavaScript program to print a string in reverse
      // alphabetical order upto given number

      // Function that prints the required string
      function printString(n, str) {
        var str2 = "";

        // Find modulus with 26
        var extraChar = n % 26;

        // Print extra characters required
        if (extraChar >= 1) {
          for (var i = 26 - (extraChar + 1); i <= 25; i++) str2 += str[i];
        }
        var countOfStr = parseInt(n / 26);

        // Print the given reverse string countOfStr times
        for (var i = 1; i <= countOfStr; i++) {
          for (var j = 0; j < 26; j++) str2 += str[j];
        }
        return str2;
      }

      // Driver Code
      var n = 30;

      // Initialize a string in reverse order
      var str = "zyxwvutsrqponmlkjihgfedcba";
      document.write(printString(n, str));

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
edcbazyxwvutsrqponmlkjihgfedcba
```

本文由 [**萨赫勒拉吉普特**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
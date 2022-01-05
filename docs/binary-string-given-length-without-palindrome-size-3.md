# 给定长度的二进制字符串，没有大小为 3 的回文

> 原文:[https://www . geesforgeks . org/binary-string-给定长度-不带回文-size-3/](https://www.geeksforgeeks.org/binary-string-given-length-without-palindrome-size-3/)

给定一个整数 n。找到一个由“a”和“b”组成的字符串，使该字符串不包含任何长度为 3 的回文。
**例:**

```
Input : 3
Output : "aab"
Explanation:
aab is not a palindrome.

Input : 5
Output : aabba
Explanation:
aabba does not contain a palindrome
of size 3.
```

这里的方法是，我们可以使用这个字符串' aabb '并根据给定的整数打印字符串的字符。

```
We need to make make sure that every third 
character is different.

If we perform operation AND on i and 2 where
i = 0 to any positive integer. It will generate
a pattern 0, 0, 2, 2, 0, 0, 2, 2,... 
0 AND 2 = 0
1 AND 2 = 0
2 AND 2 = 2
3 AND 2 = 2
4 AND 2 = 0 //repeat the pattern.
```

下面是上述方法的代码。

## C++

```
// CPP program find a binary string of
// given length that doesn't contain
// a palindrome of size 3.
#include <bits/stdc++.h>
using namespace std;

void generatestring(int n)
{
    // Printing the character according to i
    for (int i = 0; i < n; i++)
        putchar(i & 2 ? 'b' : 'a');
    puts("");
}

// Driver code
int main()
{
    int n = 5;
    generatestring(n);
    n = 8;
    generatestring(n);
    n = 10;
    generatestring(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program find a binary String of
// given length that doesn't contain
// a palindrome of size 3.

class GFG
{

static void generateString(int n)
{
    String s = "";

    // Printing the character according to i
    for (int i = 0; i < n; i++)
        s += ((i & 2) > 1 ? 'b' : 'a');
    System.out.println(s);
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    generateString(n);
    n = 8;
    generateString(n);
    n = 10;
    generateString(n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program find a binary String of
# given length that doesn't contain
# a palindrome of size 3.
def generateString(n):
    s = "";

    # Printing the character according to i
    for i in range(n):
        if((i & 2) > 1):
            s += 'b';
        else:
            s += 'a';
    print(s);

# Driver code
if __name__ == '__main__':

    n = 5;
    generateString(n);
    n = 8;
    generateString(n);
    n = 10;
    generateString(n);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program find a binary String of
// given length that doesn't contain
// a palindrome of size 3.
using System;

class GFG
{

static void generateString(int n)
{
    String s = "";

    // Printing the character according to i
    for (int i = 0; i < n; i++)
        s += ((i & 2) > 1 ? 'b' : 'a');
    Console.WriteLine(s);
}

// Driver code
public static void Main(String[] args)
{
    int n = 5;
    generateString(n);
    n = 8;
    generateString(n);
    n = 10;
    generateString(n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program find a binary String of
// given length that doesn't contain
// a palindrome of size 3.

function generateString(n)
{
    var s = "";

    // Printing the character according to i
    for (var i = 0; i < n; i++)
        s += ((i & 2) > 1 ? 'b' : 'a');
    document.write(s + "<br>");
}

// Driver code
var n = 5;
generateString(n);
n = 8;
generateString(n);
n = 10;
generateString(n);

</script>
```

**输出:**

```
aabba
aabbaabb
aabbaabbaa
```
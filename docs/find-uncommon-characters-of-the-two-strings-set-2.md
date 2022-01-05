# 查找两个字符串的不常见字符|集合 2

> 原文:[https://www . geesforgeks . org/find-两个字符串中不常见的字符-set-2/](https://www.geeksforgeeks.org/find-uncommon-characters-of-the-two-strings-set-2/)

给定两个字符串， **str1** 和 **str2** ，任务是在不使用额外空间的情况下，按排序顺序查找并打印两个给定字符串的不常见字符。在这里，一个不常见的字符意味着该字符要么出现在一个字符串中，要么出现在另一个字符串中，但不能同时出现在两个字符串中。字符串只包含小写字符，可以包含重复字符。

**示例:**

> **输入:** str1 =“字符”，str2 =“字母”
> T3】输出: b c l p r
> 
> **输入:** str1 =“极客之怪”，str2 =“极客之怪”
> T3】输出: f i o q r u z

**方法:**使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)的方法已经在[这里](https://www.geeksforgeeks.org/find-uncommon-characters-two-strings/)讨论过了。这个问题也可以通过使用位操作来解决。
该方法使用 2 个变量，存储每个字符的 ASCII 码为-97 的左移位 1 的位或，即 0 代表“a”，1 代表“b”，依此类推。对于这两个字符串，我们在执行这些逐位操作后得到一个整数。现在，这两个整数的异或运算将只在表示不常见字符的位置给出二进制位 1。打印这些位置的字符值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the uncommon
// characters in the given string
// in sorted order
void printUncommon(string str1, string str2)
{
    int a1 = 0, a2 = 0;
    for (int i = 0; i < str1.length(); i++) {

        // Converting character to ASCII code
        int ch = int(str1[i]) - 'a';

        // Bit operation
        a1 = a1 | (1 << ch);
    }
    for (int i = 0; i < str2.length(); i++) {

        // Converting character to ASCII code
        int ch = int(str2[i]) - 'a';

        // Bit operation
        a2 = a2 | (1 << ch);
    }

    // XOR operation leaves only uncommon
    // characters in the ans variable
    int ans = a1 ^ a2;

    int i = 0;
    while (i < 26) {
        if (ans % 2 == 1) {
            cout << char('a' + i);
        }
        ans = ans / 2;
        i++;
    }
}

// Driver code
int main()
{
    string str1 = "geeksforgeeks";
    string str2 = "geeksquiz";

    printUncommon(str1, str2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to print the uncommon
    // characters in the given string
    // in sorted order
    static void printUncommon(String str1, String str2)
    {
        int a1 = 0, a2 = 0;
        for (int i = 0; i < str1.length(); i++)
        {

            // Converting character to ASCII code
            int ch = (str1.charAt(i)) - 'a';

            // Bit operation
            a1 = a1 | (1 << ch);
        }
        for (int i = 0; i < str2.length(); i++)
        {

            // Converting character to ASCII code
            int ch = (str2.charAt(i)) - 'a';

            // Bit operation
            a2 = a2 | (1 << ch);
        }

        // XOR operation leaves only uncommon
        // characters in the ans variable
        int ans = a1 ^ a2;

        int i = 0;
        while (i < 26)
        {
            if (ans % 2 == 1)
            {
                System.out.print((char) ('a' + i));
            }
            ans = ans / 2;
            i++;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String str1 = "geeksforgeeks";
        String str2 = "geeksquiz";

        printUncommon(str1, str2);
    }
}

// This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the uncommon
// characters in the given string
// in sorted order
static void printUncommon(string str1, string str2)
{
    int a1 = 0, a2 = 0;
    for (int i = 0; i < str1.Length; i++)
    {

        // Converting character to ASCII code
        int ch = (str1[i] - 'a');

        // Bit operation
        a1 = a1 | (1 << ch);
    }
    for (int i = 0; i < str2.Length; i++)
    {

        // Converting character to ASCII code
        int ch = (str2[i] - 'a');

        // Bit operation
        a2 = a2 | (1 << ch);
    }

    // XOR operation leaves only uncommon
    // characters in the ans variable
    int ans = a1 ^ a2;

    int j = 0;
    while (j < 26)
    {
        if (ans % 2 == 1)
        {
            Console.Write((char)('a' + j));
        }
        ans = ans / 2;
        j++;
    }
}

// Driver code
public static void Main()
{
    string str1 = "geeksforgeeks";
    string str2 = "geeksquiz";

    printUncommon(str1, str2);

}
}

// This code is contributed by SoM15242
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the uncommon
# characters in the given string
# in sorted order
def printUncommon(str1, str2) :

    a1 = 0; a2 = 0;

    for i in range(len(str1)) :

        # Converting character to ASCII code
        ch = ord(str1[i]) - ord('a');

        # Bit operation
        a1 = a1 | (1 << ch);

    for i in range(len(str2)) :

        # Converting character to ASCII code
        ch = ord(str2[i]) - ord('a');

        # Bit operation
        a2 = a2 | (1 << ch);

    # XOR operation leaves only uncommon
    # characters in the ans variable
    ans = a1 ^ a2;

    i = 0;
    while (i < 26) :
        if (ans % 2 == 1) :
            print(chr(ord('a') + i),end="");

        ans = ans // 2;
        i += 1;

# Driver code
if __name__ == "__main__" :

    str1 = "geeksforgeeks";
    str2 = "geeksquiz";

    printUncommon(str1, str2);

    # This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the uncommon
// characters in the given string
// in sorted order
function printUncommon(str1, str2)
{
    var a1 = 0, a2 = 0;
    for (var i = 0; i < str1.length; i++) {

        // Converting character to ASCII code
        var ch = (str1[i].charCodeAt(0)) - 'a'.charCodeAt(0);

        // Bit operation
        a1 = a1 | (1 << ch);
    }
    for (var i = 0; i < str2.length; i++) {

        // Converting character to ASCII code
        var ch = (str2[i].charCodeAt(0)) - 'a'.charCodeAt(0);

        // Bit operation
        a2 = a2 | (1 << ch);
    }

    // XOR operation leaves only uncommon
    // characters in the ans variable
    var ans = a1 ^ a2;

    var i = 0;
    while (i < 26) {
        if (ans % 2 == 1) {
            document.write( String.fromCharCode('a'.charCodeAt(0) + i));
        }
        ans = parseInt(ans / 2);
        i++;
    }
}

// Driver code
var str1 = "geeksforgeeks";
var str2 = "geeksquiz";
printUncommon(str1, str2);

</script>
```

**Output:** 

```
fioqruz
```

时间复杂度:O(|str1| + |str2| + 26)辅助空间:O(1)
# 构造一个长度为 L 的字符串，这样长度为 X 的每个子串都有正好 Y 个不同的字母

> 原文:[https://www . geesforgeks . org/construct-a-string-length-l-so-每个长度为-x-的子串都有-y-distinct-字母/](https://www.geeksforgeeks.org/construct-a-string-of-length-l-such-that-each-substring-of-length-x-has-exactly-y-distinct-letters/)

给定字符串 l 的**长度**、子串 x 的**长度**以及长度为 x 的子串必须具有的不同字符数为 y，任务是找到长度为 l 的字符串，其中长度为 x 的每个子串都具有 y 个不同字符。
**例:**

> **输入:** l = 6，x = 5，y = 3
> **输出:**abcbc
> **解释:**
> 如果我们取前五个字符的一个子串，那么这个子串就是“abcab”。
> 子串中正好有三个不同的字符(a、b、c)。
> 同样，如果我们从长度为 5 的字符串中提取任何子字符串，那么它将有
> 正好 3 个不同的字符。
> **输入:** l = 3，x = 1，y = 1
> **输出:** aaa
> **解释:**
> 如果我们取长度为 1 的子串，那么它正好有 1 个不同的字符。

**方法:**
要解决上面提到的问题，我们按照下面给出的步骤进行:

*   将变量 p 初始化为 97，标记小写字母“a”的 ASCII 值。
*   继续增加 p 的值，直到 y 个字符。
*   然后从第一个字符开始重复该字符，直到它的长度等于给定字符串的长度，并返回最后一个字符串。

以下是上述方法的实现:

## C++

```
// C++ implementation to
// construct a string of length L
// such that each substring of length
// X has exactly Y distinct letters.
#include <iostream>
using namespace std;

void String(int l, int x, int y)
{
    // Initialize p equal to the ASCII value of a
    int p = 97;

    // Iterate till the length of the string
    for(int j = 0; j < l ; j++)
    {
        char ans = (char)(p + (j % y));
        cout << ans;
    }
}

// Driver code
int main ()
{
    int l = 6;
    int x = 5;
    int y = 3;
    String(l, x, y) ;
    return 0;
}

// This code is contributed by AnkitRai01
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// construct a string of length L
// such that each substring of length
// X has exactly Y distinct letters.

public class GFG {

    static void string(int l, int x, int y){

        // Initialize p equal to the ASCII value of a
        int p = 97;

        // Iterate till the length of the string
        for(int j = 0; j < l ; j++){

            char ans = (char)(p + (j % y));
            System.out.print(ans);
        }

    }

    // Driver code
    public static void main (String[] args) {
    int l = 6;
    int x = 5;
    int y = 3;
    string(l, x, y) ;
        }
}
// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python implementation to
# construct a string of length L
# such that each substring of length
# X has exactly Y distinct letters.

def String(l, x, y):
    # Initialize p equal to the ASCII value of a
    p = 97

    # Iterate till the length of the string
    for j in range(l):

        ans = chr(p + j % y)
        print(ans, end ="")

# Driver code
l = 6
x = 5
y = 3
String(l, x, y)
```

## C#

```
// C# implementation to
// construct a string of length L
// such that each substring of length
// X has exactly Y distinct letters.
using System;

class GFG {
    static void String(int l, int x, int y)
    {
        // Initialize p equal to the ASCII value of a
        int p = 97;

        // Iterate till the length of the string
        for(int j = 0; j < l; j++)
        {
            char ans = (char)(p + (j % y));
            Console.Write(ans);
        }
    }

    // Driver code
    public static void Main(string[] args)
    {
        int l = 6;
        int x = 5;
        int y = 3;
        String(l, x, y);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// javascript implementation to
// construct a string of length L
// such that each substring of length
// X has exactly Y distinct letters.

function string(l , x , y){

    // Initialize p equal to the ASCII value of a
    var p = 97;

    // Iterate till the length of the string
    for(var j = 0; j < l ; j++){

        var ans = String.fromCharCode(p + (j % y));
        document.write(ans);
    }

}

// Driver code
var l = 6;
var x = 5;
var y = 3;
string(l, x, y) ;

// This code contributed by shikhasingrajput
</script>
```

**Output:** 

```
abcabc
```

时间复杂度:O(l)

辅助空间:0(1)
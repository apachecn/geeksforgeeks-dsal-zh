# 将连续的字符一起打印成一行

> 原文:[https://www . geesforgeks . org/print-continuous-characters-together-line/](https://www.geeksforgeeks.org/print-consecutive-characters-together-line/)

给定一个字符序列，在一行中打印连续的字符序列，否则
在新的一行中打印。

**示例:**

```
Input  : ABCXYZACCD
Output : ABC
         XYZ
         A
         C
         CD

Input : ABCZYXACCD
Output: ABC
        ZYX
        A
        C
        CD
```

想法是从左到右遍历字符串。对于每个遍历的字符，如果它与前一个字符连续，则打印一行，否则打印一个新的行字符。

## C++

```
// C++ program to print consecutive characters
// together in a line.
#include <iostream>
using namespace std;

void print(string str)
{
    cout << str[0];
    for (int i=1; str[i]!='\0'; i++)
    {
        if ((str[i] == str[i-1]+1) ||
            (str[i] == str[i-1]-1))
            cout << str[i];
        else
            cout << "\n" << str[i];;
    }
}

// Driver code
int main()
{
    string str = "ABCXYZACCD";
    print(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print consecutive characters
// together in a line.
class GFG {

    static void print(String str1) {
        char str[] = str1.toCharArray();
        System.out.print(str[0]);
        for (int i = 1; i < str.length; i++) {
            if ((str[i] == str[i - 1] + 1)
                    || (str[i] == str[i - 1] - 1)) {
                System.out.print(str[i]);
            } else {
                System.out.print("\n" + str[i]);
            }
        }
    }

// Driver code
    public static void main(String[] args) {
        String str = "ABCXYZACCD";
        print(str);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to print consecutive characters
# together in a line.
def _print(string):
    print(string[0], end = "")

    for i in range(1, len(string)):
        if (ord(string[i]) == ord(string[i - 1]) + 1 or
            ord(string[i]) == ord(string[i - 1]) - 1):
            print(string[i], end = "")
        else:
            print()
            print(string[i], end = "")

# Driver Code
if __name__ == "__main__":

    string = "ABCXYZACCD"
    _print(string)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to print consecutive characters
// together in a line.
using System;

class GFG
{

    static void print(String str1)
    {
        char []str = str1.ToCharArray();
        Console.Write(str[0]);
        for (int i = 1; i < str.Length; i++)
        {
            if ((str[i] == str[i - 1] + 1)
                    || (str[i] == str[i - 1] - 1))
            {
                Console.Write(str[i]);
            }
            else
            {
                Console.Write("\n" + str[i]);
            }
        }
    }

    // Driver code
    public static void Main()
    {
        String str = "ABCXYZACCD";
        print(str);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to print consecutive
// characters together in a line.
function print(str1)
{
    let str = str1.split("");
    document.write(str[0]);

    for(let i = 1; i < str.length; i++)
    {
        if ((str[i].charCodeAt(0) ==
         str[i - 1].charCodeAt(0) + 1) ||
            (str[i].charCodeAt(0) ==
         str[i - 1].charCodeAt(0) - 1))
        {
            document.write(str[i]);
        }
        else
        {
            document.write("<br>" + str[i]);
        }
    }
}

// Driver code
let str = "ABCXYZACCD";
print(str);

// This code is contributed by rag2127

</script>
```

**输出:**

```
ABC
XYZ
A
C
CD
```

**时间复杂度:** O(n)

本文由**拉克什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
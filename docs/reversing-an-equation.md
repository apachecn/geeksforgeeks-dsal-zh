# 反转方程式

> 原文:[https://www.geeksforgeeks.org/reversing-an-equation/](https://www.geeksforgeeks.org/reversing-an-equation/)

给定一个使用数字/变量和+、-、*、/的数学方程。反向打印等式。

**示例:**

```
Input : 20 - 3 + 5 * 2
Output : 2 * 5 + 3 - 20

Input : 25 + 3 - 2 * 11
Output : 11 * 2 - 3 + 25

Input : a + b * c - d / e
Output : e / d - c * b + a
```

**方法:**解决这个问题的方法很简单。我们从左到右迭代字符串，一旦碰到一个符号，我们就在结果字符串的开头插入数字和符号。

## C++

```
// C++ program to reverse an equation
#include <bits/stdc++.h>
using namespace std;

// Function to reverse order of words
string reverseEquation(string s)
{
    // Resultant string
    string result;
    int j = 0;
    for (int i = 0; i < s.length(); i++) {

        // A space marks the end of the word
        if (s[i] == '+' || s[i] == '-' ||
            s[i] == '/' || s[i] == '*') {

            // insert the word at the beginning
            // of the result string
            result.insert(result.begin(),
                s.begin() + j, s.begin() + i);
            j = i + 1;

            // insert the symbol
            result.insert(result.begin(), s[i]);
        }
    }

    // insert the last word in the string
    // to the result string
    result.insert(result.begin(), s.begin() + j,
                                     s.end());
    return result;
}

// driver code
int main()
{
    string s = "a+b*c-d/e";
    cout << reverseEquation(s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse an equation
import java.util.*;

class GFG{

// Function to reverse order of words
public static String reverseEquation(String s)
{

    // Resultant string
    String result = "", str = "";
    int j = 0;

    for(int i = 0; i < s.length(); i++)
    {

        // A space marks the end of the word
        if (s.charAt(i) == '+' ||
            s.charAt(i) == '-' ||
            s.charAt(i) == '/' ||
            s.charAt(i) == '*')
        {

            // Insert the word at the beginning
            // of the result string
            result = s.charAt(i) + str + result;
            str = "";
        }
        else
        {
            str += s.charAt(i);
        }
    }
    result = str + result;
    return result;
}

// Driver code
public static void main(String args[])
{
    String s = "a+b*c-d/e";

    System.out.println(reverseEquation(s));
}
}

// This code is contributed by bolliranadheer
```

## 蟒蛇 3

```
# Python3 Program to reverse an equation
# Function to reverse order of words
def reverseEquation(s):

    # Reverse String
    result=""
    for i in range(len(s)):

        # A space marks the end of the word
        if(s[i]=='+' or s[i]=='-' or s[i]=='/' or s[i]=='*'):

            # insert the word at the beginning
            # of the result String
            result = s[i] + result

        # insert the symbol
        else:
            result = s[i] + result
    return result

# Driver Code
s = "a+b*c-d/e"
print(reverseEquation(s))

# This code is contributed by simranjenny84
```

**输出:**

```
e/d-c*b+a
```

本文由 **Raghav Sharma** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
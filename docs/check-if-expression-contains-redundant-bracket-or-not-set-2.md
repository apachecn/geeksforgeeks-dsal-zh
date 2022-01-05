# 检查表达式是否包含多余的括号|设置 2

> 原文:[https://www . geeksforgeeks . org/check-if-expression-contains-redundant-方括号-or-not-set-2/](https://www.geeksforgeeks.org/check-if-expression-contains-redundant-bracket-or-not-set-2/)

给定一串平衡表达式，查找它是否包含多余的括号。如果同一个子表达式被不必要的或多个括号包围，则一组括号是多余的。如果多余，则打印“是”，否则打印“否”。
**注:**表达式可能包含 **'+'** 、**' ***、**'–'**、**/'**运算符。给定的表达式有效，并且没有空格。
**注:**问题意在 O(1)额外空间解决。
**举例:**

> **输入:** ((a+b))
> **输出:** YES
> ((a+b)】可以减少到(a+b)
> **输入:** (a+(b)/c)
> **输出:** YES
> (a+(b)/c)可以减少到(a+b/c)，因为 b 被()包围，这是多余的
> **输入:** (a+b*(c)

**方法:**
这个想法与[上一篇文章](https://www.geeksforgeeks.org/expression-contains-redundant-bracket-not/)中讨论的想法非常相似，但是在这里代替 stack，我们正在计算符号(**'+**，**' ***，**'–'**和 **'/'** )以及表达式中使用的括号总数。
如果括号的计数不等于符号的计数，那么函数将返回 false。

## C++

```
// C++ program to check for/
// redundant braces in the string
#include <iostream>
using namespace std;

// Function to check for
// redundant braces
bool IsRedundantBraces(string A)
{
    // count of no of signs
    int a = 0, b = 0;
    for (int i = 0; i < A.size(); i++) {
        if (A[i] == '('
            && A[i + 2] == ')')
            return 1;
        if (A[i] == '*'
            || A[i] == '+'
            || A[i] == '-'
            || A[i] == '/')
            a++;
        if (A[i] == '(')
            b++;
    }
    if (b > a)
        return 1;
    return 0;
}

// Driver function
int main()
{
    string A = "(((a+b) + c) + d)";
    if (IsRedundantBraces(A)) {
        cout << "YES\n";
    }
    else {
        cout << "NO";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check for
// redundant braces in the string
class GFG
{

    // Function to check for
    // redundant braces
    static boolean IsRedundantBraces(String A)
    {
        // count of no of signs
        int a = 0, b = 0;
        for (int i = 0; i < A.length(); i++)
        {
            if (A.charAt(i) == '(' &&  
                A.charAt(i + 2) == ')')
                return true;

            if (A.charAt(i) == '*' ||
                A.charAt(i) == '+' ||
                A.charAt(i) == '-' ||
                A.charAt(i) == '/')
                a++;
            if (A.charAt(i) == '(')
                b++;
        }
        if (b > a)
            return true;
        return false;
    }

    // Driver Code
    public static void main (String[] args)
    {
        String A = "(((a+b) + c) + d)";
        if (IsRedundantBraces(A))
        {
            System.out.println("YES");
        }
        else
        {
            System.out.println("NO");
        }
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to check for/
# redundant braces in the string

# Function to check for
# redundant braces
def IsRedundantBraces(A):

    # count of no of signs
    a, b = 0, 0;
    for i in range(len(A)):
        if (A[i] == '(' and A[i + 2] == ')'):
            return True;
        if (A[i] == '*' or A[i] == '+' or
            A[i] == '-' or A[i] == '/'):
            a += 1;
        if (A[i] == '('):
            b += 1;

    if (b > a):
        return True;
    return False;

# Driver Code
if __name__ == '__main__':
    A = "(((a+b) + c) + d)";
    if (IsRedundantBraces(A)):
        print("YES");

    else:
        print("NO");

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to check for
// redundant braces in the string
using System;

class GFG
{

// Function to check for
// redundant braces
static bool IsRedundantBraces(string A)
{
    // count of no of signs
    int a = 0, b = 0;
    for (int i = 0; i < A.Length; i++)
    {
        if (A[i] == '(' && A[i + 2] == ')')
            return true;
        if (A[i] == '*' || A[i] == '+' ||
            A[i] == '-' || A[i] == '/')
            a++;
        if (A[i] == '(')
            b++;
    }
    if (b > a)
        return true;
    return false;
}

// Driver Code
public static void Main (String[] args)
{
    String A = "(((a+b) + c) + d)";
    if (IsRedundantBraces(A))
    {
        Console.WriteLine("YES");
    }
    else
    {
        Console.WriteLine("NO");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript program to check for
    // redundant braces in the string

    // Function to check for
    // redundant braces
    function IsRedundantBraces(A)
    {
        // count of no of signs
        let a = 0, b = 0;
        for (let i = 0; i < A.length; i++)
        {
            if (A[i] == '(' && A[i + 2] == ')')
                return true;
            if (A[i] == '*' || A[i] == '+' ||
                A[i] == '-' || A[i] == '/')
                a++;
            if (A[i] == '(')
                b++;
        }
        if (b > a)
            return true;
        return false;
    }

    let A = "(((a+b) + c) + d)";
    if (IsRedundantBraces(A))
    {
        document.write("YES");
    }
    else
    {
        document.write("NO");
    }

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
NO
```
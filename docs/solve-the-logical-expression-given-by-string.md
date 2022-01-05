# 求解字符串给出的逻辑表达式

> 原文:[https://www . geesforgeks . org/求解由字符串给出的逻辑表达式/](https://www.geeksforgeeks.org/solve-the-logical-expression-given-by-string/)

给定字符串 **str** 表示由运算符 **|(或)**、 **&(与)**、**组成的逻辑表达式！(NOT)** 、 **0** 、 **1** 和**、**仅适用(即字符间无空格)。任务是打印逻辑表达式的结果。
**举例:**

> **输入:**str =[[0，&，1]，|，[！，1]]"
> **输出:** 0
> [[0，&，1]，|， **[！，1]**
> [[0，&，1]，|， **0** ]
> [ **[0，&，1]** ，|，0]
> [ **0** ，|，0]
> **[0，|，0]**
> [**0**]
> **0**，[[0，&，[！,1]],|,[!,[[!，0]，&，1]]]”
> **输出:** 1

**进场:**

1.  从末尾开始解开绳子。
2.  如果找到**[**]，转到步骤 3，否则将字符推入堆栈。

4.  对向量元素执行相应的操作，然后将结果推回到堆栈中。
5.  如果字符串被完全遍历，则返回堆栈顶部的值，否则转到步骤 2。

以下是上述方法的实现:

## C++

```
// C++ program to solve the logical expression.
#include <bits/stdc++.h>
using namespace std;

// Function to evaluate the logical expression
char logicalExpressionEvaluation(string str)
{
    stack<char> arr;

    // traversing string from the end.
    for (int i = str.length() - 1; i >= 0; i--)
    {
        if (str[i] == '[')
        {
            vector<char> s;
            while (arr.top() != ']')
            {
                s.push_back(arr.top());
                arr.pop();
            }
            arr.pop();

            // for NOT operation
            if (s.size() == 3)
            {
                s[2] == '1' ? arr.push('0') : arr.push('1');
            }
            // for AND and OR operation
            else if (s.size() == 5)
            {
                int a = s[0] - 48, b = s[4] - 48, c;
                s[2] == '&' ? c = a && b : c = a || b;
                arr.push((char)c + 48);
            }
        }
        else
        {
            arr.push(str[i]);
        }
    }
    return arr.top();
}

// Driver code
int main()
{
    string str = "[[0,&,1],|,[!,1]]";

    cout << logicalExpressionEvaluation(str) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve the logical expression.
import java.util.*;

class GFG
{

// Function to evaluate the logical expression
static char logicalExpressionEvaluation(String str)
{
    Stack<Character> arr = new Stack<Character>();

    // traversing string from the end.
    for (int i = str.length() - 1; i >= 0; i--)
    {
        if (str.charAt(i) == '[')
        {
            Vector<Character> s = new Stack<Character>();
            while (arr.peek() != ']')
            {
                s.add(arr.peek());
                arr.pop();
            }
            arr.pop();

            // for NOT operation
            if (s.size() == 3)
            {
                arr.push(s.get(2) == '1' ? '0' : '1');
            }

            // for AND and OR operation
            else if (s.size() == 5)
            {
                int a = s.get(0) - 48,
                    b = s.get(4) - 48, c;
                if(s.get(2) == '&' )
                {
                    c = a & b;
                }
                else
                {
                    c = a | b;
                }
                arr.push((char)(c + 48));
            }
        }
        else
        {
            arr.push(str.charAt(i));
        }
    }
    return arr.peek();
}

// Driver code
public static void main(String[] args)
{
    String str = "[|,[&,1,[!,0]],[!,[|,[|,1,0],[!,1]]]]";

    System.out.println(logicalExpressionEvaluation(str));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to solve the
# logical expression.
import math as mt

# Function to evaluate the logical expression
def logicalExpressionEvaluation(string):

    arr = list()

    # traversing string from the end.
    n = len(string)
    for i in range(n - 1, -1, -1):
        if (string[i] == "["):

            s = list()

            while (arr[-1] != "]"):
                s.append(arr[-1])
                arr.pop()

            arr.pop()

            # for NOT operation
            if (len(s) == 3):
                if s[2] == "1":
                    arr.append("0")
                else:
                    arr.append("1")

            # for AND and OR operation
            elif (len(s) == 5):
                a = int(s[0]) - 48
                b = int(s[4]) - 48
                c = 0
                if s[2] == "&":
                    c = a & b
                else:
                    c = a | b
                arr.append((c) + 48)

        else:
            arr.append(string[i])

    return arr[-1]

# Driver code
string= "[|,[&,1,[!,0]],[!,[|,[|,1,0],[!,1]]]]"

print(logicalExpressionEvaluation(string))

# This code is contributed
# by mohit kumar 29
```

## C#

```
// C# program to solve the logical expression.
using System;
using System.Collections.Generic;

public class GFG
{

// Function to evaluate the logical expression
static char logicalExpressionEvaluation(String str)
{
    Stack<char> arr = new Stack<char>();

    // traversing string from the end.
    for (int i = str.Length - 1; i >= 0; i--)
    {
        if (str[i] == '[')
        {
            List<char> s = new List<char>();
            while (arr.Peek() != ']')
            {
                s.Add(arr.Peek());
                arr.Pop();
            }
            arr.Pop();

            // for NOT operation
            if (s.Count == 3)
            {
                arr.Push(s[2] == '1' ? '0' : '1');
            }

            // for AND and OR operation
            else if (s.Count == 5)
            {
                int a = s[0] - 48,
                    b = s[4] - 48, c;
                if(s[2] == '&' )
                {
                    c = a & b;
                }
                else
                {
                    c = a | b;
                }
                arr.Push((char)(c + 48));
            }
        }
        else
        {
            arr.Push(str[i]);
        }
    }
    return arr.Peek();
}

// Driver code
public static void Main(String[] args)
{
    String str = "[[0,&,1],|,[!,1]]";

    Console.WriteLine(logicalExpressionEvaluation(str));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to solve the logical expression.

// Function to evaluate the logical expression
function logicalExpressionEvaluation(str)
{
    let arr = [];

    // traversing string from the end.
    for (let i = str.length - 1; i >= 0; i--)
    {
        if (str[i] == '[')
        {
            let s = [];
            while (arr[arr.length-1] != ']')
            {
                s.push(arr[arr.length-1]);
                arr.pop();
            }
            arr.pop();

            // for NOT operation
            if (s.length == 3)
            {
                arr.push(s[2] == '1' ? '0' : '1');
            }

            // for AND and OR operation
            else if (s.length == 5)
            {
                let a = s[0].charCodeAt(0) - 48,
                    b = s[4].charCodeAt(0) - 48, c;

                if(s[2] == '&' )
                {
                    c = a & b;
                }
                else
                {
                    c = a | b;
                }
                arr.push(String.fromCharCode(c + 48));
            }
        }
        else
        {
            arr.push(str[i]);
        }
    }

    return arr[arr.length-1];
}

// Driver code
let str = "[|,[&,1,[!,0]],[!,[|,[|,1,0],[!,1]]]]";
document.write(logicalExpressionEvaluation(str));

// This code is contributed by patel2127
</script>
```

**Output**

```
0
```

**时间复杂度:** O(n)这里，n 是字符串的长度。
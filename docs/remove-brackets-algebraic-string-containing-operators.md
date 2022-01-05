# 删除包含+和–运算符的代数字符串中的括号

> 原文:[https://www . geesforgeks . org/remove-方括号-代数-包含字符串-运算符/](https://www.geeksforgeeks.org/remove-brackets-algebraic-string-containing-operators/)

简化给定的代数字符串，'+'、'-'运算符和括号。输出不带括号的简化字符串。
**例:**

```
Input : "(a-(b+c)+d)"
Output : "a-b-c+d"

Input : "a-(b-c-(d+e))-f"
Output : "a-b+c+d+e-f" 
```

其思想是在括号开始之前，即在字符“(”之前检查运算符。如果运算符为-，我们需要切换括号内的所有运算符。使用仅存储两个整数 0 和 1 的堆栈来指示是否切换。
我们对输入字符串的每个字符进行迭代。最初将 0 推入堆栈。每当字符是运算符('+'或'-')时，检查堆栈顶部。如果栈顶为 0，则在结果字符串中追加相同的运算符。如果堆栈顶部为 1，则在结果字符串中追加另一个运算符(如果“+”追加“-”)。

## C++

```
// C++ program to simplify algebraic string
#include <bits/stdc++.h>
using namespace std;

// Function to simplify the string
char* simplify(string str)
{
    int len = str.length();

    // resultant string of max length equal
    // to length of input string
    char* res = new char(len);
    int index = 0, i = 0;

    // create empty stack
    stack<int> s;
    s.push(0);

    while (i < len) {
          // Don't do any operation
        if(str[i] == '(' && i == 0) {
            i++;
              continue;
        }

        if (str[i] == '+') {

            // If top is 1, flip the operator
            if (s.top() == 1)
                res[index++] = '-';

            // If top is 0, append the same operator
            if (s.top() == 0)
                res[index++] = '+';

        } else if (str[i] == '-') {
            if (s.top() == 1)
                res[index++] = '+';
            else if (s.top() == 0)
                res[index++] = '-';
        } else if (str[i] == '(' && i > 0) {
            if (str[i - 1] == '-') {

                // x is opposite to the top of stack
                int x = (s.top() == 1) ? 0 : 1;
                s.push(x);
            }

            // push value equal to top of the stack
            else if (str[i - 1] == '+')
                s.push(s.top());
        }

        // If closing parentheses pop the stack once
        else if (str[i] == ')')
            s.pop();

        // copy the character to the result
        else
            res[index++] = str[i];
        i++;
    }
    return res;
}

// Driver program
int main()
{
    string s1 = "(a-(b+c)+d)";
    string s2 = "a-(b-c-(d+e))-f";
    cout << simplify(s1) << endl;
    cout << simplify(s2) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to simplify algebraic string
import java.util.*;
class GfG {

// Function to simplify the string
static String simplify(String str)
{
    int len = str.length();

    // resultant string of max length equal
    // to length of input string
    char res[] = new char[len];
    int index = 0, i = 0;

    // create empty stack
    Stack<Integer> s = new Stack<Integer> ();
    s.push(0);

    while (i < len) {
          // Don't do any operation
        if(str.charAt(i) == '(' && i == 0) {
            i++;
              continue;
        }

        if (str.charAt(i) == '+') {

            // If top is 1, flip the operator
            if (s.peek() == 1)
                res[index++] = '-';

            // If top is 0, append the same operator
            if (s.peek() == 0)
                res[index++] = '+';

        } else if (str.charAt(i) == '-') {
            if (s.peek() == 1)
                res[index++] = '+';
            else if (s.peek() == 0)
                res[index++] = '-';
        } else if (str.charAt(i) == '(' && i > 0) {
            if (str.charAt(i - 1) == '-') {

                // x is opposite to the top of stack
                int x = (s.peek() == 1) ? 0 : 1;
                s.push(x);
            }

            // push value equal to top of the stack
            else if (str.charAt(i - 1) == '+')
                s.push(s.peek());
        }

        // If closing parentheses pop the stack once
        else if (str.charAt(i) == ')')
            s.pop();

        else if(str.charAt(i) == '(' && i == 0)
              i = 0;
        // copy the character to the result
          else
            res[index++] = str.charAt(i);
        i++;
    }
    return new String(res);
}

// Driver program
public static void main(String[] args)
{
    String s1 = "(a-(b+c)+d)";
    String s2 = "a-(b-c-(d+e))-f";
    System.out.println(simplify(s1));
    System.out.println(simplify(s2));
}
}
```

## 蟒蛇 3

```
# Python3 program to simplify algebraic String

# Function to simplify the String

def simplify(Str):
    Len = len(Str)

    # resultant String of max Length
    # equal to Length of input String
    res = [None] * Len
    index = 0
    i = 0

    # create empty stack
    s = []
    s.append(0)

    while (i < Len):
          if (Str[i] == '(' and i == 0):
                i += 1
                continue

        if (Str[i] == '+'):

            # If top is 1, flip the operator
            if (s[-1] == 1):
                res[index] = '-'
                index += 1

            # If top is 0, append the
            # same operator
            if (s[-1] == 0):
                res[index] = '+'
                index += 1

        elif (Str[i] == '-'):
            if (s[-1] == 1):
                res[index] = '+'
                index += 1
            elif (s[-1] == 0):
                res[index] = '-'
                index += 1
        elif (Str[i] == '(' and i > 0):
            if (Str[i - 1] == '-'):

                # x is opposite to the top of stack
                x = 0 if (s[-1] == 1) else 1
                s.append(x)

            # append value equal to top of the stack
            elif (Str[i - 1] == '+'):
                s.append(s[-1])

        # If closing parentheses pop
        # the stack once
        elif (Str[i] == ')'):
            s.pop()

        # copy the character to the result
        else:
            res[index] = Str[i]
            index += 1
        i += 1
    return res

# Driver Code
if __name__ == '__main__':

    s1 = "(a-(b+c)+d)"
    s2 = "a-(b-c-(d+e))-f"
    r1 = simplify(s1)
    for i in r1:
        if i != None:
            print(i, end = " ")
        else:
            break
    print()
    r2 = simplify(s2)
    for i in r2:
        if i != None:
            print(i, end = " ")
        else:
            break

# This code is contributed by PranchalK
```

## C#

```
// C# program to simplify algebraic string
using System;
using System.Collections.Generic;

class GfG
{

// Function to simplify the string
static String simplify(String str)
{
    int len = str.Length;

    // resultant string of max length equal
    // to length of input string
    char []res = new char[len];
    int index = 0, i = 0;

    // create empty stack
    Stack<int> s = new Stack<int> ();
    s.Push(0);

    while (i < len)
    {
          // Don't do any operation
        if(str[i] == '(' && i == 0)
        {
            i++;
              continue;
        }

        if (str[i] == '+')
        {

            // If top is 1, flip the operator
            if (s.Peek() == 1)
                res[index++] = '-';

            // If top is 0, append the same operator
            if (s.Peek() == 0)
                res[index++] = '+';

        }
        else if (str[i] == '-')
        {
            if (s.Peek() == 1)
                res[index++] = '+';
            else if (s.Peek() == 0)
                res[index++] = '-';
        }
        else if (str[i] == '(' && i > 0)
        {
            if (str[i - 1] == '-')
            {

                // x is opposite to the top of stack
                int x = (s.Peek() == 1) ? 0 : 1;
                s.Push(x);
            }

            // push value equal to top of the stack
            else if (str[i - 1] == '+')
                s.Push(s.Peek());
        }

        // If closing parentheses pop the stack once
        else if (str[i]== ')')
            s.Pop();

        // copy the character to the result
        else
            res[index++] = str[i];
        i++;
    }
    return new String(res);
}

// Driver code
public static void Main(String[] args)
{
    String s1 = "(a-(b+c)+d)";
    String s2 = "a-(b-c-(d+e))-f";
    Console.WriteLine(simplify(s1));
    Console.WriteLine(simplify(s2));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to simplify algebraic string

// Function to simplify the string
function simplify(str)
{
    let len = str.length;

    // resultant string of max length equal
    // to length of input string
    let res = new Array(len);
    let index = 0, i = 0;

    // create empty stack
    let s = [];
    s.push(0);

    while (i < len) {
        // Don't do any operation
        if(str[i] == '(' && i == 0) {
            i++;
              continue;
        }

        if (str[i] == '+') {

            // If top is 1, flip the operator
            if (s[s.length-1] == 1)
                res[index++] = '-';

            // If top is 0, append the same operator
            if (s[s.length-1] == 0)
                res[index++] = '+';

        } else if (str[i] == '-') {
            if (s[s.length-1] == 1)
                res[index++] = '+';
            else if (s[s.length-1] == 0)
                res[index++] = '-';
        } else if (str[i] == '(' && i > 0) {
            if (str[i - 1] == '-') {

                // x is opposite to the top of stack
                let x = (s[s.length-1] == 1) ? 0 : 1;
                s.push(x);
            }

            // push value equal to top of the stack
            else if (str[i - 1] == '+')
                s.push(s[s.length-1]);
        }

        // If closing parentheses pop the stack once
        else if (str[i] == ')')
            s.pop();

        // copy the character to the result
        else
            res[index++] = str[i];
        i++;
    }
    return (res).join("");
}

// Driver program
let s1 = "(a-(b+c)+d)";
let s2 = "a-(b-c-(d+e))-f";
document.write(simplify(s1)+"<br>");
document.write(simplify(s2)+"<br>");

// This code is contributed by rag2127
</script>
```

**Output**

```
a-b-c+d
a-b+c+d+e-f

```

本文由 **Chhavi** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
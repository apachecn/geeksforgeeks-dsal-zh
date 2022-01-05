# 识别并标记表达式中不匹配的括号

> 原文:[https://www . geesforgeks . org/identify-mark-unmatched-括号-expression/](https://www.geeksforgeeks.org/identify-mark-unmatched-parenthesis-expression/)

给定一个表达式，在其中查找并标记匹配和不匹配的括号。我们需要用 0 替换所有平衡的左括号，用 1 替换所有平衡的右括号，用-1 替换所有不平衡的右括号。
**例:**

```
Input : ((a) 
Output : -10a1

Input : (a))
Output : 0a1-1

Input  : (((abc))((d)))))
Output : 000abc1100d111-1-1
```

这个想法基于一个[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)。我们从字符串 Up 的开头到结尾运行一个循环，对于每个'('，我们将它推入一个堆栈。如果堆栈是空的，并且我们遇到一个右括号“)”，我们在字符串的索引处替换-1。否则，我们用 0 替换所有左括号“(”，用 1 替换右括号。然后从堆栈中弹出。

## C++

```
// CPP program to mark balanced and unbalanced
// parenthesis.
#include <bits/stdc++.h>
using namespace std;

void identifyParenthesis(string a)
{
    stack<int> st;

    // run the loop upto end of the string
    for (int i = 0; i < a.length(); i++) {

        // if a[i] is opening bracket then push
        // into stack
        if (a[i] == '(')
            st.push(i);

        // if a[i] is closing bracket ')'
        else if (a[i] == ')') {

            // If this closing bracket is unmatched
            if (st.empty())
                a.replace(i, 1, "-1");

            else {

                // replace all opening brackets with 0
                // and closing brackets with 1
                a.replace(i, 1, "1");
                a.replace(st.top(), 1, "0");
                st.pop();
            }
        }
    }

    // if stack is not empty then pop out all
    // elements from it and replace -1 at that
    // index of the string
    while (!st.empty()) {
        a.replace(st.top(), 1, "-1");
        st.pop();
    }

    // print final string
    cout << a << endl;
}

// Driver code
int main()
{
    string str = "(a))";
    identifyParenthesis(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to mark balanced and
// unbalanced parenthesis.
import java.util.*;

class GFG
{
static void identifyParenthesis(StringBuffer a)
{
    Stack<Integer> st = new Stack<Integer>();

    // run the loop upto end of the string
    for (int i = 0; i < a.length(); i++)
    {

        // if a[i] is opening bracket then push
        // into stack
        if (a.charAt(i) == '(')
            st.push(i);

        // if a[i] is closing bracket ')'
        else if (a.charAt(i) == ')')
        {

            // If this closing bracket is unmatched
            if (st.empty())
                a.replace(i, i + 1, "-1");

            else
            {

                // replace all opening brackets with 0
                // and closing brackets with 1
                a.replace(i, i + 1, "1");
                a.replace(st.peek(), st.peek() + 1, "0");
                st.pop();
            }
        }
    }

    // if stack is not empty then pop out all
    // elements from it and replace -1 at that
    // index of the string
    while (!st.empty())
    {
        a.replace(st.peek(), 1, "-1");
        st.pop();
    }

    // print final string
    System.out.println(a);
}

// Driver code
public static void main(String[] args)
{
    StringBuffer str = new StringBuffer("(a))");
    identifyParenthesis(str);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to
# mark balanced and
# unbalanced parenthesis.
def identifyParenthesis(a):
    st = []

    # run the loop upto
    # end of the string
    for i in range (len(a)):

        # if a[i] is opening
        # bracket then push
        # into stack
        if (a[i] == '('):
            st.append(a[i])

        # if a[i] is closing bracket ')'
        elif (a[i] == ')'):

            # If this closing bracket
            # is unmatched
            if (len(st) == 0):
                a = a.replace(a[i], "-1", 1)

            else:

                # replace all opening brackets with 0
                # and closing brackets with 1
                a = a.replace(a[i], "1", 1)
                a = a.replace(st[-1], "0", 1)
                st.pop()

    # if stack is not empty
    # then pop out all
    # elements from it and
    # replace -1 at that
    # index of the string
    while (len(st) != 0):
        a = a.replace(st[-1], 1, "-1");
        st.pop()

    # print final string
    print(a)

# Driver code
if __name__ == "__main__":

    st = "(a))"
    identifyParenthesis(st)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to mark balanced and
// unbalanced parenthesis.
using System;
using System.Collections.Generic;
class GFG {

    static void identifyParenthesis(string a)
    {
        Stack<int> st = new Stack<int>();

        // run the loop upto end of the string
        for (int i = 0; i < a.Length; i++)
        {

            // if a[i] is opening bracket then push
            // into stack
            if (a[i] == '(')
                st.Push(i);

            // if a[i] is closing bracket ')'
            else if (a[i] == ')')
            {

                // If this closing bracket is unmatched
                if (st.Count == 0)
                {
                    a = a.Substring(0, i) + "-1" + a.Substring(i + 1);
                }
                else
                {

                    // replace all opening brackets with 0
                    // and closing brackets with 1
                    a = a.Substring(0, i) + "1" + a.Substring(i + 1);
                    a = a.Substring(0, st.Peek()) + "0" + a.Substring(st.Peek() + 1);
                    st.Pop();
                }
            }
        }

        // if stack is not empty then pop out all
        // elements from it and replace -1 at that
        // index of the string
        while (st.Count > 0)
        {
            a = a.Substring(0, st.Peek()) + "-1" + a.Substring(st.Peek() + 1);
            st.Pop();
        }

        // print final string
        Console.Write(new string(a));
    }

  static void Main() {
    string str = "(a))";
    identifyParenthesis(str);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program to mark balanced and
    // unbalanced parenthesis.

    function identifyParenthesis(a)
    {
        let st = [];

        // run the loop upto end of the string
        for (let i = 0; i < a.length; i++)
        {

            // if a[i] is opening bracket then push
            // into stack
            if (a[i] == '(')
                st.push(i);

            // if a[i] is closing bracket ')'
            else if (a[i] == ')')
            {

                // If this closing bracket is unmatched
                if (st.length == 0)
                {
                    a[i] = "-1";
                }
                else
                {

                    // replace all opening brackets with 0
                    // and closing brackets with 1
                    a[i] = "1";
                    a[st[st.length - 1]] = "0";
                    st.pop();
                }
            }
        }

        // if stack is not empty then pop out all
        // elements from it and replace -1 at that
        // index of the string
        while (st.length > 0)
        {
            a[st[st.length - 1]] = "-1";
            st.pop();
        }

        // print final string
        document.write(a.join(""));
    }

    let str = "(a))";
    identifyParenthesis(str.split(''));

// This code is contributed by suresh07.
</script>
```

**输出:**

```
0a1-1
```
# 后缀到前缀的转换

> 原文:[https://www.geeksforgeeks.org/postfix-prefix-conversion/](https://www.geeksforgeeks.org/postfix-prefix-conversion/)

**后缀**:如果运算子出现在运算子之后的表达式中，则该表达式称为后缀表达式。简单的形式(operand1 operand2 运算符)。
**例:** AB+CD-*(中缀:(A+B) * (C-D))

**前缀**:如果运算子出现在运算对象之前的表达式中，则该表达式称为前缀表达式。简单的形式(操作符 1 操作符 2)。
**例:** *+AB-CD(中缀:(A+B) * (C-D) )
给定一个后缀表达式，将其转换为前缀表达式。
将后缀表达式直接转换为前缀，而不经过先转换为中缀再转换为前缀的过程，在计算和更好地理解表达式方面要好得多(计算机使用后缀表达式进行评估)。

**示例:**

```
Input :  Postfix : AB+CD-*
Output : Prefix :  *+AB-CD
Explanation : Postfix to Infix : (A+B) * (C-D)
              Infix to Prefix :  *+AB-CD

Input :  Postfix : ABC/-AK/L-*
Output : Prefix :  *-A/BC-/AKL
Explanation : Postfix to Infix : ((A-(B/C))*((A/K)-L))
              Infix to Prefix :  *-A/BC-/AKL 
```

**后缀加前缀的算法** :

> *   Read suffix expressions from left to right
> *   If the symbol is an operand, it is pushed onto the stack.
> *   If the symbol is an operator, two operands
>     pop up from the stack to create a string by connecting the two operands with the operator in front of them.
>     **String = operator+operator 2+operator 1**
>     and push the result string back to the stack.
> *   Repeat the above steps until the suffix expression ends.

下面是上述想法的实现:

## C++

```
// CPP Program to convert postfix to prefix
#include <bits/stdc++.h>
using namespace std;

// function to check if character is operator or not
bool isOperator(char x)
{
    switch (x) {
    case '+':
    case '-':
    case '/':
    case '*':
        return true;
    }
    return false;
}

// Convert postfix to Prefix expression
string postToPre(string post_exp)
{
    stack<string> s;

    // length of expression
    int length = post_exp.size();

    // reading from right to left
    for (int i = 0; i < length; i++) {

        // check if symbol is operator
        if (isOperator(post_exp[i])) {

            // pop two operands from stack
            string op1 = s.top();
            s.pop();
            string op2 = s.top();
            s.pop();

            // concat the operands and operator
            string temp = post_exp[i] + op2 + op1;

            // Push string temp back to stack
            s.push(temp);
        }

        // if symbol is an operand
        else {

            // push the operand to the stack
            s.push(string(1, post_exp[i]));
        }
    }

    string ans = "";
    while (!s.empty()) {
        ans += s.top();
        s.pop();
    }
    return ans;
}

// Driver Code
int main()
{
    string post_exp = "ABC/-AK/L-*";

    // Function call
    cout << "Prefix : " << postToPre(post_exp);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to convert postfix to prefix
import java.util.*;

class GFG {

    // function to check if character
    // is operator or not
    static boolean isOperator(char x)
    {

        switch (x) {
        case '+':
        case '-':
        case '/':
        case '*':
            return true;
        }
        return false;
    }

    // Convert postfix to Prefix expression
    static String postToPre(String post_exp)
    {
        Stack<String> s = new Stack<String>();

        // length of expression
        int length = post_exp.length();

        // reading from right to left
        for (int i = 0; i < length; i++) {

            // check if symbol is operator
            if (isOperator(post_exp.charAt(i))) {

                // pop two operands from stack
                String op1 = s.peek();
                s.pop();
                String op2 = s.peek();
                s.pop();

                // concat the operands and operator
                String temp
                    = post_exp.charAt(i) + op2 + op1;

                // Push String temp back to stack
                s.push(temp);
            }

            // if symbol is an operand
            else {

                // push the operand to the stack
                s.push(post_exp.charAt(i) + "");
            }
        }

        // concatenate all strings in stack and return the
        // answer
        String ans = "";
        for (String i : s)
            ans += i;
        return ans;
    }

    // Driver Code
    public static void main(String args[])
    {
        String post_exp = "ABC/-AK/L-*";

        // Function call
        System.out.println("Prefix : "
                           + postToPre(post_exp));
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 Program to convert postfix to prefix

# function to check if
# character is operator or not

def isOperator(x):

    if x == "+":
        return True

    if x == "-":
        return True

    if x == "/":
        return True

    if x == "*":
        return True

    return False

# Convert postfix to Prefix expression

def postToPre(post_exp):

    s = []

    # length of expression
    length = len(post_exp)

    # reading from right to left
    for i in range(length):

        # check if symbol is operator
        if (isOperator(post_exp[i])):

            # pop two operands from stack
            op1 = s[-1]
            s.pop()
            op2 = s[-1]
            s.pop()

            # concat the operands and operator
            temp = post_exp[i] + op2 + op1

            # Push string temp back to stack
            s.append(temp)

        # if symbol is an operand
        else:

            # push the operand to the stack
            s.append(post_exp[i])

    ans = ""
    for i in s:
        ans += i
    return ans

# Driver Code
if __name__ == "__main__":

    post_exp = "AB+CD-"

    # Function call
    print("Prefix : ", postToPre(post_exp))

# This code is contributed by AnkitRai01
```

## C#

```
// C# Program to convert postfix to prefix
using System;
using System.Collections;

class GFG {

    // function to check if character
    // is operator or not
    static Boolean isOperator(char x)
    {

        switch (x) {
        case '+':
        case '-':
        case '/':
        case '*':
            return true;
        }
        return false;
    }

    // Convert postfix to Prefix expression
    static String postToPre(String post_exp)
    {
        Stack s = new Stack();

        // length of expression
        int length = post_exp.Length;

        // reading from right to left
        for (int i = 0; i < length; i++) {

            // check if symbol is operator
            if (isOperator(post_exp[i])) {

                // Pop two operands from stack
                String op1 = (String)s.Peek();
                s.Pop();
                String op2 = (String)s.Peek();
                s.Pop();

                // concat the operands and operator
                String temp = post_exp[i] + op2 + op1;

                // Push String temp back to stack
                s.Push(temp);
            }

            // if symbol is an operand
            else {

                // Push the operand to the stack
                s.Push(post_exp[i] + "");
            }
        }

        String ans = "";
        while (s.Count > 0)
            ans += s.Pop();
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String post_exp = "ABC/-AK/L-*";

        // Function call
        Console.WriteLine("Prefix : "
                          + postToPre(post_exp));
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
    // Javascript Program to convert postfix to prefix

    // function to check if character
    // is operator or not
    function isOperator(x)
    {

        switch (x) {
        case '+':
        case '-':
        case '/':
        case '*':
            return true;
        }
        return false;
    }

    // Convert postfix to Prefix expression
    function postToPre(post_exp)
    {
        let s = [];

        // length of expression
        let length = post_exp.length;

        // reading from right to left
        for (let i = 0; i < length; i++) {

            // check if symbol is operator
            if (isOperator(post_exp[i])) {

                // Pop two operands from stack
                let op1 = s[s.length - 1];
                s.pop();
                let op2 = s[s.length - 1];
                s.pop();

                // concat the operands and operator
                let temp = post_exp[i] + op2 + op1;

                // Push String temp back to stack
                s.push(temp);
            }

            // if symbol is an operand
            else {

                // Push the operand to the stack
                s.push(post_exp[i] + "");
            }
        }

        let ans = "";
        while (s.length > 0)
            ans += s.pop();
        return ans;
    }

    let post_exp = "ABC/-AK/L-*";

    // Function call
    document.write("Prefix : " + postToPre(post_exp));

    // This code is contributed by suresh07.
</script>
```

**Output**

```
Prefix : *-A/BC-/AKL
```
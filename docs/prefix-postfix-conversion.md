# 前缀到后缀的转换

> 原文:[https://www.geeksforgeeks.org/prefix-postfix-conversion/](https://www.geeksforgeeks.org/prefix-postfix-conversion/)

**前缀**:如果运算子出现在运算对象之前的表达式中，则该表达式称为前缀表达式。简单的形式(操作符 1 操作符 2)。
例:*+AB-CD(中缀:(A+B) * (C-D))

**后缀**:如果运算子出现在运算子之后的表达式中，则该表达式称为后缀表达式。简单的形式(operand1 operand2 运算符)。
示例:AB+CD-*(中缀:(A+B * (C-D) )
给定前缀表达式，将其转换为后缀表达式。
将前缀表达式直接转换为后缀，而不需要经过先转换为中缀再转换为后缀的过程，这在计算和更好地理解表达式方面要好得多(计算机使用后缀表达式进行评估)。

**示例:**

```
Input :  Prefix :  *+AB-CD
Output : Postfix : AB+CD-*
Explanation : Prefix to Infix :  (A+B) * (C-D)
              Infix to Postfix :  AB+CD-*

Input :  Prefix :  *-A/BC-/AKL
Output : Postfix : ABC/-AK/L-*
Explanation : Prefix to Infix :  (A-(B/C))*((A/K)-L)
              Infix to Postfix : ABC/-AK/L-* 
```

**前缀到后缀的算法**:

*   按照相反的顺序(从右到左)阅读前缀表达式
*   如果符号是一个操作数，则将它推到堆栈上
*   如果符号是运算符，则从堆栈中弹出两个操作数
    通过连接两个操作数和它们后面的运算符来创建一个字符串。
    **字符串=操作符 1 +操作符 2 +操作符**
    并将结果字符串推回堆栈
*   重复以上步骤，直到前缀表达式结束。

## C++

```
// CPP Program to convert prefix to postfix
#include <iostream>
#include <stack>
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

// Convert prefix to Postfix expression
string preToPost(string pre_exp)
{

    stack<string> s;
    // length of expression
    int length = pre_exp.size();

    // reading from right to left
    for (int i = length - 1; i >= 0; i--)
    {
        // check if symbol is operator
        if (isOperator(pre_exp[i]))
        {
            // pop two operands from stack
            string op1 = s.top();
            s.pop();
            string op2 = s.top();
            s.pop();

            // concat the operands and operator
            string temp = op1 + op2 + pre_exp[i];

            // Push string temp back to stack
            s.push(temp);
        }

        // if symbol is an operand
        else {

            // push the operand to the stack
            s.push(string(1, pre_exp[i]));
        }
    }

    // stack contains only the Postfix expression
    return s.top();
}

// Driver Code
int main()
{
    string pre_exp = "*-A/BC-/AKL";
    cout << "Postfix : " << preToPost(pre_exp);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JavaProgram to convert prefix to postfix
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

    // Convert prefix to Postfix expression
    static String preToPost(String pre_exp)
    {

        Stack<String> s = new Stack<String>();

        // length of expression
        int length = pre_exp.length();

        // reading from right to left
        for (int i = length - 1; i >= 0; i--)
        {
            // check if symbol is operator
            if (isOperator(pre_exp.charAt(i)))
            {
                // pop two operands from stack
                String op1 = s.peek();
                s.pop();
                String op2 = s.peek();
                s.pop();

                // concat the operands and operator
                String temp = op1 + op2 + pre_exp.charAt(i);

                // Push String temp back to stack
                s.push(temp);
            }

            // if symbol is an operand
            else {
                // push the operand to the stack
                s.push(pre_exp.charAt(i) + "");
            }
        }

        // stack contains only the Postfix expression
        return s.peek();
    }

    // Driver Code
    public static void main(String args[])
    {
        String pre_exp = "*-A/BC-/AKL";
        System.out.println("Postfix : "
                           + preToPost(pre_exp));
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Write Python3 code here
# -*- coding: utf-8 -*-

# Example Input
s = "*-A/BC-/AKL"

# Stack for storing operands
stack = []

operators = set(['+', '-', '*', '/', '^'])

# Reversing the order
s = s[::-1]

# iterating through individual tokens
for i in s:

    # if token is operator
    if i in operators:

        # pop 2 elements from stack
        a = stack.pop()
        b = stack.pop()

        # concatenate them as operand1 +
        # operand2 + operator
        temp = a+b+i
        stack.append(temp)

    # else if operand
    else:
        stack.append(i)

# printing final output
print(*stack)
```

## C#

```
// C# Program to convert prefix to postfix
using System;
using System.Collections.Generic;

class GFG {

    // function to check if character
    // is operator or not
    static bool isOperator(char x)
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

    // Convert prefix to Postfix expression
    static String preToPost(String pre_exp)
    {

        Stack<String> s = new Stack<String>();

        // length of expression
        int length = pre_exp.Length;

        // reading from right to left
        for (int i = length - 1; i >= 0; i--)
        {

            // check if symbol is operator
            if (isOperator(pre_exp[i]))
            {
                // pop two operands from stack
                String op1 = s.Peek();
                s.Pop();
                String op2 = s.Peek();
                s.Pop();

                // concat the operands and operator
                String temp = op1 + op2 + pre_exp[i];

                // Push String temp back to stack
                s.Push(temp);
            }

            // if symbol is an operand
            else {
                // push the operand to the stack
                s.Push(pre_exp[i] + "");
            }
        }

        // stack contains only the Postfix expression
        return s.Peek();
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String pre_exp = "*-A/BC-/AKL";
        Console.WriteLine("Postfix : "
                          + preToPost(pre_exp));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
    // Javascript Program to convert prefix to postfix

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

    // Convert prefix to Postfix expression
    function preToPost(pre_exp)
    {

        let s = [];

        // length of expression
        let length = pre_exp.length;

        // reading from right to left
        for (let i = length - 1; i >= 0; i--)
        {

            // check if symbol is operator
            if (isOperator(pre_exp[i]))
            {
                // pop two operands from stack
                let op1 = s[s.length - 1];
                s.pop();
                let op2 = s[s.length - 1];
                s.pop();

                // concat the operands and operator
                let temp = op1 + op2 + pre_exp[i];

                // Push String temp back to stack
                s.push(temp);
            }

            // if symbol is an operand
            else {
                // push the operand to the stack
                s.push(pre_exp[i] + "");
            }
        }

        // stack contains only the Postfix expression
        return s[s.length - 1];
    }

    let pre_exp = "*-A/BC-/AKL";
    document.write("Postfix : " + preToPost(pre_exp));

    // This code is contributed by suresh07.
</script>
```

**Output**

```
Postfix : ABC/-AK/L-*
```
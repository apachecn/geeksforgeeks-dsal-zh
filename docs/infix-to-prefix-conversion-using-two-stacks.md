# 使用两个堆栈进行中缀到前缀的转换

> 原文:[https://www . geesforgeks . org/infix-to-prefix-conversion-use-two-stacks/](https://www.geeksforgeeks.org/infix-to-prefix-conversion-using-two-stacks/)

**中缀**:如果运算符出现在表达式中的操作数之间，则该表达式称为中缀表达式。简单的形式(操作符 1 操作符 2)。
**例:** (A+B) * (C-D)
**前缀**:如果运算子出现在运算对象之前的表达式中，则该表达式称为前缀表达式。简单的形式(操作符 1 操作符 2)。
**示例:** *+AB-CD(中缀:(A+B) * (C-D) )
给定一个中缀表达式，使用两个栈将其转换为 Prefix 表达式。
**示例:**

```
Input : A * B + C / D
Output : + * A B/ C D 

Input : (A - B/C) * (A/K-L)
Output : *-A/BC-/AKL
```

[Recommended: Please try your approach first on IDE and then look at the solution.](https://ide.geeksforgeeks.org)

这个想法是用一个栈存储操作符，用另一个栈存储操作数。逐步算法是:

1.  遍历中缀表达式，检查给定字符是运算符还是操作数。
2.  如果是操作数，则将其推入操作数堆栈。
3.  如果是运算符，则检查当前运算符的优先级是否大于或小于或等于堆栈顶部的运算符。如果优先级更高，则将运算符推入运算符堆栈。否则从操作数栈弹出两个操作数，从操作数栈弹出操作符，将字符串**操作符+操作数 2 +操作数 1** 推入操作数栈。继续从两个堆栈中弹出并将结果推入操作数堆栈，直到当前运算符的优先级小于或等于运算符堆栈顶部的运算符。
4.  如果当前字符是'('，则将其推入运算符堆栈。
5.  如果当前字符是')'，则检查运算符堆栈顶部是否是左括号。如果不是，从操作数栈弹出两个操作数，从操作数栈弹出操作符，将字符串**操作符+操作数 2 +操作数 1** 推入操作数栈。继续从两个堆栈中弹出，并将结果推入操作数堆栈，直到操作符堆栈的顶部是一个左括号。
6.  最终前缀表达式出现在操作数堆栈的顶部。

下面是上述算法的实现:

## C++

```
// CPP program to convert infix to prefix.
#include <bits/stdc++.h>
using namespace std;

// Function to check if given character is
// an operator or not.
bool isOperator(char c)
{
    return (!isalpha(c) && !isdigit(c));
}

// Function to find priority of given
// operator.
int getPriority(char C)
{
    if (C == '-' || C == '+')
        return 1;
    else if (C == '*' || C == '/')
        return 2;
    else if (C == '^')
        return 3;
    return 0;
}

// Function that converts infix
// expression to prefix expression.
string infixToPrefix(string infix)
{
    // stack for operators.
    stack<char> operators;

    // stack for operands.
    stack<string> operands;

    for (int i = 0; i < infix.length(); i++) {

        // If current character is an
        // opening bracket, then
        // push into the operators stack.
        if (infix[i] == '(') {
            operators.push(infix[i]);
        }

        // If current character is a
        // closing bracket, then pop from
        // both stacks and push result
        // in operands stack until
        // matching opening bracket is
        // not found.
        else if (infix[i] == ')') {
            while (!operators.empty() &&
                   operators.top() != '(') {

                // operand 1
                string op1 = operands.top();
                operands.pop();

                // operand 2
                string op2 = operands.top();
                operands.pop();

                // operator
                char op = operators.top();
                operators.pop();

                // Add operands and operator
                // in form operator +
                // operand1 + operand2.
                string tmp = op + op2 + op1;
                operands.push(tmp);
            }

            // Pop opening bracket from
            // stack.
            operators.pop();
        }

        // If current character is an
        // operand then push it into
        // operands stack.
        else if (!isOperator(infix[i])) {
            operands.push(string(1, infix[i]));
        }

        // If current character is an
        // operator, then push it into
        // operators stack after popping
        // high priority operators from
        // operators stack and pushing
        // result in operands stack.
        else {
            while (!operators.empty() &&
                   getPriority(infix[i]) <=
                     getPriority(operators.top())) {

                string op1 = operands.top();
                operands.pop();

                string op2 = operands.top();
                operands.pop();

                char op = operators.top();
                operators.pop();

                string tmp = op + op2 + op1;
                operands.push(tmp);
            }

            operators.push(infix[i]);
        }
    }

    // Pop operators from operators stack
    // until it is empty and add result
    // of each pop operation in
    // operands stack.
    while (!operators.empty()) {
        string op1 = operands.top();
        operands.pop();

        string op2 = operands.top();
        operands.pop();

        char op = operators.top();
        operators.pop();

        string tmp = op + op2 + op1;
        operands.push(tmp);
    }

    // Final prefix expression is
    // present in operands stack.
    return operands.top();
}

// Driver code
int main()
{
    string s = "(A-B/C)*(A/K-L)";
    cout << infixToPrefix(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert
// infix to prefix.
import java.util.*;
class GFG
{
// Function to check if
// given character is
// an operator or not.
static boolean isOperator(char c)
{
    return (!(c >= 'a' && c <= 'z') &&
            !(c >= '0' && c <= '9') &&
            !(c >= 'A' && c <= 'Z'));
}

// Function to find priority
// of given operator.
static int getPriority(char C)
{
    if (C == '-' || C == '+')
        return 1;
    else if (C == '*' || C == '/')
        return 2;
    else if (C == '^')
        return 3;
    return 0;
}

// Function that converts infix
// expression to prefix expression.
static String infixToPrefix(String infix)
{
    // stack for operators.
    Stack<Character> operators = new Stack<Character>();

    // stack for operands.
    Stack<String> operands = new Stack<String>();

    for (int i = 0; i < infix.length(); i++)
    {

        // If current character is an
        // opening bracket, then
        // push into the operators stack.
        if (infix.charAt(i) == '(')
        {
            operators.push(infix.charAt(i));
        }

        // If current character is a
        // closing bracket, then pop from
        // both stacks and push result
        // in operands stack until
        // matching opening bracket is
        // not found.
        else if (infix.charAt(i) == ')')
        {
            while (!operators.empty() &&
                operators.peek() != '(')
                {

                // operand 1
                String op1 = operands.peek();
                operands.pop();

                // operand 2
                String op2 = operands.peek();
                operands.pop();

                // operator
                char op = operators.peek();
                operators.pop();

                // Add operands and operator
                // in form operator +
                // operand1 + operand2.
                String tmp = op + op2 + op1;
                operands.push(tmp);
            }

            // Pop opening bracket
            // from stack.
            operators.pop();
        }

        // If current character is an
        // operand then push it into
        // operands stack.
        else if (!isOperator(infix.charAt(i)))
        {
            operands.push(infix.charAt(i) + "");
        }

        // If current character is an
        // operator, then push it into
        // operators stack after popping
        // high priority operators from
        // operators stack and pushing
        // result in operands stack.
        else
        {
            while (!operators.empty() &&
                getPriority(infix.charAt(i)) <=
                    getPriority(operators.peek()))
                {

                String op1 = operands.peek();
                operands.pop();

                String op2 = operands.peek();
                operands.pop();

                char op = operators.peek();
                operators.pop();

                String tmp = op + op2 + op1;
                operands.push(tmp);
            }

            operators.push(infix.charAt(i));
        }
    }

    // Pop operators from operators
    // stack until it is empty and
    // operation in add result of
    // each pop operands stack.
    while (!operators.empty())
    {
        String op1 = operands.peek();
        operands.pop();

        String op2 = operands.peek();
        operands.pop();

        char op = operators.peek();
        operators.pop();

        String tmp = op + op2 + op1;
        operands.push(tmp);
    }

    // Final prefix expression is
    // present in operands stack.
    return operands.peek();
}

// Driver code
public static void main(String args[])
{
    String s = "(A-B/C)*(A/K-L)";
    System.out.println( infixToPrefix(s));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to convert infix to prefix.

# Function to check if
# given character is
# an operator or not.
def isOperator(c):
    return (not (c >= 'a' and c <= 'z') and not(c >= '0' and c <= '9') and not(c >= 'A' and c <= 'Z'))

# Function to find priority
# of given operator.
def getPriority(C):
    if (C == '-' or C == '+'):
        return 1
    elif (C == '*' or C == '/'):
        return 2
    elif (C == '^'):
        return 3
    return 0

# Function that converts infix
# expression to prefix expression.
def infixToPrefix(infix):
    # stack for operators.
    operators = []

    # stack for operands.
    operands = []

    for i in range(len(infix)):
        # If current character is an
        # opening bracket, then
        # push into the operators stack.
        if (infix[i] == '('):
            operators.append(infix[i])

        # If current character is a
        # closing bracket, then pop from
        # both stacks and push result
        # in operands stack until
        # matching opening bracket is
        # not found.
        elif (infix[i] == ')'):
            while (len(operators)!=0 and operators[-1] != '('):
                # operand 1
                op1 = operands[-1]
                operands.pop()

                # operand 2
                op2 = operands[-1]
                operands.pop()

                # operator
                op = operators[-1]
                operators.pop()

                # Add operands and operator
                # in form operator +
                # operand1 + operand2.
                tmp = op + op2 + op1
                operands.append(tmp)

            # Pop opening bracket
            # from stack.
            operators.pop()

        # If current character is an
        # operand then push it into
        # operands stack.
        elif (not isOperator(infix[i])):
            operands.append(infix[i] + "")

        # If current character is an
        # operator, then push it into
        # operators stack after popping
        # high priority operators from
        # operators stack and pushing
        # result in operands stack.
        else:
            while (len(operators)!=0 and getPriority(infix[i]) <= getPriority(operators[-1])):
                op1 = operands[-1]
                operands.pop()

                op2 = operands[-1]
                operands.pop()

                op = operators[-1]
                operators.pop()

                tmp = op + op2 + op1
                operands.append(tmp)
            operators.append(infix[i])

    # Pop operators from operators
    # stack until it is empty and
    # operation in add result of
    # each pop operands stack.
    while (len(operators)!=0):
        op1 = operands[-1]
        operands.pop()

        op2 = operands[-1]
        operands.pop()

        op = operators[-1]
        operators.pop()

        tmp = op + op2 + op1
        operands.append(tmp)

    # Final prefix expression is
    # present in operands stack.
    return operands[-1]

s = "(A-B/C)*(A/K-L)"
print( infixToPrefix(s))

# This code is contributed by decode2207.
```

## C#

```
// C# program to convert
// infix to prefix.
using System;
using System.Collections.Generic;
public class GFG
    {
    // Function to check if
    // given character is
    // an operator or not.
    static bool isOperator(char c)
    {
        return (!(c >= 'a' && c <= 'z') &&
                !(c >= '0' && c <= '9') &&
                !(c >= 'A' && c <= 'Z'));
    }

    // Function to find priority
    // of given operator.
    static int getPriority(char C)
    {
        if (C == '-' || C == '+')
            return 1;
        else if (C == '*' || C == '/')
            return 2;
        else if (C == '^')
            return 3;
        return 0;
    }

    // Function that converts infix
    // expression to prefix expression.
    static String infixToPrefix(String infix)
    {
        // stack for operators.
        Stack<char> operators = new Stack<char>();

        // stack for operands.
        Stack<String> operands = new Stack<String>();

        for (int i = 0; i < infix.Length; i++)
        {

            // If current character is an
            // opening bracket, then
            // push into the operators stack.
            if (infix[i] == '(')
            {
                operators.Push(infix[i]);
            }

            // If current character is a
            // closing bracket, then pop from
            // both stacks and push result
            // in operands stack until
            // matching opening bracket is
            // not found.
            else if (infix[i] == ')')
            {
                while (operators.Count!=0 &&
                    operators.Peek() != '(')
                    {

                    // operand 1
                    String op1 = operands.Peek();
                    operands.Pop();

                    // operand 2
                    String op2 = operands.Peek();
                    operands.Pop();

                    // operator
                    char op = operators.Peek();
                    operators.Pop();

                    // Add operands and operator
                    // in form operator +
                    // operand1 + operand2.
                    String tmp = op + op2 + op1;
                    operands.Push(tmp);
                }

                // Pop opening bracket
                // from stack.
                operators.Pop();
            }

            // If current character is an
            // operand then push it into
            // operands stack.
            else if (!isOperator(infix[i]))
            {
                operands.Push(infix[i] + "");
            }

            // If current character is an
            // operator, then push it into
            // operators stack after popping
            // high priority operators from
            // operators stack and pushing
            // result in operands stack.
            else
            {
                while (operators.Count!=0 &&
                    getPriority(infix[i]) <=
                        getPriority(operators.Peek()))
                    {

                    String op1 = operands.Peek();
                    operands.Pop();

                    String op2 = operands.Peek();
                    operands.Pop();

                    char op = operators.Peek();
                    operators.Pop();

                    String tmp = op + op2 + op1;
                    operands.Push(tmp);
                }

                operators.Push(infix[i]);
            }
        }

        // Pop operators from operators
        // stack until it is empty and
        // operation in add result of
        // each pop operands stack.
        while (operators.Count!=0)
        {
            String op1 = operands.Peek();
            operands.Pop();

            String op2 = operands.Peek();
            operands.Pop();

            char op = operators.Peek();
            operators.Pop();

            String tmp = op + op2 + op1;
            operands.Push(tmp);
        }

        // Final prefix expression is
        // present in operands stack.
        return operands.Peek();
    }

    // Driver code
    public static void Main()
    {
        String s = "(A-B/C)*(A/K-L)";
        Console.WriteLine( infixToPrefix(s));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to convert
// infix to prefix.

// Function to check if
// given character is
// an operator or not.
function isOperator(c)
{
    return (!(c >= 'a' && c <= 'z') &&
            !(c >= '0' && c <= '9') &&
            !(c >= 'A' && c <= 'Z'));
}

// Function to find priority
// of given operator.
function getPriority(C)
{
    if (C == '-' || C == '+')
        return 1;
    else if (C == '*' || C == '/')
        return 2;
    else if (C == '^')
        return 3;
    return 0;
}

// Function that converts infix
// expression to prefix expression.
function infixToPrefix(infix)
{
    // stack for operators.
    let operators = [];

    // stack for operands.
    let operands = [];

    for (let i = 0; i < infix.length; i++)
    {

        // If current character is an
        // opening bracket, then
        // push into the operators stack.
        if (infix[i] == '(')
        {
            operators.push(infix[i]);
        }

        // If current character is a
        // closing bracket, then pop from
        // both stacks and push result
        // in operands stack until
        // matching opening bracket is
        // not found.
        else if (infix[i] == ')')
        {
            while (operators.length!=0 &&
                operators[operators.length-1] != '(')
                {

                // operand 1
                let op1 = operands.pop();

                // operand 2
                let op2 = operands.pop();

                // operator
                let op = operators.pop();

                // Add operands and operator
                // in form operator +
                // operand1 + operand2.
                let tmp = op + op2 + op1;
                operands.push(tmp);
            }

            // Pop opening bracket
            // from stack.
            operators.pop();
        }

        // If current character is an
        // operand then push it into
        // operands stack.
        else if (!isOperator(infix[i]))
        {
            operands.push(infix[i] + "");
        }

        // If current character is an
        // operator, then push it into
        // operators stack after popping
        // high priority operators from
        // operators stack and pushing
        // result in operands stack.
        else
        {
            while (operators.length &&
                getPriority(infix[i]) <=
                    getPriority(operators[operators.length-1]))
                {

                let op1 = operands.pop();

                let op2 = operands.pop();

                let op = operators.pop();

                let tmp = op + op2 + op1;
                operands.push(tmp);
            }

            operators.push(infix[i]);
        }
    }

    // Pop operators from operators
    // stack until it is empty and
    // operation in add result of
    // each pop operands stack.
    while (operators.length!=0)
    {
        let op1 = operands.pop();

        let op2 = operands.pop();

        let op = operators.pop();

        let tmp = op + op2 + op1;
        operands.push(tmp);
    }

    // Final prefix expression is
    // present in operands stack.
    return operands[operands.length-1];
}

// Driver code
let s = "(A-B/C)*(A/K-L)";
document.write( infixToPrefix(s));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
*-A/BC-/AKL
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
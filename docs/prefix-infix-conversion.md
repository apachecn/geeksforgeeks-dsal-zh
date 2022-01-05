# 前缀到中缀的转换

> 原文:[https://www.geeksforgeeks.org/prefix-infix-conversion/](https://www.geeksforgeeks.org/prefix-infix-conversion/)

**中缀**:如果运算符出现在表达式中的操作数之间，则该表达式称为中缀表达式。简单的形式(操作符 1 操作符 2)。
例:(甲+乙)*(丙-丁)

**前缀**:如果运算子出现在运算对象之前的表达式中，则该表达式称为前缀表达式。简单的形式(操作符 1 操作符 2)。
例:*+AB-CD(中缀:(A+B) * (C-D))

给定前缀表达式，将其转换为中缀表达式。
计算机通常用前缀或后缀(通常是后缀)进行计算。但是对于人类来说，理解一个中缀表达式比理解一个前缀更容易。因此转换是人类理解的需要。

示例:

```
Input :  Prefix :  *+AB-CD
Output : Infix : ((A+B)*(C-D))

Input :  Prefix :  *-A/BC-/AKL
Output : Infix : ((A-(B/C))*((A/K)-L))
```

**前缀到中缀的算法**:

*   按照相反的顺序(从右到左)阅读前缀表达式
*   如果符号是一个操作数，则将它推到堆栈上
*   如果符号是运算符，则从堆栈中弹出两个操作数
    通过连接两个操作数和它们之间的运算符来创建一个字符串。
    **字符串=(操作符 1 +操作符 2)**
    并将结果字符串推回堆栈
*   重复以上步骤，直到前缀表达式结束。

## C++

```
// C++ Program to convert prefix to Infix
#include <iostream>
#include <stack>
using namespace std;

// function to check if character is operator or not
bool isOperator(char x) {
  switch (x) {
  case '+':
  case '-':
  case '/':
  case '*':
    return true;
  }
  return false;
}

// Convert prefix to Infix expression
string preToInfix(string pre_exp) {
  stack<string> s;

  // length of expression
  int length = pre_exp.size();

  // reading from right to left
  for (int i = length - 1; i >= 0; i--) {

    // check if symbol is operator
    if (isOperator(pre_exp[i])) {

      // pop two operands from stack
      string op1 = s.top();   s.pop();
      string op2 = s.top();   s.pop();

      // concat the operands and operator
      string temp = "(" + op1 + pre_exp[i] + op2 + ")";

      // Push string temp back to stack
      s.push(temp);
    }

    // if symbol is an operand
    else {

      // push the operand to the stack
      s.push(string(1, pre_exp[i]));
    }
  }

  // Stack now contains the Infix expression
  return s.top();
}

// Driver Code
int main() {
  string pre_exp = "*-A/BC-/AKL";
  cout << "Infix : " << preToInfix(pre_exp);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert prefix to Infix
import java.util.Stack;

class GFG{

// Function to check if character
// is operator or not    
static    boolean isOperator(char x)
{
    switch(x)
    {
        case '+':
        case '-':
        case '*':
        case '/':
            return true;
    }
    return false;
}

// Convert prefix to Infix expression
public static String convert(String str)
{
    Stack<String> stack = new Stack<>();

    // Length of expression
    int l = str.length();

    // Reading from right to left
    for(int i = l - 1; i >= 0; i--)
    {
        char c = str.charAt(i);
        if (isOperator(c))
        {
            String op1 = stack.pop();
            String op2 = stack.pop();

            // Concat the operands and operator
            String temp = "(" + op1 + c + op2 + ")";
            stack.push(temp);
        }
        else
        {

            // To make character to string
            stack.push(c + "");
        }
    }
    return stack.pop();
}

// Driver code
public static void main(String[] args)
{
    String exp = "*-A/BC-/AKL";
    System.out.println("Infix : " + convert(exp));
}
}

// This code is contributed by abbeyme
```

## 蟒蛇 3

```
# Python Program to convert prefix to Infix
def prefixToInfix(prefix):
    stack = []

    # read prefix in reverse order
    i = len(prefix) - 1
    while i >= 0:
        if not isOperator(prefix[i]):

            # symbol is operand
            stack.append(prefix[i])
            i -= 1
        else:

            # symbol is operator
            str = "(" + stack.pop() + prefix[i] + stack.pop() + ")"
            stack.append(str)
            i -= 1

    return stack.pop()

def isOperator(c):
    if c == "*" or c == "+" or c == "-" or c == "/" or c == "^" or c == "(" or c == ")":
        return True
    else:
        return False

# Driver code
if __name__=="__main__":
    str = "*-A/BC-/AKL"
    print(prefixToInfix(str))

# This code is contributed by avishekarora
```

## C#

```
// C# program to convert prefix to Infix
using System;
using System.Collections;

class GFG{

// Function to check if character
// is operator or not    
static bool isOperator(char x)
{
    switch(x)
    {
        case '+':
        case '-':
        case '*':
        case '/':
            return true;
    }
    return false;
}

// Convert prefix to Infix expression
public static string convert(string str)
{
    Stack stack = new Stack();

    // Length of expression
    int l = str.Length;

    // Reading from right to left
    for(int i = l - 1; i >= 0; i--)
    {
        char c = str[i];

        if (isOperator(c))
        {
            string op1 = (string)stack.Pop();
            string op2 = (string)stack.Pop();

            // Concat the operands and operator
            string temp = "(" + op1 + c + op2 + ")";
            stack.Push(temp);
        }
        else
        {

            // To make character to string
            stack.Push(c + "");
        }
    }
    return (string)stack.Pop();
}

// Driver code
public static void Main(string[] args)
{
    string exp = "*-A/BC-/AKL";

    Console.Write("Infix : " + convert(exp));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
    // Javascript program to convert prefix to Infix

    // Function to check if character
    // is operator or not   
    function isOperator(x)
    {
        switch(x)
        {
            case '+':
            case '-':
            case '*':
            case '/':
                return true;
        }
        return false;
    }

    // Convert prefix to Infix expression
    function convert(str)
    {
        let stack = [];

        // Length of expression
        let l = str.length;

        // Reading from right to left
        for(let i = l - 1; i >= 0; i--)
        {
            let c = str[i];

            if (isOperator(c))
            {
                let op1 = stack[stack.length - 1];
                stack.pop()
                let op2 = stack[stack.length - 1];
                stack.pop()

                // Concat the operands and operator
                let temp = "(" + op1 + c + op2 + ")";
                stack.push(temp);
            }
            else
            {

                // To make character to string
                stack.push(c + "");
            }
        }
        return stack[stack.length - 1];
    }

    let exp = "*-A/BC-/AKL";

    document.write("Infix : " + convert(exp));

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
Infix : ((A-(B/C))*((A/K)-L))
```
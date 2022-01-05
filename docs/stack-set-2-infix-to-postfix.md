# 堆栈|集合 2(中缀到后缀)

> 原文:[https://www.geeksforgeeks.org/stack-set-2-infix-to-postfix/](https://www.geeksforgeeks.org/stack-set-2-infix-to-postfix/)

先决条件–[堆栈|集合 1(简介)](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)
**中缀表达式:**当一个运算符位于每对操作数之间时，该表达式形成一个 op b。
**后缀表达式:**a b op 形式的表达式。每对操作数跟一个运算符。
**为什么用后缀表示表达式？**
编译器从左到右或从右到左扫描表达式。
考虑下面的表达式:a op1 b op2 c op3 d
如果 op1 = +，op2 = *，op3 = +
编译器首先扫描表达式来计算表达式 b * c，然后再次扫描表达式来给它添加 a。在另一次扫描后，结果被加到 d 上。
重复扫描非常低效。最好在求值之前将表达式转换为后缀(或前缀)形式。
后缀形式对应的表达式是 abc*+d+。后缀表达式可以很容易地用栈来计算。我们将在另一篇文章中讨论后缀表达式求值。
**算法**
**1。**从左到右扫描中缀表达式。
**2。**如果扫描的字符是操作数，输出。
**3。**否则，
**1** 如果被扫描运算符的优先级大于堆栈中运算符的优先级(或者堆栈为空或者堆栈中包含'(' )，则推送。
**2** 否则，从堆栈中弹出所有大于或等于被扫描运算符优先级的运算符。完成后，将扫描的操作符推送到堆栈。(如果您在弹出时遇到括号，请在此处停止并按堆栈中的扫描运算符。)
**4。**如果扫描到的字符是'('，将其推入堆栈。
**5。**如果扫描的字符是“)”，弹出堆栈并输出，直到遇到“(”，并丢弃两个括号。
T42【6】。重复步骤 2-6，直到中缀表达式被扫描。
**7。**打印输出
**8。**从堆栈弹出并输出，直到不为空。

以下是上述算法的实现

## C++

```
/* C++ implementation to convert
infix expression to postfix*/

#include<bits/stdc++.h>
using namespace std;

//Function to return precedence of operators
int prec(char c) {
    if(c == '^')
        return 3;
    else if(c == '/' || c=='*')
        return 2;
    else if(c == '+' || c == '-')
        return 1;
    else
        return -1;
}

// The main function to convert infix expression
//to postfix expression
void infixToPostfix(string s) {

    stack<char> st; //For stack operations, we are using C++ built in stack
    string result;

    for(int i = 0; i < s.length(); i++) {
        char c = s[i];

        // If the scanned character is
        // an operand, add it to output string.
        if((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z') || (c >= '0' && c <= '9'))
            result += c;

        // If the scanned character is an
        // ‘(‘, push it to the stack.
        else if(c == '(')
            st.push('(');

        // If the scanned character is an ‘)’,
        // pop and to output string from the stack
        // until an ‘(‘ is encountered.
        else if(c == ')') {
            while(st.top() != '(')
            {
                result += st.top();
                st.pop();
            }
            st.pop();
        }

        //If an operator is scanned
        else {
            while(!st.empty() && prec(s[i]) <= prec(st.top())) {
                result += st.top();
                st.pop(); 
            }
            st.push(c);
        }
    }

    // Pop all the remaining elements from the stack
    while(!st.empty()) {
        result += st.top();
        st.pop();
    }

    cout << result << endl;
}

//Driver program to test above functions
int main() {
    string exp = "a+b*(c^d-e)^(f+g*h)-i";
    infixToPostfix(exp);
    return 0;
}
```

## C

```
// C program to convert infix expression to postfix
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

// Stack type
struct Stack
{
    int top;
    unsigned capacity;
    int* array;
};

// Stack Operations
struct Stack* createStack( unsigned capacity )
{
    struct Stack* stack = (struct Stack*)
           malloc(sizeof(struct Stack));

    if (!stack)
        return NULL;

    stack->top = -1;
    stack->capacity = capacity;

    stack->array = (int*) malloc(stack->capacity *
                                   sizeof(int));

    return stack;
}
int isEmpty(struct Stack* stack)
{
    return stack->top == -1 ;
}
char peek(struct Stack* stack)
{
    return stack->array[stack->top];
}
char pop(struct Stack* stack)
{
    if (!isEmpty(stack))
        return stack->array[stack->top--] ;
    return '{content}apos;;
}
void push(struct Stack* stack, char op)
{
    stack->array[++stack->top] = op;
}

// A utility function to check if
// the given character is operand
int isOperand(char ch)
{
    return (ch >= 'a' && ch <= 'z') ||
           (ch >= 'A' && ch <= 'Z');
}

// A utility function to return
// precedence of a given operator
// Higher returned value means
// higher precedence
int Prec(char ch)
{
    switch (ch)
    {
    case '+':
    case '-':
        return 1;

    case '*':
    case '/':
        return 2;

    case '^':
        return 3;
    }
    return -1;
}

// The main function that
// converts given infix expression
// to postfix expression.
int infixToPostfix(char* exp)
{
    int i, k;

    // Create a stack of capacity
    // equal to expression size
    struct Stack* stack = createStack(strlen(exp));
    if(!stack) // See if stack was created successfully
        return -1 ;

    for (i = 0, k = -1; exp[i]; ++i)
    {

        // If the scanned character is
        // an operand, add it to output.
        if (isOperand(exp[i]))
            exp[++k] = exp[i];

        // If the scanned character is an
        // ‘(‘, push it to the stack.
        else if (exp[i] == '(')
            push(stack, exp[i]);

        // If the scanned character is an ‘)’,
        // pop and output from the stack
        // until an ‘(‘ is encountered.
        else if (exp[i] == ')')
        {
            while (!isEmpty(stack) && peek(stack) != '(')
                exp[++k] = pop(stack);
            if (!isEmpty(stack) && peek(stack) != '(')
                return -1; // invalid expression            
            else
                pop(stack);
        }
        else // an operator is encountered
        {
            while (!isEmpty(stack) &&
                 Prec(exp[i]) <= Prec(peek(stack)))
                exp[++k] = pop(stack);
            push(stack, exp[i]);
        }

    }

    // pop all the operators from the stack
    while (!isEmpty(stack))
        exp[++k] = pop(stack );

    exp[++k] = '\0';
    printf( "%s", exp );
}

// Driver program to test above functions
int main()
{
    char exp[] = "a+b*(c^d-e)^(f+g*h)-i";
    infixToPostfix(exp);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java implementation to convert
 infix expression to postfix*/
// Note that here we use Stack class for Stack operations

import java.util.Stack;

class Test
{

    // A utility function to return
    // precedence of a given operator
    // Higher returned value means
    // higher precedence
    static int Prec(char ch)
    {
        switch (ch)
        {
        case '+':
        case '-':
            return 1;

        case '*':
        case '/':
            return 2;

        case '^':
            return 3;
        }
        return -1;
    }

    // The main method that converts
    // given infix expression
    // to postfix expression.
    static String infixToPostfix(String exp)
    {
        // initializing empty String for result
        String result = new String("");

        // initializing empty stack
        Stack<Character> stack = new Stack<>();

        for (int i = 0; i<exp.length(); ++i)
        {
            char c = exp.charAt(i);

            // If the scanned character is an
            // operand, add it to output.
            if (Character.isLetterOrDigit(c))
                result += c;

            // If the scanned character is an '(',
            // push it to the stack.
            else if (c == '(')
                stack.push(c);

            //  If the scanned character is an ')',
            // pop and output from the stack
            // until an '(' is encountered.
            else if (c == ')')
            {
                while (!stack.isEmpty() &&
                        stack.peek() != '(')
                    result += stack.pop();

                    stack.pop();
            }
            else // an operator is encountered
            {
                while (!stack.isEmpty() && Prec(c)
                         <= Prec(stack.peek())){

                    result += stack.pop();
             }
                stack.push(c);
            }

        }

        // pop all the operators from the stack
        while (!stack.isEmpty()){
            if(stack.peek() == '(')
                return "Invalid Expression";
            result += stack.pop();
         }
        return result;
    }

    // Driver method
    public static void main(String[] args)
    {
        String exp = "a+b*(c^d-e)^(f+g*h)-i";
        System.out.println(infixToPostfix(exp));
    }
}
```

## 计算机编程语言

```
# Python program to convert infix expression to postfix

# Class to convert the expression
class Conversion:

    # Constructor to initialize the class variables
    def __init__(self, capacity):
        self.top = -1
        self.capacity = capacity
        # This array is used a stack
        self.array = []
        # Precedence setting
        self.output = []
        self.precedence = {'+':1, '-':1, '*':2, '/':2, '^':3}

    # check if the stack is empty
    def isEmpty(self):
        return True if self.top == -1 else False

    # Return the value of the top of the stack
    def peek(self):
        return self.array[-1]

    # Pop the element from the stack
    def pop(self):
        if not self.isEmpty():
            self.top -= 1
            return self.array.pop()
        else:
            return "{content}quot;

    # Push the element to the stack
    def push(self, op):
        self.top += 1
        self.array.append(op)

    # A utility function to check is the given character
    # is operand
    def isOperand(self, ch):
        return ch.isalpha()

    # Check if the precedence of operator is strictly
    # less than top of stack or not
    def notGreater(self, i):
        try:
            a = self.precedence[i]
            b = self.precedence[self.peek()]
            return True if a  <= b else False
        except KeyError:
            return False

    # The main function that
    # converts given infix expression
    # to postfix expression
    def infixToPostfix(self, exp):

        # Iterate over the expression for conversion
        for i in exp:
            # If the character is an operand,
            # add it to output
            if self.isOperand(i):
                self.output.append(i)

            # If the character is an '(', push it to stack
            elif i  == '(':
                self.push(i)

            # If the scanned character is an ')', pop and
            # output from the stack until and '(' is found
            elif i == ')':
                while( (not self.isEmpty()) and
                                self.peek() != '('):
                    a = self.pop()
                    self.output.append(a)
                if (not self.isEmpty() and self.peek() != '('):
                    return -1
                else:
                    self.pop()

            # An operator is encountered
            else:
                while(not self.isEmpty() and self.notGreater(i)):
                    self.output.append(self.pop())
                self.push(i)

        # pop all the operator from the stack
        while not self.isEmpty():
            self.output.append(self.pop())

        print "".join(self.output)

# Driver program to test above function
exp = "a+b*(c^d-e)^(f+g*h)-i"
obj = Conversion(len(exp))
obj.infixToPostfix(exp)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;
using System.Collections.Generic;

/* c# implementation to convert
infix expression to postfix*/
// Note that here we use Stack
// class for Stack operations

public  class Test
{

    // A utility function to return
    // precedence of a given operator
    // Higher returned value means higher precedence
    internal static int Prec(char ch)
    {
        switch (ch)
        {
        case '+':
        case '-':
            return 1;

        case '*':
        case '/':
            return 2;

        case '^':
            return 3;
        }
        return -1;
    }

    // The main method that converts given infix expression
    // to postfix expression. 
    public static string infixToPostfix(string exp)
    {
        // initializing empty String for result
        string result = "";

        // initializing empty stack
        Stack<char> stack = new Stack<char>();

        for (int i = 0; i < exp.Length; ++i)
        {
            char c = exp[i];

            // If the scanned character is an
            // operand, add it to output.
            if (char.IsLetterOrDigit(c))
            {
                result += c;
            }

            // If the scanned character is an '(',
            // push it to the stack.
            else if (c == '(')
            {
                stack.Push(c);
            }

            //  If the scanned character is an ')',
            // pop and output from the stack 
            // until an '(' is encountered.
            else if (c == ')')
            {
                while (stack.Count > 0 &&
                        stack.Peek() != '(')
                {
                    result += stack.Pop();
                }

                if (stack.Count > 0 && stack.Peek() != '(')
                {
                    return "Invalid Expression"; // invalid expression
                }
                else
                {
                    stack.Pop();
                }
            }
            else // an operator is encountered
            {
                while (stack.Count > 0 && Prec(c) <=
                                  Prec(stack.Peek()))
                {
                    result += stack.Pop();
                }
                stack.Push(c);
            }

        }

        // pop all the operators from the stack
        while (stack.Count > 0)
        {
            result += stack.Pop();
        }

        return result;
    }

    // Driver method 
    public static void Main(string[] args)
    {
        string exp = "a+b*(c^d-e)^(f+g*h)-i";
        Console.WriteLine(infixToPostfix(exp));
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    /* Javascript implementation to convert
    infix expression to postfix*/

    //Function to return precedence of operators
    function prec(c) {
        if(c == '^')
            return 3;
        else if(c == '/' || c=='*')
            return 2;
        else if(c == '+' || c == '-')
            return 1;
        else
            return -1;
    }

    // The main function to convert infix expression
    //to postfix expression
    function infixToPostfix(s) {

        let st = []; //For stack operations, we are using C++ built in stack
        let result = "";

        for(let i = 0; i < s.length; i++) {
            let c = s[i];

            // If the scanned character is
            // an operand, add it to output string.
            if((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z') || (c >= '0' && c <= '9'))
                result += c;

            // If the scanned character is an
            // ‘(‘, push it to the stack.
            else if(c == '(')
                st.push('(');

            // If the scanned character is an ‘)’,
            // pop and to output string from the stack
            // until an ‘(‘ is encountered.
            else if(c == ')') {
                while(st[st.length - 1] != '(')
                {
                    result += st[st.length - 1];
                    st.pop();
                }
                st.pop();
            }

            //If an operator is scanned
            else {
                while(st.length != 0 && prec(s[i]) <= prec(st[st.length - 1])) {
                    result += st[st.length - 1];
                    st.pop();
                }
                st.push(c);
            }
        }

        // Pop all the remaining elements from the stack
        while(st.length != 0) {
            result += st[st.length - 1];
            st.pop();
        }

        document.write(result + "</br>");
    }

    let exp = "a+b*(c^d-e)^(f+g*h)-i";
    infixToPostfix(exp);

// This code is contributed by decode2207.
</script>
```

**Output**

```
abcd^e-fgh*+^*+i-
```

https://youtu . be/ysdharaxk？list = plqm 7 alxfysf7 lap-wi 5 qlad 8 oebx 9 rmv**测验**:T3【堆叠问题】

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
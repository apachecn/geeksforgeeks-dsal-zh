# 使用不同的栈内和栈外优先级值对后缀进行中缀

> 原文:[https://www . geeksforgeeks . org/infix-to-postfix-使用不同优先级的值进行堆栈内和堆栈外/](https://www.geeksforgeeks.org/infix-to-postfix-using-different-precedence-values-for-in-stack-and-out-stack/)

中缀到后缀表达式的转换可以使用两个优先函数优雅地完成。每个运算符都被赋予一个值(值越大意味着优先级越高)，这取决于运算符是在堆栈内部还是外部。不同运算符的左右结合律也可以通过改变它在两个优先函数中的值来处理。
**中缀表达式示例:** a+b*c
**其对应的后缀表达式** : abc*+
要了解更多[中缀](https://en.wikipedia.org/wiki/Infix_notation)和[后缀](https://en.wikipedia.org/wiki/Reverse_Polish_notation)表达式，请访问链接。
**注:**在本文中，我们假设所有操作符都是从左到右关联的。
**示例:**

> **输入:**str =“a+b * c-(d/e+f * g * h)”
> **输出:**ABC *+de/fg * h *+-
> T6】输入:a+b * c
> T9】输出: abc*+

**进场:**

1.  如果输入字符是操作数，打印它。
2.  如果输入字符是运算符-
    *   如果堆栈为空，将其推入堆栈。
    *   如果其优先级值大于顶部字符的优先级值，则按下。
    *   如果其优先级值小于或等于，则从堆栈中弹出并打印，同时顶部字符的优先级大于输入字符的优先级值。
3.  如果输入字符是“)”，则弹出并打印，直到顶部是“(”。(' Pop '('但不要打印。)
4.  如果堆栈在遇到“(”之前变成空的，那么它就是一个无效的表达式。
5.  重复步骤 1-4，直到输入表达式被完全读取。
6.  从堆栈中弹出剩余的元素并打印出来。

上面的方法处理幂运算子(这里是^)的右结合性，方法是在栈外赋予它较高的优先值，在栈内赋予它较低的优先值，而对于左结合运算子则相反。
下面是上述方法的实现:

## C++

```
// C++ program to convert an infix expression to a
// postfix expression using two precedence function
#include <bits/stdc++.h>
using namespace std;

// to check if the input character
// is an operator or a '('
int isOperator(char input)
{
    switch (input) {
    case '+':
        return 1;
    case '-':
        return 1;
    case '*':
        return 1;
    case '%':
        return 1;
    case '/':
        return 1;
    case '(':
        return 1;
    }
    return 0;
}

// to check if the input character is an operand
int isOperand(char input)
{
    if (input >= 65 && input <= 90
        || input >= 97 && input <= 122)
        return 1;
    return 0;
}

// function to return precedence value
// if operator is present in stack
int inPrec(char input)
{
    switch (input) {
    case '+':
    case '-':
        return 2;
    case '*':
    case '%':
    case '/':
        return 4;
    case '(':
        return 0;
    }
}

// function to return precedence value
// if operator is present outside stack.
int outPrec(char input)
{
    switch (input) {
    case '+':
    case '-':
        return 1;
    case '*':
    case '%':
    case '/':
        return 3;
    case '(':
        return 100;
    }
}

// function to convert infix to postfix
void inToPost(char* input)
{
    stack<char> s;

    // while input is not NULL iterate
    int i = 0;
    while (input[i] != '\0') {

        // if character an operand
        if (isOperand(input[i])) {
            printf("%c", input[i]);
        }

        // if input is an operator, push
        else if (isOperator(input[i])) {
            if (s.empty()
                || outPrec(input[i]) > inPrec(s.top()))
                s.push(input[i]);
            else {
                while (!s.empty()
                    && outPrec(input[i]) < inPrec(s.top())) {
                    printf("%c", s.top());
                    s.pop();
                }
                s.push(input[i]);
            }
        }

        // condition for opening bracket
        else if (input[i] == ')') {
            while (s.top() != '(') {
                printf("%c", s.top());
                s.pop();

                // if opening bracket not present
                if (s.empty()) {
                    printf("Wrong input\n");
                    exit(1);
                }
            }

            // pop the opening bracket.
            s.pop();
        }
        i++;
    }

    // pop the remaining operators
    while (!s.empty()) {
        if (s.top() == '(') {
            printf("\n Wrong input\n");
            exit(1);
        }
        printf("%c", s.top());
        s.pop();
    }
}

// Driver code
int main()
{
    char input[] = "a+b*c-(d/e+f*g*h)";
    inToPost(input);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import static java.lang.System.exit;
import java.util.Stack;

// Java program to convert an infix expression to a
// postfix expression using two precedence function
class GFG {

    // to check if the input character
    // is an operator or a '('
    static int isOperator(char input)
    {
        switch (input) {
        case '+':
            return 1;
        case '-':
            return 1;
        case '*':
            return 1;
        case '%':
            return 1;
        case '/':
            return 1;
        case '(':
            return 1;
        }
        return 0;
    }

    // to check if the input character is an operand
    static int isOperand(char input)
    {
        if (input >= 65 && input <= 90
            || input >= 97 && input <= 122) {
            return 1;
        }
        return 0;
    }

    // function to return precedence value
    // if operator is present in stack
    static int inPrec(char input)
    {
        switch (input) {
        case '+':
        case '-':
            return 2;
        case '*':
        case '%':
        case '/':
            return 4;
        case '(':
            return 0;
        }
        return 0;
    }

    // function to return precedence value
    // if operator is present outside stack.
    static int outPrec(char input)
    {
        switch (input) {
        case '+':
        case '-':
            return 1;
        case '*':
        case '%':
        case '/':
            return 3;
        case '(':
            return 100;
        }
        return 0;
    }

    // function to convert infix to postfix
    static void inToPost(char[] input)
    {
        Stack<Character> s = new Stack<Character>();

        // while input is not NULL iterate
        int i = 0;
        while (input.length != i) {

            // if character an operand
            if (isOperand(input[i]) == 1) {
                System.out.printf("%c", input[i]);
            } // if input is an operator, push
            else if (isOperator(input[i]) == 1) {
                if (s.empty()
                    || outPrec(input[i]) > inPrec(s.peek())) {
                    s.push(input[i]);
                }
                else {
                    while (!s.empty()
                           && outPrec(input[i]) < inPrec(s.peek())) {
                        System.out.printf("%c", s.peek());
                        s.pop();
                    }
                    s.push(input[i]);
                }
            } // condition for opening bracket
            else if (input[i] == ')') {
                while (s.peek() != '(') {
                    System.out.printf("%c", s.peek());
                    s.pop();

                    // if opening bracket not present
                    if (s.empty()) {
                        System.out.printf("Wrong input\n");
                        exit(1);
                    }
                }

                // pop the opening bracket.
                s.pop();
            }
            i++;
        }

        // pop the remaining operators
        while (!s.empty()) {
            if (s.peek() == '(') {
                System.out.printf("\n Wrong input\n");
                exit(1);
            }
            System.out.printf("%c", s.peek());
            s.pop();
        }
    }

    // Driver code
    static public void main(String[] args)
    {
        char input[] = "a+b*c-(d/e+f*g*h)".toCharArray();
        inToPost(input);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to convert an infix
# expression to a postfix expression
# using two precedence function

# To check if the input character
# is an operator or a '('
def isOperator(input):

    switch = {
        '+': 1,
        '-': 1,
        '*': 1,
        '/': 1,
        '%': 1,
        '(': 1,
    }

    return switch.get(input, False)

# To check if the input character is an operand
def isOperand(input):

    if ((ord(input) >= 65 and ord(input) <= 90) or
        (ord(input) >= 97 and ord(input) <= 122)):
        return 1

    return 0

# Function to return precedence value
# if operator is present in stack
def inPrec(input):

    switch = {
        '+': 2,
        '-': 2,
        '*': 4,
        '/': 4,
        '%': 4,
        '(': 0,
    }

    return switch.get(input, 0)

# Function to return precedence value
# if operator is present outside stack.
def outPrec(input):

    switch = {
        '+': 1,
        '-': 1,
        '*': 3,
        '/': 3,
        '%': 3,
        '(': 100,
    }

    return switch.get(input, 0)

# Function to convert infix to postfix
def inToPost(input):

    i = 0
    s = []

    # While input is not NULL iterate
    while (len(input) != i):

        # If character an operand
        if (isOperand(input[i]) == 1):
            print(input[i], end = "")

        # If input is an operator, push
        elif (isOperator(input[i]) == 1):
            if (len(s) == 0 or
                outPrec(input[i]) >
                 inPrec(s[-1])):
                s.append(input[i])

            else:
                while(len(s) > 0 and
                      outPrec(input[i]) <
                      inPrec(s[-1])):
                    print(s[-1], end = "")
                    s.pop()

                s.append(input[i])

        # Condition for opening bracket
        elif(input[i] == ')'):
            while(s[-1] != '('):
                print(s[-1], end = "")
                s.pop()

                # If opening bracket not present
                if(len(s) == 0):
                    print('Wrong input')
                    exit(1)

            # pop the opening bracket.
            s.pop()

        i += 1

    # pop the remaining operators
    while(len(s) > 0):
        if(s[-1] == '('):
            print('Wrong input')
            exit(1)

        print(s[-1], end = "")
        s.pop()

# Driver code
input = "a+b*c-(d/e+f*g*h)"

inToPost(input)

# This code is contributed by dheeraj_2801
```

## C#

```
// C# program to convert an infix expression to a
// postfix expression using two precedence function
using System.Collections.Generic;
using System;
public class GFG {

    // to check if the input character
    // is an operator or a '('
    static int isOperator(char input)
    {
        switch (input) {
        case '+':
            return 1;
        case '-':
            return 1;
        case '*':
            return 1;
        case '%':
            return 1;
        case '/':
            return 1;
        case '(':
            return 1;
        }
        return 0;
    }

    // to check if the input character is an operand
    static int isOperand(char input)
    {
        if (input >= 65 && input <= 90
            || input >= 97 && input <= 122) {
            return 1;
        }
        return 0;
    }

    // function to return precedence value
    // if operator is present in stack
    static int inPrec(char input)
    {
        switch (input) {
        case '+':
        case '-':
            return 2;
        case '*':
        case '%':
        case '/':
            return 4;
        case '(':
            return 0;
        }
        return 0;
    }

    // function to return precedence value
    // if operator is present outside stack.
    static int outPrec(char input)
    {
        switch (input) {
        case '+':
        case '-':
            return 1;
        case '*':
        case '%':
        case '/':
            return 3;
        case '(':
            return 100;
        }
        return 0;
    }

    // function to convert infix to postfix
    static void inToPost(char[] input)
    {
        Stack<char> s = new Stack<char>();

        // while input is not NULL iterate
        int i = 0;
        while (input.Length != i) {

            // if character an operand
            if (isOperand(input[i]) == 1) {
                Console.Write(input[i]);
            }

            // if input is an operator, push
            else if (isOperator(input[i]) == 1) {
                if (s.Count == 0
                    || outPrec(input[i]) > inPrec(s.Peek())) {
                    s.Push(input[i]);
                }
                else {
                    while (s.Count != 0
                           && outPrec(input[i]) < inPrec(s.Peek())) {
                        Console.Write(s.Peek());
                        s.Pop();
                    }
                    s.Push(input[i]);
                }
            } // condition for opening bracket
            else if (input[i] == ')') {
                while (s.Peek() != '(') {
                    Console.Write(s.Peek());
                    s.Pop();

                    // if opening bracket not present
                    if (s.Count == 0) {
                        Console.Write("Wrong input\n");
                        return;
                    }
                }

                // pop the opening bracket.
                s.Pop();
            }
            i++;
        }

        // pop the remaining operators
        while (s.Count != 0) {
            if (s.Peek() == '(') {
                Console.Write("\n Wrong input\n");
                return;
            }
            Console.Write(s.Peek());
            s.Pop();
        }
    }

    // Driver code
    static public void Main()
    {
        char[] input = "a+b*c-(d/e+f*g*h)".ToCharArray();
        inToPost(input);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to convert an infix expression to a
    // postfix expression using two precedence function

    // to check if the input character
    // is an operator or a '('
    function isOperator(input)
    {
        switch (input) {
          case '+':
              return 1;
          case '-':
              return 1;
          case '*':
              return 1;
          case '%':
              return 1;
          case '/':
              return 1;
          case '(':
              return 1;
        }
        return 0;
    }

    // to check if the input character is an operand
    function isOperand(input)
    {
        if (input.charCodeAt() >= 65 && input.charCodeAt() <= 90
            || input.charCodeAt() >= 97 && input.charCodeAt() <= 122) {
            return 1;
        }
        return 0;
    }

    // function to return precedence value
    // if operator is present in stack
    function inPrec(input)
    {
        switch (input) {
          case '+':
          case '-':
              return 2;
          case '*':
          case '%':
          case '/':
              return 4;
          case '(':
              return 0;
        }
        return 0;
    }

    // function to return precedence value
    // if operator is present outside stack.
    function outPrec(input)
    {
        switch (input) {
          case '+':
          case '-':
              return 1;
          case '*':
          case '%':
          case '/':
              return 3;
          case '(':
              return 100;
        }
        return 0;
    }

    // function to convert infix to postfix
    function inToPost(input)
    {
        let s = [];

        // while input is not NULL iterate
        let i = 0;
        while (input.length != i) {

            // if character an operand
            if (isOperand(input[i]) == 1) {
                document.write(input[i]);
            }

            // if input is an operator, push
            else if (isOperator(input[i]) == 1) {
                if (s.length == 0
                    || outPrec(input[i]) > inPrec(s[s.length - 1])) {
                    s.push(input[i]);
                }
                else {
                    while (s.length != 0
                           && outPrec(input[i]) < inPrec(s[s.length - 1])) {
                        document.write(s[s.length - 1]);
                        s.pop();
                    }
                    s.push(input[i]);
                }
            } // condition for opening bracket
            else if (input[i] == ')') {
                while (s[s.length - 1] != '(') {
                    document.write(s[s.length - 1]);
                    s.pop();

                    // if opening bracket not present
                    if (s.length == 0) {
                        document.write("Wrong input" + "</br>");
                        return;
                    }
                }

                // pop the opening bracket.
                s.pop();
            }
            i++;
        }

        // pop the remaining operators
        while (s.length != 0) {
            if (s[s.length - 1] == '(') {
                document.write("</br>" + " Wrong input" + "</br>");
                return;
            }
            document.write(s[s.length - 1]);
            s.pop();
        }
    }

    let input = "a+b*c-(d/e+f*g*h)".split('');
      inToPost(input);

    // This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
abc*+de/fg*h*+-
```

**如何处理具有从右到左关联性的运算符？**
例如，电力操作员^.“a^b^c”的后缀是“abc^^”，但上面的解决方案会将后缀打印为“ab^c^”，这是错误的。
在上面的实现中，当我们看到一个优先级相等的运算符时，我们将其视为 lower。如果两个操作符留有关联性，我们需要考虑同样的问题。但是在从右向左结合的情况下，我们需要把它当作更高的优先级，并把它推到堆栈中。
T5 进场:

1.  如果输入字符是操作数，打印它。
2.  如果输入字符是运算符-
    *   如果堆栈为空，将其推入堆栈。
    *   如果((其优先级值大于顶部字符的优先级值)或(优先级相同且结合性从右向左)，按下。
    *   如果((其优先级值较低)或(优先级相同，关联性从左到右))，则从堆栈中弹出并打印，同时顶部字符的优先级大于输入字符的优先级值。
3.  如果输入字符是“)”，则弹出并打印，直到顶部是“(”。(' Pop '('但不要打印。)
4.  如果堆栈在遇到“(”之前变成空的，那么它就是一个无效的表达式。
5.  重复步骤 1-4，直到输入表达式被完全读取。
6.  从堆栈中弹出剩余的元素并打印出来。
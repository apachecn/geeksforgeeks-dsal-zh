# 栈|集合 4(后缀表达式的求值)

> 原文:[https://www . geesforgeks . org/stack-set-4-evaluation-postfix-expression/](https://www.geeksforgeeks.org/stack-set-4-evaluation-postfix-expression/)

后缀符号用于表示代数表达式。由于后缀中不需要括号，所以以后缀形式编写的表达式的计算速度比中缀符号快。我们已经讨论了[中缀到后缀的转换](https://www.geeksforgeeks.org/stack-set-2-infix-to-postfix/)。在这篇文章中，我们将讨论后缀表达式的求值。

以下是计算后缀表达式的算法。
1)创建一个堆栈来存储操作数(或值)。
2)扫描给定的表达式，并对每个扫描的元素执行以下操作。
…..a)如果元素是数字，将其推入堆栈
…..b)如果元素是运算符，从堆栈中弹出运算符的操作数。评估运算符并将结果推回到堆栈
3)当表达式结束时，堆栈中的数字就是最终答案

**例:**
让给定的表达式为“2 3 1 * + 9 -”。我们逐一扫描所有元素。
1)扫描‘2’，是个数字，就推栈。栈包含‘2’
2)扫描‘3’，再次是一个数字，把它推到栈，栈现在包含‘2 ^ 3’(从下往上)
3)扫描‘1’，再次是一个数字，把它推到栈，栈现在包含‘2 ^ 3 ^ 1’
4)扫描‘*’，它是一个运算符，从栈中弹出两个操作数，对操作数应用*运算符，我们得到 3*1，结果是 3。我们将结果“3”叠加。堆栈现在变成“2 3”。
5)扫描“+”，这是一个运算符，从堆栈中弹出两个操作数，对操作数应用+运算符，我们得到 3 + 2，结果是 5。我们将结果“5”叠加。堆栈现在变成“5”。
6)扫描‘9’，这是一个数字，我们把它推到堆栈上。堆栈现在变成了“5 9”。
7)扫描'-'，这是一个运算符，从堆栈中弹出两个操作数，对操作数应用–运算符，我们得到 5–9，结果是-4。我们将结果“-4”推送到堆栈。堆栈现在变成“-4”。
8)没有更多的元素需要扫描，我们从堆栈中返回顶部元素(这是堆栈中唯一剩下的元素)。

下面是上述算法的实现。

## C++

```
// C++ program to evaluate value of a postfix expression
#include <iostream>
#include <string.h>

using namespace std;

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
    struct Stack* stack = (struct Stack*) malloc(sizeof(struct Stack));

    if (!stack) return NULL;

    stack->top = -1;
    stack->capacity = capacity;
    stack->array = (int*) malloc(stack->capacity * sizeof(int));

    if (!stack->array) return NULL;

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

// The main function that returns value of a given postfix expression
int evaluatePostfix(char* exp)
{
    // Create a stack of capacity equal to expression size
    struct Stack* stack = createStack(strlen(exp));
    int i;

    // See if stack was created successfully
    if (!stack) return -1;

    // Scan all characters one by one
    for (i = 0; exp[i]; ++i)
    {
        // If the scanned character is an operand (number here),
        // push it to the stack.
        if (isdigit(exp[i]))
            push(stack, exp[i] - '0');

        // If the scanned character is an operator, pop two
        // elements from stack apply the operator
        else
        {
            int val1 = pop(stack);
            int val2 = pop(stack);
            switch (exp[i])
            {
            case '+': push(stack, val2 + val1); break;
            case '-': push(stack, val2 - val1); break;
            case '*': push(stack, val2 * val1); break;
            case '/': push(stack, val2/val1); break;
            }
        }
    }
    return pop(stack);
}

// Driver program to test above functions
int main()
{
    char exp[] = "231*+9-";
    cout<<"postfix evaluation: "<< evaluatePostfix(exp);
    return 0;
}
```

## C

```
// C program to evaluate value of a postfix expression
#include <stdio.h>
#include <string.h>
#include <ctype.h>
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
    struct Stack* stack = (struct Stack*) malloc(sizeof(struct Stack));

    if (!stack) return NULL;

    stack->top = -1;
    stack->capacity = capacity;
    stack->array = (int*) malloc(stack->capacity * sizeof(int));

    if (!stack->array) return NULL;

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

// The main function that returns value of a given postfix expression
int evaluatePostfix(char* exp)
{
    // Create a stack of capacity equal to expression size
    struct Stack* stack = createStack(strlen(exp));
    int i;

    // See if stack was created successfully
    if (!stack) return -1;

    // Scan all characters one by one
    for (i = 0; exp[i]; ++i)
    {
        // If the scanned character is an operand (number here),
        // push it to the stack.
        if (isdigit(exp[i]))
            push(stack, exp[i] - '0');

        // If the scanned character is an operator, pop two
        // elements from stack apply the operator
        else
        {
            int val1 = pop(stack);
            int val2 = pop(stack);
            switch (exp[i])
            {
            case '+': push(stack, val2 + val1); break;
            case '-': push(stack, val2 - val1); break;
            case '*': push(stack, val2 * val1); break;
            case '/': push(stack, val2/val1); break;
            }
        }
    }
    return pop(stack);
}

// Driver program to test above functions
int main()
{
    char exp[] = "231*+9-";
    printf ("postfix evaluation: %d", evaluatePostfix(exp));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to evaluate value of a postfix expression

import java.util.Stack;

public class Test
{
    // Method to evaluate value of a postfix expression
    static int evaluatePostfix(String exp)
    {
        //create a stack
        Stack<Integer> stack=new Stack<>();

        // Scan all characters one by one
        for(int i=0;i<exp.length();i++)
        {
            char c=exp.charAt(i);

            // If the scanned character is an operand (number here),
            // push it to the stack.
            if(Character.isDigit(c))
            stack.push(c - '0');

            //  If the scanned character is an operator, pop two
            // elements from stack apply the operator
            else
            {
                int val1 = stack.pop();
                int val2 = stack.pop();

                switch(c)
                {
                    case '+':
                    stack.push(val2+val1);
                    break;

                    case '-':
                    stack.push(val2- val1);
                    break;

                    case '/':
                    stack.push(val2/val1);
                    break;

                    case '*':
                    stack.push(val2*val1);
                    break;
              }
            }
        }
        return stack.pop();   
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        String exp="231*+9-";
        System.out.println("postfix evaluation: "+evaluatePostfix(exp));
    }
}
// Contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to evaluate value of a postfix expression

# Class to convert the expression
class Evaluate:

    # Constructor to initialize the class variables
    def __init__(self, capacity):
        self.top = -1
        self.capacity = capacity
        # This array is used a stack
        self.array = []

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

    # The main function that converts given infix expression
    # to postfix expression
    def evaluatePostfix(self, exp):

        # Iterate over the expression for conversion
        for i in exp:

            # If the scanned character is an operand
            # (number here) push it to the stack
            if i.isdigit():
                self.push(i)

            # If the scanned character is an operator,
            # pop two elements from stack and apply it.
            else:
                val1 = self.pop()
                val2 = self.pop()
                self.push(str(eval(val2 + i + val1)))

        return int(self.pop())

# Driver program to test above function
exp = "231*+9-"
obj = Evaluate(len(exp))
print "postfix evaluation: %d"%(obj.evaluatePostfix(exp))
# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to evaluate value of a postfix expression
using System;
using System.Collections;

namespace GFG
{
    class Geek
    {
        //Main() method
        static void Main()
        {
            Geek e = new Geek();
            e.v = ("231*+9-");
            e.expression();
            Console.WriteLine("postfix evaluation: " + e.answer);
            Console.Read();
        }

        public string v;
        //'v' is variable to store the string value

        public string answer;
        Stack i = new Stack();
        //'Stack()' is inbuilt function for namespace 'System.Collections'

        public void expression()
        //evaluation method
        {
            int a, b, ans;
            for (int j = 0; j < v.Length; j++)
            //'v.Length' means length of the string
            {
                String c = v.Substring(j, 1);
                if (c.Equals("*"))
                {
                    String sa = (String)i.Pop();
                    String sb = (String)i.Pop();
                    a = Convert.ToInt32(sb);
                    b = Convert.ToInt32(sa);
                    ans = a * b;
                    i.Push(ans.ToString());

                }
                else if (c.Equals("/"))
                {
                    String sa = (String)i.Pop();
                    String sb = (String)i.Pop();
                    a = Convert.ToInt32(sb);
                    b = Convert.ToInt32(sa);
                    ans = a / b;
                    i.Push(ans.ToString());
                }
                else if (c.Equals("+"))
                {
                    String sa = (String)i.Pop();
                    String sb = (String)i.Pop();
                    a = Convert.ToInt32(sb);
                    b = Convert.ToInt32(sa);
                    ans = a + b;
                    i.Push(ans.ToString());

                }
                else if (c.Equals("-"))
                {
                    String sa = (String)i.Pop();
                    String sb = (String)i.Pop();
                    a = Convert.ToInt32(sb);
                    b = Convert.ToInt32(sa);
                    ans = a - b;
                    i.Push(ans.ToString());

                }
                else
                {
                    i.Push(v.Substring(j, 1));
                }
            }
            answer = (String)i.Pop();
        }
    }
}
```

## java 描述语言

```
<script>

// Javascript program to evaluate value of a postfix expression

// Method to evaluate value of a postfix expression
function evaluatePostfix(exp)
{
    //create a stack
        let stack=[];

        // Scan all characters one by one
        for(let i=0;i<exp.length;i++)
        {
            let c=exp[i];

            // If the scanned character is an operand (number here),
            // push it to the stack.
            if(! isNaN( parseInt(c) ))
            stack.push(c.charCodeAt(0) - '0'.charCodeAt(0));

            //  If the scanned character is an operator, pop two
            // elements from stack apply the operator
            else
            {
                let val1 = stack.pop();
                let val2 = stack.pop();

                switch(c)
                {
                    case '+':
                    stack.push(val2+val1);
                    break;

                    case '-':
                    stack.push(val2- val1);
                    break;

                    case '/':
                    stack.push(val2/val1);
                    break;

                    case '*':
                    stack.push(val2*val1);
                    break;
              }
            }
        }
        return stack.pop();  
}

// Driver program to test above functions
let exp="231*+9-";
document.write("postfix evaluation: "+evaluatePostfix(exp));

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
postfix evaluation: -4
```

评估算法的时间复杂度为 O(n)，其中 n 是输入表达式中的字符数。

上述实现有以下限制。
1)它只支持 4 个二进制运算符“+”、“*”、“-”和“/”。通过增加更多的开关箱，可以扩展到更多的操作员。
2)允许的操作数只有一位数。通过在给定表达式的所有元素(运算符和操作数)之间添加一个类似分隔符的空格，程序可以扩展为多个数字。

下面给出的是扩展程序，它允许操作数有多个数字。

## C++

```
// C++ program to evaluate value of a postfix
// expression having multiple digit operands
#include <bits/stdc++.h>
using namespace std;

// Stack type
class Stack
{
    public:
    int top;
    unsigned capacity;
    int* array;
};

// Stack Operations
Stack* createStack( unsigned capacity )
{
    Stack* stack = new Stack();

    if (!stack) return NULL;

    stack->top = -1;
    stack->capacity = capacity;
    stack->array = new int[(stack->capacity * sizeof(int))];

    if (!stack->array) return NULL;

    return stack;
}

int isEmpty(Stack* stack)
{
    return stack->top == -1 ;
}

int peek(Stack* stack)
{
    return stack->array[stack->top];
}

int pop(Stack* stack)
{
    if (!isEmpty(stack))
        return stack->array[stack->top--] ;
    return '{content}apos;;
}

void push(Stack* stack,int op)
{
    stack->array[++stack->top] = op;
}

// The main function that returns value
// of a given postfix expression
int evaluatePostfix(char* exp)
{
    // Create a stack of capacity equal to expression size
    Stack* stack = createStack(strlen(exp));
    int i;

    // See if stack was created successfully
    if (!stack) return -1;

    // Scan all characters one by one
    for (i = 0; exp[i]; ++i)
    {
        //if the character is blank space then continue
        if(exp[i] == ' ')continue;

        // If the scanned character is an
        // operand (number here),extract the full number
        // Push it to the stack.
        else if (isdigit(exp[i]))
        {
            int num=0;

            //extract full number
            while(isdigit(exp[i]))
            {
            num = num * 10 + (int)(exp[i] - '0');
                i++;
            }
            i--;

            //push the element in the stack
            push(stack,num);
        }

        // If the scanned character is an operator, pop two
        // elements from stack apply the operator
        else
        {
            int val1 = pop(stack);
            int val2 = pop(stack);

            switch (exp[i])
            {
            case '+': push(stack, val2 + val1); break;
            case '-': push(stack, val2 - val1); break;
            case '*': push(stack, val2 * val1); break;
            case '/': push(stack, val2/val1); break;

            }
        }
    }
    return pop(stack);
}

// Driver code
int main()
{
    char exp[] = "100 200 + 2 / 5 * 7 +";
    cout << evaluatePostfix(exp);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to evaluate value of a postfix
// expression having multiple digit operands
#include <stdio.h>
#include <string.h>
#include <ctype.h>
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
    struct Stack* stack = (struct Stack*) malloc(sizeof(struct Stack));

    if (!stack) return NULL;

    stack->top = -1;
    stack->capacity = capacity;
    stack->array = (int*) malloc(stack->capacity * sizeof(int));

    if (!stack->array) return NULL;

    return stack;
}

int isEmpty(struct Stack* stack)
{
    return stack->top == -1 ;
}

int peek(struct Stack* stack)
{
    return stack->array[stack->top];
}

int pop(struct Stack* stack)
{
    if (!isEmpty(stack))
        return stack->array[stack->top--] ;
    return '{content}apos;;
}

void push(struct Stack* stack,int op)
{
    stack->array[++stack->top] = op;
}

// The main function that returns value
// of a given postfix expression
int evaluatePostfix(char* exp)
{
    // Create a stack of capacity equal to expression size
    struct Stack* stack = createStack(strlen(exp));
    int i;

    // See if stack was created successfully
    if (!stack) return -1;

    // Scan all characters one by one
    for (i = 0; exp[i]; ++i)
    {
        //if the character is blank space then continue
        if(exp[i]==' ')continue;

        // If the scanned character is an
        // operand (number here),extract the full number
        // Push it to the stack.
        else if (isdigit(exp[i]))
        {
            int num=0;

            //extract full number
            while(isdigit(exp[i]))
            {
            num=num*10 + (int)(exp[i]-'0');
                i++;
            }
            i--;

            //push the element in the stack
            push(stack,num);
        }

        // If the scanned character is an operator, pop two
        // elements from stack apply the operator
        else
        {
            int val1 = pop(stack);
            int val2 = pop(stack);

            switch (exp[i])
            {
            case '+': push(stack, val2 + val1); break;
            case '-': push(stack, val2 - val1); break;
            case '*': push(stack, val2 * val1); break;
            case '/': push(stack, val2/val1); break;

            }
        }
    }
    return pop(stack);
}

// Driver program to test above functions
int main()
{
    char exp[] = "100 200 + 2 / 5 * 7 +";
    printf ("%d", evaluatePostfix(exp));
    return 0;
}

// This code is contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to evaluate value of a postfix
// expression having multiple digit operands
import java.util.Stack;

class Test1
{
    // Method to evaluate value of a postfix expression
    static int evaluatePostfix(String exp)
    {
        //create a stack
        Stack<Integer> stack = new Stack<>();

        // Scan all characters one by one
        for(int i = 0; i < exp.length(); i++)
        {
            char c = exp.charAt(i);

            if(c == ' ')
            continue;

            // If the scanned character is an operand
            // (number here),extract the number
            // Push it to the stack.
            else if(Character.isDigit(c))
            {
                int n = 0;

                //extract the characters and store it in num
                while(Character.isDigit(c))
                {
                    n = n*10 + (int)(c-'0');
                    i++;
                    c = exp.charAt(i);
                }
                i--;

                //push the number in stack
                stack.push(n);
            }

            // If the scanned character is an operator, pop two
            // elements from stack apply the operator
            else
            {
                int val1 = stack.pop();
                int val2 = stack.pop();

                switch(c)
                {
                    case '+':
                    stack.push(val2+val1);
                    break;

                    case '-':
                    stack.push(val2- val1);
                    break;

                    case '/':
                    stack.push(val2/val1);
                    break;

                    case '*':
                    stack.push(val2*val1);
                    break;
            }
            }
        }
        return stack.pop();
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        String exp = "100 200 + 2 / 5 * 7 +";
        System.out.println(evaluatePostfix(exp));
    }
}

// This code is contributed by Arnab Kundu
```

## 计算机编程语言

```
# Python program to evaluate value of a postfix
# expression with integers containing multiple digits

class evalpostfix:
    def __init__(self):
        self.stack =[]
        self.top =-1
    def pop(self):
        if self.top ==-1:
            return
        else:
            self.top-= 1
            return self.stack.pop()
    def push(self, i):
        self.top+= 1
        self.stack.append(i)

    def centralfunc(self, ab):
        for i in ab:

            # if the component of the list is an integer
            try:
                self.push(int(i))
            # if the component of the list is not an integer,
            # it must be an operator. Using ValueError, we can
            # evaluate components of the list other than type int
            except ValueError:
                val1 = self.pop()
                val2 = self.pop()

                # switch statement to perform operation
                switcher ={'+':val2 + val1, '-':val2-val1, '*':val2 * val1, '/':val2 / val1, '^':val2**val1}
                self.push(switcher.get(i))
        return int(self.pop())

str ='100 200 + 2 / 5 * 7 +'

# splitting the given string to obtain
# integers and operators into a list
strconv = str.split(' ')
obj = evalpostfix()
print(obj.centralfunc(strconv))

# This code is contributed by Amarnath Reddy
```

## C#

```
// C# program to evaluate value of a postfix
// expression having multiple digit operands
using System;
using System.Collections.Generic;

class GFG
{
// Method to evaluate value of
// a postfix expression
public static int evaluatePostfix(string exp)
{
    // create a stack
    Stack<int> stack = new Stack<int>();

    // Scan all characters one by one
    for (int i = 0; i < exp.Length; i++)
    {
        char c = exp[i];

        if (c == ' ')
        {
            continue;
        }

        // If the scanned character is an 
        // operand (number here),extract
        // the number. Push it to the stack.
        else if (char.IsDigit(c))
        {
            int n = 0;

            // extract the characters and
            // store it in num
            while (char.IsDigit(c))
            {
                n = n * 10 + (int)(c - '0');
                i++;
                c = exp[i];
            }
            i--;

            // push the number in stack
            stack.Push(n);
        }

        // If the scanned character is
        // an operator, pop two elements
        // from stack apply the operator
        else
        {
            int val1 = stack.Pop();
            int val2 = stack.Pop();

            switch (c)
            {
                case '+':
                stack.Push(val2 + val1);
                break;

                case '-':
                stack.Push(val2 - val1);
                break;

                case '/':
                stack.Push(val2 / val1);
                break;

                case '*':
                stack.Push(val2 * val1);
                break;
            }
        }
    }
    return stack.Pop();
}

// Driver Code
public static void Main(string[] args)
{
    string exp = "100 200 + 2 / 5 * 7 +";
    Console.WriteLine(evaluatePostfix(exp));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript program to evaluate value of a postfix
    // expression having multiple digit operands

    // Method to evaluate value of
    // a postfix expression
    function evaluatePostfix(exp)
    {
        // create a stack
        let stack = [];

        // Scan all characters one by one
        for (let i = 0; i < exp.length; i++)
        {
            let c = exp[i];

            if (c == ' ')
            {
                continue;
            }

            // If the scanned character is an
            // operand (number here),extract
            // the number. Push it to the stack.
            else if (c >= '0' && c <= '9')
            {
                let n = 0;

                // extract the characters and
                // store it in num
                while (c >= '0' && c <= '9')
                {
                    n = n * 10 + (c - '0');
                    i++;
                    c = exp[i];
                }
                i--;

                // push the number in stack
                stack.push(n);
            }

            // If the scanned character is
            // an operator, pop two elements
            // from stack apply the operator
            else
            {
                let val1 = stack.pop();
                let val2 = stack.pop();

                switch (c)
                {
                    case '+':
                    stack.push(val2 + val1);
                    break;

                    case '-':
                    stack.push(val2 - val1);
                    break;

                    case '/':
                    stack.push(parseInt(val2 / val1, 10));
                    break;

                    case '*':
                    stack.push(val2 * val1);
                    break;
                }
            }
        }
        return stack.pop();
    }

    let exp = "100 200 + 2 / 5 * 7 +";
    document.write(evaluatePostfix(exp));

// This code is contributed by decode2207.
</script>
```

**输出:**

```
757
```

**参考文献:**
[http://www . cs . nthu . edu . tw/~ wk hon/ds/ds10/tutorial 2 . pdf](http://www.cs.nthu.edu.tw/~wkhon/ds/ds10/tutorial/tutorial2.pdf)
如有不正确之处请写评论，或想分享以上讨论话题的更多信息
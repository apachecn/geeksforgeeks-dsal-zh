# 将符号串解析为表达式

> 原文:[https://www . geesforgeks . org/parsing-字符串到表达式/](https://www.geeksforgeeks.org/parsing-string-of-symbols-to-expression/)

给定一个表达式为由数字和基本算术运算符(+、-、*、/)组成的字符串 **str** ，任务是求解该表达式。**注意**本程序使用的数字为一位数，不允许使用括号。
**例:**

> **输入:** str = "3/3+4*6-9"
> **输出:** 16
> 自(3 / 3) = 1 和(4 * 6) = 24。
> 于是整体表达式变成(1+24–9)= 16
> **输入:**str =“9 * 5-4 * 5+9”
> **输出:** 16

**方法:**创建一个[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)类来存储数字和运算符(都是字符)。堆栈是一种有用的存储机制，因为在解析表达式时，需要频繁访问最后存储的项；而堆栈是一个[后进先出](https://www.geeksforgeeks.org/lifo-last-in-first-out-approach-in-programming/)(后进先出)容器。
除了 Stack 类之外，还创建了一个名为 express(expression 的缩写)的类，表示整个算术表达式。此类的成员函数允许用户使用字符串形式的表达式初始化对象，解析表达式，并返回结果算术值。
下面是算术表达式的解析方法。
一个[指针](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)从左边开始，迭代查看每个字符。它可以是数字(始终是 0 到 9 之间的一位数字符)或运算符(字符+、-、*、和/)。
如果字符是一个数字，则被推送到堆栈上。遇到的第一个运算符也被推入堆栈。诀窍是处理后续的操作符。请注意，当前运算符无法执行，因为它后面的数字尚未被读取。找到一个运算符只是一个信号，表明我们可以执行存储在堆栈中的前一个运算符。也就是说，如果序列 2+3 在堆栈上，我们会等到找到另一个运算符后再执行加法。
因此，只要当前字符是运算符(除了第一个)，前一个数字(在前面的例子中是 3)和前一个运算符(+)就会从堆栈中弹出，将它们放在变量 lastval 和 lastop 中。最后，弹出第一个数字(2)，对两个数字进行算术运算(得到 5)。
但是，当遇到优先级高于+和–的*和/时，表达式无法执行。在表达式 3+4/2 中，在执行除法之前不能执行+运算。所以，2 和+被放回堆栈，直到执行除法。
另一方面，如果当前操作符是+或-，可以执行上一个操作符。也就是说，当表达式 4-5+6 中遇到+时，可以执行-，当表达式 6/2-3 中遇到–时，可以进行除法运算。表 10.1 显示了四种可能性。

<figure class="table">

| 上一个操作员 | 当前操作员 | 例子 | 行动 |
| --- | --- | --- | --- |
| +或– | *或/ | 3+4/ | 按下上一个运算符和上一个数字(+，4) |
| *或/ | *或/ | 9/3* | 执行前一个运算符，推送结果(3) |
| +或– | +或– | 6+3+ | 执行前一个运算符，推送结果(9) |
| *或/ | +或– | 8/2- | 执行前一个运算符，推送结果(4) |

</figure>

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <cstring>
#include <iostream>
using namespace std;

// Length of expressions in characters
const int LEN = 80;

// Size of the stack
const int MAX = 40;

class Stack {
private:
    // Stack: array of characters
    char st[MAX];

    // Number at top of the stack
    int top;

public:
    Stack()
    {
        top = 0;
    }

    // Function to put a character in stack
    void push(char var)
    {
        st[++top] = var;
    }

    // Function to return a character off stack
    char pop()
    {
        return st[top--];
    }

    // Function to get the top of the stack
    int gettop()
    {
        return top;
    }
};

// Expression class
class Express {
private:
    // Stack for analysis
    Stack s;

    // Pointer to input string
    char* pStr;

    // Length of the input string
    int len;

public:
    Express(char* ptr)
    {
        pStr = ptr;
        len = strlen(pStr);
    }

    // Parse the input string
    void parse();

    // Evaluate the stack
    int solve();
};

void Express::parse()
{

    // Character from the input string
    char ch;

    // Last value
    char lastval;

    // Last operator
    char lastop;

    // For each input character
    for (int j = 0; j < len; j++) {
        ch = pStr[j];

        // If it's a digit then save
        // the numerical value
        if (ch >= '0' && ch <= '9')
            s.push(ch - '0');

        // If it's an operator
        else if (ch == '+' || ch == '-'
                 || ch == '*' || ch == '/') {

            // If it is the first operator
            // then put it in the stack
            if (s.gettop() == 1)

                s.push(ch);

            // Not the first operator
            else {
                lastval = s.pop();
                lastop = s.pop();

                // If it is either '*' or '/' and the
                // last operator was either '+' or '-'
                if ((ch == '*' || ch == '/')
                    && (lastop == '+' || lastop == '-')) {

                    // Restore the last two pops
                    s.push(lastop);
                    s.push(lastval);
                }

                // In all the other cases
                else {

                    // Perform the last operation
                    switch (lastop) {

                    // Push the result in the stack
                    case '+':
                        s.push(s.pop() + lastval);
                        break;
                    case '-':
                        s.push(s.pop() - lastval);
                        break;
                    case '*':
                        s.push(s.pop() * lastval);
                        break;
                    case '/':
                        s.push(s.pop() / lastval);
                        break;
                    default:
                        cout << "\nUnknown oper";
                        exit(1);
                    }
                }
                s.push(ch);
            }
        }
        else {
            cout << "\nUnknown input character";
            exit(1);
        }
    }
}

int Express::solve()
{
    // Remove the items from stack
    char lastval;
    while (s.gettop() > 1) {
        lastval = s.pop();
        switch (s.pop()) {

        // Perform operation, push answer
        case '+':
            s.push(s.pop() + lastval);
            break;
        case '-':
            s.push(s.pop() - lastval);
            break;
        case '*':
            s.push(s.pop() * lastval);
            break;
        case '/':
            s.push(s.pop() / lastval);
            break;
        default:
            cout << "\nUnknown operator";
            exit(1);
        }
    }
    return int(s.pop());
}

// Driver code
int main()
{

    char string[LEN] = "2+3*4/3-2";

    // Make expression
    Express* eptr = new Express(string);

    // Parse it
    eptr->parse();

    // Solve the expression
    cout << eptr->solve();

    return 0;
}
```

**Output:** 

```
4
```

**时间复杂度** : O(N)。
**辅助空间** : O(N)。
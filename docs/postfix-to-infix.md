# 后缀到中缀

> 原文:[https://www.geeksforgeeks.org/postfix-to-infix/](https://www.geeksforgeeks.org/postfix-to-infix/)

**中缀表达式**:当一个运算符位于每对操作数之间时，a 运算 b 形式的表达式。
**后缀表达式**:a b op 形式的表达式，每对操作数后面跟一个运算符。
后缀表示法，也称为逆波兰表示法，是一种数学表达式的语法，其中数学运算符总是放在操作数之后。尽管后缀表达式很容易被计算机有效地评估，但是人类很难读懂它们。使用标准带括号中缀符号的复杂表达式通常比相应的后缀表达式更易读。因此，我们有时希望允许最终用户使用中缀符号，然后将其转换为后缀符号，以供计算机处理。此外，有时表达式是以后缀形式存储或生成的，我们希望将其转换为中缀，以便阅读和编辑
**示例:**

```
Input : abc++
Output : (a + (b + c))

Input  : ab*c+
Output : ((a*b)+c)
```

我们已经讨论过[中缀到后缀](https://www.geeksforgeeks.org/stack-set-2-infix-to-postfix/)。下面是后缀到中缀的算法。
T3】算法 T5】1。当左侧有输入符号时
…1.1 从输入中读取下一个符号。
2。如果符号是操作数
…2.1 将其推到堆栈上。
3。否则，
…3.1 符号为运算符。
…3.2 从堆栈中弹出前 2 个值。
…3.3 放操作符，以值为自变量，组成字符串。
…3.4 将结果字符串推回堆栈。
4。如果堆栈中只有一个值
…4.1 堆栈中的那个值是所需的中缀字符串。
以下是上述方法的实施:

## C++

```
// CPP program to find infix for
// a given postfix.
#include <bits/stdc++.h>
using namespace std;

bool isOperand(char x)
{
   return (x >= 'a' && x <= 'z') ||
          (x >= 'A' && x <= 'Z');
}

// Get Infix for a given postfix
// expression
string getInfix(string exp)
{
    stack<string> s;

    for (int i=0; exp[i]!='\0'; i++)
    {
        // Push operands
        if (isOperand(exp[i]))
        {
           string op(1, exp[i]);
           s.push(op);
        }

        // We assume that input is
        // a valid postfix and expect
        // an operator.
        else
        {
            string op1 = s.top();
            s.pop();
            string op2 = s.top();
            s.pop();
            s.push("(" + op2 + exp[i] +
                   op1 + ")");
        }
    }

    // There must be a single element
    // in stack now which is the required
    // infix.
    return s.top();
}

// Driver code
int main()
{
    string exp = "ab*c+";
    cout << getInfix(exp);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find infix for
// a given postfix.
import java.util.*;

class GFG
{

static boolean isOperand(char x)
{
    return (x >= 'a' && x <= 'z') ||
            (x >= 'A' && x <= 'Z');
}

// Get Infix for a given postfix
// expression
static String getInfix(String exp)
{
    Stack<String> s = new Stack<String>();

    for (int i = 0; i < exp.length(); i++)
    {
        // Push operands
        if (isOperand(exp.charAt(i)))
        {
        s.push(exp.charAt(i) + "");
        }

        // We assume that input is
        // a valid postfix and expect
        // an operator.
        else
        {
            String op1 = s.peek();
            s.pop();
            String op2 = s.peek();
            s.pop();
            s.push("(" + op2 + exp.charAt(i) +
                    op1 + ")");
        }
    }

    // There must be a single element
    // in stack now which is the required
    // infix.
    return s.peek();
}

// Driver code
public static void main(String args[])
{
    String exp = "ab*c+";
    System.out.println( getInfix(exp));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find infix for
# a given postfix.
def isOperand(x):
    return ((x >= 'a' and x <= 'z') or
            (x >= 'A' and x <= 'Z'))

# Get Infix for a given postfix
# expression
def getInfix(exp) :

    s = []

    for i in exp:    

        # Push operands
        if (isOperand(i)) :        
            s.insert(0, i)

        # We assume that input is a
        # valid postfix and expect
        # an operator.
        else:

            op1 = s[0]
            s.pop(0)
            op2 = s[0]
            s.pop(0)
            s.insert(0, "(" + op2 + i +
                             op1 + ")")

    # There must be a single element in
    # stack now which is the required
    # infix.
    return s[0]

# Driver Code
if __name__ == '__main__':

    exp = "ab*c+"
    print(getInfix(exp.strip()))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to find infix for
// a given postfix.
using System;
using System.Collections;

class GFG
{

static Boolean isOperand(char x)
{
    return (x >= 'a' && x <= 'z') ||
            (x >= 'A' && x <= 'Z');
}

// Get Infix for a given postfix
// expression
static String getInfix(String exp)
{
    Stack s = new Stack();

    for (int i = 0; i < exp.Length; i++)
    {
        // Push operands
        if (isOperand(exp[i]))
        {
            s.Push(exp[i] + "");
        }

        // We assume that input is
        // a valid postfix and expect
        // an operator.
        else
        {
            String op1 = (String) s.Peek();
            s.Pop();
            String op2 = (String) s.Peek();
            s.Pop();
            s.Push("(" + op2 + exp[i] +
                    op1 + ")");
        }
    }

    // There must be a single element
    // in stack now which is the required
    // infix.
    return (String)s.Peek();
}

// Driver code
public static void Main(String []args)
{
    String exp = "ab*c+";
    Console.WriteLine( getInfix(exp));
}
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

class Stack {
    protected $stack;
    protected $limit;

   function CreateStack($limit){
        $this->stack = array();
        $this->limit = $limit;
    }

    function push($item) {
        // trap for stack overflow
        if (count($this->stack) < $this->limit) {
            // prepend item to the start of the array
            array_unshift($this->stack, $item);
        } else {
            throw new RunTimeException('Stack is full!');
        }
    }

     function pop() {
        if ($this->isEmpty()) {
            // trap for stack underflow
          throw new RunTimeException('Stack is empty!');
      } else {
            // pop item from the start of the array
            return array_shift($this->stack);
        }
    }

     function top() {
        return current($this->stack);
    }

     function isEmpty() {
        return empty($this->stack);
    }

    function Prec($ch)
    {
        switch ($ch)
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
    function isOperand($ch)
    {
        return ($ch >= 'a' && $ch <= 'z') || ($ch >= 'A' && $ch <= 'Z');
    }

    function isOperator($x) {
      switch ($x) {
      case '+':
      case '-':
      case '/':
      case '*':
        return true;
      }
      return false;
    }

    public function  getInfix($exp)
    {

     $this->CreateStack(sizeof($exp));

    for ($i=0; $exp[$i]!= null; $i++)
    {
        // Push operands
        if ($this->isOperand($exp[$i]))
        {
            $op = $exp[$i];
            $this->push($op);
        }

        // We assume that input is
        // a valid postfix and expect
        // an operator.
        else
        {
                   $op1 = $this->top(); $this->pop();
                    $op2 = $this->top(); $this->pop();
                    $this->push("(". $op2 . $exp[$i] . $op1 . ")");
                    //$this->push($temp);

        }
    }

    // There must be a single element
    // in stack now which is the required
    // infix.
    return $this->top();
}
}
$myExample = new Stack();
echo $input =  "ab*c+";
$exp =  str_split($input,sizeof($input));
echo '<br>'.$data = $myExample->getInfix($exp);
?>
```

## java 描述语言

```
<script>

// JavaScript program to find infix for
// a given postfix.

function isOperand(x)
{
    return (x >= 'a' && x <= 'z') ||
            (x >= 'A' && x <= 'Z');
}

// Get Infix for a given postfix
// expression
function getInfix(exp)
{
    let s = [];

    for (let i = 0; i < exp.length; i++)
    {
        // Push operands
        if (isOperand(exp[i]))
        {
        s.push(exp[i] + "");
        }

        // We assume that input is
        // a valid postfix and expect
        // an operator.
        else
        {
            let op1 = s.pop();

            let op2 = s.pop();
            s.pop();
            s.push("(" + op2 + exp[i] +
                    op1 + ")");
        }
    }

    // There must be a single element
    // in stack now which is the required
    // infix.
    return s[s.length-1];
}

// Driver code
let exp = "ab*c+";
document.write( getInfix(exp));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
((a*b)+c)
```
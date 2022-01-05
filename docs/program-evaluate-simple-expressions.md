# 计算简单表达式的程序

> 原文:[https://www . geesforgeks . org/program-evaluate-simple-expressions/](https://www.geeksforgeeks.org/program-evaluate-simple-expressions/)

给你一个表示数字和操作数表达式的字符串。例如 1+2*3，1-2+4。您需要计算字符串或表达式。不，BODMAS 紧随其后。如果表达式的语法不正确，返回-1。
测试用例:
a) 1+2*3 将被评估为 9。
b) 4-2+6*3 将被评估为 24。
c) 1++2 将被评估为-1(无效)。
同样，在字符串中也可以出现空格。在这种情况下，我们需要忽略空格。比如:- 1*2 -1 等于 1。
来源:[亚马逊面试问题](https://www.geeksforgeeks.org/amazon-interview-set-98-campus/)
**强烈建议尽量减少浏览器，先自己试试这个。**
思路很简单，从第一个字符开始，从左到右遍历，检查两个连续的运算符和操作数等错误。我们还跟踪结果，并在遍历表达式时更新结果。
下面是计算给定表达式的程序。

## C++

```
// C++ program to evaluate a given expression
#include <iostream>
using namespace std;

// A utility function to check if a given character is operand
bool isOperand(char c) { return (c >= '0' && c <= '9'); }

// utility function to find value of and operand
int value(char c) {  return (c - '0'); }

// This function evaluates simple expressions. It returns -1 if the
// given expression is invalid.
int evaluate(char *exp)
{
    // Base Case: Given expression is empty
    if (*exp == '\0')  return -1;

    // The first character must be an operand, find its value
    int res = value(exp[0]);

    // Traverse the remaining characters in pairs
    for (int i = 1; exp[i]; i += 2)
    {
        // The next character must be an operator, and
        // next to next an operand
        char opr = exp[i], opd = exp[i+1];

        // If next to next character is not an operand
        if (!isOperand(opd))  return -1;

        // Update result according to the operator
        if (opr == '+')       res += value(opd);
        else if (opr == '-')  res -= value(opd);
        else if (opr == '*')  res *= value(opd);
        else if (opr == '/')  res /= value(opd);

        // If not a valid operator
        else                  return -1;
    }
    return res;
}

// Driver program to test above function
int main()
{
    char expr1[] = "1+2*5+3";
    int res = evaluate(expr1);
    (res == -1)? cout << expr1 << " is " << "Invalid\n":
                 cout << "Value of " << expr1 << " is " << res << endl;

    char expr2[] = "1+2*3";
    res = evaluate(expr2);
    (res == -1)? cout << expr2 << " is " << "Invalid\n":
                 cout << "Value of " << expr2 << " is " << res << endl;

    char expr3[] = "4-2+6*3";
    res = evaluate(expr3);
    (res == -1)? cout << expr3 << " is " << "Invalid\n":
                 cout << "Value of " << expr3 << " is " << res << endl;

    char expr4[] = "1++2";
    res = evaluate(expr4);
    (res == -1)? cout << expr4 << " is " << "Invalid\n":
                 cout << "Value of " << expr4 << " is " << res << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to evaluate a given expression

class GFG{
// A utility function to check if
// a given character is operand
static boolean isOperand(char c)
{
    return (c >= '0' && c <= '9');

}

// utility function to find value of and operand
static int value(char c)
{
    return (int)(c - '0');

}

// This function evaluates simple expressions.
// It returns -1 if the given
// expression is invalid.
static int evaluate(String exp)
{
    // Base Case: Given expression is empty
    if (exp.length() == 0) return -1;

    // The first character must be
    // an operand, find its value
    int res = value(exp.charAt(0));

    // Traverse the remaining characters in pairs
    for (int i = 1; i<exp.length(); i += 2)
    {
        // The next character must be an operator, and
        // next to next an operand
        char opr = exp.charAt(i), opd = exp.charAt(i+1);

        // If next to next character is not an operand
        if (isOperand(opd) == false) return -1;

        // Update result according to the operator
        if (opr == '+') res += value(opd);
        else if (opr == '-') res -= value(opd);
        else if (opr == '*') res *= value(opd);
        else if (opr == '/') res /= value(opd);

        // If not a valid operator
        else                 return -1;
    }
    return res;
}

// Driver program to test above function
public static void main(String[] args)
{
    String expr1 = "1+2*5+3";
    int res = evaluate(expr1);
    if(res == -1) System.out.println(expr1+" is Invalid");
    else     System.out.println("Value of "+expr1+" is "+res);

    String expr2 = "1+2*3";
    res = evaluate(expr2);
    if(res == -1) System.out.println(expr2+" is Invalid");
    else         System.out.println("Value of "+expr2+" is "+res);

    String expr3 = "4-2+6*3";
    res = evaluate(expr3);
    if(res == -1) System.out.println(expr3+" is Invalid");
    else         System.out.println("Value of "+expr3+" is "+res);

    String expr4 = "1++2";
    res = evaluate(expr4);
    if(res == -1) System.out.println(expr4+" is Invalid");
    else         System.out.println("Value of "+expr4+" is "+res);
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to evaluate a
# given expression

# A utility function to check if
# a given character is operand
def isOperand(c):

    return (c >= '0' and c <= '9');

# utility function to find
# value of and operand
def value(c):
    return ord(c) - ord('0');

# This function evaluates simple
# expressions. It returns -1 if the
# given expression is invalid.
def evaluate(exp):

    len1 = len(exp);

    # Base Case: Given expression is empty
    if (len1 == 0):
        return -1;

    # The first character must be
    # an operand, find its value
    res = value(exp[0]);

    # Traverse the remaining
    # characters in pairs
    for i in range(1,len1,2):
        # The next character must be
        # an operator, and next to
        # next an operand
        opr = exp[i];
        opd = exp[i + 1];

        # If next to next character
        # is not an operand
        if (isOperand(opd)==False):
            return -1;

        # Update result according
        # to the operator
        if (opr == '+'):
            res += value(opd);
        elif (opr == '-'):
            res -= int(value(opd));
        elif (opr == '*'):
            res *= int(value(opd));
        elif (opr == '/'):
            res /= int(value(opd));

        # If not a valid operator
        else:
            return -1;

    return res;

# Driver Code
expr1 = "1+2*5+3";
res = evaluate(expr1);
print(expr1,"is Invalid") if (res == -1) else print("Value of",expr1,"is",res);

expr2 = "1+2*3";
res = evaluate(expr2);
print(expr2,"is Invalid") if (res == -1) else print("Value of",expr2,"is",res);

expr3 = "4-2+6*3";
res = evaluate(expr3);
print(expr3,"is Invalid") if (res == -1) else print("Value of",expr3,"is",res);

expr4 = "1++2";
res = evaluate(expr4);
print(expr4,"is Invalid") if (res == -1) else print("Value of",expr4,"is",res);

# This code is contributed by mits
```

## C#

```
// C# program to evaluate a given expression
using System;
class GFG{

// A utility function to check if
// a given character is operand
static bool isOperand(char c) {
    return (c >= '0' && c <= '9');

}

// utility function to find value of and operand
static int value(char c) { return (int)(c - '0'); }

// This function evaluates simple
// expressions. It returns -1 if the
// given expression is invalid.
static int evaluate(string exp)
{
    // Base Case: Given expression is empty
    if (exp.Length == 0) return -1;

    // The first character must be
    // an operand, find its value
    int res = value(exp[0]);

    // Traverse the remaining characters in pairs
    for (int i = 1; i<exp.Length; i += 2)
    {
        // The next character must be an operator, and
        // next to next an operand
        char opr = exp[i], opd = exp[i+1];

        // If next to next character is not an operand
        if (isOperand(opd)==false) return -1;

        // Update result according to the operator
        if (opr == '+') res += value(opd);
        else if (opr == '-') res -= value(opd);
        else if (opr == '*') res *= value(opd);
        else if (opr == '/') res /= value(opd);

        // If not a valid operator
        else                 return -1;
    }
    return res;
}

// Driver program to test above function
static void Main()
{
    string expr1 = "1+2*5+3";
    int res = evaluate(expr1);
    if(res == -1)
    Console.WriteLine(expr1+" is Invalid");
    else    
    Console.WriteLine("Value of "+expr1+" is "+res);

    string expr2 = "1+2*3";
    res = evaluate(expr2);
    if(res == -1)
    Console.WriteLine(expr2+" is Invalid");
    else        
    Console.WriteLine("Value of "+expr2+" is "+res);

    string expr3 = "4-2+6*3";
    res = evaluate(expr3);
    if(res == -1)
    Console.WriteLine(expr3+" is Invalid");
    else        
    Console.WriteLine("Value of "+expr3+" is "+res);

    string expr4 = "1++2";
    res = evaluate(expr4);
    if(res == -1)
    Console.WriteLine(expr4+" is Invalid");
    else        
    Console.WriteLine("Value of "+expr4+" is "+res);
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to evaluate a
// given expression

// A utility function to check if
// a given character is operand
function isOperand($c)
{
    return ($c >= '0' && $c <= '9');
}

// utility function to find
// value of and operand
function value($c)
{
    return ($c - '0');
}

// This function evaluates simple
// expressions. It returns -1 if the
// given expression is invalid.
function evaluate($exp)
{
    $len = strlen($exp);

    // Base Case: Given expression is empty
    if ($len == 0) return -1;

    // The first character must be
    // an operand, find its value
    $res = (int)(value($exp[0]));

    // Traverse the remaining
    // characters in pairs
    for ($i = 1; $i < $len; $i += 2)
    {
        // The next character must be 
        // an operator, and next to
        // next an operand
        $opr = $exp[$i];
        $opd = $exp[$i + 1];

        // If next to next character
        // is not an operand
        if (!isOperand($opd))
        return -1;

        // Update result according
        // to the operator
        if ($opr == '+')    
        $res += value($opd);
        else if ($opr == '-')
            $res -= (int)(value($opd));
        else if ($opr == '*')
            $res *= (int)(value($opd));
        else if ($opr == '/')
            $res /= (int)(value($opd));

        // If not a valid operator
        else               
        return -1;
    }
    return $res;
}

// Driver Code
$expr1 = "1+2*5+3";
$res = evaluate($expr1);
($res == -1) ? print($expr1." is Invalid\n"):
               print("Value of " . $expr1 .
                     " is " . $res . "\n");

$expr2 = "1+2*3";
$res = evaluate($expr2);
($res == -1) ? print($expr2." is Invalid\n"):
               print("Value of " . $expr2 .
                     " is " . $res . "\n");

$expr3 = "4-2+6*3";
$res = evaluate($expr3);
($res == -1) ? print($expr3." is Invalid\n"):
               print("Value of " . $expr3 .
                     " is " . $res . "\n");

$expr4 = "1++2";
$res = evaluate($expr4);
($res == -1) ? print($expr4." is Invalid\n"):
               print("Value of " . $expr4 .
                     " is " . $res . "\n");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to evaluate a given expression

// A utility function to check if
// a given character is operand
function isOperand(c)
{
    return (c.charCodeAt(0) >= '0'.charCodeAt(0) && c.charCodeAt(0) <= '9'.charCodeAt(0));
}

// utility function to find value of and operand
function value(c)
{
    return (c.charCodeAt(0) - '0'.charCodeAt(0));
}

// This function evaluates simple expressions.
// It returns -1 if the given
// expression is invalid.
function evaluate(exp)
{
    // Base Case: Given expression is empty
    if (exp.length == 0) return -1;

    // The first character must be
    // an operand, find its value
    let res = value(exp[0]);

    // Traverse the remaining characters in pairs
    for (let i = 1; i<exp.length; i += 2)
    {
        // The next character must be an operator, and
        // next to next an operand
        let opr = exp[i], opd = exp[i+1];

        // If next to next character is not an operand
        if (isOperand(opd) == false) return -1;

        // Update result according to the operator
        if (opr == '+') res += value(opd);
        else if (opr == '-') res -= value(opd);
        else if (opr == '*') res *= value(opd);
        else if (opr == '/') res /= value(opd);

        // If not a valid operator
        else                 return -1;
    }
    return res;
}

// Driver program to test above function
let expr1 = "1+2*5+3";
let res = evaluate(expr1);
if(res == -1) document.write(expr1+" is Invalid<br>");
else     document.write("Value of "+expr1+" is "+res+"<br>");

let expr2 = "1+2*3";
res = evaluate(expr2);
if(res == -1) document.write(expr2+" is Invalid<br>");
else         document.write("Value of "+expr2+" is "+res+"<br>");

let expr3 = "4-2+6*3";
res = evaluate(expr3);
if(res == -1) document.write(expr3+" is Invalid<br>");
else         document.write("Value of "+expr3+" is "+res+"<br>");

let expr4 = "1++2";
res = evaluate(expr4);
if(res == -1) document.write(expr4+" is Invalid<br>");
else         document.write("Value of "+expr4+" is "+res+"<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Value of 1+2*5+3 is 18
Value of 1+2*3 is 9
Value of 4-2+6*3 is 24
1++2 is Invalid
```

时间复杂度:O(|exp|)

辅助空间:0(1)

上面的代码不处理空格。我们可以通过首先移除给定字符串中的所有空格来处理空格。更好的解决方案是在单次遍历中处理空间。这是一个练习。
时间复杂度为 O(n)，其中 n 为给定表达式的长度。
本文由**阿布舍克**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息
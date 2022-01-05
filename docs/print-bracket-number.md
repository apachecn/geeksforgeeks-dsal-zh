# 打印括号号

> 原文:[https://www.geeksforgeeks.org/print-bracket-number/](https://www.geeksforgeeks.org/print-bracket-number/)

给定一个长度为 **n** 的表达式 **exp** ，由一些括号组成。任务是在解析表达式时打印括号数字。
**例:**

```
Input : (a+(b*c))+(d/e)
Output : 1 2 2 1 3 3
The highlighted brackets in the given expression
(a+(b*c))+(d/e) has been assigned the numbers as:
1 2 2 1 3 3.

Input : ((())(()))
Output : 1 2 3 3 2 4 5 5 4 1 
```

**来源:**T2】Flipkart 采访体验|第 49 集。

**接近** :

1.  定义一个变量 **left_bnum** = 1。
2.  创建一个堆栈 **right_bnum** 。
3.  现在，对于 i = 0 到 n-1。
    1.  如果 exp[i] == '(')，则打印 **left_bnum** ，将 **left_bnum** 推到堆栈 **right_bnum** 上，最后将 **left_bnum** 增加 1。
    2.  否则如果 exp[i] == ')'，则打印堆栈的顶部元素 **right_bnum** ，然后从堆栈中弹出顶部元素。

## C++

```
// C++ implementation to print the bracket number
#include <bits/stdc++.h>

using namespace std;

// function to print the bracket number
void printBracketNumber(string exp, int n)
{
    // used to print the bracket number
    // for the left bracket
    int left_bnum = 1;

    // used to obtain the bracket number
    // for the right bracket
    stack<int> right_bnum;

    // traverse the given expression 'exp'
    for (int i = 0; i < n; i++) {

        // if current character is a left bracket
        if (exp[i] == '(') {
            // print 'left_bnum',
            cout << left_bnum << " ";

            // push 'left_bum' on to the stack 'right_bnum'
            right_bnum.push(left_bnum);

            // increment 'left_bnum' by 1
            left_bnum++;
        }

        // else if current character is a right bracket
        else if(exp[i] == ')') {

            // print the top element of stack 'right_bnum'
            // it will be the right bracket number
            cout << right_bnum.top() << " ";

            // pop the top element from the stack
            right_bnum.pop();
        }
    }
}

// Driver program to test above
int main()
{
    string exp = "(a+(b*c))+(d/e)";
    int n = exp.size();

    printBracketNumber(exp, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// print the bracket number
import java.io.*;
import java.util.*;

class GFG
{
    // function to print
    // the bracket number
    static void printBracketNumber(String exp,
                                   int n)
    {
        // used to print the
        // bracket number for
        // the left bracket
        int left_bnum = 1;

        // used to obtain the
        // bracket number for
        // the right bracket
        Stack<Integer> right_bnum =
                   new Stack<Integer>();

        // traverse the given
        // expression 'exp'
        for (int i = 0; i < n; i++)
        {

            // if current character
            // is a left bracket
            if (exp.charAt(i) == '(')
            {

                // print 'left_bnum',
                System.out.print(
                       left_bnum + " ");

                // push 'left_bum' on to
                // the stack 'right_bnum'
                right_bnum.push(left_bnum);

                // increment 'left_bnum' by 1
                left_bnum++;
            }

            // else if current character
            // is a right bracket
            else if(exp.charAt(i) == ')')
            {

                // print the top element
                // of stack 'right_bnum'
                // it will be the right
                // bracket number
                System.out.print(
                       right_bnum.peek() + " ");

                // pop the top element
                // from the stack
                right_bnum.pop();
            }
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        String exp = "(a+(b*c))+(d/e)";
        int n = exp.length();

        printBracketNumber(exp, n);
    }
}

// This code is contributed
// by Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 implementation to print the bracket number

# function to print the bracket number
def printBracketNumber(exp, n):

    # used to print the bracket number
    # for the left bracket
    left_bnum = 1

    # used to obtain the bracket number
    # for the right bracket
    right_bnum = list()

    # traverse the given expression 'exp'
    for i in range(n):

        # if current character is a left bracket
        if exp[i] == '(':

            # print 'left_bnum',
            print(left_bnum, end = " ")

            # push 'left_bum' on to the stack 'right_bnum'
            right_bnum.append(left_bnum)

            # increment 'left_bnum' by 1
            left_bnum += 1

        # else if current character is a right bracket
        elif exp[i] == ')':

            # print the top element of stack 'right_bnum'
            # it will be the right bracket number
            print(right_bnum[-1], end = " ")

            # pop the top element from the stack
            right_bnum.pop()

# Driver Code
if __name__ == "__main__":
    exp = "(a+(b*c))+(d/e)"
    n = len(exp)

    printBracketNumber(exp, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation to
// print the bracket number
using System;
using System.Collections.Generic;

class GFG
{
    // function to print
    // the bracket number
    static void printBracketNumber(string exp,
                                   int n)
    {
        // used to print the bracket
        // number for the left bracket
        int left_bnum = 1;

        // used to obtain the bracket 
        // number for the right bracket
        Stack<int> right_bnum = new Stack<int>();

        // traverse the given
        // expression 'exp'
        for (int i = 0; i < n; i++)
        {

            // if current character
            // is a left bracket
            if (exp[i] == '(')
            {

                // print 'left_bnum',
                Console.Write(left_bnum + " ");

                // Push 'left_bum' on to
                // the stack 'right_bnum'
                right_bnum.Push(left_bnum);

                // increment 'left_bnum' by 1
                left_bnum++;
            }

            // else if current character
            // is a right bracket
            else if(exp[i] == ')')
            {

                // print the top element
                // of stack 'right_bnum'
                // it will be the right
                // bracket number
                Console.Write(right_bnum.Peek() + " ");

                // Pop the top element
                // from the stack
                right_bnum.Pop();
            }
        }
    }

    // Driver Code
    static void Main()
    {
        string exp = "(a+(b*c))+(d/e)";
        int n = exp.Length;

        printBracketNumber(exp, n);
    }
}

// This code is contributed
// by Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// print the bracket number

// function to print
// the bracket number
function printBracketNumber($exp, $n)
{
    // used to print the
    // bracket number for
    // the left bracket
    $left_bnum = 1;

    // used to obtain the
    // bracket number for
    // the right bracket
    $right_bnum = array();
    $t = 0;

    // traverse the given
    // expression 'exp'
    for ($i = 0; $i < $n; $i++)
    {

        // if current character
        // is a left bracket
        if ($exp[$i] == '(')
        {

            // print 'left_bnum',
            echo $left_bnum . " ";

            // push 'left_bum' on to
            // the stack 'right_bnum'
            $right_bnum[$t++] = $left_bnum;

            // increment 'left_bnum' by 1
            $left_bnum++;
        }

        // else if current character
        // is a right bracket
        else if($exp[$i] == ')')
        {

            // print the top element
            // of stack 'right_bnum'
            // it will be the right
            // bracket number
            echo $right_bnum[$t - 1] . " ";

            // pop the top element
            // from the stack
            $right_bnum[$t - 1] = 1;
            $t--;
        }
    }
}

// Driver Code
$exp = "(a+(b*c))+(d/e)";
$n = strlen($exp);

printBracketNumber($exp, $n);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation to print the bracket number

// function to print the bracket number
function printBracketNumber(exp, n)
{
    // used to print the bracket number
    // for the left bracket
    var left_bnum = 1;

    // used to obtain the bracket number
    // for the right bracket
    var right_bnum = [];

    // traverse the given expression 'exp'
    for (var i = 0; i < n; i++) {

        // if current character is a left bracket
        if (exp[i] == '(') {
            // print 'left_bnum',
            document.write( left_bnum + " ");

            // push 'left_bum' on to the stack 'right_bnum'
            right_bnum.push(left_bnum);

            // increment 'left_bnum' by 1
            left_bnum++;
        }

        // else if current character is a right bracket
        else if(exp[i] == ')') {

            // print the top element of stack 'right_bnum'
            // it will be the right bracket number
            document.write( right_bnum[right_bnum.length-1] + " ");

            // pop the top element from the stack
            right_bnum.pop();
        }
    }
}

// Driver program to test above
var exp = "(a+(b*c))+(d/e)";
var n = exp.length;

printBracketNumber(exp, n);

</script>
```

**Output:** 

```
1 2 2 1 3 3
```

**时间复杂度:** O(n)。
**辅助空间:** O(n)。
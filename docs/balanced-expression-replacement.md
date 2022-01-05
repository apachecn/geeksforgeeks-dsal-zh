# 带替换的平衡表达

> 原文:[https://www . geesforgeks . org/balanced-expression-replacement/](https://www.geeksforgeeks.org/balanced-expression-replacement/)

给定一个只包含以下内容的字符串= >“{”、“}”、“(”、“)”、“[”、“]”。有些地方用“X”代替任何括号。确定是否可以通过用适当的括号替换所有的 X 来建立有效的括号序列。

**先决条件:** [平衡括号表达式](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)

**示例:**

```
Input : S = "{(X[X])}"
Output : Balanced
The balanced expression after 
replacing X with suitable bracket is:
{([[]])}.

Input : [{X}(X)]
Output : Not balanced
No substitution of X with any bracket
results in a balanced expression.
```

**方法:**我们讨论了一个验证给定的[括号表达式是否平衡的解决方案](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)。
遵循本文描述的相同方法，堆栈数据结构用于验证给定表达式是否平衡。对于字符串中的每种类型的字符，要在堆栈上执行的操作是:

1.  { '或'('或'[':当字符串的当前元素是左括号时，将该元素推入堆栈。
2.  } '或']'或')' :当字符串的当前元素是右括号时，弹出堆栈的顶部元素，并检查它是否是右括号的匹配左括号。如果匹配，则移动到字符串的下一个元素。如果不是，则当前字符串不平衡。从堆栈中弹出的元素也有可能是“X”。在这种情况下，“X”是一个匹配的开括号，因为只有当它被假定为下一步中描述的开括号时，它才会被推入堆栈。
3.  ' X ':当当前元素是 X 时，它可以是一个开始括号或结束括号。首先假设它是一个起始括号，并通过在堆栈中推入 X 来递归调用下一个元素。如果递归的结果为假，那么 X 是一个结束括号，它与堆栈顶部的括号匹配(如果堆栈非空)。所以弹出顶部元素并递归调用下一个元素。如果递归的结果再次为假，则表达式不平衡。

还要检查堆栈为空且当前元素为右括号时的情况。在这种情况下，表达式是不平衡的。

**实施:**

## C++

```
// C++ program to determine whether given
// expression is balanced/ parenthesis
// expression or not.
#include <bits/stdc++.h>
using namespace std;

// Function to check if two brackets are matching
// or not.
int isMatching(char a, char b)
{
    if ((a == '{' && b == '}') || (a == '[' && b == ']')
        || (a == '(' && b == ')') || a == 'X')
        return 1;
    return 0;
}

// Recursive function to check if given expression
// is balanced or not.
int isBalanced(string s, stack<char> ele, int ind)
{

    // Base case.
    // If the string is balanced then all the opening
    // brackets had been popped and stack should be
    // empty after string is traversed completely.
    if (ind == s.length())
        return ele.empty();

    // variable to store element at the top of the stack.
    char topEle;

    // variable to store result of recursive call.
    int res;

    // Case 1: When current element is an opening bracket
    // then push that element in the stack.
    if (s[ind] == '{' || s[ind] == '(' || s[ind] == '[') {
        ele.push(s[ind]);
        return isBalanced(s, ele, ind + 1);
    }

    // Case 2: When current element is a closing bracket
    // then check for matching bracket at the top of the
    // stack.
    else if (s[ind] == '}' || s[ind] == ')' || s[ind] == ']') {

        // If stack is empty then there is no matching opening
        // bracket for current closing bracket and the
        // expression is not balanced.
        if (ele.empty())
            return 0;

        topEle = ele.top();
        ele.pop();

        // Check bracket is matching or not.
        if (!isMatching(topEle, s[ind]))
            return 0;

        return isBalanced(s, ele, ind + 1);
    }

    // Case 3: If current element is 'X' then check
    // for both the cases when 'X' could be opening
    // or closing bracket.
    else if (s[ind] == 'X') {
        stack<char> tmp = ele;
        tmp.push(s[ind]);
        res = isBalanced(s, tmp, ind + 1);
        if (res)
            return 1;
        if (ele.empty())
            return 0;
        ele.pop();
        return isBalanced(s, ele, ind + 1);
    }
}

int main()
{
    string s = "{(X}[]";
    stack<char> ele;
    if (isBalanced(s, ele, 0))
        cout << "Balanced";   
    else
        cout << "Not Balanced";   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to determine
// whether given expression
// is balanced/ parenthesis
// expression or not.
import java.util.Stack;

class GFG {
    // Function to check if two
    // brackets are matching or not.

    static int isMatching(char a,
            char b) {
        if ((a == '{' && b == '}')
                || (a == '[' && b == ']')
                || (a == '(' && b == ')') || a == 'X') {
            return 1;
        }
        return 0;
    }

    // Recursive function to
    // check if given expression
    // is balanced or not.
    static int isBalanced(String s,
            Stack<Character> ele,
            int ind) {

        // Base case.
        // If the string is balanced
        // then all the opening brackets
        // had been popped and stack
        // should be empty after string
        // is traversed completely.
        if (ind == s.length()) {
            if (ele.size() == 0) {
                return 1;
            } else {
                return 0;
            }
        }

        // variable to store element
        // at the top of the stack.
        char topEle;

        // variable to store result
        // of recursive call.
        int res;

        // Case 1: When current element
        // is an opening bracket
        // then push that element
        // in the stack.
        if (s.charAt(ind) == '{'
                || s.charAt(ind) == '('
                || s.charAt(ind) == '[') {
            ele.push(s.charAt(ind));
            return isBalanced(s, ele, ind + 1);
        } // Case 2: When current element
        // is a closing bracket then
        // check for matching bracket
        // at the top of the stack.
        else if (s.charAt(ind) == '}'
                || s.charAt(ind) == ')'
                || s.charAt(ind) == ']') {

            // If stack is empty then there
            // is no matching opening bracket
            // for current closing bracket and
            // the expression is not balanced.
            if (ele.size() == 0) {
                return 0;
            }

            topEle = ele.peek();
            ele.pop();

            // Check bracket is
            // matching or not.
            if (isMatching(topEle, s.charAt(ind)) == 0) {
                return 0;
            }

            return isBalanced(s, ele, ind + 1);
        } // Case 3: If current element
        // is 'X' then check for both
        // the cases when 'X' could be
        // opening or closing bracket.
        else if (s.charAt(ind) == 'X') {
            Stack<Character> tmp = new Stack<>();
            //because in java, direct assignment copies only reference and not the whole object
            tmp.addAll(ele);
            tmp.push(s.charAt(ind));
            res = isBalanced(s, tmp, ind + 1);
            if (res == 1) {
                return 1;
            }
            if (ele.size() == 0) {
                return 0;
            }
            ele.pop();
            return isBalanced(s, ele, ind + 1);
        }
        return 1;
    }

    // Driver Code
    public static void main(String[] args) {

        String s = "{(X}[]";
        Stack<Character> ele = new Stack<Character>();

        if (isBalanced(s, ele, 0) != 0) {
            System.out.println("Balanced");
        } else {
            System.out.println("Not Balanced");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 program to determine whether
# given expression is balanced/ parenthesis
# expression or not.

# Function to check if two brackets are
# matching or not.
def isMatching(a, b):

    if ((a == '{' and b == '}') or
        (a == '[' and b == ']') or
        (a == '(' and b == ')') or
         a == 'X'):
        return 1

    return 0

# Recursive function to check if given
# expression is balanced or not.
def isBalanced(s, ele, ind):

    # Base case.
    # If the string is balanced then all the
    # opening brackets had been popped and
    # stack should be empty after string is
    # traversed completely.
    if (ind == len(s)):
        if len(ele) == 0:
            return True
        else:
            return False

    # Variable to store element at the top
    # of the stack.
    # char topEle;

    # Variable to store result of
    # recursive call.
    # int res;

    # Case 1: When current element is an
    # opening bracket then push that
    # element in the stack.
    if (s[ind] == '{' or s[ind] == '(' or
        s[ind] == '['):
        ele.append(s[ind])
        return isBalanced(s, ele, ind + 1)

    # Case 2: When current element is a closing
    # bracket then check for matching bracket
    # at the top of the stack.
    elif (s[ind] == '}' or s[ind] == ')' or
          s[ind] == ']'):

        # If stack is empty then there is no matching
        # opening bracket for current closing bracket
        # and the expression is not balanced.
        if (len(ele) == 0):
            return 0

        topEle = ele[-1]
        ele.pop()

        # Check bracket is matching or not.
        if (isMatching(topEle, s[ind]) == 0):
            return 0

        return isBalanced(s, ele, ind + 1)

    # Case 3: If current element is 'X' then check
    # for both the cases when 'X' could be opening
    # or closing bracket.
    elif (s[ind] == 'X'):
        tmp = ele
        tmp.append(s[ind])
        res = isBalanced(s, tmp, ind + 1)

        if (res):
            return 1
        if (len(ele) == 0):
            return 0

        ele.pop()

        return isBalanced(s, ele, ind + 1)

# Driver Code
s = "{(X}[]"
ele = []

if (isBalanced(s, ele, 0)):
    print("Balanced")
else:
    print("Not Balanced")

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to determine
// whether given expression
// is balanced/ parenthesis
// expression or not.
using System;
using System.Collections.Generic;

class GFG
{
    // Function to check if two
    // brackets are matching or not.
    static int isMatching(char a,
                          char b)
    {
        if ((a == '{' && b == '}') ||
            (a == '[' && b == ']') ||
            (a == '(' && b == ')') || a == 'X')
            return 1;
        return 0;
    }

    // Recursive function to
    // check if given expression
    // is balanced or not.
    static int isBalanced(string s,
                          Stack<char> ele,
                          int ind)
    {

        // Base case.
        // If the string is balanced
        // then all the opening brackets
        // had been popped and stack
        // should be empty after string
        // is traversed completely.
        if (ind == s.Length)
        {
            if (ele.Count == 0)
                return 1;
            else
                return 0;
        }

        // variable to store element
        // at the top of the stack.
        char topEle;

        // variable to store result
        // of recursive call.
        int res;

        // Case 1: When current element
        // is an opening bracket
        // then push that element
        // in the stack.
        if (s[ind] == '{' ||
            s[ind] == '(' ||
            s[ind] == '[')
        {
            ele.Push(s[ind]);
            return isBalanced(s, ele, ind + 1);
        }

        // Case 2: When current element
        // is a closing bracket then
        // check for matching bracket
        // at the top of the stack.
        else if (s[ind] == '}' ||
                 s[ind] == ')' ||
                 s[ind] == ']')
        {

            // If stack is empty then there
            // is no matching opening bracket
            // for current closing bracket and
            // the expression is not balanced.
            if (ele.Count == 0)
                return 0;

            topEle = ele.Peek();
            ele.Pop();

            // Check bracket is
            // matching or not.
            if (isMatching(topEle, s[ind]) == 0)
                return 0;

            return isBalanced(s, ele, ind + 1);
        }

        // Case 3: If current element
        // is 'X' then check for both
        // the cases when 'X' could be
        // opening or closing bracket.
        else if (s[ind] == 'X')
        {
            Stack<char> tmp = ele;
            tmp.Push(s[ind]);
            res = isBalanced(s, tmp, ind + 1);
            if (res == 1)
                return 1;
            if (ele.Count == 0)
                return 0;
            ele.Pop();
            return isBalanced(s, ele, ind + 1);
        }
        return 1;
    }

    // Driver Code
    static void Main()
    {
        string s = "{(X}[]";
        Stack<char> ele = new Stack<char>();

        if (isBalanced(s, ele, 0) != 0)
            Console.Write("Balanced");
        else
            Console.Write("Not Balanced");
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>

// JavaScript program to determine whether given
// expression is balanced/ parenthesis
// expression or not.

// Function to check if two brackets are matching
// or not.
function isMatching(a, b)
{
    if ((a == '{' && b == '}') || (a == '[' && b == ']')
        || (a == '(' && b == ')') || a == 'X')
        return 1;
    return 0;
}

// Recursive function to check if given expression
// is balanced or not.
function isBalanced(s, ele, ind)
{

    // Base case.
    // If the string is balanced then all the opening
    // brackets had been popped and stack should be
    // empty after string is traversed completely.
    if (ind == s.length)
        return ele.length==0;

    // variable to store element at the top of the stack.
    var topEle;

    // variable to store result of recursive call.
    var res;

    // Case 1: When current element is an opening bracket
    // then push that element in the stack.
    if (s[ind] == '{' || s[ind] == '(' || s[ind] == '[') {
        ele.push(s[ind]);
        return isBalanced(s, ele, ind + 1);
    }

    // Case 2: When current element is a closing bracket
    // then check for matching bracket at the top of the
    // stack.
    else if (s[ind] == '}' || s[ind] == ')' || s[ind] == ']') {

        // If stack is empty then there is no matching opening
        // bracket for current closing bracket and the
        // expression is not balanced.
        if (ele.length==0)
            return 0;

        topEle = ele[ele.length-1];
        ele.pop();

        // Check bracket is matching or not.
        if (!isMatching(topEle, s[ind]))
            return 0;

        return isBalanced(s, ele, ind + 1);
    }

    // Case 3: If current element is 'X' then check
    // for both the cases when 'X' could be opening
    // or closing bracket.
    else if (s[ind] == 'X') {
        var tmp = ele;
        tmp.push(s[ind]);
        res = isBalanced(s, tmp, ind + 1);
        if (res)
            return 1;
        if (ele.length==0)
            return 0;
        ele.pop();
        return isBalanced(s, ele, ind + 1);
    }
}

var s = "{(X}[]";
var ele = [];
if (isBalanced(s, ele, 0))
    document.write( "Balanced");   
else
    document.write( "Not Balanced");   

</script>
```

**Output:** 

```
Balanced
```

**时间复杂度:**o((2^n)*n)
T3】辅助空间: O(N)
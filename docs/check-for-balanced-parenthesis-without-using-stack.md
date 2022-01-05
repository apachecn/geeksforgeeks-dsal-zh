# 不使用堆栈检查平衡括号

> 原文:[https://www . geesforgeks . org/检查平衡括号-不使用堆栈/](https://www.geeksforgeeks.org/check-for-balanced-parenthesis-without-using-stack/)

给定一个表达式字符串 exp，编写一个程序来检查“{”、“}”、“(”、“”、“[”、“]”的对和顺序在 exp 中是否正确。
**例:**

```
Input : exp = “[()]{}{[()()]()}”
Output : true

Input : exp = “[(])”
Output : false
```

[Recommended: Please solve it on “***<u>PRACTICE</u>***” first, before moving on to the solution.](https://practice.geeksforgeeks.org/problems/parenthesis-checker/0)

我们已经讨论了基于[堆栈的解决方案](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)。这里不允许我们使用堆栈。看来这个问题没有多余的空间是解决不了的(请看最后的评论)。我们使用[递归](https://www.geeksforgeeks.org/recursion/)来解决这个问题。
下面是上述算法的实现:

## C++

```
// CPP program to check if parenthesis are
// balanced or not in an expression.
#include <bits/stdc++.h>
using namespace std;

char findClosing(char c)
{
    if (c == '(')
        return ')';
    if (c == '{')
        return '}';
    if (c == '[')
        return ']';
    return -1;
}

// function to check if parenthesis are
// balanced.
bool check(char expr[], int n)
{
    // Base cases
    if (n == 0)
        return true;
    if (n == 1)
        return false;
    if (expr[0] == ')' || expr[0] == '}' || expr[0] == ']')
        return false;

    // Search for closing bracket for first
    // opening bracket.
    char closing = findClosing(expr[0]);

    // count is used to handle cases like
    // "((()))".  We basically need to
    // consider matching closing bracket.
    int i, count = 0;
    for (i = 1; i < n; i++) {
        if (expr[i] == expr[0])
            count++;
        if (expr[i] == closing) {
            if (count == 0)
                break;
            count--;
        }
    }

    // If we did not find a closing
    // bracket
    if (i == n)
        return false;

    // If closing bracket was next
    // to open
    if (i == 1)
        return check(expr + 2, n - 2);

    // If closing bracket was somewhere
    // in middle.
    return check(expr + 1, i - 1) && check(expr + i + 1, n - i - 1);
}

// Driver program to test above function
int main()
{
    char expr[] = "[(])";
    int n = strlen(expr);
    if (check(expr, n))
        cout << "Balanced";
    else
        cout << "Not Balanced";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if parenthesis are
// balanced or not in an expression.
import java.util.Arrays;

class GFG {

    static char findClosing(char c)
    {
        if (c == '(')
            return ')';
        if (c == '{')
            return '}';
        if (c == '[')
            return ']';
        return Character.MIN_VALUE;
    }

    // function to check if parenthesis are
    // balanced.
    static boolean check(char expr[], int n)
    {
        // Base cases
        if (n == 0)
            return true;
        if (n == 1)
            return false;
        if (expr[0] == ')' || expr[0] == '}' || expr[0] == ']')
            return false;

        // Search for closing bracket for first
        // opening bracket.
        char closing = findClosing(expr[0]);

        // count is used to handle cases like
        // "((()))". We basically need to
        // consider matching closing bracket.
        int i, count = 0;
        for (i = 1; i < n; i++) {
            if (expr[i] == expr[0])
                count++;
            if (expr[i] == closing) {
                if (count == 0)
                    break;
                count--;
            }
        }

        // If we did not find a closing
        // bracket
        if (i == n)
            return false;

        // If closing bracket was next
        // to open
        if (i == 1)
            return check(Arrays.copyOfRange(expr, i + 1, n), n - 2);
        // If closing bracket was somewhere
        // in middle.
        return check(Arrays.copyOfRange(expr, 1, n), i - 1) && check(Arrays.copyOfRange(expr, (i + 1), n), n - i - 1);
    }

    // Driver code
    public static void main(String[] args)
    {
        char expr[] = "[(])".toCharArray();
        int n = expr.length;
        if (check(expr, n))
            System.out.println("Balanced");
        else
            System.out.println("Not Balanced");
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to check if parenthesis are
# balanced or not in an expression.
def findClosing(c):
    if c == '(':
        return ')'
    elif c == '{':
        return '}'
    elif c == '[':
        return ']'
    return -1

# function to check if parenthesis
# are balanced.
def check(expr, n):

    # Base cases
    if n == 0:
        return True
    if n == 1:
        return False
    if expr[0] == ')' or \
       expr[0] == '}' or expr[0] == ']':
        return False

    # Search for closing bracket for first
    # opening bracket.
    closing = findClosing(expr[0])

    # count is used to handle cases like
    # "((()))". We basically need to
    # consider matching closing bracket.
    i = -1
    count = 0
    for i in range(1, n):
        if expr[i] == expr[0]:
            count += 1
        if expr[i] == closing:
            if count == 0:
                break
            count -= 1

    # If we did not find a closing
    # bracket
    if i == n:
        return False

    # If closing bracket was next
    # to open
    if i == 1:
        return check(expr[2:], n - 2)

    # If closing bracket was somewhere
    # in middle.
    return check(expr[1:], i - 1) and \
           check(expr[i + 1:], n - i - 1)

# Driver Code
if __name__ == "__main__":
    expr = "[(])"
    n = len(expr)

    if check(expr, n):
        print("Balanced")
    else:
        print("Not Balanced")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to check
// if parenthesis are
// balanced or not in
// an expression.
using System;
class GFG{

static char[] copyOfRange (char[] src,
                           int start,
                           int end)
{
  int len = end - start;
  char[] dest = new char[len];
  Array.Copy(src, start,
             dest, 0, len);
  return dest;
}

static char findClosing(char c)
{
  if (c == '(')
    return ')';
  if (c == '{')
    return '}';
  if (c == '[')
    return ']';
  return char.MinValue;
}

// Function to check if
// parenthesis are balanced.
static bool check(char []expr,
                  int n)
{
  // Base cases
  if (n == 0)
    return true;
  if (n == 1)
    return false;
  if (expr[0] == ')' ||
      expr[0] == '}' ||
      expr[0] == ']')
    return false;

  // Search for closing bracket for first
  // opening bracket.
  char closing = findClosing(expr[0]);

  // count is used to handle cases like
  // "((()))". We basically need to
  // consider matching closing bracket.
  int i, count = 0;
  for (i = 1; i < n; i++)
  {
    if (expr[i] == expr[0])
      count++;
    if (expr[i] == closing)
    {
      if (count == 0)
        break;
      count--;
    }
  }

  // If we did not find
  // a closing bracket
  if (i == n)
    return false;

  // If closing bracket
  // was next to open
  if (i == 1)
    return check(copyOfRange(expr,
                             i + 1, n),
                              n - 2);
  // If closing bracket
  // was somewhere in middle.
  return check(copyOfRange(expr, 1, n),
                           i - 1) &&
         check(copyOfRange(expr, (i + 1),
                           n), n - i - 1);
}

// Driver code
public static void Main(String[] args)
{
  char []expr = "[(])".ToCharArray();
  int n = expr.Length;
  if (check(expr, n))
    Console.WriteLine("Balanced");
  else
    Console.WriteLine("Not Balanced");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to check if parenthesis are
// balanced or not in an expression.

function findClosing(c)
{
    if (c == '(')
        return ')';
    if (c == '{')
        return '}';
    if (c == '[')
        return ']';
    return -1;
}

// function to check if parenthesis are
// balanced.
function check(expr, n)
{
    // Base cases
    if (n == 0)
        return true;
    if (n == 1)
        return false;
    if (expr[0] == ')' || expr[0] == '}' || expr[0] == ']')
        return false;

    // Search for closing bracket for first
    // opening bracket.
    var closing = findClosing(expr[0]);

    // count is used to handle cases like
    // "((()))".  We basically need to
    // consider matching closing bracket.
    var i, count = 0;
    for (i = 1; i < n; i++) {
        if (expr[i] == expr[0])
            count++;
        if (expr[i] == closing) {
            if (count == 0)
                break;
            count--;
        }
    }

    // If we did not find a closing
    // bracket
    if (i == n)
        return false;

    // If closing bracket was next
    // to open
    if (i == 1)
        return check(expr + 2, n - 2);

    // If closing bracket was somewhere
    // in middle.
    return check(expr + 1, i - 1) && check(expr + i + 1, n - i - 1);
}

// Driver program to test above function
var expr = "[(])";
var n = expr.length;
if (check(expr, n))
    document.write( "Balanced");
else
    document.write( "Not Balanced");

// This code is contributed by itsok.
</script>
```

**Output:** 

```
Not Balanced
```

与基于堆栈的解决方案相比，上述解决方案效率非常低。这似乎只对递归练习问题有用。
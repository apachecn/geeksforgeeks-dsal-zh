# 检查两个带括号的表达式是否相同

> 原文:[https://www . geesforgeks . org/check-two-expressions-方括号/](https://www.geeksforgeeks.org/check-two-expressions-brackets/)

给定两个字符串形式的表达式。任务是比较它们并检查它们是否相似。表达式由小写字母、“+”、“-”和“()”组成。
示例:

```
Input  : exp1 = "-(a+b+c)"
         exp2 = "-a-b-c"
Output : Yes

Input  : exp1 = "-(c+b+a)"
         exp2 = "-c-b-a"
Output : Yes

Input  : exp1 = "a-b-(c-d)"
         exp2 = "a-b-c-d"
Output : No
```

可以假设从“a”到“z”最多有 26 个操作数，每个操作数只出现一次。

背后的一个简单想法是通过表达式记录*全局和局部符号(+/)*。这里的全局符号是指每个操作数的乘法符号。操作数的合成符号是本地符号乘以该操作数的全局符号。
例如，表达式 a+b-(c-d)计算为(+)+a(+)+b(-)+c(-)-d =>a+b–c+d。全局符号(括号内表示)乘以每个操作数的局部符号。
在给定的解决方案中，stack 用于保存全局标志的记录。计数向量记录操作数的计数(这里是小写拉丁字母)。以相反的方式评估两个表达式，最后，检查计数向量中的所有条目是否为零。

## C++

```
// CPP program to check if two expressions
// evaluate to same.
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// Return local sign of the operand. For example,
// in the expr a-b-(c), local signs of the operands
// are +a, -b, +c
bool adjSign(string s, int i)
{
    if (i == 0)
        return true;
    if (s[i - 1] == '-')
        return false;
    return true;
};

// Evaluate expressions into the count vector of
// the 26 alphabets.If add is true, then add count
// to the count vector of the alphabets, else remove
// count from the count vector.
void eval(string s, vector<int>& v, bool add)
{
    // stack stores the global sign
    // for operands.
    stack<bool> stk;
    stk.push(true);

    // + means true
    // global sign is positive initially

    int i = 0;
    while (s[i] != '\0') {
        if (s[i] == '+' || s[i] == '-') {
            i++;
            continue;
        }
        if (s[i] == '(') {

            // global sign for the bracket is
            // pushed to the stack
            if (adjSign(s, i))
                stk.push(stk.top());
            else
                stk.push(!stk.top());
        }

        // global sign is popped out which
        // was pushed in for the last bracket
        else if (s[i] == ')')
            stk.pop();

        else {

            // global sign is positive (we use different
            // values in two calls of functions so that
            // we finally check if all vector elements
            // are 0.
            if (stk.top())                
                v[s[i] - 'a'] += (adjSign(s, i) ? add ? 1 : -1 :
                                                  add ? -1 : 1);

            // global sign is negative here
            else                
                v[s[i] - 'a'] += (adjSign(s, i) ? add ? -1 : 1 :
                                                  add ? 1 : -1);
        }
        i++;
    }
};

// Returns true if expr1 and expr2 represent
// same expressions
bool areSame(string expr1, string expr2)
{
    // Create a vector for all operands and
    // initialize the vector as 0.
    vector<int> v(MAX_CHAR, 0);

    // Put signs of all operands in expr1
    eval(expr1, v, true);

    // Subtract signs of operands in expr2
    eval(expr2, v, false);

    // If expressions are same, vector must
    // be 0.
    for (int i = 0; i < MAX_CHAR; i++)
        if (v[i] != 0)
            return false;

    return true;
}

// Driver code
int main()
{
    string expr1 = "-(a+b+c)", expr2 = "-a-b-c";
    if (areSame(expr1, expr2))
        cout << "Yes\n";
    else
        cout << "No\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two expressions
// evaluate to same.
import java.io.*;
import java.util.*;

class GFG
{

    static final int MAX_CHAR = 26;

    // Return local sign of the operand. For example,
    // in the expr a-b-(c), local signs of the operands
    // are +a, -b, +c
    static boolean adjSign(String s, int i)
    {
        if (i == 0)
            return true;
        if (s.charAt(i - 1) == '-')
            return false;
        return true;
    };

    // Evaluate expressions into the count vector of
    // the 26 alphabets.If add is true, then add count
    // to the count vector of the alphabets, else remove
    // count from the count vector.
    static void eval(String s, int[] v, boolean add)
    {

        // stack stores the global sign
        // for operands.
        Stack<Boolean> stk = new Stack<>();
        stk.push(true);

        // + means true
        // global sign is positive initially

        int i = 0;
        while (i < s.length())
        {
            if (s.charAt(i) == '+' || s.charAt(i) == '-')
            {
                i++;
                continue;
            }
            if (s.charAt(i) == '(')
            {

                // global sign for the bracket is
                // pushed to the stack
                if (adjSign(s, i))
                    stk.push(stk.peek());
                else
                    stk.push(!stk.peek());
            }

            // global sign is popped out which
            // was pushed in for the last bracket
            else if (s.charAt(i) == ')')
                stk.pop();

            else
            {

                // global sign is positive (we use different
                // values in two calls of functions so that
                // we finally check if all vector elements
                // are 0.
                if (stk.peek())
                    v[s.charAt(i) - 'a'] += (adjSign(s, i) ?
                               add ? 1 : -1 : add ? -1 : 1);

                // global sign is negative here
                else
                    v[s.charAt(i) - 'a'] += (adjSign(s, i) ?
                                add ? -1 : 1 : add ? 1 : -1);
            }
            i++;
        }
    };

    // Returns true if expr1 and expr2 represent
    // same expressions
    static boolean areSame(String expr1, String expr2)
    {

        // Create a vector for all operands and
        // initialize the vector as 0.
        int[] v = new int[MAX_CHAR];

        // Put signs of all operands in expr1
        eval(expr1, v, true);

        // Subtract signs of operands in expr2
        eval(expr2, v, false);

        // If expressions are same, vector must
        // be 0.
        for (int i = 0; i < MAX_CHAR; i++)
            if (v[i] != 0)
                return false;

        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {

        String expr1 = "-(a+b+c)", expr2 = "-a-b-c";
        if (areSame(expr1, expr2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to check if two expressions
# evaluate to same.
MAX_CHAR = 26;

# Return local sign of the operand. For example,
# in the expr a-b-(c), local signs of the operands
# are +a, -b, +c
def adjSign(s, i):
  if (i == 0):
    return True;
  if (s[i - 1] == '-'):
    return False;
  return True;

# Evaluate expressions into the count vector of
# the 26 alphabets.If add is True, then add count
# to the count vector of the alphabets, else remove
# count from the count vector.
def eval(s, v, add):

  # stack stores the global sign
  # for operands.
  stk = []
  stk.append(True);

  # + means True
  # global sign is positive initially
  i = 0;

  while (i < len(s)):

    if (s[i] == '+' or s[i] == '-'):
      i += 1
      continue;

    if (s[i] == '('):

      # global sign for the bracket is
      # pushed to the stack
      if (adjSign(s, i)):
        stk.append(stk[-1]);
      else:
        stk.append(not stk[-1]);

    # global sign is popped out which
    # was pushed in for the last bracket
    elif (s[i] == ')'):
      stk.pop();
    else:

      # global sign is positive (we use different
      # values in two calls of functions so that
      # we finally check if all vector elements
      # are 0.
      if (stk[-1]):
        v[ord(s[i]) - ord('a')] += (1 if add else -1) if adjSign(s, i) else (-1 if add else 1)

      # global sign is negative here
      else:
        v[ord(s[i]) - ord('a')] += (-1 if add else 1) if adjSign(s, i) else (1 if add else -1)

    i += 1

# Returns True if expr1 and expr2 represent
# same expressions
def areSame(expr1, expr2):

  # Create a vector for all operands and
  # initialize the vector as 0.
  v = [0 for i in range(MAX_CHAR)];

  # Put signs of all operands in expr1
  eval(expr1, v, True);

  # Subtract signs of operands in expr2
  eval(expr2, v, False);

  # If expressions are same, vector must
  # be 0.
  for i in range(MAX_CHAR):
    if (v[i] != 0):
      return False;
  return True;

# Driver Code
if __name__=='__main__':
  expr1 = "-(a+b+c)"
  expr2 = "-a-b-c";
  if (areSame(expr1, expr2)):
    print("Yes");
  else:
    print("No");

    # This code is contributed by rutvik_56.
```

## C#

```
// C# program to check if two expressions
// evaluate to same.
using System;
using System.Collections.Generic;
public class GFG
{

  static readonly int MAX_CHAR = 26;

  // Return local sign of the operand. For example,
  // in the expr a-b-(c), local signs of the operands
  // are +a, -b, +c
  static bool adjSign(String s, int i)
  {
    if (i == 0)
      return true;
    if (s[i-1] == '-')
      return false;
    return true;
  }

  // Evaluate expressions into the count vector of
  // the 26 alphabets.If add is true, then add count
  // to the count vector of the alphabets, else remove
  // count from the count vector.
  static void eval(String s, int[] v, bool add)
  {

    // stack stores the global sign
    // for operands.
    Stack<Boolean> stk = new Stack<Boolean>();
    stk.Push(true);

    // + means true
    // global sign is positive initially
    int i = 0;
    while (i < s.Length)
    {
      if (s[i] == '+' || s[i] == '-')
      {
        i++;
        continue;
      }
      if (s[i] == '(')
      {

        // global sign for the bracket is
        // pushed to the stack
        if (adjSign(s, i))
          stk.Push(stk.Peek());
        else
          stk.Push(!stk.Peek());
      }

      // global sign is popped out which
      // was pushed in for the last bracket
      else if (s[i] == ')')
        stk.Pop();

      else
      {

        // global sign is positive (we use different
        // values in two calls of functions so that
        // we finally check if all vector elements
        // are 0.
        if (stk.Peek())
          v[s[i] - 'a'] += (adjSign(s, i) ?
                            add ? 1 : -1 : add ? -1 : 1);

        // global sign is negative here
        else
          v[s[i] - 'a'] += (adjSign(s, i) ?
                            add ? -1 : 1 : add ? 1 : -1);
      }
      i++;
    }
  }

  // Returns true if expr1 and expr2 represent
  // same expressions
  static bool areSame(String expr1, String expr2)
  {

    // Create a vector for all operands and
    // initialize the vector as 0.
    int[] v = new int[MAX_CHAR];

    // Put signs of all operands in expr1
    eval(expr1, v, true);

    // Subtract signs of operands in expr2
    eval(expr2, v, false);

    // If expressions are same, vector must
    // be 0.
    for (int i = 0; i < MAX_CHAR; i++)
      if (v[i] != 0)
        return false;

    return true;
  }

  // Driver Code
  public static void Main(String[] args)
  {

    String expr1 = "-(a+b+c)", expr2 = "-a-b-c";
    if (areSame(expr1, expr2))
      Console.WriteLine("Yes");
    else
      Console.WriteLine("No");
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to check if two expressions
    // evaluate to same.

    let MAX_CHAR = 26;

    // Return local sign of the operand. For example,
    // in the expr a-b-(c), local signs of the operands
    // are +a, -b, +c
    function adjSign(s, i)
    {
        if (i == 0)
            return true;
        if (s[i - 1] == '-')
            return false;
        return true;
    }

    // Evaluate expressions into the count vector of
    // the 26 alphabets.If add is true, then add count
    // to the count vector of the alphabets, else remove
    // count from the count vector.
    function eval(s, v, add)
    {

        // stack stores the global sign
        // for operands.
        let stk = [];
        stk.push(true);

        // + means true
        // global sign is positive initially

        let i = 0;
        while (i < s.length)
        {
            if (s[i] == '+' || s[i] == '-')
            {
                i++;
                continue;
            }
            if (s[i] == '(')
            {

                // global sign for the bracket is
                // pushed to the stack
                if (adjSign(s, i))
                    stk.push(stk[stk.length - 1]);
                else
                    stk.push(!stk[stk.length - 1]);
            }

            // global sign is popped out which
            // was pushed in for the last bracket
            else if (s[i] == ')')
                stk.pop();

            else
            {

                // global sign is positive (we use different
                // values in two calls of functions so that
                // we finally check if all vector elements
                // are 0.
                if (stk[stk.length - 1])
                    v[s[i] - 'a'] += (adjSign(s, i) ?
                               add ? 1 : -1 : add ? -1 : 1);

                // global sign is negative here
                else
                    v[s[i] - 'a'] += (adjSign(s, i) ?
                                add ? -1 : 1 : add ? 1 : -1);
            }
            i++;
        }
    };

    // Returns true if expr1 and expr2 represent
    // same expressions
    function areSame(expr1, expr2)
    {

        // Create a vector for all operands and
        // initialize the vector as 0.
        let v = new Array(MAX_CHAR);
        v.fill(0);

        // Put signs of all operands in expr1
        eval(expr1, v, true);

        // Subtract signs of operands in expr2
        eval(expr2, v, false);

        // If expressions are same, vector must
        // be 0.
        for (let i = 0; i < MAX_CHAR; i++)
            if (v[i] != 0)
                return false;

        return true;
    }

    let expr1 = "-(a+b+c)", expr2 = "-a-b-c";
    if (areSame(expr1, expr2))
      document.write("YES");
    else
      document.write("NO");

    // This code is contributed by suresh07.
</script>
```

**输出:**

```
YES
```

本文由 [**Amol Mejari**](https://auth.geeksforgeeks.org/profile.php?user=Amol Mejari) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
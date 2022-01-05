# 根据给定的字符串计算括号的分数

> 原文:[https://www . geeksforgeeks . org/从给定字符串计算括号分数/](https://www.geeksforgeeks.org/calculate-score-of-parentheses-from-a-given-string/)

给定长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，由成对的平衡括号组成，任务是根据给定的规则计算给定字符串的分数:

*   **“()”**得分 **1** 。
*   **“a b”**的得分为 **a + b** ，其中 **a** 和 **b** 是单独的一对平衡括号。
*   **“(a)**的得分是 **a** 的两倍，即得分是**2 * a**的得分。

**示例:**

> **输入:**str =())”
> **输出:** 2
> **说明:**字符串为“ab”形式，即总分=(a 分)+(b 分)= 1 + 1 = 2。
> 
> **输入:**str =(()(())))”
> **输出:** 6
> **解释:**字符串的形式为“(a(b))”，这样总得分= 2 *(a 的得分)+2 *(b 的得分))= 2*(1 + 2*(1)) = 6。

[**基于树的**](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/) **方法:**关于基于树的方法，请参考本文[之前的帖子](https://www.geeksforgeeks.org/score-of-parentheses-using-tree/)。
***时间复杂度:** O(N)*
***辅助空间:** O(N)*

[**堆叠**](https://www.geeksforgeeks.org/stack-data-structure/) **【基于】的方法:**思路是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，在遍历字符串的同时，如果遇到括号 **')'** ，则计算这一对括号的得分。按照以下步骤解决问题:

*   初始化一个堆栈，说 **S** ，记录分数，最初[将 **0** 推入堆栈](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)。
*   使用变量 **i** 遍历字符串 **字符串**，并执行以下步骤:
    *   如果 **str[i]** 的值等于**(“**)，则将 **0** 推到堆栈 **S** 。
    *   否则，请执行以下步骤:
        *   将栈顶**S**存储在一个变量中，说 **temp** ，[从栈顶](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)[弹出元素](https://www.geeksforgeeks.org/stack-top-c-stl/)。
        *   如果**温度**的值为**非零**，则内括号存在。将 **2 *温度**添加到堆栈的[顶部。否则，将 **1** 添加到堆栈](https://www.geeksforgeeks.org/stack-top-c-stl/)的[顶部。](https://www.geeksforgeeks.org/stack-top-c-stl/)
*   完成上述步骤后，打印堆栈顶部的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the score
// of the parentheses using stack
void scoreOfParentheses(string s)
{
    // To keep track of the score
    stack<int> stack;

    // Initially, push 0 to stack
    stack.push(0);

    // Traverse the string s
    for (char c : s) {

        // If '(' is encountered,
        // then push 0 to stack
        if (c == '(')
            stack.push(0);

        // Otherwise
        else {

            // Balance the last '(', and store
            // the score of inner parentheses
            int tmp = stack.top();
            stack.pop();

            int val = 0;

            // If tmp is not zero, it means
            // inner parentheses exists
            if (tmp > 0)
                val = tmp * 2;

            // Otherwise, it means no
            // inner parentheses exists
            else
                val = 1;

            // Pass the score of this level
            // to parent parentheses
            stack.top() += val;
        }
    }

    // Print the score
    cout << stack.top();
}

// Driver Code
int main()
{
    string S = "(()(()))";
    scoreOfParentheses(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to calculate the score
  // of the parentheses using stack
  static void scoreOfParentheses(String s)
  {

    // To keep track of the score
    Stack<Integer> stack = new Stack<>();

    // Initially, push 0 to stack
    stack.push(0);

    // Traverse the string s
    for (char c : s.toCharArray()) {

      // If '(' is encountered,
      // then push 0 to stack
      if (c == '(')
        stack.push(0);

      // Otherwise
      else {

        // Balance the last '(', and store
        // the score of inner parentheses
        int tmp = stack.pop();

        int val = 0;

        // If tmp is not zero, it means
        // inner parentheses exists
        if (tmp > 0)
          val = tmp * 2;

        // Otherwise, it means no
        // inner parentheses exists
        else
          val = 1;

        // Pass the score of this level
        // to parent parentheses
        stack.push(stack.pop() + val);
      }
    }

    // Print the score
    System.out.println(stack.peek());
  }

  // Driver code
  public static void main(String[] args)
  {

    String S = "(()(()))";

    // Function call
    scoreOfParentheses(S);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to calculate the score
# of the parentheses using stack
def scoreOfParentheses(s):

    # To keep track of the score
    stack = []

    # Initially, push 0 to stack
    stack.append(0)

    # Traverse the string s
    for c in s:

        # If '(' is encountered,
        # then push 0 to stack
        if (c == '('):
            stack.append(0)

        # Otherwise
        else:

            # Balance the last '(', and store
            # the score of inner parentheses
            tmp = stack[len(stack) - 1]
            stack = stack[:-1]

            val = 0

            # If tmp is not zero, it means
            # inner parentheses exists
            if (tmp > 0):
                val = tmp * 2

            # Otherwise, it means no
            # inner parentheses exists
            else:
                val = 1

            # Pass the score of this level
            # to parent parentheses
            stack[len(stack) - 1] += val

    # Print the score
    print(stack[len(stack) - 1])

# Driver Code
if __name__ == '__main__':
    S = "(()(()))"
    scoreOfParentheses(S)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

  // Function to calculate the score
  // of the parentheses using stack
  static void scoreOfParentheses(String s)
  {

    // To keep track of the score
    Stack<int> stack = new Stack<int>();

    // Initially, push 0 to stack
    stack.Push(0);

    // Traverse the string s
    foreach (char c in s.ToCharArray()) {

      // If '(' is encountered,
      // then push 0 to stack
      if (c == '(')
        stack.Push(0);

      // Otherwise
      else {

        // Balance the last '(', and store
        // the score of inner parentheses
        int tmp = stack.Pop();

        int val = 0;

        // If tmp is not zero, it means
        // inner parentheses exists
        if (tmp > 0)
          val = tmp * 2;

        // Otherwise, it means no
        // inner parentheses exists
        else
          val = 1;

        // Pass the score of this level
        // to parent parentheses
        stack.Push(stack.Pop() + val);
      }
    }

    // Print the score
    Console.WriteLine(stack.Peek());
  }

  // Driver code
  public static void Main(String[] args)
  {

    String S = "(()(()))";

    // Function call
    scoreOfParentheses(S);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate the score
// of the parentheses using stack
function scoreOfParentheses(s)
{
    // To keep track of the score
    var stack = [];

    // Initially, push 0 to stack
    stack.push(0);

    // Traverse the string s
    s.split('').forEach(c => {

        // If '(' is encountered,
        // then push 0 to stack
        if (c == '(')
            stack.push(0);

        // Otherwise
        else {

            // Balance the last '(', and store
            // the score of inner parentheses
            var tmp = stack[stack.length-1];
            stack.pop();

            var val = 0;

            // If tmp is not zero, it means
            // inner parentheses exists
            if (tmp > 0)
                val = tmp * 2;

            // Otherwise, it means no
            // inner parentheses exists
            else
                val = 1;

            // Pass the score of this level
            // to parent parentheses
            stack[stack.length-1] += val;
        }
    });

    // Print the score
    document.write( stack[stack.length-1]);
}

// Driver Code
var S = "(()(()))";
scoreOfParentheses(S);

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
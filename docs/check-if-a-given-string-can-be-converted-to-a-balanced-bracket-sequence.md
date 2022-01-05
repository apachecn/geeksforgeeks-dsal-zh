# 检查给定的字符串是否可以转换为平衡括号序列

> 原文:[https://www . geesforgeks . org/check-if-a-给定字符串-可转换为平衡括号-sequence/](https://www.geeksforgeeks.org/check-if-a-given-string-can-be-converted-to-a-balanced-bracket-sequence/)

给定大小为 **N** 的[弦](https://www.geeksforgeeks.org/string-data-structure/)T2 S，由**(**、**)**和**{ content }组成；**，任务是通过用 **)** 或 **(** 替换每次出现的 **$** 来检查给定字符串是否可以转换为**平衡括号序列**。

> A **平衡括号序列**是每个开括号**(**有对应的闭括号**)**的序列。

**示例:**

> ***输入:***S =()({ content } # x201；
> ***输出:*** 是
> ***说明:*** 将字符串转换成平衡的括号序列:()()。
> 
> ***输入:***S = $($)$(“
> ***输出:*** 否
> ***说明:*** 可能的替换为”(((((()、“())()”、“()()”()”、“))()()()())())(")，没有一个是平衡的。因此，不能获得平衡的括号序列。

**方法:**使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)可以解决上述问题。想法是检查所有 **)** 是否可以与 **(** 或 **$** 平衡，反之亦然。按照以下步骤解决此问题:

*   [存储**(**、**)**、**“{ content }”的频率**](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)；分别出现在**计数打开**、**计数关闭**和**计数符号**等变量中。
*   将变量**和**初始化为 **1** 以存储所需结果，并初始化一个堆栈 **stack_1** 以检查所有**“**是否可以与**”(“**或 **$** 平衡。
*   使用变量 **i** 遍历字符串 **S** ，并执行以下操作:
    *   如果当前字符 **S[i]** 为**”**，如果 **stack_1** 为空，则将 **ans** 设置为 **0** ，否则[从 **stack_1**](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/) 弹出字符。
    *   Else [将人物**S【I】**推至 **stack_1**](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/) 。
*   [倒扣](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/) **S** ，按照同样的程序检查所有**(**是否能与**)**或**“{ content }”平衡；**。
*   如果 **countSymbol** 的值小于 **countOpen** 和 **countClosed** 的绝对差值，则将 **ans** 设置为 **0** 。否则用符号平衡多余的括号。平衡[后，如果**计数符号**为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则将 **ans** 设置为 **0** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the string
// can be balanced by replacing the
// '{content}apos; with opening or closing brackets
bool canBeBalanced(string sequence)
{
    // If string can never be balanced
    if (sequence.size() % 2)
        return false;

    // Declare 2 stacks to check if all
    // ) can be balanced with ( or $
    // and vice-versa
    stack<char> stack_, stack2_;

    // Store the count the occurence
    // of (, ) and $
    int countOpen = 0, countClosed = 0;
    int countSymbol = 0;

    // Traverse the string
    for (int i = 0;
         i < sequence.size(); i++) {

        if (sequence[i] == ')') {

            // Increment closed bracket
            // count by 1
            countClosed++;

            // If there are no opening
            // bracket to match it
            // then return false
            if (stack_.empty()) {
                return false;
            }

            // Otherwise, pop the character
            // from the stack
            else {
                stack_.pop();
            }
        }

        else {

            // If current character is
            // an opening bracket or $,
            // push it to the stack
            if (sequence[i] == '{content}apos;) {

                // Increment symbol
                // count by 1
                countSymbol++;
            }
            else {

                // Increment open
                // bracket count by 1
                countOpen++;
            }
            stack_.push(sequence[i]);
        }
    }

    // Traverse the string from end
    // and repeat the same process
    for (int i = sequence.size() - 1;
         i >= 0; i--) {

        if (sequence[i] == '(') {

            // If there are no closing
            // brackets to match it
            if (stack2_.empty()) {
                return false;
            }

            // Otherwise, pop character
            // from stack
            else {
                stack2_.pop();
            }
        }
        else {
            stack2_.push(sequence[i]);
        }
    }

    // Store the extra ( or ) which
    // are not balanced yet
    int extra = abs(countClosed - countOpen);

    // Check if $ is available to
    // balance the extra brackets
    if (countSymbol < extra) {
        return false;
    }

    else {

        // Count ramaining $ after
        // balancing extra ( and )
        countSymbol -= extra;

        // Check if each pair of $
        // is convertable in ()
        if (countSymbol % 2 == 0) {
            return true;
        }
    }
    return false;
}

// Driver Code
int main()
{
    string S = "()({content}quot;;

    // Function Call
    if (canBeBalanced(S)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to check if the String
// can be balanced by replacing the
// '{content}apos; with opening or closing brackets
static boolean canBeBalanced(String sequence)
{

    // If String can never be balanced
    if (sequence.length() % 2 == 1)
        return false;

    // Declare 2 stacks to check if all
    // ) can be balanced with ( or $
    // and vice-versa
    Stack<Character> stack_ = new Stack<Character>();
    Stack<Character> stack2_ = new Stack<Character>();

    // Store the count the occurence
    // of (, ) and $
    int countOpen = 0, countClosed = 0;
    int countSymbol = 0;

    // Traverse the String
    for (int i = 0;
         i < sequence.length(); i++)
    {

        if (sequence.charAt(i) == ')')
        {

            // Increment closed bracket
            // count by 1
            countClosed++;

            // If there are no opening
            // bracket to match it
            // then return false
            if (stack_.isEmpty())
            {
                return false;
            }

            // Otherwise, pop the character
            // from the stack
            else
            {
                stack_.pop();
            }
        }

        else
        {

            // If current character is
            // an opening bracket or $,
            // push it to the stack
            if (sequence.charAt(i) == '{content}apos;)
            {

                // Increment symbol
                // count by 1
                countSymbol++;
            }
            else
            {

                // Increment open
                // bracket count by 1
                countOpen++;
            }
            stack_.add(sequence.charAt(i));
        }
    }

    // Traverse the String from end
    // and repeat the same process
    for (int i = sequence.length() - 1;
         i >= 0; i--)
    {

        if (sequence.charAt(i) == '(')
        {

            // If there are no closing
            // brackets to match it
            if (stack2_.isEmpty())
            {
                return false;
            }

            // Otherwise, pop character
            // from stack
            else
            {
                stack2_.pop();
            }
        }
        else
        {
            stack2_.add(sequence.charAt(i));
        }
    }

    // Store the extra ( or ) which
    // are not balanced yet
    int extra = Math.abs(countClosed - countOpen);

    // Check if $ is available to
    // balance the extra brackets
    if (countSymbol < extra)
    {
        return false;
    }

    else
    {

        // Count ramaining $ after
        // balancing extra ( and )
        countSymbol -= extra;

        // Check if each pair of $
        // is convertable in ()
        if (countSymbol % 2 == 0)
        {
            return true;
        }
    }
    return false;
}

// Driver Code
public static void main(String[] args)
{
    String S = "()({content}quot;;

    // Function Call
    if (canBeBalanced(S))
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the
# can be balanced by replacing the
# '{content}apos; with opening or closing brackets
def canBeBalanced(sequence):

    # If string can never be balanced
    if (len(sequence) % 2):
        return False

    # Declare 2 stacks to check if all
    # ) can be balanced with ( or $
    # and vice-versa
    stack_, stack2_ = [], []

    # Store the count the occurence
    # of (, ) and $
    countOpen ,countClosed = 0, 0
    countSymbol = 0

    # Traverse the string
    for i in range(len(sequence)):
        if (sequence[i] == ')'):

            # Increment closed bracket
            # count by 1
            countClosed += 1

            # If there are no opening
            # bracket to match it
            # then return False
            if (len(stack_) == 0):
                return False

            # Otherwise, pop the character
            # from the stack
            else:
                del stack_[-1]
        else:

            # If current character is
            # an opening bracket or $,
            # push it to the stack
            if (sequence[i] == '{content}apos;):

                # Increment symbol
                # count by 1
                countSymbol += 1
            else:

                # Increment open
                # bracket count by 1
                countOpen += 1
            stack_.append(sequence[i])

    # Traverse the string from end
    # and repeat the same process
    for i in range(len(sequence)-1, -1, -1):
        if (sequence[i] == '('):

            # If there are no closing
            # brackets to match it
            if (len(stack2_) == 0):
                return False

            # Otherwise, pop character
            # from stack
            else:
                del stack2_[-1]
        else :
            stack2_.append(sequence[i])

    # Store the extra ( or ) which
    # are not balanced yet
    extra = abs(countClosed - countOpen)

    # Check if $ is available to
    # balance the extra brackets
    if (countSymbol < extra):
        return False
    else :

        # Count ramaining $ after
        # balancing extra ( and )
        countSymbol -= extra

        # Check if each pair of $
        # is convertable in ()
        if (countSymbol % 2 == 0) :
            return True
    return False

# Driver Code
if __name__ == '__main__':
    S = "()({content}quot;

    # Function Call
    if (canBeBalanced(S)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to check if the String
  // can be balanced by replacing the
  // '{content}apos; with opening or closing brackets
  static bool canBeBalanced(String sequence)
  {

    // If String can never be balanced
    if (sequence.Length % 2 == 1)
      return false;

    // Declare 2 stacks to check if all
    // ) can be balanced with ( or $
    // and vice-versa
    Stack<char> stack_ = new Stack<char>();
    Stack<char> stack2_ = new Stack<char>();

    // Store the count the occurence
    // of (, ) and $
    int countOpen = 0, countClosed = 0;
    int countSymbol = 0;

    // Traverse the String
    for (int i = 0;
         i < sequence.Length; i++)
    {
      if (sequence[i] == ')')
      {

        // Increment closed bracket
        // count by 1
        countClosed++;

        // If there are no opening
        // bracket to match it
        // then return false
        if (stack_.Count==0)
        {
          return false;
        }

        // Otherwise, pop the character
        // from the stack
        else
        {
          stack_.Pop();
        }
      }

      else
      {

        // If current character is
        // an opening bracket or $,
        // push it to the stack
        if (sequence[i] == '{content}apos;)
        {

          // Increment symbol
          // count by 1
          countSymbol++;
        }
        else
        {

          // Increment open
          // bracket count by 1
          countOpen++;
        }
        stack_.Push(sequence[i]);
      }
    }

    // Traverse the String from end
    // and repeat the same process
    for (int i = sequence.Length - 1;
         i >= 0; i--)
    {

      if (sequence[i] == '(')
      {

        // If there are no closing
        // brackets to match it
        if (stack2_.Count == 0)
        {
          return false;
        }

        // Otherwise, pop character
        // from stack
        else
        {
          stack2_.Pop();
        }
      }
      else
      {
        stack2_.Push(sequence[i]);
      }
    }

    // Store the extra ( or ) which
    // are not balanced yet
    int extra = Math.Abs(countClosed - countOpen);

    // Check if $ is available to
    // balance the extra brackets
    if (countSymbol < extra)
    {
      return false;
    }

    else
    {

      // Count ramaining $ after
      // balancing extra ( and )
      countSymbol -= extra;

      // Check if each pair of $
      // is convertable in ()
      if (countSymbol % 2 == 0)
      {
        return true;
      }
    }
    return false;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    String S = "()({content}quot;;

    // Function Call
    if (canBeBalanced(S))
    {
      Console.Write("Yes");
    }
    else
    {
      Console.Write("No");
    }
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to check if the String
    // can be balanced by replacing the
    // '{content}apos; with opening or closing brackets
    function canBeBalanced(sequence)
    {
        // If String can never be balanced
        if (sequence.length % 2 == 1)
            return false;

        // Declare 2 stacks to check if all
        // ) can be balanced with ( or $
            // and vice-versa
        let stack_ = [];
        let stack2_ = [];

        // Store the count the occurence
        // of (, ) and $
        let countOpen = 0, countClosed = 0;
        let countSymbol = 0;

        // Traverse the String
        for (let i = 0;
             i < sequence.length; i++)
        {

            if (sequence[i] == ')')
                {

                // Increment closed bracket
                // count by 1
                countClosed++;

                // If there are no opening
                // bracket to match it
                // then return false
                if (stack_.length==0)
                {
                    return false;
                    }

                // Otherwise, pop the character
                // from the stack
                else
                {
                    stack_.pop();
                }
            }

            else
            {

                // If current character is
                // an opening bracket or $,
                // push it to the stack
                if (sequence[i] == '{content}apos;)
                {

                    // Increment symbol
                    // count by 1
                    countSymbol++;
                }
                else
                {

                    // Increment open
                    // bracket count by 1
                    countOpen++;
                }
                stack_.push(sequence[i]);
            }
        }

        // Traverse the String from end
        // and repeat the same process
        for (let i = sequence.length - 1;
             i >= 0; i--)
        {

            if (sequence[i] == '(')
            {

                // If there are no closing
                // brackets to match it
                if (stack2_.length==0)
                {
                    return false;
                }

                // Otherwise, pop character
                // from stack
                else
                {
                    stack2_.pop();
                }
            }
            else
            {
                stack2_.push(sequence[i]);
            }
            }

        // Store the extra ( or ) which
        // are not balanced yet
        let extra = Math.abs(countClosed - countOpen);

        // Check if $ is available to
        // balance the extra brackets
        if (countSymbol < extra)
        {
            return false;
        }

        else
        {

            // Count ramaining $ after
            // balancing extra ( and )
            countSymbol -= extra;

            // Check if each pair of $
            // is convertable in ()
            if (countSymbol % 2 == 0)
            {
                return true;
            }
        }
        return false;
      }

    // Driver Code

    let S = "()({content}quot;;
    // Function Call
    if (canBeBalanced(S))
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
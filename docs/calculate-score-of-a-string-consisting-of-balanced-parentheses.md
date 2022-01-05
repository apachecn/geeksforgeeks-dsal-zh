# 计算由平衡括号组成的字符串的分数

> 原文:[https://www . geesforgeks . org/compute-score-of-a-string-compound-of-balanced-括号/](https://www.geeksforgeeks.org/calculate-score-of-a-string-consisting-of-balanced-parentheses/)

给定一个由成对的平衡括号组成的[字符串**字符串**，任务是根据以下规则计算给定字符串的分数:](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)

1.  “ **()** ”得 1 分。
2.  “ **x y** ”的得分为 **x + y** ，其中 **x** 和 **y** 是单独的一对平衡括号。
3.  “ **(x)** ”有两次得分 **x** (即， **2 *得分 x** 。

**示例:**

> **输入:**str = "()"
> **输出:** 2
> **说明:**有两个平衡括号“()()”的单个 psirs。因此，得分=得分为“()”+得分为“()”= 1 + 1 = 2
> 
> **输入:**str =(())”
> **输出:** 2
> **说明:**由于输入为“(x)”形式，总分= 2 *得分为“()”= 2 * 1 = 2

**方法:**使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)可以解决问题。这个想法是[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符。对于每个 **i <sup>th</sup>** 字符，检查该字符是否为**(“**)。如果发现为真，则将该字符插入堆栈。否则，计算内括号的分数，并将分数的两倍插入堆栈。按照以下步骤解决问题:

*   初始化一个[栈](https://www.geeksforgeeks.org/stack-data-structure/)来存储当前遍历的字符或者内部平衡括号的分数。
*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)、**字符串**的字符。对于每个**I<sup>th</sup>T7】字符，检查以下条件:**
    *   如果当前字符是 **'('** )或者不是。如果发现为真，则[将当前角色推入堆栈](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)。
    *   否则，检查堆叠的[顶部元素是否为**(“**)。如果发现为真，则在代表内部平衡括号得分的堆栈中插入**“1”**。](https://www.geeksforgeeks.org/stack-top-c-stl/)
    *   否则，将堆栈的[顶部元素加倍，](https://www.geeksforgeeks.org/stack-top-c-stl/)[将获得的值推入堆栈](https://www.geeksforgeeks.org/stack-push-method-in-java/)。
*   最后，打印得到的总分。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
#include <stack>
using namespace std;

// Function to calculate
// score of parentheses
long long scoreOfParentheses(string S)
{

    stack<string> s;

    // Stores index of
    // character of string
    int i = 0;

    // Stores total scores
    // obtained from the string
    long long ans = 0;

    // Iterate over characters
    // of the string
    while (i < S.length()) {

        // If s[i] is '('
        if (S[i] == '(')
            s.push("(");
        else {

            // If top element of
            // stack is '('
            if (s.top() == "(") {
                s.pop();
                s.push("1");
            }
            else {

                // Stores score of
                // inner parentheses
                long long count = 0;

                // Calculate score of
                // inner parentheses
                while (s.top() != "(") {

                    // Update count
                    count += stoi(s.top());
                    s.pop();
                }

                // Pop from stack
                s.pop();

                // Insert score of
                // inner parentheses
                s.push(to_string(2 * count));
            }
        }

        // Update i
        i++;
    }

    // Calculate score
    // of the string
    while (!s.empty()) {

        // Update ans
        ans += stoi(s.top());
        s.pop();
    }
    return ans;
}

// Driver Code
int main()
{
    string S1 = "(()(()))";
    cout << scoreOfParentheses(S1) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to calculate
  // score of parentheses
  static long scoreOfParentheses(String S)
  {
    Stack<String> s = new Stack<>();

    // Stores index of
    // character of String
    int i = 0;

    // Stores total scores
    // obtained from the String
    long ans = 0;

    // Iterate over characters
    // of the String
    while (i < S.length())
    {

      // If s[i] is '('
      if (S.charAt(i) == '(')
        s.add("(");
      else
      {

        // If top element of
        // stack is '('
        if (s.peek() == "(")
        {
          s.pop();
          s.add("1");
        }
        else
        {

          // Stores score of
          // inner parentheses
          long count = 0;

          // Calculate score of
          // inner parentheses
          while (s.peek() != "(")
          {

            // Update count
            count += Integer.parseInt(s.peek());
            s.pop();
          }

          // Pop from stack
          s.pop();

          // Insert score of
          // inner parentheses
          s.add(String.valueOf(2 * count));
        }
      }

      // Update i
      i++;
    }

    // Calculate score
    // of the String
    while (!s.isEmpty())
    {

      // Update ans
      ans += Integer.parseInt(s.peek());
      s.pop();
    }
    return ans;
  }

  // Driver Code
  public static void main(String[] args)
  {
    String S1 = "(()(()))";
    System.out.print(scoreOfParentheses(S1) +"\n");
  }
}

// This code is contributed by 29AjayKumar.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate
# score of parentheses
def scoreOfParentheses(S):
    s = []

    # Stores index of
    # character of string
    i = 0

    # Stores total scores
    # obtained from the string
    ans = 0

    # Iterate over characters
    # of the string
    while (i < len(S)):

        # If s[i] is '('
        if (S[i] == '('):
            s.append("(")
        else:

            # If top element of
            # stack is '('
            if (s[-1] == "("):
                s.pop()
                s.append("1")
            else:

                # Stores score of
                # inner parentheses
                count = 0

                # Calculate score of
                # inner parentheses
                while (s[-1] != "("):

                    # Update count
                    count += int(s[-1])
                    s.pop()

                # Pop from stack
                s.pop()

                # Insert score of
                # inner parentheses
                s.append(str(2 * count))

        # Update i
        i += 1

    # Calculate score
    # of the string
    while len(s) > 0:

        # Update ans
        ans += int(s[-1])
        s.pop()
    return ans

# Driver Code
if __name__ == '__main__':
    S1 = "(()(()))"
    print(scoreOfParentheses(S1))

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to calculate
  // score of parentheses
  static long scoreOfParentheses(String S)
  {
    Stack<String> s = new Stack<String>();

    // Stores index of
    // character of String
    int i = 0;

    // Stores total scores
    // obtained from the String
    long ans = 0;

    // Iterate over characters
    // of the String
    while (i < S.Length)
    {

      // If s[i] is '('
      if (S[i] == '(')
        s.Push("(");
      else
      {

        // If top element of
        // stack is '('
        if (s.Peek() == "(")
        {
          s.Pop();
          s.Push("1");
        }
        else
        {

          // Stores score of
          // inner parentheses
          long count = 0;

          // Calculate score of
          // inner parentheses
          while (s.Peek() != "(")
          {

            // Update count
            count += Int32.Parse(s.Peek());
            s.Pop();
          }

          // Pop from stack
          s.Pop();

          // Insert score of
          // inner parentheses
          s.Push(String.Join("", 2 * count));
        }
      }

      // Update i
      i++;
    }

    // Calculate score
    // of the String
    while (s.Count != 0)
    {

      // Update ans
      ans += Int32.Parse(s.Peek());
      s.Pop();
    }
    return ans;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    String S1 = "(()(()))";
    Console.Write(scoreOfParentheses(S1) +"\n");
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to calculate
// score of parentheses
function scoreOfParentheses(S)
{

    var s = [];

    // Stores index of
    // character of string
    var i = 0;

    // Stores total scores
    // obtained from the string
    var ans = 0;

    // Iterate over characters
    // of the string
    while (i < S.length) {

        // If s[i] is '('
        if (S[i] == '(')
            s.push("(");
        else {

            // If top element of
            // stack is '('
            if (s[s.length-1] == "(") {
                s.pop();
                s.push("1");
            }
            else {

                // Stores score of
                // inner parentheses
                var count = 0;

                // Calculate score of
                // inner parentheses
                while (s[s.length-1] != "(") {

                    // Update count
                    count += parseInt(s[s.length-1]);
                    s.pop();
                }

                // Pop from stack
                s.pop();

                // Insert score of
                // inner parentheses
                s.push((2 * count).toString());
            }
        }

        // Update i
        i++;
    }

    // Calculate score
    // of the string
    while (s.length!=0) {

        // Update ans
        ans += parseInt(s[s.length-1]);
        s.pop();
    }
    return ans;
}

// Driver Code
var S1 = "(()(()))";
document.write( scoreOfParentheses(S1));

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
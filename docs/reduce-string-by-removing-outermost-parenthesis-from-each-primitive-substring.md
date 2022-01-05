# 通过移除每个基本子串的最外层括号来减少字符串

> 原文:[https://www . geesforgeks . org/通过从每个基元子串中移除最外层括号来减少字符串/](https://www.geeksforgeeks.org/reduce-string-by-removing-outermost-parenthesis-from-each-primitive-substring/)

给定一个[有效括号](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-python/)**“(****”**)的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是打印从 **S** 中去掉每个**原始子字符串**最外层括号得到的字符串。

> 一个[有效括号](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)子串 **S** 如果是**非空**，则是**原语**，不能拆分成两个或两个以上非空[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，也是一个有效括号。

**示例:**

> **输入:**S =(()())(())()”
> **输出:** ()()()
> **说明:**输入的字符串是”(()())(())()()“可以分解成原始的支撑”(()())”+“()”+“()”)。删除每个主要子字符串的最外层括号后，得到的字符串是”()()"+ "()" = "()("
> 
> **输入:**S =((()())(())((()())))”
> T3】输出:()()()((())

**方法:**按照以下步骤解决问题:

1.  初始化一个变量**计数**来存储**圆括号**的个数，即**(“**)。
2.  如果**计数**大于 **0** ，则在结果中添加每一个**(“**”)，即在遇到一个原始子串的第一个**(“**)之后添加所有**(“**)。
3.  如果**计数**大于 **0** ，则在结果中添加每一个**')**，即在遇到一个原始子串的最后一个**')**之前添加所有**')**。
4.  最后，打印得到的结果字符串。

**以下是上述方法的实现-**

## C++

```
// C++ program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to remove the outermost
// parentheses of every primitive
// substring from the given string
string removeOuterParentheses(string S)
{

    // Stores the resultant string
    string res;

    // Stores the count of
    // opened parentheses
    int count = 0;

    // Traverse the string
    for (char c : S) {

        // If opening parenthesis is
        // encountered and their
        // count exceeds 0
        if (c == '(' && count++ > 0)

            // Include the character
            res += c;

        // If closing parenthesis is
        // encountered and their
        // count is less than count
        // of opening parentheses
        if (c == ')' && count-- > 1)

            // Include the character
            res += c;
    }

    // Return the resultant string
    return res;
}

// Driver Code
int main()
{
    string S = "(()())(())()";
    cout << removeOuterParentheses(S);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.io.*;
class GFG{

// Function to remove the outermost
// parentheses of every primitive
// substring from the given string
static String removeOuterParentheses(String S)
{
  // Stores the resultant
  // string
  String res = "";

  // Stores the count of
  // opened parentheses
  int count = 0;

  // Traverse the string
  for (int c = 0;
           c < S.length(); c++)
  {
    // If opening parenthesis is
    // encountered and their
    // count exceeds 0
    if (S.charAt(c) == '(' &&
        count++ > 0)

      // Include the character
      res += S.charAt(c);

    // If closing parenthesis is
    // encountered and their
    // count is less than count
    // of opening parentheses
    if (S.charAt(c) == ')' &&
        count-- > 1)

      // Include the character
      res += S.charAt(c);
  }

  // Return the resultant string
  return res;
}

// Driver Code
public static void main(String[] args)
{
  String S = "(()())(())()";
  System.out.print(removeOuterParentheses(S));
}
}

// This code is contributed by Chitranayal
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

# Function to remove the outermost
# parentheses of every primitive
# substring from the given string
def removeOuterParentheses(S):

    # Stores the resultant string
    res = ""

    # Stores the count of
    # opened parentheses
    count = 0

    # Traverse the string
    for c in S:

        # If opening parenthesis is
        # encountered and their
        # count exceeds 0
        if (c == '(' and count > 0):

            # Include the character
            res += c

        # If closing parenthesis is
        # encountered and their
        # count is less than count
        # of opening parentheses
        if (c == '('):
            count += 1
        if (c == ')' and count > 1):

            # Include the character
            res += c

        if (c == ')'):
          count -= 1

    # Return the resultant string
    return res

# Driver Code
if __name__ == '__main__':

    S = "(()())(())()"

    print(removeOuterParentheses(S))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to remove the outermost
// parentheses of every primitive
// substring from the given string
static string removeOuterParentheses(string S)
{

  // Stores the resultant
  // string
  string res = "";

  // Stores the count of
  // opened parentheses
  int count = 0;

  // Traverse the string
  for(int c = 0; c < S.Length; c++)
  {

    // If opening parenthesis is
    // encountered and their
    // count exceeds 0
    if (S == '(' &&
        count++ > 0)

      // Include the character
      res += S;

    // If closing parenthesis is
    // encountered and their
    // count is less than count
    // of opening parentheses
    if (S == ')' &&
        count-- > 1)

      // Include the character
      res += S;
  }

  // Return the resultant string
  return res;
}

// Driver Code
public static void Main()
{
  string S = "(()())(())()";

  Console.Write(removeOuterParentheses(S));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to implement the
// above approach

// Function to remove the outermost
// parentheses of every primitive
// substring from the given string
function removeOuterParentheses(S)
{

// Stores the resultant
// string
let res = "";

// Stores the count of
// opened parentheses
let count = 0;

// Traverse the string
for (let c = 0;
        c < S.length; c++)
{
    // If opening parenthesis is
    // encountered and their
    // count exceeds 0
    if (S.charAt(c) == '(' &&
        count++ > 0)

    // Include the character
    res += S.charAt(c);

    // If closing parenthesis is
    // encountered and their
    // count is less than count
    // of opening parentheses
    if (S.charAt(c) == ')' &&
        count-- > 1)

    // Include the character
    res += S.charAt(c);
}

// Return the resultant string
return res;
}

// Driver Code

let S = "(()())(())()";
document.write(removeOuterParentheses(S));

// This code is contributed by jana_sayantan.
</script>
```

**Output:** 

```
()()()
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
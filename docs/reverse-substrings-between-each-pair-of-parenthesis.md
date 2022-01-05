# 反转每对括号之间的子字符串

> 原文:[https://www . geesforgeks . org/reverse-每对括号之间的子字符串/](https://www.geeksforgeeks.org/reverse-substrings-between-each-pair-of-parenthesis/)

给定一个由小写英文字母和括号组成的字符串。任务是反转每对匹配括号中的子字符串，从最里面的开始。结果不应包含任何括号。

**示例:**

> **输入:** str =“(斯基格(for)斯基格)”
> **输出:**极客们
> 
> **输入:**str =“(ng)IPM(ca))”
> T3】输出:露营

**方法:**这个问题可以用[栈](https://www.geeksforgeeks.org/stack-data-structure/)解决。首先，每当遇到一个 **'('** )时，将元素的索引推入堆栈，每当遇到一个 **')'** 时，将堆栈的顶部元素作为最新的索引，并从堆栈顶部反转当前索引和索引之间的字符串。对字符串的其余部分执行此操作，最后打印更新后的字符串。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the modified string
string reverseParentheses(string str, int len)
{
    stack<int> st;

    for (int i = 0; i < len; i++) {

        // Push the index of the current
        // opening bracket
        if (str[i] == '(') {
            st.push(i);
        }

        // Reverse the substring starting
        // after the last encountered opening
        // bracket till the current character
        else if (str[i] == ')') {
            reverse(str.begin() + st.top() + 1,
                    str.begin() + i);
            st.pop();
        }
    }

    // To store the modified string
    string res = "";
    for (int i = 0; i < len; i++) {
        if (str[i] != ')' && str[i] != '(')
            res += (str[i]);
    }
    return res;
}

// Driver code
int main()
{
    string str = "(skeeg(for)skeeg)";
    int len = str.length();

    cout << reverseParentheses(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;
class GFG {
  static void reverse(char A[], int l, int h)
  {
    if (l < h)
    {
      char ch = A[l];
      A[l] = A[h];
      A[h] = ch;
      reverse(A, l + 1, h - 1);
    }
  }

  // Function to return the modified string
  static String reverseParentheses(String str, int len)
  {
    Stack<Integer> st = new Stack<Integer>();
    for (int i = 0; i < len; i++)
    {

      // Push the index of the current
      // opening bracket
      if (str.charAt(i) == '(')
      {
        st.push(i);
      }

      // Reverse the substring starting
      // after the last encountered opening
      // bracket till the current character
      else if (str.charAt(i) == ')')
      {
        char[] A = str.toCharArray();
        reverse(A, st.peek() + 1, i);
        str = String.copyValueOf(A);
        st.pop();
      }
    }

    // To store the modified string
    String res = "";
    for (int i = 0; i < len; i++)
    {
      if (str.charAt(i) != ')' && str.charAt(i) != '(')
      {
        res += (str.charAt(i));
      }
    }
    return res;
  }

  // Driver code
  public static void main (String[] args)
  {
    String str = "(skeeg(for)skeeg)";
    int len = str.length();
    System.out.println(reverseParentheses(str, len));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the modified string
def reverseParentheses(strr, lenn):
    st = []

    for i in range(lenn):

        # Push the index of the current
        # opening bracket
        if (strr[i] == '('):
            st.append(i)

        # Reverse the substarting
        # after the last encountered opening
        # bracket till the current character
        elif (strr[i] == ')'):
            temp = strr[st[-1]:i + 1]
            strr = strr[:st[-1]] + temp[::-1] + \
                   strr[i + 1:]
            del st[-1]

    # To store the modified string
    res = ""
    for i in range(lenn):
        if (strr[i] != ')' and strr[i] != '('):
            res += (strr[i])
    return res

# Driver code
if __name__ == '__main__':
    strr = "(skeeg(for)skeeg)"
    lenn = len(strr)
    st = [i for i in strr]

    print(reverseParentheses(strr, lenn))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
using System.Text;

class GFG{

static void reverse(char[] A, int l, int h)
{
    if (l < h)
    {
        char ch = A[l];
        A[l] = A[h];
        A[h] = ch;
        reverse(A, l + 1, h - 1);
    }
}

// Function to return the modified string
static string reverseParentheses(string str, int len)
{
    Stack<int> st = new Stack<int>();

    for(int i = 0; i < len; i++)
    {

        // Push the index of the current
        // opening bracket
        if (str[i] == '(')
        {
            st.Push(i);
        }

        // Reverse the substring starting
        // after the last encountered opening
        // bracket till the current character
        else if (str[i] == ')')
        {
            char[] A = str.ToCharArray();
            reverse(A, st.Peek() + 1, i);
            str = new string(A);
            st.Pop();
        }
    }

    // To store the modified string
    string res = "";
    for(int i = 0; i < len; i++)
    {
        if (str[i] != ')' && str[i] != '(')
        {
            res += str[i];
        }
    }
    return res;
}

// Driver code
static public void Main()
{
    string str = "(skeeg(for)skeeg)";
    int len = str.Length;

    Console.WriteLine(reverseParentheses(str, len));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
function reverse(A,l,h)
{
    if (l < h)
    {
      let ch = A[l];
      A[l] = A[h];
      A[h] = ch;
      reverse(A, l + 1, h - 1);
    }
}

 // Function to return the modified string
function reverseParentheses(str,len)
{
    let st = [];
    for (let i = 0; i < len; i++)
    {

      // Push the index of the current
      // opening bracket
      if (str[i] == '(')
      {
        st.push(i);
      }

      // Reverse the substring starting
      // after the last encountered opening
      // bracket till the current character
      else if (str[i] == ')')
      {

        let A = [...str]
        reverse(A, st[st.length-1] + 1, i);
        str = [...A];
        st.pop();
      }
    }

    // To store the modified string
    let res = "";
    for (let i = 0; i < len; i++)
    {
      if (str[i] != ')' && str[i] != '(')
      {
        res += (str[i]);
      }
    }
    return res;
}

 // Driver code
let str = "(skeeg(for)skeeg)";
let len = str.length;
document.write(reverseParentheses(str, len));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
geeksforgeeks
```
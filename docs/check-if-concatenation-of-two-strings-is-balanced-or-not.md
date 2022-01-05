# 检查两个字符串的连接是否平衡

> 原文:[https://www . geesforgeks . org/check-if-concation-two-string-is-balanced-or-not/](https://www.geeksforgeeks.org/check-if-concatenation-of-two-strings-is-balanced-or-not/)

给定由“(”和“)”组成的两个括号序列 S1 和 S2。任务是检查通过连接两个序列获得的字符串是否平衡。s1+s2 或 s2+s1 可以实现串联。

**示例:**

> **输入:** s1 =()((())))”、S2 =(()(()(“
> )T3】输出:平衡
> s2 + s1 =(()((()())()))))”，其中
> 为平衡括号序列。
> 
> **输入:** s1 =(())("，S2 =()))"
> **输出:**不平衡
> S1+S2 =())(()(()))))"–>不平衡
> S2+S1 =())())(()))))("–>不平衡

一个简单的解决方案是首先连接两个序列，然后用堆栈检查结果序列是否平衡。首先，检查 s1 + s2 是否平衡。如果不是，则检查 s2 + s1 是否平衡。要检查给定的括号序列是否平衡，或者是否使用堆栈，可以使用以下算法。

1.  声明一个字符堆栈 s。
2.  现在遍历表达式字符串 exp。
    *   如果当前字符是一个开始括号('('或' {或'[')')，则将其推入堆栈。
    *   如果当前字符是右括号(')'或' } '或']')，则从堆栈中弹出，如果弹出的字符是匹配的起始括号，则细否则括号不均衡。
3.  在完成遍历之后，如果堆栈中还剩下一些起始括号，那么就是“不平衡的”。

下面是上述方法的实现:

## C++

```
// CPP program to check if sequence obtained
// by concatenating two bracket sequences
// is balanced or not.
#include <bits/stdc++.h>
using namespace std;

// Check if given string is balanced bracket
// sequence or not.
bool isBalanced(string s)
{

    stack<char> st;

    int n = s.length();

    for (int i = 0; i < n; i++) {

        // If current bracket is an opening
        // bracket push it to stack.
        if (s[i] == '(')
            st.push(s[i]);

        // If current bracket is a closing
        // bracket then pop from stack if
        // it is not empty. If stack is empty
        // then sequence is not balanced.
        else {
            if (st.empty()) {
                return false;
            }

            else
                st.pop();
        }
    }

    // If stack is not empty, then sequence
    // is not balanced.
    if (!st.empty())
        return false;

    return true;
}

// Function to check if string obtained by
// concatenating two bracket sequences is
// balanced or not.
bool isBalancedSeq(string s1, string s2)
{

    // Check if s1 + s2 is balanced or not.
    if (isBalanced(s1 + s2))
        return true;

    // Check if s2 + s1 is balanced or not.
    return isBalanced(s2 + s1);
}

// Driver code.
int main()
{
    string s1 = ")()(())))";
    string s2 = "(()(()(";

    if (isBalancedSeq(s1, s2))
        cout << "Balanced";
    else
        cout << "Not Balanced";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if sequence obtained
// by concatenating two bracket sequences
// is balanced or not.
import java.util.Stack;

class GFG
{

    // Check if given string is balanced bracket
    // sequence or not.
    static boolean isBalanced(String s)
    {

        Stack<Character> st = new Stack<Character>();

        int n = s.length();

        for (int i = 0; i < n; i++)
        {

            // If current bracket is an opening
            // bracket push it to stack.
            if (s.charAt(i) == '(')
            {
                st.push(s.charAt(i));
            }

            // If current bracket is a closing
            // bracket then pop from stack if
            // it is not empty. If stack is empty
            // then sequence is not balanced.
            else if (st.empty())
            {
                return false;
            }
            else
            {
                st.pop();
            }
        }

        // If stack is not empty, then sequence
        // is not balanced.
        if (!st.empty())
        {
            return false;
        }
        return true;
    }

    // Function to check if string obtained by
    // concatenating two bracket sequences is
    // balanced or not.
    static boolean isBalancedSeq(String s1, String s2)
    {

        // Check if s1 + s2 is balanced or not.
        if (isBalanced(s1 + s2))
        {
            return true;
        }

        // Check if s2 + s1 is balanced or not.
        return isBalanced(s2 + s1);
    }

    // Driver code.
    public static void main(String[] args)
    {
        String s1 = ")()(())))";
        String s2 = "(()(()(";

        if (isBalancedSeq(s1, s2))
        {
            System.out.println("Balanced");
        }
        else
        {
            System.out.println("Not Balanced");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to check if sequence obtained
# by concatenating two bracket sequences
# is balanced or not.

# Check if given string is balanced bracket
# sequence or not.
def isBalanced(s):
    st = list()

    n = len(s)

    for i in range(n):

        # If current bracket is an opening
        # bracket push it to stack.
        if s[i] == '(':
            st.append(s[i])

        # If current bracket is a closing
        # bracket then pop from stack if
        # it is not empty. If stack is empty
        # then sequence is not balanced.
        else:
            if len(st) == 0:
                return False
            else:
                st.pop()

    # If stack is not empty, then sequence
    # is not balanced.
    if len(st) > 0:
        return False

    return True

# Function to check if string obtained by
# concatenating two bracket sequences is
# balanced or not.
def isBalancedSeq(s1, s2):

    # Check if s1 + s2 is balanced or not.
    if (isBalanced(s1 + s2)):
        return True

    # Check if s2 + s1 is balanced or not.
    return isBalanced(s2 + s1)

# Driver Code
if __name__ == "__main__":
    s1 = ")()(())))"
    s2 = "(()(()("

    if isBalancedSeq(s1, s2):
        print("Balanced")
    else:
        print("Not Balanced")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to check if sequence obtained
// by concatenating two bracket sequences
// is balanced or not.
using System;
using System.Collections.Generic;

class GFG
{

    // Check if given string is balanced bracket
    // sequence or not.
    static bool isBalanced(String s)
    {

        Stack<char> st = new Stack<char>();

        int n = s.Length;

        for (int i = 0; i < n; i++)
        {

            // If current bracket is an opening
            // bracket push it to stack.
            if (s[i] == '(')
            {
                st.Push(s[i]);
            }

            // If current bracket is a closing
            // bracket then pop from stack if
            // it is not empty. If stack is empty
            // then sequence is not balanced.
            else if (st.Count==0)
            {
                return false;
            }
            else
            {
                st.Pop();
            }
        }

        // If stack is not empty, then sequence
        // is not balanced.
        if (st.Count!=0)
        {
            return false;
        }
        return true;
    }

    // Function to check if string obtained by
    // concatenating two bracket sequences is
    // balanced or not.
    static bool isBalancedSeq(String s1, String s2)
    {

        // Check if s1 + s2 is balanced or not.
        if (isBalanced(s1 + s2))
        {
            return true;
        }

        // Check if s2 + s1 is balanced or not.
        return isBalanced(s2 + s1);
    }

    // Driver code.
    public static void Main(String[] args)
    {
        String s1 = ")()(())))";
        String s2 = "(()(()(";

        if (isBalancedSeq(s1, s2))
        {
            Console.WriteLine("Balanced");
        }
        else
        {
            Console.WriteLine("Not Balanced");
        }
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to check if sequence
// obtained by concatenating two bracket
// sequences is balanced or not.

// Check if given string is balanced
// bracket sequence or not.
function isBalanced(s)
{
    let st = [];
    let n = s.length;

    for(let i = 0; i < n; i++)
    {

        // If current bracket is an opening
        // bracket push it to stack.
        if (s[i] == '(')
        {
            st.push(s[i]);
        }

        // If current bracket is a closing
        // bracket then pop from stack if
        // it is not empty. If stack is empty
        // then sequence is not balanced.
        else if (st.length == 0)
        {
            return false;
        }
        else
        {
            st.pop();
        }
    }

    // If stack is not empty, then sequence
    // is not balanced.
    if (st.length != 0)
    {
        return false;
    }
    return true;
}

// Function to check if string obtained by
// concatenating two bracket sequences is
// balanced or not.
function isBalancedSeq(s1, s2)
{

    // Check if s1 + s2 is balanced or not.
    if (isBalanced(s1 + s2))
    {
        return true;
    }

    // Check if s2 + s1 is balanced or not.
    return isBalanced(s2 + s1);
}

// Driver code
let s1 = ")()(())))";
let s2 = "(()(()(";

if (isBalancedSeq(s1, s2))
{
    document.write("Balanced");
}
else
{
    document.write("Not Balanced");
}

// This code is contributed by mukesh07 

</script>
```

**Output:** 

```
Balanced
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

一个**有效的**解决方案是检查给定的序列是否可以在不使用堆栈的情况下产生平衡的括号序列，即在恒定的额外空间中。
让串联的序列为 s，有两种可能:s = s1 + s2 平衡或者 s = s2 + s1 平衡。检查两种可能性，s 是否平衡。

*   如果 S 是平衡的，那么在遍历 S 的任何时刻，S 中左括号的数量应该总是大于或等于 S 中右括号的数量。这是因为如果在任何时刻 s 中的结束括号的数量大于开始括号的数量，那么最后一个结束括号在 s 中将没有匹配的开始括号(这就是为什么计数更多)
*   如果序列是平衡的，那么在遍历结束时，s 中左括号的数量等于 s 中右括号的数量。

下面是上述方法的实现:

## C++

```
// C++ program to check if sequence obtained
// by concatenating two bracket sequences
// is balanced or not.
#include <bits/stdc++.h>
using namespace std;

// Check if given string is balanced bracket
// sequence or not.
bool isBalanced(string s)
{

    // To store result of comparison of
    // count of opening brackets and
    // closing brackets.
    int cnt = 0;

    int n = s.length();

    for (int i = 0; i < n; i++) {

        // If current bracket is an
        // opening bracket, then
        // increment count.
        if (s[i] == '(')
            cnt++;

        // If current bracket is a
        // closing bracket, then
        // decrement count and check
        // if count is negative.
        else {
            cnt--;
            if (cnt < 0)
                return false;
        }
    }

    // If count is positive then
    // some opening brackets are
    // not balanced.
    if (cnt > 0)
        return false;

    return true;
}

// Function to check if string obtained by
// concatenating two bracket sequences is
// balanced or not.
bool isBalancedSeq(string s1, string s2)
{

    // Check if s1 + s2 is balanced or not.
    if (isBalanced(s1 + s2))
        return true;

    // Check if s2 + s1 is balanced or not.
    return isBalanced(s2 + s1);
}

// Driver code.
int main()
{
    string s1 = ")()(())))";
    string s2 = "(()(()(";

    if (isBalancedSeq(s1, s2))
        cout << "Balanced";
    else
        cout << "Not Balanced";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// sequence obtained by
// concatenating two bracket
// sequences is balanced or not.
import java.io.*;

class GFG
{

// Check if given string
// is balanced bracket
// sequence or not.
static boolean isBalanced(String s)
{

// To store result of comparison
// of count of opening brackets
// and closing brackets.
int cnt = 0;
int n = s.length();
for (int i = 0; i < n; i++)
{

    // If current bracket is
    // an opening bracket,
    // then increment count.
    if (s.charAt(i) =='(')
    {
        cnt = cnt + 1;
    }

    // If current bracket is a
    // closing bracket, then
    // decrement count and check
    // if count is negative.
    else
    {
        cnt = cnt - 1;
        if (cnt < 0)
            return false;
    }
}

// If count is positive then
// some opening brackets are
// not balanced.
if (cnt > 0)
    return false;

return true;
}

// Function to check if string
// obtained by concatenating
// two bracket sequences is
// balanced or not.
static boolean isBalancedSeq(String s1,
                             String s2)
{

// Check if s1 + s2 is
// balanced or not.
if (isBalanced(s1 + s2))
    return true;

// Check if s2 + s1 is
// balanced or not.
return isBalanced(s2 + s1);
}

// Driver code
public static void main(String [] args)
{
    String s1 = ")()(())))";
    String s2 = "(()(()(";

    if (isBalancedSeq(s1, s2))
    {
        System.out.println("Balanced");
    }
    else
    {
        System.out.println("Not Balanced");
    }
}
}

// This code is contributed
// by Shivi_Aggarwal
```

## 蟒蛇 3

```
# Python3 program to check
# if sequence obtained by
# concatenating two bracket
# sequences is balanced or not.

# Check if given string
# is balanced bracket
# sequence or not.
def isBalanced(s):

    # To store result of
    # comparison of count
    # of opening brackets
    # and closing brackets.
    cnt = 0
    n = len(s)

    for i in range(0, n):
        if (s[i] == '('):
            cnt = cnt + 1
        else :
            cnt = cnt - 1
            if (cnt < 0):
                return False
    if (cnt > 0):
        return False

    return True

def isBalancedSeq(s1, s2):

    if (isBalanced(s1 + s2)):
        return True

    return isBalanced(s2 + s1)

# Driver code
a = ")()(())))";
b = "(()(()(";

if (isBalancedSeq(a, b)):
        print("Balanced")
else:
    print("Not Balanced")

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program to check if
// sequence obtained by
// concatenating two bracket
// sequences is balanced or not.
using System;
class GFG
{

    // Check if given string
    // is balanced bracket
    // sequence or not.
    static bool isBalanced(String s)
    {

        // To store result of comparison
        // of count of opening brackets
        // and closing brackets.
        int cnt = 0;
        int n = s.Length;
        for (int i = 0; i < n; i++)
        {

            // If current bracket is
            // an opening bracket,
            // then increment count.
            if (s[i] =='(')
            {
                cnt = cnt + 1;
            }

            // If current bracket is a
            // closing bracket, then
            // decrement count and check
            // if count is negative.
            else
            {
                cnt = cnt - 1;
                if (cnt < 0)
                    return false;
            }
        }

        // If count is positive then
        // some opening brackets are
        // not balanced.
        if (cnt > 0)
            return false;

        return true;
    }

    // Function to check if string
    // obtained by concatenating
    // two bracket sequences is
    // balanced or not.
    static bool isBalancedSeq(String s1,
                                String s2)
    {

        // Check if s1 + s2 is
        // balanced or not.
       if (isBalanced(s1 + s2))
            return true;

       // Check if s2 + s1 is
       // balanced or not.
       return isBalanced(s2 + s1);
    }

    // Driver code
    public static void Main()
    {
        String s1 = ")()(())))";
        String s2 = "(()(()(";
        if (isBalancedSeq(s1, s2))
        {
            Console.WriteLine("Balanced");
        }
        else
        {
            Console.WriteLine("Not Balanced");
        }
    }
}

// This code is contributed by
// PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP program to check if sequence obtained
// by concatenating two bracket sequences
// is balanced or not.
// Check if given string is balanced bracket
// sequence or not.

function isBalanced($s)
{

    // To store result of comparison of
    // count of opening brackets and
    // closing brackets.
    $cnt = 0;

    $n = strlen($s);

    for ($i = 0; $i < $n; $i++)
    {

        // If current bracket is an
        // opening bracket, then
        // increment count.
        if ($s[$i] == '(')
            $cnt++;

        // If current bracket is a
        // closing bracket, then
        // decrement count and check
        // if count is negative.
        else
        {
            $cnt--;
            if ($cnt < 0)
                return false;
        }
    }

    // If count is positive then
    // some opening brackets are
    // not balanced.
    if ($cnt > 0)
        return false;

    return true;
}

// Function to check if string obtained by
// concatenating two bracket sequences is
// balanced or not.
function isBalancedSeq($s1, $s2)
{

    // Check if s1 + s2 is balanced or not.
    if (isBalanced($s1 + $s2))
        return true;

    // Check if s2 + s1 is balanced or not.
    return isBalanced($s2 + $s1);
}

// Driver code.
    $s1 = ")()(())))";
    $s2 = "(()(()(";

    if (!isBalancedSeq($s1, $s2))
        echo "Balanced";
    else
        echo "Not Balanced";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to check if sequence obtained
// by concatenating two bracket sequences
// is balanced or not.

// Check if given string is balanced bracket
// sequence or not.
function isBalanced(s)
{

    // To store result of comparison of
    // count of opening brackets and
    // closing brackets.
    var cnt = 0;

    var n = s.length;

    for (var i = 0; i < n; i++) {

        // If current bracket is an
        // opening bracket, then
        // increment count.
        if (s[i] == '(')
            cnt++;

        // If current bracket is a
        // closing bracket, then
        // decrement count and check
        // if count is negative.
        else {
            cnt--;
            if (cnt < 0)
                return false;
        }
    }

    // If count is positive then
    // some opening brackets are
    // not balanced.
    if (cnt > 0)
        return false;

    return true;
}

// Function to check if string obtained by
// concatenating two bracket sequences is
// balanced or not.
function isBalancedSeq(s1, s2)
{

    // Check if s1 + s2 is balanced or not.
    if (isBalanced(s1 + s2))
        return true;

    // Check if s2 + s1 is balanced or not.
    return isBalanced(s2 + s1);
}

// Driver code.
var s1 = ")()(())))";
var s2 = "(()(()(";
if (isBalancedSeq(s1, s2))
    document.write( "Balanced");
else
    document.write( "Not Balanced");

</script>
```

**Output:** 

```
Balanced
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
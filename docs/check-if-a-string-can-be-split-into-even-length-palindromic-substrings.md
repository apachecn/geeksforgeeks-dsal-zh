# 检查一个字符串是否可以拆分成偶数长度的回文子串

> 原文:[https://www . geesforgeks . org/check-if-a-string-can-split-in-even-length-回文-substrings/](https://www.geeksforgeeks.org/check-if-a-string-can-be-split-into-even-length-palindromic-substrings/)

给定一个字符串 **str** ，任务是检查是否有可能将给定的字符串拆分成偶数长度的[回文子字符串](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string/)。
**例:**

> **输入:**str = " Abbas cc "
> **输出:**是
> **解释:**
> 字符串“abba”和“cc”是偶数长度回文子串。
> **输入:** str = "abcde"
> **输出:**无
> **解释:**
> 无偶长回文子串可能。

**方法:**思路是使用[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)。以下是步骤:

1.  初始化一个空堆栈。
2.  遍历给定的字符串**字符串**。
3.  对于给定字符串中的每个字符，请执行以下操作:
    *   如果字符等于堆栈顶部的字符，则从堆栈中弹出顶部元素。
    *   否则将当前字符推入堆栈。
4.  如果在上述步骤之后堆栈为空，那么给定的字符串可以被分解成偶数长度的回文子串。
5.  否则给定的字符串不能分解成偶数长度的回文子串。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check string str can be
// split a string into even length
// palindromic substrings
bool check(string s, int n)
{

    // Initialize a stack
    stack<char> st;

    // Iterate the string
    for (int i = 0; i < n; i++) {

        // If the i-th character is same
        // as that at the top of the stack
        // then pop the top element
        if (!st.empty() && st.top() == s[i])
            st.pop();

        // Else push the current character
        // into the stack
        else
            st.push(s[i]);
    }

    // If the stack is empty, then even
    // palindromic substrings are possible
    if (st.empty()) {
        return true;
    }

    // Else not-possible
    else {
        return false;
    }
}

// Driver Code
int main()
{
    // Given string
    string str = "aanncddc";

    int n = str.length();

    // Function Call
    if (check(str, n)) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check String str can be
// split a String into even length
// palindromic subStrings
static boolean check(String s, int n)
{

    // Initialize a stack
    Stack<Character> st = new Stack<Character>();

    // Iterate the String
    for(int i = 0; i < n; i++)
    {

       // If the i-th character is same
       // as that at the top of the stack
       // then pop the top element
       if (!st.isEmpty() &&
               st.peek() == s.charAt(i))
           st.pop();

       // Else push the current character
       // into the stack
       else
           st.add(s.charAt(i));
    }

    // If the stack is empty, then even
    // palindromic subStrings are possible
    if (st.isEmpty())
    {
        return true;
    }

    // Else not-possible
    else
    {
        return false;
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    String str = "aanncddc";

    int n = str.length();

    // Function Call
    if (check(str, n))
    {
        System.out.print("Yes" + "\n");
    }
    else
    {
        System.out.print("No" + "\n");
    }
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check string str can be
# split a string into even length
# palindromic substrings
def check(s, n):

    st = []

    # Iterate the string
    for i in range(n):

        # If the i-th character is same
        # as that at the top of the stack
        # then pop the top element
        if (len(st) != 0 and
         st[len(st) - 1] == s[i]):
            st.pop();

        # Else push the current character
        # into the stack
        else:
            st.append(s[i]);

    # If the stack is empty, then even
    # palindromic substrings are possible
    if (len(st) == 0):
        return True;

    # Else not-possible
    else:
        return False;

# Driver Code

# Given string
str = "aanncddc";
n = len(str)

# Function Call
if (check(str, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by grand_master   
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check String str can be
// split a String into even length
// palindromic subStrings
static bool check(String s, int n)
{

    // Initialize a stack
    Stack<int> st = new Stack<int>();

    // Iterate the String
    for(int i = 0; i < n; i++)
    {

        // If the i-th character is same
        // as that at the top of the stack
        // then pop the top element
        if (st.Count != 0 &&
            st.Peek() == s[i])
            st.Pop();

        // Else push the current character
        // into the stack
        else
            st.Push(s[i]);
    }

    // If the stack is empty, then even
    // palindromic subStrings are possible
    if (st.Count == 0)
    {
        return true;
    }

    // Else not-possible
    else
    {
        return false;
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given String
    String str = "aanncddc";

    int n = str.Length;

    // Function call
    if (check(str, n))
    {
        Console.Write("Yes" + "\n");
    }
    else
    {
        Console.Write("No" + "\n");
    }
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check string str can be
// split a string into even length
// palindromic substrings
function check(s, n)
{

    // Initialize a stack
    var st = [];

    // Iterate the string
    for (var i = 0; i < n; i++) {

        // If the i-th character is same
        // as that at the top of the stack
        // then pop the top element
        if (st.length!=0 && st[st.length-1] == s[i])
            st.pop();

        // Else push the current character
        // into the stack
        else
            st.push(s[i]);
    }

    // If the stack is empty, then even
    // palindromic substrings are possible
    if (st.length==0) {
        return true;
    }

    // Else not-possible
    else {
        return false;
    }
}

// Driver Code

// Given string
var str = "aanncddc";
var n = str.length;

// Function Call
if (check(str, n)) {
    document.write( "Yes" );
}
else {
    document.write( "No" );
}

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(N)* ，其中 N 为给定字符串的长度。
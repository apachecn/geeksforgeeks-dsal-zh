# 打印所有可以通过替换通配符“？”形成的平衡括号字符串

> 原文:[https://www . geeksforgeeks . org/print-all-balanced-方括号-字符串-可通过替换通配符形成的字符串/](https://www.geeksforgeeks.org/print-all-balanced-brackets-strings-that-can-be-formed-by-replacing-wild-card/)

给定包含字符**“？”的[字符串](https://www.geeksforgeeks.org/string-class-in-java/)和**字符串**，'('****)'，**任务是替换**'？'**字符，带**(“**或**)”**、[打印所有包含](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)[平衡括号](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)的字符串

**示例:**

> **输入:** str =？？？?"
> **输出:**
> ()
> (()
> 
> **输入:** str =((()？)
> **输出:**(())

**方法:**给定的问题可以使用[递归](https://www.geeksforgeeks.org/recursion/)和[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)来解决。想法是用每一个**“？”**字符带 **')'** 然后递归调用下一个索引，回溯后改到**'(**然后递归调用下一个索引，回溯后改回**'？'**。按照以下步骤解决问题:

*   将[字符串**字符串**转换为字符数组](https://www.geeksforgeeks.org/convert-a-string-to-character-array-in-java/)，比如 **ch**
*   将字符数组 **ch** 和**索引** 0 作为参数传递给递归函数，并在每次递归调用时执行以下操作:
    *   如果索引等于字符数组的长度:
        *   检查字符数组是否为[平衡括号字符串](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)
        *   如果上述条件成立，则打印字符串
    *   如果当前字符 **ch【索引】**是**(**或**)**，则对下一个索引进行递归调用
    *   如果当前字符 **ch【索引】**是“？”然后:
        *   将其替换为**(“**)并对下一个索引进行递归调用
        *   替换为 **')'** ，并对下一个索引进行递归调用
        *   改回**'？'**从功能返回之前

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the
// characters of the string
void print(string ch)
{

    for (char c : ch) {
        cout << c;
    }
    cout << endl;
}

// Function to check if the
// brackets are valid or not
bool check(string ch)
{

    // Initialize a stack
    stack<char> S;

    // If character is an open bracket
    // then return false
    if (ch[0] == ')') {

        return false;
    }

    // Iterate the character array
    for (int i = 0; i < ch.length(); i++) {

        // If character is an open bracket
        // then push it in the stack
        if (ch[i] == '(') {

            S.push('(');
        }

        // If character is a close bracket
        else {

            // If stack is empty, there is no
            // corresponding opening bracket
            // so return false
            if (S.size() == 0)
                return false;

            // Else pop the corresponding
            // opening bracket from the stack
            else
                S.pop();
        }
    }

    // If no opening bracket remains
    // then return true
    if (S.size() == 0)
        return true;

    // If there are opening brackets
    // then return false
    else
        return false;
}

// Function to find number of
// strings having balanced brackets
void count(string ch, int index)
{

    // Reached end of character array
    if (index == ch.length()) {

        // Check if the character array
        // contains balanced string
        if (check(ch)) {

            // If it is a balanced string
            // then print its characters
            print(ch);
        }

        return;
    }

    if (ch[index] == '?') {

        // replace ? with (
        ch[index] = '(';

        count(ch, index + 1);

        // replace ? with )
        ch[index] = ')';

        count(ch, index + 1);

        // backtrack
        ch[index] = '?';
    }
    else {

        // If current character is a
        // valid bracket then continue
        // to the next character
        count(ch, index + 1);
    }
}

// Driver function
int main()
{

    string ch = "????";

    // Call the function
    count(ch, 0);
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class Main {

    // Function to print the
    // characters of the string
    static void print(char ch[])
    {

        for (Character c : ch) {
            System.out.print(c);
        }
        System.out.println();
    }

    // Function to check if the
    // brackets are valid or not
    static boolean check(char ch[])
    {

        // Initialize a stack
        Stack<Character> S = new Stack<>();

        // If character is an open bracket
        // then return false
        if (ch[0] == ')') {

            return false;
        }

        // Iterate the character array
        for (int i = 0; i < ch.length; i++) {

            // If character is an open bracket
            // then push it in the stack
            if (ch[i] == '(') {

                S.add('(');
            }

            // If character is a close bracket
            else {

                // If stack is empty, there is no
                // corresponding opening bracket
                // so return false
                if (S.size() == 0)
                    return false;

                // Else pop the corresponding
                // opening bracket from the stack
                else
                    S.pop();
            }
        }

        // If no opening bracket remains
        // then return true
        if (S.size() == 0)
            return true;

        // If there are opening brackets
        // then return false
        else
            return false;
    }

    // Function to find number of
    // strings having balanced brackets
    static void count(char ch[], int index)
    {

        // Reached end of character array
        if (index == ch.length) {

            // Check if the character array
            // contains balanced string
            if (check(ch)) {

                // If it is a balanced string
                // then print its characters
                print(ch);
            }

            return;
        }

        if (ch[index] == '?') {

            // replace ? with (
            ch[index] = '(';

            count(ch, index + 1);

            // replace ? with )
            ch[index] = ')';

            count(ch, index + 1);

            // backtrack
            ch[index] = '?';
        }
        else {

            // If current character is a
            // valid bracket then continue
            // to the next character
            count(ch, index + 1);
        }
    }

    // Driver function
    public static void main(String[] args)
    {

        String m = "????";
        char ch[] = m.toCharArray();

        // Call the function
        count(ch, 0);
    }
}
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to print the
# characters of the string
def printf(ch):

  for c in ch:
    print(c, end="");
  print("");

# Function to check if the
# brackets are valid or not
def check(ch):

  # Initialize a stack
  S = [];

  # If character is an open bracket
  # then return false
  if (ch[0] == ')'):
    return False;

  # Iterate the character array
  for i in range(len(ch)):

    # If character is an open bracket
    # then push it in the stack
    if (ch[i] == '('):
      S.append('(');

    # If character is a close bracket
    else:

      # If stack is empty, there is no
      # corresponding opening bracket
      # so return false
      if (len(S) == 0):
        return False;

      # Else pop the corresponding
      # opening bracket from the stack
      else:
        S.pop();

  # If no opening bracket remains
  # then return true
  if (len(S) == 0):
    return True;

  # If there are opening brackets
  # then return false
  else:
    return False;

# Function to find number of
# strings having balanced brackets
def count(ch, index):

  # Reached end of character array
  if (index == len(ch)):

    # Check if the character array
    # contains balanced string
    if (check(ch)):

      # If it is a balanced string
      # then print its characters
      printf(ch);

    return;

  if (ch[index] == '?'):

    # replace ? with (
    ch[index] = '(';

    count(ch, index + 1);

    # replace ? with )
    ch[index] = ')';

    count(ch, index + 1);

    # backtrack
    ch[index] = '?';
  else:

    # If current character is a
    # valid bracket then continue
    # to the next character
    count(ch, index + 1);

# Driver function
ch = "????";

# Call the function
count(list(ch), 0);

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections;

public class Gfg{

    // Function to print the
    // characters of the string
    static void print(char []ch)
    {

        foreach (char c in ch) {
            Console.Write(c);
        }
        Console.WriteLine();
    }

    // Function to check if the
    // brackets are valid or not
    static bool check(char []ch)
    {

        // Initialize a stack
        Stack S = new Stack();

        // If character is an open bracket
        // then return false
        if (ch[0] == ')') {

            return false;
        }

        // Iterate the character array
        for (int i = 0; i < ch.Length; i++) {

            // If character is an open bracket
            // then push it in the stack
            if (ch[i] == '(') {

                S.Push('(');
            }

            // If character is a close bracket
            else {

                // If stack is empty, there is no
                // corresponding opening bracket
                // so return false
                if (S.Count == 0)
                    return false;

                // Else pop the corresponding
                // opening bracket from the stack
                else
                    S.Pop();
            }
        }

        // If no opening bracket remains
        // then return true
        if (S.Count == 0)
            return true;

        // If there are opening brackets
        // then return false
        else
            return false;
    }

    // Function to find number of
    // strings having balanced brackets
    static void count(char []ch, int index)
    {

        // Reached end of character array
        if (index == ch.Length) {

            // Check if the character array
            // contains balanced string
            if (check(ch)) {

                // If it is a balanced string
                // then print its characters
                print(ch);
            }

            return;
        }

        if (ch[index] == '?') {

            // replace ? with (
            ch[index] = '(';

            count(ch, index + 1);

            // replace ? with )
            ch[index] = ')';

            count(ch, index + 1);

            // backtrack
            ch[index] = '?';
        }
        else {

            // If current character is a
            // valid bracket then continue
            // to the next character
            count(ch, index + 1);
        }
    }

    // Driver function
    public static void Main(string[] args)
    {

        string m = "????";
        char []ch = m.ToCharArray();

        // Call the function
        count(ch, 0);
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to print the
// characters of the string
function printf(ch) {
  for (c of ch) {
    document.write(c);
  }
  document.write("<br>");
}

// Function to check if the
// brackets are valid or not
function check(ch) {

  // Initialize a stack
  let S = [];

  // If character is an open bracket
  // then return false
  if (ch[0] == ')') {

    return false;
  }

  // Iterate the character array
  for (let i = 0; i < ch.length; i++) {

    // If character is an open bracket
    // then push it in the stack
    if (ch[i] == '(') {

      S.push('(');
    }

    // If character is a close bracket
    else {

      // If stack is empty, there is no
      // corresponding opening bracket
      // so return false
      if (S.length == 0)
        return false;

      // Else pop the corresponding
      // opening bracket from the stack
      else
        S.pop();
    }
  }

  // If no opening bracket remains
  // then return true
  if (S.length == 0)
    return true;

  // If there are opening brackets
  // then return false
  else
    return false;
}

// Function to find number of
// strings having balanced brackets
function count(ch, index) {

  // Reached end of character array
  if (index == ch.length) {

    // Check if the character array
    // contains balanced string
    if (check(ch)) {

      // If it is a balanced string
      // then print its characters
      printf(ch);
    }

    return;
  }

  if (ch[index] == '?') {

    // replace ? with (
    ch[index] = '(';

    count(ch, index + 1);

    // replace ? with )
    ch[index] = ')';

    count(ch, index + 1);

    // backtrack
    ch[index] = '?';
  }
  else {

    // If current character is a
    // valid bracket then continue
    // to the next character
    count(ch, index + 1);
  }
}

// Driver function
let ch = "????";

// Call the function
count(ch.split(""), 0);

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output**

```
(())
()()
```

**时间复杂度:**o(n*2^n)
T3】辅助空间: O(N)
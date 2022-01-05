# 通过递归删除子串“abc”检查仅由 a、b、c 组成的字符串是否可以为空

> 原文:[https://www . geeksforgeeks . org/check-if-a-string-仅由-a-b-c 组成-可通过移除-substring-ABC-递归使-空/](https://www.geeksforgeeks.org/check-if-a-string-consisting-only-of-a-b-c-can-be-made-empty-by-removing-substring-abc-recursively/)

给定一个大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，仅由字符“ **a** ”、“ **b** ”和“ **c** ”组成，任务是通过递归移除字符串“abc”来检查给定字符串是否可以为空。如果**发现**为**真**，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:***S = ababc*
> T5】输出:是
> T8】说明:
> 以下是清空字符串的操作:
> 
> 1.  从字符串中删除子字符串 S[3，5]会将字符串 S 修改为“abc”。
> 2.  从字符串中删除子字符串[0，2]会将字符串修改为“”。
> 
> 在上述操作之后，可以通过移除子字符串“abc”来使给定的字符串 S 为空。因此，打印“是”。
> 
> **输入:***S =*abcbababccc
> T5】输出:否

**方法:**给定的问题可以通过使用[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)来解决。这个想法是[通过移除所有出现的“ABC”](https://www.geeksforgeeks.org/replace-all-occurrences-of-a-string-with-space/)将字符串最小化为空字符串。按照以下步骤解决给定的问题:

*   初始化一个[栈](https://www.geeksforgeeks.org/stack-data-structure/)，比如说**栈**来存储给定字符串 **S** 的字符。
*   遍历给定的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，并执行以下步骤:
    *   如果当前角色是“ **a** ”或“ **b** ”，则推至[栈](https://www.geeksforgeeks.org/stack-data-structure/) **栈**。
    *   如果当前字符为“ **c** ”，最后两个字符分别为“ **b** ”和“ **a** ，则[从堆栈](https://www.geeksforgeeks.org/stack-pop-method-in-java/)中弹出两次。
    *   如果当前字符是“ **c** ”，最后两个字符是**不是**“**b**”和“ **a** ”，那么给定的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 就无法形成。
*   完成上述步骤后，如果[堆栈为空](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the given
// string S can be made empty
string canMadeEmpty(string s, int n)
{
    // Stores the characters
    // of the string S
    stack<char> St;

    // Traverse the given string
    for (int i = 0; i < n; i++) {
        // If the character is c
        if (s[i] == 'c') {

            // If stack size is greater
            // than 2
            if (St.size() >= 2) {

                // Pop from the stack
                char b = St.top();
                St.pop();
                char a = St.top();
                St.pop();

                // Top two characters in
                // the stack should be 'b'
                // and 'a' respectively
                if (a != 'a' || b != 'b')
                    return "No";
            }

            // Otherwise, print No
            else
                return "No";
        }

        // If character is 'a' or 'b'
        // push to stack
        else
            St.push(s[i]);
    }

    // If stack is empty, then print
    // Yes. Otherwise print No
    if (St.size() == 0) {
        return "Yes";
    }
    else {
        return "No";
    }
}

// Driver Code
int main()
{
    string S = "aabcbc";
    int N = S.length();
    cout << canMadeEmpty(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to check if the given
// String S can be made empty
static String canMadeEmpty(String s, int n)
{

    // Stores the characters
    // of the String S
    Stack<Character> St = new Stack<Character>();

    // Traverse the given String
    for (int i = 0; i < n; i++)
    {

        // If the character is c
        if (s.charAt(i) == 'c') {

            // If stack size is greater
            // than 2
            if (St.size() >= 2) {

                // Pop from the stack
                char b = St.peek();
                St.pop();
                char a = St.peek();
                St.pop();

                // Top two characters in
                // the stack should be 'b'
                // and 'a' respectively
                if (a != 'a' || b != 'b')
                    return "No";
            }

            // Otherwise, print No
            else
                return "No";
        }

        // If character is 'a' or 'b'
        // push to stack
        else
            St.add(s.charAt(i));
    }

    // If stack is empty, then print
    // Yes. Otherwise print No
    if (St.size() == 0) {
        return "Yes";
    }
    else {
        return "No";
    }
}

// Driver Code
public static void main(String[] args)
{
    String S = "aabcbc";
    int N = S.length();
    System.out.print(canMadeEmpty(S, N));
}
}

// This code is contributed by Princi Singh.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if the given
# string S can be made empty
def canMadeEmpty(s, n):

    # Stores the characters
    # of the string S
    st = []

    # Traverse the given string
    for i in range(n):

        # If the character is c
        if s[i] == 'c':

             # If stack size is greater
            # than 2
            if len(st) >= 2:

                # Pop from the stack
                b = st[-1]
                st.pop()
                a = st[-1]
                st.pop()

                 # Top two characters in
                # the stack should be 'b'
                # and 'a' respectively
                if a != 'a' or b != 'b':
                    return "No"

             # Otherwise, print No
            else:
                return "No"

        # If character is 'a' or 'b'
        # push to stack
        else:
            st.append(s[i])

    # If stack is empty, then print
    # Yes. Otherwise print No
    if len(st) == 0:
        return "Yes"
    else:
        return "No"

# Driver code
s = "aabcbc"
n = len(s)
print(canMadeEmpty(s, n))

# This code is contributed by Parth Manchanda
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to check if the given
// String S can be made empty
static String canMadeEmpty(String s, int n)
{

    // Stores the characters
    // of the String S
    Stack<char> St = new Stack<char>();

    // Traverse the given String
    for (int i = 0; i < n; i++)
    {

        // If the character is c
        if (s[i] == 'c') {

            // If stack size is greater
            // than 2
            if (St.Count >= 2) {

                // Pop from the stack
                char b = St.Peek();
                St.Pop();
                char a = St.Peek();
                St.Pop();

                // Top two characters in
                // the stack should be 'b'
                // and 'a' respectively
                if (a != 'a' || b != 'b')
                    return "No";
            }

            // Otherwise, print No
            else
                return "No";
        }

        // If character is 'a' or 'b'
        // push to stack
        else
            St.Push(s[i]);
    }

    // If stack is empty, then print
    // Yes. Otherwise print No
    if (St.Count == 0) {
        return "Yes";
    }
    else {
        return "No";
    }
}

// Driver Code
public static void Main(String[] args)
{
    String S = "aabcbc";
    int N = S.Length;
    Console.Write(canMadeEmpty(S, N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
        // JavaScript Program for the above approach

        // Function to check if the given
        // string S can be made empty
        function canMadeEmpty(s, n) {
            // Stores the characters
            // of the string S
            let St = [];

            // Traverse the given string
            for (let i = 0; i < n; i++) {
                // If the character is c
                if (s[i] == 'c') {

                    // If stack size is greater
                    // than 2
                    if (St.length >= 2) {

                        // Pop from the stack
                        let b = St[St.length - 1];
                        St.pop();
                        let a = St[St.length - 1];
                        St.pop();

                        // Top two characters in
                        // the stack should be 'b'
                        // and 'a' respectively
                        if (a != 'a' || b != 'b')
                            return "No";
                    }

                    // Otherwise, print No
                    else
                        return "No";
                }

                // If character is 'a' or 'b'
                // push to stack
                else
                    St.push(s[i]);
            }

            // If stack is empty, then print
            // Yes. Otherwise print No
            if (St.length == 0) {
                return "Yes";
            }
            else {
                return "No";
            }
        }

        // Driver Code

        let S = "aabcbc";
        let N = S.length;
        document.write(canMadeEmpty(S, N));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
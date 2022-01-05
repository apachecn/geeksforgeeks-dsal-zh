# 检查弦 S1 是否可以通过重复插入另一根弦 S2

形成

> 原文:[https://www . geeksforgeeks . org/check-if-string-S1-can-formed-use-repeat-insertions-other-string-S2/](https://www.geeksforgeeks.org/check-if-string-s1-can-be-formed-using-repeated-insertions-of-another-string-s2/)

给定由唯一字符组成的两个字符串 **S1** 和 **S2** ，任务是检查 S1 是否可以通过重复插入字符串 **S2** 而形成。

> **输入:**S1 =“AABB”，S2 =“ab”
> **输出:**是
> **说明:**所述弦经过一系列招式即可获得:
> 
> *   在空字符串中插入字符串“ab”。当前字符串将是“ **ab**
> *   在" a "之后插入" ab "。最后一串将是“a **ab** b”
> 
> **输入:**S1 =“ababcd”，S2 =“ABC”
> **输出:**否
> **说明:**任何一个系列的招式都不可能获得上面的弦。

**方法:**给定的问题可以使用[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)来解决。想法是将 S1 的角色插入堆栈，直到找到 S2 的最后一个角色。然后从堆栈中弹出长度为(S2)的字符，并与 S2 进行比较。如果不一样，停止并返回 false。否则重复这个过程，直到 S1 变空。

以下是上述方法的步骤:

*   首先，检查以下案例，如果发现真实，则返回 false:
    *   S1 独特人物的数量必须与 S2 相同
    *   字符串 S1 的长度必须是 S2 的倍数
*   维护一个[](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)****为所有角色****
*   ****遍历[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S1** 并推送堆栈中的字符****
*   ****如果当前字符是字符串 **S2** 的最后一个字符，则匹配堆栈左侧的所有字符****
*   ****如果任何位置的堆栈为空或字符不匹配，则返回 False****
*   ****在字符串上完成迭代后，检查堆栈是否为空。如果堆栈不为空，则返回 false，否则返回 true****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check a valid insertion
bool validInsertionstring(string S1, string S2)
{

    // Store the size of string
    int N = S1.length();
    int M = S2.length();

    // Maintain a stack for characters
    stack<char> st;

    // Iterate through the string
    for (int i = 0; i < N; i++) {

        // push the current character
        // on top of the stack
        st.push(S1[i]);

        // If the current character is the
        // last character of string S2 then
        // pop characters until S2 is not formed
        if (S1[i] == S2[M - 1]) {

            // index of last character of the string S2
            int idx = M - 1;

            // pop characters till 0-th index
            while (idx >= 0) {
                if (st.empty()) {
                    return false;
                }
                char c = st.top();
                st.pop();
                if (c != S2[idx]) {
                    return false;
                }
                idx--;
            }
        }
    }

    // Check if stack in non-empty
    if (!st.empty()) {
        return false;
    }
    else {
        return true;
    }
}

// Driver Code
int main()
{
    string S1 = "aabb";
    string S2 = "ab";
    validInsertionstring(S1, S2) ? cout << "Yes\n"
                                 : cout << "No\n";
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG
{

    // Function to check a valid insertion
    static boolean validInsertionstring(String S1,
                                        String S2)
    {

        // Store the size of string
        int N = S1.length();
        int M = S2.length();

        // Maintain a stack for characters
        Stack<Character> st = new Stack<>();

        // Iterate through the string
        for (int i = 0; i < N; i++) {

            // push the current character
            // on top of the stack
            st.push(S1.charAt(i));

            // If the current character is the
            // last character of string S2 then
            // pop characters until S2 is not formed
            if (S1.charAt(i) == S2.charAt(M - 1)) {

                // index of last character of the string S2
                int idx = M - 1;

                // pop characters till 0-th index
                while (idx >= 0) {
                    if (st.size() == 0) {
                        return false;
                    }
                    char c = st.peek();
                    st.pop();
                    if (c != S2.charAt(idx)) {
                        return false;
                    }
                    idx--;
                }
            }
        }

        // Check if stack in non-empty
        if (st.size() > 0) {
            return false;
        }
        else {
            return true;
        }
    }

  // Driver code
    public static void main(String[] args)
    {
        String S1 = "aabb";
        String S2 = "ab";
        if (validInsertionstring(S1, S2) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Potta Lokesh**
```

## ****蟒蛇 3****

```
**# Python3 implementation for the above approach

# Function to check a valid insertion
def validInsertionstring(S1, S2):
    # Store the size of string
    N = len(S1)
    M = len(S2)

    # Maintain a stack for characters
    st = []

    # Iterate through the string
    for i in range(N):
        # push the current character
        # on top of the stack
        st.append(S1[i])

        # If the current character is the
        # last character of string S2 then
        # pop characters until S2 is not formed
        if (S1[i] == S2[M - 1]):
            # index of last character of the string S2
            idx = M - 1

            # pop characters till 0-th index
            while (idx >= 0):
                if (len(st) == 0):
                    return False
                c = st[-1]
                st.pop()
                if (c != S2[idx]):
                    return False
                idx-=1

    # Check if stack in non-empty
    if (len(st) != 0):
        return False
    else:
        return True

S1 = "aabb"
S2 = "ab"
if validInsertionstring(S1, S2):
    print("Yes")
else:
    print("No")

    # This code is contributed by divyeshrabadiya07.**
```

## ****C#****

```
**// C# implementation for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check a valid insertion
static bool validInsertionstring(string S1, string S2)
{

    // Store the size of string
    int N = S1.Length;
    int M = S2.Length;

    // Maintain a stack for characters
    Stack<char> st = new Stack<char>();

    // Iterate through the string
    for (int i = 0; i < N; i++) {

        // push the current character
        // on top of the stack
        st.Push(S1[i]);

        // If the current character is the
        // last character of string S2 then
        // pop characters until S2 is not formed
        if (S1[i] == S2[M - 1]) {

            // index of last character of the string S2
            int idx = M - 1;

            // pop characters till 0-th index
            while (idx >= 0) {
                if (st.Count==0) {
                    return false;
                }
                char c = st.Peek();
                st.Pop();
                if (c != S2[idx]) {
                    return false;
                }
                idx--;
            }
        }
    }

    // Check if stack in non-empty
    if (st.Count > 0) {
        return false;
    }
    else {
        return true;
    }
}

// Driver Code
public static void Main()
{
    string S1 = "aabb";
    string S2 = "ab";
    if(validInsertionstring(S1, S2)==true)
     Console.Write("Yes");
    else
     Console.Write("No");
}
}

// This code is contributed by SURENDRA_GANGWAR.**
```

## ****java 描述语言****

```
**<script>
    // Javascript implementation for the above approach

    // Function to check a valid insertion
    function validInsertionstring(S1, S2)
    {

        // Store the size of string
        let N = S1.length;
        let M = S2.length;

        // Maintain a stack for characters
        let st = [];

        // Iterate through the string
        for (let i = 0; i < N; i++) {

            // push the current character
            // on top of the stack
            st.push(S1[i]);

            // If the current character is the
            // last character of string S2 then
            // pop characters until S2 is not formed
            if (S1[i] == S2[M - 1]) {

                // index of last character of the string S2
                let idx = M - 1;

                // pop characters till 0-th index
                while (idx >= 0) {
                    if (st.length == 0) {
                        return false;
                    }
                    let c = st[st.length - 1];
                    st.pop();
                    if (c != S2[idx]) {
                        return false;
                    }
                    idx--;
                }
            }
        }

        // Check if stack in non-empty
        if (st.length != 0) {
            return false;
        }
        else {
            return true;
        }
    }

    let S1 = "aabb";
    let S2 = "ab";
    validInsertionstring(S1, S2) ? document.write("Yes")
                                 : document.write("No");

// This code is contributed by suresh07.
</script>**
```

******Output:** 

```
Yes
```**** 

******时间复杂度:**O(N * M)
T3】辅助空间: O(N)****
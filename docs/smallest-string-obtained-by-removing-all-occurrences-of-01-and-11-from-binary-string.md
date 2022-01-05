# 通过从二进制字符串

中移除 01 和 11 的所有出现而获得的最小字符串

> 原文:[https://www . geesforgeks . org/minist-string-通过从二进制字符串中删除所有出现的-01 和-11 获得/](https://www.geeksforgeeks.org/smallest-string-obtained-by-removing-all-occurrences-of-01-and-11-from-binary-string/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是通过移除所有出现的子字符串**【01】**和**【11】**来找到可能的最小字符串。删除任何子字符串后，连接字符串的其余部分。

**示例:**

> **输入:** S = "0010110"
> **输出:**
> 长度= 1 串= 0
> **说明:**串可以通过以下步骤进行变换:
> 0<u>01</u>0110→0<u>01</u>10→<u>01</u>0→0。
> 由于没有剩余子串 01 和 11 的出现，串“0”具有最小可能长度 1。
> 
> **输入:** S = "0011101111"
> **输出:**长度= 0
> **说明:**
> 字符串可以通过以下步骤进行转换:
> 0<u>01</u>1101111→0110<u>11</u>11→<u>01</u>1011→1<u>01</u>1

**方法:**解决问题的思路是观察以下几种情况:

*   **01****11**是说**吗？1** 可在**“？”处拆除**可以是 **1** 或 **0** 。
*   最终字符串将始终采用 **1000…** 或 **000…** 的形式

这个问题可以通过在从左到右处理给定字符串 **S** 时维护一个[堆栈](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)来解决。如果当前二进制数字是 **0** ，将其添加到堆栈中，如果当前二进制数字是 **1** ，则从堆栈中移除顶部位。如果[堆栈](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)为空，则将当前位推入堆栈。按照以下步骤解决问题:

1.  初始化一个**栈**来存储最小可能的字符串。
2.  在范围**【0，N–1】**内遍历给定的字符串。
3.  如果堆栈为空，按堆栈中当前的二进制数字 **S[i]** 。
4.  如果堆栈不为空，且当前位 **S[i]** 为 **1** ，则从堆栈中移除顶部位。
5.  如果当前元素 **S[i]** 为 **0** ，则将其推至堆栈。
6.  最后，从上到下追加堆栈中的所有元素，并作为结果打印出来。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum
// length of the given string
void findMinLength(string s, int n)
{
    // Initialize a stack
    stack<int> st;

    // Traverse the string
    for (int i = 0; i < n; i++) {

        // If the stack is empty
        if (st.empty())

            // Push the character
            st.push(s[i]);

        // If the character is 1
        else if (s[i] == '1')

            // Pop the top element
            st.pop();

        // Otherwise
        else
            // Push the character
            // to the stack
            st.push(s[i]);
    }

    // Initialize length
    int ans = 0;

    // Append the characters
    // from top to bottom
    vector<char> finalStr;

    // Until Stack is empty
    while (!st.empty()) {
        ans++;
        finalStr.push_back(st.top());
        st.pop();
    }

    // Print the final string size
    cout << "Length = " << ans;

    // If length of the string is not 0
    if (ans != 0) {

        // Print the string
        cout << "\nString = ";
        for (int i = 0; i < ans; i++)
            cout << finalStr[i];
    }
}

// Driver Code
int main()
{
    // Given string
    string S = "101010";

    // String length
    int N = S.size();

    // Function call
    findMinLength(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find minimum
// length of the given string
static void findMinLength(String s, int n)
{

    // Initialize a stack
    Stack<Character> st = new Stack<>(); 

    // Traverse the string
    for(int i = 0; i < n; i++)
    {

        // If the stack is empty
        if (st.empty())

            // Push the character
            st.push(s.charAt(i));

        // If the character is 1
        else if (s.charAt(i) == '1')

            // Pop the top element
            st.pop();

        // Otherwise
        else

            // Push the character
            // to the stack
            st.push(s.charAt(i));
    }

    // Initialize length
    int ans = 0;

    // Append the characters
    // from top to bottom
    Vector<Character> finalStr = new Vector<Character>();

    // Until Stack is empty
    while (st.size() > 0)
    {
        ans++;
        finalStr.add(st.peek());
        st.pop();
    }

    // Print the final string size
    System.out.println("Length = " + ans);

    // If length of the string is not 0
    if (ans != 0)
    {

        // Print the string
        System.out.print("String = ");

        for(int i = 0; i < ans; i++)
            System.out.print(finalStr.get(i));
    }
}

// Driver Code
public static void main(String args[])
{

    // Given string
    String S = "101010";

    // String length
    int N = S.length();

    // Function call
    findMinLength(S, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program for the above approach

from collections import deque

# Function to find minimum length
# of the given string
def findMinLength(s, n):

    # Initialize a stack
    st = deque()

    # Traverse the string from
    # left to right
    for i in range(n):

        # If the stack is empty,
        # push the character
        if (len(st) == 0):
            st.append(s[i])

        # If the character
        # is B, pop from stack
        elif (s[i] == '1'):
            st.pop()

        # Otherwise, push the
        # character to the stack
        else:
            st.append(s[i])

    # Stores resultant string
    ans = 0
    finalStr = []
    while (len(st) > 0):
        ans += 1
        finalStr.append(st[-1]);
        st.pop()

    # Print the final string size
    print("The final string size is: ", ans)

    # If length is not 0
    if (ans == 0):
        print("The final string is: EMPTY")

    # Print the string
    else:
        print("The final string is: ", *finalStr)

# Driver Code
if __name__ == '__main__':

    # Given string
    s = "0010110"

    # String length
    n = 7

    # Function Call
    findMinLength(s, n)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find minimum
// length of the given string
static void findMinLength(String s, int n)
{

    // Initialize a stack
    Stack<char> st = new Stack<char>(); 

    // Traverse the string
    for(int i = 0; i < n; i++)
    {

        // If the stack is empty
        if (st.Count == 0)

            // Push the character
            st.Push(s[i]);

        // If the character is 1
        else if (s[i] == '1')

            // Pop the top element
            st.Pop();

        // Otherwise
        else

            // Push the character
            // to the stack
            st.Push(s[i]);
    }

    // Initialize length
    int ans = 0;

    // Append the characters
    // from top to bottom
    List<char> finalStr = new List<char>();

    // Until Stack is empty
    while (st.Count > 0)
    {
        ans++;
        finalStr.Add(st.Peek());
        st.Pop();
    }

    // Print the readonly string size
    Console.WriteLine("Length = " + ans);

    // If length of the string is not 0
    if (ans != 0)
    {

        // Print the string
        Console.Write("String = ");

        for(int i = 0; i < ans; i++)
            Console.Write(finalStr[i]);
    }
}

// Driver Code
public static void Main(String []args)
{

    // Given string
    String S = "101010";

    // String length
    int N = S.Length;

    // Function call
    findMinLength(S, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find minimum
// length of the given string
function findMinLength(s, n)
{
    // Initialize a stack
    var st = [];

    // Traverse the string
    for (var i = 0; i < n; i++) {

        // If the stack is empty
        if (st.length==0)

            // Push the character
            st.push(s[i]);

        // If the character is 1
        else if (s[i] == '1')

            // Pop the top element
            st.pop();

        // Otherwise
        else
            // Push the character
            // to the stack
            st.push(s[i]);
    }

    // Initialize length
    var ans = 0;

    // Append the characters
    // from top to bottom
    var finalStr = [];

    // Until Stack is empty
    while (st.length!=0) {
        ans++;
        finalStr.push(st[st.length-1]);
        st.pop();
    }

    // Print the final string size
    document.write( "Length = " + ans);

    // If length of the string is not 0
    if (ans != 0) {

        // Print the string
        document.write( "<br>String = ");
        for(var i = 0; i < ans; i++)
            document.write( finalStr[i]);
    }
}

// Driver Code

// Given string
var S = "101010";

// String length
var N = S.length;

// Function call
findMinLength(S, N);

</script>
```

**Output:** 

```
Length = 2
String = 01
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
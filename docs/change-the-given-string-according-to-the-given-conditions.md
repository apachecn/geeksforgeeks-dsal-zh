# 根据给定的条件改变给定的字符串

> 原文:[https://www . geesforgeks . org/根据给定条件更改给定字符串/](https://www.geeksforgeeks.org/change-the-given-string-according-to-the-given-conditions/)

给定一个字符串 **S，**任务是更改字符串 id，它不遵循下面给出的任何规则，并打印更新后的字符串。校对的规则是:

1.  如果有三个连续的字符，那么它是一个错误的拼写。删除其中一个字符。**比如**弦**“ooops”**可以改成**“哎呀”**。
2.  如果两对相同的字符(AABB)连接在一起，这是一个错误的拼写。删除第二对字符中的一个。**比如**串**“你好”**可以改成**“你好”**。
3.  规则遵循从左到右的优先级。

**示例:**

> **输入:** S =【你好】
> T3】输出:你好
> **解释:**
> 按照规则#2
> 你好= >你好
> 
> **输入:**S = " wooow "
> **输出:** woow
> **解释:**
> 根据规则# 2
> wooow =>woow
> 根据规则# 1
> woow =>woow

**方法:**思路是遍历字符串，如果有拼写错误，根据给定的条件去掉多余的字符。由于错误的优先级是从左到右，根据给定的规则，可以看出对拼写错误的判断不会冲突。考虑从左向右遍历，将已经合法的字符添加到结果中。以下是步骤:

*   初始化一个[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)来存储字符并比较字符串的最后一个字符。
*   遍历字符串并将字符添加到堆栈中。
*   检查堆栈的最后 3 个字符，如果相同，则弹出堆栈顶部的字符。
*   检查堆栈的最后 4 个字符，如果相同，则弹出堆栈顶部的字符。
*   最后，返回堆栈的字符。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to proofread the spells
string proofreadSpell(string& str)
{
    vector<char> result;

    // Loop to iterate over the
    // characters of the string
    for (char c : str) {

        // Push the current character c
        // in the stack
        result.push_back(c);

        int n = result.size();

        // Check for Rule 1
        if (n >= 3) {
            if (result[n - 1]
                    == result[n - 2]
                && result[n - 1]
                       == result[n - 3]) {
                result.pop_back();
            }
        }
        n = result.size();

        // Check for Rule 2
        if (n >= 4) {
            if (result[n - 1]
                    == result[n - 2]
                && result[n - 3]
                       == result[n - 4]) {
                result.pop_back();
            }
        }
    }

    // To store the resultant string
    string resultStr = "";

    // Loop to iterate over the
    // characters of stack
    for (char c : result) {
        resultStr += c;
    }

    // Return the resultant string
    return resultStr;
}

// Driver Code
int main()
{
    // Given string str
    string str = "hello";

    // Function Call
    cout << proofreadSpell(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to proofread the spells
public static String proofreadSpell(String str)
{
    Vector<Character> result = new Vector<Character>();

    // Loop to iterate over the
    // characters of the string
    for(int i = 0; i < str.length(); i++)
    {

        // Push the current character c
        // in the stack
        result.add(str.charAt(i));

        int n = result.size();

        // Check for Rule 1
        if (n >= 3)
        {
            if (result.get(n - 1) ==
                result.get(n - 2) &&
                result.get(n - 1) ==
                result.get(n - 3))
            {
                result.remove(result.size() - 1);
            }
        }
        n = result.size();

        // Check for Rule 2
        if (n >= 4)
        {
            if (result.get(n - 1) ==
                result.get(n - 2) &&
                result.get(n - 3) ==
                result.get(n - 4))
            {
                result.remove(result.size() - 1);
            }
        }
    }

    // To store the resultant string
    String resultStr = "";

    // Loop to iterate over the
    // characters of stack
    for(Character c : result)
    {
        resultStr += c;
    }

    // Return the resultant string
    return resultStr;
}

// Driver Code
public static void main(String[] args)
{

    // Given string str
    String str = "hello";

    // Function call
    System.out.println(proofreadSpell(str));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to proofread
# the spells
def proofreadSpell(str):

    result = []

    # Loop to iterate over the
    # characters of the string
    for c in str:

        # Push the current character c
        # in the stack
        result.append(c)
        n = len(result)

        # Check for Rule 1
        if(n >= 3):
            if(result[n - 1] == result[n - 2] and
               result[n - 1] == result[n - 3]):
                result.pop()
        n = len(result)

        # Check for Rule 2
        if(n >= 4):
            if(result[n - 1] == result[n - 2] and
               result[n - 3] == result[n - 4]):
                result.pop()

    # To store the
    # resultant string
    resultStr = ""

    # Loop to iterate over the
    # characters of stack
    for c in result:
        resultStr += c

    # Return the resultant string
    return resultStr

# Driver Code

# Given string str
str = "hello"

# Function Call
print(proofreadSpell(str))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach 
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to proofread the spells
static string proofreadSpell(string str)
{

    // ArrayList result=new ArrayList();
    List<char> result = new List<char>();

    // Loop to iterate over the
    // characters of the string
    foreach(char c in str)
    {

        // Push the current character c
        // in the stack
        result.Add(c);

        int n = result.Count;

        // Check for Rule 1
        if (n >= 3)
        {
            if (result[n - 1] == result[n - 2] &&
                result[n - 1] == result[n - 3])
            {
                result.RemoveAt(n - 1);
            }
        }

        n = result.Count;

        // Check for Rule 2
        if (n >= 4)
        {
            if (result[n - 1] == result[n - 2] &&
                result[n - 3] == result[n - 4])
            {
                result.RemoveAt(n - 1);
            }
        }
    }

    // To store the resultant string
    string resultStr = "";

    // Loop to iterate over the
    // characters of stack
    foreach(char c in result)
    {
        resultStr += c;
    }

    // Return the resultant string
    return resultStr;
}

// Driver code
public static void Main(string[] args)
{

    // Given string str
    string str = "hello";

    // Function call
    Console.Write(proofreadSpell(str));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to proofread the spells
function proofreadSpell(str)
{
    var result = [];

    // Loop to iterate over the
    // characters of the string
    str.split('').forEach(c => {

        // Push the current character c
        // in the stack
        result.push(c);

        var n = result.length;

        // Check for Rule 1
        if (n >= 3) {
            if (result[n - 1]
                    == result[n - 2]
                && result[n - 1]
                       == result[n - 3]) {
                result.pop();
            }
        }
        n = result.length;

        // Check for Rule 2
        if (n >= 4) {
            if (result[n - 1]
                    == result[n - 2]
                && result[n - 3]
                       == result[n - 4]) {
                result.pop();
            }
        }
    });

    // To store the resultant string
    var resultStr = "";

    // Loop to iterate over the
    // characters of stack
    result.forEach(c => {

        resultStr += c;
    });

    // Return the resultant string
    return resultStr;
}

// Driver Code
// Given string str
var str = "hello";
// Function Call
document.write( proofreadSpell(str));

</script>
```

**Output:** 

```
hello
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*
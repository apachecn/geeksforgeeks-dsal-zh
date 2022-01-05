# 用给定的操作

将弦线减小到最小长度

> 原文:[https://www . geesforgeks . org/通过给定的操作将字符串减少到最小长度/](https://www.geeksforgeeks.org/reduce-the-string-to-minimum-length-with-the-given-operation/)

给定一个由小写和大写字符组成的字符串 **str** ，任务是在执行任意次数的给定操作后，找到该字符串可以缩减到的最小可能长度。在单个操作中，如果任意两个连续的字符在不同的情况下代表相同的字符，则可以删除它们，即**【aA】**和**【Cc】**可以删除，但**【Cc】**和**【EE】**不能删除。
**举例:**

> **输入:**str = " ASbBsd "
> T3】输出: 2
> 操作 1:“AS**bB**SD”->“ASsd”
> 操作 2:“A**Ss**d”->“Ad”
> 字符串无法进一步缩小。
> **输入:** str = "阿萨达"
> **输出:** 1
> 操作 1:“A**sS**AddA”->“Adda”
> 操作 2:“**Aa**Dda”->“Dda”
> 操作 3:“**Dd**A->A”

**进场:**

*   创建一个[栈](https://www.geeksforgeeks.org/stack-data-structure/)来存储字符串的字符。
*   对于从第一个字符开始的字符串的每个字符，如果堆栈为空，则推入堆栈中的当前字符。
*   否则，将当前字符与堆栈顶部匹配，如果它们只是大小写不同，则从堆栈中弹出元素并继续。
*   如果它们不相等，则将当前元素推入堆栈，并对字符串的其余部分重复上述步骤。
*   堆栈的大小最终是必需的答案。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// possible length str can be reduced
// to with the given operation
int minLength(string str, int len)
{

    // Stack to store the characters
    // of the given string
    stack<char> s;

    // For every character of the string
    for (int i = 0; i < len; i++) {

        // If the stack is empty then push the
        // current character in the stack
        if (s.empty()) {
            s.push(str[i]);
        }
        else {

            // Get the top character
            char c = s.top();

            // If the top element is not equal
            // to the current element and it
            // only differs in the case
            if (c != str[i]
                && toupper(c) == toupper(str[i])) {

                // Pop the top element from stack
                s.pop();
            }

            // Else push the current element
            else {
                s.push(str[i]);
            }
        }
    }

    return s.size();
}

// Driver code
int main()
{
    string str = "ASbBsd";
    int len = str.length();

    cout << minLength(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the minimum
// possible length str can be reduced
// to with the given operation
static int minLength(String str, int len)
{

    // Stack to store the characters
    // of the given string
    Stack<Character> s = new Stack<Character>();

    // For every character of the string
    for (int i = 0; i < len; i++)
    {

        // If the stack is empty then push the
        // current character in the stack
        if (s.empty())
        {
            s.push(str.charAt(i));
        }
        else
        {

            // Get the top character
            char c = s.peek();

            // If the top element is not equal
            // to the current element and it
            // only differs in the case
            if (c != str.charAt(i) &&
                Character.toUpperCase(c) ==
                Character.toUpperCase((str.charAt(i))))
            {

                // Pop the top element from stack
                s.pop();
            }

            // Else push the current element
            else
            {
                s.push(str.charAt(i));
            }
        }
    }
    return s.size();
}

// Driver code
public static void main(String []args)
{
    String str = "ASbBsd";
    int len = str.length();

    System.out.println(minLength(str, len));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# possible length str can be reduced
# to with the given operation
def minLength(string, l) :

    # Stack to store the characters
    # of the given string
    s = [];

    # For every character of the string
    for i in range(l) :

        # If the stack is empty then push the
        # current character in the stack
        if (len(s) == 0) :
            s.append(string[i]);

        else :

            # Get the top character
            c = s[-1];

            # If the top element is not equal
            # to the current element and it
            # only differs in the case
            if (c != string[i] and
                c.upper() == string[i].upper()) :

                # Pop the top element from stack
                s.pop();

            # Else push the current element
            else :
                s.append(string[i]);

    return len(s);

# Driver code
if __name__ == "__main__" :

    string = "ASbBsd";
    l = len(string);

    print(minLength(string, l));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the minimum
// possible length str can be reduced
// to with the given operation
static int minLength(String str, int len)
{

    // Stack to store the characters
    // of the given string
    Stack<char> s = new Stack<char>();

    // For every character of the string
    for (int i = 0; i < len; i++)
    {

        // If the stack is empty then push the
        // current character in the stack
        if (s.Count==0)
        {
            s.Push(str[i]);
        }
        else
        {

            // Get the top character
            char c = s.Peek();

            // If the top element is not equal
            // to the current element and it
            // only differs in the case
            if (c != str[i] &&
                char.ToUpper(c) ==
                char.ToUpper((str[i])))
            {

                // Pop the top element from stack
                s.Pop();
            }

            // Else push the current element
            else
            {
                s.Push(str[i]);
            }
        }
    }
    return s.Count;
}

// Driver code
public static void Main(String []args)
{
    String str = "ASbBsd";
    int len = str.Length;

    Console.WriteLine(minLength(str, len));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the minimum
    // possible length str can be reduced
    // to with the given operation
    function minLength(str, len)
    {

        // Stack to store the characters
        // of the given string
        let s = [];

        // For every character of the string
        for (let i = 0; i < len; i++)
        {

            // If the stack is empty then push the
            // current character in the stack
            if (s.length==0)
            {
                s.push(str[i]);
            }
            else
            {

                // Get the top character
                let c = s[s.length - 1];

                // If the top element is not equal
                // to the current element and it
                // only differs in the case
                if (c != str[i] &&
                    c.toUpperCase() ==
                    str[i].toUpperCase())
                {

                    // Pop the top element from stack
                    s.pop();
                }

                // Else push the current element
                else
                {
                    s.push(str[i]);
                }
            }
        }
        return s.length;
    }

    let str = "ASbBsd";
    let len = str.length;

    document.write(minLength(str, len));

</script>
```

**Output:** 

```
2
```

**时间复杂度** : O(N)。
**辅助空间** : O(N)。
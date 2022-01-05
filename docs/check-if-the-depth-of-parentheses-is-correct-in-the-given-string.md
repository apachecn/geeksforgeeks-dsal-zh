# 检查给定字符串中括号的深度是否正确

> 原文:[https://www . geesforgeks . org/check-如果括号深度在给定字符串中是正确的/](https://www.geeksforgeeks.org/check-if-the-depth-of-parentheses-is-correct-in-the-given-string/)

给定一个由左圆括号、右圆括号和整数组成的字符串 **S** ，如果在这个字符串中，整数正确地指示了它的深度，那么任务就是打印 Yes。深度是指围绕该整数的嵌套括号集的数量。否则打印否。
**例:**

> **输入:**S =((2)((3)))”
> **输出:**是
> **输入:**
> 开&圆括号数 2 = 2
> 开&圆括号数 3 = 3
> **输入:**S =((35)(2))”
> **输出:**否
> **输入:**

**进场:**

1.  逐个字符地迭代字符串
2.  如果是左括号或右括号，则追加到数组中 **arr[]**
3.  如果字符是数字，则迭代直到整个数字被读取，然后追加到 **arr[]** 中
4.  逐元素迭代数组 **arr[]**
    *   如果元素是'('增加深度并打开 1
    *   如果元素为')'，则深度减 1，接近深度增 1
    *   如果元素是整数，检查“整数！=深度”，如果为真
        将标志设置为 0 并中断循环
5.  迭代整个字符串后，检查 open 是否不等于 close，如果 true，则设置 flag = 0

以下是上述方法的实施

## C++

```
// Function to check if the Depth
// of Parentheses is correct
// in the given String

#include <bits/stdc++.h>
using namespace std;

bool Formatted(string s)
{
    vector<char> k;
    int i = 0;

    while (i < s.size())
    {
        // Appending if the
        // Character is not integer
        if (s[i]==')' or s[i]=='(')
        {
            k.push_back(s[i]);
            i += 1;
        }
        else
        {
            // Iterating till the entire
            // Digit is read
            char st;
            while (s[i]!=')' and s[i]!=')')
            {
                st = s[i];
                i = i + 1;
            }
            k.push_back(st);
        }
    }

    int depth = 0, flag = 1;
    int open = 0, close = 0;

    for (char i:k)
    {

        // Check if character is '('
        if (i == '(')
        {
            // Increment depth by 1
            depth += 1;

            // Increment open by 1
            open += 1;

        // Check if character is ')'
    }else if (i == ')'){

            // Decrement depth by 1
            depth -= 1;

            // Increment close by 1
            close += 1;
        }
        else{
            if (i-'0' != depth){
                flag = 0;
                break;
            }
        }
    }

    // Check if open parentheses
    // NOT equals close parentheses
    if (open != close)
        flag = 0;

    return (flag == 1)?true:false;
}

// Driver Code
int main()
{
    string s = "((2)((3)))";
    bool k = Formatted(s);
    if (k == true)
        printf("Yes");
    else
        printf("No");
    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Function to check if the Depth
// of Parentheses is correct
// in the given String
import java.util.*;

class GFG{

static boolean Formatted(String s)
{
    Vector<Character> k = new Vector<Character>();
    int i = 0;

    while (i < s.length())
    {
        // Appending if the
        // Character is not integer
        if (s.charAt(i)==')' || s.charAt(i)=='(')
        {
            k.add(s.charAt(i));
            i += 1;
        }
        else
        {
            // Iterating till the entire
            // Digit is read
            char st = 0;
            while (s.charAt(i)!=')' && s.charAt(i)!=')')
            {
                st = s.charAt(i);
                i = i + 1;
            }
            k.add(st);
        }
    }

    int depth = 0, flag = 1;
    int open = 0, close = 0;

    for (char i2 : k)
    {

        // Check if character is '('
        if (i2 == '(')
        {
            // Increment depth by 1
            depth += 1;

            // Increment open by 1
            open += 1;

        // Check if character is ')'
    }else if (i2 == ')'){

            // Decrement depth by 1
            depth -= 1;

            // Increment close by 1
            close += 1;
        }
        else{
            if (i2-'0' != depth){
                flag = 0;
                break;
            }
        }
    }

    // Check if open parentheses
    // NOT equals close parentheses
    if (open != close)
        flag = 0;

    return (flag == 1)?true:false;
}

// Driver Code
public static void main(String[] args)
{
    String s = "((2)((3)))";
    boolean k = Formatted(s);
    if (k == true)
        System.out.printf("Yes");
    else
        System.out.printf("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Function to check if the Depth
# of Parentheses is correct
# in the given String

def Formatted(s):
    k = []
    i = 0

    while i < len(s):

        # Appending if the
        # Character is not integer
        if s[i].isdigit() == False:

            k.append(s[i])
            i += 1
        else:

            # Iterating till the entire
            # Digit is read
            st = ""
            while s[i].isdigit():
                st += s[i]
                i = i + 1
            k.append(int(st))

    depth, flag = 0, 1
    open, close = 0, 0

    for i in k:

        # Check if character is '('
        if i == '(':

            # Increment depth by 1
            depth += 1

            # Increment open by 1
            open += 1

        # Check if character is ')'
        elif i == ')':

            # Decrement depth by 1
            depth -= 1

            # Increment close by 1
            close += 1
        else:
            if i != depth:
                flag = 0
                break

    # Check if open parentheses
    # NOT equals close parentheses
    if open != close:
        flag = 0

    return True if flag == 1 else False

# Driver Code
if __name__ == '__main__':
    s = '((2)((3)))'
    k = Formatted(s)
    if k == True:
        print("Yes")
    else:
        print("No")
```

## C#

```
// Function to check if the Depth
// of Parentheses is correct
// in the given String
using System;
using System.Collections.Generic;

class GFG
{

static bool Formatted(String s)
{
    List<char> k = new List<char>();
    int i = 0;

    while (i < s.Length)
    {
        // Appending if the
        // char is not integer
        if (s[i]==')' || s[i]=='(')
        {
            k.Add(s[i]);
            i += 1;
        }
        else
        {
            // Iterating till the entire
            // Digit is read
            char st = '\x0000';
            while (s[i] != ')' && s[i] != ')')
            {
                st = s[i];
                i = i + 1;
            }
            k.Add(st);
        }
    }

    int depth = 0, flag = 1;
    int open = 0, close = 0;

    foreach (char i2 in k)
    {

        // Check if character is '('
        if (i2 == '(')
        {
            // Increment depth by 1
            depth += 1;

            // Increment open by 1
            open += 1;

        // Check if character is ')'
    }else if (i2 == ')'){

            // Decrement depth by 1
            depth -= 1;

            // Increment close by 1
            close += 1;
        }
        else{
            if (i2-'0' != depth){
                flag = 0;
                break;
            }
        }
    }

    // Check if open parentheses
    // NOT equals close parentheses
    if (open != close)
        flag = 0;

    return (flag == 1)?true:false;
}

// Driver Code
public static void Main(String[] args)
{
    String s = "((2)((3)))";
    bool k = Formatted(s);
    if (k == true)
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Function to check if the Depth
// of Parentheses is correct
// in the given String
function Formatted(s)
{
    let k = [];
    let i = 0;

    while (i < s.length)
    {
        // Appending if the
        // Character is not integer
        if (s[i]==')' || s[i]=='(')
        {
            k.push(s[i]);
            i += 1;
        }
        else
        {
            // Iterating till the entire
            // Digit is read
            let st = 0;
            while (s[i]!=')' && s[i]!=')')
            {
                st = s[i];
                i = i + 1;
            }
            k.push(st);
        }
    }

    let depth = 0, flag = 1;
    let open = 0, close = 0;

    for (let i2=0;i2< k.length;i2++)
    {

        // Check if character is '('
        if (k[i2] == '(')
        {
            // Increment depth by 1
            depth += 1;

            // Increment open by 1
            open += 1;

        // Check if character is ')'
    }else if (k[i2] == ')'){

            // Decrement depth by 1
            depth -= 1;

            // Increment close by 1
            close += 1;
        }
        else{
            if (k[i2]-'0' != depth){
                flag = 0;
                break;
            }
        }
    }

    // Check if open parentheses
    // NOT equals close parentheses
    if (open != close)
        flag = 0;

    return (flag == 1)?true:false;
}

// Driver Code
let s = "((2)((3)))";
let k = Formatted(s);
if (k == true)
    document.write("Yes");
else
    document.write("No");

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Yes
```
# 使用堆栈对字符串进行排序

> 原文:[https://www . geesforgeks . org/sort-字符串-使用-stack/](https://www.geeksforgeeks.org/sort-string-of-characters-using-stack/)

给定一串字符。任务是编写一个程序，使用 stack 按排序顺序打印这个字符串的字符。

**示例:**

```
Input: str = "geeksforgeeks" 
Output: eeeefggkkorss

Input: str = "hello395world216"
Output: 123569dehllloorw
```

**进场:**

*   初始化两个栈，一个**栈**，另一个**临时栈**。
*   在**栈**中插入字符串的第一个字符。
*   迭代字符串中的所有字符
    1.  如果第 i <sup>个</sup>字符大于或等于堆栈的顶部元素，则推送该元素。
    2.  如果第 i <sup>个</sup>字符不大于，则将**栈**的所有元素推入 **tempstack** ，然后将该字符推入**栈**。之后，将 **tempstack** 的所有大元素推至 **stack** 。

迭代完成后，以相反的顺序打印**栈**的所有元素。

下面是上述方法的实现:

## C++

```
// C++ program to sort string of
// characters using stack 
#include <bits/stdc++.h>
using namespace std;

// Function to print the characters 
// in sorted order 
void printSorted(string s, int l)
{

    // Primary stack
    stack<char> Stack; 

    // Secondary stack
    stack<char> tempstack; 

    // Append first character  
    Stack.push(s[0]);

    // Iterate for all character in string 
    for(int i = 1; i < l; i++)
    {

        // i-th character ASCII 
        int a = s[i];

        // stack's top element ASCII 
        int b = Stack.top(); 

        // If greater or equal to top element 
        // then push to stack 
        if ((a - b) >= 1 or (a == b))
            Stack.push(s[i]); 

        // If smaller, then push all element 
        // to the temporary stack 
        else if ((b - a) >= 1)
        {

            // Push all greater elements 
            while ((b - a) >= 1)
            {

                // Push operation 
                tempstack.push(Stack.top());
                Stack.pop();

                // Push till the stack is not-empty 
                if (Stack.size() > 0)
                    b = Stack.top();
                else
                    break;
            }

            // Push the i-th character 
            Stack.push(s[i]);

            // Push the tempstack back to stack 
            while (tempstack.size() > 0)
            {
                Stack.push(tempstack.top());
                tempstack.pop();
            }
        }
    }

    // Print the stack in reverse order
    string answer;
    while (Stack.size() > 0)
    {
        answer = Stack.top() + answer;
        Stack.pop();
    }
    cout << answer << endl;
}

// Driver Code   
int main()
{
    string s = "geeksforgeeks";
    int l = s.length();

    printSorted(s, l);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort string of
// characters using stack 
import java.io.*;
import java.util.*;

class GFG{

// Function to print the characters 
// in sorted order
public static void printSorted(String s,int l)
{

    // Primary stack
    Stack<Character> stack = new Stack<Character>();

    // Secondary stack
    Stack<Character> tempstack  = new Stack<Character>();

    // Append first character  
    stack.push(s.charAt(0));

    // Iterate for all character in string 
    for(int i = 1; i < l; i++)
    {

        // i-th character ASCII 
        int a = s.charAt(i);

        // Stack's top element ASCII 
        int b = (int)((char)stack.peek());

        // If greater or equal to top element 
        // then push to stack 
        if ((a - b) >= 1 || (a == b))
        {
            stack.push(s.charAt(i));
        }

        // If smaller, then push all element 
        // to the temporary stack
        else if ((b - a) >= 1)
        {

            // Push all greater elements 
            while ((b - a) >= 1)
            {

                // Push operation 
                tempstack.push(stack.peek());
                stack.pop();

                // Push till the stack is not-empty 
                if (stack.size() > 0)
                {
                    b = (int)((char)stack.peek());
                }
                else
                {
                    break;
                }
            }

            // Push the i-th character 
            stack.push(s.charAt(i));

            // Push the tempstack back to stack 
            while (tempstack.size() > 0)
            {
                stack.push(tempstack.peek());
                tempstack.pop();
            }
        }
    }

    // Print the stack in reverse order
    String answer = "";
    while (stack.size() > 0)
    {
        answer = stack.peek()+answer;
        stack.pop();
    }
    System.out.println(answer);
}

// Driver Code
public static void main(String []args)
{
    String s = "geeksforgeeks";
    int l = s.length();

    printSorted(s, l);
}
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program to sort
# string of characters using stack

# function to print the characters
# in sorted order
def printSorted(s, l):

    # primary stack
    stack =[]

    # secondary stack
    tempstack =[]

    # append first character 
    stack.append(s[0])

    # iterate for all character in string
    for i in range(1, l):

        # i-th character ASCII
        a = ord(s[i])

        # stack's top element ASCII
        b = ord(stack[-1])

        # if greater or equal to top element
        # then push to stack
        if((a-b)>= 1 or (a == b)):
            stack.append(s[i])

        # if smaller, then push all element
        # to the temporary stack
        elif((b-a)>= 1):

            # push all greater elements
            while((b-a)>= 1):

                # push operation
                tempstack.append(stack.pop())

                # push till the stack is not-empty
                if(len(stack)>0):
                    b = ord(stack[-1])
                else:
                    break

            # push the i-th character
            stack.append(s[i])

            # push the tempstack back to stack
            while(len(tempstack)>0):
                stack.append(tempstack.pop())

    # print the stack in reverse order
    print(''.join(stack))

# Driver Code
s = "geeksforgeeks"
l = len(s)
printSorted(s, l)
```

## C#

```
// C# program to sort string of
// characters using stack 
using System;
using System.Collections;
class GFG {

    // Function to print the characters 
    // in sorted order 
    static void printSorted(string s, int l)
    {

        // Primary stack
        Stack stack = new Stack();

        // Secondary stack
        Stack tempstack = new Stack();

        // Append first character  
        stack.Push(s[0]);

        // Iterate for all character in string 
        for(int i = 1; i < l; i++)
        {

            // i-th character ASCII 
            int a = s[i];

            // stack's top element ASCII 
            int b = (int)((char)stack.Peek()); 

            // If greater or equal to top element 
            // then push to stack 
            if ((a - b) >= 1 || (a == b))
                stack.Push(s[i]); 

            // If smaller, then push all element 
            // to the temporary stack 
            else if ((b - a) >= 1)
            {

                // Push all greater elements 
                while ((b - a) >= 1)
                {

                    // Push operation 
                    tempstack.Push(stack.Peek());
                    stack.Pop();

                    // Push till the stack is not-empty 
                    if (stack.Count > 0)
                        b = (int)((char)stack.Peek());
                    else
                        break;
                }

                // Push the i-th character 
                stack.Push(s[i]);

                // Push the tempstack back to stack 
                while (tempstack.Count > 0)
                {
                    stack.Push(tempstack.Peek());
                    tempstack.Pop();
                }
            }
        }

        // Print the stack in reverse order
        string answer = "";
        while (stack.Count > 0)
        {
            answer = stack.Peek() + answer;
            stack.Pop();
        }
        Console.WriteLine(answer);
    }

  static void Main() {
    string s = "geeksforgeeks";
    int l = s.Length;

    printSorted(s, l);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// JavaScript program to sort string of
// characters using stack 

// Function to print the characters 
// in sorted order 
function printSorted(s, l)
{

    // Primary stack
    var Stack = []; 

    // Secondary stack
    var tempstack = []; 

    // Append first character  
    Stack.push(s[0].charCodeAt(0));

    // Iterate for all character in string 
    for(var i = 1; i < l; i++)
    {

        // i-th character ASCII 
        var a = s[i].charCodeAt(0);

        // stack's top element ASCII 
        var b = Stack[Stack.length-1]; 

        // If greater or equal to top element 
        // then push to stack 
        if ((a - b) >= 1 || (a == b))
            Stack.push(s[i].charCodeAt(0)); 

        // If smaller, then push all element 
        // to the temporary stack 
        else if ((b - a) >= 1)
        {

            // Push all greater elements 
            while ((b - a) >= 1)
            {

                // Push operation 
                tempstack.push(Stack[Stack.length-1]);
                Stack.pop();

                // Push till the stack is not-empty 
                if (Stack.length > 0)
                    b = Stack[Stack.length-1];
                else
                    break;
            }

            // Push the i-th character 
            Stack.push(s[i].charCodeAt(0));

            // Push the tempstack back to stack 
            while (tempstack.length > 0)
            {
                Stack.push(tempstack[tempstack.length-1]);
                tempstack.pop();
            }
        }
    }

    // Print the stack in reverse order
    var answer = "";
    while (Stack.length > 0)
    {
        answer = String.fromCharCode(Stack[Stack.length-1]) + answer;
        Stack.pop();
    }
    document.write( answer)
}

// Driver Code   
var s = "geeksforgeeks";
var l = s.length;

printSorted(s, l);

</script>
```

**Output:** 

```
eeeefggkkorss
```

在这篇文章
中已经实现了一种使用散列法的有效方法
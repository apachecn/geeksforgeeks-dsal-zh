# Sudo 放置【1.3】|堆叠设计

> 原文:[https://www . geesforgeks . org/sudo-placement 1-3-stack-design/](https://www.geeksforgeeks.org/sudo-placement1-3-stack-design/)

给定 q 个查询，您需要在堆栈上执行操作。查询有三种类型 1、2 和 3。如果操作是推送(1)，则推送元素，如果操作是弹出(2)，则弹出元素，如果是 Top (3)，则在堆栈顶部打印元素(如果堆栈为空，则打印“-1”，不带引号)。
**例:**

```
Input: Queries =  6
                  3
                  1 5
                  1 6
                  1 7
                  2
                  3
Output: -1
         6 
The first query is to print top, but since the stack is empty, so we print -1.
Next three queries are to push 5, 6, and 7, so we pushed them on a stack. 
Next query is pop, so we popped 7 from a stack. Final query is to print the
top, so 6 is there at the top and thus printed.
```

**方法:** [堆栈](https://www.geeksforgeeks.org/stack-data-structure/)可用于执行给定的操作。如果一个查询的输入是 1，那么接受另一个输入，并使用 [push()](https://www.geeksforgeeks.org/stackpush-stackpop-c-stl/) 函数将元素推入堆栈。如果查询的输入是 2，那么在堆栈中使用[pop()](https://www.geeksforgeeks.org/stackpush-stackpop-c-stl/)函数弹出元素。如果查询输入为 3，则使用[top()](https://www.geeksforgeeks.org/stack-top-c-stl/)功能打印顶部元素。
以下是上述方法的实施:

## C++

```
// C++ program for
// Sudo-Placement | Stack Design
#include <bits/stdc++.h>
using namespace std;

stack<int> s;

// function to perform type-1 operation
void _push(int n)
{
    s.push(n);
}

// function to perform type-2 operation
void _pop()
{
    s.pop();
}

// function to perform type-3 operation
void print()
{
    // if the stack is not empty
    if (!s.empty())
        cout << s.top() << endl;
    else
        cout << -1 << endl;
}

// Driver Code
int main()
{
    // 1st query
    print();
    // 2nd query
    _push(5);

    // 3rd query
    _push(6);

    // 4th query
    _push(7);

    // 5th query
    _pop();

    // 6th query
    print();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
// Java program for
// Sudo-Placement | Stack Design

class GFG
{

    static Stack<Integer> s = new Stack<>();

    // function to perform type-1 operation
    static void _push(int n)
    {
        s.push(n);
    }

    // function to perform type-2 operation
    static void _pop()
    {
        s.pop();
    }

    // function to perform type-3 operation
    static void print()
    {

        // if the stack is not empty
        if (!s.empty())
        {
            System.out.println(s.peek());
        }
        else
        {
            System.out.println(-1);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // 1st query
        print();
        // 2nd query
        _push(5);

        // 3rd query
        _push(6);

        // 4th query
        _push(7);

        // 5th query
        _pop();

        // 6th query
        print();
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for
# Sudo-Placement | Stack Design
s = [];

# function to perform
# type-1 operation
def _push(n):
    s.append(n);

# function to perform
# type-2 operation
def _pop():
    s.pop();

# function to perform
# type-3 operation
def _print():

    # if the stack is not
    # empty
    if (len(s) > 0):
        print(s[len(s) - 1]);
    else:
        print("-1");

# Driver Code
if __name__ == '__main__':

    # 1st query
    _print();

    # 2nd query
    _push(5);

    # 3rd query
    _push(6);

    # 4th query
    _push(7);

    # 5th query
    _pop();

    # 6th query
    _print();

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for
// Sudo-Placement | Stack Design
using System;
using System.Collections.Generic;

class GFG
{

    static Stack<int> s = new Stack<int>();

    // function to perform type-1 operation
    static void _push(int n)
    {
        s.Push(n);
    }

    // function to perform type-2 operation
    static void _pop()
    {
        s.Pop();
    }

    // function to perform type-3 operation
    static void print()
    {

        // if the stack is not empty
        if (s.Count != 0)
        {
            Console.WriteLine(s.Peek());
        }
        else
        {
            Console.WriteLine(-1);
        }
    }

    // Driver Code
    public static void Main()
    {
        // 1st query
        print();
        // 2nd query
        _push(5);

        // 3rd query
        _push(6);

        // 4th query
        _push(7);

        // 5th query
        _pop();

        // 6th query
        print();
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// Javascript program for
// Sudo-Placement | Stack Design

let s=[];

 // function to perform type-1 operation
function _push(n)
{
    s.push(n);
}

// function to perform type-2 operation
function _pop()
{
    s.pop();
}

// function to perform type-3 operation
function  print()
{
    // if the stack is not empty
        if (s.length!=0)
        {
            document.write(s[s.length-1]+"<br>");
        }
        else
        {
            document.write(-1+"<br>");
        }
}

// Driver Code

// 1st query
print();
// 2nd query
_push(5);

// 3rd query
_push(6);

// 4th query
_push(7);

// 5th query
_pop();

// 6th query
print();

// This code is contributed by rag2127
</script>
```

**Output:** 

```
-1
6
```
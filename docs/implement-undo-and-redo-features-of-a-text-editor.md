# 实现文本编辑器的撤销和重做功能

> 原文:[https://www . geesforgeks . org/implement-undo-and-redo-features-of-a-text-editor/](https://www.geeksforgeeks.org/implement-undo-and-redo-features-of-a-text-editor/)

给定一个由[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **Q[]** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，由以下类型的查询组成:

*   **“写 X”:**在文档中写一个字符 **X** 。
*   **“撤销”:**删除对文档的最后一次更改。
*   **“REDO”:**恢复对文档执行的最近的**撤销**操作。
*   **“READ”:**读取并打印文档内容。

**示例:**

> **输入:**Q = {“WRITE A”、“WRITE B”、“WRITE C”、“UNDO”、“READ”、“REDO”、“READ”}
> **输出:** AB ABC
> **解释:**
> 对文档执行“WRITE A”。因此，该文档只包含“A”。
> 对文档执行“写 B”。因此，该文档包含“AB”。
> 对文档执行“写 C”。因此，该文件包含“作业成本法”。
> 对文档执行“撤销”。因此，该文档包含“AB”。
> 打印文档内容，即“AB”
> 对文档执行“REDO”。因此，该文件包含“作业成本法”。
> 打印文档内容，即“ABC”
> 
> **输入:**Q = {“WRITE x”、“WRITE y”、“UNDO”、“WRITE z”、“READ”、“REDO”、“READ”}
> **输出:** xz xzy

**方法:**使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)可以解决问题。按照以下步骤解决问题:

*   初始化两个栈，说**撤销**和**重做**。
*   [遍历字符串数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **Q** ，执行以下操作:
*   如果遇到**“WRITE”**字符串，将字符推到**撤销**栈
*   如果遇到**“撤销”**字符串，从**撤销**堆栈[弹出](https://www.geeksforgeeks.org/stack-push-method-in-java/)[顶部元素，并将其推至**重做**堆栈](https://www.geeksforgeeks.org/stack-top-c-stl/)。
*   如果遇到**【重做】**弦，弹出**重做**叠[的](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)[顶元素，推入**松开**叠](https://www.geeksforgeeks.org/stack-top-c-stl/)。
*   如果遇到**“READ”**字符串，[按相反顺序打印**撤销**堆栈的所有元素](https://www.geeksforgeeks.org/print-stack-elements-from-bottom-to-top/)。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform
// "WRITE X" operation
void WRITE(stack<char>& Undo,
           char X)
{
    // Push an element to
    // the top of stack
    Undo.push(X);
}

// Function to perform
// "UNDO" operation
void UNDO(stack<char>& Undo,
          stack<char>& Redo)
{
    // Stores top element
    // of the stack
    char X = Undo.top();

    // Erase top element
    // of the stack
    Undo.pop();

    // Push an element to
    // the top of stack
    Redo.push(X);
}

// Function to perform
// "REDO" operation
void REDO(stack<char>& Undo,
          stack<char>& Redo)
{
    // Stores the top element
    // of the stack
    char X = Redo.top();

    // Erase the top element
    // of the stack
    Redo.pop();

    // Push an element to
    // the top of the stack
    Undo.push(X);
}

// Function to perform
// "READ" operation
void READ(stack<char> Undo)
{
    // Store elements of stack
    // in reverse order
    stack<char> revOrder;

    // Traverse Undo stack
    while (!Undo.empty()) {
        // Push an element to
        // the top of stack
        revOrder.push(Undo.top());

        // Erase top element
        // of stack
        Undo.pop();
    }

    while (!revOrder.empty()) {
        // Print the top element
        // of the stack
        cout << revOrder.top();
      Undo.push(revOrder.top());

        // Erase the top element
        // of the stack
        revOrder.pop();
    }

    cout << " ";
}

// Function to perform the
// queries on the document
void QUERY(vector<string> Q)
{
    // Stores the history of all
    // the queries that have been
    // processed on the document
    stack<char> Undo;

    // Stores the elements
    // of REDO query
    stack<char> Redo;

    // Stores total count
    // of queries
    int N = Q.size();

    // Traverse all the query
    for (int i = 0; i < N; i++) {
        if (Q[i] == "UNDO") {
            UNDO(Undo, Redo);
        }
        else if (Q[i] == "REDO") {
            REDO(Undo, Redo);
        }
        else if (Q[i] == "READ") {
            READ(Undo);
        }
        else {
            WRITE(Undo, Q[i][6]);
        }
    }
}

// Driver Code
int main()
{

    vector<string> Q = { "WRITE A", "WRITE B",
                         "WRITE C", "UNDO",
                         "READ", "REDO", "READ" };
    QUERY(Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the above approach
import java.util.*;
public class Main
{
    // Stores the history of all
    // the queries that have been
    // processed on the document
    static Stack<Character> Undo = new Stack<Character>();

    // Stores the elements
    // of REDO query
    static Stack<Character> Redo = new Stack<Character>();

    // Function to perform
    // "WRITE X" operation
    static void WRITE(Stack<Character> Undo, char X)
    {

        // Push an element to
        // the top of stack
        Undo.push(X);
    }

    // Function to perform
    // "UNDO" operation
    static void UNDO(Stack<Character> Undo, Stack<Character> Redo)
    {

        // Stores top element
        // of the stack
        char X = (char)Undo.peek();

        // Erase top element
        // of the stack
        Undo.pop();

        // Push an element to
        // the top of stack
        Redo.push(X);
    }

    // Function to perform
    // "REDO" operation
    static void REDO(Stack<Character> Undo, Stack<Character> Redo)
    {

        // Stores the top element
        // of the stack
        char X = (char)Redo.peek();

        // Erase the top element
        // of the stack
        Redo.pop();

        // Push an element to
        // the top of the stack
        Undo.push(X);
    }

    // Function to perform
    // "READ" operation
    static void READ(Stack<Character> Undo)
    {

        // Store elements of stack
        // in reverse order
        Stack<Character> revOrder = new Stack<Character>();

        // Traverse Undo stack
        while (Undo.size() > 0)
        {

            // Push an element to
            // the top of stack
            revOrder.push(Undo.peek());

            // Erase top element
            // of stack
            Undo.pop();
        }

        while (revOrder.size() > 0)
        {

            // Print the top element
            // of the stack
            System.out.print(revOrder.peek());
              Undo.push(revOrder.peek());

            // Erase the top element
            // of the stack
            revOrder.pop();
        }

        System.out.print(" ");
    }

    // Function to perform the
    // queries on the document
    static void QUERY(String[] Q)
    {
        // Stores total count
        // of queries
        int N = Q.length;

        // Traverse all the query
        for (int i = 0; i < N; i++)
        {
            if(Q[i] == "UNDO")
            {
                UNDO(Undo, Redo);
            }
            else if(Q[i] == "REDO")
            {
                REDO(Undo, Redo);
            }
            else if(Q[i] == "READ")
            {
                READ(Undo);
            }
            else
            {
                WRITE(Undo, Q[i].charAt(6));
            }
        }
    }

    public static void main(String[] args) {
        String[] Q = { "WRITE A", "WRITE B", "WRITE C", "UNDO", "READ", "REDO", "READ" };
        QUERY(Q);
    }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach
global Undo
global Redo

# Stores the history of all
# the queries that have been
# processed on the document
Undo = []

# Stores the elements
# of REDO query
Redo = []

# Function to perform
# "WRITE X" operation
def WRITE(Undo, X):

    # Push an element to
    # the top of stack
    Undo.append(X)

# Function to perform
# "UNDO" operation
def UNDO(Undo, Redo):

    # Stores top element
    # of the stack
    X = Undo[-1]

    # Erase top element
    # of the stack
    Undo.pop()

    # Push an element to
    # the top of stack
    Redo.append(X)

# Function to perform
# "REDO" operation
def REDO(Undo, Redo):

    # Stores the top element
    # of the stack
    X = Redo[-1]

    # Erase the top element
    # of the stack
    Redo.pop()

    # Push an element to
    # the top of the stack
    Undo.append(X)

# Function to perform
# "READ" operation
def READ(Undo):
    print(*Undo, sep = "",
          end = " ")

# Function to perform the
# queries on the document
def QUERY(Q):

    # Stores total count
    # of queries
    N = len(Q)

    # Traverse all the query
    for i in range(N):
        if(Q[i] == "UNDO"):
            UNDO(Undo, Redo)
        elif(Q[i] == "REDO"):
            REDO(Undo, Redo)
        elif(Q[i] == "READ"):
            READ(Undo)
        else:
            WRITE(Undo, Q[i][6])

# Driver Code
Q = ["WRITE A", "WRITE B", "WRITE C",
     "UNDO", "READ", "REDO", "READ"]
QUERY(Q)

#This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# Program to implement the above approach
using System;
using System.Collections;
class GFG {

    // Stores the history of all
    // the queries that have been
    // processed on the document
    static Stack Undo = new Stack();

    // Stores the elements
    // of REDO query
    static Stack Redo = new Stack();

    // Function to perform
    // "WRITE X" operation
    static void WRITE(Stack Undo, char X)
    {

        // Push an element to
        // the top of stack
        Undo.Push(X);
    }

    // Function to perform
    // "UNDO" operation
    static void UNDO(Stack Undo, Stack Redo)
    {

        // Stores top element
        // of the stack
        char X = (char)Undo.Peek();

        // Erase top element
        // of the stack
        Undo.Pop();

        // Push an element to
        // the top of stack
        Redo.Push(X);
    }

    // Function to perform
    // "REDO" operation
    static void REDO(Stack Undo, Stack Redo)
    {

        // Stores the top element
        // of the stack
        char X = (char)Redo.Peek();

        // Erase the top element
        // of the stack
        Redo.Pop();

        // Push an element to
        // the top of the stack
        Undo.Push(X);
    }

    // Function to perform
    // "READ" operation
    static void READ(Stack Undo)
    {

        // Store elements of stack
        // in reverse order
        Stack revOrder = new Stack();

        // Traverse Undo stack
        while (Undo.Count > 0)
        {

            // Push an element to
            // the top of stack
            revOrder.Push(Undo.Peek());

            // Erase top element
            // of stack
            Undo.Pop();
        }

        while (revOrder.Count > 0)
        {

            // Print the top element
            // of the stack
            Console.Write(revOrder.Peek());
              Undo.Push(revOrder.Peek());

            // Erase the top element
            // of the stack
            revOrder.Pop();
        }

        Console.Write(" ");
    }

    // Function to perform the
    // queries on the document
    static void QUERY(string[] Q)
    {
        // Stores total count
        // of queries
        int N = Q.Length;

        // Traverse all the query
        for (int i = 0; i < N; i++)
        {
            if(Q[i] == "UNDO")
            {
                UNDO(Undo, Redo);
            }
            else if(Q[i] == "REDO")
            {
                REDO(Undo, Redo);
            }
            else if(Q[i] == "READ")
            {
                READ(Undo);
            }
            else
            {
                WRITE(Undo, Q[i][6]);
            }
        }
    }

  static void Main() {
    string[] Q = { "WRITE A", "WRITE B", "WRITE C", "UNDO", "READ", "REDO", "READ" };
    QUERY(Q);
  }
}

// This code is contributed by rameshtravel07
```

## java 描述语言

```
<script>
    // Javascript Program to implement the above approach

    // Stores the history of all
    // the queries that have been
    // processed on the document
    let Undo = [];

    // Stores the elements
    // of REDO query
    let Redo = [];

    // Function to perform
    // "WRITE X" operation
    function WRITE(Undo, X)
    {

        // Push an element to
        // the top of stack
        Undo.push(X)
    }

    // Function to perform
    // "UNDO" operation
    function UNDO(Undo, Redo)
    {

        // Stores top element
        // of the stack
        let X = Undo[Undo.length - 1];

        // Erase top element
        // of the stack
        Undo.pop();

        // Push an element to
        // the top of stack
        Redo.push(X);
    }

    // Function to perform
    // "REDO" operation
    function REDO(Undo, Redo)
    {

        // Stores the top element
        // of the stack
        let X = Redo[Redo.length - 1];

        // Erase the top element
        // of the stack
        Redo.pop();

        // Push an element to
        // the top of the stack
        Undo.push(X);
    }

    // Function to perform
    // "READ" operation
    function READ(Undo)
    {

        // Store elements of stack
        // in reverse order
        let revOrder = [];

        // Traverse Undo stack
        while (Undo.length > 0)
        {

            // Push an element to
            // the top of stack
            revOrder.push(Undo[Undo.length - 1]);

            // Erase top element
            // of stack
            Undo.pop();
        }

        while (revOrder.length > 0)
        {

            // Print the top element
            // of the stack
            document.write(revOrder[revOrder.length - 1]);
              Undo.push(revOrder[revOrder.length - 1]);

            // Erase the top element
            // of the stack
            revOrder.pop();
        }

        document.write(" ");
    }

    // Function to perform the
    // queries on the document
    function QUERY(Q)
    {
        // Stores total count
        // of queries
        N = Q.length

        // Traverse all the query
        for (let i = 0; i < N; i++)
        {
            if(Q[i] == "UNDO")
            {
                UNDO(Undo, Redo);
            }
            else if(Q[i] == "REDO")
            {
                REDO(Undo, Redo);
            }
            else if(Q[i] == "READ")
            {
                READ(Undo);
            }
            else
            {
                WRITE(Undo, Q[i][6]);
            }
        }
    }

    let Q = [ "WRITE A", "WRITE B", "WRITE C", "UNDO", "READ", "REDO", "READ" ];
    QUERY(Q);

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
AB ABC
```

**时间复杂度:**
**UNDO:**O(1)
**REDO:**O(1)
**WRITE:**O(1)
**READ:**(N)，其中 N 表示 UNDO 堆栈的大小
**辅助空间:** O(N)
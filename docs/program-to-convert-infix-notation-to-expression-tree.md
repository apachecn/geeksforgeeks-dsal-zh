# 将中缀符号转换为表达式树的程序

> 原文:[https://www . geesforgeks . org/program-to-convert-infix-notification-to-expression-tree/](https://www.geeksforgeeks.org/program-to-convert-infix-notation-to-expression-tree/)

给定一个表示**中缀符号**的字符串。任务是将其转换为表达式树。
表达式树是一种二叉树，其中操作数由叶节点表示，运算符由中间节点表示。任何节点都不能有一个子节点。

**表达式树的构建**

该算法结合了**调车场**和**后缀-表达式树转换**。

考虑下面这条线:

```
((s[i]!='^' && p[stC.top()]>=p[s[i]]) || 
(s[i]=='^' && p[stC.top()]>p[s[i]])))
```

你可能还记得不像**“+”**、**“-”**、**“***和**/“**； **'^'** 是右联想。
用更简单的话来说，a^b^c 是 a^(b^c)不是(a^b)^c.所以必须从右评价。

现在让我们来看看算法是如何工作的，(快速浏览一下代码，以便更好地了解所使用的变量)

```
Let us have an expression s = ((a+b)*c-e*f)
currently both the stacks are empty- 
(we'll use C to denote the char stack and N for node stack)
    s[0] = '('            ((a+b)*c-e*f)
                          ^
        C|(|, N| |

    s[1] = '('           ((a+b)*c-e*f)
                          ^
         |(|  
        C|(|, N| |

    s[2] = 'a'            ((a+b)*c-e*f)
                            ^
         |(|  
        C|(|, N|a|

    s[3] = '+'            ((a+b)*c-e*f)
                             ^
         |+|
         |(|  
        C|(|, N|a|

    s[4] = 'b'             ((a+b)*c-e*f)
                               ^
         |+|
         |(|   |b|
        C|(|, N|a|

    s[5] = ')'             ((a+b)*c-e*f)
                                ^
         |+|            t = '+'         +
         |(|   |b|  ->  t1= 'b'        / \    ->  
        C|(|, N|a|      t2= 'a'       a   b      C|(|, N|+|

    s[6] = '*'              ((a+b)*c-e*f)
                                  ^
         |*|  
        C|(|, N|+|

    s[7] = 'c'              ((a+b)*c-e*f)
                                   ^
         |*|   |c|
        C|(|, N|+|

    s[8] = '-'   ((a+b)*c-e*f)              now (C.top(*)>s[8](-))
                         ^    t = '*'        *
         |*|   |c|            t1 = c        / \  ->    |-|
        C|(|, N|+|            t2 = +       +   c      C|(|, N|*|
                                          / \
                                         a   b
    s[9] = 'e'            ((a+b)*c-e*f)
                                   ^
         |-|   |e|
        C|(|, N|*|

    s[10] = '*'            ((a+b)*c-e*f)      now (C.top(-)>s[10](*))
                                     ^
         |*|                          
         |-|   |e| 
        C|(|, N|*|

    s[11] = 'f'             ((a+b)*c-e*f)
                                       ^
         |*|   |f|
         |-|   |e|
        C|(|, N|*|

    s[12] = ')'             ((a+b)*c-e*f)
       1>                               ^
         |*|   |f|         t = '*'          *        
         |-|   |e|  ->     t1= 'f'  ->     / \  ->   |-|   |*|
        C|(|, N|*|         t2= 'e'        e   f     C|(|, N|*|

       2>                               
                           t = '-'           -        
         |-|   |*|  ->     t1= '*'  ->     /   \  ->   
        C|(|, N|*|         t2= '*'        *     *     C| |, N|-|
                                         / \   / \
                                        +   c  e  f
                                       / \
                                      a   b 
      now make (-) the root of the tree
```

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Tree Structure
typedef struct node
{
    char data;
    struct node *left, *right;
} * nptr;

// Function to create new node
nptr newNode(char c)
{
    nptr n = new node;
    n->data = c;
    n->left = n->right = nullptr;
    return n;
}

// Function to build Expression Tree
nptr build(string& s)
{

    // Stack to hold nodes
    stack<nptr> stN;

    // Stack to hold chars
    stack<char> stC;
    nptr t, t1, t2;

    // Prioritising the operators
    int p[123] = { 0 };
    p['+'] = p['-'] = 1, p['/'] = p['*'] = 2, p['^'] = 3,
    p[')'] = 0;

    for (int i = 0; i < s.length(); i++)
    {
        if (s[i] == '(') {

            // Push '(' in char stack
            stC.push(s[i]);
        }

        // Push the operands in node stack
        else if (isalpha(s[i]))
        {
            t = newNode(s[i]);
            stN.push(t);
        }
        else if (p[s[i]] > 0)
        {
            // If an operator with lower or
            // same associativity appears
            while (
                !stC.empty() && stC.top() != '('
                && ((s[i] != '^' && p[stC.top()] >= p[s[i]])
                    || (s[i] == '^'
                        && p[stC.top()] > p[s[i]])))
            {

                // Get and remove the top element
                // from the character stack
                t = newNode(stC.top());
                stC.pop();

                // Get and remove the top element
                // from the node stack
                t1 = stN.top();
                stN.pop();

                // Get and remove the currently top
                // element from the node stack
                t2 = stN.top();
                stN.pop();

                // Update the tree
                t->left = t2;
                t->right = t1;

                // Push the node to the node stack
                stN.push(t);
            }

            // Push s[i] to char stack
            stC.push(s[i]);
        }
        else if (s[i] == ')') {
            while (!stC.empty() && stC.top() != '(')
            {
                t = newNode(stC.top());
                stC.pop();
                t1 = stN.top();
                stN.pop();
                t2 = stN.top();
                stN.pop();
                t->left = t2;
                t->right = t1;
                stN.push(t);
            }
            stC.pop();
        }
    }
    t = stN.top();
    return t;
}

// Function to print the post order
// traversal of the tree
void postorder(nptr root)
{
    if (root)
    {
        postorder(root->left);
        postorder(root->right);
        cout << root->data;
    }
}

// Driver code
int main()
{
    string s = "(a^b^(c/d/e-f)^(x*y-m*n))";
    s = "(" + s;
    s += ")";
    nptr root = build(s);

    // Function call
    postorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Tree Structure
static class nptr
{
    char data;
    nptr left, right;
} ;

// Function to create new node
static nptr newNode(char c)
{
    nptr n = new nptr();
    n.data = c;
    n.left = n.right = null;
    return n;
}

// Function to build Expression Tree
static nptr build(String s)
{

    // Stack to hold nodes
    Stack<nptr> stN = new Stack<>();

    // Stack to hold chars
    Stack<Character> stC = new Stack<>();
    nptr t, t1, t2;

    // Prioritising the operators
    int []p = new int[123];
    p['+'] = p['-'] = 1;
    p['/'] = p['*'] = 2;
    p['^'] = 3;
    p[')'] = 0;

    for (int i = 0; i < s.length(); i++)
    {
        if (s.charAt(i) == '(') {

            // Push '(' in char stack
            stC.add(s.charAt(i));
        }

        // Push the operands in node stack
        else if (Character.isAlphabetic(s.charAt(i)))
        {
            t = newNode(s.charAt(i));
            stN.add(t);
        }
        else if (p[s.charAt(i)] > 0)
        {

            // If an operator with lower or
            // same associativity appears
            while (
                !stC.isEmpty() && stC.peek() != '('
                && ((s.charAt(i) != '^' && p[stC.peek()] >= p[s.charAt(i)])
                    || (s.charAt(i) == '^'
                        && p[stC.peek()] > p[s.charAt(i)])))
            {

                // Get and remove the top element
                // from the character stack
                t = newNode(stC.peek());
                stC.pop();

                // Get and remove the top element
                // from the node stack
                t1 = stN.peek();
                stN.pop();

                // Get and remove the currently top
                // element from the node stack
                t2 = stN.peek();
                stN.pop();

                // Update the tree
                t.left = t2;
                t.right = t1;

                // Push the node to the node stack
                stN.add(t);
            }

            // Push s[i] to char stack
            stC.push(s.charAt(i));
        }
        else if (s.charAt(i) == ')') {
            while (!stC.isEmpty() && stC.peek() != '(')
            {
                t = newNode(stC.peek());
                stC.pop();
                t1 = stN.peek();
                stN.pop();
                t2 = stN.peek();
                stN.pop();
                t.left = t2;
                t.right = t1;
                stN.add(t);
            }
            stC.pop();
        }
    }
    t = stN.peek();
    return t;
}

// Function to print the post order
// traversal of the tree
static void postorder(nptr root)
{
    if (root != null)
    {
        postorder(root.left);
        postorder(root.right);
        System.out.print(root.data);
    }
}

// Driver code
public static void main(String[] args)
{
    String s = "(a^b^(c/d/e-f)^(x*y-m*n))";
    s = "(" + s;
    s += ")";
    nptr root = build(s);

    // Function call
    postorder(root);
}
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Tree Structure
class nptr:

    # Constructor to set the data of
    # the newly created tree node
    def __init__(self, c):
        self.data = c
        self.left = None
        self.right = None

# Function to create new node
def newNode(c):
    n = nptr(c)
    return n

# Function to build Expression Tree
def build(s):

    # Stack to hold nodes
    stN = []

    # Stack to hold chars
    stC = []

    # Prioritising the operators
    p = [0]*(123)
    p[ord('+')] = p[ord('-')] = 1
    p[ord('/')] = p[ord('*')] = 2
    p[ord('^')] = 3
    p[ord(')')] = 0

    for i in range(len(s)):
        if (s[i] == '('):
            # Push '(' in char stack
            stC.append(s[i])

        # Push the operands in node stack
        elif (s[i].isalpha()):
            t = newNode(s[i])
            stN.append(t)
        elif (p[ord(s[i])] > 0):

            # If an operator with lower or
            # same associativity appears
            while (len(stC) != 0 and stC[-1] != '(' and ((s[i] != '^' and p[ord(stC[-1])] >= p[ord(s[i])])
                    or (s[i] == '^'and
                    p[ord(stC[-1])] > p[ord(s[i])]))):

                # Get and remove the top element
                # from the character stack
                t = newNode(stC[-1])
                stC.pop()

                # Get and remove the top element
                # from the node stack
                t1 = stN[-1]
                stN.pop()

                # Get and remove the currently top
                # element from the node stack
                t2 = stN[-1]
                stN.pop()

                # Update the tree
                t.left = t2
                t.right = t1

                # Push the node to the node stack
                stN.append(t)

            # Push s[i] to char stack
            stC.append(s[i])

        elif (s[i] == ')'):
            while (len(stC) != 0 and stC[-1] != '('):
                t = newNode(stC[-1])
                stC.pop()
                t1 = stN[-1]
                stN.pop()
                t2 = stN[-1]
                stN.pop()
                t.left = t2
                t.right = t1
                stN.append(t)
            stC.pop()
    t = stN[-1]
    return t

# Function to print the post order
# traversal of the tree
def postorder(root):
    if (root != None):
        postorder(root.left)
        postorder(root.right)
        print(root.data, end = "")

s = "(a^b^(c/d/e-f)^(x*y-m*n))"
s = "(" + s
s += ")"
root = build(s)

# Function call
postorder(root)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

// Tree Structure
public  class nptr
{
   public char data;
   public nptr left, right;
} ;

// Function to create new node
static nptr newNode(char c)
{
    nptr n = new nptr();
    n.data = c;
    n.left = n.right = null;
    return n;
}

// Function to build Expression Tree
static nptr build(String s)
{

    // Stack to hold nodes
    Stack<nptr> stN = new Stack<nptr>();

    // Stack to hold chars
    Stack<char> stC = new Stack<char>();
    nptr t, t1, t2;

    // Prioritising the operators
    int []p = new int[123];
    p['+'] = p['-'] = 1;
    p['/'] = p['*'] = 2;
    p['^'] = 3;
    p[')'] = 0;

    for (int i = 0; i < s.Length; i++)
    {
        if (s[i] == '(')
        {

            // Push '(' in char stack
            stC.Push(s[i]);
        }

        // Push the operands in node stack
        else if (char.IsLetter(s[i]))
        {
            t = newNode(s[i]);
            stN.Push(t);
        }
        else if (p[s[i]] > 0)
        {

            // If an operator with lower or
            // same associativity appears
            while (stC.Count != 0 && stC.Peek() != '('
                && ((s[i] != '^' && p[stC.Peek()] >= p[s[i]])
                    || (s[i] == '^'&& p[stC.Peek()] > p[s[i]])))
            {

                // Get and remove the top element
                // from the character stack
                t = newNode(stC.Peek());
                stC.Pop();

                // Get and remove the top element
                // from the node stack
                t1 = stN.Peek();
                stN.Pop();

                // Get and remove the currently top
                // element from the node stack
                t2 = stN.Peek();
                stN.Pop();

                // Update the tree
                t.left = t2;
                t.right = t1;

                // Push the node to the node stack
                stN.Push(t);
            }

            // Push s[i] to char stack
            stC.Push(s[i]);
        }
        else if (s[i] == ')')
        {
            while (stC.Count != 0 && stC.Peek() != '(')
            {
                t = newNode(stC.Peek());
                stC.Pop();
                t1 = stN.Peek();
                stN.Pop();
                t2 = stN.Peek();
                stN.Pop();
                t.left = t2;
                t.right = t1;
                stN.Push(t);
            }
            stC.Pop();
        }
    }
    t = stN.Peek();
    return t;
}

// Function to print the post order
// traversal of the tree
static void postorder(nptr root)
{
    if (root != null)
    {
        postorder(root.left);
        postorder(root.right);
        Console.Write(root.data);
    }
}

// Driver code
public static void Main(String[] args)
{
    String s = "(a^b^(c/d/e-f)^(x*y-m*n))";
    s = "(" + s;
    s += ")";
    nptr root = build(s);

    // Function call
    postorder(root);
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Tree Structure
    class nptr
    {
       constructor(c) {
           this.left = null;
           this.right = null;
           this.data = c;
        }
    }

    // Function to create new node
    function newNode(c)
    {
        let n = new nptr(c);
        return n;
    }

    // Function to build Expression Tree
    function build(s)
    {

        // Stack to hold nodes
        let stN = [];

        // Stack to hold chars
        let stC = [];
        let t, t1, t2;

        // Prioritising the operators
        let p = new Array(123);
        p['+'.charCodeAt()] = p['-'.charCodeAt()] = 1;
        p['/'.charCodeAt()] = p['*'.charCodeAt()] = 2;
        p['^'.charCodeAt()] = 3;
        p[')'.charCodeAt()] = 0;

        for (let i = 0; i < s.length; i++)
        {
            if (s[i] == '(')
            {

                // Push '(' in char stack
                stC.push(s[i]);
            }

            // Push the operands in node stack
            else if ((/[a-zA-Z]/).test(s[i]))
            {
                t = newNode(s[i]);
                stN.push(t);
            }
            else if (p[s[i].charCodeAt()] > 0)
            {

                // If an operator with lower or
                // same associativity appears
                while (stC.length != 0 && stC[stC.length - 1] != '('
                    && ((s[i] != '^' &&
                    p[stC[stC.length - 1].charCodeAt()] >=
                    p[s[i].charCodeAt()])
                        || (s[i] == '^'&&
                        p[stC[stC.length - 1].charCodeAt()] >
                        p[s[i].charCodeAt()])))
                {

                    // Get and remove the top element
                    // from the character stack
                    t = newNode(stC[stC.length - 1]);
                    stC.pop();

                    // Get and remove the top element
                    // from the node stack
                    t1 = stN[stN.length - 1];
                    stN.pop();

                    // Get and remove the currently top
                    // element from the node stack
                    t2 = stN[stN.length - 1];
                    stN.pop();

                    // Update the tree
                    t.left = t2;
                    t.right = t1;

                    // Push the node to the node stack
                    stN.push(t);
                }

                // Push s[i] to char stack
                stC.push(s[i]);
            }
            else if (s[i] == ')')
            {
                while (stC.length != 0 &&
                stC[stC.length - 1] != '(')
                {
                    t = newNode(stC[stC.length - 1]);
                    stC.pop();
                    t1 = stN[stN.length - 1];
                    stN.pop();
                    t2 = stN[stN.length - 1];
                    stN.pop();
                    t.left = t2;
                    t.right = t1;
                    stN.push(t);
                }
                stC.pop();
            }
        }
        t = stN[stN.length - 1];
        return t;
    }

    // Function to print the post order
    // traversal of the tree
    function postorder(root)
    {
        if (root != null)
        {
            postorder(root.left);
            postorder(root.right);
            document.write(root.data);
        }
    }

    let s = "(a^b^(c/d/e-f)^(x*y-m*n))";
    s = "(" + s;
    s += ")";
    let root = build(s);

    // Function call
    postorder(root);

</script>
```

**Output**

```
abcd/e/f-xy*mn*-^^^
```

时间复杂度为 **O(n)** ，因为每个字符只被访问一次。
空间复杂度为**O(n)**as(char _ stack+node _ stack)<= n
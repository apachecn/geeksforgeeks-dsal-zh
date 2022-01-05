# 克隆一个栈而不使用额外空间|集合 2

> 原文:[https://www . geesforgeks . org/clone-a-stack-不使用额外空间-set-2/](https://www.geeksforgeeks.org/clone-a-stack-without-using-extra-space-set-2/)

给定一个[栈](https://www.geeksforgeeks.org/stack-data-structure/) **S** ，任务是将给定栈 **S** 的内容复制到另一个栈 **T** 保持相同的顺序。

**示例:**

> **输入:**来源:-| 5 |
> | 4 |
> | 3 |
> | 2 |
> | 1 |
> **输出:**目的地:-| 5 |
> | 4 |
> | 3 |
> | 2 |
> | 1 |
> 
> **输入:**来源:-| 12 |
> | 13 |
> | 14 |
> | 15 |
> | 16 |
> | T7】输出:目的地:-| 12 |
> | 13 |
> | 14 |
> | 15 |
> | 16 |

[**反转叠加**](https://www.geeksforgeeks.org/reverse-a-stack-using-recursion/) **为主的进场方式:**反转叠加为主的进场方式请参考本文[前一帖](https://www.geeksforgeeks.org/clone-a-stack-without-extra-space/)。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

[**基于链表**](https://www.geeksforgeeks.org/data-structures/linked-list/) **的方法:**基于链表的方法请参考本文[之前的帖子](https://www.geeksforgeeks.org/clone-a-stack-without-extra-space/)。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

[**递归**](https://www.geeksforgeeks.org/recursion/)**-基于方法:**给定的问题也可以通过使用[递归](https://www.geeksforgeeks.org/recursion/)来解决。按照以下步骤解决问题:

*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如说 **RecursiveCloneStack(栈< int > S，栈< int > Des)** 其中 **S** 是源栈 **Des** 是目的栈:
    *   定义一个基本情况，好像 **S.size()** 是 **0** 然后从函数返回。
    *   将源栈的[顶元素存储在一个变量中，说 **val** ，然后](https://www.geeksforgeeks.org/stack-top-c-stl/)[移除栈的顶元素](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/) **S** [。](https://www.geeksforgeeks.org/stack-top-c-stl/)
    *   现在用更新的源栈 **S** 调用递归函数，即**recursiveloconestack(S，Des)** 。
    *   完成上述步骤后，将**阀**推入**德斯**堆。
*   初始化一个[栈](https://www.geeksforgeeks.org/stack-data-structure/)，说 **Des** 来存储目的栈。
*   现在调用函数**recursivelocenstack(S，Des)** 将源栈的元素复制到目标栈。
*   完成以上步骤后，[打印堆栈的元素](https://www.geeksforgeeks.org/print-stack-elements-from-top-to-bottom/) **Des** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Auxiliary function to copy elements
// of source stack to destination stack
void RecursiveCloneStack(stack<int>& S,
                         stack<int>& Des)
{
    // Base case for Recursion
    if (S.size() == 0)
        return;

    // Stores the top element of the
    // source stack
    int val = S.top();

    // Removes the top element of the
    // source stack
    S.pop();

    // Recursive call to the function
    // with remaining stack
    RecursiveCloneStack(S, Des);

    // Push the top element of the source
    // stack into the Destination stack
    Des.push(val);
}

// Function to copy the elements of the
// source stack to destination stack
void cloneStack(stack<int>& S)
{
    // Stores the destination stack
    stack<int> Des;

    // Recursive function call to copy
    // the source stack to the
    // destination stack
    RecursiveCloneStack(S, Des);

    cout << "Destination:- ";
    int f = 0;

    // Iterate until stack Des is
    // non-empty
    while (!Des.empty()) {

        if (f == 0) {
            cout << Des.top();
            f = 1;
        }

        else
            cout << "              "
                 << Des.top();
        Des.pop();

        cout << '\n';
    }
}

// Driver Code
int main()
{
    stack<int> S;
    S.push(1);
    S.push(2);
    S.push(3);
    S.push(4);
    S.push(5);
    cloneStack(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    static Stack<Integer> S = new Stack<Integer>();
    static Stack<Integer> Des = new Stack<Integer>(); // Stores the destination stack

    // Auxiliary function to copy elements
    // of source stack to destination stack
    static void RecursiveCloneStack()
    {

        // Base case for Recursion
        if (S.size() == 0)
            return;

        // Stores the top element of the
        // source stack
        int val = S.peek();

        // Removes the top element of the
        // source stack
        S.pop();

        // Recursive call to the function
        // with remaining stack
        RecursiveCloneStack();

        // Push the top element of the source
        // stack into the Destination stack
        Des.push(val);
    }

    // Function to copy the elements of the
    // source stack to destination stack
    static void cloneStack()
    {
        // Recursive function call to copy
        // the source stack to the
        // destination stack
        RecursiveCloneStack();

        System.out.print("Destination:- ");
        int f = 0;

        // Iterate until stack Des is
        // non-empty
        while (Des.size() > 0) {

            if (f == 0) {
                System.out.print(Des.peek());
                f = 1;
            }

            else
                System.out.print("              " + Des.peek());
            Des.pop();

            System.out.println();
        }
    }

  // Driver code
    public static void main(String[] args) {
        S.push(1);
        S.push(2);
        S.push(3);
        S.push(4);
        S.push(5);
        cloneStack();
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

S = []
Des = [] # Stores the destination stack

# Auxiliary function to copy elements
# of source stack to destination stack
def RecursiveCloneStack():

    # Base case for Recursion
    if (len(S) == 0):
        return

    # Stores the top element of the
    # source stack
    val = S[-1]

    # Removes the top element of the
    # source stack
    S.pop()

    # Recursive call to the function
    # with remaining stack
    RecursiveCloneStack()

    # Push the top element of the source
    # stack into the Destination stack
    Des.append(val)

# Function to copy the elements of the
# source stack to destination stack
def cloneStack():
    # Recursive function call to copy
    # the source stack to the
    # destination stack
    RecursiveCloneStack()

    print("Destination:- ", end = "")
    f = 0

    # Iterate until stack Des is
    # non-empty
    while len(Des) > 0:
        if (f == 0):
            print(Des[-1], end = "")
            f = 1

        else:
            print("             ", Des[-1], end = "")
        Des.pop()

        print()

S.append(1)
S.append(2)
S.append(3)
S.append(4)
S.append(5)
cloneStack()

# This code is contributed by decode2207.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG {

    static Stack S = new Stack();
    static Stack Des = new Stack(); // Stores the destination stack

    // Auxiliary function to copy elements
    // of source stack to destination stack
    static void RecursiveCloneStack()
    {
        // Base case for Recursion
        if (S.Count == 0)
            return;

        // Stores the top element of the
        // source stack
        int val = (int)S.Peek();

        // Removes the top element of the
        // source stack
        S.Pop();

        // Recursive call to the function
        // with remaining stack
        RecursiveCloneStack();

        // Push the top element of the source
        // stack into the Destination stack
        Des.Push(val);
    }

    // Function to copy the elements of the
    // source stack to destination stack
    static void cloneStack()
    {
        // Recursive function call to copy
        // the source stack to the
        // destination stack
        RecursiveCloneStack();

        Console.Write("Destination:- ");
        int f = 0;

        // Iterate until stack Des is
        // non-empty
        while (Des.Count > 0) {

            if (f == 0) {
                Console.Write(Des.Peek());
                f = 1;
            }

            else
                Console.Write("              " + Des.Peek());
            Des.Pop();

            Console.WriteLine();
        }
    }

  static void Main() {
    S.Push(1);
    S.Push(2);
    S.Push(3);
    S.Push(4);
    S.Push(5);
    cloneStack();
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach
    S = [];
    Des = []; // Stores the destination stack

    // Auxiliary function to copy elements
    // of source stack to destination stack
    function RecursiveCloneStack()
    {

        // Base case for Recursion
        if (S.length == 0)
            return;

        // Stores the top element of the
        // source stack
        let val = S[S.length - 1];

        // Removes the top element of the
        // source stack
        S.pop();

        // Recursive call to the function
        // with remaining stack
        RecursiveCloneStack();

        // Push the top element of the source
        // stack into the Destination stack
        Des.push(val);
    }

    // Function to copy the elements of the
    // source stack to destination stack
    function cloneStack()
    {
        // Recursive function call to copy
        // the source stack to the
        // destination stack
        RecursiveCloneStack();

        document.write("Destination:- ");
        let f = 0;

        // Iterate until stack Des is
        // non-empty
        while (Des.length > 0) {

            if (f == 0) {
                document.write(Des[Des.length - 1]);
                f = 1;
            }

            else{
                document.write("                      " + Des[Des.length - 1]);
            }
            Des.pop();

            document.write("</br>");
        }
    }

    S.push(1);
    S.push(2);
    S.push(3);
    S.push(4);
    S.push(5);
    cloneStack();

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
Destination:- 5
              4
              3
              2
              1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
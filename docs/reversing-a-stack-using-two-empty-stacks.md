# 使用两个空堆栈反转堆栈

> 原文:[https://www . geeksforgeeks . org/反转堆栈-使用两个空堆栈/](https://www.geeksforgeeks.org/reversing-a-stack-using-two-empty-stacks/)

给定一个[叠加](https://www.geeksforgeeks.org/stack-data-structure/) **S** ，任务是[使用两个额外叠加反转叠加](https://www.geeksforgeeks.org/reverse-a-stack-using-recursion/) **S** 。

**示例:**

> **输入:** S={1，2，3，4，5}
> **输出:** 5 4 3 2 1
> **解释:**
> 初始堆栈 S:
> 1→顶部
> 2
> 3
> 4
> 5
> 反转后，再使用两个额外的堆栈:
> 5→顶部
> 4
> 3
> 2
> 1
> 
> **输入:** S={1，25，17 }
> T3】输出: 17 25 1

**方法:**按照以下步骤解决问题:

1.  创建两个额外的空[栈](https://www.geeksforgeeks.org/stack-in-cpp-stl/)，比如 **A** 和 **B** 。
2.  定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **transfer()** ，该函数接受两个堆栈 **X** 和 **Y** 作为参数，并执行以下操作:
    1.  [循环，同时](https://www.geeksforgeeks.org/loops-in-c-and-cpp/) **X** 不为空，并执行以下操作:
        1.  [将 **X** 的](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)[顶](https://www.geeksforgeeks.org/stack-top-c-stl/)元素推入 **Y** 。
        2.  [从 **X** 中弹出](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)那个元素。
3.  调用**转移(S，A)** tos 将堆栈的所有元素 **S** 转移到 **A** 。(*元素顺序颠倒*)。
4.  调用**转移(A，B)** 将叠加的所有元素 **A** 转移到 **B** 。(*元素的顺序与最初在 **S*** 中的顺序相同)
5.  调用**转移(B，S)** 将 **B** 的所有元素转移到 **S** 。(*元素顺序颠倒*)
6.  最后显示堆栈 **S** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to transfer elements
// from the stack X to the stack Y
void transfer(stack<int>& X,
              stack<int>& Y)
{
    // Iterate while X is not empty
    while (!X.empty()) {

        // Push the top element
        // of X into Y
        Y.push(X.top());

        // Pop from X
        X.pop();
    }
}

// Function to display the
// contents of the stack S
void display(stack<int> S)
{
    // Iterate while S is
    // not empty
    while (!S.empty()) {

        // Print the top
        // element of the stack S
        cout << S.top() << " ";

        // Pop from S
        S.pop();
    }
    cout << endl;
}

// Function to reverse a stack using two stacks
void reverseStackUsingTwoStacks(stack<int>& S)
{
    // Two additional stacks
    stack<int> A, B;

    // Transfer all elements
    // from the stack S to A
    transfer(S, A);

    // Transfer all elements
    // from the stack A to B
    transfer(A, B);

    // Transfer all elements
    // from the stack B to S
    transfer(B, S);

    // Print the contents of S
    display(S);
}
// Driver Code
int main()
{
    // Input
    stack<int> S;
    S.push(5);
    S.push(4);
    S.push(3);
    S.push(2);
    S.push(1);

    // Function call
    reverseStackUsingTwoStacks(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Stack;
public class GFG
{

    // Function to transfer elements
    // from the stack X to the stack Y
    static void transfer(Stack<Integer> X, Stack<Integer> Y)
    {
        // Iterate while X is not empty
        while (!X.empty())
        {

            // Push the top element
            // of X into Y
            Y.push(X.peek());

            // Pop from X
            X.pop();
        }
    }

    // Function to display the
    // contents of the stack S
    static void display(Stack<Integer> S)
    {
        // Iterate while S is
        // not empty
        while (!S.empty()) {

            // Print the top
            // element of the stack S
            System.out.print(S.peek() + " ");

            // Pop from S
            S.pop();
        }
        System.out.println();
    }

    // Function to reverse a stack using two stacks
    static void reverseStackUsingTwoStacks(Stack<Integer> S)
    {
        // Two additional stacks
        Stack<Integer> A = new Stack<>();
        Stack<Integer> B = new Stack<>();

        // Transfer all elements
        // from the stack S to A
        while (!S.empty())
            A.push(S.pop());

        // Transfer all elements
        // from the stack A to B
        while (!A.empty())
            B.push(A.pop());

        // Transfer all elements
        // from the stack B to S
        while (!B.empty())
            S.push(B.pop());

        // Print the contents of S
        display(S);
    }

    // Driver code
    public static void main(String[] args)
    {

      // Given Input
      // Input
        Stack<Integer> S = new Stack<>();
        S.push(5);
        S.push(4);
        S.push(3);
        S.push(2);
        S.push(1);

        // Function call
        reverseStackUsingTwoStacks(S);
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to display the
# contents of the stack S
def display(S):

    # Iterate while S is
    # not empty
    while len(S) > 0:

        # Print the top
        # element of the stack S
        print(S[-1], end = " ")

        # Pop from S
        S.pop()
    print()

# Function to reverse a stack using two stacks
def reverseStackUsingTwoStacks(S):

    # Two additional stacks
    A = []
    B = []

    # Transfer all elements
    # from the stack S to A
    while len(S) > 0:
        A.append(S[-1])
        S.pop()

    # Transfer all elements
    # from the stack A to B
    while len(A) > 0:
        B.append(A[-1])
        A.pop()

    # Transfer all elements
    # from the stack B to S
    while len(B) > 0:
        S.append(B[-1])
        B.pop()

    # Print the contents of S
    display(S)

# Given Input
# Input
S = []
S.append(5)
S.append(4)
S.append(3)
S.append(2)
S.append(1)

# Function call
reverseStackUsingTwoStacks(S)

# This code is contributed by suresh07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG {

    // Function to transfer elements
    // from the stack X to the stack Y
    static void transfer(Stack X, Stack Y)
    {
        // Iterate while X is not empty
        while (X.Count > 0)
        {

            // Push the top element
            // of X into Y
            Y.Push(X.Peek());

            // Pop from X
            X.Pop();
        }
    }

    // Function to display the
    // contents of the stack S
    static void display(Stack S)
    {
        // Iterate while S is
        // not empty
        while (S.Count > 0) {

            // Print the top
            // element of the stack S
            Console.Write(S.Peek() + " ");

            // Pop from S
            S.Pop();
        }
        Console.WriteLine();
    }

    // Function to reverse a stack using two stacks
    static void reverseStackUsingTwoStacks(Stack S)
    {
        // Two additional stacks
        Stack A = new Stack();
        Stack B = new Stack();

        // Transfer all elements
        // from the stack S to A
        while (S.Count > 0)
            A.Push(S.Pop());

        // Transfer all elements
        // from the stack A to B
        while (A.Count > 0)
            B.Push(A.Pop());

        // Transfer all elements
        // from the stack B to S
        while (B.Count > 0)
            S.Push(B.Pop());

        // Print the contents of S
        display(S);
    }

  static void Main() {
    // Given Input
    // Input
    Stack S = new Stack();
    S.Push(5);
    S.Push(4);
    S.Push(3);
    S.Push(2);
    S.Push(1);

    // Function call
    reverseStackUsingTwoStacks(S);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to display the
    // contents of the stack S
    function display(S)
    {
        // Iterate while S is
        // not empty
        while (S.length > 0) {

            // Print the top
            // element of the stack S
            document.write(S[S.length - 1] + " ");

            // Pop from S
            S.pop();
        }
        document.write("</br>");
    }

    // Function to reverse a stack using two stacks
    function reverseStackUsingTwoStacks(S)
    {
        // Two additional stacks
        let A = [];
        let B = [];

        // Transfer all elements
        // from the stack S to A
        while (S.length > 0)
        {
            A.push(S[S.length - 1]);
            S.pop();
        }

        // Transfer all elements
        // from the stack A to B
        while (A.length > 0)
        {
            B.push(A[A.length - 1]);
            A.pop();
        }

        // Transfer all elements
        // from the stack B to S
        while (B.length > 0)
        {
            S.push(B[B.length - 1]);
            B.pop();
        }

        // Print the contents of S
        display(S);
    }

    // Given Input
    // Input
    let S = [];
    S.push(5);
    S.push(4);
    S.push(3);
    S.push(2);
    S.push(1);

    // Function call
    reverseStackUsingTwoStacks(S);

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
5 4 3 2 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
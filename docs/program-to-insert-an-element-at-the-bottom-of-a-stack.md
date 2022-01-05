# 在堆栈底部插入元素的程序

> 原文:[https://www . geesforgeks . org/program-to-insert-一个栈底元素/](https://www.geeksforgeeks.org/program-to-insert-an-element-at-the-bottom-of-a-stack/)

给定一个[栈](https://www.geeksforgeeks.org/stack-data-structure/) **S** 和一个整数 **N** ，任务是在栈底插入 **N** 。

**示例:**

> **输入:**N = 7
> S = 1<--(上)
> 2
> 3
> 4
> 5
> T8】输出: 1 2 3 4 5 7
> 
> **输入:**N = 17
> S = 1<--(上)
> 12
> 34
> 47
> 15
> T8】输出: 1 12 34 47 15 17

**天真的方法:**最简单的方法是创建另一个堆栈。按照以下步骤解决问题:

1.  [初始化堆栈](https://www.geeksforgeeks.org/stack-in-cpp-stl/)，比如**温度**。
2.  继续从给定堆栈 **S** 和[弹出，将弹出的元素推入**temp**T5】，直到堆栈 **S** 变空。](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)
3.  [将 **N** 推入堆栈**S**T5。](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)
4.  现在，继续从堆栈**温度**弹出，并将弹出的元素推入堆栈 **S** ，直到[堆栈**温度**变为空的](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to insert an element
// at the bottom of a given stack
void insertToBottom(stack<int> S, int N)
{
    // Temporary stack
    stack<int> temp;

    // Iterate until S becomes empty
    while (!S.empty()) {

        // Push the top element of S
        // into the stack temp
        temp.push(S.top());

        // Pop the top element of S
        S.pop();
    }

    // Push N into the stack S
    S.push(N);

    // Iterate until temp becomes empty
    while (!temp.empty()) {

        // Push the top element of
        // temp into the stack S
        S.push(temp.top());

        // Pop the top element of temp
        temp.pop();
    }

    // Print the elements of S
    while (!S.empty()) {
        cout << S.top() << " ";
        S.pop();
    }
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

    int N = 7;

    insertToBottom(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Stack;

class GFG{

// Function to insert an element
// at the bottom of a given stack
static void insertToBottom(Stack<Integer> S, int N)
{

    // Temporary stack
    Stack<Integer> temp = new Stack<>();

    // Iterate until S becomes empty
    while (!S.empty())
    {

        // Push the top element of S
        // into the stack temp
        temp.push(S.peek());

        // Pop the top element of S
        S.pop();
    }

    // Push N into the stack S
    S.push(N);

    // Iterate until temp becomes empty
    while (!temp.empty())
    {

        // Push the top element of
        // temp into the stack S
        S.push(temp.peek());

        // Pop the top element of temp
        temp.pop();
    }

    // Print the elements of S
    while (!S.empty())
    {
        System.out.print(S.peek() + " ");
        S.pop();
    }
}

// Driver code
public static void main(String[] args)
{

    // Given Binary Tree
    Stack<Integer> S = new Stack<>();
    S.push(5);
    S.push(4);
    S.push(3);
    S.push(2);
    S.push(1);

    int N = 7;

    insertToBottom(S, N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to insert an element
# at the bottom of a given stack
def insertToBottom(S, N):

    # Temporary stack
    temp = []

    # Iterate until S becomes empty
    while (len(S) != 0):

        # Push the top element of S
        # into the stack temp
        temp.append(S[-1])

        # Pop the top element of S
        S.pop()

    # Push N into the stack S
    S.append(N)

    # Iterate until temp becomes empty
    while (len(temp) != 0):

        # Push the top element of
        # temp into the stack S
        S.append(temp[-1])

        # Pop the top element of temp
        temp.pop()

    # Print the elements of S
    while (len(S) != 0):
        print(S[-1], end = " ")
        S.pop()

# Driver Code
if __name__ == "__main__":

    # Input
    S = []
    S.append(5)
    S.append(4)
    S.append(3)
    S.append(2)
    S.append(1)

    N = 7

    insertToBottom(S, N)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach

using System;
using System.Collections;

public class GFG {

    // Function to insert an element
    // at the bottom of a given stack
    static void insertToBottom(Stack S, int N)
    {

        // Temporary stack
        Stack temp = new Stack();

        // Iterate until S becomes empty
        while (S.Count != 0) {

            // Push the top element of S
            // into the stack temp
            temp.Push(S.Peek());

            // Pop the top element of S
            S.Pop();
        }

        // Push N into the stack S
        S.Push(N);

        // Iterate until temp becomes empty
        while (temp.Count != 0) {

            // Push the top element of
            // temp into the stack S
            S.Push(temp.Peek());

            // Pop the top element of temp
            temp.Pop();
        }

        // Print the elements of S
        while (S.Count != 0) {
            Console.Write(S.Peek() + " ");
            S.Pop();
        }
    }

    // Driver code
    static public void Main()
    {

        // Given Binary Tree
        Stack S = new Stack();
        S.Push(5);
        S.Push(4);
        S.Push(3);
        S.Push(2);
        S.Push(1);

        int N = 7;

        insertToBottom(S, N);
    }
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to insert an element
// at the bottom of a given stack
function insertToBottom(S, N)
{
    // Temporary stack
    var temp = [];

    // Iterate until S becomes empty
    while (S.length!=0) {

        // Push the top element of S
        // into the stack temp
        temp.push(S[S.length-1]);

        // Pop the top element of S
        S.pop();
    }

    // Push N into the stack S
    S.push(N);

    // Iterate until temp becomes empty
    while (temp.length!=0) {

        // Push the top element of
        // temp into the stack S
        S.push(temp[temp.length-1]);

        // Pop the top element of temp
        temp.pop();
    }

    // Print the elements of S
    while (S.length!=0) {
        document.write( S[S.length-1] + " ");
        S.pop();
    }
}

// Driver Code

// Input
var S = [];
S.push(5);
S.push(4);
S.push(3);
S.push(2);
S.push(1);
var N = 7;
insertToBottom(S, N);

</script>
```

**Output:** 

```
1 2 3 4 5 7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**高效方法:**不使用临时堆栈，*隐式堆栈*可以通过[递归](https://www.geeksforgeeks.org/recursion/)来使用。按照以下步骤解决问题:

1.  定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，该函数接受堆栈 **S** 和一个整数作为参数，并返回一个堆栈。
2.  要考虑的基本情况是[堆栈为空](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)。对于这种情况，[将 **N** 推入堆栈](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)并返回。
3.  否则，去掉**S**T3 的[顶元素，存储在一个变量中，比如说 **X** 。](https://www.geeksforgeeks.org/stack-top-c-stl/)
4.  使用新堆栈再次递归
5.  将 **X** 推入 **S** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to use implicit stack
// to insert an element at the bottom of stack
stack<int> recur(stack<int> S, int N)
{
    // If stack is empty
    if (S.empty())
        S.push(N);

    else {

        // Stores the top element
        int X = S.top();

        // Pop the top element
        S.pop();

        // Recurse with remaining elements
        S = recur(S, N);

        // Push the previous
        // top element again
        S.push(X);
    }
    return S;
}

// Function to insert an element
// at the bottom of stack
void insertToBottom(
    stack<int> S, int N)
{

    // Recursively insert
    // N at the bottom of S
    S = recur(S, N);

    // Print the stack S
    while (!S.empty()) {
        cout << S.top() << " ";
        S.pop();
    }
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

    int N = 7;

    insertToBottom(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Recursive function to use implicit stack
    // to insert an element at the bottom of stack
    static Stack<Integer> recur(Stack<Integer> S, int N)
    {
        // If stack is empty
        if (S.size() == 0)
            S.push(N);

        else {

            // Stores the top element
            int X = S.peek();

            // Pop the top element
            S.pop();

            // Recurse with remaining elements
            S = recur(S, N);

            // Push the previous
            // top element again
            S.push(X);
        }
        return S;
    }

    // Function to insert an element
    // at the bottom of stack
    static void insertToBottom(Stack<Integer> S, int N)
    {

        // Recursively insert
        // N at the bottom of S
        S = recur(S, N);

        // Print the stack S
        while (S.size() > 0) {
            System.out.print(S.peek() + " ");
            S.pop();
        }
    }

    public static void main(String[] args) {
        // Input
        Stack<Integer> S = new Stack<Integer>();
        S.push(5);
        S.push(4);
        S.push(3);
        S.push(2);
        S.push(1);

        int N = 7;

        insertToBottom(S, N);
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Recursive function to use implicit stack
# to insert an element at the bottom of stack
def recur(S, N):

    # If stack is empty
    if (len(S) == 0):
        S.append(N)

    else:

        # Stores the top element
        X = S[-1]

        # Pop the top element
        S.pop()

        # Recurse with remaining elements
        S = recur(S, N)

        # Push the previous
        # top element again
        S.append(X)

    return S

# Function to insert an element
# at the bottom of stack
def insertToBottom(S, N):

    # Recursively insert
    # N at the bottom of S
    S = recur(S, N)

    # Print the stack S
    while (len(S) > 0):
        print(S.pop(), end = " ")

# Driver code

# Input
S = []
S.append(5)
S.append(4)
S.append(3)
S.append(2)
S.append(1)

N = 7

insertToBottom(S, N)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG {

    // Recursive function to use implicit stack
    // to insert an element at the bottom of stack
    static Stack recur(Stack S, int N)
    {
        // If stack is empty
        if (S.Count == 0)
            S.Push(N);

        else {

            // Stores the top element
            int X = (int)S.Peek();

            // Pop the top element
            S.Pop();

            // Recurse with remaining elements
            S = recur(S, N);

            // Push the previous
            // top element again
            S.Push(X);
        }
        return S;
    }

    // Function to insert an element
    // at the bottom of stack
    static void insertToBottom(Stack S, int N)
    {

        // Recursively insert
        // N at the bottom of S
        S = recur(S, N);

        // Print the stack S
        while (S.Count > 0) {
            Console.Write((int)S.Peek() + " ");
            S.Pop();
        }
    }

  static void Main() {
    // Input
    Stack S = new Stack();
    S.Push(5);
    S.Push(4);
    S.Push(3);
    S.Push(2);
    S.Push(1);

    int N = 7;

    insertToBottom(S, N);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Recursive function to use implicit stack
    // to insert an element at the bottom of stack
    function recur(S, N)
    {
        // If stack is empty
        if (S.length == 0)
            S.push(N);

        else {

            // Stores the top element
            let X = S[S.length - 1];

            // Pop the top element
            S.pop();

            // Recurse with remaining elements
            S = recur(S, N);

            // Push the previous
            // top element again
            S.push(X);
        }
        return S;
    }

    // Function to insert an element
    // at the bottom of stack
    function insertToBottom(S, N)
    {

        // Recursively insert
        // N at the bottom of S
        S = recur(S, N);

        // Print the stack S
        while (S.length > 0) {
            document.write(S[S.length - 1] + " ");
            S.pop();
        }
    }

    // Input
    let S = [];
    S.push(5);
    S.push(4);
    S.push(3);
    S.push(2);
    S.push(1);

    let N = 7;

    insertToBottom(S, N);

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
1 2 3 4 5 7
```

***时间复杂度:** O(N)，其中 N 为* *栈中元素总数。*
***辅助空间:** O(N)*
# 检查堆栈的元素是否成对排序

> 原文:[https://www . geeksforgeeks . org/check-如果堆栈元素是成对排序的/](https://www.geeksforgeeks.org/check-if-the-elements-of-stack-are-pairwise-sorted/)

给定一个整数堆栈，编写一个检查堆栈中的数字是否成对排序的函数 pairWiseSorted()。
对必须是递增的，如果栈有奇数个元素，则顶部的元素从一对中被遗漏。该函数应保留原始堆栈内容。

> 堆栈上只允许以下标准操作。
> 
> 1.  **推** (X):在栈顶输入一个元素 X。
> 2.  **弹出**():移除堆栈顶部元素。
> 3.  **清空**():检查堆栈是否为空。

示例:

```
Input: 4, 5, 6, 7, 8, 9
Output: Yes

Input: 4, 9, 2, 1, 10, 8
Output: No
```

**方法:**思路是用另一个栈。

*   创建辅助堆栈辅助。
*   将给定堆栈的内容传输到辅助。
*   遍历辅助。遍历提取前两个元素并检查它们是否排序。
*   检查后，将这些元素放回原始堆栈。

以下是上述方法的实现:

## C++

```
// C++ program to check if successive
// pair of numbers in the stack are
// sorted or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if elements are
// pairwise sorted in stack
bool pairWiseConsecutive(stack<int> s)
{
    // Transfer elements of s to aux.
    stack<int> aux;
    while (!s.empty()) {
        aux.push(s.top());
        s.pop();
    }

    // Traverse aux and see if
    // elements are pairwise
    // sorted or not. We also
    // need to make sure that original
    // content is retained.
    bool result = true;
    while (!aux.empty()) {

        // Fetch current top two
        // elements of aux and check
        // if they are sorted.
        int x = aux.top();
        aux.pop();
        int y = aux.top();
        aux.pop();
        if (x > y)
            result = false;

        // Push the elements to original
        // stack.
        s.push(x);
        s.push(y);
    }

    if (aux.size() == 1)
        s.push(aux.top());

    return result;
}

// Driver program
int main()
{
    stack<int> s;
    s.push(4);
    s.push(5);
    s.push(-3);
    s.push(-2);
    s.push(10);
    s.push(11);
    s.push(5);
    s.push(6);
    // s.push(20);

    if (pairWiseConsecutive(s))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    cout << "Stack content (from top)"
            " after function call\n";
    while (s.empty() == false) {
        cout << s.top() << " ";
        s.pop();
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if successive
// pair of numbers in the stack are
// sorted or not
import java.util.Stack;

class GFG {

// Function to check if elements are
// pairwise sorted in stack
    static boolean pairWiseConsecutive(Stack<Integer> s) {
        // Transfer elements of s to aux.
        Stack<Integer> aux = new Stack<>();
        while (!s.empty()) {
            aux.push(s.peek());
            s.pop();
        }

        // Traverse aux and see if
        // elements are pairwise
        // sorted or not. We also
        // need to make sure that original
        // content is retained.
        boolean result = true;
        while (!aux.empty()) {

            // Fetch current top two
            // elements of aux and check
            // if they are sorted.
            int x = aux.peek();
            aux.pop();
            int y = aux.peek();
            aux.pop();
            if (x > y) {
                result = false;
            }

            // Push the elements to original
            // stack.
            s.push(x);
            s.push(y);
        }

        if (aux.size() == 1) {
            s.push(aux.peek());
        }

        return result;
    }

// Driver program
    public static void main(String[] args) {

        Stack<Integer> s = new Stack<>();
        s.push(4);
        s.push(5);
        s.push(-3);
        s.push(-2);
        s.push(10);
        s.push(11);
        s.push(5);
        s.push(6);
        // s.push(20);

        if (pairWiseConsecutive(s)) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }

        System.out.println("Stack content (from top)"
                + " after function call");
        while (s.empty() == false) {
            System.out.print(s.peek() + " ");
            s.pop();
        }

    }

}
```

## 蟒蛇 3

```
# Python program to check if successive
# pair of numbers in the stack are
# sorted or not

# using deque as stack
from collections import deque

# Function to check if elements are
# pairwise sorted in stack
def pairWiseConsecutive(s):

    # Transfer elements of s to aux.
    aux = deque()
    while len(s) > 0:
        aux.append(s.pop())

    # Traverse aux and see if
    # elements are pairwise
    # sorted or not. We also
    # need to make sure that original
    # content is retained.
    result = True
    while len(aux) != 0:

        # Fetch current top two
        # elements of aux and check
        # if they are sorted.
        x = aux.pop()
        y = aux.pop()
        if x > y:
            result = False

        # Push the elements to original
        # stack.
        s.append(x)
        s.append(y)

    if len(aux) == 1:
        s.append(aux.pop())

    return result

# Driver Code
if __name__ == "__main__":
    s = deque()
    s.append(4)
    s.append(5)
    s.append(-3)
    s.append(-2)
    s.append(10)
    s.append(11)
    s.append(5)
    s.append(6)

    if pairWiseConsecutive(s):
        print("Yes")
    else:
        print("No")

    print("Stack content (from top) after function call")
    while len(s) > 0:
        print(s.pop(), end=" ")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to check if successive
// pair of numbers in the stack are
using System;
using System.Collections.Generic;
public class GFG{

// Function to check if elements are
// pairwise sorted in stack
    static bool pairWiseConsecutive(Stack<int> s) {
        // Transfer elements of s to aux.
        Stack<int> aux = new Stack<int>();
        while (!(s.Count==0)) {
            aux.Push(s.Peek());
            s.Pop();
        }

        // Traverse aux and see if
        // elements are pairwise
        // sorted or not. We also
        // need to make sure that original
        // content is retained.
        bool result = true;
        while (!(aux.Count==0)) {

            // Fetch current top two
            // elements of aux and check
            // if they are sorted.
            int x = aux.Peek();
            aux.Pop();
            int y = aux.Peek();
            aux.Pop();
            if (x > y) {
                result = false;
            }

            // Push the elements to original
            // stack.
            s.Push(x);
            s.Push(y);
        }

        if (aux.Count == 1) {
            s.Push(aux.Peek());
        }

        return result;
    }

// Driver program
    public static void Main() {

        Stack<int> s = new Stack<int>();
        s.Push(4);
        s.Push(5);
        s.Push(-3);
        s.Push(-2);
        s.Push(10);
        s.Push(11);
        s.Push(5);
        s.Push(6);
        // s.push(20);

        if (pairWiseConsecutive(s)) {
            Console.WriteLine("Yes");
        } else {
            Console.WriteLine("No");
        }

        Console.WriteLine("Stack content (from top)"
                + " after function call");
        while (!(s.Count == 0)) {
            Console.Write(s.Peek() + " ");
            s.Pop();
        }

    }

}
```

## java 描述语言

```
<script>

// JavaScript program to check if successive
// pair of numbers in the stack are
// sorted or not

// Function to check if elements are
// pairwise sorted in stack
function pairWiseConsecutive(s)
{
    // Transfer elements of s to aux.
    var aux = [];
    while (s.length!=0) {
        aux.push(s[s.length-1]);
        s.pop();
    }

    // Traverse aux and see if
    // elements are pairwise
    // sorted or not. We also
    // need to make sure that original
    // content is retained.
    var result = true;
    while (aux.length!=0) {

        // Fetch current top two
        // elements of aux and check
        // if they are sorted.
        var x = aux[aux.length-1];
        aux.pop();
        var y = aux[aux.length-1];
        aux.pop();
        if (x > y)
            result = false;

        // Push the elements to original
        // stack.
        s.push(x);
        s.push(y);
    }

    if (aux.length == 1)
        s.push(aux[aux.length-1]);

    return result;
}

// Driver program
var s = [];
s.push(4);
s.push(5);
s.push(-3);
s.push(-2);
s.push(10);
s.push(11);
s.push(5);
s.push(6);
// s.push(20);
if (pairWiseConsecutive(s))
    document.write( "Yes" + "<br>");
else
    document.write( "No" + "<br>");
document.write( "Stack content (from top)"+
        " after function call<br>");
while (s.length!=0) {
    document.write( s[s.length-1] + " ");
    s.pop();
}

</script>
```

**Output:** 

```
Yes
Stack content (from top) after function call
6 5 11 10 -2 -3 5 4
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)
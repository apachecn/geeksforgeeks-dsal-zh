# 检查堆栈元素是否成对连续

> 原文:[https://www . geesforgeks . org/check-if-stack-elements-is-pair-continuous/](https://www.geeksforgeeks.org/check-if-stack-elements-are-pairwise-consecutive/)

给定一堆整数，编写一个函数 pair wise continuous()来检查堆栈中的数字是否成对连续。这些对可以是增加的，也可以是减少的，如果堆栈中有奇数个元素，则顶部的元素将被排除在一对元素之外。该函数应保留原始堆栈内容。
堆栈上只允许以下标准操作。

*   push(X):在堆栈顶部输入一个元素 X。
*   pop():移除堆栈的顶部元素。
*   empty():检查堆栈是否为空。

**例:**

```
Input : stack = [4, 5, -2, -3, 11, 10, 5, 6, 20]
Output : Yes
Each of the pairs (4, 5), (-2, -3), (11, 10) and
(5, 6) consists of consecutive numbers.

Input : stack = [4, 6, 6, 7, 4, 3]
Output : No
(4, 6) are not consecutive.
```

想法是使用另一个堆栈。

1.  创建一个辅助堆栈**辅助**。
2.  将给定堆栈的内容传输到**辅助**。
3.  遍历辅助。遍历提取前两个元素并检查它们是否连续。检查后，将这些元素放回原始堆栈。

## C++

```
// C++ program to check if successive
// pair of numbers in the stack are
// consecutive or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if elements are
// pairwise consecutive in stack
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
    // consecutive or not. We also
    // need to make sure that original
    // content is retained.
    bool result = true;
    while (aux.size() > 1) {

        // Fetch current top two
        // elements of aux and check
        // if they are consecutive.
        int x = aux.top();
        aux.pop();
        int y = aux.top();
        aux.pop();
        if (abs(x - y) != 1)
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
    s.push(-2);
    s.push(-3);
    s.push(11);
    s.push(10);
    s.push(5);
    s.push(6);
    s.push(20);

    if (pairWiseConsecutive(s))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    cout << "Stack content (from top)"
          " after function call\n";
    while (s.empty() == false)
    {
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
// consecutive or not
import java.util.*;
class GfG {

// Function to check if elements are
// pairwise consecutive in stack
static boolean pairWiseConsecutive(Stack<Integer> s)
{
    // Transfer elements of s to aux.
    Stack<Integer> aux = new Stack<Integer> ();
    while (!s.isEmpty()) {
        aux.push(s.peek());
        s.pop();
    }

    // Traverse aux and see if
    // elements are pairwise
    // consecutive or not. We also
    // need to make sure that original
    // content is retained.
    boolean result = true;
    while (aux.size() > 1) {

        // Fetch current top two
        // elements of aux and check
        // if they are consecutive.
        int x = aux.peek();
        aux.pop();
        int y = aux.peek();
        aux.pop();
        if (Math.abs(x - y) != 1)
        result = false;

        // Push the elements to original
        // stack.
        s.push(x);
        s.push(y);
    }

    if (aux.size() == 1)
        s.push(aux.peek());

    return result;
}

// Driver program
public static void main(String[] args)
{
    Stack<Integer> s = new Stack<Integer> ();
    s.push(4);
    s.push(5);
    s.push(-2);
    s.push(-3);
    s.push(11);
    s.push(10);
    s.push(5);
    s.push(6);
    s.push(20);

    if (pairWiseConsecutive(s))
        System.out.println("Yes");
    else
        System.out.println("No");

    System.out.println("Stack content (from top) after function call");
    while (s.isEmpty() == false)
    {
    System.out.print(s.peek() + " ");
    s.pop();
    }

}
}
```

## 蟒蛇 3

```
# Python3 program to check if successive
# pair of numbers in the stack are
# consecutive or not

# Function to check if elements are
# pairwise consecutive in stack
def pairWiseConsecutive(s):

    # Transfer elements of s to aux.
    aux = []
    while (len(s) != 0):
        aux.append(s[-1])
        s.pop()

    # Traverse aux and see if elements
    # are pairwise consecutive or not.
    # We also need to make sure that
    # original content is retained.
    result = True
    while (len(aux) > 1):

        # Fetch current top two
        # elements of aux and check
        # if they are consecutive.
        x = aux[-1]
        aux.pop()
        y = aux[-1]
        aux.pop()
        if (abs(x - y) != 1):
            result = False

        # append the elements to
        # original stack.
        s.append(x)
        s.append(y)

    if (len(aux) == 1):
        s.append(aux[-1])

    return result

# Driver Code
if __name__ == '__main__':

    s = []
    s.append(4)
    s.append(5)
    s.append(-2)
    s.append(-3)
    s.append(11)
    s.append(10)
    s.append(5)
    s.append(6)
    s.append(20)

    if (pairWiseConsecutive(s)):
        print("Yes")
    else:
        print("No")

    print("Stack content (from top)",
               "after function call")
    while (len(s) != 0):
        print(s[-1], end = " ")
        s.pop()

# This code is contributed by PranchalK
```

## C#

```
// C# program to check if successive
// pair of numbers in the stack are
// consecutive or not
using System;
using System.Collections.Generic;

class GfG
{

// Function to check if elements are
// pairwise consecutive in stack
static bool pairWiseConsecutive(Stack<int> s)
{
    // Transfer elements of s to aux.
    Stack<int> aux = new Stack<int> ();
    while (s.Count != 0)
    {
        aux.Push(s.Peek());
        s.Pop();
    }

    // Traverse aux and see if
    // elements are pairwise
    // consecutive or not. We also
    // need to make sure that original
    // content is retained.
    bool result = true;
    while (aux.Count > 1)
    {

        // Fetch current top two
        // elements of aux and check
        // if they are consecutive.
        int x = aux.Peek();
        aux.Pop();
        int y = aux.Peek();
        aux.Pop();
        if (Math.Abs(x - y) != 1)
            result = false;

        // Push the elements to original
        // stack.
        s.Push(x);
        s.Push(y);
    }

    if (aux.Count == 1)
        s.Push(aux.Peek());

    return result;
}

// Driver code
public static void Main()
{
    Stack<int> s = new Stack<int> ();
    s.Push(4);
    s.Push(5);
    s.Push(-2);
    s.Push(-3);
    s.Push(11);
    s.Push(10);
    s.Push(5);
    s.Push(6);
    s.Push(20);

    if (pairWiseConsecutive(s))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

    Console.WriteLine("Stack content (from top)" +
                        "after function call");
    while (s.Count != 0)
    {
        Console.Write(s.Peek() + " ");
        s.Pop();
    }

}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to check if successive
// pair of numbers in the stack are
// consecutive or not

// Function to check if elements are
// pairwise consecutive in stack
function pairWiseConsecutive( s)
{
    // Transfer elements of s to aux.
    var aux = [];
    while (s.length!=0) {
        aux.push(s[s.length-1]);
        s.pop();
    }

    // Traverse aux and see if
    // elements are pairwise
    // consecutive or not. We also
    // need to make sure that original
    // content is retained.
    var result = true;
    while (aux.length > 1) {

        // Fetch current top two
        // elements of aux and check
        // if they are consecutive.
        var x = aux[aux.length-1];
        aux.pop();
        var y = aux[aux.length-1];
        aux.pop();
        if (Math.abs(x - y) != 1)
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
s.push(-2);
s.push(-3);
s.push(11);
s.push(10);
s.push(5);
s.push(6);
s.push(20);
if (pairWiseConsecutive(s))
    document.write( "Yes<br>" );
else
    document.write( "No<br>" );
document.write( "Stack content (from top)"+
      " after function call<br>");
while (s.length!=0)
{
   document.write( s[s.length-1] + " ");
   s.pop();
}

</script>
```

**输出:**

```
Yes
Stack content (from top) after function call
20 6 5 10 11 -3 -2 5 4 
```

**时间复杂度:** O(n)。
**辅助空间:** O(n)。
本文由 **Prakriti Gupta** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
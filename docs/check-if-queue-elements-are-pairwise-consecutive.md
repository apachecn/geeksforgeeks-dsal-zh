# 检查队列元素是否成对连续

> 原文:[https://www . geesforgeks . org/check-if-queue-elements-is-pair-continuous/](https://www.geeksforgeeks.org/check-if-queue-elements-are-pairwise-consecutive/)

给定一个整数队列。任务是检查队列中的连续元素是否成对连续。
**例:**

```
Input : 1 2 5 6 9 10
Output : Yes

Input : 2 3 9 11 8 7
Output : No
```

**方法:**使用两个堆栈:

*   将队列的所有元素转移到一个辅助堆栈 aux。
*   现在，将元素从这个堆栈转移到另一个辅助堆栈 aux2。
*   从 aux2 开始弹出两个元素，然后检查这两个元素之间的区别。如果它们的差为 1，则继续其他对，直到堆栈中剩下一个元素。
*   此外，弹出后，将它们同时推入队列以保持原始队列。
*   最后，如果有差不等于 1 的对，返回 false，否则返回 true。

以下是上述方法的实现:

## C++

```
// C++ program to check if successive
// pair of numbers in the queue are
// consecutive or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if elements are
// pairwise consecutive in queue
bool pairWiseConsecutive(queue<int> q)
{
    // Transfer elements of q to aux.
    stack<int> aux;
    while (!q.empty()) {
        aux.push(q.front());
        q.pop();
    }

    // Again transfer the
    // elements of aux to aux2
    stack<int> aux2;
    while (!aux.empty()) {
        aux2.push(aux.top());
        aux.pop();
    }

    // Traverse aux2 and see if
    // elements are pairwise
    // consecutive or not. We also
    // need to make sure that original
    // content is retained.
    bool result = true;
    while (aux2.size() > 1) {

        // Fetch current top two
        // elements of aux2 and check
        // if they are consecutive.
        int x = aux2.top();
        aux2.pop();

        int y = aux2.top();
        aux2.pop();

        if (abs(x - y) != 1)
            result = false;

        // Push the elements to queue
        q.push(x);
        q.push(y);
    }

    if (aux2.size() == 1)
        q.push(aux2.top());

    return result;
}

// Driver program
int main()
{
    // Pushing elements into the queue
    queue<int> q;
    q.push(4);
    q.push(5);
    q.push(-2);
    q.push(-3);
    q.push(11);
    q.push(10);
    q.push(5);
    q.push(6);

    if (pairWiseConsecutive(q))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    // Printing the original queue
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if successive
// pair of numbers in the queue are
// consecutive or not

import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

public class GFG {

// Function to check if elements are
// pairwise consecutive in queue
static boolean pairWiseConsecutive(Queue<Integer> q)
{
    // Transfer elements of q to aux.
    Stack<Integer> aux = new Stack<>();
    while (!q.isEmpty()) {
        aux.push(q.peek());
        q.poll();
    }

    // Again transfer the
    // elements of aux to aux2
    Stack<Integer> aux2 = new Stack<>();
    while (!aux.empty()) {
        aux2.push(aux.peek());
        aux.pop();
    }

    // Traverse aux2 and see if
    // elements are pairwise
    // consecutive or not. We also
    // need to make sure that original
    // content is retained.
    boolean result = true;
    while (aux2.size() > 1) {

        // Fetch current top two
        // elements of aux2 and check
        // if they are consecutive.
        int x = aux2.peek();
        aux2.pop();

        int y = aux2.peek();
        aux2.pop();

        if (Math.abs(x - y) != 1)
            result = false;

        // Push the elements to queue
        q.add(x);
        q.add(y);
    }

    if (aux2.size() == 1)
        q.add(aux2.peek());

    return result;
}

// Driver program
  static public void main(String[] args) {
           // Pushing elements into the queue
    Queue<Integer> q= new LinkedList<Integer>();
    q.add(4);
    q.add(5);
    q.add(-2);
    q.add(-3);
    q.add(11);
    q.add(10);
    q.add(5);
    q.add(6);

    if (pairWiseConsecutive(q))
        System.out.println("Yes");
    else
        System.out.println("No");

    // Printing the original queue
    while (!q.isEmpty()) {
        System.out.print(q.peek() + " ");
        q.remove();
    }
    System.out.println();

    }
}
// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to check
# if successive pair of numbers
# in the queue are consecutive or not
import queue

# Function to check if elements are
# pairwise consecutive in queue
def pairWiseConsecutive(q):

    # Transfer elements of
    # q to aux.
    aux = []

    while (q.qsize() != 0):
        aux.append(q.queue[0])
        q.get()

    # Again transfer the
    # elements of aux to aux2
    aux2 = []

    while (len(aux) != 0):
        aux2.append(aux[len(aux) - 1])
        aux.pop()

    # Traverse aux2 and see if
    # elements are pairwise
    # consecutive or not. We also
    # need to make sure that original
    # content is retained.
    result = bool(True)
    while (len(aux2) > 1):

        # Fetch current top two
        # elements of aux2 and check
        # if they are consecutive.
        x = aux2[len(aux2) - 1]
        aux2.pop()

        y = aux2[len(aux2) - 1]
        aux2.pop()

        if (abs(x - y) != 1):
            result = bool(False)

        # Push the elements
        # to queue
        q.put(x)
        q.put(y)

    if (len(aux2) == 1):
        q.put(aux2[len(aux2) - 1])

    return result 

# Driver code
# Pushing elements
# into the queue
q = queue.Queue() 

q.put(4)
q.put(5)
q.put(-2)
q.put(-3)
q.put(11)
q.put(10)
q.put(5)
q.put(6)

if (pairWiseConsecutive(q)):
    print("Yes")
else:
    print("No")

# Printing the original queue
while (not q.empty()):
    print(q.queue[0] ,
          end = " ")
    q.get()

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to check if successive
// pair of numbers in the queue are
// consecutive or not
using System;
using System.Collections.Generic;

class GFG
{

// Function to check if elements are
// pairwise consecutive in queue
static Boolean pairWiseConsecutive(Queue<int> q)
{
    // Transfer elements of q to aux.
    Stack<int> aux = new Stack<int>();
    while (q.Count != 0)
    {
        aux.Push(q.Peek());
        q.Dequeue();
    }

    // Again transfer the
    // elements of aux to aux2
    Stack<int> aux2 = new Stack<int>();
    while (aux.Count != 0)
    {
        aux2.Push(aux.Peek());
        aux.Pop();
    }

    // Traverse aux2 and see if
    // elements are pairwise
    // consecutive or not. We also
    // need to make sure that original
    // content is retained.
    Boolean result = true;
    while (aux2.Count > 1)
    {

        // Fetch current top two
        // elements of aux2 and check
        // if they are consecutive.
        int x = aux2.Peek();
        aux2.Pop();

        int y = aux2.Peek();
        aux2.Pop();

        if (Math.Abs(x - y) != 1)
            result = false;

        // Push the elements to queue
        q.Enqueue(x);
        q.Enqueue(y);
    }

    if (aux2.Count == 1)
        q.Enqueue(aux2.Peek());

    return result;
}

// Driver code
static public void Main(String[] args)
{
    // Pushing elements into the queue
    Queue<int> q = new Queue<int>();
    q.Enqueue(4);
    q.Enqueue(5);
    q.Enqueue(-2);
    q.Enqueue(-3);
    q.Enqueue(11);
    q.Enqueue(10);
    q.Enqueue(5);
    q.Enqueue(6);

    if (pairWiseConsecutive(q))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

    // Printing the original queue
    while (q.Count != 0)
    {
        Console.Write(q.Peek() + " ");
        q.Dequeue();
    }
    Console.WriteLine();

    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to check if successive
// pair of numbers in the queue are
// consecutive or not

// Function to check if elements are
// pairwise consecutive in queue
function pairWiseConsecutive(q)
{
    // Transfer elements of q to aux.
    var aux = [];
    while (q.length!=0) {
        aux.push(q[0]);
        q.shift();
    }

    // Again transfer the
    // elements of aux to aux2
    var aux2 = [];
    while (aux.length!=0) {
        aux2.push(aux[aux.length-1]);
        aux.pop();
    }

    // Traverse aux2 and see if
    // elements are pairwise
    // consecutive or not. We also
    // need to make sure that original
    // content is retained.
    var result = true;
    while (aux2.length > 1) {

        // Fetch current top two
        // elements of aux2 and check
        // if they are consecutive.
        var x = aux2[aux2.length-1];
        aux2.pop();

        var y = aux2[aux2.length-1];
        aux2.pop();

        if (Math.abs(x - y) != 1)
            result = false;

        // Push the elements to queue
        q.push(x);
        q.push(y);
    }

    if (aux2.length == 1)
        q.push(aux2[aux2.length-1]);

    return result;
}

// Driver program
// Pushing elements into the queue
var q = [];
q.push(4);
q.push(5);
q.push(-2);
q.push(-3);
q.push(11);
q.push(10);
q.push(5);
q.push(6);
if (pairWiseConsecutive(q))
    document.write( "Yes<br>" );
else
    document.write( "No<br>" );
// Printing the original queue
while (q.length!=0) {
    document.write( q[0] + " ");
    q.shift();
}
document.write("<br>");

</script>
```

**输出:**

```
Yes
4 5 -2 -3 11 10 5 6 
```

**时间复杂度:** *O(n)* ，其中 n 是队列的大小。
**辅助空间:** *O(n)* ，其中 n 是堆叠的大小。
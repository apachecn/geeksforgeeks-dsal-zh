# 使用递归对队列进行排序

> 原文:[https://www . geeksforgeeks . org/使用递归对队列进行排序/](https://www.geeksforgeeks.org/sort-the-queue-using-recursion/)

给定一个队列，任务是使用递归对其进行排序，而不使用任何循环。我们只能使用队列的以下功能:

> **空(q):** 测试队列是否为空。
> **push(q):** 给队列添加新元素。
> **弹出(q):** 从队列中移除前端元素。
> **大小(q):** 返回队列中元素的数量。
> **front(q):** 返回 front 元素的值，不移除它。

**例:**

> **输入:**队列= {10，7，16，9，20，5}
> **输出:** 5 7 9 10 16 20
> **输入:**队列= {0，-2，-1，2，3，1}
> **输出:** -2 -1 0 1 2 3

**方法:**解决方案的思路是在函数调用栈中保存所有值，直到队列变空。当队列变空时，按排序顺序逐个插入所有保留的项目。在这里，排序很重要。
**如何管理排序顺序？**
每当你从函数调用栈中获取项目时，那么首先计算队列的大小，并将其与队列的元素进行比较。这里出现两种情况:

1.  如果项目(由函数调用堆栈返回)大于队列的前元素，则使前元素出列，并通过减小大小将该元素排入同一队列。
2.  如果该项目少于队列中的前元素，则将该元素排入队列，将剩余元素从队列中出队，并通过减小大小来入队重复情况 1 和 2，除非大小变为零。注意一件事，如果大小变为零，并且您的元素保持大于队列的所有元素，那么将您的元素推入队列。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to push element in last by
// popping from front until size becomes 0
void FrontToLast(queue<int>& q, int qsize)
{
    // Base condition
    if (qsize <= 0)
        return;

    // pop front element and push
    // this last in a queue
    q.push(q.front());
    q.pop();

    // Recursive call for pushing element
    FrontToLast(q, qsize - 1);
}

// Function to push an element in the queue
// while maintaining the sorted order
void pushInQueue(queue<int>& q, int temp, int qsize)
{

    // Base condition
    if (q.empty() || qsize == 0) {
        q.push(temp);
        return;
    }

    // If current element is less than
    // the element at the front
    else if (temp <= q.front()) {

        // Call stack with front of queue
        q.push(temp);

        // Recursive call for inserting a front
        // element of the queue to the last
        FrontToLast(q, qsize);
    }
    else {

        // Push front element into
        // last in a queue
        q.push(q.front());
        q.pop();

        // Recursive call for pushing
        // element in a queue
        pushInQueue(q, temp, qsize - 1);
    }
}

// Function to sort the given
// queue using recursion
void sortQueue(queue<int>& q)
{

    // Return if queue is empty
    if (q.empty())
        return;

    // Get the front element which will
    // be stored in this variable
    // throughout the recursion stack
    int temp = q.front();

    // Remove the front element
    q.pop();

    // Recursive call
    sortQueue(q);

    // Push the current element into the queue
    // according to the sorting order
    pushInQueue(q, temp, q.size());
}

// Driver code
int main()
{

    // Push elements to the queue
    queue<int> qu;
    qu.push(10);
    qu.push(7);
    qu.push(16);
    qu.push(9);
    qu.push(20);
    qu.push(5);

    // Sort the queue
    sortQueue(qu);

    // Print the elements of the
    // queue after sorting
    while (!qu.empty()) {
        cout << qu.front() << " ";
        qu.pop();
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to push element in last by
// popping from front until size becomes 0
static void FrontToLast(Queue<Integer> q,
                        int qsize)
{
    // Base condition
    if (qsize <= 0)
        return;

    // pop front element and push
    // this last in a queue
    q.add(q.peek());
    q.remove();

    // Recursive call for pushing element
    FrontToLast(q, qsize - 1);
}

// Function to push an element in the queue
// while maintaining the sorted order
static void pushInQueue(Queue<Integer> q,
                        int temp, int qsize)
{

    // Base condition
    if (q.isEmpty() || qsize == 0)
    {
        q.add(temp);
        return;
    }

    // If current element is less than
    // the element at the front
    else if (temp <= q.peek())
    {

        // Call stack with front of queue
        q.add(temp);

        // Recursive call for inserting a front
        // element of the queue to the last
        FrontToLast(q, qsize);
    }
    else
    {

        // Push front element into
        // last in a queue
        q.add(q.peek());
        q.remove();

        // Recursive call for pushing
        // element in a queue
        pushInQueue(q, temp, qsize - 1);
    }
}

// Function to sort the given
// queue using recursion
static void sortQueue(Queue<Integer> q)
{

    // Return if queue is empty
    if (q.isEmpty())
        return;

    // Get the front element which will
    // be stored in this variable
    // throughout the recursion stack
    int temp = q.peek();

    // Remove the front element
    q.remove();

    // Recursive call
    sortQueue(q);

    // Push the current element into the queue
    // according to the sorting order
    pushInQueue(q, temp, q.size());
}

// Driver code
public static void main(String[] args)
{

    // Push elements to the queue
    Queue<Integer> qu = new LinkedList<>();
    qu.add(10);
    qu.add(7);
    qu.add(16);
    qu.add(9);
    qu.add(20);
    qu.add(5);

    // Sort the queue
    sortQueue(qu);

    // Print the elements of the
    // queue after sorting
    while (!qu.isEmpty())
    {
        System.out.print(qu.peek() + " ");
        qu.remove();
    }
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# defining a class Queue
class Queue:

    def __init__(self):
        self.queue = []

    def put(self, item):
        self.queue.append(item)

    def get(self):
        if len(self.queue) < 1:
            return None
        return self.queue.pop(0)

    def front(self):
        return self.queue[0]

    def size(self):
        return len(self.queue)

    def empty(self):
        return not(len(self.queue))

# Function to push element in last by
# popping from front until size becomes 0
def FrontToLast(q, qsize) :

    # Base condition
    if qsize <= 0:
        return

    # pop front element and push
    # this last in a queue
    q.put(q.get())

    # Recursive call for pushing element
    FrontToLast(q, qsize - 1)

# Function to push an element in the queue
# while maintaining the sorted order
def pushInQueue(q, temp, qsize) :

    # Base condition
    if q.empty() or qsize == 0:
        q.put(temp)
        return

    # If current element is less than
    # the element at the front
    elif temp <= q.front() :

        # Call stack with front of queue
        q.put(temp)

        # Recursive call for inserting a front
        # element of the queue to the last
        FrontToLast(q, qsize)

    else :

        # Push front element into
        # last in a queue
        q.put(q.get())

        # Recursive call for pushing
        # element in a queue
        pushInQueue(q, temp, qsize - 1)

# Function to sort the given
# queue using recursion
def sortQueue(q):

    # Return if queue is empty
    if q.empty():
        return

    # Get the front element which will
    # be stored in this variable
    # throughout the recursion stack
    temp = q.get()

    # Recursive call
    sortQueue(q)

    # Push the current element into the queue
    # according to the sorting order
    pushInQueue(q, temp, q.size())

# Driver code
qu = Queue()

# Data is inserted into Queue
# using put() Data is inserted
# at the end
qu.put(10)
qu.put(7)
qu.put(16)
qu.put(9)
qu.put(20)
qu.put(5)

# Sort the queue
sortQueue(qu)

# Print the elements of the
# queue after sorting
while not qu.empty():
    print(qu.get(), end = ' ')

# This code is contributed by Sadik Ali
```

## C#

```
// Program to print the given pattern
using System;
using System.Collections.Generic;

class GFG
{

// Function to push element in last by
// popping from front until size becomes 0
static void FrontToLast(Queue<int> q,
                        int qsize)
{
    // Base condition
    if (qsize <= 0)
        return;

    // pop front element and push
    // this last in a queue
    q.Enqueue(q.Peek());
    q.Dequeue();

    // Recursive call for pushing element
    FrontToLast(q, qsize - 1);
}

// Function to push an element in the queue
// while maintaining the sorted order
static void pushInQueue(Queue<int> q,
                        int temp, int qsize)
{

    // Base condition
    if (q.Count == 0 || qsize == 0)
    {
        q.Enqueue(temp);
        return;
    }

    // If current element is less than
    // the element at the front
    else if (temp <= q.Peek())
    {

        // Call stack with front of queue
        q.Enqueue(temp);

        // Recursive call for inserting a front
        // element of the queue to the last
        FrontToLast(q, qsize);
    }
    else
    {

        // Push front element into
        // last in a queue
        q.Enqueue(q.Peek());
        q.Dequeue();

        // Recursive call for pushing
        // element in a queue
        pushInQueue(q, temp, qsize - 1);
    }
}

// Function to sort the given
// queue using recursion
static void sortQueue(Queue<int> q)
{

    // Return if queue is empty
    if (q.Count==0)
        return;

    // Get the front element which will
    // be stored in this variable
    // throughout the recursion stack
    int temp = q.Peek();

    // Remove the front element
    q.Dequeue();

    // Recursive call
    sortQueue(q);

    // Push the current element into the queue
    // according to the sorting order
    pushInQueue(q, temp, q.Count);
}

// Driver code
public static void Main(String[] args)
{

    // Push elements to the queue
    Queue<int> qu = new Queue<int>();
    qu.Enqueue(10);
    qu.Enqueue(7);
    qu.Enqueue(16);
    qu.Enqueue(9);
    qu.Enqueue(20);
    qu.Enqueue(5);

    // Sort the queue
    sortQueue(qu);

    // Print the elements of the
    // queue after sorting
    while (qu.Count != 0)
    {
        Console.Write(qu.Peek() + " ");
        qu.Dequeue();
    }
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to push element in last by
    // popping from front until size becomes 0
    function FrontToLast(q, qsize)
    {
        // Base condition
        if (qsize <= 0)
            return;

        // pop front element and push
        // this last in a queue
        q.push(q[0]);
        q.shift();

        // Recursive call for pushing element
        FrontToLast(q, qsize - 1);
    }

    // Function to push an element in the queue
    // while maintaining the sorted order
    function pushInQueue(q, temp, qsize)
    {

        // Base condition
        if (q.length == 0 || qsize == 0)
        {
            q.push(temp);
            return;
        }

        // If current element is less than
        // the element at the front
        else if (temp <= q[0])
        {

            // Call stack with front of queue
            q.push(temp);

            // Recursive call for inserting a front
            // element of the queue to the last
            FrontToLast(q, qsize);
        }
        else
        {

            // Push front element into
            // last in a queue
            q.push(q[0]);
            q.shift();

            // Recursive call for pushing
            // element in a queue
            pushInQueue(q, temp, qsize - 1);
        }
    }

    // Function to sort the given
    // queue using recursion
    function sortQueue(q)
    {

        // Return if queue is empty
        if (q.length==0)
            return;

        // Get the front element which will
        // be stored in this variable
        // throughout the recursion stack
        let temp = q[0];

        // Remove the front element
        q.shift();

        // Recursive call
        sortQueue(q);

        // Push the current element into the queue
        // according to the sorting order
        pushInQueue(q, temp, q.length);
    }

    // Push elements to the queue
    let qu = [];
    qu.push(10);
    qu.push(7);
    qu.push(16);
    qu.push(9);
    qu.push(20);
    qu.push(5);

    // Sort the queue
    sortQueue(qu);

    // Print the elements of the
    // queue after sorting
    while (qu.length != 0)
    {
        document.write(qu[0] + " ");
        qu.shift();
    }

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
5 7 9 10 16 20
```
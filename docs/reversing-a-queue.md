# 反转队列

> 原文:[https://www.geeksforgeeks.org/reversing-a-queue/](https://www.geeksforgeeks.org/reversing-a-queue/)

给出一个反转队列 q 的算法。在队列上只允许进行以下标准操作。

1.  入队(x):在队列后面添加一个项目 x。
2.  出列() :从队列前面移除项目。
3.  empty():检查队列是否为空。

**例:**

```
Input :  Q = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
Output : Q = [100, 90, 80, 70, 60, 50, 40, 30, 20, 10]

Input : [1, 2, 3, 4, 5]
Output : [5, 4, 3, 2, 1]
```

**方法:**为了反转队列，一种方法是将队列的元素存储在临时数据结构中，这样，如果我们在队列中重新插入元素，它们将以相反的顺序插入。所以现在我们的任务是选择这样的数据结构，它可以服务于这个目的。根据这种方法，数据结构应该具有“后进先出”的属性，因为要插入到数据结构中的最后一个元素实际上应该是反向队列的第一个元素。堆栈可以帮助解决这个问题。这将是一个两步走的过程:

1.  从队列中弹出元素并插入堆栈。(堆栈的最顶层元素是队列的最后一个元素)
2.  弹出堆栈的元素，重新插入队列。(最后一个元素是第一个插入队列的元素)

## C++

```
// CPP program to reverse a Queue
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the queue
void Print(queue<int>& Queue)
{
    while (!Queue.empty()) {
        cout << Queue.front() << " ";
        Queue.pop();
    }
}

// Function to reverse the queue
void reverseQueue(queue<int>& Queue)
{
    stack<int> Stack;
    while (!Queue.empty()) {
        Stack.push(Queue.front());
        Queue.pop();
    }
    while (!Stack.empty()) {
        Queue.push(Stack.top());
        Stack.pop();
    }
}

// Driver code
int main()
{
    queue<int> Queue;
    Queue.push(10);
    Queue.push(20);
    Queue.push(30);
    Queue.push(40);
    Queue.push(50);
    Queue.push(60);
    Queue.push(70);
    Queue.push(80);
    Queue.push(90);
    Queue.push(100);

    reverseQueue(Queue);
    Print(Queue);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse a Queue
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

// Java program to reverse a queue
public class Queue_reverse {

    static Queue<Integer> queue;

    // Utility function to print the queue
    static void Print()
    {
        while (!queue.isEmpty()) {
            System.out.print( queue.peek() + ", ");
            queue.remove();
        }
    }

    // Function to reverse the queue
    static void reversequeue()
    {
        Stack<Integer> stack = new Stack<>();
        while (!queue.isEmpty()) {
            stack.add(queue.peek());
            queue.remove();
        }
        while (!stack.isEmpty()) {
            queue.add(stack.peek());
            stack.pop();
        }
    }

    // Driver code
    public static void main(String args[])
    {
        queue = new LinkedList<Integer>();
        queue.add(10);
        queue.add(20);
        queue.add(30);
        queue.add(40);
        queue.add(50);
        queue.add(60);
        queue.add(70);
        queue.add(80);
        queue.add(90);
        queue.add(100);

        reversequeue();
        Print();
    }
}
//This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to reverse a queue
from queue import Queue

# Utility function to print the queue
def Print(queue):
    while (not queue.empty()):
        print(queue.queue[0], end = ", ")
        queue.get()

# Function to reverse the queue
def reversequeue(queue):
    Stack = []
    while (not queue.empty()):
        Stack.append(queue.queue[0])
        queue.get()
    while (len(Stack) != 0):
        queue.put(Stack[-1])
        Stack.pop()

# Driver code
if __name__ == '__main__':
    queue = Queue()
    queue.put(10)
    queue.put(20)
    queue.put(30)
    queue.put(40)
    queue.put(50)
    queue.put(60)
    queue.put(70)
    queue.put(80)
    queue.put(90)
    queue.put(100)

    reversequeue(queue)
    Print(queue)

# This code is contributed by PranchalK
```

## C#

```
// c# program to reverse a Queue
using System;
using System.Collections.Generic;

public class GFG
{

public static LinkedList<int> queue;

// Utility function to print the queue
public static void Print()
{
    while (queue.Count > 0)
    {
        Console.Write(queue.First.Value + ", ");
        queue.RemoveFirst();
    }
}

// Function to reverse the queue
public static void reversequeue()
{
    Stack<int> stack = new Stack<int>();
    while (queue.Count > 0)
    {
        stack.Push(queue.First.Value);
        queue.RemoveFirst();
    }
    while (stack.Count > 0)
    {
        queue.AddLast(stack.Peek());
        stack.Pop();
    }
}

// Driver code
public static void Main(string[] args)
{
    queue = new LinkedList<int>();
    queue.AddLast(10);
    queue.AddLast(20);
    queue.AddLast(30);
    queue.AddLast(40);
    queue.AddLast(50);
    queue.AddLast(60);
    queue.AddLast(70);
    queue.AddLast(80);
    queue.AddLast(90);
    queue.AddLast(100);

    reversequeue();
    Print();
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript program to reverse a Queue

    let queue = [];

    // Utility function to print the queue
    function Print()
    {
        while (queue.length > 0) {
            document.write( queue[0] + ", ");
            queue.shift();
        }
    }

    // Function to reverse the queue
    function reversequeue()
    {
        let stack = [];
        while (queue.length > 0) {
            stack.push(queue[0]);
            queue.shift();
        }
        while (stack.length > 0) {
            queue.push(stack[stack.length - 1]);
            stack.pop();
        }
    }

    queue = []
    queue.push(10);
    queue.push(20);
    queue.push(30);
    queue.push(40);
    queue.push(50);
    queue.push(60);
    queue.push(70);
    queue.push(80);
    queue.push(90);
    queue.push(100);

    reversequeue();
    Print();

</script>
```

**输出:**

```
100, 90, 80, 70, 60, 50, 40, 30, 20, 10
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    因为我们需要将堆栈中的所有元素插入到队列中。
*   **辅助空间:** O(N)。
    使用堆栈存储值。

本文由 **Raghav Sharma** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
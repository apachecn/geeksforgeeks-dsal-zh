# 反转队列的前 K 个元素

> 原文:[https://www . geesforgeks . org/reversing-first-k-elements-queue/](https://www.geeksforgeeks.org/reversing-first-k-elements-queue/)

给定一个整数 k 和一个整数的[队列](https://www.geeksforgeeks.org/queue-data-structure/)，我们需要颠倒队列前 k 个元素的顺序，让其他元素保持相同的相对顺序。
仅允许在队列中执行以下标准操作。

*   入队(x):将项目 x 添加到队列的后面
*   出列() :从队列前面移除项目
*   size():返回队列中的元素数。
*   front():查找前端项目。

**示例:**

```
Input : Q = [10, 20, 30, 40, 50, 60, 
            70, 80, 90, 100]
        k = 5
Output : Q = [50, 40, 30, 20, 10, 60, 
             70, 80, 90, 100]

Input : Q = [10, 20, 30, 40, 50, 60, 
            70, 80, 90, 100]
        k = 4
Output : Q = [40, 30, 20, 10, 50, 60, 
             70, 80, 90, 100]
```

想法是用一个辅助[叠加](https://www.geeksforgeeks.org/stack-data-structure/)。

1.  创建一个空堆栈。
2.  逐个从给定队列中取出前 K 个项目，并将取出的项目推入堆栈。
3.  将堆栈的内容排列在队列的后面
4.  将(size-k)元素从前面出队，并将它们一个接一个地排入同一个队列。

## C++

```
// C++ program to reverse first
// k elements of a queue.
#include <bits/stdc++.h>
using namespace std;

/* Function to reverse the first
   K elements of the Queue */
void reverseQueueFirstKElements(
    int k, queue<int>& Queue)
{
    if (Queue.empty() == true
        || k > Queue.size())
        return;
    if (k <= 0)
        return;

    stack<int> Stack;

    /* Push the first K elements
       into a Stack*/
    for (int i = 0; i < k; i++) {
        Stack.push(Queue.front());
        Queue.pop();
    }

    /* Enqueue the contents of stack
       at the back of the queue*/
    while (!Stack.empty()) {
        Queue.push(Stack.top());
        Stack.pop();
    }

    /* Remove the remaining elements and
       enqueue them at the end of the Queue*/
    for (int i = 0; i < Queue.size() - k; i++) {
        Queue.push(Queue.front());
        Queue.pop();
    }
}

/* Utility Function to print the Queue */
void Print(queue<int>& Queue)
{
    while (!Queue.empty()) {
        cout << Queue.front() << " ";
        Queue.pop();
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

    int k = 5;
    reverseQueueFirstKElements(k, Queue);
    Print(Queue);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse first k elements
// of a queue.
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

public class Reverse_k_element_queue {

    static Queue<Integer> queue;

    // Function to reverse the first
    // K elements of the Queue
    static void reverseQueueFirstKElements(int k)
    {
        if (queue.isEmpty() == true
            || k > queue.size())
            return;
        if (k <= 0)
            return;

        Stack<Integer> stack = new Stack<Integer>();

        // Push the first K elements into a Stack
        for (int i = 0; i < k; i++) {
            stack.push(queue.peek());
            queue.remove();
        }

        // Enqueue the contents of stack
        // at the back of the queue
        while (!stack.empty()) {
            queue.add(stack.peek());
            stack.pop();
        }

        // Remove the remaining elements and enqueue
        // them at the end of the Queue
        for (int i = 0; i < queue.size() - k; i++) {
            queue.add(queue.peek());
            queue.remove();
        }
    }

    // Utility Function to print the Queue
    static void Print()
    {
        while (!queue.isEmpty()) {
            System.out.print(queue.peek() + " ");
            queue.remove();
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

        int k = 5;
        reverseQueueFirstKElements(k);
        Print();
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to reverse first k
# elements of a queue.
from queue import Queue

# Function to reverse the first K
# elements of the Queue
def reverseQueueFirstKElements(k, Queue):
    if (Queue.empty() == True or
             k > Queue.qsize()):
        return
    if (k <= 0):
        return

    Stack = []

    # put the first K elements
    # into a Stack
    for i in range(k):
        Stack.append(Queue.queue[0])
        Queue.get()

    # Enqueue the contents of stack
    # at the back of the queue
    while (len(Stack) != 0 ):
        Queue.put(Stack[-1])
        Stack.pop()

    # Remove the remaining elements and
    # enqueue them at the end of the Queue
    for i in range(Queue.qsize() - k):
        Queue.put(Queue.queue[0])
        Queue.get()

# Utility Function to print the Queue
def Print(Queue):
    while (not Queue.empty()):
        print(Queue.queue[0], end =" ")
        Queue.get()

# Driver code
if __name__ == '__main__':
    Queue = Queue()
    Queue.put(10)
    Queue.put(20)
    Queue.put(30)
    Queue.put(40)
    Queue.put(50)
    Queue.put(60)
    Queue.put(70)
    Queue.put(80)
    Queue.put(90)
    Queue.put(100)

    k = 5
    reverseQueueFirstKElements(k, Queue)
    Print(Queue)

# This code is contributed by PranchalK
```

## C#

```
// C# program to reverse first k elements
// of a queue.
using System;
using System.Collections.Generic;

class GFG {

    public static LinkedList<int> queue;

    // Function to reverse the first K
    // elements of the Queue
    public static void reverseQueueFirstKElements(int k)
    {
        if (queue.Count == 0 || k > queue.Count) {
            return;
        }
        if (k <= 0) {
            return;
        }

        Stack<int> stack = new Stack<int>();

        // Push the first K elements into a Stack
        for (int i = 0; i < k; i++) {
            stack.Push(queue.First.Value);
            queue.RemoveFirst();
        }

        // Enqueue the contents of stack at
        // the back of the queue
        while (stack.Count > 0) {
            queue.AddLast(stack.Peek());
            stack.Pop();
        }

        // Remove the remaining elements and
        // enqueue them at the end of the Queue
        for (int i = 0; i < queue.Count - k; i++) {
            queue.AddLast(queue.First.Value);<li><strong>Complexity Analysis:</strong>
<strong>Time Complexity:</strong> O(n<sup>3</sup>).
As three nested for loops are used.
<strong>Auxiliary Space :</strong>No use of any data structure for storing values-: O(1)
</li>
        queue.RemoveFirst();
        }
    }

    // Utility Function to print the Queue
    public static void Print()
    {
        while (queue.Count > 0) {
            Console.Write(queue.First.Value + " ");
            queue.RemoveFirst();
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

        int k = 5;
        reverseQueueFirstKElements(k);
        Print();
    }
}

// This code is contributed by Shrikant13
```

**Output:** 

```
50 40 30 20 10 60 70 80 90 100
```

**复杂度分析:**

*   **时间复杂度:** O(n+k)。
    其中“n”是队列中元素的总数，“k”是要反转的元素数。这是因为首先整个队列被清空到堆栈中，然后第一个“k”元素被清空并以相同的方式排队。
*   **辅助空间:**使用堆栈存储值，目的是反转-: O(n)

-s
本文由**拉格哈夫·夏尔马**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
# 将队列的前半部分与后半部分交错

> 原文:[https://www . geesforgeks . org/interlace-前半部分-队列-后半部分/](https://www.geeksforgeeks.org/interleave-first-half-queue-second-half/)

给定一个偶数长度的整数队列，通过交错队列的前半部分和后半部分来重新排列元素。

只有一个栈可以作为辅助空间。

**示例:**

```
Input :  1 2 3 4
Output : 1 3 2 4

Input : 11 12 13 14 15 16 17 18 19 20
Output : 11 16 12 17 13 18 14 19 15 20

```

以下是解决问题的步骤:
1。将队列的前半部分元素推入堆栈。
2。将堆栈元素排入队列。
3。将队列的前半部分元素出队，然后将它们重新入队。
4。再次将前半部分元素推入堆栈。
5。交错队列和堆栈的元素。

## C++

```
// C++ program to interleave the first half of the queue
// with the second half
#include <bits/stdc++.h>
using namespace std;

// Function to interleave the queue
void interLeaveQueue(queue<int>& q)
{
    // To check the even number of elements
    if (q.size() % 2 != 0)
        cout << "Input even number of integers." << endl;

    // Initialize an empty stack of int type
    stack<int> s;
    int halfSize = q.size() / 2;

    // Push first half elements into the stack
    // queue:16 17 18 19 20, stack: 15(T) 14 13 12 11
    for (int i = 0; i < halfSize; i++) {
        s.push(q.front());
        q.pop();
    }

    // enqueue back the stack elements
    // queue: 16 17 18 19 20 15 14 13 12 11
    while (!s.empty()) {
        q.push(s.top());
        s.pop();
    }

    // dequeue the first half elements of queue
    // and enqueue them back
    // queue: 15 14 13 12 11 16 17 18 19 20
    for (int i = 0; i < halfSize; i++) {
        q.push(q.front());
        q.pop();
    }

    // Again push the first half elements into the stack
    // queue: 16 17 18 19 20, stack: 11(T) 12 13 14 15
    for (int i = 0; i < halfSize; i++) {
        s.push(q.front());
        q.pop();
    }

    // interleave the elements of queue and stack
    // queue: 11 16 12 17 13 18 14 19 15 20
    while (!s.empty()) {
        q.push(s.top());
        s.pop();
        q.push(q.front());
        q.pop();
    }
}

// Driver program to test above function
int main()
{
    queue<int> q;
    q.push(11);
    q.push(12);
    q.push(13);
    q.push(14);
    q.push(15);
    q.push(16);
    q.push(17);
    q.push(18);
    q.push(19);
    q.push(20);
    interLeaveQueue(q);
    int length = q.size();
    for (int i = 0; i < length; i++) {
        cout << q.front() << " ";
        q.pop();
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to interleave
// the first half of the queue
// with the second half
import java.util.*;

class GFG 
{

// Function to interleave the queue
static void interLeaveQueue(Queue<Integer>q)
{
    // To check the even number of elements
    if (q.size() % 2 != 0)
        System.out.println("Input even number of integers." );

    // Initialize an empty stack of int type
    Stack<Integer> s = new Stack<>();
    int halfSize = q.size() / 2;

    // Push first half elements into the stack
    // queue:16 17 18 19 20, stack: 15(T) 14 13 12 11
    for (int i = 0; i < halfSize; i++)
    {
        s.push(q.peek());
        q.poll();
    }

    // enqueue back the stack elements
    // queue: 16 17 18 19 20 15 14 13 12 11
    while (!s.empty()) 
    {
        q.add(s.peek());
        s.pop();
    }

    // dequeue the first half elements of queue
    // and enqueue them back
    // queue: 15 14 13 12 11 16 17 18 19 20
    for (int i = 0; i < halfSize; i++) 
    {
        q.add(q.peek());
        q.poll();
    }

    // Again push the first half elements into the stack
    // queue: 16 17 18 19 20, stack: 11(T) 12 13 14 15
    for (int i = 0; i < halfSize; i++)
    {
        s.push(q.peek());
        q.poll();
    }

    // interleave the elements of queue and stack
    // queue: 11 16 12 17 13 18 14 19 15 20
    while (!s.empty())
    {
        q.add(s.peek());
        s.pop();
        q.add(q.peek());
        q.poll();
    }
}

// Driver code
public static void main(String[] args) 
{
    Queue<Integer> q = new java.util.LinkedList<>();
    q.add(11);
    q.add(12);
    q.add(13);
    q.add(14);
    q.add(15);
    q.add(16);
    q.add(17);
    q.add(18);
    q.add(19);
    q.add(20);
    interLeaveQueue(q);
    int length = q.size();
    for (int i = 0; i < length; i++) 
    {
        System.out.print(q.peek() + " ");
        q.poll();
    }
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to interleave the first 
# half of the queue with the second half 
from queue import Queue 

# Function to interleave the queue 
def interLeaveQueue(q):

    # To check the even number of elements 
    if (q.qsize() % 2 != 0): 
        print("Input even number of integers.")

    # Initialize an empty stack of int type 
    s = []
    halfSize = int(q.qsize() / 2) 

    # put first half elements into 
    # the stack queue:16 17 18 19 20, 
    # stack: 15(T) 14 13 12 11
    for i in range(halfSize):
        s.append(q.queue[0]) 
        q.get()

    # enqueue back the stack elements 
    # queue: 16 17 18 19 20 15 14 13 12 11 
    while len(s) != 0: 
        q.put(s[-1]) 
        s.pop()

    # dequeue the first half elements of 
    # queue and enqueue them back 
    # queue: 15 14 13 12 11 16 17 18 19 20
    for i in range(halfSize):
        q.put(q.queue[0]) 
        q.get()

    # Again put the first half elements into 
    # the stack queue: 16 17 18 19 20,
    # stack: 11(T) 12 13 14 15 
    for i in range(halfSize):
        s.append(q.queue[0]) 
        q.get()

    # interleave the elements of queue and stack 
    # queue: 11 16 12 17 13 18 14 19 15 20 
    while len(s) != 0: 
        q.put(s[-1]) 
        s.pop() 
        q.put(q.queue[0]) 
        q.get()

# Driver Code
if __name__ == '__main__':
    q = Queue()
    q.put(11) 
    q.put(12) 
    q.put(13) 
    q.put(14) 
    q.put(15) 
    q.put(16) 
    q.put(17) 
    q.put(18) 
    q.put(19) 
    q.put(20) 
    interLeaveQueue(q) 
    length = q.qsize()
    for i in range(length):
        print(q.queue[0], end = " ") 
        q.get()

# This code is contributed by PranchalK
```

## C#

```
// C# program to interleave
// the first half of the queue
// with the second half
using System;
using System.Collections.Generic;

class GFG 
{

// Function to interleave the queue
static void interLeaveQueue(Queue<int>q)
{
    // To check the even number of elements
    if (q.Count % 2 != 0)
        Console.WriteLine("Input even number of integers." );

    // Initialize an empty stack of int type
    Stack<int> s = new Stack<int>();
    int halfSize = q.Count / 2;

    // Push first half elements into the stack
    // queue:16 17 18 19 20, stack: 15(T) 14 13 12 11
    for (int i = 0; i < halfSize; i++)
    {
        s.Push(q.Peek());
        q.Dequeue();
    }

    // enqueue back the stack elements
    // queue: 16 17 18 19 20 15 14 13 12 11
    while (s.Count != 0) 
    {
        q.Enqueue(s.Peek());
        s.Pop();
    }

    // dequeue the first half elements of queue
    // and enqueue them back
    // queue: 15 14 13 12 11 16 17 18 19 20
    for (int i = 0; i < halfSize; i++) 
    {
        q.Enqueue(q.Peek());
        q.Dequeue();
    }

    // Again push the first half elements into the stack
    // queue: 16 17 18 19 20, stack: 11(T) 12 13 14 15
    for (int i = 0; i < halfSize; i++)
    {
        s.Push(q.Peek());
        q.Dequeue();
    }

    // interleave the elements of queue and stack
    // queue: 11 16 12 17 13 18 14 19 15 20
    while (s.Count != 0)
    {
        q.Enqueue(s.Peek());
        s.Pop();
        q.Enqueue(q.Peek());
        q.Dequeue();
    }
}

// Driver code
public static void Main(String[] args) 
{
    Queue<int> q = new Queue<int>();
    q.Enqueue(11);
    q.Enqueue(12);
    q.Enqueue(13);
    q.Enqueue(14);
    q.Enqueue(15);
    q.Enqueue(16);
    q.Enqueue(17);
    q.Enqueue(18);
    q.Enqueue(19);
    q.Enqueue(20);
    interLeaveQueue(q);
    int length = q.Count;
    for (int i = 0; i < length; i++) 
    {
        Console.Write(q.Peek() + " ");
        q.Dequeue();
    }
}
}

// This code is contributed by Princi Singh
```

**Output:**

```
11 16 12 17 13 18 14 19 15 20 

```

**时间复杂度:** O(n)。
**辅助空间:** O(n)。

本文由 **Prakriti Gupta** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
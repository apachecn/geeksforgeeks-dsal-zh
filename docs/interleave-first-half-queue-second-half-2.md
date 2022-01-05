# 将队列的前半部分与后半部分交错

> 原文:[https://www . geesforgeks . org/interlace-前半部分-队列-后半部分-2/](https://www.geeksforgeeks.org/interleave-first-half-queue-second-half-2/)

给定一个偶数长度的整数队列，通过交错队列的前半部分和后半部分来重新排列元素。我们只能使用队列数据结构。
示例:

```
Input :  1 2 3 4
Output : 1 3 2 4

Input : 11 12 13 14 15 16 17 18 19 20
Output : 11 16 12 17 13 18 14 19 15 20
```

创建两个辅助队列 q1 和 q2。将前半部分插入一个队列 q1，另一半插入另一个队列 q2。现在，通过交替从 q1 和 q2 中选择元素，将它们插入给定的队列。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to interleave queue elements
// using only queue data structure.
#include <bits/stdc++.h>
using namespace std;

void interleave(queue<int> &q)
{
    queue<int> q1, q2;

    int n = q.size();

    // Insert first half in q1
    for (int i = 0; i < n / 2; i++) {
        q1.push(q.front());
        q.pop();
    }

    // insert second half in q2
    for (int i = 0; i < n / 2; i++) {
        q2.push(q.front());
        q.pop();
    }

    // Insert elements of q1 and q2 back
    // to q in alternate order.
    for (int i = 0; i < n/2; i++) {
        q.push(q1.front());
        q1.pop();
        q.push(q2.front());
        q2.pop();
    }
}

// Driver code
int main()
{
    // Creating an example queue with 10
    // elements.
    queue<int> q;
    for (int i = 1; i <= 10; i++)
        q.push(i); 

    interleave(q);

    // Printing queue elements
    int n = q.size();
    for (int i = 0; i < n; i++) {
        cout << q.front() << " ";
        q.pop();
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to interleave queue elements
// using only queue data structure.
import java.util.LinkedList;
import java.util.Queue;

public class GFG {

    static void interleave(Queue<Integer> q)
    {
        Queue<Integer> q1, q2;
        q1 = new LinkedList<Integer>();
        q2 = new LinkedList<Integer>();

        int n = q.size();

        // Insert first half in q1
        for (int i = 0; i < n / 2; i++) {
            q1.add(q.peek());
            q.poll();
        }

        // insert second half in q2
        for (int i = 0; i < n / 2; i++) {
            q2.add(q.peek());
            q.poll();
        }

        // Insert elements of q1 and q2 back
        // to q in alternate order.
        for (int i = 0; i < n / 2; i++) {
            q.add(q1.peek());
            q1.poll();
            q.add(q2.peek());
            q2.poll();
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // Creating an example queue with 10
        // elements.
        Queue<Integer> q = new LinkedList<Integer>();
        for (int i = 1; i <= 10; i++)
            q.add(i);

        interleave(q);

        // Printing queue elements
        int n = q.size();
        for (int i = 0; i < n; i++) {
            System.out.print(q.peek() + " ");
            q.poll();
        }
    }
}

// This code is contributed by jainlovely450
```

## 蟒蛇 3

```
# Python3 program to interleave the first
# half of the queue with the second half
from queue import Queue

# Function to interleave the queue
def interLeaveQueue(q):

    # Initialize an empty stack of int type
    q1 = Queue()
    q2 = Queue()
    halfSize = int(q.qsize() / 2)

    # Insert first half in q1
    for i in range(halfSize):
        q1.put(q.queue[0])
        q.get()

    # Insert second half in q2
    for i in range(halfSize):
        q2.put(q.queue[0])
        q.get()

    # Insert elements of q1 and q2 back
    # to q in alternate order
    for i in range(halfSize):
        q.put(q1.queue[0])
        q1.get()
        q.put(q2.queue[0])
        q2.get()

# Driver Code
if __name__ == '__main__':
    q = Queue()
    q.put(1)
    q.put(2)
    q.put(3)
    q.put(4)
    q.put(5)
    q.put(6)
    q.put(7)
    q.put(8)
    q.put(9)
    q.put(10)
    interLeaveQueue(q)
    length = q.qsize()
    for i in range(length):
        print(q.queue[0], end=" ")
        q.get()

# This code is contributed by jainlovely450
```

**Output:** 

```
1 6 2 7 3 8 4 9 5 10
```
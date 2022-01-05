# 使用另一个队列反转一个队列

> 原文:[https://www . geesforgeks . org/reversing-a-queue-use-other-queue/](https://www.geeksforgeeks.org/reversing-a-queue-using-another-queue/)

给定一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)。任务是使用另一个空队列来反转队列。

**示例:**

```
Input: queue[] = {1, 2, 3, 4, 5}
Output: 5 4 3 2 1

Input: queue[] = {10, 20, 30, 40}
Output: 40 30 20 10
```

**进场:**

*   给定一个队列和一个空队列。
*   队列的最后一个元素应该是新队列的第一个元素。
*   要获取最后一个元素，需要逐个弹出队列，并将其添加到队列的末尾，**size–1**次。
*   之后，我们将获得队列前面的最后一个元素。现在将该元素弹出，并将其添加到新队列中。重复步骤**s–1**次，其中 **s** 是队列的原始大小。

以下是该方法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the reversed queue
queue<int> reverse(queue<int> q)
{
    // Size of queue
    int s = q.size();

    // Second queue
    queue<int> ans;

    for (int i = 0; i < s; i++) {

        // Get the last element to the
        // front of queue
        for (int j = 0; j < q.size() - 1; j++) {
            int x = q.front();
            q.pop();
            q.push(x);
        }

        // Get the last element and
        // add it to the new queue
        ans.push(q.front());
        q.pop();
    }
    return ans;
}

// Driver Code
int main()
{
    queue<int> q;

    // Insert elements
    q.push(1);
    q.push(2);
    q.push(3);
    q.push(4);
    q.push(5);

    q = reverse(q);

    // Print the queue
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GFG
{

// Function to return the reversed queue
static Queue<Integer> reverse(Queue<Integer> q)
{
    // Size of queue
    int s = q.size();

    // Second queue
    Queue<Integer> ans = new LinkedList<>();

    for (int i = 0; i < s; i++)
    {

        // Get the last element to the
        // front of queue
        for (int j = 0; j < q.size() - 1; j++)
        {
            int x = q.peek();
            q.remove();
            q.add(x);
        }

        // Get the last element and
        // add it to the new queue
        ans.add(q.peek());
        q.remove();
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    Queue<Integer> q = new LinkedList<>();

    // Insert elements
    q.add(1);
    q.add(2);
    q.add(3);
    q.add(4);
    q.add(5);

    q = reverse(q);

    // Print the queue
    while (!q.isEmpty())
    {
        System.out.print(q.peek() + " ");
        q.remove();
    }
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from collections import deque

# Function to return the reversed queue
def reverse(q):

    # Size of queue
    s = len(q)

    # Second queue
    ans = deque()

    for i in range(s):

        # Get the last element to the
        # front of queue
        for j in range(s - 1):
            x = q.popleft()
            q.appendleft(x)

        # Get the last element and
        # add it to the new queue
        ans.appendleft(q.popleft())
    return ans

# Driver Code
q = deque()

# Insert elements
q.append(1)
q.append(2)
q.append(3)
q.append(4)
q.append(5)

q = reverse(q)

# Print the queue
while (len(q) > 0):
    print(q.popleft(), end = " ")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# Program to print the given pattern
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the reversed queue
static Queue<int> reverse(Queue<int> q)
{
    // Size of queue
    int s = q.Count;

    // Second queue
    Queue<int> ans = new Queue<int>();

    for (int i = 0; i < s; i++)
    {

        // Get the last element to the
        // front of queue
        for (int j = 0; j < q.Count - 1; j++)
        {
            int x = q.Peek();
            q.Dequeue();
            q.Enqueue(x);
        }

        // Get the last element and
        // add it to the new queue
        ans.Enqueue(q.Peek());
        q.Dequeue();
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    Queue<int> q = new Queue<int>();

    // Insert elements
    q.Enqueue(1);
    q.Enqueue(2);
    q.Enqueue(3);
    q.Enqueue(4);
    q.Enqueue(5);

    q = reverse(q);

    // Print the queue
    while (q.Count!=0)
    {
        Console.Write(q.Peek() + " ");
        q.Dequeue();
    }
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the reversed queue
function reverse(q)
{

    // Size of queue
    let s = q.length;

    // Second queue
    let ans = [];

    for(let i = 0; i < s; i++)
    {

        // Get the last element to the
        // front of queue
        for(let j = 0; j < q.length - 1; j++)
        {
            let x = q.shift();
            q.push(x);
        }

        // Get the last element and
        // add it to the new queue
        ans.push(q[0]);
        q.shift();
    }
    return ans;
}

// Driver Code
let q = [];

// Insert elements
q.push(1);
q.push(2);
q.push(3);
q.push(4);
q.push(5);

q = reverse(q);

// Print the queue
while (q.length != 0)
{
    document.write(q[0] + " ");
    q.shift();
}

// This code is contributed by patel2127

</script>
```

**Output:** 

```
5 4 3 2 1
```
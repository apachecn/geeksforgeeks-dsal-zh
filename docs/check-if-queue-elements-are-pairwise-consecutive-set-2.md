# 检查队列元素是否成对连续| Set-2

> 原文:[https://www . geesforgeks . org/check-if-queue-elements-is-pair-continuous-set-2/](https://www.geeksforgeeks.org/check-if-queue-elements-are-pairwise-consecutive-set-2/)

给定一个整数队列。任务是检查队列中的连续元素是否成对连续。

**示例:**

```
Input: 1 2 5 6 9 10
Output: Yes

Input: 2 3 9 11 8 7
Output: No
```

**进场:**

*   取一个变量 n 来存储队列的大小。
*   将一个元素推送到充当标记的队列中。
*   现在，如果队列的大小是奇数，当 n > 2 时开始弹出一对。此外，弹出这些对时，检查它们的差异，并将 n 减少 2，如果差异不等于 1，则将 flag 设置为 false。
*   如果队列大小相等，当 n > 1 时开始弹出一对。此外，弹出这些对时，检查它们的差异，并将 n 减少 2，如果它们的差异不等于 1，则将 flag 设置为 false。
*   最后，检查标志，如果为真，表示队列中的元素是成对排序的，否则不是。

下面是上述方法的实现:

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
    // Fetching size of queue
    int n = q.size();

    // Pushing extra element to the queue
    // which acts as marker
    q.push(INT_MIN);

    // Result flag
    bool result = true;

    // If number of elements in the
    // queue is odd pop elements while
    // its size is greater than 2.
    // Else, pop elements while its
    // size is greater than 1
    if (n % 2 != 0) {

        while (n > 2) {
            int x = q.front();
            q.pop();
            q.push(x);
            n--;

            int y = q.front();
            q.pop();
            q.push(y);
            n--;

            if (abs(x - y) != 1) {
                result = false;
            }
        }

        // Popping the last element of queue
        // and pushing it again.
        // Also, popping the extra element
        // that we have pushed as marker
        q.push(q.front());
        q.pop();
        q.pop();
    }

    else {
        while (n > 1) {
            int x = q.front();
            q.pop();
            q.push(x);
            n--;

            int y = q.front();
            q.pop();
            q.push(y);
            n--;

            if (abs(x - y) != 1) {
                result = false;
            }
        }

        // popping the extra element that
        // we have pushed as marker
        q.pop();
    }

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
    q.push(8);

    if (pairWiseConsecutive(q))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.LinkedList;
import java.util.Queue;

// Java program to check if successive
// pair of numbers in the queue are
// consecutive or not
public class GFG {

// Function to check if elements are
// pairwise consecutive in queue
    static boolean pairWiseConsecutive(Queue<Integer> q) {
        // Fetching size of queue
        int n = q.size();

        // Pushing extra element to the queue
        // which acts as marker
        q.add(Integer.MAX_VALUE);

        // Result flag
        boolean result = true;

        // If number of elements in the
        // queue is odd pop elements while
        // its size is greater than 2.
        // Else, pop elements while its
        // size is greater than 1
        if (n % 2 != 0) {

            while (n > 2) {
                int x = q.peek();
                q.remove();
                q.add(x);
                n--;

                int y = q.peek();
                q.remove();
                q.add(y);
                n--;

                if (Math.abs(x - y) != 1) {
                    result = false;
                }
            }

            // Popping the last element of queue
            // and pushing it again.
            // Also, popping the extra element
            // that we have pushed as marker
            q.add(q.peek());
            q.remove();
            q.remove();
        } else {
            while (n > 1) {
                int x = q.peek();
                q.remove();
                q.add(x);
                n--;

                int y = q.peek();
                q.remove();
                q.add(y);
                n--;

                if (Math.abs(x - y) != 1) {
                    result = false;
                }
            }

            // popping the extra element that
            // we have pushed as marker
            q.remove();
        }

        return result;
    }

// Driver program
    static public void main(String[] args) {
        // Pushing elements into the queue
        Queue<Integer> q = new LinkedList<>();
        q.add(4);
        q.add(5);
        q.add(-2);
        q.add(-3);
        q.add(11);
        q.add(10);
        q.add(5);
        q.add(6);
        q.add(8);

        if (pairWiseConsecutive(q)) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }

    }
}
// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to check if successive
# pair of numbers in the queue are
# consecutive or not
import sys, queue

# Function to check if elements are
# pairwise consecutive in queue
def pairWiseConsecutive(q):

    # Fetching size of queue
    n = q.qsize()

    # Pushing extra element to the
    # queue which acts as marker
    q.put(-sys.maxsize);

    # Result flag
    result = bool(True)

    # If number of elements in the
    # queue is odd pop elements while
    # its size is greater than 2.
    # Else, pop elements while its
    # size is greater than 1
    if (n % 2 != 0):
        while (n > 2):
            x = q.queue[0]
            q.get()
            q.put(x)
            n -= 1

            y = q.queue[0]
            q.get()
            q.put(y)
            n -= 1

            if (abs(x - y) != 1):
                result = bool(False)

        # Popping the last element of queue
        # and pushing it again.
        # Also, popping the extra element
        # that we have pushed as marker
        q.put(q.queue[0])
        q.get()
        q.get()

    else:
        while (n > 1):
            x = q.queue[0]
            q.get()
            q.put(x)
            n -= 1

            y = q.queue[0] 
            q.get()
            q.put(y)
            n -= 1

            if (abs(x - y) != 1):
                result = bool(False)

        # popping the extra element that
        # we have pushed as marker
        q.get()

    return result

# Driver code

# Pushing elements into the queue
q = queue.Queue()
q.put(4)
q.put(5)
q.put(-2)
q.put(-3)
q.put(11)
q.put(10)
q.put(5)
q.put(6)
q.put(8)

if (bool(pairWiseConsecutive(q))):
    print("Yes")
else:
    print("No")

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
        // Fetching size of queue
        int n = q.Count;

        // Pushing extra element to the queue
        // which acts as marker
        q.Enqueue(int.MaxValue);

        // Result flag
        Boolean result = true;

        // If number of elements in the
        // queue is odd pop elements while
        // its size is greater than 2.
        // Else, pop elements while its
        // size is greater than 1
        if (n % 2 != 0)
        {
            while (n > 2)
            {
                int x = q.Peek();
                q.Dequeue();
                q.Enqueue(x);
                n--;

                int y = q.Peek();
                q.Dequeue();
                q.Enqueue(y);
                n--;

                if (Math.Abs(x - y) != 1)
                {
                    result = false;
                }
            }

            // Popping the last element of queue
            // and pushing it again.
            // Also, popping the extra element
            // that we have pushed as marker
            q.Enqueue(q.Peek());
            q.Dequeue();
            q.Dequeue();
        } else
        {
            while (n > 1)
            {
                int x = q.Peek();
                q.Dequeue();
                q.Enqueue(x);
                n--;

                int y = q.Peek();
                q.Dequeue();
                q.Enqueue(y);
                n--;

                if (Math.Abs(x - y) != 1)
                {
                    result = false;
                }
            }

            // popping the extra element that
            // we have pushed as marker
            q.Dequeue();
        }

        return result;
    }

    // Driver Code
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
        q.Enqueue(8);

        if (pairWiseConsecutive(q))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
Yes
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
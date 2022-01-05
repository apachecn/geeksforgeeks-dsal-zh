# 使用堆栈检查一个队列是否可以排序到另一个队列中

> 原文:[https://www . geesforgeks . org/check-queue-can-sorted-other-queue-use-stack/](https://www.geeksforgeeks.org/check-queue-can-sorted-another-queue-using-stack/)

给定一个由第一个 **n 个**自然数(以随机顺序)组成的队列。任务是检查给定的队列元素是否可以使用堆栈在另一个队列中以递增的顺序排列。允许的操作有:
1。从堆栈中推送和弹出元素
2。从给定队列中弹出(或出队)。
3。在另一个队列中推送(或排队)。

**示例:**

> 输入:队列[] = { 5，1，2，3，4 }
> 输出:是
> 弹出给定队列的第一个元素，即 5。
> 将 5 推入堆栈。
> 现在，弹出给定队列的所有元素，并将其推送到
> 第二队列。
> 现在，弹出堆栈中的元素 5，并将其推入第二个队列。
> 
> 输入:Queue[] = { 5，1，2，6，3，4 }
> 输出:No
> 推 5 叠。
> 从给定队列弹出 1、2，并将其推送到另一个队列。
> 从给定队列弹出 6 并推入堆栈。
> 从给定队列弹出 3、4，并推送到第二个队列。
> 现在，通过使用上述任何操作，我们不能将 5
> 推入第二个队列，因为它低于堆栈中的 6。

请注意，第二个队列(将包含已排序的元素)从给定的队列或堆栈中获取输入(或排队元素)。因此，下一个预期的(最初为 1)元素必须作为给定队列的前元素或堆栈的顶部元素出现。因此，只需通过将预期的元素初始化为 1 来模拟第二个队列的过程。并检查我们是否可以从给定队列的前面或堆栈的顶部获得期望的元素。如果我们不能从它们中的任何一个获取它，那么弹出给定队列的前面元素，并将其推入堆栈。
此外，请注意，堆栈也必须在每个实例中进行排序，即堆栈顶部的元素必须是堆栈中最小的元素。例如，让 x >为 y，那么 x 将总是在 y 之前。因此，在堆栈中，x 不能被推到 y 之前。因此，我们不能将具有较高值的元素推到具有较小值的元素之上。

算法:
1。初始化期望的元素= 1
2。检查给定队列的前面元素或堆栈的顶部元素是否有预期的元素
…。a)如果是，将 expected_element 增加 1，重复步骤 2。
…。b)否则，弹出队列前面，并将其推入堆栈。如果弹出的元素大于堆栈顶部，则返回“否”。

下面是该方法的实现:

## C++

```
// CPP Program to check if a queue of first
// n natural number can be sorted using a stack
#include <bits/stdc++.h>
using namespace std;

// Function to check if given queue element
// can be sorted into another queue using a
// stack.
bool checkSorted(int n, queue<int>& q)
{
    stack<int> st;
    int expected = 1;
    int fnt;

    // while given Queue is not empty.
    while (!q.empty()) {
        fnt = q.front();
        q.pop();

        // if front element is the expected element
        if (fnt == expected)
            expected++;

        else {
            // if stack is empty, push the element
            if (st.empty()) {
                st.push(fnt);
            }

            // if top element is less than element which
            // need to be pushed, then return false.
            else if (!st.empty() && st.top() < fnt) {
                return false;
            }

            // else push into the stack.
            else
                st.push(fnt);
        }

        // while expected element are coming from
        // stack, pop them out.
        while (!st.empty() && st.top() == expected) {
            st.pop();
            expected++;
        }
    }

    // if the final expected element value is equal
    // to initial Queue size and the stack is empty.
    if (expected - 1 == n && st.empty())
        return true;

    return false;
}

// Driven Program
int main()
{
    queue<int> q;
    q.push(5);
    q.push(1);
    q.push(2);
    q.push(3);
    q.push(4);

    int n = q.size();

    (checkSorted(n, q) ? (cout << "Yes") :
                         (cout << "No"));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a queue
// of first n natural number can
// be sorted using a stack
import java.io.*;
import java.util.*;

class GFG
{
    static Queue<Integer> q =
                    new LinkedList<Integer>();

    // Function to check if given
    // queue element can be sorted
    // into another queue using a stack.
    static boolean checkSorted(int n)
    {
        Stack<Integer> st =
                    new Stack<Integer>();
        int expected = 1;
        int fnt;

        // while given Queue
        // is not empty.
        while (q.size() != 0)
        {
            fnt = q.peek();
            q.poll();

            // if front element is
            // the expected element
            if (fnt == expected)
                expected++;

            else
            {
                // if stack is empty,
                // push the element
                if (st.size() == 0)
                {
                    st.push(fnt);
                }

                // if top element is less than
                // element which need to be
                // pushed, then return false.
                else if (st.size() != 0 &&
                         st.peek() < fnt)
                {
                    return false;
                }

                // else push into the stack.
                else
                    st.push(fnt);
            }

            // while expected element are
            // coming from stack, pop them out.
            while (st.size() != 0 &&
                   st.peek() == expected)
            {
                st.pop();
                expected++;
            }
        }

        // if the final expected element
        // value is equal to initial Queue
        // size and the stack is empty.
        if (expected - 1 == n &&
                st.size() == 0)
            return true;

        return false;
    }

    // Driver Code
    public static void main(String args[])
    {
        q.add(5);
        q.add(1);
        q.add(2);
        q.add(3);
        q.add(4);

        int n = q.size();

        if (checkSorted(n))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python Program to check if a queue of first
# n natural number can be sorted using a stack
from queue import Queue

# Function to check if given queue element
# can be sorted into another queue using a
# stack.
def checkSorted(n, q):
    st = []
    expected = 1
    fnt = None

    # while given Queue is not empty.
    while (not q.empty()):
        fnt = q.queue[0]
        q.get()

        # if front element is the
        # expected element
        if (fnt == expected):
            expected += 1

        else:

            # if stack is empty, put the element
            if (len(st) == 0):
                st.append(fnt)

            # if top element is less than element which
            # need to be puted, then return false.
            elif (len(st) != 0 and st[-1] < fnt):
                return False

            # else put into the stack.
            else:
                st.append(fnt)

        # while expected element are coming
        # from stack, pop them out.
        while (len(st) != 0 and
                   st[-1] == expected):
            st.pop()
            expected += 1

    # if the final expected element value is equal
    # to initial Queue size and the stack is empty.
    if (expected - 1 == n and len(st) == 0):
        return True

    return False

# Driver Code
if __name__ == '__main__':
    q = Queue()
    q.put(5)
    q.put(1)
    q.put(2)
    q.put(3)
    q.put(4)

    n = q.qsize()

    if checkSorted(n, q):
        print("Yes")
    else:
        print("No")

# This code is contributed by PranchalK
```

## C#

```
// C# Program to check if a queue
// of first n natural number can
// be sorted using a stack
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{
    // Function to check if given
    // queue element can be sorted
    // into another queue using a stack.
    static bool checkSorted(int n,
                            ref Queue<int> q)
    {
        Stack<int> st = new Stack<int>();
        int expected = 1;
        int fnt;

        // while given Queue
        // is not empty.
        while (q.Count != 0)
        {
            fnt = q.Peek();
            q.Dequeue();

            // if front element is
            // the expected element
            if (fnt == expected)
                expected++;

            else
            {
                // if stack is empty,
                // push the element
                if (st.Count != 0)
                {
                    st.Push(fnt);
                }

                // if top element is less than
                // element which need to be
                // pushed, then return false.
                else if (st.Count != 0 &&
                         st.Peek() < fnt)
                {
                    return false;
                }

                // else push into the stack.
                else
                    st.Push(fnt);
            }

            // while expected element are
            // coming from stack, pop them out.
            while (st.Count != 0 &&
                   st.Peek() == expected)
            {
                st.Pop();
                expected++;
            }
        }
        // if the final expected element
        // value is equal to initial Queue
        // size and the stack is empty.
        if (expected - 1 == n &&
                st.Count == 0)
            return true;

        return false;
    }

    // Driver Code
    static void Main()
    {
        Queue<int> q = new Queue<int>();
        q.Enqueue(5);
        q.Enqueue(1);
        q.Enqueue(2);
        q.Enqueue(3);
        q.Enqueue(4);

        int n = q.Count;

        if (checkSorted(n, ref q))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>
    // Javascript Program to check if a queue
    // of first n natural number can
    // be sorted using a stack

    let q = [];

    // Function to check if given
    // queue element can be sorted
    // into another queue using a stack.
    function checkSorted(n)
    {
        let st = [];
        let expected = 1;
        let fnt;

        // while given Queue
        // is not empty.
        while (q.length != 0)
        {
            fnt = q[0];
            q.shift();

            // if front element is
            // the expected element
            if (fnt == expected)
                expected++;

            else
            {
                // if stack is empty,
                // push the element
                if (st.length == 0)
                {
                    st.push(fnt);
                }

                // if top element is less than
                // element which need to be
                // pushed, then return false.
                else if (st.length != 0 &&
                         st[st.length - 1] < fnt)
                {
                    return false;
                }

                // else push into the stack.
                else
                    st.push(fnt);
            }

            // while expected element are
            // coming from stack, pop them out.
            while (st.length != 0 &&
                   st[st.length - 1] == expected)
            {
                st.pop();
                expected++;
            }
        }

        // if the final expected element
        // value is equal to initial Queue
        // size and the stack is empty.
        if ((expected - 1) == n && st.length == 0)
            return true;

        return false;
    }

    q.push(5);
    q.push(1);
    q.push(2);
    q.push(3);
    q.push(4);

    let n = q.length;

    if (checkSorted(n))
      document.write("Yes");
    else
      document.write("No");

   // This code is contributed by suresh07.
</script>
```

**Output :** 

```
Yes
```

视频由[帕鲁尔·山迪利亚](https://auth.geeksforgeeks.org/user/ParulShandilya/practice/)T2 供稿
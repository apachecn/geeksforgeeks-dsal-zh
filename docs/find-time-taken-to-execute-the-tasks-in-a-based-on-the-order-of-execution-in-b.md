# 根据在 B 中的执行顺序，找出在 A 中执行任务所花费的时间

> 原文:[https://www . geesforgeks . org/find-基于 b 中执行顺序的任务执行时间/](https://www.geeksforgeeks.org/find-time-taken-to-execute-the-tasks-in-a-based-on-the-order-of-execution-in-b/)

给定两个队列 **A** 和 **B** ，每个队列大小为 **N** ，任务是根据 **B** 中的执行顺序找到执行 **A** 中的任务所需的最短时间，其中:

1.  如果在队列 **B** 前发现的任务在队列 **A** 前，则弹出该任务并执行。
2.  如果在队列 **B** 前面找到的任务在队列 **A** 前面找不到，那么从队列 **A** 弹出当前任务，推到最后。
3.  队列中的推送和弹出操作花费一个单位的时间，任务的执行是在恒定的时间内完成的。

**例**

> **输入:** A = { 3，2，1 }，B = { 1，3，2 }
> **输出:** 7
> **解释:**
> 对于 A = 3 和 B = 1 = >由于队列 A 的前面和队列 B 的前面不匹配，在队列的后面 Pop 和 Push 3。然后，A 变为{ 2，1，3 }，消耗的时间= 2(每次推送和弹出操作的时间单位为 1)
> 对于 A = 2 和 B = 1 = >，因为队列 A 的前面与队列 B 的前面不匹配。弹出和推送 2 在队列的后面。然后，A 变成{ 1，3，2 }，时间= 2 + 2 = 4
> 对于 A = 1 和 B = 1 = >由于队列的前面，A 等于队列 B 的前面，从两个队列中弹出 1 并执行，然后 A 变成{ 3，2 }，B 变成{ 3， 2 }和时间= 4 + 1 = 5
> 对于 A = 3 和 B = 3 = >由于队列的前面，A 等于队列 B 的前面。从两个队列中弹出 3 并执行它，那么 A 变成{ 2 }和 B 变成{ 2 }和时间= 5 + 1 = 6
> 对于 A = 2 和 B = 2 = >由于队列的前面，A 等于队列 B 的前面。从两个队列中弹出 2 并执行它。 所有的任务都被执行了。时间= 6 + 1 = 7
> 因此总时间为 7。
> 
> **输入:** A = { 3，2，1，4 }，B = { 4，1，3，2 }
> T3】输出: 14

**进场:**T2**A**队列中每个任务:

1.  如果[队列](https://www.geeksforgeeks.org/queue-data-structure/) A 的前置任务与[队列](https://www.geeksforgeeks.org/queue-data-structure/) **B** 的前置任务相同。从两个队列中弹出任务并执行它。将总时间增加一个单位。
2.  如果[队列](https://www.geeksforgeeks.org/queue-data-structure/) A 的前置任务和[队列](https://www.geeksforgeeks.org/queue-data-structure/) **B** 的前置任务不一样。从[队列](https://www.geeksforgeeks.org/queue-data-structure/) A 弹出任务，推到[队列](https://www.geeksforgeeks.org/queue-data-structure/) A 后面，总时间增加两个单位。(1 个用于弹出操作，1 个用于推动操作)
3.  重复以上步骤，直到[队列](https://www.geeksforgeeks.org/queue-data-structure/) A 中的所有任务都被执行。

下面是上述方法的实现:

## C++

```
// C++ program to find the total
// time taken to execute the task
// in given order

#include "bits/stdc++.h"
using namespace std;

// Function to calculate the
// total time taken to execute
// the given task in original order
int run_tasks(queue<int>& A,
              queue<int>& B)
{

    // To find the total time
    // taken for executing
    // the task
    int total_time = 0;

    // While A is not empty
    while (!A.empty()) {

        // Store the front element of queue A and B
        int x = A.front();
        int y = B.front();

        // If the front element of the queue A
        // is equal to the front element of queue B
        // then pop the element from both
        // the queues and execute the task
        // Increment total_time by 1
        if (x == y) {
            A.pop();
            B.pop();
            total_time++;
        }

        // If front element of queue A is not equal
        // to front element of queue B then
        // pop the element from queue A &
        // push it at the back of queue A
        // Increment the total_time by 2
        //(1 for push operation and
        // 1 for pop operation)
        else {
            A.pop();
            A.push(x);
            total_time += 2;
        }
    }

    // Return the total time taken
    return total_time;
}

// Driver Code
int main()
{
    // Given task to be executed
    queue<int> A;
    A.push(3);
    A.push(2);
    A.push(1);
    A.push(4);

    // Order in which task need to be
    // executed
    queue<int> B;
    B.push(4);
    B.push(1);
    B.push(3);
    B.push(2);

    // Function the returns the total
    // time taken to execute all the task
    cout << run_tasks(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the total
// time taken to execute the task
// in given order
import java.util.*;

class GFG
{

// Function to calculate the
// total time taken to execute
// the given task in original order
static int run_tasks(Queue<Integer> A,
                    Queue<Integer> B)
{

    // To find the total time
    // taken for executing
    // the task
    int total_time = 0;

    // While A is not empty
    while (!A.isEmpty())
    {

        // Store the front element of queue A and B
        int x = A.peek();
        int y = B.peek();

        // If the front element of the queue A
        // is equal to the front element of queue B
        // then pop the element from both
        // the queues and execute the task
        // Increment total_time by 1
        if (x == y)
        {
            A.remove();
            B.remove();
            total_time++;
        }

        // If front element of queue A is not equal
        // to front element of queue B then
        // pop the element from queue A &
        // push it at the back of queue A
        // Increment the total_time by 2
        //(1 for push operation and
        // 1 for pop operation)
        else
        {
            A.remove();
            A.add(x);
            total_time += 2;
        }
    }

    // Return the total time taken
    return total_time;
}

// Driver Code
public static void main(String[] args)
{
    // Given task to be executed
    Queue<Integer> A = new LinkedList<Integer>();
    A.add(3);
    A.add(2);
    A.add(1);
    A.add(4);

    // Order in which task need to be
    // executed
    Queue<Integer> B = new LinkedList<Integer>();
    B.add(4);
    B.add(1);
    B.add(3);
    B.add(2);

    // Function the returns the total
    // time taken to execute all the task
    System.out.print(run_tasks(A, B));

}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find the total
# time taken to execute the task
# in given order
from collections import deque

# Function to calculate the
# total time taken to execute
# the given task in original order
def run_tasks(A, B):

    # To find the total time
    # taken for executing
    # the task
    total_time = 0

    # While A is not empty
    while (len(A) > 0):

        # Store the front element of queue A and B
        x = A.popleft()
        y = B.popleft()

        # If the front element of the queue A
        # is equal to the front element of queue B
        # then pop the element from both
        # the queues and execute the task
        # Increment total_time by 1
        if (x == y):
            total_time += 1

        # If front element of queue A is not equal
        # to front element of queue B then
        # pop the element from queue A &
        # append it at the back of queue A
        # Increment the total_time by 2
        #(1 for append operation and
        # 1 for pop operation)
        else:
            B.appendleft(y)
            A.append(x)
            total_time += 2

    # Return the total time taken
    return total_time

# Driver Code
if __name__ == '__main__':

    # Given task to be executed
    A = deque()
    A.append(3)
    A.append(2)
    A.append(1)
    A.append(4)

    # Order in which task need to be
    # executed
    B = deque()
    B.append(4)
    B.append(1)
    B.append(3)
    B.append(2)

    # Function the returns the total
    # time taken to execute all the task
    print(run_tasks(A, B))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the total
// time taken to execute the task
// in given order
using System;
using System.Collections.Generic;

class GFG
{

// Function to calculate the
// total time taken to execute
// the given task in original order
static int run_tasks(Queue<int> A,
                    Queue<int> B)
{

    // To find the total time
    // taken for executing
    // the task
    int total_time = 0;

    // While A is not empty
    while (A.Count != 0)
    {

        // Store the front element of queue A and B
        int x = A.Peek();
        int y = B.Peek();

        // If the front element of the queue A
        // is equal to the front element of queue B
        // then pop the element from both
        // the queues and execute the task
        // Increment total_time by 1
        if (x == y)
        {
            A.Dequeue();
            B.Dequeue();
            total_time++;
        }

        // If front element of queue A is not equal
        // to front element of queue B then
        // pop the element from queue A &
        // push it at the back of queue A
        // Increment the total_time by 2
        //(1 for push operation and
        // 1 for pop operation)
        else
        {
            A.Dequeue();
            A.Enqueue(x);
            total_time += 2;
        }
    }

    // Return the total time taken
    return total_time;
}

// Driver Code
public static void Main(String[] args)
{
    // Given task to be executed
    Queue<int> A = new Queue<int>();
    A.Enqueue(3);
    A.Enqueue(2);
    A.Enqueue(1);
    A.Enqueue(4);

    // Order in which task need to be
    // executed
    Queue<int> B = new Queue<int>();
    B.Enqueue(4);
    B.Enqueue(1);
    B.Enqueue(3);
    B.Enqueue(2);

    // Function the returns the total
    // time taken to execute all the task
    Console.Write(run_tasks(A, B));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the total
// time taken to execute the task
// in given order

// Function to calculate the
// total time taken to execute
// the given task in original order
function run_tasks(A, B)
{

    // To find the total time
    // taken for executing
    // the task
    let total_time = 0;

    // While A is not empty
    while (A.length != 0)
    {

        // Store the front element of
        // queue A and B
        let x = A[0];
        let y = B[0];

        // If the front element of the queue A
        // is equal to the front element of queue B
        // then pop the element from both
        // the queues and execute the task
        // Increment total_time by 1
        if (x == y)
        {
            A.shift();
            B.shift();
            total_time++;
        }

        // If front element of queue A is not equal
        // to front element of queue B then
        // pop the element from queue A &
        // push it at the back of queue A
        // Increment the total_time by 2
        //(1 for push operation and
        // 1 for pop operation)
        else
        {
            A.shift();
            A.push(x);
            total_time += 2;
        }
    }

    // Return the total time taken
    return total_time;
}

// Driver code

// Given task to be executed
let A = [ 3, 2, 1, 4 ];

// Order in which task need to be
// executed
let B = [ 4, 1, 3, 2 ];

// Function the returns the total
// time taken to execute all the task
document.write(run_tasks(A, B));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
14
```

**时间复杂度:** O(N <sup>2</sup> ，其中 N 为任务数。
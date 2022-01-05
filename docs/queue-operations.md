# 队列操作

> 原文:[https://www.geeksforgeeks.org/queue-operations/](https://www.geeksforgeeks.org/queue-operations/)

给定 **N** 个整数，任务是将这些元素插入队列。此外，给定 **M** 整数，任务是找到队列中每个数字的频率。

**示例:**

> **输入:**
> N = 8
> 1 2 3 4 5 2 3 1 (N 个整数)
> M = 5
> 1 3 2 9 10 (M 个整数)
> **输出:**
> 2 2-1-1
> 
> **说明:**
> 在队列中插入 1、2、3、4、5、2、3、1 后，1 的频率为 2，3 为 2，2 为 2，9 为-1，10 为-1(因为队列中没有 9 和 10)。
> 
> **输入:**
> N = 5
> 5 2 4 5(N 个整数)
> M = 5
> 2 3 4 5 1 (M 个整数)
> **输出:**
> 2 -1 1 2 -1

**方法:**给定的问题可以通过使用简单的[队列](https://www.geeksforgeeks.org/queue-data-structure/)来解决。思路是将 **N** 个整数逐一插入**队列**中，然后检查 **M** 个整数的出现频率。将创建单独的函数来执行这两种操作。按照以下步骤解决问题。

*   创建一个队列，将所有给定的整数推入**队列**。
*   将所有元素推入**队列后**创建另一个函数，用于逐个计算给定 **M** 元素的频率。
*   取一个变量 **cntFrequency** 来记录当前元件的频率。
*   从队列中弹出所有元素直到其大小，每次检查**队列**中的当前元素是否等于我们正在检查频率的元素。
    –如果两者相等，将**频率**增加 1
    –否则，什么也不做。
*   将当前元素推回到队列中，以便在下一种情况下队列不会受到干扰。
*   打印找到的每个元素的频率。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement above approach
import java.io.*;
import java.util.*;

class GFG {

    // Driver code
    public static void main(String[] args)
    {
        // Declaring Queue
        Queue<Integer> q = new LinkedList<>();
        int N = 8;
        int[] a = new int[] { 1, 2, 3, 4, 5, 2, 3, 1 };
        int M = 5;
        int[] b = new int[] { 1, 3, 2, 9, 10 };

        // Invoking object of Geeks class
        Geeks obj = new Geeks();

        for (int i = 0; i < N; i++) {
            // calling insert()
            // to add elements in queue
            obj.insert(q, a[i]);
        }

        for (int i = 0; i < M; i++) {
            // calling findFrequency()
            int f = obj.findFrequency(q, b[i]);
            if (f != 0) {
                // variable f
                // will have final frequency
                System.out.print(f + " ");
            }
            else {
                System.out.print("-1"
                                 + " ");
            }
        }
    }
}

// Helper class Geeks to implement
// insert() and findFrequency()
class Geeks {

    // Function to insert
    // element into the queue
    static void insert(Queue<Integer> q, int k)
    {
        // adding N integers into the Queue
        q.add(k);
    }

    // Function to find frequency of an element
    // return the frequency of k
    static int findFrequency(Queue<Integer> q, int k)
    {
        // to count frequency of elements
        int cntFrequency = 0;

        // storing size of queue in a variable
        int size = q.size();

        // running loop until size becomes zero
        while (size-- != 0) {

            // storing and deleting
            // first element from queue
            int x = q.poll();

            // comparing if it's equal to integer K
            // that belongs to M
            if (x == k) {
                // increment count
                cntFrequency++;
            }
            // add element back to queue because
            // we also want N integers
            q.add(x);
        }
        // return the count
        return cntFrequency;
    }
}
```

## 蟒蛇 3

```
# Python Program to implement above approach
import collections

# Helper class Geeks to implement
# insert() and findFrequency()
class Geeks:

    # Function to insert
    # element into the queue
    def insert(self, q, k):

        # adding N integers into the Queue
        q.append(k)

    # Function to find frequency of an element
    # return the frequency of k
    def findFrequency(self, q, k):

        # to count frequency of elements
        cntFrequency = 0

        # storing size of queue in a variable
        size = len(q)

        # running loop until size becomes zero
        while (size):
            size = size - 1

            # storing and deleting
            # first element from queue
            x = q.popleft()

            # comparing if it's equal to integer K
            # that belongs to M
            if (x == k):

                # increment count
                cntFrequency += 1

            # add element back to queue because
            # we also want N integers
            q.append(x)

        # return the count
        return cntFrequency

# Declaring Queue
q = collections.deque()
N = 8
a = [1, 2, 3, 4, 5, 2, 3, 1]
M = 5
b = [1, 3, 2, 9, 10]

# Invoking object of Geeks class
obj = Geeks()

for i in range(N):

    # calling insert()
    # to add elements in queue
    obj.insert(q, a[i])

for i in range(M):

    # calling findFrequency()
    f = obj.findFrequency(q, b[i])
    if (f != 0):

        # variable f
        # will have final frequency
        print(f, end=" ")
    else:
        print("-1", end=" ")
print(" ")

# This code is contributed by gfgking.
```

## C#

```
// C# Program to implement above approach
using System;
using System.Collections.Generic;

public class GFG {

  // Helper class Geeks to implement
// insert() and findFrequency()
public class Geeks {

    // Function to insert
    // element into the queue
   public void insert(Queue<int> q, int k)
    {
        // adding N integers into the Queue
        q.Enqueue(k);
    }

    // Function to find frequency of an element
    // return the frequency of k
    public int findFrequency(Queue<int> q, int k)
    {
        // to count frequency of elements
        int cntFrequency = 0;

        // storing size of queue in a variable
        int size = q.Count;

        // running loop until size becomes zero
        while (size-- != 0) {

            // storing and deleting
            // first element from queue
            int x = q.Peek();
            q.Dequeue();

            // comparing if it's equal to integer K
            // that belongs to M
            if (x == k) {
                // increment count
                cntFrequency++;
            }
            // add element back to queue because
            // we also want N integers
            q.Enqueue(x);
        }
        // return the count
        return cntFrequency;
    }
}

    // Driver code
    public static void Main()
    {

        // Declaring Queue
        Queue<int> q = new Queue<int>();
        int N = 8;
        int[] a = new int[] { 1, 2, 3, 4, 5, 2, 3, 1 };
        int M = 5;
        int[] b = new int[] { 1, 3, 2, 9, 10 };

        // Invoking object of Geeks class
        Geeks obj = new Geeks();

        for (int i = 0; i < N; i++)
        {

            // calling insert()
            // to add elements in queue
            obj.insert(q, a[i]);
        }

        for (int i = 0; i < M; i++)
        {

            // calling findFrequency()
            int f = obj.findFrequency(q, b[i]);
            if (f != 0)
            {

                // variable f
                // will have final frequency
                Console.Write(f + " ");
            }
            else {
                Console.Write("-1"
                                 + " ");
            }
        }
    }
}

// This code is contributed by SURENDRA_GANGWAR.
```

**Output**

```
2 2 2 -1 -1 
```

**时间复杂度** : O(N*M)
**辅助空间:** O(N)
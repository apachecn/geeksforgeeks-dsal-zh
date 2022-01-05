# 打印第 n 个步进或自传号

> 原文:[https://www . geesforgeks . org/print-n-steping-or-自传-number/](https://www.geeksforgeeks.org/print-nth-stepping-or-autobiographical-number/)

给定一个自然数 **N** ，任务是打印第 N 个[步进或自传号](https://www.geeksforgeeks.org/stepping-numbers/)。

> 如果所有相邻数字的绝对差值都为 1，则该数字称为步进数。以下系列为步进自然数列表:
> **1、2、3、4、5、6、7、8、9、10、11、12、21、22、23、32、…。**

**例:**

```
Input: N = 16 
Output: 32
Explanation:
16th Stepping number is 32.

Input: N = 14 
Output: 22
Explanation:
14th Stepping number is 22.
```

**方法:**这个问题可以使用 [**队列**](https://www.geeksforgeeks.org/queue-data-structure/) 数据结构来解决。首先，准备一个空队列，**按照**的顺序将 1，2，…，9 入队。
然后为了生成第 N 个步进号，必须执行以下操作 N 次:

*   从队列中执行出列。设 x 为出列元素。
*   如果 x mod 10 不等于 0，则入队 10x+(x mod 10)–1
*   Enqueue 10x + (x mod 10)。
*   如果 x mod 10 不等于 9，那么入队 10x + (x mod 10) + 1。

第 N 个操作中的出列号是第 N 个步进号。
**以下是上述方法的实施:**

## C++

```
// C++ implementation to find
// N’th stepping natural Number
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// Nth stepping natural number
int NthSmallest(int K)
{

    // Declare the queue
    queue<int> Q;

    int x;

    // Enqueue 1, 2, ..., 9 in this order
    for (int i = 1; i < 10; i++)
        Q.push(i);

    // Perform K operation on queue
    for (int i = 1; i <= K; i++) {

        // Get the ith Stepping number
        x = Q.front();

        // Perform Dequeue from the Queue
        Q.pop();

        // If x mod 10 is not equal to 0
        if (x % 10 != 0) {

            // then Enqueue 10x + (x mod 10) - 1
            Q.push(x * 10 + x % 10 - 1);
        }

        // Enqueue 10x + (x mod 10)
        Q.push(x * 10 + x % 10);

        // If x mod 10 is not equal to 9
        if (x % 10 != 9) {

            // then Enqueue 10x + (x mod 10) + 1
            Q.push(x * 10 + x % 10 + 1);
        }
    }

    // Return the dequeued number of the K-th
    // operation as the Nth stepping number
    return x;
}

// Driver Code
int main()
{

    // initialise K
    int N = 16;

    cout << NthSmallest(N) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// N'th stepping natural Number
import java.util.*;

class GFG{

// Function to find the
// Nth stepping natural number
static int NthSmallest(int K)
{

    // Declare the queue
    Queue<Integer> Q = new LinkedList<>();

    int x = 0;

    // Enqueue 1, 2, ..., 9 in this order
    for (int i = 1; i < 10; i++)
        Q.add(i);

    // Perform K operation on queue
    for (int i = 1; i <= K; i++) {

        // Get the ith Stepping number
        x = Q.peek();

        // Perform Dequeue from the Queue
        Q.remove();

        // If x mod 10 is not equal to 0
        if (x % 10 != 0) {

            // then Enqueue 10x + (x mod 10) - 1
            Q.add(x * 10 + x % 10 - 1);
        }

        // Enqueue 10x + (x mod 10)
        Q.add(x * 10 + x % 10);

        // If x mod 10 is not equal to 9
        if (x % 10 != 9) {

            // then Enqueue 10x + (x mod 10) + 1
            Q.add(x * 10 + x % 10 + 1);
        }
    }

    // Return the dequeued number of the K-th
    // operation as the Nth stepping number
    return x;
}

// Driver Code
public static void main(String[] args)
{

    // initialise K
    int N = 16;

    System.out.print(NthSmallest(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find
# N’th stepping natural Number

# Function to find the
# Nth stepping natural number
def NthSmallest(K):
    # Declare the queue
    Q = []

    # Enqueue 1, 2, ..., 9 in this order
    for i in range(1,10):
        Q.append(i)

    # Perform K operation on queue
    for i in range(1,K+1):
        # Get the ith Stepping number
        x = Q[0]

        # Perform Dequeue from the Queue
        Q.remove(Q[0])

        # If x mod 10 is not equal to 0
        if (x % 10 != 0):
            # then Enqueue 10x + (x mod 10) - 1
            Q.append(x * 10 + x % 10 - 1)

        # Enqueue 10x + (x mod 10)
        Q.append(x * 10 + x % 10)

        # If x mod 10 is not equal to 9
        if (x % 10 != 9):
            # then Enqueue 10x + (x mod 10) + 1
            Q.append(x * 10 + x % 10 + 1)

    # Return the dequeued number of the K-th
    # operation as the Nth stepping number
    return x

# Driver Code
if __name__ == '__main__':
    # initialise K
    N = 16

    print(NthSmallest(N))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation to find
// N'th stepping natural Number
using System;
using System.Collections.Generic;

class GFG{

// Function to find the
// Nth stepping natural number
static int NthSmallest(int K)
{

    // Declare the queue
    List<int> Q = new List<int>();

    int x = 0;

    // Enqueue 1, 2, ..., 9 in this order
    for (int i = 1; i < 10; i++)
        Q.Add(i);

    // Perform K operation on queue
    for (int i = 1; i <= K; i++) {

        // Get the ith Stepping number
        x = Q[0];

        // Perform Dequeue from the Queue
        Q.RemoveAt(0);

        // If x mod 10 is not equal to 0
        if (x % 10 != 0) {

            // then Enqueue 10x + (x mod 10) - 1
            Q.Add(x * 10 + x % 10 - 1);
        }

        // Enqueue 10x + (x mod 10)
        Q.Add(x * 10 + x % 10);

        // If x mod 10 is not equal to 9
        if (x % 10 != 9) {

            // then Enqueue 10x + (x mod 10) + 1
            Q.Add(x * 10 + x % 10 + 1);
        }
    }

    // Return the dequeued number of the K-th
    // operation as the Nth stepping number
    return x;
}

// Driver Code
public static void Main(String[] args)
{

    // initialise K
    int N = 16;

    Console.Write(NthSmallest(N));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation to find
// N’th stepping natural Number

// Function to find the
// Nth stepping natural number
function NthSmallest(K)
{

    // Declare the queue
    var Q = [];

    var x;

    // Enqueue 1, 2, ..., 9 in this order
    for (var i = 1; i < 10; i++)
        Q.push(i);

    // Perform K operation on queue
    for (var i = 1; i <= K; i++) {

        // Get the ith Stepping number
        x = Q[0];

        // Perform Dequeue from the Queue
        Q.shift();

        // If x mod 10 is not equal to 0
        if (x % 10 != 0) {

            // then Enqueue 10x + (x mod 10) - 1
            Q.push(x * 10 + x % 10 - 1);
        }

        // Enqueue 10x + (x mod 10)
        Q.push(x * 10 + x % 10);

        // If x mod 10 is not equal to 9
        if (x % 10 != 9) {

            // then Enqueue 10x + (x mod 10) + 1
            Q.push(x * 10 + x % 10 + 1);
        }
    }

    // Return the dequeued number of the K-th
    // operation as the Nth stepping number
    return x;
}

// Driver Code
// initialise K
var N = 16;
document.write( NthSmallest(N));

// This code is contributed by famously.
</script>
```

**Output:** 

```
32
```

***时间复杂度:** O(N)*

***辅助空间:**O(N)*T4】
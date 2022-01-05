# 相邻数字的绝对差最多为 1 的第 n 个正数

> 原文:[https://www . geesforgeks . org/n-正数-其相邻数字的绝对差值最多为 1/](https://www.geeksforgeeks.org/nth-positive-number-whose-absolute-difference-of-adjacent-digits-is-at-most-1/)

给定一个数字 **N** ，任务是找到 **N** <sup>第</sup>个数字，其每对相邻数字之间的绝对差值为 1。
**举例:**

> **输入:** N = 5
> **输出:** 5
> **说明:**
> 前 5 个这样的数字是 1、2、3、4、 **5** 。
> **输入:** N = 15
> **输出:** 23
> **说明:**
> 前 15 个这样的数字是 1、2、3、4、5、6、7、8、9、10、11、12、21、22、 **23** 。

**方法:**为了解决这个问题，我们使用了[队列](https://www.geeksforgeeks.org/queue-data-structure/)数据结构。

*   准备一个空队列，将所有整数 1 到 9 按递增顺序排队。

*   现在执行以下操作 N 次。
    *   出列并存储在数组 **arr** 中，该数组在 arr[i]中存储所需类型的数量。
    *   If (arr[i] % 10！= 0)，然后将**10 * arr[I]+(arr[I]% 10)–1**入队。
    *   入队 **10 * arr[i] + (arr[i] % 10)** 。
    *   If (arr[i] % 10！= 9)，然后将 **10 * arr[i] + (arr[i] % 10) + 1** 入队。
*   返回**arr【N】**作为答案。

下面是给定方法的实现:

## C++

```
// C++ Program to find Nth number with
// absolute difference between all
// adjacent digits at most 1.

#include <bits/stdc++.h>
using namespace std;

// Return Nth number with
// absolute difference between all
// adjacent digits at most 1.
void findNthNumber(int N)
{
    // To store all such numbers
    long long arr[N + 1];

    queue<long long> q;

    // Enqueue all integers from 1 to 9
    // in increasing order.
    for (int i = 1; i <= 9; i++)
        q.push(i);

    // Perform the operation N times so that
    // we can get all such N numbers.
    for (int i = 1; i <= N; i++) {

        // Store the front element of queue,
        // in array and pop it from queue.
        arr[i] = q.front();
        q.pop();

        // If the last digit of dequeued integer is
        // not 0, then enqueue the next such number.
        if (arr[i] % 10 != 0)
            q.push(arr[i] * 10 + arr[i] % 10 - 1);

        // Enqueue the next such number
        q.push(arr[i] * 10 + arr[i] % 10);

        // If the last digit of dequeued integer is
        // not 9, then enqueue the next such number.
        if (arr[i] % 10 != 9)
            q.push(arr[i] * 10 + arr[i] % 10 + 1);
    }

    cout<<arr[N]<<endl;
}

// Driver Code
int main()
{
    int N = 21;
    findNthNumber(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Nth number with
// absolute difference between all
// adjacent digits at most 1.
import java.util.*;

class GFG{

// Return Nth number with
// absolute difference between all
// adjacent digits at most 1.
static void findNthNumber(int N)
{

    // To store all such numbers
    int []arr = new int[N + 1];

    Queue<Integer> q = new LinkedList<>();

    // Enqueue all integers from 1 to 9
    // in increasing order.
    for(int i = 1; i <= 9; i++)
       q.add(i);

    // Perform the operation N times so
    // that we can get all such N numbers.
    for(int i = 1; i <= N; i++)
    {

       // Store the front element of queue,
       // in array and pop it from queue.
       arr[i] = q.peek();
       q.remove();

       // If the last digit of dequeued
       // integer is not 0, then enqueue
       // the next such number.
       if (arr[i] % 10 != 0)
           q.add(arr[i] * 10 + arr[i] % 10 - 1);

       // Enqueue the next such number
       q.add(arr[i] * 10 + arr[i] % 10);

       // If the last digit of dequeued
       // integer is not 9, then enqueue
       // the next such number.
       if (arr[i] % 10 != 9)
           q.add(arr[i] * 10 + arr[i] % 10 + 1);
    }
    System.out.println(arr[N]);
}

// Driver Code
public static void main(String[] args)
{
    int N = 21;

    findNthNumber(N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python 3 Program to find Nth number with
# absolute difference between all
# adjacent digits at most 1.

# Return Nth number with
# absolute difference between all
# adjacent digits at most 1.
def findNthNumber(N):

    # To store all such numbers
    arr = [0 for i in range(N + 1)]

    q = []

    # Enqueue all integers from 1 to 9
    # in increasing order.
    for i in range(1, 10, 1):
        q.append(i)

    # Perform the operation N times so that
    # we can get all such N numbers.
    for i in range(1, N+1, 1):

        # Store the front element of queue,
        # in array and pop it from queue.
        arr[i] = q[0]
        q.remove(q[0])

        # If the last digit of dequeued integer is
        # not 0, then enqueue the next such number.
        if (arr[i] % 10 != 0):
            q.append(arr[i] * 10 + arr[i] % 10 - 1)

        # Enqueue the next such number
        q.append(arr[i] * 10 + arr[i] % 10)

        # If the last digit of dequeued integer is
        # not 9, then enqueue the next such number.
        if (arr[i] % 10 != 9):
            q.append(arr[i] * 10 + arr[i] % 10 + 1)

    print(arr[N])

# Driver Code
if __name__ == '__main__':

    N = 21
    findNthNumber(N)

# This code is contributed by Samarth
```

## C#

```
// C# program to find Nth number with
// absolute difference between all
// adjacent digits at most 1.
using System;
using System.Collections.Generic;

class GFG{

// Return Nth number with
// absolute difference between all
// adjacent digits at most 1.
static void findNthNumber(int N)
{

    // To store all such numbers
    int []arr = new int[N + 1];

    Queue<int> q = new Queue<int>();

    // Enqueue all integers from 1 to 9
    // in increasing order.
    for(int i = 1; i <= 9; i++)
       q.Enqueue(i);

    // Perform the operation N times so
    // that we can get all such N numbers.
    for(int i = 1; i <= N; i++)
    {

       // Store the front element of queue,
       // in array and pop it from queue.
       arr[i] = q.Peek();
       q.Dequeue();

       // If the last digit of dequeued
       // integer is not 0, then enqueue
       // the next such number.
       if (arr[i] % 10 != 0)
           q.Enqueue(arr[i] * 10 +
                     arr[i] % 10 - 1);

       // Enqueue the next such number
       q.Enqueue(arr[i] * 10 + arr[i] % 10);

       // If the last digit of dequeued
       // integer is not 9, then enqueue
       // the next such number.
       if (arr[i] % 10 != 9)
           q.Enqueue(arr[i] * 10 +
                     arr[i] % 10 + 1);
    }
    Console.WriteLine(arr[N]);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 21;

    findNthNumber(N);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

    // JavaScript program to find Nth number with
    // absolute difference between all
    // adjacent digits at most 1.

    // Return Nth number with
    // absolute difference between all
    // adjacent digits at most 1.
    function findNthNumber(N)
    {

        // To store all such numbers
        let arr = new Array(N + 1);

        let q = [];

        // Enqueue all integers from 1 to 9
        // in increasing order.
        for(let i = 1; i <= 9; i++)
           q.push(i);

        // Perform the operation N times so
        // that we can get all such N numbers.
        for(let i = 1; i <= N; i++)
        {

           // Store the front element of queue,
           // in array and pop it from queue.
           arr[i] = q[0];
           q.shift();

           // If the last digit of dequeued
           // integer is not 0, then enqueue
           // the next such number.
           if (arr[i] % 10 != 0)
               q.push(arr[i] * 10 + arr[i] % 10 - 1);

           // Enqueue the next such number
           q.push(arr[i] * 10 + arr[i] % 10);

           // If the last digit of dequeued
           // integer is not 9, then enqueue
           // the next such number.
           if (arr[i] % 10 != 9)
               q.push(arr[i] * 10 + arr[i] % 10 + 1);
        }
        document.write(arr[N] + "</br>");
    }

    let N = 21;

    findNthNumber(N);

</script>
```

**Output:** 

```
45
```

时间复杂度:0(N)

辅助空间:O(N)
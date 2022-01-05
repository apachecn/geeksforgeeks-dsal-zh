# 查询二进制数组中最左边的给定类型整数

> 原文:[https://www . geesforgeks . org/query-to-find-最左侧给定类型-二进制数组中的整数/](https://www.geeksforgeeks.org/queries-to-find-the-left-most-given-type-integer-in-a-binary-array/)

给定一个二进制数组 **arr[]** ，任务是设计一个支持 O(1)中以下操作的数据结构。

*   **键入 1:** 从数组中移除并打印最左边的 **0** 。
*   **键入 2:** 从数组中移除并打印最左边的 **1** 。
*   **键入 3:** 移除并打印数组中最左边的元素。

如果任何请求的元素不在数组中，那么 print -1。
**例:**

> **输入:** arr[] = {1，0，1，1，1}，q[] = {1，3，1}
> **输出:**
> 0
> 1
> -1
> 类型 1 查询:打印 0，数组变成{1，1，1，1}
> 类型 3 查询:打印 1，arr[] = {1，1，1}
> 类型 1 查询:没有 0 了，所以打印-1
> **输入::**

**天真的方法:**一个简单的方法是将所有元素插入到支持先进先出的队列中。这种方法在 0(1)中可以找到数组中最左边的元素，但在 0(1)中找不到最左边的 1 或 0。
**高效方法:**创建两个队列，第一个队列将按照出现的顺序存储 0 的索引，第二个队列将按照出现的顺序存储 1 的索引。现在，给定的操作可以如下执行:

*   **类型 1:** 打印 O(1)中删除第一个队列的头。
*   **类型 2:** 打印 O(1)中删除第二个队列的头。
*   **类型 3:** 比较两个队列的头，返回索引最小的那个，然后删除它..

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// To store the indices of 0s and 1s
static queue<int> zero;
static queue<int> one ;

// Function to return the leftmost 0
static int getLeftMostZero()
{

    // If there are no 0s
    if (zero.empty())
        return -1;

    // pop the head of the queue
    zero.pop();
    return 0;
}

// Function to return the leftmost 1
static int getLeftMostOne()
{

    // If there are no 1s
    if (one.empty())
        return -1;

    // pop the head of the queue
    one.pop();
    return 1;
}

// Function to return the pre-calculate array
// such that arr[i] stores the count of
// valid numbers in the range [0, i]
int getLeftMostElement()
{

    // If there are no elements left
    if (zero.empty() && one.empty())
        return -1;

    // If only 1s are there
    else if (zero.empty())
    {
        one.pop();
        return 1;
    }

    // If only 0s are there
    else if (one.empty())
    {
        zero.pop();
        return 0;
    }

    // Get the element which is at
    // the left-most position
    int res = (zero.front() < one.front()) ? 0 : 1;

    if (res == 0)
        zero.pop();
    else
        one.pop();

    return res;
}

// Function to perform the queries
void performQueries(int arr[], int n,
                    int queries[], int q)
{

    for (int i = 0; i < n; i++)
    {
        if (arr[i] == 0)
            zero.push(i);
        else
            one.push(i);
    }

    // For every query
    for (int i = 0; i < q; i++)
    {

        // Get its type
        int type = queries[i];
        switch (type)
        {

            // Perform type 1 query
            case 1:
                cout << (getLeftMostZero())
                     << endl;
                break;

            // Perform type 2 query
            case 2:
                cout << (getLeftMostOne())
                     << endl;
                break;

            // Perform type 3 query
            case 3:
                cout << (getLeftMostElement())
                     << endl;
                break;
        }
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 0, 1, 1, 1 };
    int n = sizeof(arr) / sizeof(int);
    int queries[] = { 1, 3, 1 };
    int q = sizeof(queries) / sizeof(int);

    performQueries(arr, n, queries, q);
}

// This code is contributed by andrew1234
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG {

    // Function to return the leftmost 0
    static int getLeftMostZero(Queue<Integer> zero)
    {

        // If there are no 0s
        if (zero.isEmpty())
            return -1;

        // Remove the head of the queue
        zero.remove();
        return 0;
    }

    // Function to return the leftmost 1
    static int getLeftMostOne(Queue<Integer> one)
    {

        // If there are no 1s
        if (one.isEmpty())
            return -1;

        // Remove the head of the queue
        one.remove();
        return 1;
    }

    // Function to return the pre-calculate array
    // such that arr[i] stores the count of
    // valid numbers in the range [0, i]
    static int getLeftMostElement(Queue<Integer> zero, Queue<Integer> one)
    {

        // If there are no elements left
        if (zero.isEmpty() && one.isEmpty())
            return -1;

        // If only  1s are there
        else if (zero.isEmpty()) {
            one.remove();
            return 1;
        }

        // If only 0s are there
        else if (one.isEmpty()) {
            zero.remove();
            return 0;
        }

        // Get the element which is at
        // the left-most position
        int res = (zero.peek() < one.peek()) ? 0 : 1;

        if (res == 0)
            zero.remove();
        else
            one.remove();

        return res;
    }

    // Function to perform the queries
    static void performQueries(int arr[], int n, int queries[], int q)
    {

        // To store the indices of 0s and 1s
        Queue<Integer> zero = new LinkedList<>();
        Queue<Integer> one = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (arr[i] == 0)
                zero.add(i);
            else
                one.add(i);
        }

        // For every query
        for (int i = 0; i < q; i++) {

            // Get its type
            int type = queries[i];
            switch (type) {

            // Perform type 1 query
            case 1:
                System.out.println(getLeftMostZero(zero));
                break;

            // Perform type 2 query
            case 2:
                System.out.println(getLeftMostOne(one));
                break;

            // Perform type 3 query
            case 3:
                System.out.println(getLeftMostElement(zero, one));
                break;
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 1, 0, 1, 1, 1 };
        int n = arr.length;
        int queries[] = { 1, 3, 1 };
        int q = queries.length;

        performQueries(arr, n, queries, q);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import deque

# To store the indices of 0s and 1s
zero = deque()
one = deque()

# Function to return the leftmost 0
def getLeftMostZero():

    # If there are no 0s
    if not len(zero):
        return -1

    # pop the head of the queue
    zero.popleft()
    return 0

# Function to return the leftmost 1
def getLeftMostOne():

    # If there are no 1s
    if not len(one):
        return -1

    # pop the head of the queue
    one.popleft()
    return 1

# Function to return the pre-calculate array
# such that arr[i] stores the count of
# valid numbers in the range [0, i]
def getLeftMostElement():

    # If there are no elements left
    if not len(zero) and not len(one):
        return -1

    # If only 1s are there
    elif not len(zero):
        one.popleft()
        return 1

    # If only 0s are there
    elif not len(one):
        zero.popleft()
        return 0

    # Get the element which is at
    # the left-most position
    res = 0 if zero[0] < one[0] else 1

    if res == 0:
        zero.popleft()
    else:
        one.popleft()

    return res

# Function to perform the queries
def performQueries(arr: list, n: int, queries: list, q: int):
    for i in range(n):
        if arr[i] == 0:
            zero.append(i)
        else:
            one.append(i)

    # For every query
    for i in range(q):

        # Get its type
        type = queries[i]

        # Perform type 1 query
        if type == 1:
            print(getLeftMostZero())

        # Perform type 2 query
        elif type == 2:
            print(getLeftMostOne())

        # Perform type 3 query
        elif type == 3:
            print(getLeftMostElement())

# Driver Code
if __name__ == "__main__":

    arr = [1, 0, 1, 1, 1]
    n = len(arr)
    queries = [1, 3, 1]
    q = len(queries)

    performQueries(arr, n, queries, q)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the leftmost 0
    static int getLeftMostZero(Queue<int> zero)
    {

        // If there are no 0s
        if (zero.Count == 0)
            return -1;

        // Remove the head of the queue
        zero.Dequeue();
        return 0;
    }

    // Function to return the leftmost 1
    static int getLeftMostOne(Queue<int> one)
    {

        // If there are no 1s
        if (one.Count == 0)
            return -1;

        // Remove the head of the queue
        one.Dequeue();
        return 1;
    }

    // Function to return the pre-calculate array
    // such that arr[i] stores the count of
    // valid numbers in the range [0, i]
    static int getLeftMostElement(Queue<int> zero, 
                                  Queue<int> one)
    {

        // If there are no elements left
        if (zero.Count == 0 && one.Count == 0)
            return -1;

        // If only 1s are there
        else if (zero.Count == 0)
        {
            one.Dequeue();
            return 1;
        }

        // If only 0s are there
        else if (one.Count == 0)
        {
            zero.Dequeue();
            return 0;
        }

        // Get the element which is at
        // the left-most position
        int res = (zero.Peek() < one.Peek()) ? 0 : 1;

        if (res == 0)
            zero.Dequeue();
        else
            one.Dequeue();

        return res;
    }

    // Function to perform the queries
    static void performQueries(int []arr, int n,
                               int []queries, int q)
    {

        // To store the indices of 0s and 1s
        Queue<int> zero = new Queue<int>();
        Queue<int> one = new Queue<int>();
        for (int i = 0; i < n; i++)
        {
            if (arr[i] == 0)
                zero.Enqueue(i);
            else
                one.Enqueue(i);
        }

        // For every query
        for (int i = 0; i < q; i++)
        {

            // Get its type
            int type = queries[i];
            switch (type)
            {

                // Perform type 1 query
                case 1:
                    Console.WriteLine(getLeftMostZero(zero));
                    break;

                // Perform type 2 query
                case 2:
                    Console.WriteLine(getLeftMostOne(one));
                    break;

                // Perform type 3 query
                case 3:
                    Console.WriteLine(getLeftMostElement(zero, one));
                    break;
            }
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 1, 0, 1, 1, 1 };
        int n = arr.Length;
        int []queries = { 1, 3, 1 };
        int q = queries.Length;

        performQueries(arr, n, queries, q);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the leftmost 0
function getLeftMostZero(zero)
{
    // If there are no 0s
        if (zero.length==0)
            return -1;

        // Remove the head of the queue
        zero.shift();
        return 0;
}

// Function to return the leftmost 1
function getLeftMostOne(one)
{
    // If there are no 1s
        if (one.length==0)
            return -1;

        // Remove the head of the queue
        one.shift();
        return 1;
}

// Function to return the pre-calculate array
    // such that arr[i] stores the count of
    // valid numbers in the range [0, i]
function getLeftMostElement(zero,one)
{
    // If there are no elements left
        if (zero.length==0 && one.length==0)
            return -1;

        // If only  1s are there
        else if (zero.length==0) {
            one.shift();
            return 1;
        }

        // If only 0s are there
        else if (one.length==0) {
            zero.shift();
            return 0;
        }

        // Get the element which is at
        // the left-most position
        let res = (zero[0] < one[0]) ? 0 : 1;

        if (res == 0)
            zero.shift();
        else
            one.shift();

        return res;
}

// Function to perform the queries
function performQueries(arr,n,queries,q)
{
    // To store the indices of 0s and 1s
        let zero = [];
        let one = [];
        for (let i = 0; i < n; i++) {
            if (arr[i] == 0)
                zero.push(i);
            else
                one.push(i);
        }

        // For every query
        for (let i = 0; i < q; i++) {

            // Get its type
            let type = queries[i];
            switch (type) {

            // Perform type 1 query
            case 1:
                document.write(getLeftMostZero(zero)+"<br>");
                break;

            // Perform type 2 query
            case 2:
                document.write(getLeftMostOne(one)+"<br>");
                break;

            // Perform type 3 query
            case 3:
                document.write(getLeftMostElement(zero, one)+"<br>");
                break;
            }
        }
}

// Driver code
let arr=[1, 0, 1, 1, 1];
let n = arr.length;
let queries=[1, 3, 1 ];
let q = queries.length;

performQueries(arr, n, queries, q);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
0
1
-1
```
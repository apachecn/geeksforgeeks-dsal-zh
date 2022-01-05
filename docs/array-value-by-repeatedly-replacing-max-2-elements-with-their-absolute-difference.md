# 用最大 2 个元素的绝对差重复替换最大 2 个元素的数组值

> 原文:[https://www . geesforgeks . org/array-value-by-replace-max-2-elements-with-absolute-difference/](https://www.geeksforgeeks.org/array-value-by-repeatedly-replacing-max-2-elements-with-their-absolute-difference/)

给定一个数组 **arr** size **N** ，任务是当数组的最大值和第二个最大值元素被它们在数组中的绝对差替换时，重复打印数组中剩余的最终数组值。

**注意:**如果最大两个元素相同，那么两个元素都从数组中移除，不替换任何值。

**示例:**

> **输入:** arr = [2，7，4，1，8，1]
> **输出:** 1
> **解释:**
> 合并 7 和 8:绝对差= 7–8 = 1。所以数组转换成[2，4，1，1，1]。
> 合并 2 和 4:绝对差= 4–2 = 2。所以数组转换成[2，1，1，1]。
> 合并 2 和 1:绝对差= 2–1 = 1。所以数组转换成[1，1，1]。
> 合并 1 和 1:绝对差= 4–2 = 0。所以没有什么会被合并。
> 所以最终数组= [1]。
> 
> **输入:** arr = [7，10，5，4，11，25]
> **输出:** 2

**高效方法:使用** [**优先队列**](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)

*   [制作优先级队列(二进制最大堆)](https://www.geeksforgeeks.org/max-heap-in-java/)，自动按排序顺序排列元素。
*   然后选择第一个元素(最大值)和第二个元素(第二个最大值)，如果两者相等，则不推送任何内容，如果不相等，则推送队列中两者的绝对差值。
*   执行以上步骤，直到队列大小等于 1，然后返回最后一个元素。如果队列在达到大小 1 之前变空，则返回 0。

下面是上述方法的实现:

## C

```
// C++ program to find the array value
// by repeatedly replacing max 2 elements
// with their absolute difference

#include <bits/stdc++.h>
using namespace std;

// function that return last
// value of array
int lastElement(vector<int>& arr)
{
    // Build a binary max_heap.
    priority_queue<int> pq;
    for (int i = 0; i < arr.size(); i++) {
        pq.push(arr[i]);
    }

    // For max 2 elements
    int m1, m2;

    // Iterate until queue is not empty
    while (!pq.empty()) {

        // if only 1 element is left
        if (pq.size() == 1)

// return the last
// remaining value
            return pq.top();

        m1 = pq.top();
        pq.pop();
        m2 = pq.top();
        pq.pop();

        // check that difference
        // is non zero
        if (m1 != m2)
            pq.push(m1 - m2);
    }

    // finally return 0
    return 0;
}

// Driver Code
int main()
{
    vector<int> arr = { 2, 7, 4, 1, 8, 1, 1 };

    cout << lastElement(arr) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the array value
// by repeatedly replacing max 2 elements
// with their absolute difference
import java.util.*;

class GFG{

// Function that return last
// value of array
static int lastElement(int[] arr)
{

    // Build a binary max_heap
    PriorityQueue<Integer> pq = new PriorityQueue<>(
                                (a, b) -> b - a);

    for(int i = 0; i < arr.length; i++)
        pq.add(arr[i]);

    // For max 2 elements
    int m1, m2;

    // Iterate until queue is not empty
    while(!pq.isEmpty())
    {

        // If only 1 element is left
        if (pq.size() == 1)
        {

            // Return the last
            // remaining value
            return pq.poll();
        }

        m1 = pq.poll();
        m2 = pq.poll();

        // Check that difference
        // is non zero
        if (m1 != m2)
            pq.add(m1 - m2);
    }

    // Finally return 0
    return 0;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = new int[]{2, 7, 4, 1, 8, 1, 1 };

    System.out.println(lastElement(arr));
}
}

// This code is contributed by dadi madhav
```

## 蟒蛇 3

```
# Python3 program to find the array value
# by repeatedly replacing max 2 elements
# with their absolute difference
from queue import PriorityQueue

# Function that return last
# value of array
def lastElement(arr):

    # Build a binary max_heap.
    pq = PriorityQueue()
    for i in range(len(arr)):

        # Multiplying by -1 for
        # max heap
        pq.put(-1 * arr[i])

    # For max 2 elements
    m1 = 0
    m2 = 0

    # Iterate until queue is not empty
    while not pq.empty():

        # If only 1 element is left
        if pq.qsize() == 1:

            # Return the last
            # remaining value
            return -1 * pq.get()
        else:
            m1 = -1 * pq.get()
            m2 = -1 * pq.get()

        # Check that difference
        # is non zero
        if m1 != m2 :
            pq.put(-1 * abs(m1 - m2))

    return 0

# Driver Code
arr = [ 2, 7, 4, 1, 8, 1, 1 ]

print(lastElement(arr))

# This code is contributed by ishayadav181
```

## C#

```
// C# program to find the array value
// by repeatedly replacing max 2 elements
// with their absolute difference
using System;
using System.Collections.Generic;

class GFG{

// Function that return last
// value of array
static int lastElement(int[] arr)
{

    // Build a binary max_heap
    Queue<int> pq = new Queue<int>();

    for(int i = 0; i < arr.Length; i++)
        pq.Enqueue(arr[i]);

    // For max 2 elements
    int m1, m2;

    // Iterate until queue is not empty
    while (pq.Contains(0))
    {

        // If only 1 element is left
        if (pq.Count == 1)
        {

            // Return the last
            // remaining value
            return pq.Peek();
        }

        m1 = pq.Dequeue();
        m2 = pq.Peek();

        // Check that difference
        // is non zero
        if (m1 != m2)
            pq.Enqueue(m1 - m2);
    }

    // Finally return 0
    return 0;
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 2, 7, 4, 1, 8, 1, 1 };

    Console.WriteLine(lastElement(arr));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program to find the array value
// by repeatedly replacing max 2 elements
// with their absolute difference

// function that return last
// value of array
function lastElement(arr) {
    // Build a binary max_heap.
    let pq = [];
    for (let i = 0; i < arr.length; i++) {
        pq.push(arr[i]);
    }

    // For max 2 elements
    let m1, m2;

    // Iterate until queue is not empty
    while (pq.length) {

        // if only 1 element is left
        if (pq.length == 1)

            // return the last
            // remaining value
            return pq[pq.length - 1];

        pq.sort((a, b) => a - b)
        m1 = pq[pq.length - 1];
        pq.pop();
        m2 = pq[pq.length - 1];
        pq.pop();

        // check that difference
        // is non zero
        if (m1 != m2)
            pq.push(m1 - m2);
    }

    // finally return 0
    return 0;
}

// Driver Code

let arr = [2, 7, 4, 1, 8, 1, 1];

document.write(lastElement(arr) + "<br>");

</script>
```

**Output:** 

```
0
```

***时间复杂度:** O(N)*
***辅助复杂度:** O(N)*
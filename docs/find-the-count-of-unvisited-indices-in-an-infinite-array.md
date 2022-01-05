# 求无限数组中未访问索引的个数

> 原文:[https://www . geeksforgeeks . org/find-无限数组中未访问索引的计数/](https://www.geeksforgeeks.org/find-the-count-of-unvisited-indices-in-an-infinite-array/)

给定一个无限长的数组和两个整数 **M** 和 **N** ,它们是同素的，任务是从第一个位置开始，当从**arr【I】**单次移动时，找到不能访问的位置数，可以达到**arr【I+M】**或**arr【I+N】**。**注意**结果总是有限的。

**示例**:

> **输入:** M = 2，N = 5
> T3】输出: 2
> 从指标 0 开始， 可以访问的指数有
> 0+2 = 2
> 0+2+2 = 4
> 0+5 = 5
> 0+2+2+2 = 6
> 0+2+5 = 7
> 0+2+2+2+2 = 8
> 0+2+2+5 = 9
> 0+5+5 = 10
> ……
> 1 和 3 是唯一不能访问的指数。
> 
> **输入:** M = 5，N = 6
> T3】输出: 15

**进场:**

*   使用[弗罗贝纽斯数](https://en.wikipedia.org/wiki/Coin_problem)说出**X =(M * N)–M–N**找到无法使用 **M** & **N** 任意组合获得的最大指数。
*   因为， **X** 是不能访问的最大索引，所以大于它的每个索引都不需要检查。
*   现在，对于小于 **X** 的指数，如果 **X** 不可见，那么**Y = X–M**和**Z = X–N**也不可见，同样的还有**Y–M**和**Z–N**等等..直到指数大于 **0** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach 
#include <bits/stdc++.h>
using namespace std;

// Function to return the count 
// of unvisited indices starting 
// from the index 0 
int countUnvisited(int n, int m)
{

    // Largest index that 
    // cannot be visited 
    int X = (m * n) - m - n; 

    // Push the index to the queue 
    queue<int> queue;

    queue.push(X); 

    // To store the required count 
    int count = 0; 
    while (queue.size() > 0) 
    { 

        // Current index that cannot be visited 
        int curr = queue.front(); 
        queue.pop();

        // Increment the count for 
        // the current index 
        count++; 

        // (curr - m) and (curr - n) are also 
        // unreachable if they are valid indices 
        if (curr - m > 0) 
            queue.push(curr - m); 
        if (curr - n > 0) 
            queue.push(curr - n); 
    } 

    // Return the required count 
    return count; 
}

// Driver code 
int main()
{
    int n = 2, m = 5; 

    cout << countUnvisited(n, m);

    return 0;
}

// This code is contributed by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.LinkedList;
import java.util.Queue;

class GFG {

    // Function to return the count
    // of unvisited indices starting
    // from the index 0
    public static int countUnvisited(int n, int m)
    {

        // Largest index that
        // cannot be visited
        int X = (m * n) - m - n;

        // Push the index to the queue
        Queue<Integer> queue = new LinkedList<>();
        queue.add(X);

        // To store the required count
        int count = 0;
        while (!queue.isEmpty()) {

            // Current index that cannot be visited
            int curr = queue.poll();

            // Increment the count for
            // the current index
            count++;

            // (curr - m) and (curr - n) are also
            // unreachable if they are valid indices
            if (curr - m > 0)
                queue.add(curr - m);
            if (curr - n > 0)
                queue.add(curr - n);
        }

        // Return the required count
        return count;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 2, m = 5;
        System.out.print(countUnvisited(n, m));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach 

# Function to return the count 
# of unvisited indices starting 
# from the index 0 
def countUnvisited(n, m):

    # Largest index that 
    # cannot be visited 
    i = 0
    X = (m * n) - m - n

    # Push the index to the queue 
    queue = []

    queue.append(X)

    # To store the required count 
    count = 0
    while (len(queue) > 0):

        # Current index that cannot be visited 
        curr = queue[0] 
        queue.remove(queue[0])

        # Increment the count for 
        # the current index 
        count += 1

        # (curr - m) and (curr - n) are also 
        # unreachable if they are valid indices 
        if (curr - m > 0):
            queue.append(curr - m) 
        if (curr - n > 0):
            queue.append(curr - n) 

    # Return the required count 
    return count

# Driver code 
if __name__ == '__main__':
    n = 2
    m = 5

    print(countUnvisited(n, m))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach 
using System;
using System.Collections.Generic;

class GFG 
{

    // Function to return the count
    // of unvisited indices starting
    // from the index 0
    public static int countUnvisited(int n, int m)
    {

        // Largest index that
        // cannot be visited
        int X = (m * n) - m - n;

        // Push the index to the queue
        Queue<int> queue = new Queue<int>();
        queue.Enqueue(X);

        // To store the required count
        int count = 0;
        while (queue.Count != 0) 
        {

            // Current index that cannot be visited
            int curr = queue.Dequeue();

            // Increment the count for
            // the current index
            count++;

            // (curr - m) and (curr - n) are also
            // unreachable if they are valid indices
            if (curr - m > 0)
                queue.Enqueue(curr - m);
            if (curr - n > 0)
                queue.Enqueue(curr - n);
        }

        // Return the required count
        return count;
    }

    // Driver code
    public static void Main(String []args)
    {
        int n = 2, m = 5;
        Console.WriteLine(countUnvisited(n, m));
    }
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
2

```
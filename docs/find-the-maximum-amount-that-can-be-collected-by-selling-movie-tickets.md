# 找到卖电影票能收的最大金额

> 原文:[https://www . geeksforgeeks . org/find-通过出售电影票可以收集的最大金额/](https://www.geeksforgeeks.org/find-the-maximum-amount-that-can-be-collected-by-selling-movie-tickets/)

给定一个整数 **N** 和一个数组**座位【】**，其中 **N** 是排队买电影票的人数，**座位【I】**是电影院第**I**排的空座数。任务是找到影院老板通过向 **N** 人出售电影票可以赚到的最大金额。一张票的价格等于所有排中空座位的最大数量。
**例:**

> **输入:**席[] = {1，2，4}，N = 3
> **输出:** 9
> 
> <figure class="table">
> 
> | 人 | 空座位 | 门票成本 |
> | --- | --- | --- |
> | one | 1 2 4 | four |
> | Two | 1 2 3 | three |
> | three | 1 2 2 | Two |
> 
> 4 + 3 + 2 = 9
> **输入:**席[] = {2，3，5，3}，N = 4
> **输出:** 15
> 
> </figure>

**方法:**这个问题可以通过使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)来解决，该队列将存储每行的空座位数，其中最大值将在顶部可用。

*   创建一个空的优先级队列 **q** 并遍历**席位【】**数组，并将所有元素插入优先级队列。
*   初始化两个整数变量 **ticketSold = 0** 和 **ans = 0** ，这两个变量将存储售出的门票数量和迄今为止的总收藏量。
*   现在在**ticket sald<N**和 **q.top() > 0** 时检查，然后从 priority_queue 中移除顶部元素，并通过添加优先级队列的顶部元素来更新 ans。也将该最高值存储在变量**温度**中，并将**温度–1**插入优先级队列。
*   重复这些步骤，直到所有的人都卖了票，打印出最终结果。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum amount
// that can be collected by selling tickets
int maxAmount(int M, int N, int seats[])
{

    // Priority queue that stores
    // the count of empty seats
    priority_queue<int> q;

    // Insert each array element
    // into the priority queue
    for (int i = 0; i < M; i++) {
        q.push(seats[i]);
    }

    // To store the  total
    // number of tickets sold
    int ticketSold = 0;

    // To store the total amount
    // of collection
    int ans = 0;

    // While tickets sold are less than N
    // and q.top > 0 then update the collected
    // amount with the top of the priority
    // queue
    while (ticketSold < N && q.top() > 0) {
        ans = ans + q.top();
        int temp = q.top();
        q.pop();
        q.push(temp - 1);
        ticketSold++;
    }

    return ans;
}

// Driver code
int main()
{
    int seats[] = { 1, 2, 4 };
    int M = sizeof(seats) / sizeof(int);
    int N = 3;

    cout << maxAmount(N, M, seats);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    static int[] seats = new int[]{ 1, 2, 4 };

    // Function to return the maximum amount
    // that can be collected by selling tickets
    public static int maxAmount(int M, int N)
    {

        // Priority queue that stores
        // the count of empty seats
        PriorityQueue<Integer> q =
            new PriorityQueue<Integer>(Collections.reverseOrder());

        // Insert each array element
        // into the priority queue
        for (int i = 0; i < M; i++)
        {
            q.add(seats[i]);
        }

        // To store the total
        // number of tickets sold
        int ticketSold = 0;

        // To store the total amount
        // of collection
        int ans = 0;

        // While tickets sold are less than N
        // and q.top > 0 then update the collected
        // amount with the top of the priority
        // queue
        while (ticketSold < N && q.peek() > 0)
        {
            ans = ans + q.peek();
            int temp = q.peek();
            q.poll();
            q.add(temp - 1);
            ticketSold++;
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int M = seats.length;
        int N = 3;

        System.out.print(maxAmount(M, N));
    }
}

// This code is contributed by Sanjit_Prasad
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the maximum amount
# that can be collected by selling tickets
def maxAmount(M, N, seats):

    # Priority queue that stores
    # the count of empty seats
    q = []

    # Insert each array element
    # into the priority queue
    for i in range(M):
        q.append(seats[i])

    # To store the total
    # number of tickets sold
    ticketSold = 0

    # To store the total amount
    # of collection
    ans = 0

    # While tickets sold are less than N
    # and q.top > 0 then update the collected
    # amount with the top of the priority
    # queue
    q.sort(reverse = True)
    while (ticketSold < N and q[0] > 0):
        ans = ans + q[0]
        temp = q[0]
        q = q[1:]
        q.append(temp - 1)
        q.sort(reverse = True)
        ticketSold += 1

    return ans

# Driver code
if __name__ == '__main__':
    seats = [1, 2, 4]
    M = len(seats)
    N = 3

    print(maxAmount(N, M, seats))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to return the maximum amount
    // that can be collected by selling tickets
    static int maxAmount(int M, int N, int[] seats)
    {

        // Priority queue that stores
        // the count of empty seats
        List<int> q = new List<int>();

        // Insert each array element
        // into the priority queue
        for (int i = 0; i < M; i++) {
            q.Add(seats[i]);
        }

        q.Sort();
        q.Reverse();

        // To store the  total
        // number of tickets sold
        int ticketSold = 0;

        // To store the total amount
        // of collection
        int ans = 0;

        // While tickets sold are less than N
        // and q.top > 0 then update the collected
        // amount with the top of the priority
        // queue
        while (ticketSold < N && q[0] > 0) {
            ans = ans + q[0];
            int temp = q[0];
            q.RemoveAt(0);
            q.Add(temp - 1);
            q.Sort();
            q.Reverse();
            ticketSold++;
        }  
        return ans;
    }

  // Driver code
  static void Main()
  {
    int[] seats = { 1, 2, 4 };
    int M = seats.Length;
    int N = 3;
    Console.WriteLine(maxAmount(N, M, seats));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the maximum amount
    // that can be collected by selling tickets
    function maxAmount(M, N, seats)
    {

        // Priority queue that stores
        // the count of empty seats
        let q = [];

        // Insert each array element
        // into the priority queue
        for (let i = 0; i < M; i++) {
            q.push(seats[i]);
        }

        q.sort(function(a, b){return a - b});
        q.reverse();

        // To store the  total
        // number of tickets sold
        let ticketSold = 0;

        // To store the total amount
        // of collection
        let ans = 0;

        // While tickets sold are less than N
        // and q.top > 0 then update the collected
        // amount with the top of the priority
        // queue
        while ((ticketSold < N) && (q[0] > 0)) {
            ans = ans + q[0];
            let temp = q[0];
            q.shift();
            q.push(temp - 1);
            q.sort(function(a, b){return a - b});
            q.reverse();
            ticketSold++;
        } 
        return ans;
    }

    let seats = [ 1, 2, 4 ];
    let M = seats.length;
    let N = 3;
    document.write(maxAmount(N, M, seats));

</script>
```

**Output:** 

```
9
```

时间复杂度:O(M*logM)

辅助空间:O(M)
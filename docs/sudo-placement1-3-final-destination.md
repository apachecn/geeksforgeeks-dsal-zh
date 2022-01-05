# Sudo 放置[1.3] |最终目的地

> 原文:[https://www . geesforgeks . org/sudo-placement 1-3-final-destination/](https://www.geeksforgeeks.org/sudo-placement1-3-final-destination/)

给定一个整数数组和一个带有初始值和终值的数 K。您的任务是找到从初始值开始使用数组元素获得最终值所需的最小步骤数。您只能对值执行加法(加法运算% 1000)来获得最终值。在每一步中，您都可以通过模数运算添加任何数组元素。

**示例:**

> **输入:**初始= 1，最终= 6，a[] = {1，2，3，4}
> **输出:** 2
> 步骤 1: (1 + 1 ) % 1000 = 2。
> 步骤 2: (2 + 4) % 1000 = 6(这是必需的最终值)。
> 
> **输入:**开始= 998 结束= 2 a[] = {2，1，3}
> **输出:** 2
> 步骤 1 : (998 + 2) % 1000 = 0。
> 第二步:(0 + 2) % 1000 = 2。
> OR
> 第一步:(998 + 1) % 1000 = 999。
> 第二步:(999 + 3) % 1000 = 2

**方法:**由于在上述问题中给定的模数是 1000，因此最大状态数将是 10 <sup>3</sup> 。使用简单的 [BFS](https://www.geeksforgeeks.org/bfs-using-stl-competitive-coding/) 即可检查所有状态。用-1 初始化 ans[]数组，表示该状态未被访问。ans[i]存储从开始到到达 I 所采取的步骤数。首先将起点推到队列中，然后应用 BFS。弹出顶部元素，检查它是否等于结束，如果是，则打印 ans[end]。如果元素不等于最上面的元素，那么将最上面的元素与数组中的每个元素相加，并用 1000 执行 mod 操作。如果之前没有访问过添加的元素状态，则将它推入队列。由 ans[top_element] + 1 初始化 ans[pushed_element]。一旦访问了所有的状态，并且无法通过执行所有可能的乘法来达到该状态，则打印-1。

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum steps
// to reach end from start by performing
// additions and mod operations with array elements
#include <bits/stdc++.h>
using namespace std;

// Function that returns the minimum operations
int minimumAdditions(int start, int end, int a[], int n)
{
    // array which stores the minimum steps
    // to reach i from start
    int ans[1001];

    // -1 indicated the state has not been visited
    memset(ans, -1, sizeof(ans));
    int mod = 1000;

    // queue to store all possible states
    queue<int> q;

    // initially push the start
    q.push(start % mod);

    // to reach start we require 0 steps
    ans[start] = 0;

    // till all states are visited
    while (!q.empty()) {

        // get the topmost element in the queue
        int top = q.front();

        // pop the topmost element
        q.pop();

        // if the topmost element is end
        if (top == end)
            return ans[end];

        // perform addition with all array elements
        for (int i = 0; i < n; i++) {
            int pushed = top + a[i];
            pushed = pushed % mod;

            // if not visited, then push it to queue
            if (ans[pushed] == -1) {
                ans[pushed] = ans[top] + 1;
                q.push(pushed);
            }
        }
    }
    return -1;
}

// Driver Code
int main()
{
    int start = 998, end = 2;
    int a[] = { 2, 1, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    // Calling function
    cout << minimumAdditions(start, end, a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum steps
// to reach end from start by performing
// additions and mod operations with array elements
import java.util.*;

class GFG
{

    // Function that returns
    // the minimum operations
    static int minimumAdditions(int start,
                    int end, int a[], int n)
    {
        // array which stores the minimum steps
        // to reach i from start
        int ans[] = new int[1001];

        // -1 indicated the state has not been visited
        Arrays.fill(ans, -1);
        int mod = 1000;

        // queue to store all possible states
        Queue<Integer> q = new java.util.LinkedList<>();

        // initially push the start
        q.add(start % mod);

        // to reach start we require 0 steps
        ans[start] = 0;

        // till all states are visited
        while (!q.isEmpty())
        {

            // get the topmost element in the queue
            int top = q.peek();

            // pop the topmost element
            q.poll();

            // if the topmost element is end
            if (top == end)
            {
                return ans[end];
            }

            // perform addition with all array elements
            for (int i = 0; i < n; i++)
            {
                int pushed = top + a[i];
                pushed = pushed % mod;

                // if not visited, then push it to queue
                if (ans[pushed] == -1)
                {
                    ans[pushed] = ans[top] + 1;
                    q.add(pushed);
                }
            }
        }
        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int start = 998, end = 2;
        int a[] = {2, 1, 3};
        int n = a.length;

        // Calling function
        System.out.println(minimumAdditions(start, end, a, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to find the minimum steps
# to reach end from start by performing
# additions and mod operations with array
# elements
from collections import deque
from typing import List

# Function that returns the minimum operations
def minimumAdditions(start: int, end: int,
                     a: List[int], n: int) -> int:

    # Array which stores the minimum steps
    # to reach i from start
    # -1 indicated the state has not been visited
    ans = [-1] * 1001

    mod = 1000

    # Queue to store all possible states
    q = deque()

    # Initially push the start
    q.append(start % mod)

    # To reach start we require 0 steps
    ans[start] = 0

    # Till all states are visited
    while q:

        # Get the topmost element in the queue
        top = q[0]

        # Pop the topmost element
        q.popleft()

        # If the topmost element is end
        if (top == end):
            return ans[end]

        # Perform addition with all array elements
        for i in range(n):
            pushed = top + a[i]
            pushed = pushed % mod

            # If not visited, then push it to queue
            if (ans[pushed] == -1):
                ans[pushed] = ans[top] + 1
                q.append(pushed)

    return -1

# Driver Code
if __name__ == "__main__":

    start = 998
    end = 2
    a = [ 2, 1, 3 ]
    n = len(a)

    # Calling function
    print(minimumAdditions(start, end, a, n))

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to find the minimum steps
// to reach end from start by performing
// additions and mod operations with array elements
using System;
using System.Collections.Generic;

class GFG
{

    // Function that returns
    // the minimum operations
    static int minimumAdditions(int start,
                    int end, int []a, int n)
    {
        // array which stores the minimum steps
        // to reach i from start
        int []ans = new int[1001];

        // -1 indicated the state has not been visited
        for(int i = 0; i < 1001; i++)
        {
            ans[i] = -1;
        }
        int mod = 1000;

        // queue to store all possible states
        Queue<int> q = new Queue<int>();

        // initially push the start
        q.Enqueue(start % mod);

        // to reach start we require 0 steps
        ans[start] = 0;

        // till all states are visited
        while (q.Count != 0)
        {

            // get the topmost element in the queue
            int top = q.Peek();

            // pop the topmost element
            q.Dequeue();

            // if the topmost element is end
            if (top == end)
            {
                return ans[end];
            }

            // perform addition with all array elements
            for (int i = 0; i < n; i++)
            {
                int pushed = top + a[i];
                pushed = pushed % mod;

                // if not visited, then push it to queue
                if (ans[pushed] == -1)
                {
                    ans[pushed] = ans[top] + 1;
                    q.Enqueue(pushed);
                }
            }
        }
        return -1;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int start = 998, end = 2;
        int []a = {2, 1, 3};
        int n = a.Length;

        // Calling function
        Console.WriteLine(minimumAdditions(start, end, a, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find the minimum steps
// to reach end from start by performing
// additions and mod operations with array elements

// Function that returns
    // the minimum operations
function minimumAdditions(start,end,a,n)
{
    // array which stores the minimum steps
        // to reach i from start
        let ans = new Array(1001);

        // -1 indicated the state has not been visited
        for(let i=0;i<1001;i++)
            ans[i]=-1;
        let mod = 1000;

        // queue to store all possible states
        let q = [];

        // initially push the start
        q.push(start % mod);

        // to reach start we require 0 steps
        ans[start] = 0;

        // till all states are visited
        while (q.length!=0)
        {

            // get the topmost element in the queue
            let top = q[0];

            // pop the topmost element
            q.shift();

            // if the topmost element is end
            if (top == end)
            {
                return ans[end];
            }

            // perform addition with all array elements
            for (let i = 0; i < n; i++)
            {
                let pushed = top + a[i];
                pushed = pushed % mod;

                // if not visited, then push it to queue
                if (ans[pushed] == -1)
                {
                    ans[pushed] = ans[top] + 1;
                    q.push(pushed);
                }
            }
        }
        return -1;
}

// Driver Code
let start = 998, end = 2;
let a=[2, 1, 3];
let n = a.length;

// Calling function
document.write(minimumAdditions(start, end, a, n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
2
```

**时间复杂度** : O(N)
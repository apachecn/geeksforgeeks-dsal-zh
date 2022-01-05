# 达到一级的最小步长

> 原文:[https://www.geeksforgeeks.org/minimum-step-reach-one/](https://www.geeksforgeeks.org/minimum-step-reach-one/)

给定一个正数 N，我们需要在最小步数上达到 1，其中一步被定义为把 N 转换成(N-1)或把 N 转换成它的一个较大的除数。

形式上，如果我们在 N，那么在第一步中，我们可以达到(N–1)，或者如果 N = u*v，那么我们可以达到最大值(u，v)，其中 u > 1，v > 1。

示例:

```
Input : N = 17
Output : 4
We can reach to 1 in 4 steps as shown below,
17 -> 16(from 17 - 1) -> 4(from 4 * 4) -> 
2(from 2 * 2) -> 1(from 2 - 1)

Input : N = 50
Output : 5
We can reach to 1 in 5 steps as shown below,
50 -> 10(from 5 * 10) -> 5(from 2 * 5) -> 
4(from 5 - 1) -> 2(from 2 *2) -> 1(from 2 - 1)
```

我们可以使用广度优先搜索来解决这个问题，因为它逐级工作，所以我们将在最少的步骤数中达到 1，其中 N 的下一级包含(N–1)和更大的 N 的适当因子。
完整的 BFS 过程如下:首先，我们将步骤为 0 的 N 推入数据队列，然后在每一级，我们将推他们的下一级元素，比其前一级元素多 1 步。这样，当 1 从队列中弹出时，它将包含最少的步骤数，这将是我们的最终结果。
在下面的代码中，使用了一个“数据”类型结构的队列，它存储了值和从 N 开始的步长，另一组整数类型用于避免我们多次推送同一元素，这可能导致无限循环。因此，在每一步，我们在将值推入队列后，将该值推入 set，这样该值不会被访问超过一次。

请参见下面的代码，以便更好地理解，

## C++

```
//  C++ program to get minimum step to reach 1
// under given constraints
#include <bits/stdc++.h>
using namespace std;

//  structure represent one node in queue
struct data
{
    int val;
    int steps;
    data(int val, int steps) : val(val), steps(steps)
    {}
};

//  method returns minimum step to reach one
int minStepToReachOne(int N)
{
    queue<data> q;
    q.push(data(N, 0));

    // set is used to visit numbers so that they
    // won't be pushed in queue again
    set<int> st;

    //  loop until we reach to 1
    while (!q.empty())
    {
        data t = q.front();     q.pop();

        // if current data value is 1, return its
        // steps from N
        if (t.val == 1)
            return t.steps;

        //  check curr - 1, only if it not visited yet
        if (st.find(t.val - 1) == st.end())
        {
            q.push(data(t.val - 1, t.steps + 1));
            st.insert(t.val - 1);
        }

        //  loop from 2 to sqrt(value) for its divisors
        for (int i = 2; i*i <= t.val; i++)
        {

            // check divisor, only if it is not visited yet
            // if i is divisor of val, then val / i will
            // be its bigger divisor
            if (t.val % i == 0 && st.find(t.val / i) == st.end())
            {
                q.push(data(t.val / i, t.steps + 1));
                st.insert(t.val / i);
            }
        }
    }
}

//  Driver code to test above methods
int main()
{
    int N = 17;
    cout << minStepToReachOne(N) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get minimum step to reach 1
// under given constraints
import java.util.*;

class GFG
{

// structure represent one node in queue
static class data
{
    int val;
    int steps;
    public data(int val, int steps)
    {
        this.val = val;
        this.steps = steps;
    }

};

// method returns minimum step to reach one
static int minStepToReachOne(int N)
{
    Queue<data> q = new LinkedList<>();
    q.add(new data(N, 0));

    // set is used to visit numbers so that they
    // won't be pushed in queue again
    HashSet<Integer> st = new HashSet<Integer>();

    // loop until we reach to 1
    while (!q.isEmpty())
    {
        data t = q.peek(); q.remove();

        // if current data value is 1, return its
        // steps from N
        if (t.val == 1)
            return t.steps;

        // check curr - 1, only if it not visited yet
        if (!st.contains(t.val - 1))
        {
            q.add(new data(t.val - 1, t.steps + 1));
            st.add(t.val - 1);
        }

        // loop from 2 to Math.sqrt(value) for its divisors
        for (int i = 2; i*i <= t.val; i++)
        {

            // check divisor, only if it is not visited yet
            // if i is divisor of val, then val / i will
            // be its bigger divisor
            if (t.val % i == 0 && !st.contains(t.val / i) )
            {
                q.add(new data(t.val / i, t.steps + 1));
                st.add(t.val / i);
            }
        }
    }
    return -1;
}

// Driver code 
public static void main(String[] args)
{
    int N = 17;
    System.out.print(minStepToReachOne(N) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program to get minimum step to reach 1
// under given constraints
using System;
using System.Collections.Generic;

class GFG
{

// structure represent one node in queue
class data
{
    public int val;
    public int steps;
    public data(int val, int steps)
    {
        this.val = val;
        this.steps = steps;
    }
};

// method returns minimum step to reach one
static int minStepToReachOne(int N)
{
    Queue<data> q = new Queue<data>();
    q.Enqueue(new data(N, 0));

    // set is used to visit numbers so that they
    // won't be pushed in queue again
    HashSet<int> st = new HashSet<int>();

    // loop until we reach to 1
    while (q.Count != 0)
    {
        data t = q.Peek(); q.Dequeue();

        // if current data value is 1, return its
        // steps from N
        if (t.val == 1)
            return t.steps;

        // check curr - 1, only if it not visited yet
        if (!st.Contains(t.val - 1))
        {
            q.Enqueue(new data(t.val - 1, t.steps + 1));
            st.Add(t.val - 1);
        }

        // loop from 2 to Math.Sqrt(value) for its divisors
        for (int i = 2; i*i <= t.val; i++)
        {

            // check divisor, only if it is not visited yet
            // if i is divisor of val, then val / i will
            // be its bigger divisor
            if (t.val % i == 0 && !st.Contains(t.val / i) )
            {
                q.Enqueue(new data(t.val / i, t.steps + 1));
                st.Add(t.val / i);
            }
        }
    }
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    int N = 17;
    Console.Write(minStepToReachOne(N) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to get minimum step
// to reach 1 under given constraints

// Structure represent one node in queue
class data
{
    constructor(val, steps)
    {
        this.val = val;
        this.steps = steps;
    }
}

// Method returns minimum step to reach one
function minStepToReachOne(N)
{
    let q = [];
    q.push(new data(N, 0));

    // Set is used to visit numbers
    // so that they won't be pushed
    // in queue again
    let st = new Set();

    // Loop until we reach to 1
    while (q.length != 0)
    {
        let t = q.shift();

        // If current data value is 1,
        // return its steps from N
        if (t.val == 1)
            return t.steps;

        // Check curr - 1, only if
        // it not visited yet
        if (!st.has(t.val - 1))
        {
            q.push(new data(t.val - 1,
                          t.steps + 1));
            st.add(t.val - 1);
        }

        // Loop from 2 to Math.sqrt(value)
        // for its divisors
        for(let i = 2; i*i <= t.val; i++)
        {

            // Check divisor, only if it is not
            // visited yet if i is divisor of val,
            // then val / i will be its bigger divisor
            if (t.val % i == 0 && !st.has(t.val / i))
            {
                q.push(new data(t.val / i,
                              t.steps + 1));
                st.add(t.val / i);
            }
        }
    }
    return -1;
}

// Driver code 
let N = 17;
document.write(minStepToReachOne(N) + "<br>");

// This code is contributed by rag2127

</script>
```

**输出:**

```
4
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
# 找出给定数字

的最小二进制数倍

> 原文： [https://www.geeksforgeeks.org/find-the-smallest-binary-digit-multiple-of-given-number/](https://www.geeksforgeeks.org/find-the-smallest-binary-digit-multiple-of-given-number/)

如果十进制数字的数字是二进制的，则称其为**二进制数字数字**。 例如，102 不是二进制数字，而 101 是。
我们给定十进制数 N，我们需要找到 N 的最小倍数，即二进制数。
**示例：**

```
Input : N = 2
Output: 10
Explanation: 10 is a multiple of 2\. 
              Note that 5 * 2 = 10

Input  : N = 17
Output : 11101
Explanation: 11101 is a multiple of 17\. 
              Note that 653 * 17 = 11101

```

我们可以使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 解决此问题，隐式图的每个节点将是一个二进制数字，如果数字是 x，则其下一级节点将是 x0 和 x1（x 分别与 0 和 1 串联） ）。
首先，我们将 1 推入队列，稍后将 10 和 11 推入队列，依此类推，从队列中取出数字后，我们将检查该数字是否为给定数字的倍数， 如果是，则返回该数字作为结果，这将是我们的最终结果，因为 BFS 逐级进行，因此我们得到的第一个答案也将是我们的最小答案。
在下面的代码中，二进制数字被视为字符串，因为对于某些数字而言，它可能非常大且可能超出甚至更长的限制，因此还对存储为字符串的数字执行了 mod 操作。
代码的主要优化调整是使用一组模块化值，如果以前曾出现过具有相同 mod 值的字符串，我们不会将此新字符串推送到我们的队列中。 不解释新字符串的原因如下：
令 x 和 y 为字符串，它具有相同的模数值。 令 x 为较小的一个。 令 z 为另一个字符串，该字符串在附加到 y 时会给我们提供一个可被 N 整除的数字。 因此，我们可以放心地忽略 y，因为最小的结果只能通过 x 获得。

## C ++

```

// C++ code to get the smallest multiple of N with
// binary digits only.
#include <bits/stdc++.h>
using namespace std;

// Method return t % N, where t is stored as
// a string
int mod(string t, int N)
{
    int r = 0;
    for (int i = 0; i < t.length(); i++)
    {
        r = r * 10 + (t[i] - '0');
        r %= N;
    }
    return r;
}

// method returns smallest multiple which has
// binary digits
string getMinimumMultipleOfBinaryDigit(int N)
{
    queue<string> q;
    set<int> visit;

    string t = "1";

    //  In starting push 1 into our queue
    q.push(t);

    //  loop untill queue is not empty
    while (!q.empty())
    {
        // Take the front number from queue.
        t = q.front();      q.pop();

        // Find remainder of t with respect to N.
        int rem = mod(t, N);

        // if remainder is 0 then we have
        // found our solution
        if (rem == 0)
            return t;

        // If this remainder is not previously seen,
        // then push t0 and t1 in our queue
        else if(visit.find(rem) == visit.end())
        {
            visit.insert(rem);
            q.push(t + "0");
            q.push(t + "1");
        }
    }
}

//  Driver code to test above methods
int main()
{
    int N = 12;
    cout << getMinimumMultipleOfBinaryDigit(N);
    return 0;
}

```

## 爪哇

```

// Java code to get the smallest multiple
// of N with binary digits only.
import java.util.*;
import java.io.*;

class GFG{

// Method return t % N, where t is stored as
// a string
public static int mod(String t, int N)
{
    int r = 0;
    for(int i = 0; i < t.length(); i++)
    {
        r = r * 10 + (t.charAt(i) - '0');
        r %= N;
    }
    return r;
}

// method returns smallest multiple which has
// binary digits
public static String getMinimumMultipleOfBinaryDigit(int N)
{
    Queue<String> q = new LinkedList<String>();
    Set<Integer> visit = new HashSet<>();

    String t = "1";

    // In starting push 1 into our queue
    q.add(t);

    // loop untill queue is not empty
    while (!q.isEmpty())
    {

        // Take the front number from queue.
        t = q.remove();

        // Find remainder of t with respect to N.
        int rem = mod(t, N);

        // If remainder is 0 then we have
        // found our solution
        if (rem == 0)
            return t;

        // If this remainder is not previously seen,
        // then push t0 and t1 in our queue
        else if(!visit.contains(rem))
        {
            visit.add(rem);
            q.add(t + "0");
            q.add(t + "1");
        }
    }
    return "";
}

// Driver code 
public static void main (String[] args)
{
    int N = 12;
    System.out.println(
        getMinimumMultipleOfBinaryDigit(N));
}
}

// This code is contributed by 
// Naresh Saharan and Sagar Jangra

```

## Python3

```

def getMinimumMultipleOfBinaryDigit(A):

    # queue for BFS
    q = []

    # set of visited remainders
    visitedRem = set([]) 
    t = '1'
    q.append(t)
    while q:
        t = q.pop(0)
        rem = int(t) % A
        if rem == 0:
            return t
        if rem not in visitedRem:
            visitedRem.add(rem)
            q.append(t+'0')
            q.append(t+'1')

# Driver code
n = 12
print( getMinimumMultipleOfBinaryDigit(n))

# This code is contributed
# by Jeet9

```

## C＃

```

// C# code to get the smallest 
// multiple of N with binary 
// digits only.
using System;
using System.Collections.Generic;
class GFG{

// Method return t % N, 
// where t is stored as
// a string
public static int mod(String t, 
                      int N)
{
  int r = 0;
  for(int i = 0; 
          i < t.Length; i++)
  {
    r = r * 10 + (t[i] - '0');
    r %= N;
  }
  return r;
}

// method returns smallest 
// multiple which has
// binary digits
public static String getMinimumMultipleOfBinaryDigit(int N)
{
  Queue<String> q = new Queue<String>();
  HashSet<int> visit = new HashSet<int>();

  String t = "1";

  // In starting push 1 
  // into our queue
  q.Enqueue(t);

  // loop untill queue 
  // is not empty
  while (q.Count != 0)
  {
    // Take the front number 
    // from queue.
    t = q.Dequeue();

    // Find remainder of t 
    // with respect to N.
    int rem = mod(t, N);

    // If remainder is 0 then
    // we have found our solution
    if (rem == 0)
      return t;

    // If this remainder is not 
    // previously seen, then push 
    // t0 and t1 in our queue
    else if(!visit.Contains(rem))
    {
      visit.Add(rem);
      q.Enqueue(t + "0");
      q.Enqueue(t + "1");
    }
  }
  return "";
}

// Driver code 
public static void Main(String[] args)
{
  int N = 12;
  Console.WriteLine(getMinimumMultipleOfBinaryDigit(N));
}
}

// This code is contributed by Rajput-Ji

```

**输出：**

```
11100

```

本文由 [**Utkarsh Trivedi**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。


# 求给定数的最小二进制数倍数

> 原文:[https://www . geesforgeks . org/find-最小二进制数字-给定数字的倍数/](https://www.geeksforgeeks.org/find-the-smallest-binary-digit-multiple-of-given-number/)

如果一个十进制数的位数是二进制的，则称之为**二进制数**。例如，102 不是二进制数字，101 是。
给我们一个十进制数 N，我们需要找到 N 的最小倍数这是一个二进制数，
T4【示例:

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

我们可以使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 来解决这个问题，隐式图的每个节点都将是一个二进制数字，如果这个数字是 x，那么它的下一级节点将是 x0 和 x1 (x 与 0 和 1 连接)。
在开始时，我们将把 1 推入我们的队列，这将把 10 和 11 推入队列，以此类推，从队列中取出数字后，我们将检查这个数字是否是给定数字的倍数，如果是，则返回这个数字作为结果，这将是我们的最终结果，因为 BFS 一级一级地进行，所以我们得到的第一个答案也将是我们的最小答案。
在下面的代码中，二进制数字被视为字符串，因为对于某些数字来说，它可能非常大，并且可能超出偶数长的限制，所以对存储为字符串的数字也执行 mod 操作。
代码的主要优化调整是使用一组模值，如果之前出现了一个具有相同模值的字符串，我们不会将这个新字符串推入我们的队列。不推新字符串的原因解释如下，
让 x 和 y 为字符串，给出相同的模值。让 x 是较小的那个。让 z 是另一个字符串，当它附加到 y 时，给我们一个可被 n 整除的数，如果是这样，那么我们也可以将这个字符串附加到 x，它比 y 小，但仍然得到一个可被 n 整除的数，所以我们可以放心地忽略 y，因为最小的结果将只通过 x 得到。

## C++

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

    //  loop until queue is not empty
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

## Java 语言(一种计算机语言，尤用于创建网站)

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

    // loop until queue is not empty
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

## 蟒蛇 3

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

## C#

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

  // loop until queue
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

**输出:**

```
11100
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
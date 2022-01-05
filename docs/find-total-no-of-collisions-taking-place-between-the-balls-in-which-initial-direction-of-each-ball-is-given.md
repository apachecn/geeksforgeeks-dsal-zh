# 找出给出每个球初始方向的球之间发生碰撞的总数

> 原文:[https://www . geeksforgeeks . org/find-球与球之间完全没有碰撞发生-每个球的初始方向是给定的/](https://www.geeksforgeeks.org/find-total-no-of-collisions-taking-place-between-the-balls-in-which-initial-direction-of-each-ball-is-given/)

给定一行中的 N 个球。每个球的初始方向由分别只包含“L”和“R”的左右方向的字符串表示。假设两个球在碰撞后方向相反，速度在碰撞前后保持不变。计算发生碰撞的总数。
**例:**

```
Input: str = "RRLL"
Output: 4

Explanation
After first collision: RLRL
After second collision: LRRL
After third collision: LRLR
After fourth collision: LLRR

Input: str = "RRLR"
Output:  2

Explanation
After first collision: RLRR
After second collision: LRRR
```

**方法:**
在每个阶段，我们必须找到子串“RL”的数量，将子串“RL”更改为“LR”，并再次计算结果字符串中子串“RL”的数量，并在下面重复，直到没有其他子串“RL”可用。我们不会在每个阶段计算子串“RL”的数量，因为这将消耗大量时间。另一种方法是，观察我们在每个阶段看到的以下结果字符串–>“RRLL”->“RLRL”->“LRLR”->“LLRR”。
首串为“RRLL”。让我们来看第三个球，它的方向是 L。现在观察这个 L 向弦的左边移动。当我们把“RL”换成“LR”的时候，我们就把 L 移向了整个字符串的左边。现在类似地，如果我们继续这个交换，这个 L 将面对那个弦左边的每个 R，所以再次形成“RL”。因此，对于这个 L，“r L”的总数将是出现在那个特定 L 的左侧的 R 的总数。我们将对每个 L 重复这个。因此，一般来说，为了在每个阶段计数每个可能的子串“RL”，我们将计数每个 L 的左侧的表示的总数，因为这些 R 和 L 将在每个阶段形成“RL”，这可以以线性时间复杂度来完成。
以下是上述方法的实施:

## C++

```
// C++ implementation to Find total
// no of collisions taking place between
// the balls in which initial direction
// of each ball is given

#include <bits/stdc++.h>
using namespace std;

// Function to count no of collision
int count(string s)
{
    int N, i, cnt = 0, ans = 0;

    // length of the string
    N = s.length();

    for (i = 0; i < N; i++) {
        if (s[i] == 'R')
            cnt++;

        if (s[i] == 'L')
            ans += cnt;
    }

    return ans;
}

// Driver code
int main()
{

    string s = "RRLL";

    cout << count(s) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Find total
// no of collisions taking place between
// the balls in which initial direction
// of each ball is given
import java.io.*;
class GFG {

// Function to count
// no of collision
static int count(String s)
{
  int N, i, cnt = 0, ans = 0;

  // length of the string
  N = s.length();

  for (i = 0; i < N; i++)
  {
    if (s.charAt(i) == 'R')
      cnt++;

    if (s.charAt(i) == 'L')
      ans += cnt;
  }
  return ans;
}

// Driver code
static public void main(String[] args)
{
  String s = "RRLL";
  System.out.println(count(s));
}
}

// This code is contributed by Rutvik_56
```

## 蟒蛇 3

```
# Python3 implementation to find total
# no of collisions taking place between
# the balls in which initial direction
# of each ball is given

# Function to count no of collision
def count(s):

    cnt, ans = 0, 0

    # Length of the string
    N = len(s)

    for i in range(N):
        if (s[i] == 'R'):
            cnt += 1

        if (s[i] == 'L'):
            ans += cnt

    return ans

# Driver code
s = "RRLL"

print( count(s))

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to Find total
// no of collisions taking place between
// the balls in which initial direction
// of each ball is given
using System;

class GFG{

// Function to count no of collision
static int count(String s)
{
    int N, i, cnt = 0, ans = 0;

    // length of the string
    N = s.Length;

    for(i = 0; i < N; i++)
    {
        if (s[i] == 'R')
            cnt++;

        if (s[i] == 'L')
            ans += cnt;
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    String s = "RRLL";

    Console.Write(count(s));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
  // Javascript implementation to Find total
  // no of collisions taking place between
  // the balls in which initial direction
  // of each ball is given

  // Function to count no of collision
  function count(s)
  {
      let N, i, cnt = 0, ans = 0;

      // length of the string
      N = s.length;

      for (i = 0; i < N; i++) {
          if (s[i] == 'R')
              cnt++;

          if (s[i] == 'L')
              ans += cnt;
      }

      return ans;
  }

  let s = "RRLL";

  document.write(count(s));

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
4
```

时间复杂度:0(N)

辅助空间:0(1)
# 一个骑士在 k 次移动中可以移动到的棋盘方块数

> 原文:[https://www . geeksforgeeks . org/棋盘中的方块数-骑士可以移动到精确的 k-moves/](https://www.geeksforgeeks.org/number-of-blocks-in-a-chessboard-a-knight-can-move-to-in-exactly-k-moves/)

给定整数 **i，j，k 和 n** ，其中 **(i，j)** 是骑士在 **n * n** 棋盘上的初始位置，任务是找到骑士在 **k** 移动中可以移动到的位置数量。
**举例:**

> **输入:** i = 5，j = 5，k = 1，n = 10
> **输出:** 8
> **输入:** i = 0，j = 0，k = 2，n = 10
> **输出:** 10
> 骑士在第 2 次移动中总共可以看到 10 个不同的位置。

**方法:**使用[递归方法](https://www.geeksforgeeks.org/recursion/)解决问题。
首先找到骑士可以移动到的所有可能位置，如果初始位置是 **i，j** 。在一次移动中到达所有有效的位置，并递归地找到骑士可以在**k–1**步中移动到的所有可能位置。这种递归的基本情况是当 **k == 0** (不移动)时，如果棋盘没有标记，我们会将棋盘的位置标记为已访问，并增加计数。最后，显示计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// function that will be called recursively
int recursive_solve(int i, int j, int steps, int n,
                      map<pair<int, int>, int> &m)
{
    // If there's no more move to make and
    // this position hasn't been visited before
    if (steps == 0 && m[make_pair(i, j)] == 0) {

        // mark the position
        m[make_pair(i, j)] = 1;

        // increase the count       
        return 1;
    }

    int res = 0;
    if (steps > 0) {

        // valid movements for the knight
        int dx[] = { -2, -1, 1, 2, -2, -1, 1, 2 };
        int dy[] = { -1, -2, -2, -1, 1, 2, 2, 1 };

        // find all the possible positions
        // where knight can move from i, j
        for (int k = 0; k < 8; k++) {

            // if the positions lies within the
            // chessboard
            if ((dx[k] + i) >= 0
                && (dx[k] + i) <= n - 1
                && (dy[k] + j) >= 0
                && (dy[k] + j) <= n - 1) {

                // call the function with k-1 moves left
                res += recursive_solve(dx[k] + i, dy[k] + j,
                                       steps - 1, n, m);
            }
        }
    }
    return res;
}

// find all the positions where the knight can
// move after k steps
int solve(int i, int j, int steps, int n)
{
    map<pair<int, int>, int> m;
    return recursive_solve(i, j, steps, n, m);
}

// driver code
int main()
{
    int i = 0, j = 0, k = 2, n = 10;

    cout << solve(i, j, k, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
import java.awt.Point;
public class GFG
{

  // function that will be called recursively
  static int recursive_solve(int i, int j, int steps, int n,
                             HashMap<Point,Integer> m)
  {

    // If there's no more move to make and
    // this position hasn't been visited before
    if (steps == 0 && !m.containsKey(new Point(i, j)))
    {

      // mark the position
      m.put(new Point(i, j), 1);

      // increase the count       
      return 1;
    }
    int res = 0;
    if (steps > 0)
    {

      // valid movements for the knight
      int[] dx = { -2, -1, 1, 2, -2, -1, 1, 2 };
      int[] dy = { -1, -2, -2, -1, 1, 2, 2, 1 };

      // find all the possible positions
      // where knight can move from i, j
      for (int k = 0; k < 8; k++)
      {

        // if the positions lies within the
        // chessboard
        if ((dx[k] + i) >= 0
            && (dx[k] + i) <= n - 1
            && (dy[k] + j) >= 0
            && (dy[k] + j) <= n - 1)
        {

          // call the function with k-1 moves left
          res += recursive_solve(dx[k] + i, dy[k] + j,
                                 steps - 1, n, m);
        }
      }
    }
    return res;
  }

  // find all the positions where the knight can
  // move after k steps
  static int solve(int i, int j, int steps, int n)
  {
    HashMap<Point, Integer> m = new HashMap<>();
    return recursive_solve(i, j, steps, n, m);
  }

  // Driver code
  public static void main(String[] args)
  {
    int i = 0, j = 0, k = 2, n = 10;
    System.out.print(solve(i, j, k, n));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 implementation of above approach
from collections import defaultdict

# Function that will be called recursively
def recursive_solve(i, j, steps, n, m):

    # If there's no more move to make and
    # this position hasn't been visited before
    if steps == 0 and m[(i, j)] == 0:

        # mark the position
        m[(i, j)] = 1

        # increase the count        
        return 1

    res = 0
    if steps > 0:

        # valid movements for the knight
        dx = [-2, -1, 1, 2, -2, -1, 1, 2]
        dy = [-1, -2, -2, -1, 1, 2, 2, 1]

        # find all the possible positions
        # where knight can move from i, j
        for k in range(0, 8):

            # If the positions lies
            # within the chessboard
            if (dx[k] + i >= 0 and
                dx[k] + i <= n - 1 and
                dy[k] + j >= 0 and
                dy[k] + j <= n - 1):

                # call the function with k-1 moves left
                res += recursive_solve(dx[k] + i, dy[k] + j,
                                       steps - 1, n, m)

    return res

# Find all the positions where the
# knight can move after k steps
def solve(i, j, steps, n):

    m = defaultdict(lambda:0)
    return recursive_solve(i, j, steps, n, m)

# Driver code
if __name__ == "__main__":

    i, j, k, n = 0, 0, 2, 10

    print(solve(i, j, k, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// function that will be called recursively
static int recursive_solve(int i, int j, int steps, int n,
                      Dictionary<Tuple<int,int>,int>m)
{
    // If there's no more move to make and
    // this position hasn't been visited before
    if (steps == 0 && !m.ContainsKey(new Tuple<int,int>(i, j))) {

        // mark the position
        m[new Tuple<int,int>(i, j)] = 1;

        // increase the count       
        return 1;
    }

    int res = 0;

    if (steps > 0) {

        // valid movements for the knight
        int []dx = { -2, -1, 1, 2, -2, -1, 1, 2 };
        int []dy = { -1, -2, -2, -1, 1, 2, 2, 1 };

        // find all the possible positions
        // where knight can move from i, j
        for (int k = 0; k < 8; k++) {

            // if the positions lies within the
            // chessboard
            if ((dx[k] + i) >= 0
                && (dx[k] + i) <= n - 1
                && (dy[k] + j) >= 0
                && (dy[k] + j) <= n - 1) {

                // call the function with k-1 moves left
                res += recursive_solve(dx[k] + i, dy[k] + j,
                                       steps - 1, n, m);
            }
        }
    }
    return res;
}

// find all the positions where the knight can
// move after k steps
static int solve(int i, int j, int steps, int n)
{
    Dictionary<Tuple<int,int>,int> m=new Dictionary<Tuple<int,int>,int>();
    return recursive_solve(i, j, steps, n, m);
}

// driver code
public static void Main(params string []args)
{
    int i = 0, j = 0, k = 2, n = 10;

    Console.Write(solve(i, j, k, n));

}
}
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    // function that will be called recursively
    function recursive_solve(i, j, steps, n, m)
    {
        // If there's no more move to make and
        // this position hasn't been visited before
        if (steps == 0 && !m.has([i, j])) {

            // mark the position
            m[[i, j]] = 1;

            // increase the count      
            return 1;
        }

        let res = 0;

        if (steps > 0) {

            // valid movements for the knight
            let dx = [ -2, -1, 1, 2, -2, -1, 1, 2 ];
            let dy = [ -1, -2, -2, -1, 1, 2, 2, 1 ];

            // find all the possible positions
            // where knight can move from i, j
            for (let k = 0; k < 8; k++) {

                // if the positions lies within the
                // chessboard
                if ((dx[k] + i) >= 0
                    && (dx[k] + i) <= n - 1
                    && (dy[k] + j) >= 0
                    && (dy[k] + j) <= n - 1) {

                    // call the function with k-1 moves left
                    res += recursive_solve(dx[k] + i, dy[k] + j,
                                           steps - 1, n, m);
                }
            }
        }
        return res;
    }

    // find all the positions where the knight can
    // move after k steps
    function solve(i, j, steps, n)
    {
        let m = new Map();
        return recursive_solve(i, j, steps, n, m)-2;
    }

    let i = 0, j = 0, k = 2, n = 10;

    document.write(solve(i, j, k, n));

// This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
10
```
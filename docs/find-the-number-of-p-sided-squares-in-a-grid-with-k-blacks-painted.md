# 找出涂有 K 黑的网格中 p 边正方形的数量

> 原文:[https://www . geeksforgeeks . org/find-带 k-blacks-painting 的网格中 p 面正方形的数量/](https://www.geeksforgeeks.org/find-the-number-of-p-sided-squares-in-a-grid-with-k-blacks-painted/)

给定一个大小为 H*W 的网格，所有单元格最初都是白色的。给定数组中的 N 对(I，j)，对于每对，用黑色绘制单元格(I，j)。任务是在绘制 N 个单元格后，确定网格中有多少大小为 p×p 的正方形恰好包含 K 个黑色单元格。

**示例:**

```
Input: H = 4, W = 5,
      N = 8, K = 4, p = 3 
      arr=[ (3, 1), (3, 2), (3, 4), (4, 4), 
            (1, 5), (2, 3), (1, 1), (1, 4) ]
Output: 4
Cells the are being painted are shown in the figure below:
Here p = 3\. 
There are six subrectangles of size 3*3\. 
Two of them contain three black cells each, 
and the remaining four contain four black cells each.
```

![](img/3893ac0cf4d96b251e0d7b9cf54f13d4.png)

```
Input: H = 1, W = 1, 
       N = 1, K = 1, p = 1
       arr=[ (1, 1) ]
Output: 1
```

**进场:**

*   首先要观察的是，如果一个 p*p 子网格的起点不同，那么另一个也会不同。
*   第二件事是，如果单元格被涂成黑色，它将贡献给 p^2 不同的 p*p 子网格。
*   例如，假设单元格[i，j]被涂成黑色。那么它将对具有起始点
    【I-p+1】【j-p+1】到【I，j】的所有子网格贡献额外的+1。
*   由于最多可以有 N 个黑色，因此对每个黑色单元进行 p*p 次迭代，并更新其对每个 p*p 个子网格的贡献。
*   保留一张地图来记录网格中每个单元的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a cell is safe or not
bool isSafe(int x, int y, int h, int w, int p)
{
    if (x >= 1 and x <= h) {
        if (y >= 1 and y <= w) {
            if (x + p - 1 <= h) {
                if (y + p - 1 <= w) {
                    return true;
                }
            }
        }
    }
    return false;
}

// Function to print the number of p-sided squares
// having k blacks
void CountSquares(int h, int w, int n, int k,
        int p, vector<pair<int, int> > painted)
{
    // Map to keep track for each cell that is
    // being affected by other blacks
    map<pair<int, int>, int> mp;
    for (int i = 0; i < painted.size(); ++i) {
        int x = painted[i].first;
        int y = painted[i].second;

        // For a particular row x and column y,
        // it will affect all the cells starting
        // from row = x-p+1 and column = y-p+1
        // and ending at x, y
        // hence there will be total
        // of p^2 different cells
        for (int j = x - p + 1; j <= x; ++j) {
            for (int k = y - p + 1; k <= y; ++k) {

                // If the cell is safe
                if (isSafe(j, k, h, w, p)) {
                    pair<int, int> temp = { j, k };

                    // No need to increase the value
                    // as there is no sense of paint
                    // 2 blacks in one cell
                    if (mp[temp] >= p * p)
                        continue;
                    else
                        mp[temp]++;
                }
            }
        }
    }

    // Answer array to store the answer.
    int ans[p * p + 1];
    memset(ans, 0, sizeof ans);
    for (auto& x : mp) {
        int cnt = x.second;
        ans[cnt]++;
    }

    // sum variable to store sum for all the p*p sub
    // grids painted with 1 black, 2 black,
    // 3 black, ..., p^2 blacks,
    // Since there is no meaning in painting p*p sub
    // grid with p^2+1 or more blacks
    int sum = 0;
    for (int i = 1; i <= p * p; ++i)
        sum = sum + ans[i];

    // There will be total of
    // (h-p+1) * (w-p+1), p*p sub grids
    int total = (h - p + 1) * (w - p + 1);
    ans[0] = total - sum;
    cout << ans[k] << endl;
    return;
}

// Driver code
int main()
{
    int H = 4, W = 5, N = 8, K = 4, P = 3;
    vector<pair<int, int> > painted;

    // Initializing matrix
    painted.push_back({ 3, 1 });
    painted.push_back({ 3, 2 });
    painted.push_back({ 3, 4 });
    painted.push_back({ 4, 4 });
    painted.push_back({ 1, 5 });
    painted.push_back({ 2, 3 });
    painted.push_back({ 1, 1 });
    painted.push_back({ 1, 4 });

    CountSquares(H, W, N, K, P, painted);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
import java.awt.Point;
class GFG
{
  // Function to check if a cell is safe or not
  static boolean isSafe(int x, int y, int h,
                        int w, int p)
  {
    if (x >= 1 && x <= h)
    {
      if (y >= 1 && y <= w)
      {
        if (x + p - 1 <= h)
        {
          if (y + p - 1 <= w)
          {
            return true;
          }
        }
      }
    }
    return false;
  }

  // Function to print the number of p-sided squares 
  // having k blacks
  static void CountSquares(int h, int w, int n, int K,
                           int p, List<Point> painted)
  {

    // Map to keep track for each cell that is
    // being affected by other blacks
    HashMap<Point, Integer> mp = new HashMap<>();

    for(int i = 0; i < painted.size(); ++i)
    {
      int x = painted.get(i).x;
      int y = painted.get(i).y;

      // For a particular row x and column y, 
      // it will affect all the cells starting
      // from row = x-p+1 and column = y-p+1 
      // and ending at x, y
      // hence there will be total 
      // of p^2 different cells
      for(int j = x - p + 1; j <= x; ++j)
      {
        for(int k = y - p + 1; k <= y; ++k)
        {

          // If the cell is safe
          if (isSafe(j, k, h, w, p))
          {

            Point temp = new Point(j, k);

            // No need to increase the value
            // as there is no sense of paint 
            // 2 blacks in one cell
            if (mp.containsKey(temp))
            {
              if (mp.get(temp) >= p * p)
                continue; 
              else
                mp.put(temp, mp.get(temp) + 1);
            }
            else
            {
              mp.put(temp, 1);
            }
          }
        }
      }
    }

    // Answer array to store the answer.
    int[] ans = new int[p * p + 1]; 
    for (Map.Entry<Point, Integer> x : mp.entrySet())
    {
      int cnt = x.getValue();
      ans[cnt]++;
    }

    // sum variable to store sum for all the p*p sub
    // grids painted with 1 black, 2 black, 
    // 3 black, ..., p^2 blacks,
    // Since there is no meaning in painting p*p sub
    // grid with p^2+1 or more blacks
    int sum = 0; 
    for(int i = 1; i <= p * p; ++i)
      sum = sum + ans[i];

    // There will be total of 
    // (h-p+1) * (w-p+1), p*p sub grids
    int total = (h - p + 1) * (w - p + 1); 
    ans[0] = total - sum;
    System.out.println(ans[K]);
    return;
  }  

  // Driver code
  public static void main(String[] args)
  {
    int H = 4, W = 5, N = 8, K = 4, P = 3;
    List<Point> painted = new ArrayList<Point>();

    // Initializing matrix
    painted.add(new Point(3, 1));
    painted.add(new Point(3, 2));
    painted.add(new Point(3, 4));
    painted.add(new Point(4, 4));
    painted.add(new Point(1, 5));
    painted.add(new Point(2, 3));
    painted.add(new Point(1, 1));
    painted.add(new Point(1, 4));

    CountSquares(H, W, N, K, P, painted);
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to check if a cell is safe or not
def isSafe(x, y, h, w, p):
    if (x >= 1 and x <= h):
        if (y >= 1 and y <= w):
            if (x + p - 1 <= h):
                if (y + p - 1 <= w):
                    return True
    return False

# Function to print the number of p-sided squares
# having k blacks
def CountSquares(h, w, n, k, p, painted):

    # Map to keep track for each cell that is
    # being affected by other blacks
    mp = dict()
    for i in range(len(painted)):
        x = painted[i][0]
        y = painted[i][1]

        # For a particular row x and column y,
        # it will affect all the cells starting
        # from row = x-p+1 and column = y-p+1
        # and ending at x, y
        # hence there will be total
        # of p^2 different cells
        for j in range(x - p + 1, x + 1):
            for k in range(y - p + 1, y + 1):

                # If the cell is safe
                if (isSafe(j, k, h, w, p)):
                    temp = (j, k)

                    # No need to increase the value
                    # as there is no sense of pa
                    # 2 blacks in one cell
                    if (temp in mp.keys() and mp[temp] >= p * p):
                        continue
                    else:
                        mp[temp] = mp.get(temp, 0) + 1

    # Answer array to store the answer.
    ans = [0 for i in range(p * p + 1)]

    # memset(ans, 0, sizeof ans)
    for x in mp:
        cnt = mp[x]
        ans[cnt] += 1

    # Sum variable to store Sum for all the p*p sub
    # grids painted with 1 black, 2 black,
    # 3 black, ..., p^2 blacks,
    # Since there is no meaning in painting p*p sub
    # grid with p^2+1 or more blacks
    Sum = 0
    for i in range(1, p * p + 1):
        Sum = Sum + ans[i]

    # There will be total of
    # (h-p+1) * (w-p+1), p*p sub grids
    total = (h - p + 1) * (w - p + 1)
    ans[0] = total - Sum
    print(ans[k])
    return

# Driver code
H = 4
W = 5
N = 8
K = 4
P = 3
painted = []

# Initializing matrix
painted.append([ 3, 1 ])
painted.append([ 3, 2 ])
painted.append([ 3, 4 ])
painted.append([ 4, 4 ])
painted.append([ 1, 5 ])
painted.append([ 2, 3 ])
painted.append([ 1, 1 ])
painted.append([ 1, 4 ])

CountSquares(H, W, N, K, P, painted)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if a cell is safe or not
static bool isSafe(int x, int y, int h,
                   int w, int p)
{
    if (x >= 1 && x <= h)
    {
        if (y >= 1 && y <= w)
        {
            if (x + p - 1 <= h)
            {
                if (y + p - 1 <= w)
                {
                    return true;
                }
            }
        }
    }
    return false;
}

// Function to print the number of p-sided squares 
// having k blacks
static void CountSquares(int h, int w, int n, int K,
                         int p, List<Tuple<int, int>> painted)
{

    // Map to keep track for each cell that is
    // being affected by other blacks
    Dictionary<Tuple<int,
                     int>, int> mp = new Dictionary<Tuple<int,
                                                          int>, int>(); 

    for(int i = 0; i < painted.Count; ++i)
    {
        int x = painted[i].Item1;
        int y = painted[i].Item2;

        // For a particular row x and column y, 
        // it will affect all the cells starting
        // from row = x-p+1 and column = y-p+1 
        // and ending at x, y
        // hence there will be total 
        // of p^2 different cells
        for(int j = x - p + 1; j <= x; ++j)
        {
            for(int k = y - p + 1; k <= y; ++k)
            {

                // If the cell is safe
                if (isSafe(j, k, h, w, p))
                {

                    Tuple<int,
                          int> temp = new Tuple<int,
                                                int>(j, k);

                    // No need to increase the value
                    // as there is no sense of paint 
                    // 2 blacks in one cell
                    if (mp.ContainsKey(temp))
                    {
                        if (mp[temp] >= p * p)
                            continue; 
                        else
                            mp[temp]++;
                    }
                    else
                    {
                        mp[temp] = 1;
                    }
                }
            }
        }
    }

    // Answer array to store the answer.
    int[] ans = new int[p * p + 1]; 
    foreach(KeyValuePair<Tuple<int, int>, int> x in mp)
    {
        int cnt = x.Value;
        ans[cnt]++;
    }

    // sum variable to store sum for all the p*p sub
    // grids painted with 1 black, 2 black, 
    // 3 black, ..., p^2 blacks,
    // Since there is no meaning in painting p*p sub
    // grid with p^2+1 or more blacks
    int sum = 0; 
    for(int i = 1; i <= p * p; ++i)
        sum = sum + ans[i];

    // There will be total of 
    // (h-p+1) * (w-p+1), p*p sub grids
    int total = (h - p + 1) * (w - p + 1); 
    ans[0] = total - sum;
    Console.WriteLine(ans[K]);
    return;
} 

// Driver Code
static void Main()
{
    int H = 4, W = 5, N = 8, K = 4, P = 3;
    List<Tuple<int,
               int>> painted = new List<Tuple<int,
                                              int>>();

    // Initializing matrix
    painted.Add(new Tuple<int, int>(3, 1));
    painted.Add(new Tuple<int, int>(3, 2));
    painted.Add(new Tuple<int, int>(3, 4));
    painted.Add(new Tuple<int, int>(4, 4));
    painted.Add(new Tuple<int, int>(1, 5));
    painted.Add(new Tuple<int, int>(2, 3));
    painted.Add(new Tuple<int, int>(1, 1));
    painted.Add(new Tuple<int, int>(1, 4));

    CountSquares(H, W, N, K, P, painted);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to check if a cell is safe or not
function isSafe(x,y,h,w,p)
{
    if (x >= 1 && x <= h)
    {
      if (y >= 1 && y <= w)
      {
        if (x + p - 1 <= h)
        {
          if (y + p - 1 <= w)
          {
            return true;
          }
        }
      }
    }
    return false;
}

// Function to print the number of p-sided squares
  // having k blacks
function CountSquares(h,w,n,K,p,painted)
{
    // Map to keep track for each cell that is
    // being affected by other blacks
    let mp = new Map();

    for(let i = 0; i < painted.length; ++i)
    {
      let x = painted[i][0];
      let y = painted[i][1];

      // For a particular row x and column y,
      // it will affect all the cells starting
      // from row = x-p+1 and column = y-p+1
      // and ending at x, y
      // hence there will be total
      // of p^2 different cells
      for(let j = x - p + 1; j <= x; ++j)
      {
        for(let k = y - p + 1; k <= y; ++k)
        {

          // If the cell is safe
          if (isSafe(j, k, h, w, p))
          {

            let temp = [j, k].toString();

            // No need to increase the value
            // as there is no sense of paint
            // 2 blacks in one cell
            if (mp.has(temp))
            {
              if (mp.get(temp) >= p * p)
                continue;
              else
                mp.set(temp, mp.get(temp) + 1);
            }
            else
            {
              mp.set(temp, 1);
            }
          }
        }
      }
    }

    // Answer array to store the answer.
    let ans = new Array(p * p + 1);
    for(let i=0;i<ans.length;i++)
    {
        ans[i]=0;
    }
    for (let [key, value] of mp.entries())
    {
      let cnt = value;
      ans[cnt]++;
    }

    // sum variable to store sum for all the p*p sub
    // grids painted with 1 black, 2 black,
    // 3 black, ..., p^2 blacks,
    // Since there is no meaning in painting p*p sub
    // grid with p^2+1 or more blacks
    let sum = 0;
    for(let i = 1; i <= p * p; ++i)
      sum = sum + ans[i];

    // There will be total of
    // (h-p+1) * (w-p+1), p*p sub grids
    let total = (h - p + 1) * (w - p + 1);
    ans[0] = total - sum;
    document.write(ans[K]+"<br>");
    return;
}

 // Driver code
let H = 4, W = 5, N = 8, K = 4, P = 3;

let painted = []

// Initializing matrix
painted.push([ 3, 1 ])
painted.push([ 3, 2 ])
painted.push([ 3, 4 ])
painted.push([ 4, 4 ])
painted.push([ 1, 5 ])
painted.push([ 2, 3 ])
painted.push([ 1, 1 ])
painted.push([ 1, 4 ])

CountSquares(H, W, N, K, P, painted)

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N*p*p)
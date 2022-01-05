# 检查从原点

是否可以到达给定圆圆周上的任意点

> 原文:[https://www . geeksforgeeks . org/check-如果有可能从原点到达给定圆圆周上的任何点/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-any-point-on-the-circumference-of-a-given-circle-from-origin/)

给定一个代表一系列动作的[弦](https://www.geeksforgeeks.org/string-data-structure/)**S**(**L**、 **R** 、 **U** 和 **D** )和一个代表圆心为原点 **(0，0)** 的圆的[半径的整数 **R** ，任务是检查是否有可能到达给定的](https://www.geeksforgeeks.org/radius-of-the-circle-when-the-width-and-height-of-an-arc-is-given/)[圆周上的任何一点如果有可能到达圆周上的一个点，则打印**“是”**。否则，打印**“否”**。
每个方向需要执行的操作如下:](https://www.geeksforgeeks.org/program-find-circumference-circle/)

*   如果当前字符为 **L** ，则减量**x**-按 **1** 坐标。
*   如果当前字符为 **R** ，则按 **1** 增加**x**-坐标。
*   如果当前字符为 **U** ，则按 **1** 增加**y**-坐标。
*   如果当前字符为 **D** ，则递减**y**-按 **1** 坐标。

**示例:**

> **输入:**S =“LLRULD”，R = 3
> **输出:**是
> **解释:**
> 选择子序列“LLL”，通过执行移动序列的坐标变化为:
> (0，0) → ( -1，0) → (-2，0) → (-3，0)
> 由于(-3，0)位于给定圆的圆周上，因此有可能到达
> 
> **输入:** S = "ULRDLD "，R = 6
> T3】输出:否

**简单方法:**最简单的方法是[生成给定字符串](https://www.geeksforgeeks.org/print-subsequences-string/) **S** 的所有可能的子序列，如果存在任何导致从原点 **(0，0)** 到达圆的圆周的子序列，则打印**“是”**。否则，打印**“否”**。

***时间复杂度:**O(2<sup>N</sup>)* *****辅助空间:** O(1)***

****高效方法:**上述方法可以基于以下观察进行优化:**

*   **由于需要考虑的路径是从原点 **(0，0)** 开始的，如果字符串中每个字符 **L** 、 **R** 、 **U** 和 **D** 中的最大计数超过了 **R** ，那么从原点到圆周的路径是存在的。**
*   **如果存在任意两个值 **X** 和 **Y** 使得[的 **X** 和 **Y** 的平方和为 **R <sup>2</sup>** ，则从原点到圆的圆周存在三角形路径。](https://www.geeksforgeeks.org/python-program-for-sum-of-squares-of-first-n-natural-numbers/)**

**按照以下步骤解决给定的问题:**

*   **将给定字符串 **S** 中的[字符数](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)**L****R****U**和 **D** 存储在一个变量中，分别表示 **cntL** 、 **cntR** 、 **cntU** 和 **cntD** 。**
*   **如果 **cntL** 、 **cntR** 、 **cntU** 、 **cntD** 的最大值至少为 **R** ，则存在从原点到圆周的直线路径。因此，打印**“是”**。**
*   **如果 **cntL** 和 **cntR** 的最大值与 **cntU** 和 **cntD** 的最大值的平方至少为 **R <sup>2</sup>** ，则打印**“是”、**，因为从原点到圆周存在三角形路径。**
*   **如果没有出现上述情况，则打印**“否”**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to reach any point on circumference
// of the given circle from (0,0)
string isPossible(string S, int R, int N)
{
    // Stores the count of 'L', 'R'
    int cntl = 0, cntr = 0;

    // Stores the count of 'U', 'D'
    int cntu = 0, cntd = 0;

    // Traverse the string S
    for (int i = 0; i < N; i++) {
        // Update the count of L
        if (S[i] == 'L')
            cntl++;

        // Update the count of R
        else if (S[i] == 'R')
            cntr++;

        // Update the count of U
        else if (S[i] == 'U')
            cntu++;

        // Update the count of D
        else
            cntd++;
    }

    // Condition 1 for reaching
    // the circumference
    if (max(max(cntl, cntr), max(cntu, cntd)) >= R)
        return "Yes";

    unordered_map<int, int> mp;

    int r_square = R * R;

    for (int i = 1; i * i <= r_square; i++) {

        // Store the the value
        // of (i * i) in the Map
        mp[i * i] = i;

        // Check if (r_square - i*i)
        // already present in HashMap
        if (mp.find(r_square - i * i) != mp.end()) {

            // If it is possible to reach the
            // point (± mp[r_square - i*i], ± i)
            if (max(cntl, cntr)
                >= mp[r_square - i * i]
                && max(cntu, cntd) >= i)

                return "Yes";

            // If it is possible to reach the
            // point (±i, ±mp[r_square-i*i])
            if (max(cntl, cntr) >= i
                && max(cntu, cntd)
                >= mp[r_square - i * i])

                return "Yes";
        }
    }

    // If it is impossible to reach
    return "No";
}

// Driver Code
int main()
{
    string S = "RDLLDDLDU";
    int R = 5;
    int N = S.length();

    cout << isPossible(S, R, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if it is possible
// to reach any point on circumference
// of the given circle from (0,0)
static String isPossible(String S, int R, int N)
{

    // Stores the count of 'L', 'R'
    int cntl = 0, cntr = 0;

    // Stores the count of 'U', 'D'
    int cntu = 0, cntd = 0;

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

        // Update the count of L
        if (S.charAt(i) == 'L')
            cntl++;

        // Update the count of R
        else if (S.charAt(i) == 'R')
            cntr++;

        // Update the count of U
        else if (S.charAt(i) == 'U')
            cntu++;

        // Update the count of D
        else
            cntd++;
    }

    // Condition 1 for reaching
    // the circumference
    if (Math.max(Math.max(cntl, cntr),
                 Math.max(cntu, cntd)) >= R)
        return "Yes";

    HashMap<Integer, Integer> mp = new HashMap<>();

    int r_square = R * R;

    for(int i = 1; i * i <= r_square; i++)
    {

        // Store the the value
        // of (i * i) in the Map
        mp.put(i * i, i);

        // Check if (r_square - i*i)
        // already present in HashMap
        if (mp.containsKey(r_square - i * i))
        {

            // If it is possible to reach the
            // point (± mp[r_square - i*i], ± i)
            if (Math.max(cntl, cntr) >=
                mp.get(r_square - i * i) &&
                Math.max(cntu, cntd) >= i)
                return "Yes";

            // If it is possible to reach the
            // point (±i, ±mp[r_square-i*i])
            if (Math.max(cntl, cntr) >= i &&
                Math.max(cntu, cntd) >=
                mp.get(r_square - i * i))
                return "Yes";
        }
    }

    // If it is impossible to reach
    return "No";
}

// Driver Code
public static void main(String[] args)
{
    String S = "RDLLDDLDU";
    int R = 5;
    int N = S.length();

    System.out.println(isPossible(S, R, N));
}
}

// This code is contributed by Kingash
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to check if it is possible
# to reach any point on circumference
# of the given circle from (0,0)
def isPossible(S, R, N):

    # Stores the count of 'L', 'R'
    cntl = 0
    cntr = 0

    # Stores the count of 'U', 'D'
    cntu = 0
    cntd = 0

    # Traverse the string S
    for i in range(N):

        # Update the count of L
        if (S[i] == 'L'):
            cntl += 1

        # Update the count of R
        elif (S[i] == 'R'):
            cntr += 1

        # Update the count of U
        elif (S[i] == 'U'):
            cntu += 1

        # Update the count of D
        else:
            cntd += 1

    # Condition 1 for reaching
    # the circumference
    if (max(max(cntl, cntr), max(cntu, cntd)) >= R):
        return "Yes"

    mp = {}

    r_square = R * R

    i = 1
    while i * i <= r_square:

        # Store the the value
        # of (i * i) in the Map
        mp[i * i] = i

        # Check if (r_square - i*i)
        # already present in HashMap
        if ((r_square - i * i) in mp):

            # If it is possible to reach the
            # point (± mp[r_square - i*i], ± i)
            if (max(cntl, cntr) >= mp[r_square - i * i] and
               max(cntu, cntd) >= i):

                return "Yes"

            # If it is possible to reach the
            # point (±i, ±mp[r_square-i*i])
            if (max(cntl, cntr) >= i and
               max(cntu, cntd) >= mp[r_square - i * i]):

                return "Yes"

        i += 1

    # If it is impossible to reach
    return "No"

# Driver Code
if __name__ == "__main__":

    S = "RDLLDDLDU"
    R = 5
    N = len(S)

    print(isPossible(S, R, N))

# This code is contributed by ukasp
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

  // Function to check if it is possible
  // to reach any point on circumference
  // of the given circle from (0,0)
  static string isPossible(string S, int R, int N)
  {

    // Stores the count of 'L', 'R'
    int cntl = 0, cntr = 0;

    // Stores the count of 'U', 'D'
    int cntu = 0, cntd = 0;

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

      // Update the count of L
      if (S[i] == 'L')
        cntl++;

      // Update the count of R
      else if (S[i] == 'R')
        cntr++;

      // Update the count of U
      else if (S[i] == 'U')
        cntu++;

      // Update the count of D
      else
        cntd++;
    }

    // Condition 1 for reaching
    // the circumference
    if (Math.Max(Math.Max(cntl, cntr),
                 Math.Max(cntu, cntd)) >= R)
      return "Yes";

    Dictionary<int, int> mp = new Dictionary<int, int>();

    int r_square = R * R;

    for(int i = 1; i * i <= r_square; i++)
    {

      // Store the the value
      // of (i * i) in the Map
      mp.Add(i * i, i);

      // Check if (r_square - i*i)
      // already present in HashMap
      if (mp.ContainsKey(r_square - i * i))
      {

        // If it is possible to reach the
        // point (± mp[r_square - i*i], ± i)
        if (Math.Max(cntl, cntr) >=
            mp[r_square - i * i] &&
            Math.Max(cntu, cntd) >= i)
          return "Yes";

        // If it is possible to reach the
        // point (±i, ±mp[r_square-i*i])
        if (Math.Max(cntl, cntr) >= i &&
            Math.Max(cntu, cntd) >=
            mp[r_square - i * i])
          return "Yes";
      }
    }

    // If it is impossible to reach
    return "No";
  }
  static public void Main ()
  {
    string S = "RDLLDDLDU";
    int R = 5;
    int N = S.Length;

    Console.WriteLine(isPossible(S, R, N));
  }
}

// This code is contributed by offbeat
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to check if it is possible
// to reach any point on circumference
// of the given circle from (0,0)
function isPossible(S, R, N)
{
    // Stores the count of 'L', 'R'
    var cntl = 0, cntr = 0;

    // Stores the count of 'U', 'D'
    var cntu = 0, cntd = 0;

    // Traverse the string S
    for (var i = 0; i < N; i++) {
        // Update the count of L
        if (S[i] == 'L')
            cntl++;

        // Update the count of R
        else if (S[i] == 'R')
            cntr++;

        // Update the count of U
        else if (S[i] == 'U')
            cntu++;

        // Update the count of D
        else
            cntd++;
    }

    // Condition 1 for reaching
    // the circumference
    if (Math.max(Math.max(cntl, cntr), Math.max(cntu, cntd)) >= R)
        return "Yes";

    var mp = new Map();

    var r_square = R * R;

    for (var i = 1; i * i <= r_square; i++) {

        // Store the the value
        // of (i * i) in the Map
        mp.set(i * i, i);

        // Check if (r_square - i*i)
        // already present in HashMap
        if (mp.has(r_square - i * i)) {

            // If it is possible to reach the
            // point (± mp[r_square - i*i], ± i)
            if (Math.max(cntl, cntr)
                >= mp.get(r_square - i * i)
                && Math.max(cntu, cntd) >= i)

                return "Yes";

            // If it is possible to reach the
            // point (±i, ±mp[r_square-i*i])
            if (Math.max(cntl, cntr) >= i
                && Math.max(cntu, cntd)
                >= mp.get(r_square - i * i))

                return "Yes";
        }
    }

    // If it is impossible to reach
    return "No";
}

// Driver Code
var S = "RDLLDDLDU";
var R = 5;
var N = S.length;

document.write( isPossible(S, R, N));

</script>
```

****Output:** 

```
Yes
```** 

*****时间复杂度:** O(N + R)*
***辅助空间:** O(R <sup>2</sup> )***
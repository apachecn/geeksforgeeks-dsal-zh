# 找出曼哈顿距离至少为 N 的整数点(x，y)

> 原文:[https://www . geesforgeks . org/find-the-integer-points-x-y-with-Manhattan-distance-至少-n/](https://www.geeksforgeeks.org/find-the-integer-points-x-y-with-manhattan-distance-atleast-n/)

给定一个数字 N，任务是找到整数点(x，y)，使得任意两点之间的 0 <= x, y <= N and [曼哈顿距离](https://www.geeksforgeeks.org/sum-manhattan-distances-pairs-points/)至少为 N.
**示例:**

```
Input: N = 3
Output: (0, 0) (0, 3) (3, 0) (3, 3)

Input: N = 4
Output: (0, 0) (0, 4) (4, 0) (4, 4) (2, 2)
```

**进场:**

*   两点之间的曼哈顿距离(x <sub>1</sub> ，y <sub>1</sub> )和(x <sub>2</sub> ，y <sub>2</sub> 为:
    T9】| x<sub>1</sub>–x<sub>2</sub>|+| y<sub>1</sub>–y<sub>2</sub>|
*   这里，对于所有点对，该距离至少为 n
*   如**0<= x<= N****0<= y<= N**那么我们可以想象一个边长为 N 的正方形，其左下角为(0，0)，右上角为(N，N)。
*   所以如果我们在这个角落放 4 个点，那么曼哈顿的距离至少是 n
*   现在，由于我们必须最大化点的数量，我们必须检查正方形内是否有可用的点。
*   如果 N 为偶数，则(N/2，N/2)的平方的中点为整数点，否则，当 N 为奇数时，由于 N/2 不是整数，所以为浮点值。
*   所以唯一可用的位置是中间点，只有当 N 是偶数时，我们才能在那里放一个点。
*   所以如果 N 是奇数，点数是 4，如果 N 是偶数，点数是 5。

以下是上述方法的实现:

## C++

```
// C++ code to Find the integer points (x, y)
// with Manhattan distance atleast N

#include <bits/stdc++.h>
using namespace std;

// C++ function to find all possible point
vector<pair<int, int> > FindPoints(int n)
{

    vector<pair<int, int> > v;

    // Find all 4 corners of the square
    // whose side length is n
    v.push_back({ 0, 0 });
    v.push_back({ 0, n });
    v.push_back({ n, 0 });
    v.push_back({ n, n });

    // If n is even then the middle point
    // of the square will be an integer,
    // so we will take that point
    if (n % 2 == 0)
        v.push_back({ n / 2, n / 2 });

    return v;
}

// Driver Code
int main()
{

    int N = 8;

    vector<pair<int, int> > v
        = FindPoints(N);

    // Printing all possible points
    for (auto i : v) {
        cout << "(" << i.first << ", "
             << i.second << ") ";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to Find the integer points (x, y)
// with Manhattan distance atleast N
import java.util.*;

class GFG
{

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Java function to find all possible point
static Vector<pair> FindPoints(int n)
{
    Vector<pair> v = new Vector<pair>();

    // Find all 4 corners of the square
    // whose side length is n
    v.add(new pair( 0, 0 ));
    v.add(new pair( 0, n ));
    v.add(new pair( n, 0 ));
    v.add(new pair( n, n ));

    // If n is even then the middle point
    // of the square will be an integer,
    // so we will take that point
    if (n % 2 == 0)
        v.add(new pair( n / 2, n / 2 ));

    return v;
}

// Driver Code
public static void main(String[] args)
{
    int N = 8;

    Vector<pair > v = FindPoints(N);

    // Printing all possible points
    for (pair i : v)
    {
        System.out.print("(" + i.first + ", " +
                               i.second + ") ");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 code to Find the integer points (x, y)
# with Manhattan distance atleast N

# function to find all possible point
def FindPoints(n) :

    v = [];

    # Find all 4 corners of the square
    # whose side length is n
    v.append([ 0, 0 ]);
    v.append([ 0, n ]);
    v.append([ n, 0 ]);
    v.append([ n, n ]);

    # If n is even then the middle point
    # of the square will be an integer,
    # so we will take that point
    if (n % 2 == 0) :
        v.append([ n // 2, n // 2 ]);

    return v;

# Driver Code
if __name__ == "__main__" :

    N = 8;

    v = FindPoints(N);

    # Printing all possible points
    for element in v :
        print("(", element[0],
              ",", element[1], ")", end = " ");

# This code is contributed by AnkitRai01
```

## C#

```
// C# code to Find the integer points (x, y)
// with Manhattan distance atleast N
using System;
using System.Collections.Generic;

class GFG
{

class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find all possible point
static List<pair> FindPoints(int n)
{
    List<pair> v = new List<pair>();

    // Find all 4 corners of the square
    // whose side length is n
    v.Add(new pair( 0, 0 ));
    v.Add(new pair( 0, n ));
    v.Add(new pair( n, 0 ));
    v.Add(new pair( n, n ));

    // If n is even then the middle point
    // of the square will be an integer,
    // so we will take that point
    if (n % 2 == 0)
        v.Add(new pair( n / 2, n / 2 ));

    return v;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 8;

    List<pair > v = FindPoints(N);

    // Printing all possible points
    foreach (pair i in v)
    {
        Console.Write("(" + i.first + ", " +
                            i.second + ") ");
    }
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript code to Find the integer points (x, y)
// with Manhattan distance atleast N

// C++ function to find all possible point
function FindPoints(n)
{

    var v = [];

    // Find all 4 corners of the square
    // whose side length is n
    v.push([ 0, 0 ]);
    v.push([ 0, n ]);
    v.push([ n, 0 ]);
    v.push([ n, n ]);

    // If n is even then the middle point
    // of the square will be an integer,
    // so we will take that point
    if (n % 2 == 0)
        v.push([ n / 2, n / 2 ]);

    return v;
}

// Driver Code
var N = 8;
var v = FindPoints(N);
// Printing all possible points
v.forEach(i => {
    document.write( "(" + i[0] + ", "
         + i[1] + ") ");
});

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
(0, 0) (0, 8) (8, 0) (8, 8) (4, 4)
```
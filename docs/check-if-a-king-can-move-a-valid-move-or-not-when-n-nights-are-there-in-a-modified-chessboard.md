# 在修改后的棋盘

中有 N 个夜晚时，检查一个国王是否可以移动一个有效的移动

> 原文:[https://www . geesforgeks . org/check-if-a-king-move-a-valid-move-or-not-当-n-nights-in-a-modified-bodget/](https://www.geeksforgeeks.org/check-if-a-king-can-move-a-valid-move-or-not-when-n-nights-are-there-in-a-modified-chessboard/)

给定一个与国际象棋规则相同的无限棋盘。还给出了无限 chessboard(-10^ <sup>9</sup> < = x，y < = 10^ <sup>9</sup> 上的 n 个骑士坐标和国王的坐标，任务是检查国王是否将死。
**例:**

```
Input: a[] = { {1, 0}, {0, 2}, {2, 5}, {4, 4}, {5, 0}, {6, 2} } king -> {3, 2} 
Output: Yes
The king cannot make any move as it has been check mate. 

Input: a[] = { {1, 1} } king -> {3, 4} 
Output: No
The king can make valid moves. 
```

**进场:**骑士的招式在棋子中不常见。它移动到一个正方形，水平方向两个正方形，垂直方向一个正方形，或者垂直方向两个正方形，水平方向一个正方形。因此，在所有可能的形状中，完整的移动看起来像字母“L”(8 个可能的移动)。因此，使用配对的散列图来标记骑士可以移动的所有可能的坐标。如果国王不能移动到它附近的 8 个坐标中的任何一个，也就是说，如果坐标被骑士的移动散列，那么它就是一个“将死”。
以下是上述办法的实施情况。

## C++

```
// C++ program for checking if a king
// can move a valid move or not when
// N nights are there in a modified chessboard
#include <bits/stdc++.h>
using namespace std;
bool checkCheckMate(pair<int, int> a[], int n, int kx, int ky)
{

    // Pair of hash to mark the coordinates
    map<pair<int, int>, int> mpp;

    // iterate for Given N knights
    for (int i = 0; i < n; i++) {
        int x = a[i].first;
        int y = a[i].second;

        // mark all the "L" shaped coordinates
        // that can be reached by a Knight

        // initial position
        mpp[{ x, y }] = 1;

        // 1-st move
        mpp[{ x - 2, y + 1 }] = 1;

        // 2-nd move
        mpp[{ x - 2, y - 1 }] = 1;

        // 3-rd move
        mpp[{ x + 1, y + 2 }] = 1;

        // 4-th move
        mpp[{ x + 1, y - 2 }] = 1;

        // 5-th move
        mpp[{ x - 1, y + 2 }] = 1;

        // 6-th move
        mpp[{ x + 2, y + 1 }] = 1;

        // 7-th move
        mpp[{ x + 2, y - 1 }] = 1;

        // 8-th move
        mpp[{ x - 1, y - 2 }] = 1;
    }

    // iterate for all possible 8 coordinates
    for (int i = -1; i < 2; i++) {
        for (int j = -1; j < 2; j++) {
            int nx = kx + i;
            int ny = ky + j;
            if (i != 0 && j != 0) {

                // check a move can be made or not
                if (!mpp[{ nx, ny }]) {
                    return true;
                }
            }
        }
    }

    // any moves
    return false;
}

// Driver Code
int main()
{
    pair<int, int> a[] = { { 1, 0 }, { 0, 2 }, { 2, 5 },
                           { 4, 4 }, { 5, 0 }, { 6, 2 }};

    int n = sizeof(a) / sizeof(a[0]);

    int x = 3, y = 2;
    if (checkCheckMate(a, n, x, y))
        cout << "Not Checkmate!";
    else
        cout << "Yes its checkmate!";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for checking if a king
// can move a valid move or not when
// N nights are there in a modified chessboard
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

static boolean checkCheckMate(pair a[], int n,
                              int kx, int ky)
{

    // Pair of hash to mark the coordinates
    HashMap<pair,
            Integer> mpp = new HashMap<pair,
                                       Integer>();

    // iterate for Given N knights
    for (int i = 0; i < n; i++)
    {
        int x = a[i].first;
        int y = a[i].second;

        // mark all the "L" shaped coordinates
        // that can be reached by a Knight

        // initial position
        mpp.put(new pair( x, y ), 1);

        // 1-st move
        mpp.put(new pair( x - 2, y + 1 ), 1);

        // 2-nd move
        mpp.put(new pair( x - 2, y - 1 ), 1);

        // 3-rd move
        mpp.put(new pair( x + 1, y + 2 ), 1);

        // 4-th move
        mpp.put(new pair( x + 1, y - 2 ), 1);

        // 5-th move
        mpp.put(new pair( x - 1, y + 2 ), 1);

        // 6-th move
        mpp.put(new pair( x + 2, y + 1 ), 1);

        // 7-th move
        mpp.put(new pair( x + 2, y - 1 ), 1);

        // 8-th move
        mpp.put(new pair( x - 1, y - 2 ), 1);
    }

    // iterate for all possible 8 coordinates
    for (int i = -1; i < 2; i++)
    {
        for (int j = -1; j < 2; j++)
        {
            int nx = kx + i;
            int ny = ky + j;
            if (i != 0 && j != 0)
            {

                // check a move can be made or not
                pair p =new pair(nx, ny );
                if (mpp.get(p) != null)
                {
                    return true;
                }
            }
        }
    }

    // any moves
    return false;
}

// Driver Code
public static void main(String[] args)
{
    pair a[] = {new pair( 1, 0 ), new pair( 0, 2 ),
                new pair( 2, 5 ), new pair( 4, 4 ),
                new pair( 5, 0 ), new pair( 6, 2 )};

    int n = a.length;

    int x = 3, y = 2;
    if (checkCheckMate(a, n, x, y))
        System.out.println("Not Checkmate!");
    else
        System.out.println("Yes its checkmate!");
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for checking if a king
# can move a valid move or not when
# N nights are there in a modified chessboard

def checkCheckMate(a, n, kx, ky):

    # Pair of hash to mark the coordinates
    mpp = {}

    # iterate for Given N knights
    for i in range(0, n):
        x = a[i][0]
        y = a[i][1]

        # mark all the "L" shaped coordinates
        # that can be reached by a Knight

        # initial position
        mpp[(x, y)] = 1

        # 1-st move
        mpp[(x - 2, y + 1)] = 1

        # 2-nd move
        mpp[(x - 2, y - 1)] = 1

        # 3-rd move
        mpp[(x + 1, y + 2)] = 1

        # 4-th move
        mpp[(x + 1, y - 2)] = 1

        # 5-th move
        mpp[(x - 1, y + 2)] = 1

        # 6-th move
        mpp[(x + 2, y + 1)] = 1

        # 7-th move
        mpp[(x + 2, y - 1)] = 1

        # 8-th move
        mpp[(x - 1, y - 2)] = 1

    # iterate for all possible 8 coordinates
    for i in range(-1, 2):
        for j in range(-1, 2):
            nx = kx + i
            ny = ky + j

            if i != 0 and j != 0:

                # check a move can be made or not
                if not mpp[(nx, ny)]:
                    return True

    # any moves
    return False

# Driver Code
if __name__ == "__main__":

    a = [[1, 0], [0, 2], [2, 5],
         [4, 4], [5, 0], [6, 2]]

    n = len(a)
    x, y = 3, 2

    if checkCheckMate(a, n, x, y):
        print("Not Checkmate!")
    else:
        print("Yes its checkmate!")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program for checking if a king
// can move a valid move or not when
// N nights are there in a modified chessboard
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

static bool checkCheckMate(pair []a, int n,
                             int kx, int ky)
{

    // Pair of hash to mark the coordinates
    Dictionary<pair,
               int> mpp = new Dictionary<pair,
                                         int>();

    // iterate for Given N knights
    for (int i = 0; i < n; i++)
    {
        int x = a[i].first;
        int y = a[i].second;

        // mark all the "L" shaped coordinates
        // that can be reached by a Knight

        // initial position
        mpp.Add(new pair( x, y ), 1);

        // 1-st move
        mpp.Add(new pair( x - 2, y + 1 ), 1);

        // 2-nd move
        mpp.Add(new pair( x - 2, y - 1 ), 1);

        // 3-rd move
        mpp.Add(new pair( x + 1, y + 2 ), 1);

        // 4-th move
        mpp.Add(new pair( x + 1, y - 2 ), 1);

        // 5-th move
        mpp.Add(new pair( x - 1, y + 2 ), 1);

        // 6-th move
        mpp.Add(new pair( x + 2, y + 1 ), 1);

        // 7-th move
        mpp.Add(new pair( x + 2, y - 1 ), 1);

        // 8-th move
        mpp.Add(new pair( x - 1, y - 2 ), 1);
    }

    // iterate for all possible 8 coordinates
    for (int i = -1; i < 2; i++)
    {
        for (int j = -1; j < 2; j++)
        {
            int nx = kx + i;
            int ny = ky + j;
            if (i != 0 && j != 0)
            {

                // check a move can be made or not
                pair p = new pair(nx, ny);
                if (mpp.ContainsKey(p))
                {
                    return true;
                }
            }
        }
    }

    // any moves
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    pair []a = {new pair( 1, 0 ), new pair( 0, 2 ),
                new pair( 2, 5 ), new pair( 4, 4 ),
                new pair( 5, 0 ), new pair( 6, 2 )};

    int n = a.Length;

    int x = 3, y = 2;
    if (checkCheckMate(a, n, x, y))
        Console.WriteLine("Not Checkmate!");
    else
        Console.WriteLine("Yes its checkmate!");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program for checking if a king
// can move a valid move or not when
// N nights are there in a modified chessboard

class pair
{
    constructor(first, second)
    {
        this.first = first;
        this.second = second;
    }
}

function checkCheckMate(a, n, kx, ky)
{

    // Pair of hash to mark the coordinates
    var mpp = new Map();

    // iterate for Given N knights
    for (var i = 0; i < n; i++)
    {
        var x = a[i].first;
        var y = a[i].second;

        // mark all the "L" shaped coordinates
        // that can be reached by a Knight

        // initial position
        mpp.set(new pair( x, y ), 1);

        // 1-st move
        mpp.set(new pair( x - 2, y + 1 ), 1);

        // 2-nd move
        mpp.set(new pair( x - 2, y - 1 ), 1);

        // 3-rd move
        mpp.set(new pair( x + 1, y + 2 ), 1);

        // 4-th move
        mpp.set(new pair( x + 1, y - 2 ), 1);

        // 5-th move
        mpp.set(new pair( x - 1, y + 2 ), 1);

        // 6-th move
        mpp.set(new pair( x + 2, y + 1 ), 1);

        // 7-th move
        mpp.set(new pair( x + 2, y - 1 ), 1);

        // 8-th move
        mpp.set(new pair( x - 1, y - 2 ), 1);
    }

    // iterate for all possible 8 coordinates
    for (var i = -1; i < 2; i++)
    {
        for (var j = -1; j < 2; j++)
        {
            var nx = kx + i;
            var ny = ky + j;
            if (i != 0 && j != 0)
            {

                // check a move can be made or not
                var p = new pair(nx, ny);
                if (mpp.has(p))
                {
                    return true;
                }
            }
        }
    }

    // any moves
    return false;
}

// Driver Code
var a = [new pair( 1, 0 ), new pair( 0, 2 ),
            new pair( 2, 5 ), new pair( 4, 4 ),
            new pair( 5, 0 ), new pair( 6, 2 )];
var n = a.length;
var x = 3, y = 2;
if (checkCheckMate(a, n, x, y))
    document.write("Not Checkmate!");
else
    document.write("Yes its checkmate!");

</script>
```

**Output:** 

```
Yes its checkmate!
```
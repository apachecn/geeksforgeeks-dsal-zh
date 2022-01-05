# 求给定 3 个顶点的矩形第四个顶点的坐标

> 原文:[https://www . geeksforgeeks . org/find-给定三个顶点的矩形的第四个顶点的坐标/](https://www.geeksforgeeks.org/find-the-cordinates-of-the-fourth-vertex-of-a-rectangle-with-given-3-vertices/)

给定一个 **N * M** 网格。它正好包含三个**' ***和每隔一个细胞是一个**' '**其中“*”表示矩形的顶点。任务是找到第四个(缺失的)顶点的坐标(基于 1 的索引)。
**举例:**

> **输入:**网格[][] = {"*。*", "*.."、“…”}
> **输出:** 2 3
> (1，1)、(1，3)和(2，1)是矩形的给定坐标，其中(2，3)是缺失的坐标。
> **输入:**网格[][] = {"*。*", "..* }
> **输出:** 2 1

**方法:**通过迭代给定的网格，找到 3 个顶点的坐标。因为矩形由 2 个 X 坐标、2 个 Y 坐标和 4 个顶点组成，所以每个 X 坐标和 Y 坐标应该正好出现两次。我们可以计算每个 X 和 Y 坐标在 3 个给定顶点中出现的次数，第 4 个顶点的坐标只出现一次。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that return the coordinates
// of the fourth vertex of the rectangle
pair<int, int> findFourthVertex(int n, int m, string s[])
{
    unordered_map<int, int> row, col;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)

            // Save the coordinates of the given
            // vertices of the rectangle
            if (s[i][j] == '*') {
                row[i]++;
                col[j]++;
            }
    int x, y;
    for (auto tm : row)
        if (tm.second == 1)
            x = tm.first;
    for (auto tm : col)
        if (tm.second == 1)
            y = tm.first;

    // 1-based indexing
    return make_pair(x + 1, y + 1);
}

// Driver code
int main()
{
    string s[] = { "*.*", "*..", "..." };
    int n = sizeof(s) / sizeof(s[0]);
    int m = s[0].length();

    auto rs = findFourthVertex(n, m, s);
    cout << rs.first << " " << rs.second;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;
import java.util.Map;

class GfG
{

    // Function that return the coordinates
    // of the fourth vertex of the rectangle
    static Pair<Integer, Integer> findFourthVertex(int n,
                                        int m, String s[])
    {
        HashMap<Integer, Integer> row = new HashMap<>();
        HashMap<Integer, Integer> col = new HashMap<>();

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {

                // Save the coordinates of the given
                // vertices of the rectangle
                if (s[i].charAt(j) == '*')
                {

                    if (row.containsKey(i))
                    {
                        row.put(i, row.get(i) + 1);
                    }
                    else
                    {
                        row.put(i, 1);
                    }

                    if (col.containsKey(j))
                    {
                        col.put(j, col.get(j) + 1);
                    }
                    else
                    {
                        col.put(j, 1);
                    }
                }
            }
        }

        int x = 0, y = 0;
        for (Map.Entry<Integer, Integer> entry : row.entrySet())
        {
            if (entry.getValue() == 1)
                x = entry.getKey();
        }

        for (Map.Entry<Integer, Integer> entry : col.entrySet())
        {
            if (entry.getValue() == 1)
                y = entry.getKey();
        }

        // 1-based indexing
        Pair<Integer, Integer> ans = new Pair<>(x + 1, y + 1);
        return ans;
    }

    // Driver Code
    public static void main(String []args)
    {

        String s[] = { "*.*", "*..", "..." };
        int n = s.length;
        int m = s[0].length();

        Pair<Integer, Integer> rs = findFourthVertex(n, m, s);
        System.out.println(rs.first + " " + rs.second);
    }
}

class Pair<A, B>
{
    A first;
    B second;

    public Pair(A first, B second)
    {
        this.first = first;
        this.second = second;
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that return the coordinates
# of the fourth vertex of the rectangle
def findFourthVertex(n, m, s) :

    row = dict.fromkeys(range(n), 0)
    col = dict.fromkeys(range(m), 0)

    for i in range(n) :
        for j in range(m) :

            # Save the coordinates of the given
            # vertices of the rectangle
            if (s[i][j] == '*') :
                row[i] += 1;
                col[j] += 1;

    for keys,values in row.items() :
        if (values == 1) :
            x = keys;

    for keys,values in col.items() :
        if (values == 1) :
            y = keys;

    # 1-based indexing
    return (x + 1, y + 1) ;

# Driver code
if __name__ == "__main__" :

    s = [ "*.*", "*..", "..." ]
    n = len(s);
    m = len(s[0]);

    rs = findFourthVertex(n, m, s);
    print(rs[0], rs[1])

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GfG
{

    // Function that return the coordinates
    // of the fourth vertex of the rectangle
    static Pair<int, int> findFourthVertex(int n,
                                        int m, String []s)
    {
        Dictionary<int, int> row = new Dictionary<int, int>();
        Dictionary<int, int> col = new Dictionary<int, int>();

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {

                // Save the coordinates of the given
                // vertices of the rectangle
                if (s[i][j] == '*')
                {

                    if (row.ContainsKey(i))
                    {
                        row[i] = row[i] + 1;
                    }
                    else
                    {
                        row.Add(i, 1);
                    }

                    if (col.ContainsKey(j))
                    {
                        col[j] = col[j] + 1;
                    }
                    else
                    {
                        col.Add(j, 1);
                    }
                }
            }
        }

        int x = 0, y = 0;
        foreach(KeyValuePair<int, int> entry in row)
        {
            if (entry.Value == 1)
                x = entry.Key;
        }

        foreach(KeyValuePair<int, int> entry in col)
        {
            if (entry.Value == 1)
                y = entry.Key;
        }

        // 1-based indexing
        Pair<int, int> ans = new Pair<int, int>(x + 1, y + 1);
        return ans;
    }

    // Driver Code
    public static void Main(String []args)
    {

        String []s = { "*.*", "*..", "..." };
        int n = s.Length;
        int m = s[0].Length;

        Pair<int, int> rs = findFourthVertex(n, m, s);
        Console.WriteLine(rs.first + " " + rs.second);
    }
}

class Pair<A, B>
{
    public A first;
    public B second;

    public Pair(A first, B second)
    {
        this.first = first;
        this.second = second;
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that return the coordinates
// of the fourth vertex of the rectangle
function findFourthVertex(n, m, s)
{
    var row = new Map(), col = new Map();
    for (var i = 0; i < n; i++)
        for (var j = 0; j < m; j++)

            // Save the coordinates of the given
            // vertices of the rectangle
            if (s[i][j] == '*') {

                if(row.has(i))
                    row.set(i, row.get(i)+1)
                else
                    row.set(i, 1)

                if(col.has(j))
                    col.set(j, col.get(j)+1)
                else
                    col.set(j, 1)
            }
    var x, y;
    row.forEach((value, key) => {
        if (value == 1)
            x = key;
    });

    col.forEach((value, key) => {
        if (value == 1)
            y = key;
    });

    // 1-based indexing
    return [x + 1, y + 1];
}

// Driver code
var s = ["*.*", "*..", "..." ];
var n = s.length;
var m = s[0].length;
var rs = findFourthVertex(n, m, s);
document.write( rs[0] + " " + rs[1]);

// This code is contributed by famously.
</script>
```

**Output:** 

```
2 3
```

**时间复杂度:**O(N * M)
T3】辅助空间: O(N + M)
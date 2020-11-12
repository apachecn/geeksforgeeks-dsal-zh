# N 个轴平行矩形之间缺少顶点

> 原文：[https://www.geeksforgeeks.org/missing-vertex-among-n-axis-parallel-rectangles/](https://www.geeksforgeeks.org/missing-vertex-among-n-axis-parallel-rectangles/)

给定二维笛卡尔坐标系中的`N`个轴平行矩形以及`4N-1`个顶点的坐标，任务是找到缺失的单个顶点。 

**示例**：

> **输入**：`N = 2, V[][] = {{1, 1}, {1, 2}, {4, 6}, {2, 1}, {9, 6}, { 9, 3}, {4, 3}`
>
> **输出**：`{2, 2}`
>
> **说明**：
>
> 形成轴平行矩形的坐标为`{4, 6}, {9, 6}, {4, 3}, {9, 3}`。
>
> 对于要形成矩形`{1, 1}, {1, 2}, {2, 1}`的剩余坐标，丢失的坐标是`{2, 2}`
>
> **输入**：`N = 3, V[][] = {{3, 8}, {0, 0}, {4, 6}, {0, 2}, {9, 6}, {9, 3}, {4, 3 }, {6, 4}, {1, 0}, {3, 4}, {6, 8}}`
>
> **输出**：`{1, 2}`

**方法**：

请按照以下步骤解决问题：

*   将频率`x`坐标和`y`坐标存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。

*   在映射上进行迭代，以找到两个坐标的频率都为奇数的元素。

*   最后，以奇数频率打印`x`和`y`坐标。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

void MissingPoint(vector<pair<int, int> > V,
                  int N)
{
    map<int, int> mp;
    for (int i = 0; i < V.size(); i++) {
        mp[V[i].first]++;
    }

    int x, y;
    for (auto it : mp) {
        if (it.second % 2 == 1) {
            x = it.first;
            break;
        }
    }
    mp.clear();
    for (int i = 0; i < V.size(); i++) {
        mp[V[i].second]++;
    }

    for (auto it : mp) {
        if (it.second % 2 == 1) {
            y = it.first;
            break;
        }
    }

    cout << x << " " << y;
}

// Driver Code
int main()
{

    // Number of rectangles
    int N = 2;

    // Stores the coordinates
    vector<pair<int, int> > V;

    // Insert the coordinates
    V.push_back({ 1, 1 });
    V.push_back({ 1, 2 });
    V.push_back({ 4, 6 });
    V.push_back({ 2, 1 });
    V.push_back({ 9, 6 });
    V.push_back({ 9, 3 });
    V.push_back({ 4, 3 });

    MissingPoint(V, N);

    return 0;
}

```

## Java

```java

// Java Program to implement
// the above approach
import java.util.*;
class GFG{
    static class pair
    { 
        int first, second; 
        public pair(int first, int second)  
        { 
            this.first = first; 
            this.second = second; 
        }    
    } 
static void MissingPoint(Vector<pair> V, int N)
{
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();
    for (int i = 0; i < V.size(); i++) 
    {
        if(mp.containsKey(V.get(i).first))
            mp.put(V.get(i).first, 
                   V.get(i).first + 1);
        else
            mp.put(V.get(i).first, 1);
    }
    int x = 0, y = 0;
    for (Map.Entry<Integer,
                   Integer> it : mp.entrySet()) 
    {
        if (it.getValue() % 2 == 1) 
        {
            x = it.getKey();
            break;
        }
    }
    mp.clear();
    for (int i = 0; i < V.size(); i++) 
    {
        if(mp.containsKey(V.get(i).second))
            mp.put(V.get(i).second, 
                   V.get(i).second + 1);
        else
            mp.put(V.get(i).second, 1);
    }
    for (Map.Entry<Integer,
                   Integer> it : mp.entrySet()) 
    {
        if (it.getValue() % 2 == 1) 
        {
            y = it.getKey();
            break;
        }
    }
    System.out.print(x + " " + y);
}

// Driver Code
public static void main(String[] args)
{
    // Number of rectangles
    int N = 2;

    // Stores the coordinates
    Vector<pair> V = new Vector<pair>();

    // Insert the coordinates
    V.add(new pair(1, 1));
    V.add(new pair(1, 2));
    V.add(new pair(4, 6));
    V.add(new pair(2, 1));
    V.add(new pair(9, 6));
    V.add(new pair(9, 3));
    V.add(new pair(4, 3));

    MissingPoint(V, N);
}
}

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 program for the above approach
from collections import defaultdict

def MissingPoint(V, N):

    mp = defaultdict(lambda : 0)
    for i in range(len(V)):
        mp[V[i][0]] += 1

    for it in mp.keys():
        if(mp[it] % 2 == 1):
            x = it
            break

    del mp
    mp = defaultdict(lambda : 0)

    for i in range(len(V)):
        mp[V[i][1]] += 1

    for it in mp.keys():
        if(mp[it] % 2 == 1):
            y = it
            break

    print(x, y)

# Driver code
if __name__ == '__main__':

    # Number of rectangles
    N = 2

    # Stores the coordinates
    V = []

    # Insert the coordinates 
    V.append([1, 1])
    V.append([1, 2])
    V.append([4, 6])
    V.append([2, 1])
    V.append([9, 6])
    V.append([9, 3])
    V.append([4, 3])

    MissingPoint(V, N)

# This code is contributed by Shivam Singh

```

## C#

```cs

// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

class pair
{ 
  public int first, second; 
  public pair(int first, int second)  
  { 
    this.first = first; 
    this.second = second; 
  }    
}

static void MissingPoint(List<pair> V, 
                         int N)
{
  Dictionary<int,
             int> mp = new Dictionary<int,
                                      int>();
  for (int i = 0; i < V.Count; i++) 
  {
    if(mp.ContainsKey(V[i].first))
      mp[V[i].first] = mp[V[i].first] + 1;
    else
      mp.Add(V[i].first, 1);
  }

  int x = 0, y = 0;
  foreach (KeyValuePair<int, 
                        int> it in mp) 
  {
    if (it.Value % 2 == 1) 
    {
      x = it.Key;
      break;
    }
  }
  mp.Clear();

  for (int i = 0; i < V.Count; i++) 
  {
    if(mp.ContainsKey(V[i].second))
      mp[V[i].second] = mp[V[i].second] + 1;
    else
      mp.Add(V[i].second, 1);
  }

  foreach (KeyValuePair<int,
                        int> it in mp) 
  {
    if (it.Value % 2 == 1) 
    {
      y = it.Key;
      break;
    }
  }
  Console.Write(x + " " + y);
}

// Driver Code
public static void Main(String[] args)
{
  // Number of rectangles
  int N = 2;

  // Stores the coordinates
  List<pair> V = new List<pair>();

  // Insert the coordinates
  V.Add(new pair(1, 1));
  V.Add(new pair(1, 2));
  V.Add(new pair(4, 6));
  V.Add(new pair(2, 1));
  V.Add(new pair(9, 6));
  V.Add(new pair(9, 3));
  V.Add(new pair(4, 3));

  MissingPoint(V, N);
}
}

// This code is contributed by Rajput-Ji

```

**输出**： 

```
2 2

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。



* * *

* * *




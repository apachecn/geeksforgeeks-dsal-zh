# 按升序打印二维坐标点，然后打印其频率

> 原文：[https://www.geeksforgeeks.org/print-2-d-co-ordinate-points-in-ascending-order-followed-by-their-frequencies/](https://www.geeksforgeeks.org/print-2-d-co-ordinate-points-in-ascending-order-followed-by-their-frequencies/)

给定两个数组 **x []** 和 **y []** ，其中 **x [i]** 代表 **x** 坐标， **y [i ]** 代表二维点的相应 y 坐标，任务是按升序打印坐标点，然后打印其频率。

**示例**：

> **输入**：x [] = {1、2、1、1、1}，y [] = {1、1、3、1、3}。
> **输出**：
> 1 1 2
> 1 3 2
> 2 1 1
> **输入**：x [] = {-1，2，1，1，-1，2}，y [] = {-1，1，-3，-1，3}。
> **输出**：
> -1 -1 2
> 1 -3 1
> 2 1 1
> 2 3 1

**方法**：想法是使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，其密钥为**（x [i]，y [i]）对**，映射值作为 同一点。 键值将存储一对坐标，而映射值将存储其各自的频率。

以下是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the coordinates along with
// their frequency in ascending order
void Print(int x[], int y[], int n)
{

    // map to store the pairs
    // and their frequencies
    map<pair<int, int>, int> m;

    // Store the coordinates along
    // with their frequencies
    for (int i = 0; i < n; i++)
        m[make_pair(x[i], y[i])]++;

    map<pair<int, int>, int>::iterator i;

    for (i = m.begin(); i != m.end(); i++) {
        cout << (i->first).first << " "
             << (i->first).second << " "
             << i->second << "\n";
    }
}

// Driver code
int main()
{
    int x[] = { 1, 2, 1, 1, 1 };
    int y[] = { 1, 1, 3, 1, 3 };
    int n = sizeof(x) / sizeof(int);

    Print(x, y, n);

    return 0;
}

```

## Python3

```py

# Python3 implementation of the approach

# Function to print the coordinates along with
# their frequency in ascending order
def Print(x, y, n):

    # map to store the pairs
    # and their frequencies
    m = dict()

    # Store the coordinates along
    # with their frequencies
    for i in range(n):
        m[(x[i], y[i])] = m.get((x[i], 
                                 y[i]), 0) + 1

    e = sorted(m)

    for i in e:
        print(i[0], i[1], m[i])

# Driver code
x = [1, 2, 1, 1, 1]
y = [1, 1, 3, 1, 3]
n = len(x)

Print(x, y, n)

# This code is contributed 
# by mohit kumar

```

## C#

```cs

// C# implementation of 
// the above approach
using System;
using System.Collections.Generic;
class GFG{

public class store : 
       IComparer<KeyValuePair<int,
                              int>>
{
  public int Compare(KeyValuePair<int,
                                  int> x, 
                     KeyValuePair<int,
                                  int> y)
  {
    if(x.Key != y.Key)
    {
      return x.Key.CompareTo(y.Key);    
    }
    else
    {
      return x.Value.CompareTo(y.Value);    
    }

  }
}

// Function to print the 
// coordinates along with
// their frequency in 
// ascending order
static void Print(int []x, 
                  int []y, int n)
{
  // Map to store the pairs
  // and their frequencies
  SortedDictionary<KeyValuePair<int,
                                int>, int> m = 
        new SortedDictionary<KeyValuePair<int,
                                          int>,
                                          int>(new store());

  // Store the coordinates along
  // with their frequencies
  for (int i = 0; i < n; i++)
  {
    KeyValuePair<int,
                 int> tmp = 
       new KeyValuePair<int,
                        int>(x[i], y[i]);

    if(m.ContainsKey(tmp))
    {
      m[tmp]++;
    }
    else{
      m[tmp] = 1;
    }
  }

  foreach(KeyValuePair<KeyValuePair<int,
                                    int>, int> i in m)
  {
    Console.Write(i.Key.Key + " " + 
                  i.Key.Value + " " + 
                  i.Value + "\n");
  }
}

// Driver code
public static void Main(string[] args) 
{
  int []x = {1, 2, 1, 1, 1};
  int []y = {1, 1, 3, 1, 3};
  int n = x.Length;
  Print(x, y, n);
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
1 1 2
1 3 2
2 1 1

```



* * *

* * *




# 矩阵中所有最小频率元素之和

> 原文:[https://www . geesforgeks . org/矩阵中所有最小频率元素之和/](https://www.geeksforgeeks.org/sum-of-all-minimum-frequency-elements-in-matrix/)

给定一个包含重复元素的 NxM 整数矩阵。任务是找出给定矩阵中所有最小出现元素的和。这是矩阵中频率均匀的所有元素的总和。
**例** :

```
Input : mat[] = {{1, 1, 2},
                {2, 3, 3},
                {4, 5, 3}}
Output : 9
The min occurring elements are 4, 5 and they 
occurs only 1 time.
Therefore, sum = 4+5 = 9

Input : mat[] = {{10, 20},
                 {40, 40}}
Output : 30
```

**接近** :

*   遍历矩阵，使用 C++中的映射来存储矩阵元素的频率，使得映射的关键是矩阵元素，值是它在矩阵中的频率。
*   然后遍历地图找到最小频率。
*   最后，遍历地图，找出元素的频率，并检查它是否与上一步中获得的最小频率相匹配，如果匹配，则将该元素的频率乘以总和。

以下是上述方法的实现:

## C++

```
// C++ program to find sum of all min
// frequency elements in a Matrix

#include <bits/stdc++.h>
using namespace std;

#define N 3 // Rows
#define M 3 // Columns

// Function to find sum of all min
// frequency elements in a Matrix
int sumMinOccurring(int arr[N][M])
{
    // Store frequencies of elements
    // in matrix
    map<int, int> mp;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            mp[arr[i][j]]++;
        }
    }

    // Find minimum frequency
    int sum = 0;
    int minFreq = INT_MAX;
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {
        if (itr->second < minFreq)
            minFreq = itr->second;
    }

    // Sum of minimum frequency elements
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {
        if (itr->second == minFreq) {
            sum += (itr->first) * (itr->second);
        }
    }

    return sum;
}

// Driver Code
int main()
{

    int mat[N][M] = { { 1, 2, 3 },
                      { 1, 3, 2 },
                      { 1, 5, 6 } };

    cout << sumMinOccurring(mat) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all min
// frequency elements in a Matrix
import java.util.HashMap;
import java.util.Iterator;

class GFG
{
    static int N = 3; // Rows
    static int M = 3; // Columns

    // Function to find sum of all min
    // frequency elements in a Matrix
    public static int sumMinOccuring(int[][] arr)
    {

        // Store frequencies of elements
        // in matrix
        HashMap<Integer, Integer> mp = new HashMap<>();
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
            {
                if (mp.containsKey(arr[i][j]))
                {
                    int x = mp.get(arr[i][j]);
                    mp.put(arr[i][j], x + 1);
                }
                else
                    mp.put(arr[i][j], 1);
            }
        }

        // Find minimum frequency
        int sum = 0;
        int minFreq = Integer.MAX_VALUE;
        for (HashMap.Entry<Integer,
                           Integer> entry : mp.entrySet())
        {
            if (entry.getValue() < minFreq)
                minFreq = entry.getValue();
        }

        // Sum of minimum frequency elements
        for (HashMap.Entry<Integer,
                           Integer> entry : mp.entrySet())
        {
            if (entry.getValue() == minFreq)
                sum += entry.getKey() * entry.getValue();
        }

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[][] mat = { { 1, 2, 3 },
                        { 1, 3, 2 },
                        { 1, 5, 6 } };

        System.out.println(sumMinOccuring(mat));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find sum of all min
# frequency elements in a Matrix

import sys
import math

# Store frequencies of elements
# in matrix
def sumMinOccuring(mat):
    n,m=len(mat),len(mat[0])
    _map={}
    for i in range(n):
        for j in range(m):
            d=mat[i][j]
            if d in _map:
                _map[d]=_map.get(d)+1
            else:
                _map[d]=1

    # Find minimum frequency
    _sum,minFreq=0,sys.maxsize
    for i in _map:
        minFreq=min(minFreq,_map.get(i))

    # Sum of minimum frequency elements
    for i in range(n):
        for j in range(m):
            if _map.get(mat[i][j])==minFreq:
                _sum+=mat[i][j]

    return _sum

# Driver Code
if __name__=='__main__':
    mat=[[1,2,3],[1,3,2],[1,5,6]]
    print(sumMinOccuring(mat))

# This code is Contributed by Vikash Kumar 37
```

## C#

```
// C# program to find sum of all min
// frequency elements in a Matrix
using System;
using System.Collections.Generic;

class GFG
{
    static int N = 3; // Rows
    static int M = 3; // Columns

    // Function to find sum of all min
    // frequency elements in a Matrix
    public static int sumMinOccuring(int[,] arr)
    {

        // Store frequencies of elements
        // in matrix
        Dictionary<int,
                   int> mp = new Dictionary<int,
                                            int>();
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
            {
                if (mp.ContainsKey(arr[i, j]))
                {
                    int x = mp[arr[i, j]];
                    mp[arr[i, j]] = x + 1;
                }
                else
                    mp[arr[i, j]] = 1;
            }
        }

        // Find minimum frequency
        int sum = 0;
        int minFreq = 10000009;
        foreach(KeyValuePair<int, int> ele1 in mp)
        {
            if(ele1.Value < minFreq)
                minFreq = ele1.Value;
        }

        // Sum of minimum frequency elements
        foreach(KeyValuePair<int, int> ele1 in mp)
        {
            if (ele1.Value == minFreq)
                sum += ele1.Key * ele1.Value;
        }
        return sum;
    }

    // Driver code
    public static void Main()
    {
        int[,] mat = new int[3, 3] {{ 1, 2, 3 },
                                    { 1, 3, 2 },
                                    { 1, 5, 6 }};

        Console.Write(sumMinOccuring(mat));
    }
}

// This code is contributed by
// Mohit kumar
```

## java 描述语言

```
<script>

// JavaScript program to find sum of all min
// frequency elements in a Matrix

let N = 3; // Rows
let M = 3; // Columns

// Function to find sum of all min
    // frequency elements in a Matrix
function sumMinOccuring(arr)
{
    // Store frequencies of elements
        // in matrix
        let mp = new Map();
        for (let i = 0; i < N; i++)
        {
            for (let j = 0; j < M; j++)
            {
                if (mp.has(arr[i][j]))
                {
                    let x = mp.get(arr[i][j]);
                    mp.set(arr[i][j], x + 1);
                }
                else
                    mp.set(arr[i][j], 1);
            }
        }

        // Find minimum frequency
        let sum = 0;
        let minFreq = Number.MAX_VALUE;
        for (let [key, value] of mp.entries())
        {
            if (value < minFreq)
                minFreq = value;
        }

        // Sum of minimum frequency elements
        for (let [key, value] of mp.entries())
        {
            if (value == minFreq)
                sum += key * value;
        }

        return sum;
}

// Driver code
let mat=[[1,2,3],[1,3,2],[1,5,6]];

document.write(sumMinOccuring(mat));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
11
```

**时间复杂度:**O(M x N)
T3】辅助空间: O(M x N)
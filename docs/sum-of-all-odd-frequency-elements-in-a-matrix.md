# 矩阵中所有奇数频率元素的和

> 原文:[https://www . geeksforgeeks . org/矩阵中所有奇数频率元素之和/](https://www.geeksforgeeks.org/sum-of-all-odd-frequency-elements-in-a-matrix/)

给定一个包含重复元素的 NxM 整数矩阵。任务是找出给定矩阵中所有奇数出现元素的和。这是矩阵中所有频率为奇数的元素的总和。
**例** :

```
Input : mat[] = {{1, 1, 2},
                {2, 3, 3},
                {4, 5, 3}}
Output : 18
The odd occurring elements are 3, 4, 5 and their number
of occurrences are 3, 1, 1 respectively. Therefore,
sum = 3+3+3+4+5 = 18.

Input : mat[] = {{10, 20},
                 {40, 40}}
Output : 30
```

**接近** :

*   遍历矩阵，使用 C++中的映射来存储矩阵元素的频率，使得映射的关键是矩阵元素，值是它在矩阵中的频率。
*   然后，遍历地图，找到元素的频率，并检查它是否是奇数，如果是奇数，然后将这个元素的频率乘以总和。

以下是上述方法的实现:

## C++

```
// C++ program to find sum of all odd
// frequency elements in a Matrix

#include <bits/stdc++.h>
using namespace std;

#define N 3 // Rows
#define M 3 // Columns

// Function to find sum of all odd
// frequency elements in a Matrix
int sumOddOccurring(int arr[N][M])
{

    // Store frequencies of elements
    // in matrix
    map<int, int> mp;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            mp[arr[i][j]]++;
        }
    }

    // Sum of odd frequency elements
    int sum = 0;
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {
        if (itr->second % 2 != 0) {
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

    cout << sumOddOccurring(mat) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all odd
// frequency elements in a Matrix

import java.util.*;

class GFG
{

    static int N = 3; // Rows
    static int M = 3; // Columns

    // Function to find sum of all odd
    // frequency elements in a Matrix
    static int sumOddOccurring(int arr[][])
    {
        // Store frequencies of elements
        // in matrix
        Map<Integer, Integer> mp = new HashMap<>();
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
            {
                if (mp.containsKey(arr[i][j]))
                {
                    mp.put(arr[i][j], mp.get(arr[i][j]) + 1);
                }
                else
                {
                    mp.put(arr[i][j], 1);
                }
            }
        }

        int sum = 0;

        // Sum of odd frequency elements
        for (Map.Entry<Integer, Integer> itr : mp.entrySet())
        {
            if (itr.getValue() % 2 != 0)
            {
                sum += (itr.getKey()) * (itr.getValue());
            }
        }

        return sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int mat[][] = {{1, 2, 3},
        {1, 3, 2},
        {1, 5, 6}};

        System.out.println(sumOddOccurring(mat));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find sum of all odd
# frequency elements in a Matrix

# Function to find sum of all odd
# frequency elements in a Matrix
def sumOddOccurring(mat):

    # Store frequencies of elements
    # in matrix
    mp = {}
    n, m = len(mat), len(mat[0])
    for i in range(n):
        for j in range(m):
            if mat[i][j] in mp:
                mp[mat[i][j]] = mp.get(mat[i][j]) + 1
            else:
                mp[mat[i][j]] = 1

    # Sum of odd frequency elements
    _sum = 0
    for i in range(n):
        for j in range(m):
            if mp.get(mat[i][j]) % 2 == 1:
                _sum+=mat[i][j]
    return _sum

# Driver Code
if __name__=='__main__':
    mat=[[1,2,3],[1,3,2],[1,5,6]]
    print(sumOddOccurring(mat))

# This code is Contributed by Vikash Kumar 37
```

## C#

```
// C# program to find sum of all odd
// frequency elements in a Matrix
using System;
using System.Collections.Generic;

class GFG
{

    static int N = 3; // Rows
    static int M = 3; // Columns

    // Function to find sum of all odd
    // frequency elements in a Matrix
    static int sumOddOccurring(int [,]arr)
    {
        // Store frequencies of elements
        // in matrix
        Dictionary<int,int> mp = new Dictionary<int,int>();
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
            {
                if (mp.ContainsKey(arr[i,j]))
                {
                    var v = mp[arr[i,j]];
                    mp.Remove(arr[i,j]);
                    mp.Add(arr[i,j], ++v);
                }
                else
                {
                    mp.Add(arr[i,j], 1);
                }
            }
        }

        int sum = 0;

        // Sum of odd frequency elements
        foreach(KeyValuePair<int, int> itr in mp)
        {
            if (itr.Value % 2 != 0)
            {
                sum += (itr.Key) * (itr.Value);
            }
        }

        return sum;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int [,]mat = {{1, 2, 3},
        {1, 3, 2},
        {1, 5, 6}};

        Console.WriteLine(sumOddOccurring(mat));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find sum of all odd
// frequency elements in a Matrix
var N = 3; // Rows
var M = 3; // Columns
// Function to find sum of all odd
// frequency elements in a Matrix
function sumOddOccurring(arr)
{
    // Store frequencies of elements
    // in matrix
    var mp = new Map();
    for (var i = 0; i < N; i++)
    {
        for (var j = 0; j < M; j++)
        {
            if (mp.has(arr[i][j]))
            {
                var v = mp.get(arr[i][j]);
                mp.delete(arr[i][j]);
                mp.set(arr[i][j], ++v);
            }
            else
            {
                mp.set(arr[i][j], 1);
            }
        }
    }
    var sum = 0;

    // Sum of odd frequency elements
    mp.forEach((value, key) => {
        if (value % 2 != 0)
        {
            sum += (key) * (value);
        }
    });
    return sum;
}
// Driver Code
var mat = [[1, 2, 3],
[1, 3, 2],
[1, 5, 6]];
document.write(sumOddOccurring(mat));

</script>
```

**Output:** 

```
14
```

**时间复杂度:**O(N x M)
T3】辅助空间: O(N x M)
# 矩阵中所有偶数频率元素的和

> 原文:[https://www . geesforgeks . org/矩阵中所有偶频元素之和/](https://www.geeksforgeeks.org/sum-of-all-even-frequency-elements-in-matrix/)

给定一个包含重复元素的 NxM 整数矩阵。任务是找出给定矩阵中所有偶数出现元素的和。这是矩阵中频率均匀的所有元素的总和。
**例** :

```
Input : mat[] = {{1, 1, 2},
                {2, 3, 3},
                {4, 5, 3}}
Output : 18
The even occurring elements are 1, 2 and their number
of occurrences are 2, 2 respectively. Therefore,
sum = 1+1+2+2 = 6.

Input : mat[] = {{10, 20},
                 {40, 40}}
Output : 80
```

**接近** :

*   遍历矩阵，使用映射存储矩阵元素的频率，这样映射的关键是矩阵元素，值是它在矩阵中的频率。
*   然后，遍历地图以找到元素的频率并检查它是否为偶数，然后将这个元素的频率乘以总和。

以下是上述方法的实现:

## C++

```
// C++ program to find sum of all even
// frequency elements in a Matrix

#include <bits/stdc++.h>
using namespace std;

#define N 3 // Rows
#define M 3 // Columns

// Function to find sum of all even
// frequency elements in a Matrix
int sumOddOccurring(int arr[N][M])
{

    // Store frequency of elements
    // in matrix
    unordered_map<int, int> mp;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            mp[arr[i][j]]++;
        }
    }

    // Sum even frequency elements
    int sum = 0;
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {
        if (itr->second % 2 == 0) {
            int x = itr->second;
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
// Java program to find sum of all even
// frequency elements in a Matrix
import java.util.*;

class GFG
{

static final int N = 3; // Rows
static final int M = 3; // Columns

// Function to find sum of all even
// frequency elements in a Matrix
static int sumOddOccurring(int arr[][])
{

    // Store frequency of elements
    // in matrix
    Map<Integer,
        Integer> mp = new HashMap<Integer,
                                  Integer>();
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {
            if(mp.get(arr[i][j]) == null)
                mp.put(arr[i][j], 1);
            else
                mp.put(arr[i][j],
                      (mp.get(arr[i][j]) + 1));
        }
    }

    // Sum even frequency elements
    int sum = 0;
    Set< Map.Entry<Integer,
                   Integer> > st = mp.entrySet();

    for (Map.Entry< Integer, Integer> me:st)
    {
        if (me.getValue() % 2 == 0)
        {
            int x = me.getValue();
            sum += (me.getKey()) * (me.getValue());
        }
    }
    return sum;
}

// Driver Code
public static void main(String args[])
{
    int mat[][] = {{ 1, 2, 3 },
                   { 1, 3, 2 },
                   { 1, 5, 6 }};

    System.out.print(sumOddOccurring(mat));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find sum of all even
# frequency elements in a Matrix
import sys

N = 3 # Rows
M = 3 # Columns

# Function to find sum of all even
# frequency elements in a Matrix
def sumOddOccuring(arr):

    # Store frequencies of elements
    # in matrix
    mp = dict()
    for i in range(N):
        for j in range(M):
            if arr[i][j] in mp:
                mp[arr[i][j]] += 1
            else:
                mp[arr[i][j]] = 1

    # Sum of even frequency elements
    s = 0
    for i in mp:
        if mp[i] % 2 == 0:
            x = mp[i]
            s += i * mp[i]

    return s

# Driver code
if __name__ == "__main__":
    mat = [[1, 2, 3],
           [1, 3, 2],
           [1, 5, 6]]

    print(sumOddOccuring(mat))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find sum of all even
// frequency elements in a Matrix
using System;
using System.Collections.Generic;

class Sol
{

static readonly int N = 3; // Rows
static readonly int M = 3; // Columns

// Function to find sum of all even
// frequency elements in a Matrix
static int sumOddOccurring(int [,]arr)
{

    // Store frequency of elements
    // in matrix
    Dictionary<int, int> mp = new Dictionary<int,int>();
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {
            if(!mp.ContainsKey(arr[i, j]))
                mp.Add(arr[i, j], 1);
            else{
                var val = mp[arr[i, j]];
                mp.Remove(arr[i, j]);
                mp.Add(arr[i, j], val + 1);
            }
        }
    }

    // Sum even frequency elements
    int sum = 0;
    foreach(KeyValuePair<int, int> entry in mp)
    {
        if(entry.Value % 2 == 0){
            sum += entry.Key * entry.Value;
        }
    }

    return sum;
}

// Driver Code
public static void Main(String []args)
{

    int [,]mat = { { 1, 2, 3 },
                    { 1, 3, 2 },
                    { 1, 5, 6 } };

    Console.Write( sumOddOccurring(mat) );

}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to find sum of all even
// frequency elements in a Matrix

var N = 3; // Rows
var M = 3; // Columns

// Function to find sum of all even
// frequency elements in a Matrix
function sumOddOccurring(arr)
{

    // Store frequency of elements
    // in matrix
    var mp = new Map();
    for (var i = 0; i < N; i++)
    {
        for (var j = 0; j < M; j++)
        {
            if(!mp.has(arr[i][j]))
                mp.set(arr[i][j], 1);
            else{
                var val = mp.get(arr[i][j]);
                mp.delete(arr[i][j]);
                mp.set(arr[i][j], val + 1);
            }
        }
    }

    // Sum even frequency elements
    var sum = 0;
    mp.forEach((value, key) => {
        if(value % 2 == 0){
            sum += key * value;
        }
    });

    return sum;
}

// Driver Code
var mat = [[1, 2, 3 ],
                [1, 3, 2 ],
                [1, 5, 6 ]];
document.write( sumOddOccurring(mat) );

</script>
```

**Output:** 

```
10
```

**时间复杂度:**O(N x M)
T3】辅助空间: O(N x M)
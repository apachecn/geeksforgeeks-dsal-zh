# 矩阵中所有最大频率元素的总和

> 原文:[https://www . geesforgeks . org/矩阵中所有最大频率元素之和/](https://www.geeksforgeeks.org/sum-of-all-maximum-frequency-elements-in-matrix/)

给定一个包含重复元素的 NxM 整数矩阵。任务是找出给定矩阵中所有最大出现元素的和。这是矩阵中频率均匀的所有元素的总和。
**例** :

```
Input : mat[] = {{1, 1, 1},
                {2, 3, 3},
                {4, 5, 3}}
Output : 12
The max occurring elements are 3 and 1
Therefore, sum = 1 + 1 + 1 + 3 + 3 + 3 = 12

Input : mat[] = {{10, 20},
                 {40, 40}}
Output : 80
```

**接近** :

*   遍历矩阵，使用哈希表存储矩阵元素的频率，这样 map 的键就是矩阵元素，值就是它在矩阵中的频率。
*   然后遍历地图，找到最大频率。
*   最后，遍历哈希表，找到元素的频率，并检查它是否与上一步中获得的最大频率相匹配，如果是，那么将这个元素的频率乘以总和。

以下是上述方法的实现:

## C++

```
// C++ program to find sum of all max
// frequency elements in a Matrix

#include <bits/stdc++.h>
using namespace std;

#define N 3 // Rows
#define M 3 // Columns

// Function to find sum of all max
// frequency elements in a Matrix
int sumMaxOccurring(int arr[N][M])
{
    // Store frequencies of elements
    // in matrix
    unordered_map<int, int> mp;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            mp[arr[i][j]]++;
        }
    }

    // loop to iterate through map
    // and find the maximum frequency
    int sum = 0;
    int maxFreq = INT_MIN;
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {
        if (itr->second > maxFreq)
            maxFreq = itr->second;
    }

    // Sum of maximum frequency elements
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {       
        if (itr->second == maxFreq) {
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

    cout << sumMaxOccurring(mat) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all max
// frequency elements in a Matrix
import java.util.*;

class GFG
{

    static int N = 3; // Rows
    static int M = 3; // Columns

    // Function to find sum of all max
    // frequency elements in a Matrix
    static int sumMaxOccurring(int arr[][])
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

        // loop to iterate through map
        // and find the maximum frequency
        int sum = 0;
        int maxFreq = Integer.MIN_VALUE;
        for (Map.Entry<Integer, Integer> itr : mp.entrySet())
        {
            if (itr.getValue() > maxFreq)
            {
                maxFreq = itr.getValue();
            }
        }

        // Sum of maximum frequency elements
        for (Map.Entry<Integer, Integer> itr : mp.entrySet())
        {
            if (itr.getValue() == maxFreq)
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

        System.out.println(sumMaxOccurring(mat));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find sum of all max
# frequency elements in a Matrix
import sys

N = 3 # Rows
M = 3 # Columns

# Function to find sum of all max
# frequency elements in a Matrix
def sumMaxOccuring(arr):

    # Store frequencies of elements
    # in matrix
    mp = dict()
    for i in range(N):
        for j in range(M):
            if arr[i][j] in mp:
                mp[arr[i][j]] += 1
            else:
                mp[arr[i][j]] = 1

    # loop to iterate through map
    # and find the maximum frequency
    s = 0
    maxFreq = -sys.maxsize
    for i in mp:
        if mp[i] > maxFreq:
            maxFreq = mp[i]

    # Sum of maximum frequency elements
    for i in mp:
        if mp[i] == maxFreq:
            s += i * mp[i]

    return s

# Driver code
if __name__ == "__main__":
    mat = [[1, 2, 3],
           [1, 3, 2],
           [1, 5, 6]]

    print(sumMaxOccuring(mat))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find sum of all max
// frequency elements in a Matrix
using System;
using System.Collections.Generic;   
public class GFG
{

    static int N = 3; // Rows
    static int M = 3; // Columns

    // Function to find sum of all max
    // frequency elements in a Matrix
    static int sumMaxOccurring(int [,]arr)
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
                    var v= mp[arr[i,j]];
                    mp.Remove(arr[i,j]);
                    mp.Add(arr[i,j], v + 1);
                }
                else
                {
                    mp.Add(arr[i,j], 1);
                }
            }
        }

        // loop to iterate through map
        // and find the maximum frequency
        int sum = 0;
        int maxFreq = int.MinValue;
        foreach(KeyValuePair<int, int> itr in mp)
        {
            if (itr.Value > maxFreq)
            {
                maxFreq = itr.Value;
            }
        }

        // Sum of maximum frequency elements
        foreach(KeyValuePair<int, int> itr in mp)
        {
            if (itr.Value == maxFreq)
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

        Console.WriteLine(sumMaxOccurring(mat));
    }
}
// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find sum of all max
// frequency elements in a Matrix

var N = 3; // Rows
var M = 3; // Columns

// Function to find sum of all max
// frequency elements in a Matrix
function sumMaxOccurring(arr)
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
                var v= mp.get(arr[i][j]);
                mp.delete(arr[i][j]);
                mp.set(arr[i][j], v + 1);
            }
            else
            {
                mp.set(arr[i][j], 1);
            }
        }
    }

    // loop to iterate through map
    // and find the maximum frequency
    var sum = 0;
    var maxFreq = -1000000000;

    mp.forEach((value, key) => {
        if (value > maxFreq)
        {
            maxFreq = value;
        }
    });

    // Sum of maximum frequency elements
    mp.forEach((value, key) => {

        if (value == maxFreq)
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
document.write(sumMaxOccurring(mat));

</script>
```

**Output:** 

```
3
```
# 计算矩阵中的多数元素

> 原文:[https://www . geesforgeks . org/count-matrix 中的多数元素/](https://www.geeksforgeeks.org/count-majority-element-in-a-matrix/)

给定一个包含重复元素的 NxM 整数矩阵。任务是找出给定矩阵中所有多数出现元素的计数，其中多数元素是那些频率大于或等于(N*M)/2 的元素。
**例** :

```
Input : mat[] = {{1, 1, 2},
                {2, 3, 3},
                {4, 3, 3}}
Output : 1
The majority elements is 3 and, its frequency is 4.

Input : mat[] = {{20, 20},
                 {40, 40}}
Output : 2
```

**接近** :

*   遍历矩阵，使用 C++中的映射来存储矩阵元素的频率，使得映射的关键是矩阵元素，值是它在矩阵中的频率。
*   然后，遍历地图，找到具有计数变量的元素的频率，以计数多数元素，并检查它是否等于或大于(N*M)/2。如果为真，则增加计数。

以下是上述方法的实现:

## C++

```
// C++ program to find count of all
// majority elements in a Matrix

#include <bits/stdc++.h>
using namespace std;

#define N 3 // Rows
#define M 3 // Columns

// Function to find count of all
// majority elements in a Matrix
int majorityInMatrix(int arr[N][M])
{

    unordered_map<int, int> mp;

    // Store frequency of elements
    // in matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            mp[arr[i][j]]++;
        }
    }

    // loop to iteratre through map   
    int countMajority = 0;
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {

        // check if frequency is greater than
        // or equal to (N*M)/2
        if (itr->second >= ((N * M) / 2)) {
            countMajority++;
        }
    }

    return countMajority;
}

// Driver Code
int main()
{

    int mat[N][M] = { { 1, 2, 2 },
                      { 1, 3, 2 },
                      { 1, 2, 6 } };

    cout << majorityInMatrix(mat) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of all
// majority elements in a Matrix
import java.util.*;

class GFG
{
    static int N = 3; // Rows
    static int M = 3; // Columns

    // Function to find count of all
    // majority elements in a Matrix
    static int majorityInMatrix(int arr[][])
    {

        HashMap<Integer, Integer> mp =
                new HashMap<Integer, Integer>();

        // Store frequency of elements
        // in matrix
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
            {
                if(mp.containsKey(arr[i][j]))
                    mp.put(arr[i][j], mp.get(arr[i][j]) + 1 );
                else
                    mp.put(arr[i][j], 1);
            }
        }

        // loop to iteratre through map
        int countMajority = 0;

        Iterator<HashMap.Entry<Integer, Integer>> itr =
                                mp.entrySet().iterator();

        while(itr.hasNext())
        {
            // check if frequency is greater than
            // or equal to (N*M)/2
            HashMap.Entry<Integer, Integer> entry = itr.next();

            if (entry.getValue() >= ((N * M) / 2))
            {
                countMajority++;
            }
        }

        return countMajority;
    }

    // Driver Code
    public static void main (String[] args)
    {

        int mat[][] = { { 1, 2, 2 },
                        { 1, 3, 2 },
                        { 1, 2, 6 } };

        System.out.println(majorityInMatrix(mat));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python 3 program to find count of all
# majority elements in a Matrix
N = 3 # Rows
M = 3 # Columns

# Function to find count of all
# majority elements in a Matrix
def majorityInMatrix(arr):

    # we take length equal to max
    # value in array
    mp = {i:0 for i in range(7)}

    # Store frequency of elements
    # in matrix
    for i in range(len(arr)):
        for j in range(len(arr)):
            mp[arr[i][j]] += 1

    # loop to iteratre through map
    countMajority = 0
    for key, value in mp.items():

        # check if frequency is greater than
        # or equal to (N*M)/2
        if (value >= (int((N * M) / 2))):
            countMajority += 1

    return countMajority

# Driver Code
if __name__ == '__main__':
    mat = [[1, 2, 2],
           [1, 3, 2],
           [1, 2, 6]]
    print(majorityInMatrix(mat))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to find count of all
// majority elements in a Matrix
using System;
using System.Collections.Generic;

class GFG
{
    static int N = 3; // Rows
    static int M = 3; // Columns

    // Function to find count of all
    // majority elements in a Matrix
    static int majorityInMatrix(int [ , ]arr)
    {

        Dictionary<int, int> mp =
                new Dictionary<int, int>();

        // Store frequency of elements
        // in matrix
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
            {
                if(mp.ContainsKey(arr[i, j]))
                    mp[arr[i, j]]++;
                else
                    mp[arr[i, j]] = 1;
            }
        }

        // loop to iteratre through map
        int countMajority = 0;
        Dictionary<int, int>.KeyCollection keyColl =
                                            mp.Keys;

        foreach( int i in keyColl)
        {    
            // check if frequency is greater than
            // or equal to (N*M)/2

            if ( mp[i] >= ((N * M) / 2))
            {
                countMajority++;
            }
        }

        return countMajority;
    }

    // Driver Code
    public static void Main ()
    {

        int [, ] mat = { { 1, 2, 2 },
                        { 1, 3, 2 },
                        { 1, 2, 6 } };

        Console.WriteLine(majorityInMatrix(mat));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// JavaScript program to find count of all
// majority elements in a Matrix
var N = 3; // Rows
var M = 3; // Columns

// Function to find count of all
// majority elements in a Matrix
function majorityInMatrix(arr)
{

    var mp = new Map();

    // Store frequency of elements
    // in matrix
    for (var i = 0; i < N; i++)
    {
        for (var j = 0; j < M; j++)
        {
            if(mp.has(arr[i][j]))
            {
                    mp.set(arr[i][j], mp.get(arr[i][j])+1)

            }
            else
                mp.set(arr[i][j], 1);
        }
    }

    // loop to iteratre through map
    var countMajority = 0;

    mp.forEach((value, key) => {

        // check if frequency is greater than
        // or equal to (N*M)/2

        if ( value >= (parseInt((N * M) / 2)))
        {
            countMajority++;
        }
    });

    return countMajority;
}

// Driver Code
var mat = [ [ 1, 2, 2 ],
                [ 1, 3, 2 ],
                [ 1, 2, 6 ]];
document.write(majorityInMatrix(mat));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N x M)
**辅助空间:** O(N X M)
**进一步优化:**
我们可以使用[摩尔投票算法](https://www.geeksforgeeks.org/majority-element/)在 O(1)个额外空间中解决上述问题。我们可以简单地把矩阵元素看作一维数组。
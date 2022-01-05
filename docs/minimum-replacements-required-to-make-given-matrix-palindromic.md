# 完成给定矩阵回文所需的最少替换次数

> 原文:[https://www . geesforgeks . org/minimum-replacements-required-to-make-given-matrix-回文/](https://www.geeksforgeeks.org/minimum-replacements-required-to-make-given-matrix-palindromic/)

给定一个具有 **N** 行和 **M** 列的[矩阵](https://www.geeksforgeeks.org/matrix/)，任务是找到生成给定矩阵[回文](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)的所有行和列所需的最小替换。

**示例:**

> **输入:** a[][] = {{1，2，3}，{4，5，3}，{1，2，1}}
> **输出:** 2
> **解释:**要使给定矩阵回文，用 **1** 替换 **a[0][2]** ，用 **4** 替换 a[1][2]。
> 
> **输入:** a[][] = {{1，2，4}，{4，5，6}}
> **输出:** 3
> **解释:**给定矩阵回文，将 **a[0][0]** 替换为 **4** ， **a[1][2]** 替换为 **4** ， **a[[0][1]** 替换为

**方法:**想法是如下所述选择矩阵的四个单元的集合，并相应地进行。

1.  要使矩阵的每一行和每一列回文，遍历给定的矩阵，对于每个单元格 **(i，j)** (i = [0，N/2]，j = [0，M/2])，选择以下四个单元格的集合:

2.  使这四个单元格的值等于其中最常出现的值。计算所需的替换。
3.  完成上述步骤后，打印已执行的更换次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum
// changes to make the matrix
// palindromic
int minchanges(vector<vector<int> > mat)
{
    // Rows in the matrix
    int N = mat.size();

    // Columns in the matrix
    int M = mat[0].size();

    int i, j, ans = 0, x;
    map<int, int> mp;

    // Traverse the given matrix
    for (i = 0; i < N / 2; i++) {
        for (j = 0; j < M / 2; j++) {

            // Store the frequency of
            // the four cells
            mp[mat[i][M - 1 - j]]++;
            mp[mat[i][j]]++;
            mp[mat[N - 1 - i][M - 1 - j]]++;
            mp[mat[N - 1 - i][j]]++;

            x = 0;

            // Iterate over the map
            for (auto it = mp.begin();
                 it != mp.end(); it++) {
                x = max(x, it->second);
            }

            // Min changes to do to make all
            ans = ans + 4 - x;

            // Four elements equal
            mp.clear();
        }
    }

    // Make the middle row palindromic
    if (N % 2 == 1) {
        for (i = 0; i < M / 2; i++) {
            if (mat[N / 2][i]
                != mat[N / 2][M - 1 - i])
                ans++;
        }
    }

    if (M % 2 == 1) {
        for (i = 0; i < N / 2; i++) {

            // Make the middle column
            // palindromic
            if (mat[i][M / 2]
                != mat[N - 1 - i][M / 2])
                ans++;
        }
    }

    // Print minimum changes
    cout << ans;
}

// Driver Code
int main()
{

    // Given matrix
    vector<vector<int> > mat{ { 1, 2, 3 },
                              { 4, 5, 3 },
                              { 1, 2, 1 } };

    // Function Call
    minchanges(mat);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to count minimum
// changes to make the matrix
// palindromic
static void minchanges(int [][]mat)
{

    // Rows in the matrix
    int N = mat.length;

    // Columns in the matrix
    int M = mat[0].length;

    int i, j, ans = 0, x;
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Traverse the given matrix
    for (i = 0; i < N / 2; i++)
    {
        for (j = 0; j < M / 2; j++)
        {

            // Store the frequency of
            // the four cells           
            if(mp.containsKey(mat[i][M - 1 - j]))
            {
                mp.put(mat[i][M - 1 - j],
                       mp.get(mat[i][M - 1 - j]) + 1);
            }
            else
            {
                mp.put(mat[i][M - 1 - j], 1);
            }
            if(mp.containsKey(mat[i][j]))
            {
                mp.put(mat[i][j], mp.get(mat[i][j]) + 1);
            }
            else
            {
                mp.put(mat[i][j], 1);
            }

            if(mp.containsKey(mat[N - 1 - i][M - 1 - j]))
            {
                mp.put(mat[N - 1 - i][M - 1 - j],
                       mp.get(mat[N - 1 - i][M - 1 - j]) + 1);
            }
            else
            {
                mp.put(mat[N - 1 - i][M - 1 - j], 1);
            }
            if(mp.containsKey(mat[N - 1 - i][j]))
            {
                mp.put(mat[N - 1 - i][j],
                       mp.get(mat[N - 1 - i][j])+1);
            }
            else
            {
                mp.put(mat[N - 1 - i][j], 1);
            }
            x = 0;

            // Iterate over the map
            for (Map.Entry<Integer,Integer> it : mp.entrySet())
            {
                x = Math.max(x, it.getValue());
            }

            // Min changes to do to make all
            ans = ans + 4 - x;

            // Four elements equal
            mp.clear();
        }
    }

    // Make the middle row palindromic
    if (N % 2 == 1)
    {
        for (i = 0; i < M / 2; i++)
        {
            if (mat[N / 2][i]
                != mat[N / 2][M - 1 - i])
                ans++;
        }
    }

    if (M % 2 == 1)
    {
        for (i = 0; i < N / 2; i++)
        {

            // Make the middle column
            // palindromic
            if (mat[i][M / 2]
                != mat[N - 1 - i][M / 2])
                ans++;
        }
    }

    // Print minimum changes
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{

    // Given matrix
    int [][]mat = { { 1, 2, 3 },
                              { 4, 5, 3 },
                              { 1, 2, 1 } };

    // Function Call
    minchanges(mat);
}
}

// This code is contributed by shikhasingrajput
```

## 计算机编程语言

```
# Python program for the above approach

# Function to count minimum
# changes to make the matrix
# palindromic
def minchanges(mat) :

    # Rows in the matrix
    N = len(mat)

    # Columns in the matrix
    M = len(mat[0])

    ans = 0
    mp = {}

    # Traverse the given matrix
    for i in range(N//2):
        for j in range(M//2):

            # Store the frequency of
            # the four cells
            mp[mat[i][M - 1 - j]] = mp.get(mat[i][M - 1 - j], 0) + 1
            mp[mat[i][j]] = mp.get(mat[i][j], 0) + 1
            mp[mat[N - 1 - i][M - 1 - j]] = mp.get(mat[N - 1 - i][M - 1 - j], 0) + 1
            mp[mat[N - 1 - i][j]] = mp.get(mat[N - 1 - i][j], 0) + 1

            x = 0

            # Iterate over the map
            for it in mp:
                x = max(x, mp[it])

            # Min changes to do to make all
            ans = ans + 4 - x

            # Four elements equal
            mp.clear()

    # Make the middle row palindromic
    if (N % 2 == 1) :
        for i in range(M // 2):
            if (mat[N // 2][i]
                != mat[N // 2][M - 1 - i]) :
                ans += 1

    if (M % 2 == 1) :
        for i in range(N // 2):

            # Make the middle column
            # palindromic
            if (mat[i][M // 2]
                != mat[N - 1 - i][M // 2]):
                ans += 1

    # Prminimum changes
    print(ans)

# Driver Code

# Given matrix
mat = [[ 1, 2, 3 ],
        [ 4, 5, 3 ],
        [1, 2, 1 ]]

# Function Call
minchanges(mat)

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

  // Function to count minimum
  // changes to make the matrix
  // palindromic
  static void minchanges(int [,]mat)
  {

    // Rows in the matrix
    int N = mat.GetLength(0);

    // Columns in the matrix
    int M = mat.GetLength(1);

    int i, j, ans = 0, x;
    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Traverse the given matrix
    for (i = 0; i < N / 2; i++)
    {
      for (j = 0; j < M / 2; j++)
      {

        // Store the frequency of
        // the four cells           
        if(mp.ContainsKey(mat[i,M - 1 - j]))
        {
          mp[mat[i,M - 1 - j]]=
            mp[mat[i,M - 1 - j]] + 1;
        }
        else
        {
          mp.Add(mat[i,M - 1 - j], 1);
        }
        if(mp.ContainsKey(mat[i,j]))
        {
          mp[mat[i,j]] = mp[mat[i,j]] + 1;
        }
        else
        {
          mp.Add(mat[i,j], 1);
        }

        if(mp.ContainsKey(mat[N - 1 - i,M - 1 - j]))
        {
          mp[mat[N - 1 - i,M - 1 - j]]=
            mp[mat[N - 1 - i,M - 1 - j]] + 1;
        }
        else
        {
          mp.Add(mat[N - 1 - i,M - 1 - j], 1);
        }
        if(mp.ContainsKey(mat[N - 1 - i,j]))
        {
          mp[mat[N - 1 - i,j]] =
            mp[mat[N - 1 - i,j]]+1;
        }
        else
        {
          mp.Add(mat[N - 1 - i,j], 1);
        }
        x = 0;

        // Iterate over the map
        foreach (KeyValuePair<int,int> it in mp)
        {
          x = Math.Max(x, it.Value);
        }

        // Min changes to do to make all
        ans = ans + 4 - x;

        // Four elements equal
        mp.Clear();
      }
    }

    // Make the middle row palindromic
    if (N % 2 == 1)
    {
      for (i = 0; i < M / 2; i++)
      {
        if (mat[N / 2,i]
            != mat[N / 2,M - 1 - i])
          ans++;
      }
    }

    if (M % 2 == 1)
    {
      for (i = 0; i < N / 2; i++)
      {

        // Make the middle column
        // palindromic
        if (mat[i,M / 2]
            != mat[N - 1 - i,M / 2])
          ans++;
      }
    }

    // Print minimum changes
    Console.Write(ans);
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given matrix
    int [,]mat = { { 1, 2, 3 },
                  { 4, 5, 3 },
                  { 1, 2, 1 } };

    // Function Call
    minchanges(mat);
  }
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to count minimum
      // changes to make the matrix
      // palindromic
      function minchanges(mat) {
        // Rows in the matrix
        var N = mat.length;

        // Columns in the matrix
        var M = mat[0].length;

        var i,
          j,
          ans = 0,
          x;
        var mp = {};

        // Traverse the given matrix
        for (i = 0; i < parseInt(N / 2); i++) {
          for (j = 0; j < parseInt(M / 2); j++) {
            // Store the frequency of
            // the four cells
            if (mp.hasOwnProperty(mat[i][M - 1 - j])) {
              mp[mat[i][M - 1 - j]] = mp[mat[i][M - 1 - j]] + 1;
            }
            else {
              mp[mat[i][M - 1 - j]] = 1;
            }
            if (mp.hasOwnProperty(mat[i][j])) {
              mp[mat[(i, j)]] = mp[mat[i][j]] + 1;
            }
            else {
              mp[mat[i][j]] = 1;
            }

            if (mp.hasOwnProperty(mat[N - 1 - i][M - 1 - j])) {
              mp[mat[N - 1 - i][M - 1 - j]] = mp[mat[N - 1 - i][M - 1 - j]] + 1;
            }
            else {
              mp[mat[N - 1 - i][M - 1 - j]] = 1;
            }
            if (mp.hasOwnProperty(mat[N - 1 - i][j])) {
              mp[mat[N - 1 - i][j]] = mp[mat[N - 1 - i][j]] + 1;
            }
            else {
              mp[mat[(N - 1 - i, j)]] = 1;
            }
            x = 0;

            // Iterate over the map
            for (const [key, value] of Object.entries(mp)) {
              x = Math.max(x, value);
            }

            // Min changes to do to make all
            ans = ans + 4 - x;

            // Four elements equal
            mp = {};
          }
        }

        // Make the middle row palindromic
        if (N % 2 === 1) {
          for (i = 0; i < parseInt(M / 2); i++) {
            if (mat[parseInt(N / 2)][i] !=
                    mat[parseInt(N / 2)][M - 1 - i])
              ans++;
          }
        }

        if (M % 2 === 1) {
          for (i = 0; i < parseInt(N / 2); i++) {
            // Make the middle column
            // palindromic
            if (mat[i][parseInt(M / 2)] !=
                    mat[N - 1 - i][parseInt(M / 2)])
              ans++;
          }
        }

        // Print minimum changes
        document.write(ans);
      }

      // Driver Code
      // Given matrix
      var mat = [
        [1, 2, 3],
        [4, 5, 3],
        [1, 2, 1],
      ];

      // Function Call
      minchanges(mat);
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N × M)*
***辅助空间:** O(1)*
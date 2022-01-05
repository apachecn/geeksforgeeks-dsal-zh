# 给定大小的子矩阵，最大值为 1

> 原文:[https://www . geeksforgeeks . org/给定最大值为 1s 的子矩阵/](https://www.geeksforgeeks.org/submatrix-of-given-size-with-maximum-1s/)

给定一个二元矩阵 **mat[][]** 和一个整数 **K** ，任务是找到大小为 K*K 的子矩阵，使得它在矩阵中包含最大数量的 1。

**示例:**

> **输入:** mat[][] = {{1，0，1}，{1，1，0}，{1，0，0}}，K = 2
> **输出:** 3
> **说明:**
> 在给定的矩阵中，有 4 个 2*2、
> |1 0| | 0 | 1 | | 1 | |1 0|
> | 1 |、| 1 0 |、| 1 0 |、| 0 |
> 的子矩阵
> 
> **输入:** mat[][] = {{1，0}，{0，1}}，K = 1
> **输出:** 1
> **说明:**
> 在给定的矩阵中，有 4 个 1*1 阶的子矩阵，
> |1|、|0|、|1|、|0|
> 在这些子矩阵中，两个矩阵包含 1、1。

**方法:**思路是使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决这个问题，在这个技术中，我们一般计算一个窗口的值，然后逐个滑动窗口来计算每个大小为 K 的窗口的解。
要计算最大 1 的子矩阵，使用滑动窗口技术计算每个大小为 K 的可能窗口的行中 1 的数量，并将 1 的计数以矩阵的形式存储。

例如:

```
Let the matrix be {{1,0,1}, {1, 1, 0}} and K = 2

For Row 1 -
Subarray 1: (1, 0), Count of 1 = 1
Subarray 2: (0, 1), Count of 1 = 1

For Row 2 -
Subarray 1: (1, 1), Count of 1 = 2
Subarray 2: (1, 0), Count of 1 = 1

Then the final matrix for count of 1's will be -
[ 1, 1 ]
[ 2, 1 ]
```

类似地，在这个矩阵的每一列上应用滑动窗口技术，计算每个可能的子矩阵中 1 的计数，并从这些计数中取出最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum count of 1's in
// submatrix of order K
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// count of 1's in the
// submatrix of order K
int maxCount(vector<vector<int>> &mat, int k) {

    int n = mat.size();
    int m = mat[0].size();
    vector<vector<int>> a;

    // Loop to find the count of 1's
    // in every possible windows
    // of rows of matrix
    for (int e = 0; e < n; ++e){
        vector<int> s = mat[e];
        vector<int> q;
        int    c = 0;

        // Loop to find the count of
        // 1's in the first window
        int i;
        for (i = 0; i < k; ++i)
            if(s[i] == 1)
                c += 1;

        q.push_back(c);
        int p = s[0];

        // Loop to find the count of
        // 1's in the remaining windows
        for (int j = i + 1; j < m; ++j) {
            if(s[j] == 1)
                c+= 1;
            if(p == 1)
                c-= 1;
            q.push_back(c);
            p = s[j-k + 1];
        }
        a.push_back(q);
    }

    vector<vector<int>> b;
    int max = 0;

    // Loop to find the count of 1's
    // in every possible submatrix
    for (int i = 0; i < a[0].size(); ++i) {
        int c = 0;
        int p = a[0][i];

        // Loop to find the count of
        // 1's in the first window
        int j;
        for (j = 0; j < k; ++j) {
            c+= a[j][i];
        }
        vector<int> q;
        if (c>max)
            max = c;
        q.push_back(c);

        // Loop to find the count of
        // 1's in the remaining windows
        for (int l = j + 1; j < n; ++j) {
            c+= a[l][i];
            c-= p;
            p = a[l-k + 1][i];
            q.push_back(c);
            if (c > max)
                max = c;
        }

        b.push_back(q);
    }

    return max;
}

// Driver code
int main()
{
    vector<vector<int>> mat = {{1, 0, 1}, {1, 1, 0}, {0, 1, 0}};
    int k = 3;

    // Function call
    cout<< maxCount(mat, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum count of 1's in
// submatrix of order K
import java.io.*;
import java.util.*;

class GFG{

// Function to find the maximum
// count of 1's in the
// submatrix of order K
static int maxCount(ArrayList<ArrayList<Integer> > mat, int k)
{
    int n = mat.size();
    int m = mat.get(0).size();
    ArrayList<ArrayList<Integer>> a = new ArrayList<ArrayList<Integer>>();

    // Loop to find the count of 1's
    // in every possible windows
    // of rows of matrix
    for(int e = 0; e < n; ++e)
    {
        ArrayList<Integer> s = mat.get(e);
        ArrayList<Integer> q = new ArrayList<Integer>();
        int c = 0;

        // Loop to find the count of
        // 1's in the first window
        int i;
        for(i = 0; i < k; ++i)
        {
            if (s.get(i) == 1)
            {
                c += 1;
            }
        }
        q.add(c);
        int p = s.get(0);

        // Loop to find the count of
        // 1's in the remaining windows
        for(int j = i + 1; j < m; ++j)
        {
            if (s.get(j) == 1)
            {
                c += 1;
            }
            if (p == 1)
            {
                c -= 1;
            }
            q.add(c);
            p = s.get(j - k + 1);
        }
        a.add(q);
    }

    ArrayList<ArrayList<Integer>> b = new ArrayList<ArrayList<Integer>>();
    int max = 0;

    // Loop to find the count of 1's
    // in every possible submatrix
    for(int i = 0; i < a.get(0).size(); ++i)
    {
        int c = 0;
        int p = a.get(0).get(i);

        // Loop to find the count of
        // 1's in the first window
        int j;
        for(j = 0; j < k; ++j)
        {
            c += a.get(j).get(i);
        }
        ArrayList<Integer> q = new ArrayList<Integer>();

        if (c > max)
        {
            max = c;
        }
        q.add(c);

        // Loop to find the count of
        // 1's in the remaining windows
        for(int l = j + 1; j < n; ++j)
        {

            c += a.get(l).get(i);
            c -= p;
            p = a.get(l - k + 1).get(i);
            q.add(c);

            if (c > max)
            {
                max = c;
            }
        }
        b.add(q);
    }
    return max;
}

// Driver code
public static void main(String[] args)
{
    ArrayList<ArrayList<Integer>> mat = new ArrayList<ArrayList<Integer>>();
    mat.add(new ArrayList<Integer>(Arrays.asList(1, 0, 1)));
    mat.add(new ArrayList<Integer>(Arrays.asList(1, 1, 0)));
    mat.add(new ArrayList<Integer>(Arrays.asList(0, 1, 0)));
    int k = 3;

    // Function call
    System.out.println(maxCount(mat, k));
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum count of 1's in
# submatrix of order K

# Function to find the maximum
# count of 1's in the
# submatrix of order K
def maxCount(mat, k):
    n, m = len(mat), len(mat[0])
    a =[]

    # Loop to find the count of 1's
    # in every possible windows
    # of rows of matrix
    for e in range(n):
        s = mat[e]
        q =[]
        c = 0

        # Loop to find the count of
        # 1's in the first window
        for i in range(k):
            if s[i] == 1:
                c += 1
        q.append(c)
        p = s[0]

        # Loop to find the count of
        # 1's in the remaining windows
        for j in range(i + 1, m):
            if s[j]==1:
                c+= 1
            if p ==1:
                c-= 1
            q.append(c)
            p = s[j-k + 1]
        a.append(q)
    b =[]
    max = 0

    # Loop to find the count of 1's
    # in every possible submatrix
    for i in range(len(a[0])):
        c = 0
        p = a[0][i]

        # Loop to find the count of
        # 1's in the first window
        for j in range(k):
            c+= a[j][i]
        q =[]
        if c>max:
            max = c
        q.append(c)

        # Loop to find the count of
        # 1's in the remaining windows
        for l in range(j + 1, n):
            c+= a[l][i]
            c-= p
            p = a[l-k + 1][i]
            q.append(c)
            if c > max:
                max = c
        b.append(q)
    return max

# Driver Code
if __name__ == "__main__":
    mat = [[1, 0, 1], [1, 1, 0], [0, 1, 0]]
    k = 3

    # Function call
    print(maxCount(mat, k))
```

## C#

```
// C# implementation to find the
// maximum count of 1's in
// submatrix of order K
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum
// count of 1's in the
// submatrix of order K
static int maxCount(List<List<int>> mat, int k)
{
    int n = mat.Count;
    int m = mat[0].Count;
    List<List<int>> a = new List<List<int>>();

    // Loop to find the count of 1's
    // in every possible windows
    // of rows of matrix
    for(int e = 0; e < n; ++e)
    {
        List<int> s = mat[e];
        List<int> q = new List<int>();
        int c = 0;

        // Loop to find the count of
        // 1's in the first window
        int i;

        for(i = 0; i < k; ++i)
        {
            if (s[i] == 1)
            {
                c++;
            }
        }
        q.Add(c);
        int p = s[0];

        // Loop to find the count of
        // 1's in the remaining windows
        for(int j = i + 1; j < m; ++j)
        {
            if (s[j] == 1)
            {
                c++;
            }
            if (p == 1)
            {
                c--;
            }
            q.Add(c);
            p = s[j - k + 1];
        }
        a.Add(q);
    }
    List<List<int>> b = new List<List<int>>();
    int max = 0;

    // Loop to find the count of 1's
    // in every possible submatrix
    for(int i = 0; i < a[0].Count; ++i)
    {
        int c = 0;
        int p = a[0][i];

        // Loop to find the count of
        // 1's in the first window
        int j;
        for(j = 0; j < k; ++j)
        {
            c += a[j][i];
        }

        List<int> q = new List<int>();

        if (c > max)
        {
            max = c;
        }
        q.Add(c);

        // Loop to find the count of
        // 1's in the remaining windows
        for(int l = j + 1; j < n; ++j)
        {
            c += a[l][i];
            c -= p;
            p = a[l - k + 1][i];
            q.Add(c);

            if (c > max)
            {
                max = c;
            }
        }
        b.Add(q);
    }
    return max;
}

// Driver code
static public void Main()
{
    List<List<int>> mat = new List<List<int>>();
    mat.Add(new List<int>(){1, 0, 1});
    mat.Add(new List<int>(){1, 1, 0});
    mat.Add(new List<int>(){0, 1, 0});
    int k = 3;

    // Function call
    Console.WriteLine(maxCount(mat, k));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// maximum count of 1's in
// submatrix of order K

// Function to find the maximum
// count of 1's in the
// submatrix of order K
function maxCount(mat,k)
{
    let n = mat.length;
    let m = mat[0].length;
    let a = [];

    // Loop to find the count of 1's
    // in every possible windows
    // of rows of matrix
    for(let e = 0; e < n; ++e)
    {
        let s = mat[e];
        let q = [];
        let c = 0;

        // Loop to find the count of
        // 1's in the first window
        let i;
        for(i = 0; i < k; ++i)
        {
            if (s[i] == 1)
            {
                c += 1;
            }
        }
        q.push(c);
        let p = s[0];

        // Loop to find the count of
        // 1's in the remaining windows
        for(let j = i + 1; j < m; ++j)
        {
            if (s[j] == 1)
            {
                c += 1;
            }
            if (p == 1)
            {
                c -= 1;
            }
            q.push(c);
            p = s[j - k + 1];
        }
        a.push(q);
    }

    let b = [];
    let max = 0;

    // Loop to find the count of 1's
    // in every possible submatrix
    for(let i = 0; i < a[0].length; ++i)
    {
        let c = 0;
        let p = a[0][i];

        // Loop to find the count of
        // 1's in the first window
        let j;
        for(j = 0; j < k; ++j)
        {
            c += a[j][i];
        }
        let q = [];

        if (c > max)
        {
            max = c;
        }
        q.push(c);

        // Loop to find the count of
        // 1's in the remaining windows
        for(let l = j + 1; j < n; ++j)
        {

            c += a[l][i];
            c -= p;
            p = a[l - k + 1][i];
            q.push(c);

            if (c > max)
            {
                max = c;
            }
        }
        b.push(q);
    }
    return max;
}

// Driver code
let mat=[[1, 0, 1],[1, 1, 0],[0, 1, 0]];
let k = 3;

// Function call
document.write(maxCount(mat, k));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
5
```

**性能分析:**

*   **时间复杂度:**和上面的方法一样，有两个需要 O(N*M)时间的循环，因此时间复杂度为 **O(N*M)** 。
*   **空间复杂度:**和上面的方法一样，使用了额外的空间，因此空间复杂度为 **O(N)** 。

**方法 2:【动态规划方法】**在该技术中，我们使用给定的 **mat[][]** 数组计算 **dp[][]** 矩阵。在 **dp[][]** 数组中，我们使用先前的 **dp[][]** 值计算直到索引 **(i，j)** 的 1 的个数，并将其存储在 **dp[i][j]** 中。

**算法:**

```
1) Construct a dp[][] matrix and assign all elements to 0

    initial dp[0][0] = mat[0][0]

    a) compute first row and column of the dp matrix:

        i) for first row:

            dp[0][i] = dp[0][i-1] + mat[0][i]

        ii) for first column:

            dp[i][0] = dp[i-1][0] + mat[i][0]

    b) now compute remaining dp matrix from (1,1) to (n,m):

        dp[i][j] = mat[i][j] + dp[i-1][j] + dp[i][j-1] - dp[i-1][j-1]

2)now, we find the maximum 1's in k X k sub matrix:

    a) initially we assign max = dp[k-1][k-1]

    b) now first we have to check maximum for k-1 row and k-1 column:

        i) for k-1 row:

            if dp[k-1][j] - dp[k-1][j-k] > max:

                max = dp[k-1][j] - dp[k-1][j-k]

        ii) for k-1 column:

            if dp[i][k-1] - dp[i-k][k-1] > max:

                max = dp[i][k-1] - dp[i-k][k-1]

    c) now, we check max for (k to n) row and (k to m) column:

        for i from k to n-1:

            for j from k to m-1:

                if dp[i][j] + dp[i-k][j-k] - dp[i-k][j] - dp[i][j-k] > max:

                    max = dp[i][j] + dp[i-k][j-k] - dp[i-k][j] - dp[i][j-k]

 now just return the max value.
```

下面是上述方法的实现:

## C++14

```
// C++14 approach
#include <bits/stdc++.h>
using namespace std;

int findMaxK(vector<vector<int>> dp,
             int k, int n, int m)
{

    // Assign first kXk matrix initial
    // value as max
    int max_ = dp[k - 1][k - 1];

    for(int i = k; i < n; i++)
    {
        int su = dp[i - k][k - 1];
            if (max_ < su)
                max_ = su;
    }
    for(int j = k; j < m; j++)
    {
        int su = dp[k - 1][j - k];
            if (max_< su)
                max_ = su;
    }
    for(int i = k; i < n; i++)
    {
        for(int j = k; j < m; j++)
        {
            int su = dp[i][j] +
                     dp[i - k][j - k] -
                     dp[i - k][j] -
                     dp[i][j - k];

            if( max_ < su)
                max_ = su;
        }
    }
    return max_;
}

vector<vector<int>> buildDPdp(vector<vector<int>> mat,
                              int k, int n, int m)
{

    // Assign mXn dp list to 0
    vector<vector<int>> dp(n, vector<int>(m, 0));

    // Assign initial starting value
    dp[0][0] = mat[0][0];

    for(int i = 1; i < m; i++)
        dp[0][i] += (dp[0][i - 1] + mat[0][i]);

    for(int i = 1; i < n; i++)
        dp[i][0] += (dp[i - 1][0] + mat[i][0]);

    for(int i = 1; i < n; i++)
        for(int j = 1; j < m; j++)
            dp[i][j] = dp[i - 1][j] +
                       dp[i][j - 1] +
                       mat[i][j] -
                       dp[i - 1][j - 1];

    return dp;
}

int maxOneInK(vector<vector<int>> mat, int k)
{

    // n is columns
    int n = mat.size();

    // m is rows
    int m = mat[0].size();

    // Build dp list
    vector<vector<int>> dp = buildDPdp(
        mat, k, n, m);

    // Call the function and return its value
    return findMaxK(dp, k, n, m);
}

// Driver Code
int main()
{

    // mXn matrix
    vector<vector<int>> mat = { { 1, 0, 1 },
                                { 1, 1, 0 },
                                { 0, 1, 0 } };

    int k = 3;

    // Calling function
    cout << maxOneInK(mat, k);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {

    static int findMaxK(int[][] dp,
                     int k, int n, int m)
    {

        // Assign first kXk matrix initial
        // value as max
        int max_ = dp[k - 1][k - 1];

        for(int i = k; i < n; i++)
        {
            int su = dp[i - k][k - 1];
                if (max_ < su)
                    max_ = su;
        }
        for(int j = k; j < m; j++)
        {
            int su = dp[k - 1][j - k];
                if (max_< su)
                    max_ = su;
        }
        for(int i = k; i < n; i++)
        {
            for(int j = k; j < m; j++)
            {
                int su = dp[i][j] +
                         dp[i - k][j - k] -
                         dp[i - k][j] -
                         dp[i][j - k];

                if( max_ < su)
                    max_ = su;
            }
        }
        return max_;
    }

    static int[][] buildDPdp(int[][] mat,
                              int k, int n, int m)
    {

        // Assign mXn dp list to 0
        int[][] dp=new int[n][m];

        // Assign initial starting value
        dp[0][0] = mat[0][0];

        for(int i = 1; i < m; i++)
            dp[0][i] += (dp[0][i - 1] + mat[0][i]);

        for(int i = 1; i < n; i++)
            dp[i][0] += (dp[i - 1][0] + mat[i][0]);

        for(int i = 1; i < n; i++)
            for(int j = 1; j < m; j++)
                dp[i][j] = dp[i - 1][j] +
                           dp[i][j - 1] +
                           mat[i][j] -
                           dp[i - 1][j - 1];

        return dp;
    }

    static int maxOneInK(int[][] mat, int k)
    {

        // n is columns
        int n = mat.length;

        // m is rows
        int m = mat[0].length;

        // Build dp list
        int[][] dp = buildDPdp(
            mat, k, n, m);

        // Call the function and return its value
        return findMaxK(dp, k, n, m);
    }

  // Driver code
    public static void main (String[] args)
    {

        // mXn matrix
        int[][] mat = { { 1, 0, 1 },
                                    { 1, 1, 0 },
                                    { 0, 1, 0 } };

        int k = 3;

        // Calling function
        System.out.println( maxOneInK(mat, k));

    }
}

// This code is contributed by ab2127.
```

## 蟒蛇 3

```
#python3 approach

def findMaxK(dp,k,n,m):

    # assign first kXk matrix initial value as max
    max_ = dp[k-1][k-1]

    for i in range(k,n):
        su = dp[i-k][k-1]
        if max_ < su:
            max_ = su

    for j in range(k,m):
        su = dp[k-1][i-k]
        if max_< su:
            max_ = su

    for i in range(k,n):
        for j in range(k,m):
            su = dp[i][j] + dp[i-k][j-k] - dp[i-k][j] - dp[i][j-k]
            if max_ < su:
                max_ = su

    return max_

def buildDPdp(mat,k,n,m):

    # assign mXn dp list to 0
    dp = [[0 for i in range(m)] for j in range(n)]

    # assign initial starting value
    dp[0][0] = mat[0][0]

    for i in range(1,m):
        dp[0][i] += (dp[0][i-1]+mat[0][i])

    for i in range(1,n):
        dp[i][0] += (dp[i-1][0]+mat[i][0])

    for i in range(1,n):
        for j in range(1,m):
            dp[i][j] = dp[i-1][j] + dp[i][j-1] + mat[i][j] - dp[i-1][j-1]

    return dp

def maxOneInK(mat,k):

    # n is columns
    n = len(mat)

    # m is rows
    m = len(mat[0])

    #build dp list
    dp = buildDPdp(mat,k,n,m)

    # call the function and return its value
    return findMaxK(dp,k,n,m)

def main():
    # mXn matrix
    mat = [[1, 0, 1], [1, 1, 0], [0, 1, 0]]

    k = 3

    #callind function
    print(maxOneInK(mat,k))

#driver code
main()

#This code is contributed by Tokir Manva
```

## java 描述语言

```
<script>
// Javascript approach
function findMaxK(dp, k, n, m)
{

    // Assign first kXk matrix initial
    // value as max
    let max_ = dp[k - 1][k - 1];

    for(let i = k; i < n; i++)
    {
        let su = dp[i - k][k - 1];
            if (max_ < su)
                max_ = su;
    }
    for(let j = k; j < m; j++)
    {
        let su = dp[k - 1][j - k];
            if (max_< su)
                max_ = su;
    }
    for(let i = k; i < n; i++)
    {
        for(let j = k; j < m; j++)
        {
            let su = dp[i][j] +
                     dp[i - k][j - k] -
                     dp[i - k][j] -
                     dp[i][j - k];

            if( max_ < su)
                max_ = su;
        }
    }
    return max_;
}

function buildDPdp( mat,k,n,m)
{
    // Assign mXn dp list to 0
    let dp=new Array(n);
    for(let i=0;i<n;i++)
    {
        dp[i]=new Array(m);
        for(let j=0;j<m;j++)
        {
            dp[i][j]=0;
        }
    }

    // Assign initial starting value
    dp[0][0] = mat[0][0];

    for(let i = 1; i < m; i++)
        dp[0][i] += (dp[0][i - 1] + mat[0][i]);

    for(let i = 1; i < n; i++)
        dp[i][0] += (dp[i - 1][0] + mat[i][0]);

    for(let i = 1; i < n; i++)
        for(let j = 1; j < m; j++)
            dp[i][j] = dp[i - 1][j] +
                       dp[i][j - 1] +
                       mat[i][j] -
                       dp[i - 1][j - 1];

    return dp;
}

function maxOneInK(mat,k)
{
    // n is columns
    let n = mat.length;

    // m is rows
    let m = mat[0].length;

    // Build dp list
    let dp = buildDPdp(
        mat, k, n, m);

    // Call the function and return its value
    return findMaxK(dp, k, n, m);
}

// Driver Code

// mXn matrix
let mat = [[ 1, 0, 1 ],[ 1, 1, 0 ],
                                [ 0, 1, 0 ]];

    let k = 3;

    // Calling function
    document.write(maxOneInK(mat, k));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
5
```

**性能分析:**

*   **时间复杂度:**和上面的动态规划方法一样，我们必须计算**N×M**DP 矩阵，该矩阵需要 O(N*M)个时间，因此时间复杂度为 **O(N*M)** 。
*   **空间复杂度:**和上面的方法一样，有额外的空间用于制作 dp **N X M** 矩阵，因此空间复杂度为 **O(N*M)** 。
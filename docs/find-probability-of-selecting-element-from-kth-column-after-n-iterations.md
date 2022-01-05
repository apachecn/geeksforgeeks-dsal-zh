# 求 N 次迭代后从第 kth 列选择元素的概率

> 原文:[https://www . geeksforgeeks . org/find-n 次迭代后从第 k 列中选择元素的概率/](https://www.geeksforgeeks.org/find-probability-of-selecting-element-from-kth-column-after-n-iterations/)

给定 N*M 阶的矩阵 M，其中 **Mij** 表示行 I 中 j 的出现。任务是在应用给定操作后，找出最后一行中给定 k 的出现概率:

*   从第一行开始，我们从整行的任何一列中选择一个元素，并将其添加到下一行的同一列中。我们一直重复到最后一排。

**例:**

```
Input: k = 1, M[][] = 
{{0, 1},
{1, 1}}   

Output:0.666667

Input: k = 1, M[][] = 
{{0, 1},
{1, 1}}  

Output: 0.333333
```

**进场:**

*   预先计算存储第一行所有元素总和的 sum[]数组。
*   用第一行的 M[][]元素填充 dp[][]的第一行。
*   计算从特定行的每一列中选择一个元素并将其添加到相应列中的概率。
*   另外，在更新 dp[][]矩阵的值时，更新行的 Sum[]。
*   最后，给定 k 的 dp[n][k]的值是在所有迭代之后选择元素 k 的概率所需的值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#define n 4
#define m 4
using namespace std;

// Function to calculate probability
float calcProbability(int M[][m], int k)
{
    // declare dp[][] and sum[]
    float dp[m][n], sum[n];

    // precalculate the first row
    for (int j = 0; j < n; j++) {
        dp[0][j] = M[0][j];
        sum[0] += dp[0][j];
    }

    // calculate the probability for
    // each element and update dp table
    for (int i = 1; i < m; i++) {
        for (int j = 0; j < n; j++) {
            dp[i][j] += dp[i - 1][j] / sum[i - 1] + M[i][j];
            sum[i] += dp[i][j];
        }
    }

    // return result
    return dp[n - 1][k - 1] / sum[n - 1];
}

// Driver code
int main()
{

    int M[m][n] = { { 1, 1, 0, 3 },
                    { 2, 3, 2, 3 },
                    { 9, 3, 0, 2 },
                    { 2, 3, 2, 2 } };
    int k = 3;

    cout << calcProbability(M, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{
    final static int n = 4 ;
    final static int m = 4 ;

    // Function to calculate probability
    static float calcProbability(int M[][], int k)
    {
        // declare dp[][] and sum[]
        float dp[][] = new float[m][n] ;
        float sum[] = new float[n];

        // precalculate the first row
        for (int j = 0; j < n; j++)
        {
            dp[0][j] = M[0][j];
            sum[0] = sum[0] + dp[0][j];
        }

        // calculate the probability for
        // each element and update dp table
        for (int i = 1; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                dp[i][j] += dp[i - 1][j] / sum[i - 1] +
                            M[i][j];
                sum[i] += dp[i][j];
            }
        }

        // return result
        return dp[n - 1][k - 1] / sum[n - 1];
    }

    // Driver code
    public static void main(String []args)
    {
        int M[][] = { { 1, 1, 0, 3 },
                      { 2, 3, 2, 3 },
                      { 9, 3, 0, 2 },
                      { 2, 3, 2, 2 } };
        int k = 3;
        System.out.println(calcProbability(M, k));

    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

n = 4
m = 4

# Function to calculate probability
def calcProbability(M, k):

    # declare dp[][] and sum[]
    dp = [[0 for i in range(n)]
             for i in range(m)]
    Sum = [0 for i in range(n)]

    # precalculate the first row
    for j in range(n):
        dp[0][j] = M[0][j]
        Sum[0] += dp[0][j]

    # calculate the probability for
    # each element and update dp table
    for i in range(1, m):
        for j in range(n):
            dp[i][j] += (dp[i - 1][j] /
                         Sum[i - 1] + M[i][j])
            Sum[i] += dp[i][j]

    # return result
    return dp[n - 1][k - 1] / Sum[n - 1]

# Driver code

M = [[ 1, 1, 0, 3 ],
     [ 2, 3, 2, 3 ],
     [ 9, 3, 0, 2 ],
     [ 2, 3, 2, 2 ]]
k = 3

print(calcProbability(M, k))

# This code is contributed
# by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static int n = 4 ;
    static int m = 4 ;

    // Function to calculate probability
    static float calcProbability(int[,] M, int k)
    {
        // declare dp[][] and sum[]
        float[,] dp = new float[m,n] ;
        float[] sum = new float[n];

        // precalculate the first row
        for (int j = 0; j < n; j++)
        {
            dp[0, j] = M[0, j];
            sum[0] = sum[0] + dp[0, j];
        }

        // calculate the probability for
        // each element and update dp table
        for (int i = 1; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                dp[i, j] += dp[i - 1,j] / sum[i - 1] +
                            M[i, j];
                sum[i] += dp[i, j];
            }
        }

        // return result
        return dp[n - 1,k - 1] / sum[n - 1];
    }

    // Driver code
    public static void Main()
    {
        int[,] M = { { 1, 1, 0, 3 },
                    { 2, 3, 2, 3 },
                    { 9, 3, 0, 2 },
                    { 2, 3, 2, 2 } };
        int k = 3;
        Console.Write(calcProbability(M, k));
    }
}

// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to calculate probability
function calcProbability($M, $k)
{
    $m = 4; $n = 4;

    // declare dp[][] and sum[]
    $dp = array();
    $sum = array();

    // precalculate the first row
    for ($j = 0; $j < $n; $j++)
    {
        $dp[0][$j] = $M[0][$j];
        $sum[0] += $dp[0][$j];
    }

    // calculate the probability for
    // each element and update dp table
    for ($i = 1; $i < $m; $i++)
    {
        for ($j = 0; $j <$n; $j++)
        {
            $dp[$i][$j] += $dp[$i - 1][$j] /
                           $sum[$i - 1] + $M[$i][$j];
            $sum[$i] += $dp[$i][$j];
        }
    }

    // return result
    return $dp[$n - 1][$k - 1] / $sum[$n - 1];
}

// Driver code
$M = array(array(1, 1, 0, 3),
           array(2, 3, 2, 3),
           array(9, 3, 0, 2),
           array(2, 3, 2, 2));
$k = 3;

echo calcProbability($M, $k);

// This code is contributed
// by Arnub Kundu
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

    let n = 4 ;
    let m = 4 ;

    // Function to calculate probability
    function calcProbability(M,k)
    {
        // declare dp[][] and sum[]
        let dp = new Array(m) ;
        let sum = new Array(n);
          for(let i = 0; i < dp.length; i++)
        {
            dp[i] = new Array(n);
            for(let j = 0; j < n; j++)
            {
                dp[i][j] = 0;
            }
        }

        for(let i = 0; i < n; i++)
        {
            sum[i] = 0;
        }

        // precalculate the first row
        for (let j = 0; j < n; j++)
        {
            dp[0][j] = M[0][j];
            sum[0] = sum[0] + dp[0][j];
        }

        // calculate the probability for
        // each element and update dp table
        for (let i = 1; i < m; i++)
        {
            for (let j = 0; j < n; j++)
            {
                dp[i][j] += dp[i - 1][j] / sum[i - 1] +
                            M[i][j];
                sum[i] += dp[i][j];
            }
        }

        // return result
        return dp[n - 1][k - 1] / sum[n - 1];
    }

    // Driver code
    let M = [[ 1, 1, 0, 3 ],
     [ 2, 3, 2, 3 ],
     [ 9, 3, 0, 2 ],
     [ 2, 3, 2, 2 ]];

    let k = 3;
    document.write(calcProbability(M, k));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
0.201212
```
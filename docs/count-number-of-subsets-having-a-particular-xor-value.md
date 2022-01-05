# 计数具有特定异或值的子集数量

> 原文:[https://www . geesforgeks . org/count-subset-number-having-a-special-xor-value/](https://www.geeksforgeeks.org/count-number-of-subsets-having-a-particular-xor-value/)

给定一个由 n 个数字和一个数字 K 组成的数组 arr[]，求元素异或为 K 的 arr[]的子集数
**示例:**

```
Input:   arr[]  = {6, 9, 4,2}, k = 6
Output:  2
The subsets are {4, 2} and {6}

Input:   arr[]  = {1, 2, 3, 4, 5}, k = 4
Output:  4
The subsets are {1, 5}, {4}, {1, 2, 3, 4}
                and {2, 3, 5}
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/subsets-with-xor-value2023/1)

**蛮力方法 O(2 <sup>n</sup> ):** 一种天真的方法是生成所有的 2 <sup>n</sup> 个子集，并对具有异或值 K 的所有子集进行计数，但是这种方法对于大的 n 值无效

**动态规划方法 O(n*m):**
我们定义一个数 m，使得 m =幂(2，(log2(max(arr))+1))–1。这个数字实际上是任何异或子集将获得的最大值。我们通过计算最大数的位数得到这个数。我们创建一个 2D 数组 dp[n+1][m+1]，使得 **dp[i][j]等于来自 arr[0…i-1]** 的子集的具有异或值 j 的子集的数量。

我们按如下方式填充 dp 阵列:

1.  我们将 dp[i][j]的所有值初始化为 0。
2.  dp[0][0]的设定值= 1，因为空集合的异或为 0。
3.  从左到右迭代 arr[i]的所有值，对于每个 arr[i]，迭代 XOR 的所有可能值，即从 0 到 m(包括 0 和 m)并填充 dp 数组如下:
    对于 i = 1 到 n:
    对于 j = 0 到 m:
    DP[I][j]= DP[I-1][j]+DP[I -1][j^arr[i-1]]
    这可以解释为，如果存在具有 XOR 值 j 的子集 arr[0…i -2],则还存在子集 arri-2]具有 XOR 值 j^arr[i]那么显然存在具有 XOR 值 j 子集 arr[0…i-1],如 j ^ arr[i-1] ^ arr[i-1] = j。
4.  计算具有异或值 k 的子集的数量:因为 dp[i][j]是从 arr[0]的子集中具有 j 作为异或值的子集的数量..i-1]，则集合 arr[0]中的子集数..将异或值作为 K 将是 dp[n][K]

## C++

```
// arr dynamic programming solution to finding the number
// of subsets having xor of their elements as k
#include<bits/stdc++.h>
using namespace std;

// Returns count of subsets of arr[] with XOR value equals
// to k.
int subsetXOR(int arr[], int n, int k)
{
    // Find maximum element in arr[]
    int max_ele = arr[0];
    for (int i=1; i<n; i++)
       if (arr[i] > max_ele)
           max_ele = arr[i];

    // Maximum possible XOR value
    int m = (1 << (int)(log2(max_ele) + 1) ) - 1;
    if( k > m  )
       return 0;
    // The value of dp[i][j] is the number of subsets having
    // XOR of their elements as j from the set arr[0...i-1]
    int dp[n+1][m+1];

    // Initializing all the values of dp[i][j] as 0
    for (int i=0; i<=n; i++)
        for (int j=0; j<=m; j++)
            dp[i][j] = 0;

    // The xor of empty subset is 0
    dp[0][0] = 1;

    // Fill the dp table
    for (int i=1; i<=n; i++)
        for (int j=0; j<=m; j++)
            dp[i][j] = dp[i-1][j] + dp[i-1][j^arr[i-1]];

    //  The answer is the number of subset from set
    //  arr[0..n-1] having XOR of elements as k
    return dp[n][k];
}

// Driver program to test above function
int main()
{
    int arr[] = {1, 2, 3, 4, 5};
    int k = 4;
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Count of subsets is " << subsetXOR(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java dynamic programming solution
// to finding the number of subsets
// having xor of their elements as k 
class GFG{

// Returns count of subsets of arr[] with 
// XOR value equals to k.
static int subsetXOR(int []arr, int n, int k)
{

    // Find maximum element in arr[]
    int max_ele = arr[0];

    for(int i = 1; i < n; i++)
        if (arr[i] > max_ele)
            max_ele = arr[i];

    // Maximum possible XOR value
    int m = (1 << (int)(Math.log(max_ele) /
                        Math.log(2) + 1) ) - 1;
    if (k > m)
    {
       return 0;  
    }

    // The value of dp[i][j] is the number
    // of subsets having XOR of their
    // elements as j from the set arr[0...i-1]
    int [][]dp = new int[n + 1][m + 1];

    // Initializing all the values of dp[i][j] as 0
    for(int i = 0; i <= n; i++)
        for(int j = 0; j <= m; j++)
            dp[i][j] = 0;

    // The xor of empty subset is 0
    dp[0][0] = 1;

    // Fill the dp table
    for(int i = 1; i <= n; i++)
        for(int j = 0; j <= m; j++)
            dp[i][j] = dp[i - 1][j] +
                       dp[i - 1][j ^ arr[i - 1]];

    // The answer is the number of
    // subset from set arr[0..n-1]
    // having XOR of elements as k
    return dp[n][k];
}

// Driver code
public static void main(String arg[])
{
    int []arr = { 1, 2, 3, 4, 5 };
    int k = 4;
    int n = arr.length;

    System.out.println("Count of subsets is " +
                        subsetXOR(arr, n, k));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python 3 arr dynamic programming solution
# to finding the number of subsets having
# xor of their elements as k
import math

# Returns count of subsets of arr[] with
# XOR value equals to k.
def subsetXOR(arr, n, k):

    # Find maximum element in arr[]
    max_ele = arr[0]
    for i in range(1, n):
        if arr[i] > max_ele :
            max_ele = arr[i]

    # Maximum possible XOR value
    m = (1 << (int)(math.log2(max_ele) + 1)) - 1
    if( k > m  ):
       return 0

    # The value of dp[i][j] is the number
    # of subsets having XOR of their elements
    # as j from the set arr[0...i-1]

    # Initializing all the values
    # of dp[i][j] as 0
    dp = [[0 for i in range(m + 1)]
             for i in range(n + 1)]

    # The xor of empty subset is 0
    dp[0][0] = 1

    # Fill the dp table
    for i in range(1, n + 1):
        for j in range(m + 1):
            dp[i][j] = (dp[i - 1][j] +
                        dp[i - 1][j ^ arr[i - 1]])

    # The answer is the number of subset
    # from set arr[0..n-1] having XOR of
    # elements as k
    return dp[n][k]

# Driver Code
arr = [1, 2, 3, 4, 5]
k = 4
n = len(arr)
print("Count of subsets is",
       subsetXOR(arr, n, k))

# This code is contributed
# by sahishelangia
```

## C#

```
// C# dynamic programming solution to finding the number
// of subsets having xor of their elements as k
using System;

class GFG
{

// Returns count of subsets of arr[] with
// XOR value equals to k.
static int subsetXOR(int []arr, int n, int k)
{
    // Find maximum element in arr[]
    int max_ele = arr[0];
    for (int i = 1; i < n; i++)
    if (arr[i] > max_ele)
        max_ele = arr[i];

    // Maximum possible XOR value
    int m = (1 << (int)(Math.Log(max_ele,2) + 1) ) - 1;
    if( k > m  ){
       return 0; 
    }
    // The value of dp[i][j] is the number of subsets having
    // XOR of their elements as j from the set arr[0...i-1]
    int [,]dp=new int[n+1,m+1];

    // Initializing all the values of dp[i][j] as 0
    for (int i = 0; i <= n; i++)
        for (int j = 0; j <= m; j++)
            dp[i, j] = 0;

    // The xor of empty subset is 0
    dp[0, 0] = 1;

    // Fill the dp table
    for (int i = 1; i <= n; i++)
        for (int j = 0; j <= m; j++)
            dp[i, j] = dp[i-1, j] + dp[i-1, j^arr[i-1]];

    // The answer is the number of subset from set
    // arr[0..n-1] having XOR of elements as k
    return dp[n, k];
}

    // Driver code
    static public void Main ()
    {
        int []arr = {1, 2, 3, 4, 5};
        int k = 4;
        int n = arr.Length;
        Console.WriteLine ("Count of subsets is " + subsetXOR(arr, n, k));
    }
}

// This code is contributed by jit_t.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP arr dynamic programming
// solution to finding the number
// of subsets having xor of their
// elements as k

// Returns count of subsets of
// arr[] with XOR value equals to k.
function subsetXOR($arr, $n, $k)
{
    // Find maximum element in arr[]
    $max_ele = $arr[0];
    for ($i = 1; $i < $n; $i++)
    if ($arr[$i] > $max_ele)
        $max_ele = $arr[$i];

    // Maximum possible XOR value
    $m = (1 << (int)(log($max_ele,
                    2) + 1) ) - 1;
    if( $k > $m  ){
       return 0;
    }
    // The value of dp[i][j] is the
    // number of subsets having
    // XOR of their elements as j
    // from the set arr[0...i-1]

    // Initializing all the
    // values of dp[i][j] as 0
    for ($i = 0; $i <= $n; $i++)
        for ($j = 0; $j <= $m; $j++)
            $dp[$i][$j] = 0;

    // The xor of empty subset is 0
    $dp[0][0] = 1;

    // Fill the dp table
    for ($i = 1; $i <= $n; $i++)
        for ( $j = 0; $j <= $m; $j++)
            $dp[$i][$j] = $dp[$i - 1][$j] +
                          $dp[$i - 1][$j ^
                          $arr[$i - 1]];

    // The answer is the number
    // of subset from set arr[0..n-1]
    // having XOR of elements as k
    return $dp[$n][$k];
}

// Driver Code
$arr = array (1, 2, 3, 4, 5);
$k = 4;
$n = sizeof($arr);
echo "Count of subsets is " ,
     subsetXOR($arr, $n, $k);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript dynamic programming solution
    // to finding the number of subsets
    // having xor of their elements as k

    // Returns count of subsets of arr[] with
    // XOR value equals to k.
    function subsetXOR(arr, n, k)
    {

        // Find maximum element in arr[]
        let max_ele = arr[0];

        for(let i = 1; i < n; i++)
            if (arr[i] > max_ele)
                max_ele = arr[i];

        // Maximum possible XOR value
        let m = (1 << parseInt(Math.log(max_ele) /
        Math.log(2) + 1, 10) ) - 1;
        if (k > m)
        {
           return 0; 
        }

        // The value of dp[i][j] is the number
        // of subsets having XOR of their
        // elements as j from the set arr[0...i-1]
        let dp = new Array(n + 1);

        // Initializing all the values of dp[i][j] as 0
        for(let i = 0; i <= n; i++)
        {
            dp[i] = new Array(m + 1);
            for(let j = 0; j <= m; j++)
            {
                dp[i][j] = 0;
            }
        }

        // The xor of empty subset is 0
        dp[0][0] = 1;

        // Fill the dp table
        for(let i = 1; i <= n; i++)
            for(let j = 0; j <= m; j++)
                dp[i][j] = dp[i - 1][j] +
                dp[i - 1][j ^ arr[i - 1]];

        // The answer is the number of
        // subset from set arr[0..n-1]
        // having XOR of elements as k
        return dp[n][k];
    }

    let arr = [ 1, 2, 3, 4, 5 ];
    let k = 4;
    let n = arr.length;

    document.write("Count of subsets is " + subsetXOR(arr, n, k));

</script>
```

**输出:**

```
Count of subsets is 4
```

***时间复杂度:** O(n * m)*

***辅助空间:** O(n * m)*

本文由**普拉内·潘迪**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息
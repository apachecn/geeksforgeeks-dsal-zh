# 计数具有特定异或值的有序子集的数量

> 原文:[https://www . geesforgeks . org/count-no-of-ordered-subset-having-a-special-xor-value/](https://www.geeksforgeeks.org/count-no-of-ordered-subsets-having-a-particular-xor-value/)

给定一个由 **n** 元素组成的数组 **arr[]** 和一个数 **K** ，求元素异或的 **arr[]** 有序子集的个数为 **K**
这是[这个](https://www.geeksforgeeks.org/count-number-of-subsets-having-a-particular-xor-value/)问题的修改版本。所以建议之前试试那个问题。
**举例:**

> **输入:** arr[] = {6，9，4，2}，k = 6
> **输出:** 2
> 子集为{4，2}、{2，4}和{6}
> **输入:** arr[] = {1，2，3}，k = 1
> **输出:** 4
> 子集为{1}、{2，3}和{3，2}

**朴素方法 O(2 <sup>n</sup> ):** 生成所有的 **2 <sup>n</sup>** 子集，并找到所有具有**异或值 K** 的子集，对于每个具有异或值 K 的子集，将该子集的排列数添加到答案中，因为我们需要有序子集，但是这种方法对于 n 的大值无效
**高效方法 O(n <sup>2</sup> * m):** 这种方法使用动态
唯一的修改是我们在解决方案中增加了一个状态。我们有两种状态，其中 **dp[i][j]** 存储了具有**异或值 j** 的**数组【0…I-1】**的子集数。现在，我们再添加一个状态 **k** ，即存储子集长度的第三维。
所以， **dp[i][j][k]** 将存储**数组【0…I-1】**中具有**异或值 j** 的长度 **k** 的子集数量。
现在我们可以看到，

![$ dp[i][j][k] = dp[i-1][j][k] + k*dp[i-1][a[i-1] XOR j][k-1] $   ](img/c70e3bc182032d7871da23dde2f1f3a0.png "Rendered by QuickLaTeX.com")

即 **dp[i][j][k]** 可以通过丢弃 **a[i]** 元素(其给出 dp[i-1][j][k]子集)并将其纳入给出 **dp[i-1][a[i] ^ j][k-1]** 子集的子集中(类似于子集和问题的思想)来找到。现在我们要在**k–1**长度子集中插入**a【I】**元素，可以用 **k** 的方式来解释 k 的因子
计算 **dp 数组**后，我们的答案将是
![$ \sum_{k=1}^{k=n} dp[n][K][k] $   ](img/7ec4bf0ae4c106183fa86b2dc6456ae3.png "Rendered by QuickLaTeX.com")
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Returns count of ordered subsets of arr[]
// with XOR value = K
int subsetXOR(int arr[], int n, int K)
{

    // Find maximum element in arr[]
    int max_ele = arr[0];
    for (int i = 1; i < n; i++)
        if (arr[i] > max_ele)
            max_ele = arr[i];

    // Maximum possible XOR value
    int m = (1 << (int)(log2(max_ele) + 1)) - 1;

    // The value of dp[i][j][k] is the number
    // of subsets of length k having XOR of their
    // elements as j from the set arr[0...i-1]
    int dp[n + 1][m + 1][n + 1];

    // Initializing all the values of dp[i][j][k]
    // as 0
    for (int i = 0; i <= n; i++)
        for (int j = 0; j <= m; j++)
            for (int k = 0; k <= n; k++)
                dp[i][j][k] = 0;

    // The xor of empty subset is 0
    for (int i = 0; i <= n; i++)
        dp[i][0][0] = 1;

    // Fill the dp table
    for (int i = 1; i <= n; i++) {
        for (int j = 0; j <= m; j++) {
            for (int k = 0; k <= n; k++) {
                dp[i][j][k] = dp[i - 1][j][k];
                if (k != 0) {
                    dp[i][j][k] += k * dp[i - 1][j ^
                                   arr[i - 1]][k - 1];
                }
            }
        }
    }

    // The answer is the number of subsets of all lengths
    // from set arr[0..n-1] having XOR of elements as k
    int ans = 0;
    for (int i = 1; i <= n; i++) {
        ans += dp[n][K][i];
    }
    return ans;
}

// Driver program to test above function
int main()
{
    int arr[] = { 1, 2, 3 };
    int k = 1;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << subsetXOR(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    // Returns count of ordered subsets of arr[]
    // with XOR value = K
    static int subsetXOR(int arr[], int n, int K)
    {

        // Find maximum element in arr[]
        int max_ele = arr[0];
        for (int i = 1; i < n; i++)
            if (arr[i] > max_ele)
                max_ele = arr[i];

        // Maximum possible XOR value
        int m = (1 << (int)(Math.log(max_ele) /
                        Math.log(2) + 1)) - 1;

        // The value of dp[i][j][k] is the number
        // of subsets of length k having XOR of their
        // elements as j from the set arr[0...i-1]
        int [][][] dp = new int[n + 1][m + 1][n + 1];

        // Initializing all the values of
        // dp[i][j][k] as 0
        for (int i = 0; i <= n; i++)
            for (int j = 0; j <= m; j++)
                for (int k = 0; k <= n; k++)
                    dp[i][j][k] = 0;

        // The xor of empty subset is 0
        for (int i = 0; i <= n; i++)
            dp[i][0][0] = 1;

        // Fill the dp table
        for (int i = 1; i <= n; i++)
        {
            for (int j = 0; j <= m; j++)
            {
                for (int k = 0; k <= n; k++)
                {
                    dp[i][j][k] = dp[i - 1][j][k];
                    if (k != 0)
                    {
                        dp[i][j][k] += k * dp[i - 1][j ^
                                    arr[i - 1]][k - 1];
                    }
                }
            }
        }

        // The answer is the number of subsets
        // of all lengths from set arr[0..n-1]
        // having XOR of elements as k
        int ans = 0;
        for (int i = 1; i <= n; i++)
        {
            ans += dp[n][K][i];
        }
        return ans;
    }

    // Driver code
    public static void main(String []args)
    {
        int arr[] = { 1, 2, 3 };
        int k = 1;
        int n = arr.length;
        System.out.println(subsetXOR(arr, n, k));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python 3implementation of the approach
from math import log2

# Returns count of ordered subsets of arr[]
# with XOR value = K
def subsetXOR(arr, n, K):

    # Find maximum element in arr[]
    max_ele = arr[0]
    for i in range(1, n):
        if (arr[i] > max_ele):
            max_ele = arr[i]

    # Maximum possible XOR value
    m = (1 << int(log2(max_ele) + 1)) - 1

    # The value of dp[i][j][k] is the number
    # of subsets of length k having XOR of their
    # elements as j from the set arr[0...i-1]
    dp = [[[0 for i in range(n + 1)]
              for j in range(m + 1)]
              for k in range(n + 1)]

    # Initializing all the values
    # of dp[i][j][k] as 0
    for i in range(n + 1):
        for j in range(m + 1):
            for k in range(n + 1):
                dp[i][j][k] = 0

    # The xor of empty subset is 0
    for i in range(n + 1):
        dp[i][0][0] = 1

    # Fill the dp table
    for i in range(1, n + 1):
        for j in range(m + 1):
            for k in range(n + 1):
                dp[i][j][k] = dp[i - 1][j][k]
                if (k != 0):
                    dp[i][j][k] += k * dp[i - 1][j ^ arr[i - 1]][k - 1]

    # The answer is the number of subsets of all lengths
    # from set arr[0..n-1] having XOR of elements as k
    ans = 0
    for i in range(1, n + 1):
        ans += dp[n][K][i]

    return ans

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3]
    k = 1
    n = len(arr)
    print(subsetXOR(arr, n, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Returns count of ordered subsets of arr[]
    // with XOR value = K
    static int subsetXOR(int []arr, int n, int K)
    {

        // Find maximum element in arr[]
        int max_ele = arr[0];
        for (int i = 1; i < n; i++)
            if (arr[i] > max_ele)
                max_ele = arr[i];

        // Maximum possible XOR value
        int m = (1 << (int)(Math.Log(max_ele) /
                        Math.Log(2) + 1)) - 1;

        // The value of dp[i][j][k] is the number
        // of subsets of length k having XOR of their
        // elements as j from the set arr[0...i-1]
        int [ , , ] dp = new int[n + 1 , m + 1 ,n + 1];

        // Initializing all the values of
        // dp[i][j][k] as 0
        for (int i = 0; i <= n; i++)
            for (int j = 0; j <= m; j++)
                for (int k = 0; k <= n; k++)
                    dp[i, j, k] = 0;

        // The xor of empty subset is 0
        for (int i = 0; i <= n; i++)
            dp[i, 0, 0] = 1;

        // Fill the dp table
        for (int i = 1; i <= n; i++)
        {
            for (int j = 0; j <= m; j++)
            {
                for (int k = 0; k <= n; k++)
                {
                    dp[i, j, k] = dp[i - 1, j, k];
                    if (k != 0) {
                        dp[i, j, k] += k * dp[i - 1, j ^
                                    arr[i - 1], k - 1];
                    }
                }
            }
        }

        // The answer is the number of subsets
        // of all lengths from set arr[0..n-1]
        // having XOR of elements as k
        int ans = 0;
        for (int i = 1; i <= n; i++)
        {
            ans += dp[n, K, i];
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 3 };
        int k = 1;
        int n = arr.Length;
        Console.WriteLine(subsetXOR(arr, n, k));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of above approach

// Returns count of ordered subsets
// of arr[] with XOR value = K
function subsetXOR($arr, $n, $K)
{

    // Find maximum element in arr[]
    $max_ele = $arr[0];
    for ($i = 1; $i < $n; $i++)
        if ($arr[$i] > $max_ele)
            $max_ele = $arr[$i];

    // Maximum possible XOR value
    $m = (1 << (floor(log($max_ele, 2))+ 1)) - 1;

    // The value of dp[i][j][k] is the number
    // of subsets of length k having XOR of their
    // elements as j from the set arr[0...i-1]
    $dp = array(array(array())) ;

    // Initializing all the values
    // of dp[i][j][k] as 0
    for ($i = 0; $i <= $n; $i++)
        for ($j = 0; $j <= $m; $j++)
            for ($k = 0; $k <= $n; $k++)
                $dp[$i][$j][$k] = 0;

    // The xor of empty subset is 0
    for ($i = 0; $i <= $n; $i++)
        $dp[$i][0][0] = 1;

    // Fill the dp table
    for ($i = 1; $i <= $n; $i++)
    {
        for ($j = 0; $j <= $m; $j++)
        {
            for ($k = 0; $k <= $n; $k++)
            {
                $dp[$i][$j][$k] = $dp[$i - 1][$j][$k];
                if ($k != 0)
                {
                    $dp[$i][$j][$k] += $k * $dp[$i - 1][$j ^
                                       $arr[$i - 1]][$k - 1];
                }
            }
        }
    }

    // The answer is the number of subsets
    // of all lengths from set arr[0..n-1]
    // having XOR of elements as k
    $ans = 0;
    for ($i = 1; $i <= $n; $i++)
    {
        $ans += $dp[$n][$K][$i];
    }
    return $ans;
}

// Driver Code
$arr = [ 1, 2, 3 ];
$k = 1;
$n = sizeof($arr);
echo subsetXOR($arr, $n, $k);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // JavaScript implementation of the approach

    // Returns count of ordered subsets of arr[]
    // with XOR value = K
    function subsetXOR(arr, n, K)
    {

        // Find maximum element in arr[]
        let max_ele = arr[0];
        for (let i = 1; i < n; i++)
            if (arr[i] > max_ele)
                max_ele = arr[i];

        // Maximum possible XOR value
        let m =
        (1 << parseInt(Math.log(max_ele) / Math.log(2) + 1, 10)) - 1;

        // The value of dp[i][j][k] is the number
        // of subsets of length k having XOR of their
        // elements as j from the set arr[0...i-1]
        let dp = new Array(n + 1);

        // Initializing all the values of
        // dp[i][j][k] as 0
        for (let i = 0; i <= n; i++)
        {
            dp[i] = new Array(m + 1);
            for (let j = 0; j <= m; j++)
            {
                dp[i][j] = new Array(n + 1);
                for (let k = 0; k <= n; k++)
                {
                    dp[i][j][k] = 0;
                }
            }
        }

        // The xor of empty subset is 0
        for (let i = 0; i <= n; i++)
            dp[i][0][0] = 1;

        // Fill the dp table
        for (let i = 1; i <= n; i++)
        {
            for (let j = 0; j <= m; j++)
            {
                for (let k = 0; k <= n; k++)
                {
                    dp[i][j][k] = dp[i - 1][j][k];
                    if (k != 0)
                    {
                        dp[i][j][k] += k * dp[i - 1][j ^
                                    arr[i - 1]][k - 1];
                    }
                }
            }
        }

        // The answer is the number of subsets
        // of all lengths from set arr[0..n-1]
        // having XOR of elements as k
        let ans = 0;
        for (let i = 1; i <= n; i++)
        {
            ans += dp[n][K][i];
        }
        return ans;
    }

    let arr = [ 1, 2, 3 ];
    let k = 1;
    let n = arr.length;
    document.write(subsetXOR(arr, n, k));

</script>
```

**Output:** 

```
3
```
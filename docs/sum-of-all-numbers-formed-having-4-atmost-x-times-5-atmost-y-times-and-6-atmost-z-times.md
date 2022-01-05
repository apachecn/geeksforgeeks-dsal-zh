# 形成的具有 4 个大气压 X 次、5 个大气压 Y 次和 6 个大气压 Z 次的所有数字的总和

> 原文:[https://www . geesforgeks . org/所有数字的总和-已形成-4-atmat-x-times-5-atmat-y-times-和-6-atmat-z-times/](https://www.geeksforgeeks.org/sum-of-all-numbers-formed-having-4-atmost-x-times-5-atmost-y-times-and-6-atmost-z-times/)

给定三个整数 **X** 、 **Y** 和 **Z** ，任务是在 mod 10^9+7.下求所有形成的最多有**4**x 次、 **5** 最多有 **Y** 次、 **6** 最多有 **Z** 次的数的和
**例:**

```
Input: X = 1, Y = 1, Z = 1 
Output: 3675
Explanation:
4 + 5 + 6 + 45 + 54 + 56 
+ 65 + 46 + 64 + 456 + 465 
+ 546 + 564 + 645 + 654 = 3675

Input: X = 4, Y = 5, Z = 6
Output: 129422134
```

**进场:**

*   由于这个问题具有 [**子问题重叠**](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/) 和 [**最优子结构**](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/) 的性质，因此 [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) 可以用来求解。
*   需要所有 **i < x，j < y，j < z** 的精确 **i 4s** ， **j 5s** 和 **k 6s** 的数字来获得所需的总和。
*   因此，DP 数组**exact num【I】【j】【k】**将存储具有精确的 **i 4s** 、 **j 5s** 和 **k 6s** 的数字的精确计数。
*   如果**exact num[I–1][j][k]**、**exact num[I][j–1][k]**和**exact num[I][j][k–1]**已经已知，那么可以观察到这些的和就是需要的答案，除非**exact num[I–1][j][k]**、**exact num[I][j–1][k]**或 **exactnum[i][j]的情况既然如此，就跳过它吧。**
*   **exactsum[i][j][k]** 以与
    相同的方式存储具有**I**4s、**j**5s 和**k**6s 的精确数字的和

```
exactsum[i][j][k] = 10 * (exactsum[i - 1][j][k] 
                        + exactsum[i][j - 1][k] 
                        + exactsum[i][j][k - 1]) 
                  + 4 * exactnum[i - 1][j][k] 
                  + 5 * exactnum[i][j - 1][k] 
                  + 6 * exactnum[i][j][k - 1] 
```

以下是上述方法的实现:

## C++

```
// C++ program to find sum of all numbers
// formed having 4 atmost X times, 5 atmost
// Y times and 6 atmost Z times
#include <bits/stdc++.h>
using namespace std;

const int N = 101;
const int mod = 1e9 + 7;

// exactsum[i][j][k] stores the sum of
// all the numbers having exact
// i 4's, j 5's and k 6's
int exactsum[N][N][N];

// exactnum[i][j][k] stores numbers
// of numbers having exact
// i 4's, j 5's and k 6's
int exactnum[N][N][N];

// Utility function to calculate the
// sum for x 4's, y 5's and z 6's
int getSum(int x, int y, int z)
{
    int ans = 0;
    exactnum[0][0][0] = 1;
    for (int i = 0; i <= x; ++i) {
        for (int j = 0; j <= y; ++j) {
            for (int k = 0; k <= z; ++k) {

                // Computing exactsum[i][j][k]
                // as explained above
                if (i > 0) {
                    exactsum[i][j][k]
                        += (exactsum[i - 1][j][k] * 10
                            + 4 * exactnum[i - 1][j][k])
                           % mod;
                    exactnum[i][j][k]
                        += exactnum[i - 1][j][k] % mod;
                }
                if (j > 0) {
                    exactsum[i][j][k]
                        += (exactsum[i][j - 1][k] * 10
                            + 5 * exactnum[i][j - 1][k])
                           % mod;
                    exactnum[i][j][k]
                        += exactnum[i][j - 1][k] % mod;
                }
                if (k > 0) {
                    exactsum[i][j][k]
                        += (exactsum[i][j][k - 1] * 10
                            + 6 * exactnum[i][j][k - 1])
                           % mod;
                    exactnum[i][j][k]
                        += exactnum[i][j][k - 1] % mod;
                }

                ans += exactsum[i][j][k] % mod;
                ans %= mod;
            }
        }
    }
    return ans;
}

// Driver code
int main()
{
    int x = 1, y = 1, z = 1;

    cout << (getSum(x, y, z) % mod);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all numbers
// formed having 4 atmost X times, 5 atmost
// Y times and 6 atmost Z times

class GFG
{

    static int N = 101;
    static int mod = (int)1e9 + 7;

    // exactsum[i][j][k] stores the sum of
    // all the numbers having exact
    // i 4's, j 5's and k 6's
    static int exactsum[][][] = new int[N][N][N];

    // exactnum[i][j][k] stores numbers
    // of numbers having exact
    // i 4's, j 5's and k 6's
    static int exactnum[][][] = new int[N][N][N];

    // Utility function to calculate the
    // sum for x 4's, y 5's and z 6's
    static int getSum(int x, int y, int z)
    {
        int ans = 0;
        exactnum[0][0][0] = 1;
        for (int i = 0; i <= x; ++i)
        {
            for (int j = 0; j <= y; ++j)
            {
                for (int k = 0; k <= z; ++k)
                {

                    // Computing exactsum[i][j][k]
                    // as explained above
                    if (i > 0)
                    {
                        exactsum[i][j][k]
                        += (exactsum[i - 1][j][k] * 10
                        + 4 * exactnum[i - 1][j][k]) % mod;

                        exactnum[i][j][k]
                        += exactnum[i - 1][j][k] % mod;
                    }
                    if (j > 0)
                    {
                        exactsum[i][j][k]
                        += (exactsum[i][j - 1][k] * 10
                        + 5 * exactnum[i][j - 1][k]) % mod;

                        exactnum[i][j][k]
                        += exactnum[i][j - 1][k] % mod;
                    }
                    if (k > 0)
                    {
                        exactsum[i][j][k]
                        += (exactsum[i][j][k - 1] * 10
                        + 6 * exactnum[i][j][k - 1]) % mod;

                        exactnum[i][j][k]
                        += exactnum[i][j][k - 1] % mod;
                    }

                    ans += exactsum[i][j][k] % mod;
                    ans %= mod;
                }
            }
        }
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int x = 1, y = 1, z = 1;

        System.out.println(getSum(x, y, z) % mod);

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find sum of all numbers
# formed having 4 atmost X times, 5 atmost
# Y times and 6 atmost Z times
import numpy as np

N = 101;
mod = int(1e9) + 7;

# exactsum[i][j][k] stores the sum of
# all the numbers having exact
# i 4's, j 5's and k 6's
exactsum = np.zeros((N, N, N));

# exactnum[i][j][k] stores numbers
# of numbers having exact
# i 4's, j 5's and k 6's
exactnum = np.zeros((N, N, N));

# Utility function to calculate the
# sum for x 4's, y 5's and z 6's
def getSum(x, y, z) :
    ans = 0;
    exactnum[0][0][0] = 1;
    for i in range(x + 1) :
        for j in range(y + 1) :
            for k in range(z + 1) :

                # Computing exactsum[i][j][k]
                # as explained above
                if (i > 0) :
                    exactsum[i][j][k] += (exactsum[i - 1][j][k] * 10 +
                                            4 * exactnum[i - 1][j][k]) % mod;

                    exactnum[i][j][k] += exactnum[i - 1][j][k] % mod;

                if (j > 0) :
                    exactsum[i][j][k] += (exactsum[i][j - 1][k] * 10+
                                        5 * exactnum[i][j - 1][k]) % mod;

                    exactnum[i][j][k] += exactnum[i][j - 1][k] % mod;

                if (k > 0) :
                    exactsum[i][j][k] += (exactsum[i][j][k - 1] * 10
                                            + 6 * exactnum[i][j][k - 1]) % mod;
                    exactnum[i][j][k] += exactnum[i][j][k - 1] % mod;

                ans += exactsum[i][j][k] % mod;
                ans %= mod;

    return ans;

# Driver code
if __name__ == "__main__" :

    x = 1; y = 1; z = 1;

    print((getSum(x, y, z) % mod));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find sum of all numbers
// formed having 4 atmost X times, 5 atmost
// Y times and 6 atmost Z times
using System;

class GFG
{

    static int N = 101;
    static int mod = (int)1e9 + 7;

    // exactsum[i][j][k] stores the sum of
    // all the numbers having exact
    // i 4's, j 5's and k 6's
    static int [,,]exactsum = new int[N, N, N];

    // exactnum[i][j][k] stores numbers
    // of numbers having exact
    // i 4's, j 5's and k 6's
    static int [,,]exactnum= new int[N, N, N];

    // Utility function to calculate the
    // sum for x 4's, y 5's and z 6's
    static int getSum(int x, int y, int z)
    {
        int ans = 0;
        exactnum[0, 0, 0] = 1;
        for (int i = 0; i <= x; ++i)
        {
            for (int j = 0; j <= y; ++j)
            {
                for (int k = 0; k <= z; ++k)
                {

                    // Computing exactsum[i, j, k]
                    // as explained above
                    if (i > 0)
                    {
                        exactsum[i, j, k]
                        += (exactsum[i - 1, j, k] * 10
                        + 4 * exactnum[i - 1, j, k]) % mod;

                        exactnum[i, j, k]
                        += exactnum[i - 1, j, k] % mod;
                    }
                    if (j > 0)
                    {
                        exactsum[i, j, k]
                        += (exactsum[i, j - 1, k] * 10
                        + 5 * exactnum[i, j - 1, k]) % mod;

                        exactnum[i, j, k]
                        += exactnum[i, j - 1, k] % mod;
                    }
                    if (k > 0)
                    {
                        exactsum[i, j, k]
                        += (exactsum[i, j, k - 1] * 10
                        + 6 * exactnum[i, j, k - 1]) % mod;

                        exactnum[i, j, k]
                        += exactnum[i, j, k - 1] % mod;
                    }

                    ans += exactsum[i, j, k] % mod;
                    ans %= mod;
                }
            }
        }
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int x = 1, y = 1, z = 1;

        Console.WriteLine(getSum(x, y, z) % mod);

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript program to find sum of all numbers
    // formed having 4 atmost X times, 5 atmost
    // Y times and 6 atmost Z times

    let N = 101;
    let mod = 1e9 + 7;

    // exactsum[i][j][k] stores the sum of
    // all the numbers having exact
    // i 4's, j 5's and k 6's
    let exactsum = new Array(N);

    // exactnum[i][j][k] stores numbers
    // of numbers having exact
    // i 4's, j 5's and k 6's
    let exactnum = new Array(N);

    for(let i = 0; i < N; i++)
    {
        exactsum[i] = new Array(N);
        exactnum[i] = new Array(N);
        for(let j = 0; j < N; j++)
        {
            exactsum[i][j] = new Array(N);
            exactnum[i][j] = new Array(N);
            for(let k = 0; k < N; k++)
            {
                exactsum[i][j][k] = 0;
                exactnum[i][j][k] = 0;
            }
        }
    }

    // Utility function to calculate the
    // sum for x 4's, y 5's and z 6's
    function getSum(x, y, z)
    {
        let ans = 0;
        exactnum[0][0][0] = 1;
        for (let i = 0; i <= x; ++i)
        {
            for (let j = 0; j <= y; ++j)
            {
                for (let k = 0; k <= z; ++k)
                {

                    // Computing exactsum[i][j][k]
                    // as explained above
                    if (i > 0)
                    {
                        exactsum[i][j][k]
                        += (exactsum[i - 1][j][k] * 10
                        + 4 * exactnum[i - 1][j][k]) % mod;

                        exactnum[i][j][k]
                        += exactnum[i - 1][j][k] % mod;
                    }
                    if (j > 0)
                    {
                        exactsum[i][j][k]
                        += (exactsum[i][j - 1][k] * 10
                        + 5 * exactnum[i][j - 1][k]) % mod;

                        exactnum[i][j][k]
                        += exactnum[i][j - 1][k] % mod;
                    }
                    if (k > 0)
                    {
                        exactsum[i][j][k]
                        += (exactsum[i][j][k - 1] * 10
                        + 6 * exactnum[i][j][k - 1]) % mod;

                        exactnum[i][j][k]
                        += exactnum[i][j][k - 1] % mod;
                    }

                    ans += exactsum[i][j][k] % mod;
                    ans %= mod;
                }
            }
        }
        return ans;
    }

    let x = 1, y = 1, z = 1;

    document.write(getSum(x, y, z) % mod);

</script>
```

**Output:** 

```
3675
```

**时间复杂度:** O(x*y*z)

**辅助空间:** O(N <sup>3</sup> )
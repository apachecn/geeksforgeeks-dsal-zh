# 将给定的球分成具有相同数量不同颜色的两半的概率

> 原文:[https://www . geeksforgeeks . org/将给定的球分成具有相同数量不同颜色的两半的概率/](https://www.geeksforgeeks.org/probability-of-distributing-given-balls-into-two-halves-having-equal-count-of-distinct-colors/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，代表每个 **N** 不同颜色的球的数量，任务是找到将所有球分配到两个盒子中的[概率，使得两个盒子包含相同数量的不同颜色的球。](https://www.geeksforgeeks.org/probability-of-distributing-m-items-among-x-bags-such-that-first-bag-contains-n-items/)

**示例:**

> **输入:** arr[] = {1，1}，N = 2
> **输出:** 1.00000
> **说明:**两种可能的分配方式如下:
> 将第 0 <sup>个</sup>色型的球放入第 1 个盒子，将第 1 个<sup>个</sup>色型的球放入第 2 个盒子。
> 将 1 <sup>st</sup> 型的颜色放在 1 <sup>st</sup> 框中，将 0 <sup>th</sup> 型的颜色放在第二个框中。
> 因此，概率等于(2 / 2) = 1.00000
> 
> **输入:** arr[] = {2，1，1}，N = 3
> T3】输出: 0.66667

**方法:**思路是用[组合学](https://www.geeksforgeeks.org/hard/combinatorial)和[回溯](https://www.geeksforgeeks.org/backtracking-introduction/)来解决问题。给定的问题可以基于以下观察来解决:

> *   Let **x** be the total number of ways to divide **k** balls into equal halves.
> *   It can be observed that **x** is the same as **k/2** ball selected from **k** balls, and is equal to **<sup>k</sup> c <sub>(k/2).</sub>**
> *   Select **j** ball from **arr [I]** and put it into a box every **0 ≤ I < n** and **j ≤ arr [I], which can be calculated by backtracking with [.](https://www.geeksforgeeks.org/backtracking-introduction/)**
> *   Therefore, the required probability is **y/X.**

按照以下步骤解决问题:

*   [计算数组中所有元素的总和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**arr【】**在一个变量中，比如 **K.**
*   如果 **K** 是奇数，打印 **0** 。
*   计算选择 **K/2** 球的方式数并存储在变量中，比如 **X** 。
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，说**有效排列(pos，usedBalls，box1，box2)** ，并执行以下步骤:
    *   定义基本情况:如果**使用的球**等于 **K/2** ，那么如果**盒 1 =盒 2** ，则返回 **1** 。否则，返回 **0** 。
    *   如果**位置≥ N** ，则返回 **0** 。
    *   现在，初始化一个变量，比如 **res** ，来存储剩余球的分配方式。
    *   迭代范围 **[0，arr[pos]]:**
        *   将**框 1** 和**框 2** 分配给变量，分别表示**新框 1** 和**新框 2** 。
        *   如果 **j > 0** 和**新箱 2** ，如果**j<arr【pos】**，则将**新箱 1** 增加 1。
        *   现在，更新 RESas**RES = RES+<sup>arr【pos】</sup>c<sub>j</sub>*验证交换(pos+1，usedballs+j，newbox1，newbox2)。**
    *   返回 **res** 的值。
*   调用函数**有效排列(0，0，0，0)** 并将其存储在变量中，比如 **Y.**
*   最后，将得到的结果打印为 **Y/X** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the count of
// distinct colors in box1
static int box1 = 0;

// Stores the count of
// distinct colors in box2
static int box2 = 0;

static int fact[11];

// Function to calculate NcR
long comb(int n, int r)
{
    long res = fact[n] / fact[r];
    res /= fact[n - r];
    return res;
}

// Function to calculate factorial of N
void factorial(int N)
{

    // Base Case
    fact[0] = 1;

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
        fact[i] = fact[i - 1] * i;
}

// Function to calculate total number
// of possible distributions which
// satisfies the given conditions
long validPermutations(int n, int balls[],
                       int usedBalls,
                       int i, int M)
{

    // If used balls is equal to K/2
    if (usedBalls == n)
    {

        // If box1 is equal to box2
        return box1 == box2 ? 1 : 0;
    }

    // Base condition
    if (i >= M)
        return 0;

    // Stores the number of ways of
    // distributing remaining balls without
    // including the current balls in box1
    long res = validPermutations(n, balls,
                                 usedBalls,
                                 i + 1, M);

    // Increment box1 by one
    box1++;

    // Iterate over the range [1, balls[i]]
    for(int j = 1; j <= balls[i]; j++)
    {

        // If all the balls goes to box1,
        // then decrease box2 by one
        if (j == balls[i])

            box2--;

        // Total number of ways of
        // selecting j balls
        long combinations = comb(balls[i], j);

        // Increment res by total number of valid
        // ways of distributing the remaining balls
        res += combinations * validPermutations(n, balls,
                                                usedBalls + j,
                                                i + 1, M);
    }

    // Decrement box1 by one
    box1--;

    // Increment box2 by 1
    box2++;

    return res;
}

// Function to calculate the required probability
double getProbability(int balls[], int M)
{

    // Calculate factorial from [1, 10]
    factorial(10);

    // Assign all distinct balls to second box
    box2 = M;

    // Total number of balls
    int K = 0;

    // Calculate total number of balls
    for(int i = 0; i < M; i++)
        K += balls[i];

    // If K is an odd number
    if (K % 2 == 1)
        return 0;

    // Total ways of distributing the balls
    // in two equal halves
    long all = comb(K, K / 2);

    // Required number of ways
    long validPermutation = validPermutations(K / 2, balls,
                                              0, 0, M);

    // Return the required probability
    return (double)validPermutation / all;
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 1 };
    int N = 4;
    int M = sizeof(arr) / sizeof(arr[0]);

    // Print the result
    cout << (getProbability(arr, M));

    return 0;
}

// This code is contributed by ukasp
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Stores the count of
    // distinct colors in box1
    static int box1 = 0;

    // Stores the count of
    // distinct colors in box2
    static int box2 = 0;

    static int[] fact = new int[11];

    // Function to calculate the required probability
    public static double getProbability(int[] balls)
    {

        // Calculate factorial from [1, 10]
        factorial(10);

        // Assign all distinct balls to second box
        box2 = balls.length;

        // Total number of balls
        int K = 0;

        // Calculate total number of balls
        for (int i = 0; i < balls.length; i++)
            K += balls[i];

        // If K is an odd number
        if (K % 2 == 1)
            return 0;

        // Total ways of distributing the balls
        // in two equal halves
        long all = comb(K, K / 2);

        // Required number of ways
        long validPermutations = validPermutations(K / 2, balls, 0, 0);

        // Return the required probability
        return (double)validPermutations / all;
    }

    // Function to calculate total number
    // of possible distributions which
    // satisfies the given conditions
    static long validPermutations(int n, int[] balls,
                          int usedBalls, int i)
    {

        // If used balls is equal to K/2
        if (usedBalls == n) {

            // If box1 is equal to box2
            return box1 == box2 ? 1 : 0;
        }

        // Base condition
        if (i >= balls.length)
            return 0;

        // Stores the number of ways of
        // distributing remaining balls without
        // including the current balls in box1
        long res = validPermutations(n, balls, usedBalls, i + 1);

        // Increment box1 by one
        box1++;

        // Iterate over the range [1, balls[i]]
        for (int j = 1; j <= balls[i]; j++) {

            // If all the balls goes to box1,
            // then decrease box2 by one
            if (j == balls[i])
                box2--;

            // Total number of ways of
            // selecting j balls
            long combinations = comb(balls[i], j);

            // Increment res by total number of valid
            // ways of distributing the remaining balls
            res += combinations * validPermutations(n, balls,
                                            usedBalls + j, i + 1);
        }

        // Decrement box1 by one
        box1--;

        // Increment box2 by 1
        box2++;

        return res;
    }

    // Function to calculate factorial of N
    static void factorial(int N)
    {

        // Base Case
        fact[0] = 1;

        // Iterate over the range [1, N]
        for (int i = 1; i <= N; i++)
            fact[i] = fact[i - 1] * i;
    }

    // Function to calculate NcR
    static long comb(int n, int r)
    {

        long res = fact[n] / fact[r];
        res /= fact[n - r];
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 2, 1, 1 };
        int N = 4;

        // Print the result
        System.out.println(getProbability(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the count of
# distinct colors in box1
box1 = 0

# Stores the count of
# distinct colors in box2
box2 = 0

fact = [0 for i in range(11)]

# Function to calculate the required probability
def getProbability(balls):

    global box1, box2, fact

    # Calculate factorial from [1, 10]
    factorial(10)

    # Assign all distinct balls to second box
    box2 = len(balls)

    # Total number of balls
    K = 0

    # Calculate total number of balls
    for i in range(len(balls)):
        K += balls[i]

    # If K is an odd number   
    if (K % 2 == 1):
        return 0

    # Total ways of distributing the balls
    # in two equal halves
    all = comb(K, K // 2)

    # Required number of ways
    validPermutation = validPermutations(
        K // 2, balls, 0, 0)

    # Return the required probability
    return validPermutation / all

# Function to calculate total number
# of possible distributions which
# satisfies the given conditions
def validPermutations(n, balls, usedBalls, i):

    global box1, box2, fact

    # If used balls is equal to K/2
    if (usedBalls == n):

        # If box1 is equal to box2
        if (box1 == box2):
            return 1
        else:
            return 0

    # Base condition
    if (i >= len(balls)):
        return 0

    # Stores the number of ways of
    # distributing remaining balls without
    # including the current balls in box1
    res = validPermutations(n, balls,
                            usedBalls, i + 1)

    # Increment box1 by one
    box1 += 1

    # Iterate over the range [1, balls[i]]
    for j in range(1, balls[i] + 1):

        # If all the balls goes to box1,
        # then decrease box2 by one
        if (j == balls[i]):
            box2 -= 1

        # Total number of ways of
        # selecting j balls
        combinations = comb(balls[i], j)

        # Increment res by total number of valid
        # ways of distributing the remaining balls
        res += combinations * validPermutations(n, balls,
                                                usedBalls + j,
                                                i + 1)

    # Decrement box1 by one
    box1 -= 1

    # Increment box2 by 1
    box2 += 1

    return res

# Function to calculate factorial of N
def factorial(N):

    global box1, box2, fact

    # Base Case
    fact[0] = 1

    # Iterate over the range [1, N]
    for i in range(1, N + 1):
        fact[i] = fact[i - 1] * i

# Function to calculate NcR   
def comb(n, r):

    global box1, box2, fact
    res = fact[n] // fact[r]
    res //= fact[n - r]
    return res

# Driver Code   
arr = [ 2, 1, 1 ]
N = 4

print(getProbability(arr))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

    // Stores the count of
    // distinct colors in box1
    static int box1 = 0;

    // Stores the count of
    // distinct colors in box2
    static int box2 = 0;
    static int[] fact = new int[11];

    // Function to calculate the required probability
    public static double getProbability(int[] balls)
    {

        // Calculate factorial from [1, 10]
        factorial(10);

        // Assign all distinct balls to second box
        box2 = balls.Length;

        // Total number of balls
        int K = 0;

        // Calculate total number of balls
        for (int i = 0; i < balls.Length; i++)
            K += balls[i];

        // If K is an odd number
        if (K % 2 == 1)
            return 0;

        // Total ways of distributing the balls
        // in two equal halves
        long all = comb(K, K / 2);

        // Required number of ways
        long validPermutationss = validPermutations((K / 2), balls, 0, 0);

        // Return the required probability
        return (double)validPermutationss / all;
    }

    // Function to calculate total number
    // of possible distributions which
    // satisfies the given conditions
    static long validPermutations(int n, int[] balls,
                          int usedBalls, int i)
    {

        // If used balls is equal to K/2
        if (usedBalls == n)
        {

            // If box1 is equal to box2
            return box1 == box2 ? 1 : 0;
        }

        // Base condition
        if (i >= balls.Length)
            return 0;

        // Stores the number of ways of
        // distributing remaining balls without
        // including the current balls in box1
        long res = validPermutations(n, balls, usedBalls, i + 1);

        // Increment box1 by one
        box1++;

        // Iterate over the range [1, balls[i]]
        for (int j = 1; j <= balls[i]; j++)
        {

            // If all the balls goes to box1,
            // then decrease box2 by one
            if (j == balls[i])
                box2--;

            // Total number of ways of
            // selecting j balls
            long combinations = comb(balls[i], j);

            // Increment res by total number of valid
            // ways of distributing the remaining balls
            res += combinations * validPermutations(n, balls,
                                            usedBalls + j, i + 1);
        }

        // Decrement box1 by one
        box1--;

        // Increment box2 by 1
        box2++;

        return res;
    }

    // Function to calculate factorial of N
    static void factorial(int N)
    {

        // Base Case
        fact[0] = 1;

        // Iterate over the range [1, N]
        for (int i = 1; i <= N; i++)
            fact[i] = fact[i - 1] * i;
    }

    // Function to calculate NcR
    static long comb(int n, int r)
    {

        long res = fact[n] / fact[r];
        res /= fact[n - r];
        return res;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 2, 1, 1 };
        int N = 4;

        // Print the result
        Console.WriteLine(getProbability(arr));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Stores the count of
// distinct colors in box1
var box1 = 0;

// Stores the count of
// distinct colors in box2
var box2 = 0;

var fact = Array(11);

// Function to calculate NcR
function comb(n, r)
{
    var res = fact[n] / fact[r];
    res /= fact[n - r];
    return res;
}

// Function to calculate factorial of N
function factorial(N)
{

    // Base Case
    fact[0] = 1;

    // Iterate over the range [1, N]
    for(var i = 1; i <= N; i++)
        fact[i] = fact[i - 1] * i;
}

// Function to calculate total number
// of possible distributions which
// satisfies the given conditions
function validPermutations(n, balls,usedBalls, i, M)
{

    // If used balls is equal to K/2
    if (usedBalls == n)
    {

        // If box1 is equal to box2
        return box1 == box2 ? 1 : 0;
    }

    // Base condition
    if (i >= M)
        return 0;

    // Stores the number of ways of
    // distributing remaining balls without
    // including the current balls in box1
    var res = validPermutations(n, balls,
                                 usedBalls,
                                 i + 1, M);

    // Increment box1 by one
    box1++;

    // Iterate over the range [1, balls[i]]
    for(var j = 1; j <= balls[i]; j++)
    {

        // If all the balls goes to box1,
        // then decrease box2 by one
        if (j == balls[i])

            box2--;

        // Total number of ways of
        // selecting j balls
        var combinations = comb(balls[i], j);

        // Increment res by total number of valid
        // ways of distributing the remaining balls
        res += combinations * validPermutations(n, balls,
                                                usedBalls + j,
                                                i + 1, M);
    }

    // Decrement box1 by one
    box1--;

    // Increment box2 by 1
    box2++;

    return res;
}

// Function to calculate the required probability
function getProbability(balls, M)
{

    // Calculate factorial from [1, 10]
    factorial(10);

    // Assign all distinct balls to second box
    box2 = M;

    // Total number of balls
    var K = 0;

    // Calculate total number of balls
    for(var i = 0; i < M; i++)
        K += balls[i];

    // If K is an odd number
    if (K % 2 == 1)
        return 0;

    // Total ways of distributing the balls
    // in two equal halves
    var all = comb(K, K / 2);

    // Required number of ways
    var validPermutation = validPermutations(K / 2, balls,
                                              0, 0, M);

    // Return the required probability
    return validPermutation / all;
}

// Driver Code
var arr = [2, 1, 1];
var N = 4;
var M = arr.length;
// Print the result
document.write(getProbability(arr, M));

</script>
```

**Output:** 

```
0.6666666666666666
```

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*
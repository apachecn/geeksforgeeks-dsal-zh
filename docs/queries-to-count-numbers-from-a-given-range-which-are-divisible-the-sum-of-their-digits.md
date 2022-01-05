# 查询给定范围内可被数字总和整除的数字的计数

> 原文:[https://www . geesforgeks . org/query-to-count-numbers-from-a-给定范围内可被其数字之和整除的数字/](https://www.geeksforgeeks.org/queries-to-count-numbers-from-a-given-range-which-are-divisible-the-sum-of-their-digits/)

给定一个由形式为 **{L，R}** 的 **N** 个查询组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **Q[][]** ，每个查询的任务是从范围**【L，R】**中找出可被其数字总和整除的数字的总数。

**示例:**

> **输入:** Q[][]= {{5，9}，{5，20}}
> **输出:**
> 5
> 9
> **说明:**
> 查询 1:范围[5，9]中可被其位数之和整除的数字为{5，6，7，8，9}。
> 查询 2:【5，20】范围内可被其数字之和整除的数字为{ *5，6，7，8，9，10，12，18，20}。*
> 
> **输入:** Q[][] = {{1，30}，{13，15}}
> **输出:**
> 17
> 0
> **解释:**
> 查询 1:范围[5，9]中可被其数字之和整除的数字为{ *1，2，3，4，5，6，7，8，9，10，12，18，20，21，24*
> 查询 2:在[13，15]范围内不存在这样的数字。

**方法:**使用[包含-排除原理](https://www.geeksforgeeks.org/inclusion-exclusion-various-applications/)和[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)数组技术可以解决这个问题。
按照以下步骤解决给定问题:

1.  初始化一个数组 **arr[]** 以在每个 i <sup>第</sup>个索引处存储可被其数字之和整除的最多 I 个数字的计数。
2.  使用一个变量迭代范围**【1，10】<sup>5</sup>**，比如说 **i** ，对于每一个**I**T8 元素，检查 **i** 是否可以被其位数的和整除。
    *   如果发现为真，设置 **arr[i] = 1** 。
    *   否则，设置 **arr[i] = 0** 。
3.  将数组 arr[]修改为其[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
4.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[][]** ，对于每个查询，从范围**【L，R】**计算所需数字的总数，该范围等于**arr[R]–arr[L–1]**。

下面是上述方法的实现:

## C++

```
// C++ program of the
// above approach
#include <bits/stdc++.h>
using namespace std;

int arr[100005];

// Function to check if the number x
// is divisible by its sum of digits
bool isDivisible(int x)
{
    // Stores sum of digits of x
    int sum = 0;

    // Temporarily store x
    int temp = x;

    // Calculate sum
    // of digits of x
    while (x != 0) {
        sum += x % 10;
        x /= 10;
    }

    // If x is not divisible by sum
    if (temp % sum)
        return false;

    // Otherwise
    else
        return true;
}

// Function to perform
// the precomputation
void precompute()
{
    // Iterate from i equals 1 to 1e5
    for (int i = 1; i <= 100000; i++) {
        // Check if i is divisible
        // by sum of its digits
        if (isDivisible(i))
            arr[i] = 1;
        else
            arr[i] = 0;
    }

    // Convert arr[] to prefix sum array
    for (int i = 1; i <= 100000; i++) {
        arr[i] = arr[i] + arr[i - 1];
    }
}

// Driver code
int main()
{
    // Given queries
    vector<pair<int, int> > Q = { { 5, 9 }, { 5, 20 } };

    precompute();

    for (auto it : Q) {
        // Using inclusion-exclusion
        // principle, calculate the result
        cout << arr[it.second] - arr[it.first - 1] << "\n";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    static int arr[] = new int[100005];

    // Function to check if the number x
    // is divisible by its sum of digits
    static boolean isDivisible(int x)
    {
        // Stores sum of digits of x
        int sum = 0;

        // Temporarily store x
        int temp = x;

        // Calculate sum
        // of digits of x
        while (x != 0) {
            sum += x % 10;
            x /= 10;
        }

        // If x is not divisible by sum
        if (temp % sum != 0)
            return false;

        // Otherwise
        else
            return true;
    }

    // Function to perform
    // the precomputation
    static void precompute()
    {

        // Iterate from i equals 1 to 1e5
        for (int i = 1; i <= 100000; i++) {

            // Check if i is divisible
            // by sum of its digits
            if (isDivisible(i))
                arr[i] = 1;
            else
                arr[i] = 0;
        }

        // Convert arr[] to prefix sum array
        for (int i = 1; i <= 100000; i++) {
            arr[i] = arr[i] + arr[i - 1];
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given queries
        int Q[][] = { { 5, 9 }, { 5, 20 } };

        precompute();

        for (int q[] : Q) {
            // Using inclusion-exclusion
            // principle, calculate the result
            System.out.println(arr[q[1]] - arr[q[0] - 1]);
        }
    }
}
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int []arr = new int[100005];

// Function to check if the number x
// is divisible by its sum of digits
static bool isDivisible(int x)
{

    // Stores sum of digits of x
    int sum = 0;

    // Temporarily store x
    int temp = x;

    // Calculate sum
    // of digits of x
    while (x != 0)
    {
        sum += x % 10;
        x /= 10;
    }

    // If x is not divisible by sum
    if (temp % sum != 0)
        return false;

    // Otherwise
    else
        return true;
}

// Function to perform
// the precomputation
static void precompute()
{

    // Iterate from i equals 1 to 1e5
    for(int i = 1; i <= 100000; i++)
    {

        // Check if i is divisible
        // by sum of its digits
        if (isDivisible(i))
            arr[i] = 1;
        else
            arr[i] = 0;
    }

    // Convert []arr to prefix sum array
    for(int i = 1; i <= 100000; i++)
    {
        arr[i] = arr[i] + arr[i - 1];
    }
}

public static int[] GetRow(int[,] matrix, int row)
{
    var rowLength = matrix.GetLength(1);
    var rowVector = new int[rowLength];

    for(var i = 0; i < rowLength; i++)
      rowVector[i] = matrix[row, i];

    return rowVector;
}

// Driver Code
public static void Main(String[] args)
{

    // Given queries
    int [,]Q = { { 5, 9 }, { 5, 20 } };
    int []q;
    precompute();

    for(int i = 0; i < Q.GetLength(0); i++)
    {
        q = GetRow(Q,i);

        // Using inclusion-exclusion
        // principle, calculate the result
        Console.WriteLine(arr[q[1]] - arr[q[0] - 1]);
    }
}
}

// This code is contributed by shikhasingrajput
```

**Output:** 

```
5
9
```

***时间复杂度:** O(N)*
***辅助空间:** O(maxm)，其中 **maxm** 表示 r 的最大值*
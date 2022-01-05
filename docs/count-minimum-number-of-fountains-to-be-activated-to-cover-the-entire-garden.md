# 计算覆盖整个花园的最小喷泉数量

> 原文:[https://www . geeksforgeeks . org/count-最小数量的喷泉将被激活以覆盖整个花园/](https://www.geeksforgeeks.org/count-minimum-number-of-fountains-to-be-activated-to-cover-the-entire-garden/)

有一个长度为 **N** 的一维花园。在**号**长花园的每个位置，都安装了一个喷泉。给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**a【】**，使得**a【I】**描述 **i <sup>th</sup>** 喷泉的覆盖范围。喷泉可以覆盖从位置**最大值(I–a[I]，1)** 到**最小值(i + a[i]，N)** 的范围。一开始，所有的喷泉都被关掉了。任务是找到需要激活的最小数量的喷泉，以便整个 **N** 长度的花园可以被水覆盖。

**示例:**

> **输入:** a[] = {1，2，1}
> **输出:** 1
> **解释:**
> 对于位置 1: a[1] = 1，范围= 1 到 2
> 对于位置 2: a[2] = 2，范围= 1 到 3
> 对于位置 3: a[3] = 1，范围= 2 到 3
> 因此，位置 a[2]的喷泉覆盖了整个花园。
> 因此，要求的输出为 1。
> 
> **输入:** a[] = {2，1，1，2，1}
> **输出:** 2

**方法:**使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于每个数组索引，即 **i** <sup>th</sup> 喷泉，找到当前喷泉覆盖的**最左边的喷泉**。
*   然后在**DP【】**数组中找到上一步得到的最左边喷泉覆盖到的最右边喷泉并更新。
*   初始化一个变量 **cntFount** 来存储需要激活的喷泉的最小数量。
*   现在，[遍历**DP【】**数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并继续激活左侧覆盖当前右侧最大喷泉的喷泉，并将**喷泉**增加 **1** 。最后，打印 **cntFount** 作为所需答案。

下面是上述方法的实现。

## C++14

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum
// number of fountains to be
// activated
int minCntFoun(int a[], int N)
{

    // dp[i]: Stores the position of
    // rightmost fountain that can
    // be covered by water of leftmost
    // fountain of the i-th fountain
    int dp[N];

    // initializing all dp[i] values to be -1,
    // so that we don't get garbage value
      for(int i=0;i<N;i++){
          dp[i]=-1;
    }

    // Stores index of leftmost fountain
    // in the range of i-th fountain
    int idxLeft;

    // Stores index of rightmost fountain
    // in the range of i-th fountain
    int idxRight;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        idxLeft = max(i - a[i], 0);
        idxRight = min(i + (a[i] + 1), N);
        dp[idxLeft] = max(dp[idxLeft],
                          idxRight);
    }

    // Stores count of fountains
    // needed to be activated
    int cntfount = 1;

    idxRight = dp[0];

    // Stores index of next fountain
    // that needed to be activated
    // initializing idxNext with -1
    // so that we don't get garbage value
    int idxNext=-1;

    // Traverse dp[] array
    for (int i = 0; i < N; i++)
    {
        idxNext = max(idxNext,
                      dp[i]);

        // If left most fountain
        // cover all its range
        if (i == idxRight)
        {
            cntfount++;
            idxRight = idxNext;
        }
    }

    return cntfount;
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 1 };
    int N = sizeof(a) / sizeof(a[0]);
    cout << minCntFoun(a, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG {

    // Function to find minimum
    // number of fountains to be
    // activated
    static int minCntFoun(int a[], int N)
    {

        // dp[i]: Stores the position of
        // rightmost fountain that can
        // be covered by water of leftmost
        // fountain of the i-th fountain
        int[] dp = new int[N];
        for(int i=0;i<N;i++)
        {
             dp[i]=-1;
        }

        // Stores index of leftmost fountain
        // in the range of i-th fountain
        int idxLeft;

        // Stores index of rightmost fountain
        // in the range of i-th fountain
        int idxRight;

        // Traverse the array
        for (int i = 0; i < N; i++)
        {
            idxLeft = Math.max(i - a[i], 0);
            idxRight = Math.min(i + (a[i] + 1), N);
            dp[idxLeft] = Math.max(dp[idxLeft],
                                   idxRight);
        }

        // Stores count of fountains
        // needed to be activated
        int cntfount = 1;

        // Stores index of next fountain
        // that needed to be activated
        int idxNext = 0;
        idxRight = dp[0];

        // Traverse dp[] array
        for (int i = 0; i < N; i++)
        {
            idxNext = Math.max(idxNext, dp[i]);

            // If left most fountain
            // cover all its range
            if (i == idxRight)
            {
                cntfount++;
                idxRight = idxNext;
            }
        }
        return cntfount;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int a[] = { 1, 2, 1 };
        int N = a.length;

        System.out.print(minCntFoun(a, N));
    }
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find minimum
# number of fountains to be
# activated

def minCntFoun(a, N):

    # dp[i]: Stores the position of
    # rightmost fountain that can
    # be covered by water of leftmost
    # fountain of the i-th fountain
    dp = [0] * N
    for i in range(N):
      dp[i] = -1

    # Traverse the array
    for i in range(N):
        idxLeft = max(i - a[i], 0)
        idxRight = min(i + (a[i] + 1), N)
        dp[idxLeft] = max(dp[idxLeft],
                          idxRight)

    # Stores count of fountains
    # needed to be activated
    cntfount = 1

    idxRight = dp[0]

    # Stores index of next fountain
    # that needed to be activated
    idxNext = 0

    # Traverse dp[] array
    for i in range(N):
        idxNext = max(idxNext,
                      dp[i])

        # If left most fountain
        # cover all its range
        if (i == idxRight):
            cntfount += 1
            idxRight = idxNext

    return cntfount

# Driver code
if __name__ == '__main__':

    a = [1, 2, 1]
    N = len(a)

    print(minCntFoun(a, N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG {

    // Function to find minimum
    // number of fountains to be
    // activated
    static int minCntFoun(int[] a, int N)
    {
        // dp[i]: Stores the position of
        // rightmost fountain that can
        // be covered by water of leftmost
        // fountain of the i-th fountain
        int[] dp = new int[N];
        for (int i = 0; i < N; i++)
        {
            dp[i] = -1;
        }

        // Stores index of leftmost
        // fountain in the range of
        // i-th fountain
        int idxLeft;

        // Stores index of rightmost
        // fountain in the range of
        // i-th fountain
        int idxRight;

        // Traverse the array
        for (int i = 0; i < N; i++) {
            idxLeft = Math.Max(i - a[i], 0);
            idxRight = Math.Min(i + (a[i] + 1),
                                N);
            dp[idxLeft] = Math.Max(dp[idxLeft],
                                   idxRight);
        }

        // Stores count of fountains
        // needed to be activated
        int cntfount = 1;

        // Stores index of next
        // fountain that needed
        // to be activated
        int idxNext = 0;
        idxRight = dp[0];

        // Traverse []dp array
        for (int i = 0; i < N; i++)
        {
            idxNext = Math.Max(idxNext, dp[i]);

            // If left most fountain
            // cover all its range
            if (i == idxRight)
            {
                cntfount++;
                idxRight = idxNext;
            }
        }
        return cntfount;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] a = { 1, 2, 1 };
        int N = a.Length;

        Console.Write(minCntFoun(a, N));
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find minimum
// number of fountains to be
// activated
function minCntFoun(a, N)
{

    // dp[i]: Stores the position of
    // rightmost fountain that can
    // be covered by water of leftmost
    // fountain of the i-th fountain
    let dp = [];
    for(let i = 0; i < N; i++)
    {
         dp[i] = -1;
    }

    // Stores index of leftmost fountain
    // in the range of i-th fountain
    let idxLeft;

    // Stores index of rightmost fountain
    // in the range of i-th fountain
    let idxRight;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {
        idxLeft = Math.max(i - a[i], 0);
        idxRight = Math.min(i + (a[i] + 1), N);
        dp[idxLeft] = Math.max(dp[idxLeft],
                               idxRight);
    }

    // Stores count of fountains
    // needed to be activated
    let cntfount = 1;

    // Stores index of next fountain
    // that needed to be activated
    let idxNext = 0;
    idxRight = dp[0];

    // Traverse dp[] array
    for(let i = 0; i < N; i++)
    {
        idxNext = Math.max(idxNext, dp[i]);

        // If left most fountain
        // cover all its range
        if (i == idxRight)
        {
            cntfount++;
            idxRight = idxNext;
        }
    }
    return cntfount;
}

// Driver Code
let a = [ 1, 2, 1 ];
let N = a.length;

document.write(minCntFoun(a, N));

// This code is contributed by souravghosh0416

</script>
```

**Output**

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
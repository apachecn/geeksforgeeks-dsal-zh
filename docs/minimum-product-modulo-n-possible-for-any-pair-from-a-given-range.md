# 给定范围内任意对的最小乘积模 N

> 原文:[https://www . geesforgeks . org/给定范围内任意对的最小乘积模 n-可能/](https://www.geeksforgeeks.org/minimum-product-modulo-n-possible-for-any-pair-from-a-given-range/)

给定三个整数 **L** 、 **R** 和 **N** ，任务是求 **(i * j) % N** 的最小可能值，其中 **L ≤ i < j ≤ R** 。

**示例:**

> **输入:** L = 2020，R = 2040，N = 2019
> T3】输出:2
> T6】说明: (2020 * 2021) % 2019 = 2
> 
> **输入:** L = 15，R = 30，N = 15
> **输出:** 0
> **说明:**如果该对元素中有一个是 15，那么所有这样的对的乘积将被 15 整除。因此，余数将为 0，这是最小可能值。

**方法:**找到 **L** 和 **R** 的区别就可以解决给定的问题。如果相差至少 **N** ，那么结果就是 **0** 。否则，迭代范围**【L，R】**，求最小乘积。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define ll long long
using namespace std;

// Function to return the minimum
// possible value of (i * j) % N
void minModulo(int L, int R, int N)
{
    if (R - L < N) {

        // Stores the minimum remainder
        int ans = INT_MAX;

        // Iterate from L to R
        for (ll i = L; i <= R; i++)

            // Iterate from L to R
            for (ll j = L; j <= R; j++)
                if (i != j)
                    ans = min(0ll + ans,
                              (i * j) % N);

        // Print the minimum value
        // of remainder
        cout << ans;
    }

    // If R - L >= N
    else {
        cout << 0;
    }
}

// Driver Code
int main()
{
    int L = 6, R = 10, N = 2019;
    minModulo(L, R, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG
{

    // Function to return the minimum
    // possible value of (i * j) % N
    static void minModulo(int L, int R, int N)
    {
        if (R - L < N)
        {

            // Stores the minimum remainder
            int ans = Integer.MAX_VALUE;

            // Iterate from L to R
            for (int i = L; i <= R; i++)

                // Iterate from L to R
                for (int j = L; j <= R; j++)
                    if (i != j)
                        ans = Math.min(ans, (i * j) % N);

            // Print the minimum value
            // of remainder
            System.out.println(ans);
        }

        // If R - L >= N
        else {
            System.out.println(0);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        int L = 6, R = 10, N = 2019;
        minModulo(L, R, N);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the minimum
# possible value of (i * j) % N
def minModulo(L, R, N):

    if (R - L < N):

        # Stores the minimum remainder
        ans = 10**9

        # Iterate from L to R
        for i in range(L, R + 1):

            # Iterate from L to R
            for j in range(L, R + 1):
                if (i != j):
                    ans = min(ans, (i * j) % N)

        # Print the minimum value
        # of remainder
        print (ans)

    # If R - L >= N
    else:
        print (0)

# Driver Code
if __name__ == '__main__':

    L, R, N = 6, 10, 2019
    minModulo(L, R, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return the minimum
// possible value of (i * j) % N
static void minModulo(int L, int R, int N)
{
    if (R - L < N)
    {

        // Stores the minimum remainder
        int ans = Int32.MaxValue;

        // Iterate from L to R
        for(int i = L; i <= R; i++)

            // Iterate from L to R
            for(int j = L; j <= R; j++)
                if (i != j)
                    ans = Math.Min(ans, (i * j) % N);

        // Print the minimum value
        // of remainder
        Console.WriteLine(ans);
    }

    // If R - L >= N
    else
    {
        Console.WriteLine(0);
    }
}

// Driver Code
public static void Main(string[] args)
{
    int L = 6, R = 10, N = 2019;
    minModulo(L, R, N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript implementation
// for the above approach

    // Function to return the minimum
    // possible value of (i * j) % N
    function minModulo(L, R, N)
    {
        if (R - L < N)
        {

            // Stores the minimum remainder
            let ans = Number.MAX_VALUE;

            // Iterate from L to R
            for (let i = L; i <= R; i++)

                // Iterate from L to R
                for (let j = L; j <= R; j++)
                    if (i != j)
                        ans = Math.min(ans, (i * j) % N);

            // Print the minimum value
            // of remainder
            document.write(ans);
        }

        // If R - L >= N
        else {
            document.write(0);
        }
    }

// Driver Code

    let L = 6, R = 10, N = 2019;
        minModulo(L, R, N);

    // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
42
```

***时间复杂度:**O((R–L)<sup>2</sup>)*
***辅助空间:** O(1)*
# 统计数列 K，K+1，K+2，K+3，K+4，…，K+N 的所有可能唯一和

> 原文:[https://www . geesforgeks . org/count-all-可能性-unique-数列之和-k-k1-k2-k3-k4-kn/](https://www.geeksforgeeks.org/count-all-possible-unique-sum-of-series-k-k1-k2-k3-k4-kn/)

给定一个数 **N** ，对于任意数 K，形成为 **K，K + 1，K + 2，K + 3，K + 4，…。，K + N** 。任务是从 **N + 1** 整数序列中找出两个或两个以上整数相加可以得到的唯一和的个数。

**示例:**

> **输入:** N = 3
> **输出:** 10
> **解释:**
> 可能的唯一组合为:
> (K)+(K+1)= 2 * K+1
> (K)+(K+2)= 2 * K+2
> (K)+(K+3)= 2 * K+3
> (K+1)+(K+3)= 2 * K+4
> (K +(K+2)= 3 * K+3
> (K)+(K+1)+(K+3)= 3 * K+4
> (K)+(K+2)+(K+3)= 3 * K+5
> (K+1)+(K+2)+(K+3)= 3 * K+6
> (K)+(K+1)+(K+2)+(K+3)= 4 * K+6
> So in
> **输入:** N = 4
> **输出:** 20
> **解释:**
> 可能的唯一组合数量为 20。

**进场:**进行以下观察:

*   既然 **K** 是数，它唯一的意义就是大小不同的两个子集不能有相同的和。
*   唯一和可以从子集的最小可能和到大小为 **X** 的子集的最大可能和获得，其中(2 ≤ X ≤ (N + 1))。

> 例如: **N = 4**
> 级数为= {K，K + 1，K + 2，K + 3，K + 4}
> 对于 **K = 2** ，最小 _ 和= (K，K + 1) = 2*K + 1
> 和最大 _ 和= (K + 3，K + 4) = 2*K + 7
> 与 **K = 2** 可能的最大相异和为**(最大 _ 和–最小 _ 和+ 1**

按照以下步骤解决问题:

1.  初始化**两个数组**数组 *fsum[]* 和 *rsum[]* ，每个数组大小为 **N + 1** 到 **0** 。
2.  对于数组 fsum[]和 rsum[]的每个元素，用**ar[I]+fsum[I–1]**更新 **fsum[i]** ，用 **ar[i] + fsum[i + 1]** 更新 **rsum[i]** 。
3.  将变量 ***和*** 初始化为 1，该变量存储给定序列的不同可能和的计数。
4.  对于每个可能的子集大小 **X** ，其中(2 ≤ X ≤ (N + 1))，将值**1+rsum[N+1–k]+fsum[k]**加到 *ans* 上。
5.  *和*的值是必需的答案，因此返回它。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the unique sum
int count_unique_sum(int n)
{

    int i, ar[n + 1], fsum[n + 1];
    int rsum[n + 1], ans = 1;

    // Initialize array fsum[] with 0
    memset(fsum, 0, sizeof fsum);

    // Initialize array rsum[] with 0
    memset(rsum, 0, sizeof rsum);

    for (i = 0; i <= n; i++) {
        ar[i] = i;
    }

    // Set fsum[0] as ar[0]
    fsum[0] = ar[0];

    // Set rsum[0] as ar[n]
    rsum[n] = ar[n];

    // For each i update fsum[i] with
    // ar[i] + fsum[i - 1]
    for (i = 1; i <= n; i++) {
        fsum[i] = ar[i] + fsum[i - 1];
    }

    // For each i from n-1, update
    // rsum[i] with ar[i] + fsum[i + 1]
    for (i = n - 1; i >= 0; i--) {
        rsum[i] = ar[i] + rsum[i + 1];
    }

    // K represent size of subset as
    // explained above
    for (int k = 2; k <= n; k++) {

        // Using above relation
        ans += 1 + rsum[n + 1 - k]
               - fsum[k - 1];
    }

    // Return the result
    return ans;
}

// Driver Code
int main()
{
    // Given a number N
    int N = 4;

    // Function Call
    cout << count_unique_sum(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to count the unique sum
static int count_unique_sum(int n)
{
    int i;
    int ar[] = new int[n + 1];
    int fsum[] = new int[n + 1];
    int rsum[] = new int[n + 1];
    int ans = 1;

    // Initialize array fsum[] with 0
    Arrays.fill(fsum, 0);

    // Initialize array rsum[] with 0
    Arrays.fill(rsum, 0);

    for (i = 0; i <= n; i++)
    {
        ar[i] = i;
    }

    // Set fsum[0] as ar[0]
    fsum[0] = ar[0];

    // Set rsum[0] as ar[n]
    rsum[n] = ar[n];

    // For each i update fsum[i] with
    // ar[i] + fsum[i - 1]
    for (i = 1; i <= n; i++)
    {
        fsum[i] = ar[i] + fsum[i - 1];
    }

    // For each i from n-1, update
    // rsum[i] with ar[i] + fsum[i + 1]
    for (i = n - 1; i >= 0; i--)
    {
        rsum[i] = ar[i] + rsum[i + 1];
    }

    // K represent size of subset as
    // explained above
    for (int k = 2; k <= n; k++)
    {

        // Using above relation
        ans += 1 + rsum[n + 1 - k] -
                     fsum[k - 1];
    }

    // Return the result
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    // Given a number N
    int N = 4;

    // Function Call
    System.out.print(count_unique_sum(N));
}
}

// This code is contributed by rock__cool
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the unique sum
def count_unique_sum(n):

    ar = [0] * (n + 1)
    fsum = [0] * (n + 1)
    rsum = [0] * (n + 1)
    ans = 1

    for i in range(0, n + 1):
        ar[i] = i

    # Set fsum[0] as ar[0]
    fsum[0] = ar[0]

    # Set rsum[0] as ar[n]
    rsum[n] = ar[n]

    # For each i update fsum[i] with
    # ar[i] + fsum[i - 1]
    for i in range(1, n + 1):
        fsum[i] = ar[i] + fsum[i - 1]

    # For each i from n-1, update
    # rsum[i] with ar[i] + fsum[i + 1]
    for i in range(n - 1, -1, -1):
        rsum[i] = ar[i] + rsum[i + 1]

    # K represent size of subset as
    # explained above
    for k in range(2, n + 1):

        # Using above relation
        ans += (1 + rsum[n + 1 - k] -
                    fsum[k - 1])

    # Return the result
    return ans

# Driver Code

# Given a number N
N = 4

# Function call
print(count_unique_sum(N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to count the unique sum
static int count_unique_sum(int n)
{
    int i;
    int []ar = new int[n + 1];
    int []fsum = new int[n + 1];
    int []rsum = new int[n + 1];
    int ans = 1;

    for (i = 0; i <= n; i++)
    {
        ar[i] = i;
    }

    // Set fsum[0] as ar[0]
    fsum[0] = ar[0];

    // Set rsum[0] as ar[n]
    rsum[n] = ar[n];

    // For each i update fsum[i] with
    // ar[i] + fsum[i - 1]
    for (i = 1; i <= n; i++)
    {
        fsum[i] = ar[i] + fsum[i - 1];
    }

    // For each i from n-1, update
    // rsum[i] with ar[i] + fsum[i + 1]
    for (i = n - 1; i >= 0; i--)
    {
        rsum[i] = ar[i] + rsum[i + 1];
    }

    // K represent size of subset as
    // explained above
    for (int k = 2; k <= n; k++)
    {

        // Using above relation
        ans += 1 + rsum[n + 1 - k] -
                   fsum[k - 1];
    }

    // Return the result
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    // Given a number N
    int N = 4;

    // Function Call
    Console.Write(count_unique_sum(N));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to count the unique sum
    function count_unique_sum(n)
    {

        let i;
        let ans = 1;
        let ar = new Array(n + 1);
        let fsum = new Array(n + 1);
        let rsum = new Array(n + 1);

        // Initialize array fsum[] with 0
        fsum.fill(0);

        // Initialize array rsum[] with 0
        rsum.fill(0);

        for (i = 0; i <= n; i++) {
            ar[i] = i;
        }

        // Set fsum[0] as ar[0]
        fsum[0] = ar[0];

        // Set rsum[0] as ar[n]
        rsum[n] = ar[n];

        // For each i update fsum[i] with
        // ar[i] + fsum[i - 1]
        for (i = 1; i <= n; i++) {
            fsum[i] = ar[i] + fsum[i - 1];
        }

        // For each i from n-1, update
        // rsum[i] with ar[i] + fsum[i + 1]
        for (i = n - 1; i >= 0; i--) {
            rsum[i] = ar[i] + rsum[i + 1];
        }

        // K represent size of subset as
        // explained above
        for (let k = 2; k <= n; k++) {

            // Using above relation
            ans += 1 + rsum[n + 1 - k]
                   - fsum[k - 1];
        }

        // Return the result
        return ans;
    }

    // Given a number N
    let N = 4;

    // Function Call
    document.write(count_unique_sum(N));

//This code is contribute by suresh07.
</script>
```

**Output**

```
20
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*
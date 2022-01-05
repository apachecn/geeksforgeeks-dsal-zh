# N 除以 K 的幂的商之和不超过 N

> 原文:[https://www . geesforgeks . org/n 除以 k 的幂的商之和-不超过-n/](https://www.geeksforgeeks.org/sum-of-quotients-of-division-of-n-by-powers-of-k-not-exceeding-n/)

给定两个正整数 **N** 和 **K** ，任务是求 **N** 除以小于或等于 **N** 的 **K** 的幂的商之和。

**示例:**

> **输入:** N = 10，K = 2
> **输出:** 18
> **说明:**
> 10 除 1 (= 2 <sup>0</sup> )。商= 10。因此，总和= 10。
> 10 除以 2 (= 2 <sup>1</sup> )。商= 5。因此，总和= 15。
> 10 除以 4 (= 2 <sup>2</sup> )。商= 2。因此，总和= 17。
> 10 除以 8 (= 2 <sup>3</sup> )。商= 1。因此，总和= 18。
> 
> **输入:** N = 5，K=2
> **输出:** 8
> **解释:**
> 5 除 1 (= 2 <sup>0</sup> )。商= 5。因此，总和= 5。
> 5 除以 2 (= 2 <sup>1</sup> )。商= 2。因此，总和= 7。
> 5 除以 4 (= 2 <sup>2</sup> )。商= 1。因此，总和= 8。

**方法:**思路是在 **K** 当前功率小于或等于 **N** 的情况下[迭代一个循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)，每次迭代不断将商加和。
按照以下步骤解决问题:

*   初始化一个变量，比如**和**，来存储需要的和。
*   初始化一个变量，说 **i** = **1** (= K <sup>0</sup> )存储 **K** 的[次幂。](https://www.geeksforgeeks.org/power-function-cc/)
*   [迭代至 **i ≤ N**](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/) 的值，执行以下操作:
    *   将 **N** 除以 **i** 得到的商存储在一个变量中，比如说 **X** 。
    *   将 **X** 的值加到 **ans** 上，将 **i** 乘以 **K** 得到 **K** 的下一次幂。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of
// quotients obtained by dividing
// N by powers of K <= N
int findSum(int N, int K)
{
    // Store the required sum
    int ans = 0;
    int i = 1;

    // Iterate until i exceeds N
    while (i <= N) {

        // Update sum
        ans += N / i;

        // Multiply i by K to
        // obtain next power of K
        i = i * K;
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    // Given N and K
    int N = 10, K = 2;
    findSum(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to calculate sum of
  // quotients obtained by dividing
  // N by powers of K <= N
  static void findSum(int N, int K)
  {

    // Store the required sum
    int ans = 0;
    int i = 1;

    // Iterate until i exceeds N
    while (i <= N)
    {

      // Update sum
      ans += N / i;

      // Multiply i by K to
      // obtain next power of K
      i = i * K;
    }

    // Print the result
    System.out.println(ans);
  }

  // Driver Code
  public static void main(String[] args)
  {
    // Given N and K
    int N = 10, K = 2;
    findSum(N, K);
  }
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate sum of
# quotients obtained by dividing
# N by powers of K <= N
def findSum(N, K):

    # Store the required sum
    ans = 0
    i = 1

    # Iterate until i exceeds N
    while (i <= N):

        # Update sum
        ans += N // i

        # Multiply i by K to
        # obtain next power of K
        i = i * K

    # Prthe result
    print (ans)

# Driver Code
if __name__ == '__main__':

    # Given N and K
    N, K = 10, 2
    findSum(N, K)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate sum of
// quotients obtained by dividing
// N by powers of K <= N
static void findSum(int N, int K)
{

    // Store the required sum
    int ans = 0;
    int i = 1;

    // Iterate until i exceeds N
    while (i <= N)
    {

        // Update sum
        ans += N / i;

        // Multiply i by K to
        // obtain next power of K
        i = i * K;
    }

    // Print the result
    Console.Write(ans);
}

// Driver code
static void Main()
{

    // Given N and K
    int N = 10, K = 2;

    findSum(N, K);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to calculate sum of
// quotients obtained by dividing
// N by powers of K <= N
function findSum(N, K)
{
    // Store the required sum
    var ans = 0;
    var i = 1;

    // Iterate until i exceeds N
    while (i <= N) {

        // Update sum
        ans += Math.floor(N / i);

        // Multiply i by K to
        // obtain next power of K
        i = i * K;
    }

    // Print the result
    document.write(ans);
}

// Driver Code

    // Given N and K
    var N = 10, K = 2;
    findSum(N, K);

</script>
```

**Output:** 

```
18
```

***时间复杂度:**O(log<sub>K</sub>(N))*
***辅助空间:** O(1)*
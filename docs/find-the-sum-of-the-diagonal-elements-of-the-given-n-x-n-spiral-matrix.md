# 求给定 N×N 螺旋矩阵对角元素的和

> 原文:[https://www . geesforgeks . org/find-给定 n-x-n-螺旋矩阵的对角线元素之和/](https://www.geeksforgeeks.org/find-the-sum-of-the-diagonal-elements-of-the-given-n-x-n-spiral-matrix/)

给定 **N** 这是 **N X N** 螺旋矩阵的大小形式:

```
16 15 14 13
5  4  3  12
6  1  2  11
7  8  9  10
```

任务是找出这个矩阵对角元素的和。
**例:**

```
Input: N = 3
Output: 25
5 4 3
6 1 2
7 8 9
The sum of elements along its two diagonals will be 
1 + 3 + 7 + 5 + 9 = 25

Input: N = 5
Output: 101
```

**递归方法:**解决方案背后的思想是使用[递归](https://www.geeksforgeeks.org/recursion/)来计算对角线元素的和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of both the
// diagonal elements of the required matrix
int findSum(int n)
{
    // Base cases
    if(n == 0) {
        return 0;
    }
    if(n == 1) {
        return 1;
    }

    int ans = 0;
    // Computing for ans
    for (int i = 2; i <= n; i++) {
        ans =(4 * (i * i))
                - 6 * (i - 1) + findSum(n - 2);
    }
    // Return ans;
    return ans;
}

// Driver code
int main()
{
    int n = 4;

    cout << findSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

public class GFG
{

// Function to return the sum of both the
// diagonal elements of the required matrix
static int findSum(int n)
{
    // Base cases
    if(n == 0) {
        return 0;
    }
    if(n == 1) {
        return 1;
    }

    int ans = 0;
    // Computing for ans
    for (int i = 2; i <= n; i++) {
        ans =(4 * (i * i))
                - 6 * (i - 1) + findSum(n - 2);
    }
    // Return ans;
    return ans;
}

// Driver code
public static void main(String args[])
{
    int n = 4;

    System.out.println(findSum(n));

}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the sum of both the
# diagonal elements of the required matrix
def findSum(n):

    # Base cases
    if(n == 0):
        return 0

    if(n == 1):
        return 1

    ans = 0
    # Computing for ans
    for i in range(2, n + 1, 1):
        ans = ((4 * (i * i)) - 6 *
                      (i - 1) + findSum(n - 2))

    return ans

# Driver code
if __name__ == '__main__':
    n = 4

    print(findSum(n))

# This code is contributed by
# Samim Hossain Mondal
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the sum of both the
// diagonal elements of the required matrix
static int findSum(int n)
{
    // Base cases
    if(n == 0) {
        return 0;
    }
    if(n == 1) {
        return 1;
    }

    int ans = 0;
    // Computing for ans
    for (int i = 2; i <= n; i++) {
        ans =(4 * (i * i))
                - 6 * (i - 1) + findSum(n - 2);
    }
    // Return ans;
    return ans;
}

// Driver code
public static void Main()
{
    int n = 4;

    Console.Write(findSum(n));

}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the sum of both the
// diagonal elements of the required matrix
function findSum(n)
{
    // Base cases
    if(n == 0) {
        return 0;
    }
    if(n == 1) {
        return 1;
    }

    let ans = 0;
    // Computing for ans
    for (let i = 2; i <= n; i++) {
        ans =(4 * (i * i))
                - 6 * (i - 1) + findSum(n - 2);
    }
    // Return ans;
    return ans;
}

// Driver code
let n = 4;
document.write(findSum(n));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
56
```

**时间复杂度:** O(2 <sup>N</sup>

**辅助空间:** 1

**动态规划法:**解决方案背后的思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的概念。我们将使用数组 **dp[]** 来存储我们的解决方案。问题中给出的 n 可以是偶数，也可以是奇数。
当 **i** 为奇数时，我们只需在**DP【I–2】**中添加 4 个角元素。

> dp[i] = dp[i – 2] + （i – 2） * （i – 2） + （i – 1） + （i – 2） * （i – 2） + 2 * （i – 1） + （i – 2） * （i – 2） + 3 * （i – 1） + （i – 2） * （i – 2） + 4 * （i – 1）
> dp[i] = dp[i – 2] + 4 * （i – 2） * （i – 2） + 10 * （i – 1）
> **dp[i] = dp[i – 2] + 4 * （i） * （i） – 6 * （i – 1）**

同样，当 **i** 为**甚至**时，我们可以检查上述公式是否成立。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of both the
// diagonal elements of the required matrix
int findSum(int n)
{
    // Array to store sum of diagonal elements
    int dp[n + 1];

    // Base cases
    dp[1] = 1;
    dp[0] = 0;

    // Computing the value of dp
    for (int i = 2; i <= n; i++) {
        dp[i] = (4 * (i * i))
                - 6 * (i - 1) + dp[i - 2];
    }

    return dp[n];
}

// Driver code
int main()
{
    int n = 4;

    cout << findSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the sum of both the
// diagonal elements of the required matrix
static int findSum(int n)
{
    // Array to store sum of diagonal elements
    int[] dp = new int[n + 1];

    // Base cases
    dp[1] = 1;
    dp[0] = 0;

    // Computing the value of dp
    for (int i = 2; i <= n; i++)
    {
        dp[i] = (4 * (i * i)) - 6 *
                    (i - 1) + dp[i - 2];
    }

    return dp[n];
}

// Driver code
public static void main(String args[])
{
    int n = 4;

    System.out.println(findSum(n));
}
}

// This code is contributed by Akanksha Rai
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the sum of both the
# diagonal elements of the required matrix
def findSum(n):

    # Array to store sum of diagonal elements
    dp = [0 for i in range(n + 1)]

    # Base cases
    dp[1] = 1
    dp[0] = 0

    # Computing the value of dp
    for i in range(2, n + 1, 1):
        dp[i] = ((4 * (i * i)) - 6 *
                      (i - 1) + dp[i - 2])

    return dp[n]

# Driver code
if __name__ == '__main__':
    n = 4

    print(findSum(n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach

class GFG
{

// Function to return the sum of both the
// diagonal elements of the required matrix
static int findSum(int n)
{
    // Array to store sum of diagonal elements
    int[] dp = new int[n + 1];

    // Base cases
    dp[1] = 1;
    dp[0] = 0;

    // Computing the value of dp
    for (int i = 2; i <= n; i++)
    {
        dp[i] = (4 * (i * i))
                - 6 * (i - 1) + dp[i - 2];
    }

    return dp[n];
}

// Driver code
static void Main()
{
    int n = 4;

    System.Console.WriteLine(findSum(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the sum of both the
// diagonal elements of the required matrix
function findSum($n)
{

    // Array to store sum of diagonal elements
    $dp = array();

    // Base cases
    $dp[1] = 1;
    $dp[0] = 0;

    // Computing the value of dp
    for ($i = 2; $i <= $n; $i++)
    {
        $dp[$i] = (4 * ($i * $i)) - 6 *
                       ($i - 1) + $dp[$i - 2];
    }

    return $dp[$n];
}

// Driver code
$n = 4;

echo findSum($n);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the sum of both the
// diagonal elements of the required matrix
let findSum(n)
{

    // Array to store sum of diagonal elements
    let dp = new Array(n + 1);

    // Base cases
    dp[1] = 1;
    dp[0] = 0;

    // Computing the value of dp
    for (let i = 2; i <= n; i++) {
        dp[i] = (4 * (i * i))
                - 6 * (i - 1) + dp[i - 2];
    }

    return dp[n];
}

// Driver code
let n = 4;

document.write(findSum(n));

// This code is contributed by rishavmahato348.
</script>
```

**Output**

```
56
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)
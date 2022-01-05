# N 的最小值，使得从 K 到 N 的所有自然数之和至少为 X

> 原文:[https://www . geesforgeks . org/n 的最小值，即从 k 到 n 的所有自然数之和至少是-x/](https://www.geeksforgeeks.org/smallest-value-of-n-such-that-the-sum-of-all-natural-numbers-from-k-to-n-is-at-least-x/)

给定两个正整数 **X** 和 **K** ，任务是找到 **N** 的最小值，使得范围**【K，N】**中所有自然数[的和至少为**X**。如果不存在 **N** 的可能值，则打印 **-1** 。](https://www.geeksforgeeks.org/sum-of-natural-numbers-using-recursion/)

**示例:**

> **输入:** K = 5，X = 13
> **输出:** 7
> **说明:**最小可能值为 7。Sum = 5 + 6 + 7 = 18，至少是 13。
> 
> **输入:** K = 3，X = 15
> T3】输出: 6

**天真法:**解决这个问题最简单的方法是检查**【K，X】**范围内的每个值，并从该范围返回第一个值，该值至少有 X 个第一个 **N** 个自然数的[和。](https://www.geeksforgeeks.org/find-given-number-sum-first-n-natural-numbers/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum possible
// value of N such that sum of natural
// numbers from K to N is at least X
void minimumNumber(int K, int X)
{
    // If K is greater than X
    if (K > X) {
        cout << "-1";
        return;
    }

    // Stores value of minimum N
    int ans = 0;

    // Stores the sum of values
    // over the range [K, ans]
    int sum = 0;

    // Iterate over the range [K, N]
    for (int i = K; i <= X; i++) {

        sum += i;

        // Check if sum of first i
        // natural numbers is >= X
        if (sum >= X) {
            ans = i;
            break;
        }
    }

    // Print the possible value of ans
    cout << ans;
}

// Driver Code
int main()
{
    int K = 5, X = 13;
    minimumNumber(K, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the minimum possible
// value of N such that sum of natural
// numbers from K to N is at least X
static void minimumNumber(int K, int X)
{

    // If K is greater than X
    if (K > X)
    {
        System.out.println("-1");
        return;
    }

    // Stores value of minimum N
    int ans = 0;

    // Stores the sum of values
    // over the range [K, ans]
    int sum = 0;

    // Iterate over the range [K, N]
    for(int i = K; i <= X; i++)
    {
        sum += i;

        // Check if sum of first i
        // natural numbers is >= X
        if (sum >= X)
        {
            ans = i;
            break;
        }
    }

    // Print the possible value of ans
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{
    int K = 5, X = 13;

    minimumNumber(K, X);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum possible
# value of N such that sum of natural
# numbers from K to N is at least X
def minimumNumber(K, X):

    # If K is greater than X
    if (K > X):
        print("-1")
        return

    # Stores value of minimum N
    ans = 0

    # Stores the sum of values
    # over the range [K, ans]
    sum = 0

    # Iterate over the range [K, N]
    for i in range(K, X + 1):
        sum += i

        # Check if sum of first i
        # natural numbers is >= X
        if (sum >= X):
            ans = i
            break

    # Print the possible value of ans
    print(ans)

# Driver Code
K = 5
X = 13

minimumNumber(K, X)

# This code is contributed by subham348
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum possible
// value of N such that sum of natural
// numbers from K to N is at least X
static void minimumNumber(int K, int X)
{

    // If K is greater than X
    if (K > X)
    {
        Console.Write("-1");
        return;
    }

    // Stores value of minimum N
    int ans = 0;

    // Stores the sum of values
    // over the range [K, ans]
    int sum = 0;

    // Iterate over the range [K, N]
    for(int i = K; i <= X; i++)
    {
        sum += i;

        // Check if sum of first i
        // natural numbers is >= X
        if (sum >= X)
        {
            ans = i;
            break;
        }
    }

    // Print the possible value of ans
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    int K = 5, X = 13;

    minimumNumber(K, X);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum possible
// value of N such that sum of natural
// numbers from K to N is at least X
function minimumNumber(K, X)
{
    // If K is greater than X
    if (K > X) {
        document.write("-1");
        return;
    }

    // Stores value of minimum N
    let ans = 0;

    // Stores the sum of values
    // over the range [K, ans]
    let sum = 0;

    // Iterate over the range [K, N]
    for (let i = K; i <= X; i++) {

        sum += i;

        // Check if sum of first i
        // natural numbers is >= X
        if (sum >= X) {
            ans = i;
            break;
        }
    }

    // Print the possible value of ans
    document.write(ans);
}

// Driver Code
    let K = 5, X = 13;
    minimumNumber(K, X);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N–K)*
***辅助空间:** O(1)*

**高效途径:**使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以优化上述途径。按照以下步骤解决给定的问题:

*   初始化一个变量，将 **res** 设为 **-1** ，以存储满足给定条件的 **N** 的最小可能值。
*   初始化两个变量，说**低**为 **K** ，说**高**为 **X** ，通过执行以下步骤在这个范围内执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/):
    *   求**中间**的值为**低+(高-低)/ 2** 。
    *   如果[从 **K** 到**中间**的自然数](https://www.geeksforgeeks.org/sum-of-natural-numbers-using-recursion/)之和大于或等于 **X** 则为否。
    *   如果发现为真，则将 **res** 更新为 **mid** ，并将**设置为高=(mid–1)**。否则，将低电平更新为**(中间+ 1)** 。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the sum of
// natural numbers from K to N is >= X
bool isGreaterEqual(int N, int K, int X)
{
    return ((N * 1LL * (N + 1) / 2)
            - ((K - 1) * 1LL * K / 2))
           >= X;
}

// Function to find the minimum value
// of N such that the sum of natural
// numbers from K to N is at least X
void minimumNumber(int K, int X)
{
    // If K is greater than X
    if (K > X) {
        cout << "-1";
        return;
    }

    int low = K, high = X, res = -1;

    // Perform the Binary Search
    while (low <= high) {
        int mid = low + (high - low) / 2;

        // If the sum of the natural
        // numbers from K to mid is atleast X
        if (isGreaterEqual(mid, K, X)) {

            // Update res
            res = mid;

            // Update high
            high = mid - 1;
        }

        // Otherwise, update low
        else
            low = mid + 1;
    }

    // Print the value of
    // res as the answer
    cout << res;
}

// Driver Code
int main()
{
    int K = 5, X = 13;
    minimumNumber(K, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if the sum of
// natural numbers from K to N is >= X
static boolean isGreaterEqual(int N, int K, int X)
{
    return ((N * 1L * (N + 1) / 2) -
           ((K - 1) * 1L * K / 2)) >= X;
}

// Function to find the minimum value
// of N such that the sum of natural
// numbers from K to N is at least X
static void minimumNumber(int K, int X)
{

    // If K is greater than X
    if (K > X)
    {
        System.out.println("-1");
        return;
    }

    int low = K, high = X, res = -1;

    // Perform the Binary Search
    while (low <= high)
    {
        int mid = low + (high - low) / 2;

        // If the sum of the natural
        // numbers from K to mid is atleast X
        if (isGreaterEqual(mid, K, X))
        {

            // Update res
            res = mid;

            // Update high
            high = mid - 1;
        }

        // Otherwise, update low
        else
            low = mid + 1;
    }

    // Print the value of
    // res as the answer
    System.out.println(res);
}

// Driver Code
public static void main(String[] args)
{
    int K = 5, X = 13;

    minimumNumber(K, X);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if the sum of
# natural numbers from K to N is >= X

def isGreaterEqual(N, K, X):
    return (((N * (N + 1) // 2)
             - ((K - 1) * K // 2))
            >= X)

# Function to find the minimum value
# of N such that the sum of natural
# numbers from K to N is at least X

def minimumNumber(K, X):
    # If K is greater than X
    if (K > X):
        print("-1")
        return

    low = K
    high = X
    res = -1

    # Perform the Binary Search
    while (low <= high):
        mid = low + ((high - low) // 2)

        # If the sum of the natural
        # numbers from K to mid is atleast X
        if (isGreaterEqual(mid, K, X)):

            # Update res
            res = mid

            # Update high
            high = mid - 1

        # Otherwise, update low
        else:
            low = mid + 1

    # Print the value of
    # res as the answer
    print(res)

# Driver Code
K = 5
X = 13
minimumNumber(K, X)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the sum of
// natural numbers from K to N is >= X
static bool isGreaterEqual(int N, int K, int X)
{
    return ((N * 1L * (N + 1) / 2) -
           ((K - 1) * 1L * K / 2)) >= X;
}

// Function to find the minimum value
// of N such that the sum of natural
// numbers from K to N is at least X
static void minimumNumber(int K, int X)
{

    // If K is greater than X
    if (K > X)
    {
        Console.Write("-1");
        return;
    }

    int low = K, high = X, res = -1;

    // Perform the Binary Search
    while (low <= high)
    {
        int mid = low + (high - low) / 2;

        // If the sum of the natural
        // numbers from K to mid is atleast X
        if (isGreaterEqual(mid, K, X))
        {

            // Update res
            res = mid;

            // Update high
            high = mid - 1;
        }

        // Otherwise, update low
        else
            low = mid + 1;
    }

    // Print the value of
    // res as the answer
    Console.WriteLine(res);
}

// Driver Code
public static void Main()
{
    int K = 5, X = 13;

    minimumNumber(K, X);
}
}

// This code is contributed by subham348
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if the sum of
// natural numbers from K to N is >= X
function isGreaterEqual(N, K, X)
{
    return ((N * parseInt((N + 1) / 2))
            - ((K - 1) * parseInt(K / 2)))
           >= X;
}

// Function to find the minimum value
// of N such that the sum of natural
// numbers from K to N is at least X
function minimumNumber(K, X)
{
    // If K is greater than X
    if (K > X) {
        document.write("-1");
        return;
    }

    let low = K, high = X, res = -1;

    // Perform the Binary Search
    while (low <= high) {
        let mid = low + parseInt((high - low) / 2);

        // If the sum of the natural
        // numbers from K to mid is atleast X
        if (isGreaterEqual(mid, K, X)) {

            // Update res
            res = mid;

            // Update high
            high = mid - 1;
        }

        // Otherwise, update low
        else
            low = mid + 1;
    }

    // Print the value of
    // res as the answer
    document.write(res);
}

// Driver Code
let K = 5, X = 13;
minimumNumber(K, X);

// This code is contributed by subham348.
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(log(X–K))*
***辅助空间:** O(1)*
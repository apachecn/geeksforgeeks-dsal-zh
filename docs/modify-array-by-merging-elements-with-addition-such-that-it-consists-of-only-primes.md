# 通过加法合并元素来修改数组，使其仅由素数组成。

> 原文:[https://www . geesforgeks . org/通过合并元素来修改数组，使其仅由素数组成/](https://www.geeksforgeeks.org/modify-array-by-merging-elements-with-addition-such-that-it-consists-of-only-primes/)

给定一个由正整数组成的数组 **arr[]** ，任务是检查我们是否可以通过添加数组的任何元素来修改该数组，使其仅由[素数](https://www.geeksforgeeks.org/prime-numbers/)组成。

**示例:**

> **输入:** arr[] = {3，5，7，21}
> **输出:** YES
> **解释:**
> 加入以下元素，3+5+21
> 这样数组就变成了只包含素数的{7，29}。
> 
> **输入:** {2，5，12，16}
> **输出:**否
> **解释:**
> 元素之间没有可能的组合会使数组包含所有素数
> 
> **输入:** {3，5，13，22}
> **输出:**是
> **说明:**
> 只能有一个组合，
> 添加所有元素–3+5+13+22 = { 43 }其中只有质数

**先决条件:** [位屏蔽-DP](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)
T5】方法:

*   我们可以使用带有位掩码的[动态编程](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)来解决这个问题。我们可以将我们的**状态表示为元素子集的掩码。**
*   因此，让我们的 dp 数组成为 **DP【掩码】**，它表示在这个掩码(所选元素)之前，所形成的意志元素子集是否只是[素数](https://www.geeksforgeeks.org/prime-numbers/)。
*   掩码中的最大位数将是数组中的元素数。
*   我们继续在掩码中标记编码为序列的元素(如果选择了第 I 个索引元素，则在掩码中设置第 I 个位)，并继续检查当前选择的元素(当前和)是否是素数，如果是素数并且访问了所有其他元素，则返回 **true** ，我们得到答案。
*   否则如果其他元素没有被访问，那么由于当前和是素数，我们只需要搜索其他可以单独或通过求和形成一些素数的元素，这样我们就可以安全地将当前和再次标记为 0。
*   如果掩码是**满的**(所有元素都被访问)并且当前和不是素数，我们返回**假的**，因为至少有一个和不是素数。
*   **复发**:

```
DP[mask] = solve(curr + arr[i], mask | 1<<i)     
where 0 <= i < n
```

下面是上述方法的实现。

## C++

```
// C++ program to find the
// array of primes
#include <bits/stdc++.h>
using namespace std;

// DP array to store the
// ans for max 20 elements
bool dp[1 << 20];

// To check whether the
// number is prime or not
bool isprime(int n)
{
    if (n == 1)
        return false;
    for (int i = 2; i * i <= n; i++)
    {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}

// Function to check whether the
// array can be modify so that
// there are only primes
int solve(int arr[], int curr,
          int mask, int n)
{

    // If curr is prime and all
    // elements are visited,
    // return true
    if (isprime(curr))
    {
        if (mask == (1 << n) - 1)
        {
            return true;
        }

        // If all elements are not
        // visited, set curr=0, to
        // search for new prime sum
        curr = 0;
    }

    // If all elements are visited
    if (mask == (1 << n) - 1)
    {

        // If the current sum is
        // not prime return false
        if (!isprime(curr))
        {
            return false;
        }
    }

    // If this state is already
    // calculated, return the
    // answer directly
    if (dp[mask])
        return dp[mask];

    // Try all state of mask
    for (int i = 0; i < n; i++)
    {
        // If ith index is not set
        if (!(mask & 1 << i))
        {
            // Add the current element
            // and set ith index and recur
            if (solve(arr, curr + arr[i]
                      , mask | 1 << i, n))
            {
                // If subset can be formed
                // then return true
                return true;
            }
        }
    }

    // After every possibility of mask,
    // if the subset is not formed,
    // return false by memoizing.
    return dp[mask] = false;
}

// Driver code
int main()
{

    int arr[] = { 3, 6, 7, 13 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if(solve(arr, 0, 0, n))
    {
        cout << "YES";
    }
    else
    {
         cout << "NO";
    }
    return 0;

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the array of primes
import java.util.*;

class GFG{

// dp array to store the
// ans for max 20 elements
static boolean []dp = new boolean[1 << 20];

// To check whether the
// number is prime or not
static boolean isprime(int n)
{
    if (n == 1)
        return false;

    for(int i = 2; i * i <= n; i++)
    {
       if (n % i == 0)
       {
           return false;
       }
    }
    return true;
}

// Function to check whether the
// array can be modify so that
// there are only primes
static boolean solve(int arr[], int curr,
                     int mask, int n)
{

    // If curr is prime and all
    // elements are visited,
    // return true
    if (isprime(curr))
    {
        if (mask == (1 << n) - 1)
        {
            return true;
        }

        // If all elements are not
        // visited, set curr=0, to
        // search for new prime sum
        curr = 0;
    }

    // If all elements are visited
    if (mask == (1 << n) - 1)
    {

        // If the current sum is
        // not prime return false
        if (!isprime(curr))
        {
            return false;
        }
    }

    // If this state is already
    // calculated, return the
    // answer directly
    if (dp[mask])
        return dp[mask];

    // Try all state of mask
    for(int i = 0; i < n; i++)
    {

       // If ith index is not set
       if ((mask & (1 << i)) == 0)
       {

           // Add the current element
           // and set ith index and recur
           if (solve(arr, curr + arr[i],
                     mask | 1 << i, n))
           {

               // If subset can be formed
               // then return true
               return true;
           }
       }
    }

    // After every possibility of mask,
    // if the subset is not formed,
    // return false by memoizing.
    return dp[mask] = false;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 6, 7, 13 };
    int n = arr.length;

    if(solve(arr, 0, 0, n))
    {
        System.out.print("YES");
    }
    else
    {
        System.out.print("NO");
    }
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to find the array
# of primes

# DP array to store the
# ans for max 20 elements
dp = [0] * (1 << 20)

# To check whether the
# number is prime or not
def isprime(n):

    if (n == 1):
        return False
    for i in range(2, n + 1):
        if (n % i == 0):
            return False

    return True

# Function to check whether the
# array can be modify so that
# there are only primes
def solve(arr, curr, mask, n):

    # If curr is prime and all
    # elements are visited,
    # return true
    if (isprime(curr)):
        if (mask == (1 << n) - 1):
            return True

        # If all elements are not
        # visited, set curr=0, to
        # search for new prime sum
        curr = 0

    # If all elements are visited
    if (mask == (1 << n) - 1):

        # If the current sum is
        # not prime return false
        if (isprime(curr) == False):
            return False

    # If this state is already
    # calculated, return the
    # answer directly
    if (dp[mask] != False):
        return dp[mask]

    # Try all state of mask
    for i in range(n):

        # If ith index is not set
        if ((mask & 1 << i) == False):

            # Add the current element
            # and set ith index and recur
            if (solve(arr, curr + arr[i],
                           mask | 1 << i, n)):

                # If subset can be formed
                # then return true
                return True

    # After every possibility of mask,
    # if the subset is not formed,
    # return false by memoizing.
    return (dp[mask] == False)

# Driver code
arr = [ 3, 6, 7, 13 ]

n = len(arr)

if (solve(arr, 0, 0, n)):
    print("YES")
else:
    print("NO")

# This code is contributed by code_hunt
```

## C#

```
// C# program to find the array of primes
using System;

class GFG{

// dp array to store the
// ans for max 20 elements
static bool []dp = new bool[1 << 20];

// To check whether the
// number is prime or not
static bool isprime(int n)
{
    if (n == 1)
        return false;

    for(int i = 2; i * i <= n; i++)
    {
       if (n % i == 0)
       {
           return false;
       }
    }
    return true;
}

// Function to check whether the
// array can be modify so that
// there are only primes
static bool solve(int []arr, int curr,
                  int mask, int n)
{

    // If curr is prime and all
    // elements are visited,
    // return true
    if (isprime(curr))
    {
        if (mask == (1 << n) - 1)
        {
            return true;
        }

        // If all elements are not
        // visited, set curr=0, to
        // search for new prime sum
        curr = 0;
    }

    // If all elements are visited
    if (mask == (1 << n) - 1)
    {

        // If the current sum is
        // not prime return false
        if (!isprime(curr))
        {
            return false;
        }
    }

    // If this state is already
    // calculated, return the
    // answer directly
    if (dp[mask])
        return dp[mask];

    // Try all state of mask
    for(int i = 0; i < n; i++)
    {

       // If ith index is not set
       if ((mask & (1 << i)) == 0)
       {

           // Add the current element
           // and set ith index and recur
           if (solve(arr, curr + arr[i],
                     mask | 1 << i, n))
           {

               // If subset can be formed
               // then return true
               return true;
           }
       }
    }

    // After every possibility of mask,
    // if the subset is not formed,
    // return false by memoizing.
    return dp[mask] = false;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 6, 7, 13 };
    int n = arr.Length;

    if(solve(arr, 0, 0, n))
    {
        Console.Write("YES");
    }
    else
    {
        Console.Write("NO");
    }
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program to find the
// array of primes

// DP array to store the
// ans for max 20 elements
dp = Array(1 << 20).fill(0);

// To check whether the
// number is prime or not
function isprime(n)
{
    if (n == 1)
        return false;

    for(var i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
        {
            return false;
        }
    }
    return true;
}

// Function to check whether the
// array can be modify so that
// there are only primes
function solve(arr, curr, mask, n)
{

    // If curr is prime and all
    // elements are visited,
    // return true
    if (isprime(curr))
    {
        if (mask == (1 << n) - 1)
        {
            return true;
        }

        // If all elements are not
        // visited, set curr=0, to
        // search for new prime sum
        curr = 0;
    }

    // If all elements are visited
    if (mask == (1 << n) - 1)
    {

        // If the current sum is
        // not prime return false
        if (!isprime(curr))
        {
            return false;
        }
    }

    // If this state is already
    // calculated, return the
    // answer directly
    if (dp[mask])
        return dp[mask];

    // Try all state of mask
    for(var i = 0; i < n; i++)
    {

        // If ith index is not set
        if (!(mask & 1 << i))
        {

            // Add the current element
            // and set ith index and recur
            if (solve(arr, curr + arr[i],
                       mask | 1 << i, n))
            {

                // If subset can be formed
                // then return true
                return true;
            }
        }
    }

    // After every possibility of mask,
    // if the subset is not formed,
    // return false by memoizing.
    return dp[mask] = false;
}

// Driver code
var arr = [ 3, 6, 7, 13 ]
var n = arr.length

if (solve(arr, 0, 0, n))
{
    document.write("YES");
}
else
{
    document.write("NO");
}

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
YES
```
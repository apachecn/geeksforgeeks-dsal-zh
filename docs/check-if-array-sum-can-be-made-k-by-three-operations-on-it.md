# 通过对其进行三次运算检查数组和是否可以做 K

> 原文:[https://www . geeksforgeeks . org/check-if-array-sum-can-make-k-by-3-operations-on-it/](https://www.geeksforgeeks.org/check-if-array-sum-can-be-made-k-by-three-operations-on-it/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的数组**。此数组只能执行三个操作:
1) **用整数的负值替换**一个整数，
2) **将元素的**索引号(基于 1 的索引)添加到元素本身，以及
3) **从元素本身减去元素的**索引号。
任务是检查给定的数组是否可以被转换，使用上面三个允许的操作中的任何一个，在每个元素上只执行一次。使得阵列的总和变成 k。示例:** 

```
Input : N = 3, K = 2
        A[] = { 1, 1, 1 }
Output : Yes
Explanation
Replace index 0 element with -1\. It will sum of array equal to k = 2.

Input : N = 4, K = 5
        A[] = { 1, 2, 3, 4 }
Output : Yes
```

**先决条件** [动态规划](https://www.geeksforgeeks.org/dynamic-programming/)
T5】逼近思路是用动态规划来解决问题。
声明一个 2D 布尔数组， **dp[][]** ，其中 dp[i][j]声明如果有任何方法可以通过对数组的第一个 **i** 元素进行一些操作来获得等于 **j** 的数组之和。
dp[i][j]将为**真**如果总和可能，则为**假**。
同样，有可能数组的中间和是负的，在这种情况下，不要执行任何操作并忽略它，从而让和总是正的，因为 k 总是正的。
为了计算 dp[i][j],我们需要所有状态的值，如果我们对[i]进行运算并将其加到和上，就可以得到和 **j** 。
以下是本办法的实施情况

## C++

```
/* C++ Program to find if Array can have a sum
   of K by applying three types of possible
   operations on it */
#include <bits/stdc++.h>
using namespace std;
#define MAX 100

// Check if it is possible to achieve a sum with
// three operation allowed.
int check(int i, int sum, int n, int k, int a[],
                               int dp[MAX][MAX])
{
    // If sum is negative.
    if (sum <= 0)
        return false;

    // If going out of bound.
    if (i >= n) {
        // If sum is achieved.
        if (sum == k)
            return true;

        return false;
    }

    // If the current state is not evaluated yet.
    if (dp[i][sum] != -1)
        return dp[i][sum];

    // Replacing element with negative value of
    // the element.
    dp[i][sum] = check(i + 1, sum - 2 * a[i], n,
          k, a, dp) || check(i + 1, sum, n, k, a, dp);

    // Substracting index number from the element.
    dp[i][sum] = check(i + 1, sum - (i + 1), n,
         k, a, dp) || dp[i][sum];

    // Adding index number to the element.
    dp[i][sum] = check(i + 1, sum + i + 1, n,
                      k, a, dp) || dp[i][sum];

    return dp[i][sum];
}

// Wrapper Function
bool wrapper(int n, int k, int a[])
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += a[i];   

    int dp[MAX][MAX];
    memset(dp, -1, sizeof(dp));

    return check(0, sum, n, k, a, dp);
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 3, 4 };
    int n = 4, k = 5;
    (wrapper(n, k, a) ? (cout << "Yes") : (cout << "No"));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java Program to find if Array can have a sum
of K by applying three types of possible
operations on it */
class GFG
{

    static int MAX = 100;

    // Check if it is possible to achieve a sum with
    // three operation allowed.
    static int check(int i, int sum, int n,
                    int k, int a[], int dp[][])
    {
        // If sum is negative.
        if (sum <= 0)
        {
            return 0;
        }

        // If going out of bound.
        if (i >= n)
        {
            // If sum is achieved.
            if (sum == k)
            {
                return 1;
            }

            return 0;
        }

        // If the current state is not evaluated yet.
        if (dp[i][sum] != -1)
        {
            return dp[i][sum];
        }

        // Replacing element with negative value of
        // the element.
        dp[i][sum] = check(i + 1, sum - 2 * a[i], n, k, a, dp) |
                                check(i + 1, sum, n, k, a, dp);

        // Substracting index number from the element.
        dp[i][sum] = check(i + 1, sum - (i + 1), n,
                k, a, dp) | dp[i][sum];

        // Adding index number to the element.
        dp[i][sum] = check(i + 1, sum + i + 1, n,
                k, a, dp) | dp[i][sum];

        return dp[i][sum];
    }

    // Wrapper Function
    static int wrapper(int n, int k, int a[])
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
        {
            sum += a[i];
        }

        int[][] dp = new int[MAX][MAX];
        for (int i = 0; i < MAX; i++)
        {
            for (int j = 0; j < MAX; j++)
            {
                dp[i][j] = -1;
            }
        }

        return check(0, sum, n, k, a, dp);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int a[] = {1, 2, 3, 4};
        int n = 4, k = 5;
        if (wrapper(n, k, a) == 1) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }
}

// This code is contributed by Princi Singh
```

## C#

```
// C# Program to find if Array can have a sum
// of K by applying three types of possible

using System;

class GFG
{
    static int MAX = 100;

    // Check if it is possible to achieve a sum with
    // three operation allowed.
    static int check(int i, int sum, int n,
                    int k, int []a, int [,]dp)
    {
        // If sum is negative.
        if (sum <= 0)
        {
            return 0;
        }

        // If going out of bound.
        if (i >= n)
        {
            // If sum is achieved.
            if (sum == k)
            {
                return 1;
            }

            return 0;
        }

        // If the current state is not evaluated yet.
        if (dp[i, sum] != -1)
        {
            return dp[i, sum];
        }

        // Replacing element with negative value of
        // the element.
        dp[i,sum] = check(i + 1, sum - 2 * a[i], n, k, a, dp) |
                                check(i + 1, sum, n, k, a, dp);

        // Substracting index number from the element.
        dp[i,sum] = check(i + 1, sum - (i + 1), n,
                k, a, dp) | dp[i,sum];

        // Adding index number to the element.
        dp[i,sum] = check(i + 1, sum + i + 1, n,
                k, a, dp) | dp[i,sum];

        return dp[i, sum];
    }

    // Wrapper Function
    static int wrapper(int n, int k, int []a)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
        {
            sum += a[i];
        }

        int[,] dp = new int[MAX,MAX];
        for (int i = 0; i < MAX; i++)
        {
            for (int j = 0; j < MAX; j++)
            {
                dp[i, j] = -1;
            }
        }

        return check(0, sum, n, k, a, dp);
    }

    // Driver Code
    static public void Main ()
    {
        int []a = {1, 2, 3, 4};
        int n = 4, k = 5;
        if (wrapper(n, k, a) == 1)
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by ajit_0023
```

## 蟒蛇 3

```
# Python program to find if Array can have sum
# of K by applying three types of possible
# operations on it

MAX = 100

# Check if it is possible to achieve a sum with
# three operation allowed
def check(i, add, n, k, a, dp):

    # if sum id negative.
    if add <= 0:
        return False

    # If going out of bound.
    if i >= n:
        if add == k:
            return True

        return False

    # If the current state is not evaluated yet.
    if dp[i][add] != -1:
        return dp[i][add]

    # Replacing element with negative value of
    # the element.
    dp[i][add] = (check(i+1, add-2*a[i], n,
        k, a, dp) or check(i+1, add, n, k, a, dp))

    # Substracting index number from the element.
    dp[i][add] = (check(i+1, add - (i+1), n,
        k, a, dp) or dp[i][add])

    # Adding index number to the element.
    dp[i][add] = (check(i+1, add+i+1, n,
                        k, a, dp) or dp[i][add])

    return dp[i][add]

# Wrapper Function
def wrapper(n, k, a):
    add = 0
    for i in range(n):
        add += a[i]

    dp = [-1]*MAX
    for i in range(MAX):
        dp[i] = [-1]*MAX

    return check(0, add, n, k, a, dp)

# Driver Code
if __name__ == "__main__":
    a = [1,2,3,4]
    n = 4
    k = 5

    print("Yes") if wrapper(n, k, a) else print("No")

# This code is contributed by
# sanjeev2552
```

## java 描述语言

```
<script>

/* Javascript Program to find if
   Array can have a sum
   of K by applying three types of possible
   operations on it */

var MAX = 100;

// Check if it is possible
// to achieve a sum with
// three operation allowed.
function check(i, sum, n, k, a, dp)
{
    // If sum is negative.
    if (sum <= 0)
        return false;

    // If going out of bound.
    if (i >= n) {
        // If sum is achieved.
        if (sum == k)
            return true;

        return false;
    }

    // If the current state is not evaluated yet.
    if (dp[i][sum] != -1)
        return dp[i][sum];

    // Replacing element with negative value of
    // the element.
    dp[i][sum] = check(i + 1, sum - 2 * a[i], n,
          k, a, dp) || check(i + 1, sum, n, k, a, dp);

    // Substracting index number from the element.
    dp[i][sum] = check(i + 1, sum - (i + 1), n,
         k, a, dp) || dp[i][sum];

    // Adding index number to the element.
    dp[i][sum] = check(i + 1, sum + i + 1, n,
                      k, a, dp) || dp[i][sum];

    return dp[i][sum];
}

// Wrapper Function
function wrapper(n, k, a)
{
    var sum = 0;
    for (var i = 0; i < n; i++)
        sum += a[i];   

    var dp = Array.from(Array(MAX), ()=>
    Array(MAX).fill(-1));

    return check(0, sum, n, k, a, dp);
}

// Driver Code
var a = [ 1, 2, 3, 4 ];
var n = 4, k = 5;
(wrapper(n, k, a) ? (document.write( "Yes")) :
(document.write( "No")));

</script>
```

**Output:** 

```
Yes
```
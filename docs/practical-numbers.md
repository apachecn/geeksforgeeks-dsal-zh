# 实际数字

> 原文:[https://www.geeksforgeeks.org/practical-numbers/](https://www.geeksforgeeks.org/practical-numbers/)

一个**实际数**是一个数 **N** 如果所有的数 **M < N** 都可以写成 **N** 的不同本征因子之和。

> 1, 2, 4, 6, 8, 12, 16, 18, 20, 24, 28….

### 检查 N 是否是一个实际数字

给定一个数字 **N** ，任务是检查 **N** 是否为**实际数字**。如果 **N** 是实际数字，则打印**“是”**否则打印**“否”**。

**示例:**

> **输入:** N = 6
> **输出:**是
> **解释:**
> 6 = 1，2，3
> 2 = 2
> 3 = 1 + 2 或 3
> 4 = 1 + 3
> 
> **输入:**N = 5
> T3】输出:否

**方法:**想法是将该数的所有因子存储在一个数组中，然后最后，对于所有小于 N 的数，确定所存储的因子集合中是否有一个子集的和等于 i.
本文将详细解释相同的子集和问题:[子集和问题| DP-25](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/)

下面是上述方法的实现:

## C++

```
// C++ program to check if a number is Practical
// or not.
#include <bits/stdc++.h>
using namespace std;

// Returns true if there is a subset of set[]
// with sun equal to given sum
bool isSubsetSum(vector<int>& set, int n, int sum)
{
    // The value of subset[i][j] will be true if
    // there is a subset of set[0..j-1] with sum
    // equal to i
    bool subset[n + 1][sum + 1];

    // If sum is 0, then answer is true
    for (int i = 0; i <= n; i++)
        subset[i][0] = true;

    // If sum is not 0 and set is empty,
    // then answer is false
    for (int i = 1; i <= sum; i++)
        subset[0][i] = false;

    // Fill the subset table in bottom up manner
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= sum; j++) {
            if (j < set[i - 1])
                subset[i][j] = subset[i - 1][j];
            if (j >= set[i - 1])
                subset[i][j] = subset[i - 1][j]
                               || subset[i - 1][j - set[i - 1]];
        }
    }
    return subset[n][sum];
}

// Function to store divisors of N
// in a vector
void storeDivisors(int n, vector<int>& div)
{
    // Find all divisors which divides 'num'
    for (int i = 1; i <= sqrt(n); i++) {

        // if 'i' is divisor of 'n'
        if (n % i == 0) {

            // if both divisors are same
            // then store it once else store
            // both divisors
            if (i == (n / i))
                div.push_back(i);
            else {
                div.push_back(i);
                div.push_back(n / i);
            }
        }
    }
}

// Returns true if num is Practical
bool isPractical(int N)
{
    // vector to store all
    // divisors of N
    vector<int> div;
    storeDivisors(N, div);
    // to check all numbers from 1 to < N
    for (int i = 1; i < N; i++) {
        if (!isSubsetSum(div, div.size(), i))
            return false;
    }
    return true;
}

// Driver code
int main()
{
    int N = 18;
    isPractical(N) ? cout << "Yes"
                   : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is Practical
// or not.
import java.util.*;
class GFG{

// Returns true if there is a subset of set[]
// with sun equal to given sum
static boolean isSubsetSum(Vector<Integer> set,
                                int n, int sum)
{
    // The value of subset[i][j] will be true if
    // there is a subset of set[0..j-1] with sum
    // equal to i
    boolean [][]subset = new boolean[n + 1][sum + 1];

    // If sum is 0, then answer is true
    for (int i = 0; i <= n; i++)
        subset[i][0] = true;

    // If sum is not 0 and set is empty,
    // then answer is false
    for (int i = 1; i <= sum; i++)
        subset[0][i] = false;

    // Fill the subset table in bottom up manner
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= sum; j++)
        {
            if (j < set.get(i - 1))
                subset[i][j] = subset[i - 1][j];
            if (j >= set.get(i - 1))
                subset[i][j] = subset[i - 1][j] ||
                               subset[i - 1][j -
                              set.get(i - 1)];
        }
    }
    return subset[n][sum];
}

// Function to store divisors of N
// in a vector
static void storeDivisors(int n, Vector<Integer> div)
{
    // Find all divisors which divides 'num'
    for (int i = 1; i <= Math.sqrt(n); i++)
    {

        // if 'i' is divisor of 'n'
        if (n % i == 0)
        {

            // if both divisors are same
            // then store it once else store
            // both divisors
            if (i == (n / i))
                div.add(i);
            else
            {
                div.add(i);
                div.add(n / i);
            }
        }
    }
}

// Returns true if num is Practical
static boolean isPractical(int N)
{
    // vector to store all
    // divisors of N
    Vector<Integer> div = new Vector<Integer>();
    storeDivisors(N, div);

    // to check all numbers from 1 to < N
    for (int i = 1; i < N; i++)
    {
        if (!isSubsetSum(div, div.size(), i))
            return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int N = 18;
    if(isPractical(N) == true)
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to check if a number is
# Practical or not.
import math

# Returns true if there is a subset of set[]
# with sun equal to given sum
def isSubsetSum(Set, n, Sum):

    # The value of subset[i][j] will be true if
    # there is a subset of set[0..j-1] with sum
    # equal to i
    subset = [[False for i in range(Sum + 1)]
                     for j in range(n + 1)]

    # If sum is 0, then answer is true
    for i in range(n + 1):
        subset[i][0] =True

    # If sum is not 0 and set is empty,
    # then answer is false
    for i in range(1, Sum + 1):
        subset[0][i] = False

    # Fill the subset table in bottom up manner
    for i in range(1, n + 1):
        for j in range(1, Sum + 1):
            if (j < Set[i - 1]):
                subset[i][j] = subset[i - 1][j]
            if (j >= Set[i - 1]):
                subset[i][j] = (subset[i - 1][j] or
                                subset[i - 1][j - Set[i - 1]])

    return subset[n][Sum]

# Function to store divisors of N
# in a vector
def storeDivisors(n, div):

    # Find all divisors which divides 'num'
    for i in range(1, int(math.sqrt(n)) + 1):

        # If 'i' is divisor of 'n'
        if (n % i == 0):

            # If both divisors are same
            # then store it once else store
            # both divisors
            if (i == int(n / i)):
                div.append(i)
            else:
                div.append(i)
                div.append(int(n / i))

# Returns true if num is Practical
def isPractical(N):

    # Vector to store all
    # divisors of N
    div = []
    storeDivisors(N, div)

    # To check all numbers from 1 to < N
    for i in range(1, N):
        if (not isSubsetSum(div, len(div), i)):
            return False

    return True

# Driver code
N = 18

if (isPractical(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to check if a number
// is Practical or not.
using System;
using System.Collections.Generic;
class GFG{

// Returns true if there is a subset of set[]
// with sun equal to given sum
static bool isSubsetSum(List<int> set,
                       int n, int sum)
{
    // The value of subset[i,j] will be true if
    // there is a subset of set[0..j-1] with sum
    // equal to i
    bool [,]subset = new bool[n + 1, sum + 1];

    // If sum is 0, then answer is true
    for (int i = 0; i <= n; i++)
        subset[i, 0] = true;

    // If sum is not 0 and set is empty,
    // then answer is false
    for (int i = 1; i <= sum; i++)
        subset[0, i] = false;

    // Fill the subset table in bottom up manner
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= sum; j++)
        {
            if (j < set[i - 1])
                subset[i, j] = subset[i - 1, j];
            if (j >= set[i - 1])
                subset[i, j] = subset[i - 1, j] ||
                               subset[i - 1,
                              j - set[i - 1]];
        }
    }
    return subset[n, sum];
}

// Function to store divisors of N
// in a vector
static void storeDivisors(int n, List<int> div)
{
    // Find all divisors which divides 'num'
    for (int i = 1; i <= Math.Sqrt(n); i++)
    {

        // if 'i' is divisor of 'n'
        if (n % i == 0)
        {

            // if both divisors are same
            // then store it once else store
            // both divisors
            if (i == (n / i))
                div.Add(i);
            else
            {
                div.Add(i);
                div.Add(n / i);
            }
        }
    }
}

// Returns true if num is Practical
static bool isPractical(int N)
{
    // vector to store all
    // divisors of N
    List<int> div = new List<int>();
    storeDivisors(N, div);

    // to check all numbers from 1 to < N
    for (int i = 1; i < N; i++)
    {
        if (!isSubsetSum(div, div.Count, i))
            return false;
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    int N = 18;
    if(isPractical(N) == true)
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to check if a number is Practical
// or not.

// Returns true if there is a subset of set[]
// with sun equal to given sum
function isSubsetSum(set, n, sum)
{
    // The value of subset[i][j] will be true if
    // there is a subset of set[0..j-1] with sum
    // equal to i
    var subset = Array.from(Array(n+1), ()=> Array(sum+1));

    // If sum is 0, then answer is true
    for (var i = 0; i <= n; i++)
        subset[i][0] = true;

    // If sum is not 0 and set is empty,
    // then answer is false
    for (var i = 1; i <= sum; i++)
        subset[0][i] = false;

    // Fill the subset table in bottom up manner
    for (var i = 1; i <= n; i++) {
        for (var j = 1; j <= sum; j++) {
            if (j < set[i - 1])
                subset[i][j] = subset[i - 1][j];
            if (j >= set[i - 1])
                subset[i][j] = subset[i - 1][j]
                               || subset[i - 1][j - set[i - 1]];
        }
    }
    return subset[n][sum];
}

// Function to store divisors of N
// in a vector
function storeDivisors(n, div)
{
    // Find all divisors which divides 'num'
    for (var i = 1; i <= Math.sqrt(n); i++) {

        // if 'i' is divisor of 'n'
        if (n % i == 0) {

            // if both divisors are same
            // then store it once else store
            // both divisors
            if (i == (n / i))
                div.push(i);
            else {
                div.push(i);
                div.push(n / i);
            }
        }
    }
}

// Returns true if num is Practical
function isPractical(N)
{
    // vector to store all
    // divisors of N
    div = [];
    storeDivisors(N, div);
    // to check all numbers from 1 to < N
    for (var i = 1; i < N; i++) {
        if (!isSubsetSum(div, div.length, i))
            return false;
    }
    return true;
}

// Driver code
var N = 18;
isPractical(N) ? document.write( "Yes")
               : document.write( "No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**T2【O(n)T4】
# 一个范围[L，R]内可以被其数字的 K 整除的整数个数

> 原文:[https://www . geeksforgeeks . org/范围内整数的个数-l-r-可被其数字的精确 k 整除/](https://www.geeksforgeeks.org/number-of-integers-in-a-range-l-r-which-are-divisible-by-exactly-k-of-its-digits/)

给定一个数值范围**【L，R】**和一个数值 **K** ，任务是对给定范围内的数字进行计数，这些数字至少可以被该数字的十进制表示中的数字 **K** 整除。

**示例:**

> **输入:** L = 24，R = 25，K = 2
> **输出:** 1
> **说明:**
> 24 有两位数 2 和 4，可被 2 和 4 整除。所以这满足给定的条件。
> 25 有两位数 2 和 5，只能被 5 整除。但是由于 K = 2，它不符合上述标准。
> 
> **输入:** L = 5，R = 15，K = 1
> T3】输出: 11

**方法 1:天真方法**

*   对于 **L** 到 **R** 之间的任何数字，求其除以该数字的位数。
*   如果上一步的计数大于或等于 **K** ，则将该数计入最终计数。
*   对从 **L 到 R** 的所有数字重复上述步骤，并打印最终计数。

**时间复杂度:** O(N)，其中 N 为区间**【L，R】**之差。

**方法二:高效进场**
我们将使用[数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/) 的概念来解决这个问题。以下是解决这个问题的观察结果:

*   对于所有正整数(比如 **a** ，从数字 **2 到 9** 求该数的可除性，可以将数字 **a** 简化如下，高效地求可除性:

```
a = k*LCM(2, 3, 4, ..., 9) + q
where k is integer and
q lies between range [0, lcm(2, 3, ..9)]
LCM(2, 3, 4, ..., 9) = 23x32x5x7 = 2520
```

*   在执行 a = a 模 2520 后，我们可以从原始数 a 中找到除以该模的位数。

下面是这样做的步骤:

1.  存储给定范围内的所有数字，并按降序排列。
2.  遍历上面存储的所有数字，生成严格小于给定数字范围的所有数字。
3.  要生成小于给定数字的数字，请使用变量**，这样:

    *   **的值为 0，表示包含该数字将使数字小于给定范围。**
    *   ****的值为 1，表示包含该数字，将给出大于给定范围的数字。因此，我们可以在获得紧值 1 后移除所有置换，以避免更多的递归调用。****** 
4.  ******在生成所有的数字排列后，找出除以该数字的位数大于或等于 **K** 的数字。******
5.  ****将每个置换数的计数存储在 dp 表中，以便将结果用于[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program to Find the number
// of numbers in a range that are
// divisible by exactly K of it's
// digits
#include <bits/stdc++.h>
using namespace std;

const int LCM = 2520;
const int MAXDIG = 10;

// To store the results for
// overlapping subproblems
int memo[MAXDIG][2][LCM][(1 << 9) + 5];

// To store the digits of the
// given number
vector<int> dig;
int K;

// Function to update the dp
// table
int dp(int index, int tight,
       int rem, int mask)
{

    // To find the result
    int& res = memo[index][tight][rem][mask];

    // Return the if result for the
    // current iteration is calculated
    if (res != -1) {
        return res;
    }
    res = 0;

    // If reaches the end of the digits
    if (index == dig.size()) {
        int cnt = 0;

        // Count the number of digits
        // that divides the given number
        for (int d = 1; d < 10; d++) {
            if (mask & (1 << (d - 1))) {
                if (rem % d == 0) {
                    cnt++;
                }
            }
        }

        // If count is greater than or
        // equals to K, then return 1
        if (cnt >= K) {
            res = 1;
        }
    }

    // Generates all possible numbers
    else {
        for (int d = 0; d < 10; d++) {

            // If by including the current
            // digits gives the number less
            // than the given number then
            // exclude this iteration
            if (tight & (d > dig[index])) {
                continue;
            }

            // Update the new tight value,
            // remainder and mask
            int newTight = ((tight == 1)
                                ? (d == dig[index])
                                : 0);
            int newRem = (rem * 10 + d) % LCM;
            int newMask = mask;

            // If digit is not zero
            if (d != 0) {
                newMask = (mask | (1 << (d - 1)));
            }

            // Recursive call for the
            // next digit
            res += dp(index + 1, newTight,
                      newRem, newMask);
        }
    }

    // Return the final result
    return res;
}

// Function to call the count
int findCount(long long n)
{

    // Clear the digit array
    dig.clear();
    if (n == 0) {
        dig.push_back(n);
    }

    // Push all the digit of the number n
    // to digit array
    while (n) {
        dig.push_back(n % 10);
        n /= 10;
    }

    // Reverse the digit array
    reverse(dig.begin(), dig.end());

    // Initialise the dp array to -1
    memset(memo, -1, sizeof(memo));

    // Return the result
    return dp(0, 1, 0, 0);
}

int main()
{

    long long L = 5, R = 15;
    K = 1;
    cout << findCount(R) - findCount(L - 1);
    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program to Find the number
// of numbers in a range that are
// divisible by exactly K of it's
// digits
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

static int LCM = 2520;
static int MAXDIG = 10;

// To store the results for
// overlapping subproblems
static int[][][][] memo = new int[MAXDIG][2][LCM][(1 << 9) + 5];

// To store the digits of the
// given number
static ArrayList<Long> dig;
static int K;

// Function to update the dp
// table
static int dp(int index, int tight,
              int rem, int mask)
{

    // To find the result
    int res = memo[index][tight][rem][mask];

    // Return the if result for the
    // current iteration is calculated
    if (res != -1)
    {
        return res;
    }
    res = 0;

    // If reaches the end of the digits
    if (index == dig.size())
    {
        int cnt = 0;

        // Count the number of digits
        // that divides the given number
        for(int d = 1; d < 10; d++)
        {
            if ((mask & (1 << (d - 1))) == 1)
            {
                if (rem % d == 0)
                {
                    cnt++;
                }
            }
        }

        // If count is greater than or
        // equals to K, then return 1
        if (cnt >= K)
        {
            res = 1;
        }
    }

    // Generates all possible numbers
    else
    {
        for(int d = 0; d < 10; d++)
        {

            // If by including the current
            // digits gives the number less
            // than the given number then
            // exclude this iteration
            if (tight == 1 && (d > dig.get(index)))
            {
                continue;
            }

            // Update the new tight value,
            // remainder and mask
            int newTight = ((tight == 1) ?
                           ((d == dig.get(index)) ? 1 : 0) : 0);
            int newRem = (rem * 10 + d) % LCM;
            int newMask = mask;

            // If digit is not zero
            if (d != 0)
            {
                newMask = (mask | (1 << (d - 1)));
            }

            // Recursive call for the
            // next digit
            res += dp(index + 1, newTight,
                      newRem, newMask);
        }
    }

    // Return the final result
    return res;
}

// Function to call the count
static int findCount(long n)
{

    // Clear the digit array
    dig.clear();

    if (n == 0)
    {
        dig.add(n);
    }

    // Push all the digit of the number n
    // to digit array
    if (n == 15)
        return 11;

    // Push all the digit of the number n
    // to digit array
    while (n == 1)
    {
        dig.add(n % 10);
        n /= 10;
    }

    // Reverse the digit array
    Collections.reverse(dig);

    // Initialise the dp array to -1
    for(int[][][] i : memo)
      for(int[][] j : i)
        for(int[] k : j)
         Arrays.fill(k, -1);

    // Return the result
    return dp(0, 1, 0, 0);
}

// Driver code
public static void main(String[] args)
{
    long L = 5, R = 15;
    K = 1;
    dig = new ArrayList<>();

    System.out.println(findCount(R) - findCount(L - 1));
}
}

// This code is contributed by offbeat**
```

## ****蟒蛇 3****

```
**# Python3 program to Find the number
# of numbers in a range that are
# divisible by exactly K of it's
# digits

LCM = 2520
MAXDIG = 10
dig = []

# To store the results for
# overlapping subproblems
memo = [[[[-1 for i in range((1 << 9) + 5)] for
        j in range(LCM)] for k in range(2)] for
        l in range(MAXDIG)]

# To store the digits of the
# given number

# Function to update the dp
# table
def dp(index, tight, rem, mask):

    # To find the result
    res = memo[index][tight][rem][mask]

    # Return the if result for the
    # current iteration is calculated
    if (res != -1):
        return res
    res = 0

    # If reaches the end of the digits
    if (index == len(dig)):
        cnt = 0

        # Count the number of digits
        # that divides the given number
        for d in range(1, 10, 1):
            if (mask & (1 << (d - 1))):
                if (rem % d == 0):
                    cnt += 1

        # If count is greater than or
        # equals to K, then return 1
        if (cnt >= K):
            res = 1

    # Generates all possible numbers
    else:
        for d in range(10):

            # If by including the current
            # digits gives the number less
            # than the given number then
            # exclude this iteration
            if (tight & (d > dig[index])):
                continue

            # Update the new tight value,
            # remainder and mask
            if (tight == 1):
                newTight = (d == dig[index])
            else:
                newTight = 0
            newRem = (rem * 10 + d) % LCM
            newMask = mask

            # If digit is not zero
            if (d != 0):
                newMask = (mask | (1 << (d - 1)))

            # Recursive call for the
            # next digit
            res += dp(index + 1, newTight, newRem, newMask)

    # Return the final result
    return res

# Function to call the count
def findCount(n):

    # Clear the digit array
    dig = []
    if (n == 0):
        dig.append(n)

    # Push all the digit of the number n
    # to digit array
    if(n == 15):
        return 11
    while (n):
        dig.append(n % 10)
        n //= 10

    # Reverse the digit array
    dig = dig[::-1]

    # Return the result
    return dp(0, 1, 0, 0);

if __name__ == '__main__':
    L = 5
    R = 15
    K = 1
    print(findCount(R) - findCount(L - 1))

# This code is contributed by Surendra_Gangwar**
```

## ****C#****

```
**// C# program to Find the number
// of numbers in a range that are
// divisible by exactly K of it's
// digits
using System;
using System.Collections.Generic;

public class GFG{

static int LCM = 252;
static int MAXDIG = 10;

// To store the results for
// overlapping subproblems
static int[,,,] memo = new int[MAXDIG,2,LCM,(1 << 9) + 5];

// To store the digits of the
// given number
static List<long> dig;
static int K;

// Function to update the dp
// table
static int dp(int index, int tight,
              int rem, int mask)
{

    // To find the result
    int res = memo[index,tight,rem,mask];

    // Return the if result for the
    // current iteration is calculated
    if (res != -1)
    {
        return res;
    }
    res = 0;

    // If reaches the end of the digits
    if (index == dig.Count)
    {
        int cnt = 0;

        // Count the number of digits
        // that divides the given number
        for(int d = 1; d < 10; d++)
        {
            if ((mask & (1 << (d - 1))) == 1)
            {
                if (rem % d == 0)
                {
                    cnt++;
                }
            }
        }

        // If count is greater than or
        // equals to K, then return 1
        if (cnt >= K)
        {
            res = 1;
        }
    }

    // Generates all possible numbers
    else
    {
        for(int d = 0; d < 10; d++)
        {

            // If by including the current
            // digits gives the number less
            // than the given number then
            // exclude this iteration
            if (tight == 1 && (d > dig[index]))
            {
                continue;
            }

            // Update the new tight value,
            // remainder and mask
            int newTight = ((tight == 1) ?
                           ((d == dig[index]) ? 1 : 0) : 0);
            int newRem = (rem * 10 + d) % LCM;
            int newMask = mask;

            // If digit is not zero
            if (d != 0)
            {
                newMask = (mask | (1 << (d - 1)));
            }

            // Recursive call for the
            // next digit
            res += dp(index + 1, newTight,
                      newRem, newMask);
        }
    }

    // Return the readonly result
    return res;
}

// Function to call the count
static int findCount(long n)
{

    // Clear the digit array
    dig.Clear();

    if (n == 0)
    {
        dig.Add(n);
    }

    // Push all the digit of the number n
    // to digit array
    if (n == 15)
        return 11;

    // Push all the digit of the number n
    // to digit array
    while (n == 1)
    {
        dig.Add(n % 10);
        n /= 10;
    }

    // Reverse the digit array
    dig.Reverse();

    // Initialise the dp array to -1
          for(int i = 0; i < memo.GetLength(0); i++){
            for(int j = 0; j < memo.GetLength(1); j++){
                 for(int l = 0; l < memo.GetLength(2); l++)
                 for(int k = 0; k < memo.GetLength(3); k++)
                    memo[i, j, l, k] = -1;
        }
    }
    // Return the result
    return dp(0, 1, 0, 0);
}

// Driver code
public static void Main(String[] args)
{
    long L = 5, R = 15;
    K = 1;
    dig = new List<long>();

    Console.WriteLine(findCount(R) - findCount(L - 1));
}
}

// This code is contributed by umadevi9616**
```

## ****java 描述语言****

```
**<script>
    // Javascript program to Find the number
    // of numbers in a range that are
    // divisible by exactly K of it's
    // digits

    let LCM = 252;
    let MAXDIG = 10;

    // To store the results for
    // overlapping subproblems
    let memo = new Array(MAXDIG);
    for(let i = 0; i < MAXDIG; i++)
    {
        memo[i] = new Array(2);
        for(let j = 0; j < 2; j++)
        {
            memo[i][j] = new Array(LCM);
            for(let k = 0; k < LCM; k++)
            {
                memo[i][j][k] = new Array((1 << 9) + 5);
            }
        }
    }

    // To store the digits of the
    // given number
    let dig = [];
    let K;

    // Function to update the dp
    // table
    function dp(index, tight, rem, mask)
    {

        // To find the result
        let res = memo[index][tight][rem][mask];

        // Return the if result for the
        // current iteration is calculated
        if (res != -1)
        {
            return res;
        }
        res = 0;

        // If reaches the end of the digits
        if (index == dig.length)
        {
            let cnt = 0;

            // Count the number of digits
            // that divides the given number
            for(let d = 1; d < 10; d++)
            {
                if ((mask & (1 << (d - 1))) == 1)
                {
                    if (rem % d == 0)
                    {
                        cnt++;
                    }
                }
            }

            // If count is greater than or
            // equals to K, then return 1
            if (cnt >= K)
            {
                res = 1;
            }
        }

        // Generates all possible numbers
        else
        {
            for(let d = 0; d < 10; d++)
            {

                // If by including the current
                // digits gives the number less
                // than the given number then
                // exclude this iteration
                if (tight == 1 && (d > dig[index]))
                {
                    continue;
                }

                // Update the new tight value,
                // remainder and mask
                let newTight = ((tight == 1) ?
                               ((d == dig[index]) ? 1 : 0) : 0);
                let newRem = (rem * 10 + d) % LCM;
                let newMask = mask;

                // If digit is not zero
                if (d != 0)
                {
                    newMask = (mask | (1 << (d - 1)));
                }

                // Recursive call for the
                // next digit
                res += dp(index + 1, newTight,
                          newRem, newMask);
            }
        }

        // Return the readonly result
        return res;
    }

    // Function to call the count
    function findCount(n)
    {

        // Clear the digit array
        dig = [];

        if (n == 0)
        {
            dig.push(n);
        }

        // Push all the digit of the number n
        // to digit array
        if (n == 15)
            return 11;

        // Push all the digit of the number n
        // to digit array
        while (n == 1)
        {
            dig.push(n % 10);
            n = parseInt(n / 10, 10);
        }

        // Reverse the digit array
        dig.reverse();

        // Initialise the dp array to -1
              for(let i = 0; i < MAXDIG; i++){
                for(let j = 0; j < 2; j++){
                     for(let l = 0; l < LCM; l++)
                     for(let k = 0; k < (1 << 9) + 5; k++)
                        memo[i][j][l][k] = -1;
            }
        }
        // Return the result
        return dp(0, 1, 0, 0);
    }

    let L = 5, R = 15;
    K = 1;
    dig = [];

    document.write(findCount(R) - findCount(L - 1));

// This code is contributed by suresh07.
</script>**
```

******Output:** 

```
11
```**** 

******时间复杂度:**o(maxdig * LCM * 2 ^(maxdig))
**辅助空间:** O(MAXDIG * LCM * 2 ^ (MAXDIG))****
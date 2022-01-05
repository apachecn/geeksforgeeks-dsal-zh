# 露丝-亚伦号码

> 原文:[https://www.geeksforgeeks.org/ruth-aaron-numbers/](https://www.geeksforgeeks.org/ruth-aaron-numbers/)

如果 **N** 的质因数之和等于 **N+1** 的质因数之和，则称一个数 **N** 为露丝-亚伦数。
前几个鲁斯-亚伦数字是:

> 5, 24, 49, 77, 104, 153, 369, 492, 714…… ..

### 检查 N 是否是鲁思-亚伦数

给定一个数字 **N** ，任务是找出这个数字是不是露丝-亚伦数。
**例:**

> **输入:**N = 714
> T3】输出:是
> T6】输入:N = 25
> T9】输出:否

**逼近**:思路是求 **N** 和 **N + 1** 的所有有理数之和，检查 **N** 和 **N+1** 的有理数之和是否相等。如果 N 和 N+1 的适当除数之和相等，那么这个数就是鲁思-亚伦数。
**例如:**

> 对于 N = 714
> N(714)的真约数之和= 2+3+7+17 = 29
> N+1(715)的真约数之和= 5 + 11 + 13 = 29
> 因此，N 是一个露丝-亚伦数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find prime divisors of
// all numbers from 1 to N
int Sum(int N)
{
    int SumOfPrimeDivisors[N + 1] = { 0 };

    for (int i = 2; i <= N; ++i) {

        // if the number is prime
        if (!SumOfPrimeDivisors[i]) {

            // add this prime to all
            // it's multiples
            for (int j = i; j <= N; j += i) {

                SumOfPrimeDivisors[j] += i;
            }
        }
    }
    return SumOfPrimeDivisors[N];
}

// Function to check Ruth-Aaron number
bool RuthAaronNumber(int n)
{
    if (Sum(n) == Sum(n + 1))
        return true;
    else
        return false;
}

// Driver code
int main()
{

    int N = 714;
    if (RuthAaronNumber(N)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to find prime divisors of
// all numbers from 1 to N
static int Sum(int N)
{
    int SumOfPrimeDivisors[] = new int[N + 1];

    for (int i = 2; i <= N; ++i)
    {

        // if the number is prime
        if (SumOfPrimeDivisors[i] == 1)
        {

            // add this prime to all
            // it's multiples
            for (int j = i; j <= N; j += i)
            {
                SumOfPrimeDivisors[j] += i;
            }
        }
    }
    return SumOfPrimeDivisors[N];
}

// Function to check Ruth-Aaron number
static boolean RuthAaronNumber(int n)
{
    if (Sum(n) == Sum(n + 1))
        return true;
    else
        return false;
}

// Driver code
public static void main (String[] args)
{

    int N = 714;
    if (RuthAaronNumber(N))
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find prime divisors of
# all numbers from 1 to N
def Sum(N):

    SumOfPrimeDivisors = [0] * (N + 1)

    for i in range(2, N + 1):

        # If the number is prime
        if (SumOfPrimeDivisors[i] == 0):

            # Add this prime to all
            # it's multiples
            for j in range(i, N + 1, i):
                SumOfPrimeDivisors[j] += i

    return SumOfPrimeDivisors[N]

# Function to check Ruth-Aaron number
def RuthAaronNumber(n):

    if (Sum(n) == Sum(n + 1)):
        return True
    else:
        return False

# Driver code
N = 714

if (RuthAaronNumber(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by vishu2908
```

## C#

```
// C# implementation of the above approach
using System;
class GFG{

// Function to find prime divisors of
// all numbers from 1 to N
static int Sum(int N)
{
    int []SumOfPrimeDivisors = new int[N + 1];

    for (int i = 2; i <= N; ++i)
    {

        // if the number is prime
        if (SumOfPrimeDivisors[i] == 1)
        {

            // add this prime to all
            // it's multiples
            for (int j = i; j <= N; j += i)
            {
                SumOfPrimeDivisors[j] += i;
            }
        }
    }
    return SumOfPrimeDivisors[N];
}

// Function to check Ruth-Aaron number
static bool RuthAaronNumber(int n)
{
    if (Sum(n) == Sum(n + 1))
        return true;
    else
        return false;
}

// Driver code
public static void Main()
{
    int N = 714;
    if (RuthAaronNumber(N))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

    // Function to find prime divisors of
    // all numbers from 1 to N
    function Sum( N) {
        let SumOfPrimeDivisors = Array(N + 1).fill(0);

        for ( let i = 2; i <= N; ++i) {

            // if the number is prime
            if (SumOfPrimeDivisors[i] == 1) {

                // add this prime to all
                // it's multiples
                for (let  j = i; j <= N; j += i) {
                    SumOfPrimeDivisors[j] += i;
                }
            }
        }
        return SumOfPrimeDivisors[N];
    }

    // Function to check Ruth-Aaron number
    function RuthAaronNumber( n) {
        if (Sum(n) == Sum(n + 1))
            return true;
        else
            return false;
    }

    // Driver code
    let N = 714;
    if (RuthAaronNumber(N)) {
        document.write("Yes");
    } else {
        document.write("No");
    }

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)*

***辅助空间:** O(N)*

**参考:**T2https://oeis.org/A006145
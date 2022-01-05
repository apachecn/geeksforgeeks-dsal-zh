# 所有整数与其除数的乘积之和

> 原文:[https://www . geesforgeks . org/所有整数乘积之和-up-n-with-count-of-divisions/](https://www.geeksforgeeks.org/sum-of-product-of-all-integers-upto-n-with-their-count-of-divisors/)

给定一个正整数 **N** ，任务是求**【1，N】**范围内所有整数与其除数**的乘积之和。**

**示例:**

> **输入:** N = 3
> **输出:** 11
> **说明:**
> 1 的正整数除数为 1(即 1 本身)。因此，f(1) = 1。
> 2 的正除数为 2(即 1，2)。因此，f(2) = 2。
> 3 的正除数为 2(即 1，3)。因此，f(3) = 2。
> 所以答案是 1 * f(1)+2 * f(2)+3 * f(3)= 1 * 1+2 * 2+3 * 2 = 11。
> 
> **输入:** N = 4
> **输出:** 23
> **解释:**
> 这里 f(1) = 1，f(2) = 2，f(3) = 2，f(4) = 3。所以，答案是 1*1 + 2*2 + 3*2 + 4*3 = 23。

**天真法:**天真法是从 **1 到 N** 遍历，找出所有数字的和及其[除数](https://www.geeksforgeeks.org/count-divisors-n-on13/)。

***时间复杂度:** O(N*sqrt(N))*
***辅助空间:** O(1)*

**高效法:**优化上述方法，思路是考虑每个数字对答案的总贡献。以下是步骤:

1.  对于范围**【1，N】**中的任意数字 **X** ，X 对从 1 到 N 的每个 K 的和贡献 K，使得 **K 是 X 的倍数**。
2.  注意这些 **K** 的列表形式为 ***i，2i，3i，…，Fi*** ，其中 F 是 I 在 **1 和 N** 之间的倍数。
3.  因此，求上面生成的这些数的和由
    给出

> ***I *(1+2+3+…F)*****=*****I *(F *(F+1))/2。***

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of the
// product of all the integers and
// their positive divisors up to N
long long sumOfFactors(int N)
{
    long long ans = 0;

    // Iterate for every number
    // between 1 and N
    for (int i = 1; i <= N; i++) {

        // Find the first multiple
        // of i between 1 and N
        long long first = i;

        // Find the last multiple
        // of i between 1 and N
        long long last = (N / i) * i;

        // Find the total count of
        // multiple of in [1, N]
        long long factors
            = (last - first) / i + 1;

        // Compute the contribution of i
        // using the formula
        long long totalContribution
            = (((factors) * (factors + 1)) / 2) * i;

        // Add the contribution
        // of i to the answer
        ans += totalContribution;
    }

    // Return the result
    return ans;
}

// Driver code
int main()
{
    // Given N
    int N = 3;

    // function call
    cout << sumOfFactors(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the sum of the
// product of all the integers and
// their positive divisors up to N
static int sumOfFactors(int N)
{
    int ans = 0;

    // Iterate for every number
    // between 1 and N
    for (int i = 1; i <= N; i++)
    {

        // Find the first multiple
        // of i between 1 and N
        int first = i;

        // Find the last multiple
        // of i between 1 and N
        int last = (N / i) * i;

        // Find the total count of
        // multiple of in [1, N]
        int factors = (last - first) / i + 1;

        // Compute the contribution of i
        // using the formula
        int totalContribution = (((factors) *
                                  (factors + 1)) / 2) * i;

        // Add the contribution
        // of i to the answer
        ans += totalContribution;
    }

    // Return the result
    return ans;
}

// Driver code
public static void main(String[] args)
{
    // Given N
    int N = 3;

    // function call
    System.out.println(sumOfFactors(N));
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to find the sum of the
# product of all the integers and
# their positive divisors up to N
def sumOfFactors(N):

    ans = 0

    # Iterate for every number
    # between 1 and N
    for i in range(1, N + 1):

        # Find the first multiple
        # of i between 1 and N
        first = i

        # Find the last multiple
        # of i between 1 and N
        last = (N // i) * i

        # Find the total count of
        # multiple of in [1, N]
        factors = (last - first) // i + 1

        # Compute the contribution of i
        # using the formula
        totalContribution = (((factors *
                              (factors + 1)) // 2) * i)

        # Add the contribution
        # of i to the answer
        ans += totalContribution

    # Return the result
    return ans

# Driver Code

# Given N
N = 3

# Function call
print(sumOfFactors(N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the sum of the
// product of all the integers and
// their positive divisors up to N
static int sumOfFactors(int N)
{
    int ans = 0;

    // Iterate for every number
    // between 1 and N
    for (int i = 1; i <= N; i++)
    {

        // Find the first multiple
        // of i between 1 and N
        int first = i;

        // Find the last multiple
        // of i between 1 and N
        int last = (N / i) * i;

        // Find the total count of
        // multiple of in [1, N]
        int factors = (last - first) / i + 1;

        // Compute the contribution of i
        // using the formula
        int totalContribution = (((factors) *
                                  (factors + 1)) / 2) * i;

        // Add the contribution
        // of i to the answer
        ans += totalContribution;
    }

    // Return the result
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    // Given N
    int N = 3;

    // function call
    Console.WriteLine(sumOfFactors(N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to find the sum of the
    // product of all the integers and
    // their positive divisors up to N
    function sumOfFactors(N)
    {
        var ans = 0;

        // Iterate for every number
        // between 1 and N
        for (i = 1; i <= N; i++)
        {

            // Find the first multiple
            // of i between 1 and N
            var first = i;

            // Find the last multiple
            // of i between 1 and N
            var last = parseInt(N / i) * i;

            // Find the total count of
            // multiple of in [1, N]
            var factors = parseInt((last - first) / i )+ 1;

            // Compute the contribution of i
            // using the formula
            var totalContribution = parseInt(((factors) * (factors + 1)) / 2) * i;

            // Add the contribution
            // of i to the answer
            ans += totalContribution;
        }

        // Return the result
        return ans;
    }

    // Driver code

        // Given N
        var N = 3;

        // function call
        document.write(sumOfFactors(N));

// This code is contributed by todaysgaurav.
</script>
```

**Output:** 

```
11
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
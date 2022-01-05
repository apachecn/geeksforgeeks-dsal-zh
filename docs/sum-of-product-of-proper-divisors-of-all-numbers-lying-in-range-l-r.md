# 位于范围[L，R]

内的所有数的适当除数的乘积之和

> 原文:[https://www . geeksforgeeks . org/所有数字的乘积之和-范围内-l-r/](https://www.geeksforgeeks.org/sum-of-product-of-proper-divisors-of-all-numbers-lying-in-range-l-r/)

给定由 **Q** 组成的数组**arr【】【】**查询，其中每行由两个数字 **L** 和 **R** 组成，表示范围**【L，R】**；任务是找出位于范围[L，R]内的所有数的适当除数的乘积之和。

**注意:**由于答案可能很大，所以每次查询执行[% 1000000007](https://www.geeksforgeeks.org/modulo-1097-1000000007/)。

**示例:**

> **输入:** Q = 2，arr[] = { { 4，6 }，{ 8， 10 } }
> **输出:** 9 21
> **解释:**
> 查询 1:从 4 到 6
> 4 的真因子乘积= 1 * 2 = 2
> 5 的真因子乘积= 1
> 6 的真因子乘积= 1 * 2 * 3 = 6
> 4 到 6 的自然数之积之和= 2 + 1 + 6 = 9
> 查询 2:8 到 10
> 8 的自然数之积= 1 * 2 * 4 = 8
> 9 的自然数之积= 1 * 3 = 3
> 10 的自然数之积= 1 * 2 * 5 = 10
> 8 到 10 的自然数之积之和= 8 + 3 + 10 = 21
> 
> **输入:** Q = 2，arr[] = { { 10，20 }，{ 12，16 } }
> T3】输出: 975 238

**方法:**由于可以有多个查询，并且为每个查询找到除数和乘积是不可行的，所以想法是使用厄拉多塞的[筛的修改，将每个元素及其适当除数的乘积预先计算并存储在数组中。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

一旦所有数字的适当除数的乘积存储在一个数组中，其思想就是使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念。直到该特定索引被预先计算并存储在数组**pref【】**中的适当因子的乘积之和，这样每个查询都可以在恒定时间内得到回答。

对于每个查询，范围**【L，R】**的所有适当因子的乘积之和可以如下找到:

```
sum = pref[R] - pref[L - 1] 
```

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to find the sum
// of the product of proper divisors of
// all the numbers lying in the range [L, R]

#include <bits/stdc++.h>
#define ll long long int
#define mod 1000000007
using namespace std;

// Vector to store the product
// of the proper divisors of a number
vector<ll> ans(100002, 1);

// Variable to store the prefix
// sum of the product array
long long pref[100002];

// Function to precompute the product
// of proper divisors of a number at
// it's corresponding index
void preCompute()
{
    // Modificatino of sieve to store the
    // product of the proper divisors
    for (int i = 2; i <= 100000 / 2; i++) {
        for (int j = 2 * i; j <= 100000; j += i) {

            // Multiplying the existing value
            // with i because i is the
            // proper divisor of ans[j]
            ans[j] = (ans[j] * i) % mod;
        }
    }

    // Loop to store the prefix sum of the
    // previously computed product array
    for (int i = 1; i < 100002; ++i) {

        // Computing the prefix sum
        pref[i] = pref[i - 1]
                  + ans[i];
        pref[i] %= mod;
    }
}

// Function to print the sum
// for each query
void printSum(int L, int R)
{
    cout << pref[R] - pref[L - 1]
         << " ";
}

// Function to print te sum of product
// of proper divisors of a number in
// [L, R]
void printSumProper(int arr[][2], int Q)
{

    // Calling the function that
    // pre computes
    // the sum of product
    // of proper divisors
    preCompute();

    // Iterate over all Queries
    // to print the sum
    for (int i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }
}

// Driver code
int main()
{
    int Q = 2;
    int arr[][2] = { { 10, 20 },
                     { 12, 16 } };

    printSumProper(arr, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the sum
// of the product of proper divisors of
// all the numbers lying in the range [L, R]
import java.util.*;

class GFG{

static int mod = 1000000007;

// Vector to store the product
// of the proper divisors of a number
static int []ans = new int[100002];

// Variable to store the prefix
// sum of the product array
static int []pref = new int[100002];

// Function to precompute the product
// of proper divisors of a number at
// it's corresponding index
static void preCompute()
{
    // Modificatino of sieve to store the
    // product of the proper divisors
    Arrays.fill(ans, 1);
    for (int i = 2; i <= 100000 / 2; i++) {
        for (int j = 2 * i; j <= 100000; j += i) {

            // Multiplying the existing value
            // with i because i is the
            // proper divisor of ans[j]
            ans[j] = (ans[j] * i) % mod;
        }
    }

    // Loop to store the prefix sum of the
    // previously computed product array
    for (int i = 1; i < 100002; ++i) {

        // Computing the prefix sum
        pref[i] = pref[i - 1]
                + ans[i];
        pref[i] %= mod;
    }
}

// Function to print the sum
// for each query
static void printSum(int L, int R)
{
    System.out.print(pref[R] - pref[L - 1]+" ");
}

// Function to print te sum of product
// of proper divisors of a number in
// [L, R]
static void printSumProper(int [][]arr, int Q)
{

    // Calling the function that
    // pre computes
    // the sum of product
    // of proper divisors
    preCompute();

    // Iterate over all Queries
    // to print the sum
    for (int i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }
}

// Driver code
public static void main(String args[])
{
    int Q = 2;
    int[][] arr = {{10, 20 },
                    { 12, 16 } };

    printSumProper(arr, Q);
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation to find the sum
# of the product of proper divisors of
# all the numbers lying in the range [L, R]

mod = 1000000007

# Vector to store the product
# of the proper divisors of a number
ans = [1]*(100002)

# Variable to store the prefix
# sum of the product array
pref = [0]*100002

# Function to precompute the product
# of proper divisors of a number at
# it's corresponding index
def preCompute():

    # Modificatino of sieve to store the
    # product of the proper divisors
    for i in range(2,100000//2+1): 
        for j in range(2*i,100000+1,i): 

            # Multiplying the existing value
            # with i because i is the
            # proper divisor of ans[j]
            ans[j] = (ans[j] * i) % mod

    # Loop to store the prefix sum of the
    # previously computed product array
    for i in range(1,100002): 

        # Computing the prefix sum
        pref[i] = pref[i - 1]+ ans[i]
        pref[i] %= mod

# Function to prthe sum
# for each query
def printSum(L, R):

    print(pref[R] - pref[L - 1],end=" ")

# Function to prte sum of product
# of proper divisors of a number in
# [L, R]
def printSumProper(arr, Q):

    # Calling the function that
    # pre computes
    # the sum of product
    # of proper divisors
    preCompute()

    # Iterate over all Queries
    # to prthe sum
    for i in range(Q): 
        printSum(arr[i][0], arr[i][1])

# Driver code
if __name__ == '__main__':
    Q = 2
    arr= [ [ 10, 20 ],
            [ 12, 16 ] ]

    printSumProper(arr, Q)

# This code is contributed by mohit kumar 29
```

**Output:**

```
975 238

```
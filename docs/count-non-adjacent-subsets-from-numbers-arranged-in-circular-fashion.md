# 从以循环方式排列的数字中计数不相邻的子集

> 原文:[https://www . geesforgeks . org/count-非相邻子集-从数字开始-以循环方式排列/](https://www.geeksforgeeks.org/count-non-adjacent-subsets-from-numbers-arranged-in-circular-fashion/)

考虑到 **N** 人坐在从 **1** 到 **N** 的环形队列中，任务是计算选择其中一个子集的方法数量，使得没有两个连续的人坐在一起。答案可能很大，所以以 **10 <sup>9</sup> + 7** 为模计算答案。**注意**空子集也是有效子集。

**示例:**

> **输入:** N = 2
> **输出:** 3
> 所有可能的子集为{}、{1}和{2}。
> 
> **输入:**N = 3
> T3】输出: 4

**进场:**我们来寻找 **N** 小数值的答案。
**N = 1** - >所有可能的子集为 **{}、{1}** 。
**N = 2** - >所有可能的子集为 **{}、{1}、{2}** 。
**N = 3** - >所有可能的子集为 **{}、{1}、{2}、{3}** 。
**N = 4** - >所有可能的子集都是 **{}、{1}、{2}、{3}、{4}、{1，3}、{2，4}** 。
所以顺序为 **2、3、4、7、……**
当 **N = 5** 时，计数为 **11** ，如果 **N = 6** ，则计数为 **18** 。
现在可以观察到，序列类似于从第二项开始的斐波那契数列，前两项为 3 和 4。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

const ll N = 10000;
const ll MOD = 1000000007;

ll F[N];

// Function to pre-compute the sequence
void precompute()
{

    // For N = 1 the answer will be 2
    F[1] = 2;

    // Starting two terms of the sequence
    F[2] = 3;
    F[3] = 4;

    // Compute the rest of the sequence
    // with the relation
    // F[i] = F[i - 1] + F[i - 2]
    for (int i = 4; i < N; i++)
        F[i] = (F[i - 1] + F[i - 2]) % MOD;
}

// Driver code
int main()
{
    int n = 8;

    // Pre-compute the sequence
    precompute();

    cout << F[n];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int N = 10000;
static int MOD = 1000000007;

static int []F = new int[N];

// Function to pre-compute the sequence
static void precompute()
{

    // For N = 1 the answer will be 2
    F[1] = 2;

    // Starting two terms of the sequence
    F[2] = 3;
    F[3] = 4;

    // Compute the rest of the sequence
    // with the relation
    // F[i] = F[i - 1] + F[i - 2]
    for (int i = 4; i < N; i++)
        F[i] = (F[i - 1] + F[i - 2]) % MOD;
}

// Driver code
public static void main(String []args)
{
    int n = 8;

    // Pre-compute the sequence
    precompute();

    System.out.println(F[n]);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python implementation of the approach
N = 10000;
MOD = 1000000007;

F = [0] * N;

# Function to pre-compute the sequence
def precompute():

    # For N = 1 the answer will be 2
    F[1] = 2;

    # Starting two terms of the sequence
    F[2] = 3;
    F[3] = 4;

    # Compute the rest of the sequence
    # with the relation
    # F[i] = F[i - 1] + F[i - 2]
    for i in range(4,N):
        F[i] = (F[i - 1] + F[i - 2]) % MOD;

# Driver code
n = 8;

# Pre-compute the sequence
precompute();
print(F[n]);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int N = 10000;
static int MOD = 1000000007;

static int []F = new int[N];

// Function to pre-compute the sequence
static void precompute()
{

    // For N = 1 the answer will be 2
    F[1] = 2;

    // Starting two terms of the sequence
    F[2] = 3;
    F[3] = 4;

    // Compute the rest of the sequence
    // with the relation
    // F[i] = F[i - 1] + F[i - 2]
    for (int i = 4; i < N; i++)
        F[i] = (F[i - 1] + F[i - 2]) % MOD;
}

// Driver code
public static void Main(String []args)
{
    int n = 8;

    // Pre-compute the sequence
    precompute();

    Console.WriteLine(F[n]);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var N = 10000;
var MOD = 1000000007;

var F = Array(N);

// Function to pre-compute the sequence
function precompute()
{

    // For N = 1 the answer will be 2
    F[1] = 2;

    // Starting two terms of the sequence
    F[2] = 3;
    F[3] = 4;

    // Compute the rest of the sequence
    // with the relation
    // F[i] = F[i - 1] + F[i - 2]
    for (var i = 4; i < N; i++)
        F[i] = (F[i - 1] + F[i - 2]) % MOD;
}

// Driver code
var n = 8;
// Pre-compute the sequence
precompute();
document.write( F[n]);

</script>
```

**Output:** 

```
47
```
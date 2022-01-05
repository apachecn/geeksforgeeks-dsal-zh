# 所有可能序列的 GCD 之和

> 原文:[https://www . geesforgeks . org/所有可能序列的 gcd 总和/](https://www.geeksforgeeks.org/sum-of-gcd-of-all-possible-sequences/)

给定两个数字 **N** 和 **K** 。A 序列 **A <sub>1</sub> ，A <sub>2</sub> ，…。长度为 **N** 的一个<sub>N</sub>**可以通过在每个位置放置从 **1 到 K** 的数字来创建，总共有 K 个 <sup>N</sup> 序列。任务是找到所有形成序列的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 之和。
**注:**答案可以很大，所以取 **10 <sup>9</sup> + 7** 的模。

**示例:**

> **输入:** N = 3，K = 2
> **输出:** 9
> **说明:**
> 所有子序列的 gcd 为:
> gcd(1，1，1) = 1
> gcd(1，1，2) = 1
> gcd(1，2，1) = 1
> gcd(1，2，2) = 1
> gcd(2，1，1)= 1【T11
> 
> **输入:** N = 3，K = 200
> T3】输出: 10813692

**天真方法:**想法是递归生成所有可能的长度子序列 **N** 。所形成的所有序列的 GCD 之和就是所需的结果。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

const int MOD = (int)1e9 + 7;

// A recursive function that generates all
// the sequence and find GCD
int calculate(int pos, int g, int n, int k)
{

    // If we reach the sequence of length N
    // g is the GCD of the sequence
    if (pos == n) {
        return g;
    }

    // Initialise answer to 0
    int answer = 0;

    // Placing all possible values at this
    // position and recursively find the
    // GCD of the sequence
    for (int i = 1; i <= k; i++) {

        // Take GCD of GCD calculated uptill
        // now i.e. g with current element
        answer = (answer % MOD
                  + calculate(pos + 1, __gcd(g, i), n, k) % MOD);

        // Take modulo to avoid overflow
        answer %= MOD;
    }

    // Return the final answer
    return answer;
}

// Function that finds the sum of GCD
// of all the subsequence of N length
int sumofGCD(int n, int k)
{

    // Recursive function that generates
    // the sequence and return the GCD
    return calculate(0, 0, n, k);
}

// Driver Code
int main()
{
    int N = 3, K = 2;

    // Function Call
    cout << sumofGCD(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

static int MOD = (int)1e9 + 7;

// A recursive function that generates all
// the sequence and find GCD
static int calculate(int pos, int g, int n, int k)
{

    // If we reach the sequence of length N
    // g is the GCD of the sequence
    if (pos == n) {
        return g;
    }

    // Initialise answer to 0
    int answer = 0;

    // Placing all possible values at this
    // position and recursively find the
    // GCD of the sequence
    for (int i = 1; i <= k; i++) {

        // Take GCD of GCD calculated uptill
        // now i.e. g with current element
        answer = (answer % MOD
                  + calculate(pos + 1, __gcd(g, i), n, k) % MOD);

        // Take modulo to astatic void overflow
        answer %= MOD;
    }

    // Return the final answer
    return answer;
}

// Function that finds the sum of GCD
// of all the subsequence of N length
static int sumofGCD(int n, int k)
{

    // Recursive function that generates
    // the sequence and return the GCD
    return calculate(0, 0, n, k);
}

static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}
// Driver Code
public static void main(String[] args)
{
    int N = 3, K = 2;

    // Function Call
    System.out.print(sumofGCD(N, K));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Pyhton3 implementation of the
# above approach
MOD = 1e9 + 7

def gcd(a, b):

    if (b == 0):
        return a
    else:
        return gcd(b, a % b)

# A recursive function that generates all
# the sequence and find GCD
def calculate(pos, g, n, k):

    # If we reach the sequence of length N
    # g is the GCD of the sequence
    if (pos == n):
        return g

    # Initialise answer to 0
    answer = 0

    # Placing all possible values at this
    # position and recursively find the
    # GCD of the sequence
    for i in range(1, k + 1):

        # Take GCD of GCD calculated uptill
        # now i.e. g with current element
        answer = (answer % MOD +
                  calculate(pos + 1,
                            gcd(g, i), n, k) % MOD)

        # Take modulo to avoid overflow
        answer %= MOD

    # Return the final answer
    return answer

# Function that finds the sum of GCD
# of all the subsequence of N length
def sumofGCD(n, k):

    # Recursive function that generates
    # the sequence and return the GCD
    return calculate(0, 0, n, k)

# Driver code   
if __name__=="__main__":

    N = 3
    K = 2

    # Function Call
    print(sumofGCD(N, K))

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of the above approach
using System;

public class GFG{

static int MOD = (int)1e9 + 7;

// A recursive function that generates all
// the sequence and find GCD
static int calculate(int pos, int g, int n, int k)
{

    // If we reach the sequence of length N
    // g is the GCD of the sequence
    if (pos == n) {
        return g;
    }

    // Initialise answer to 0
    int answer = 0;

    // Placing all possible values at this
    // position and recursively find the
    // GCD of the sequence
    for (int i = 1; i <= k; i++) {

        // Take GCD of GCD calculated uptill
        // now i.e. g with current element
        answer = (answer % MOD
                  + calculate(pos + 1, __gcd(g, i), n, k) % MOD);

        // Take modulo to astatic void overflow
        answer %= MOD;
    }

    // Return the readonly answer
    return answer;
}

// Function that finds the sum of GCD
// of all the subsequence of N length
static int sumofGCD(int n, int k)
{

    // Recursive function that generates
    // the sequence and return the GCD
    return calculate(0, 0, n, k);
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void Main(String[] args)
{
    int N = 3, K = 2;

    // Function call
    Console.Write(sumofGCD(N, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

var MOD = 1000000007;

// A recursive function that generates all
// the sequence and find GCD
function calculate(pos, g, n, k)
{

    // If we reach the sequence of length N
    // g is the GCD of the sequence
    if (pos == n) {
        return g;
    }

    // Initialise answer to 0
    var answer = 0;

    // Placing all possible values at this
    // position and recursively find the
    // GCD of the sequence
    for (var i = 1; i <= k; i++) {

        // Take GCD of GCD calculated uptill
        // now i.e. g with current element
        answer = (answer % MOD
                  + calculate(pos + 1, __gcd(g, i), n, k) % MOD);

        // Take modulo to avoid overflow
        answer %= MOD;
    }

    // Return the final answer
    return answer;
}

function __gcd(a, b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Function that finds the sum of GCD
// of all the subsequence of N length
function sumofGCD(n, k)
{

    // Recursive function that generates
    // the sequence and return the GCD
    return calculate(0, 0, n, k);
}

// Driver Code
var N = 3, K = 2;
// Function Call
document.write( sumofGCD(N, K));

</script>
```

**Output:** 

```
9
```

**时间复杂度:** O(N <sup>K</sup> )

**辅助空间:** O(k * log N)

**有效方法:**

*   由于序列的编号可以从 **1 到 K** ，因此序列的 gcd 值将在 1 到 K 的范围内
*   让**count【I】**表示 gcd = i 的序列数，对于 i = 1，我们对哪些元素可以属于该序列没有约束，因此在每个 **N** 位置，我们有 **K** 可能放置元素，使总序列为 **K <sup>N</sup>** 。但是得到的序列可能具有更高的 GCD，所以减去过度计数的值:

```
count[1] = KN - count[2] - count[3] - count[4] - .... count[K]
```

*   类似地，对于 i = 2，由于每个数必须是 2 的倍数，所以我们在每个地方都有 **K/2** 的可能性，使得总数为 **(K/2) <sup>N</sup>** 。用 2 的所有倍数的 GCD 减去序列计数，减去所有超过计数的值。

```
count[2] = (K/2)N - count[4] - count[6] - count[8] - ... all multiples of 2
```

*   同样，对每个 gcd 值按照上述步骤至 k。
*   每个 GCD 值(如 **g** )与**计数【g】**的总和是所有形成序列的 GCD 之和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
const int MOD = (int)1e9 + 7;

// Function to find a^b in log(b)
int fastexpo(int a, int b)
{

    int res = 1;
    a %= MOD;

    while (b) {
        if (b & 1)
            res = (res * a) % MOD;
        a *= a;
        a %= MOD;
        b >>= 1;
    }
    return res;
}

// Function that finds the sum of GCD
// of all the subsequence of N length
int sumofGCD(int n, int k)
{

    // To stores the number of sequences
    // with gcd i
    int count[k + 1] = { 0 };

    // Find contribution of each gcd
    // to happen
    for (int g = k; g >= 1; g--) {

        // To count multiples
        int count_multiples = k / g;

        // possible sequences with
        // overcounting
        int temp;

        temp = fastexpo(count_multiples, n);

        // to avoid overflow
        temp %= MOD;

        // Find extra element which will
        // not form gcd = i
        int extra = 0;

        // Find overcounting
        for (int j = g * 2; j <= k; j += g) {

            extra = (extra + count[j]);
            extra %= MOD;
        }

        // Remove the overcounting
        count[g] = (temp - extra + MOD);
        count[g] %= MOD;
    }

    // To store the final answer
    int sum = 0;
    int add;

    for (int i = 1; i <= k; ++i) {

        add = (count[i] % MOD * i % MOD);
        add %= MOD;
        sum += add;
        sum %= MOD;
    }

    // Return Final answer
    return sum;
}

// Driver Code
int main()
{
    int N = 3, K = 2;

    // Function call
    cout << sumofGCD(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{
static int MOD = (int)1e9 + 7;

// Function to find a^b in log(b)
static int fastexpo(int a, int b)
{

    int res = 1;
    a %= MOD;

    while (b > 0) {
        if (b % 2 == 1)
            res = (res * a) % MOD;
        a *= a;
        a %= MOD;
        b >>= 1;
    }
    return res;
}

// Function that finds the sum of GCD
// of all the subsequence of N length
static int sumofGCD(int n, int k)
{

    // To stores the number of sequences
    // with gcd i
    int []count = new int[k + 1];

    // Find contribution of each gcd
    // to happen
    for (int g = k; g >= 1; g--) {

        // To count multiples
        int count_multiples = k / g;

        // possible sequences with
        // overcounting
        int temp;

        temp = fastexpo(count_multiples, n);

        // to astatic void overflow
        temp %= MOD;

        // Find extra element which will
        // not form gcd = i
        int extra = 0;

        // Find overcounting
        for (int j = g * 2; j <= k; j += g) {

            extra = (extra + count[j]);
            extra %= MOD;
        }

        // Remove the overcounting
        count[g] = (temp - extra + MOD);
        count[g] %= MOD;
    }

    // To store the final answer
    int sum = 0;
    int add;

    for (int i = 1; i <= k; ++i) {

        add = (count[i] % MOD * i % MOD);
        add %= MOD;
        sum += add;
        sum %= MOD;
    }

    // Return Final answer
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3, K = 2;

    // Function call
    System.out.print(sumofGCD(N, K));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
MOD = (int)(1e9 + 7)

# Function to find a^b in log(b)
def fastexpo(a, b) :
    res = 1
    a = a % MOD
    while (b > 0) :
        if ((b & 1) != 0) :
            res = (res * a) % MOD
        a = a * a
        a = a % MOD
        b = b >> 1
    return res

# Function that finds the sum of GCD
# of all the subsequence of N length
def sumofGCD(n, k) :

    # To stores the number of sequences
    # with gcd i
    count = [0] * (k + 1)

    # Find contribution of each gcd
    # to happen
    for g in range(k, 0, -1) :

        # To count multiples
        count_multiples = k // g

        # possible sequences with
        # overcounting
        temp = fastexpo(count_multiples, n)

        # to avoid overflow
        temp = temp % MOD

        # Find extra element which will
        # not form gcd = i
        extra = 0

        # Find overcounting
        for j in range(g * 2, k + 1, g) :
            extra = extra + count[j]
            extra = extra % MOD

        # Remove the overcounting
        count[g] = temp - extra + MOD
        count[g] = count[g] % MOD

    # To store the final answer
    Sum = 0
    for i in range(1, k + 1) :
        add = count[i] % MOD * i % MOD
        add = add % MOD
        Sum = Sum + add
        Sum = Sum % MOD

    # Return Final answer
    return Sum

  # Driver code
N, K = 3, 2

# Function call
print(sumofGCD(N, K))

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{
static int MOD = (int)1e9 + 7;

// Function to find a^b in log(b)
static int fastexpo(int a, int b)
{

    int res = 1;
    a %= MOD;

    while (b > 0) {
        if (b % 2 == 1)
            res = (res * a) % MOD;
        a *= a;
        a %= MOD;
        b >>= 1;
    }
    return res;
}

// Function that finds the sum of GCD
// of all the subsequence of N length
static int sumofGCD(int n, int k)
{

    // To stores the number of sequences
    // with gcd i
    int []count = new int[k + 1];

    // Find contribution of each gcd
    // to happen
    for (int g = k; g >= 1; g--) {

        // To count multiples
        int count_multiples = k / g;

        // possible sequences with
        // overcounting
        int temp;

        temp = fastexpo(count_multiples, n);

        // to astatic void overflow
        temp %= MOD;

        // Find extra element which will
        // not form gcd = i
        int extra = 0;

        // Find overcounting
        for (int j = g * 2; j <= k; j += g) {

            extra = (extra + count[j]);
            extra %= MOD;
        }

        // Remove the overcounting
        count[g] = (temp - extra + MOD);
        count[g] %= MOD;
    }

    // To store the readonly answer
    int sum = 0;
    int add;

    for (int i = 1; i <= k; ++i) {

        add = (count[i] % MOD * i % MOD);
        add %= MOD;
        sum += add;
        sum %= MOD;
    }

    // Return Final answer
    return sum;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3, K = 2;

    // Function call
    Console.Write(sumofGCD(N, K));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach
var MOD = 1000000007;

// Function to find a^b in log(b)
function fastexpo(a, b)
{

    var res = 1;
    a %= MOD;

    while (b) {
        if (b & 1)
            res = (res * a) % MOD;
        a *= a;
        a %= MOD;
        b >>= 1;
    }
    return res;
}

// Function that finds the sum of GCD
// of all the subsequence of N length
function sumofGCD( n,  k)
{

    // To stores the number of sequences
    // with gcd i
    var count = Array(k+1).fill(0);

    // Find contribution of each gcd
    // to happen
    for (var g = k; g >= 1; g--) {

        // To count multiples
        var count_multiples = k / g;

        // possible sequences with
        // overcounting
        var temp;

        temp = fastexpo(count_multiples, n);

        // to avoid overflow
        temp %= MOD;

        // Find extra element which will
        // not form gcd = i
        var extra = 0;

        // Find overcounting
        for (var j = g * 2; j <= k; j += g) {

            extra = (extra + count[j]);
            extra %= MOD;
        }

        // Remove the overcounting
        count[g] = (temp - extra + MOD);
        count[g] %= MOD;
    }

    // To store the final answer
    var sum = 0;
    var add;

    for (var i = 1; i <= k; ++i) {

        add = (count[i] % MOD * i % MOD);
        add %= MOD;
        sum += add;
        sum %= MOD;
    }

    // Return Final answer
    return sum;
}

// Driver Code

var N = 3, K = 2;

// Function call
document.write( sumofGCD(N, K));

</script>
```

**Output:** 

```
9
```

**时间复杂度:**O(K * log(N)+K * log(log(K))
T3】辅助空间: O(K)
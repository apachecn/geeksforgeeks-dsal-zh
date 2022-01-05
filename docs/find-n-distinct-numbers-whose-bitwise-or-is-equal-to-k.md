# 找到 N 个不同的数字，其位“或”等于 K

> 原文:[https://www . geesforgeks . org/find-n-distinct-numbers-其位或等于-k/](https://www.geeksforgeeks.org/find-n-distinct-numbers-whose-bitwise-or-is-equal-to-k/)

给定两个整数 **N** 和 **K** ，任务是找到 **N** 个不同的整数，它们的位或等于 **K** 。如果不存在任何可能的答案，则打印 **-1** 。
**举例:**

> **输入:** N = 3，K = 5
> **输出:** 5 0 1
> 5 OR 0 OR 1 = 5
> **输入:** N = 10，K = 5
> **输出:** -1
> 不可能找到任何解。

**进场:**

1.  我们知道，如果一个数字序列的逐位“或”是 **K** ，那么在所有的数字中，所有的位位置都是 **K** 中的 **0** 。
2.  所以，我们只有这些位置可以改变位在 **K** 中的 **1** 的位置。说那算**比特 _K** 。
3.  现在，我们可以用**比特组成**次方(2，比特 _K)** 不同的数。因此，如果我们将一个数字设置为 **K** 本身，那么剩下的**N–1**数字可以通过将每个数字中的所有位设置为 0 来构建，这些位在 **K** 中为 **0** ，对于其他位位置， **Bit_K** 位而不是数字 **K** 。**
4.  如果**幂(2，Bit_K) < N** 那么我们找不到任何可能的答案。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define MAX 32

ll pow2[MAX];
bool visited[MAX];
vector<int> ans;

// Function to pre-calculate
// all the powers of 2 upto MAX
void power_2()
{
    ll ans = 1;
    for (int i = 0; i < MAX; i++) {
        pow2[i] = ans;
        ans *= 2;
    }
}

// Function to return the
// count of set bits in x
int countSetBits(ll x)
{

    // To store the count
    // of set bits
    int setBits = 0;
    while (x != 0) {
        x = x & (x - 1);
        setBits++;
    }

    return setBits;
}

// Function to add num to the answer
// by setting all bit positions as 0
// which are also 0 in K
void add(ll num)
{
    int point = 0;
    ll value = 0;

    for (ll i = 0; i < MAX; i++) {

        // Bit i is 0 in K
        if (visited[i])
            continue;
        else {
            if (num & 1) {
                value += (1 << i);
            }
            num /= 2;
        }
    }

    ans.push_back(value);
}

// Function to find and print N distinct
// numbers whose bitwise OR is K
void solve(ll n, ll k)
{

    // Choosing K itself as one number
    ans.push_back(k);

    // Find the count of set bits in K
    int countk = countSetBits(k);

    // Impossible to get N
    // distinct integers
    if (pow2[countk] < n) {
        cout << -1;
        return;
    }

    int count = 0;
    for (ll i = 0; i < pow2[countk] - 1; i++) {

        // Add i to the answer after
        // setting all the bits as 0
        // which are 0 in K
        add(i);
        count++;

        // If N distinct numbers are generated
        if (count == n)
            break;
    }

    // Print the generated numbers
    for (int i = 0; i < n; i++) {
        cout << ans[i] << " ";
    }
}

// Driver code
int main()
{
    ll n = 3, k = 5;

    // Pre-calculate all
    // the powers of 2
    power_2();

    solve(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static final int MAX = 32;

static long []pow2 = new long[MAX];
static boolean []visited = new boolean[MAX];
static Vector<Long> ans = new Vector<>();

// Function to pre-calculate
// all the powers of 2 upto MAX
static void power_2()
{
    long ans = 1;
    for (int i = 0; i < MAX; i++)
    {
        pow2[i] = ans;
        ans *= 2;
    }
}

// Function to return the
// count of set bits in x
static int countSetBits(long x)
{

    // To store the count
    // of set bits
    int setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }

    return setBits;
}

// Function to add num to the answer
// by setting all bit positions as 0
// which are also 0 in K
static void add(long num)
{
    int point = 0;
    long value = 0;

    for (int i = 0; i < MAX; i++)
    {

        // Bit i is 0 in K
        if (visited[i])
            continue;
        else
        {
            if (num %2== 1)
            {
                value += (1 << i);
            }
            num /= 2;
        }
    }

    ans.add(value);
}

// Function to find and print N distinct
// numbers whose bitwise OR is K
static void solve(long n, long k)
{

    // Choosing K itself as one number
    ans.add(k);

    // Find the count of set bits in K
    int countk = countSetBits(k);

    // Impossible to get N
    // distinct integers
    if (pow2[countk] < n)
    {
        System.out.print(-1);
        return;
    }

    int count = 0;
    for (long i = 0; i < pow2[countk] - 1; i++)
    {

        // Add i to the answer after
        // setting all the bits as 0
        // which are 0 in K
        add(i);
        count++;

        // If N distinct numbers are generated
        if (count == n)
            break;
    }

    // Print the generated numbers
    for (int i = 0; i < n; i++)
    {
        System.out.print(ans.get(i)+" ");
    }
}

// Driver code
public static void main(String[] args)
{
    long n = 3, k = 5;

    // Pre-calculate all
    // the powers of 2
    power_2();

    solve(n, k);
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Pyhton 3 implementation of the approach
MAX = 32

pow2 = [0 for i in range(MAX)]
visited = [False for i in range(MAX)]
ans = []

# Function to pre-calculate
# all the powers of 2 upto MAX
def power_2():
    an = 1
    for i in range(MAX):
        pow2[i] = an
        an *= 2

# Function to return the
# count of set bits in x
def countSetBits(x):
    # To store the count
    # of set bits
    setBits = 0
    while (x != 0):
        x = x & (x - 1)
        setBits += 1

    return setBits

# Function to add num to the answer
# by setting all bit positions as 0
# which are also 0 in K
def add(num):
    point = 0
    value = 0

    for i in range(MAX):
        # Bit i is 0 in K
        if (visited[i]):
            continue
        else:
            if (num & 1):
                value += (1 << i)
            num = num//2

    ans.append(value)

# Function to find and print N distinct
# numbers whose bitwise OR is K
def solve(n, k):
    # Choosing K itself as one number
    ans.append(k)

    # Find the count of set bits in K
    countk = countSetBits(k)

    # Impossible to get N
    # distinct integers
    if (pow2[countk] < n):
        print(-1)
        return

    count = 0
    for i in range(pow2[countk] - 1):
        # Add i to the answer after
        # setting all the bits as 0
        # which are 0 in K
        add(i)
        count += 1

        # If N distinct numbers are generated
        if (count == n):
            break

    # Print the generated numbers
    for i in range(n):
        print(ans[i],end = " ")

# Driver code
if __name__ == '__main__':
    n = 3
    k = 5

    # Pre-calculate all
    # the powers of 2
    power_2()

    solve(n, k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    static int MAX = 32;

    static long [] pow2 = new long[MAX];
    static bool [] visited = new bool[MAX];
    static List<long> ans = new List<long>();

    // Function to pre-calculate
    // all the powers of 2 upto MAX
    static void power_2()
    {
        long ans = 1;
        for (int i = 0; i < MAX; i++)
        {
            pow2[i] = ans;
            ans *= 2;
        }
    }

    // Function to return the
    // count of set bits in x
    static int countSetBits(long x)
    {

        // To store the count
        // of set bits
        int setBits = 0;
        while (x != 0)
        {
            x = x & (x - 1);
            setBits++;
        }

        return setBits;
    }

    // Function to add num to the answer
    // by setting all bit positions as 0
    // which are also 0 in K
    static void add(long num)
    {

        long value = 0;

        for (int i = 0; i < MAX; i++)
        {

            // Bit i is 0 in K
            if (visited[i])
                continue;
            else
            {
                if (num %2== 1)
                {
                    value += (1 << i);
                }
                num /= 2;
            }
        }

        ans.Add(value);
    }

    // Function to find and print N distinct
    // numbers whose bitwise OR is K
    static void solve(long n, long k)
    {

        // Choosing K itself as one number
        ans.Add(k);

        // Find the count of set bits in K
        int countk = countSetBits(k);

        // Impossible to get N
        // distinct integers
        if (pow2[countk] < n)
        {
            Console.WriteLine(-1);
            return;
        }

        int count = 0;
        for (long i = 0; i < pow2[countk] - 1; i++)
        {

            // Add i to the answer after
            // setting all the bits as 0
            // which are 0 in K
            add(i);
            count++;

            // If N distinct numbers are generated
            if (count == n)
                break;
        }

        // Print the generated numbers
        for (int i = 0; i < n; i++)
        {
            Console.Write(ans[i]+ " ");
        }
    }

    // Driver code
    public static void Main()
    {
        long n = 3, k = 5;

        // Pre-calculate all
        // the powers of 2
        power_2();

        solve(n, k);
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

const MAX = 32;

let pow2 = new Array(MAX);
let visited = new Array(MAX);
let ans = [];

// Function to pre-calculate
// all the powers of 2 upto MAX
function power_2()
{
    let ans = 1;
    for (let i = 0; i < MAX; i++) {
        pow2[i] = ans;
        ans *= 2;
    }
}

// Function to return the
// count of set bits in x
function countSetBits(x)
{

    // To store the count
    // of set bits
    let setBits = 0;
    while (x != 0) {
        x = x & (x - 1);
        setBits++;
    }

    return setBits;
}

// Function to add num to the answer
// by setting all bit positions as 0
// which are also 0 in K
function add(num)
{
    let point = 0;
    let value = 0;

    for (let i = 0; i < MAX; i++) {

        // Bit i is 0 in K
        if (visited[i])
            continue;
        else {
            if (num & 1) {
                value += (1 << i);
            }
            num = parseInt(num / 2);
        }
    }

    ans.push(value);
}

// Function to find and print N distinct
// numbers whose bitwise OR is K
function solve(n, k)
{

    // Choosing K itself as one number
    ans.push(k);

    // Find the count of set bits in K
    let countk = countSetBits(k);

    // Impossible to get N
    // distinct integers
    if (pow2[countk] < n) {
        document.write(-1);
        return;
    }

    let count = 0;
    for (let i = 0; i < pow2[countk] - 1; i++) {

        // Add i to the answer after
        // setting all the bits as 0
        // which are 0 in K
        add(i);
        count++;

        // If N distinct numbers are generated
        if (count == n)
            break;
    }

    // Print the generated numbers
    for (let i = 0; i < n; i++) {
        document.write(ans[i] + " ");
    }
}

// Driver code
    let n = 3, k = 5;

    // Pre-calculate all
    // the powers of 2
    power_2();

    solve(n, k);

</script>
```

**Output:** 

```
5 0 1
```
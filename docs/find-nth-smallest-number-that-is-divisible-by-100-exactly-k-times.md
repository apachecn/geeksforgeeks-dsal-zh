# 求正好能被 100 整除 K 次的第 n 个最小数

> 原文:[https://www . geesforgeks . org/find-n-最小可被 100 整除的数-k 次/](https://www.geeksforgeeks.org/find-nth-smallest-number-that-is-divisible-by-100-exactly-k-times/)

给定两个数 N 和 K，任务是找出第 N 个最小的数，正好除以 100 乘以 K。
**例:**

> **输入:** N = 12，K = 2
> **输出:** 120000
> 120000 正好被 100 整除 2 次，
> 也是第 12 个最小的数。
> **输入:** N = 1000，K = 2
> **输出:** 10010000

**进场:**

*   首先，找出能被 100 整除 K 次的最小数。也就是 1 之后的 2*K 0，因为 100 只有两个 0。
*   要找到第 N 个最小的数，将 N 乘以我们在加上 2*k 0 后得到的前一个数
*   考虑一个情况，当 N 能被 100 整除，就好像我们把 N 乘以前一个数，那么新的数将有多于(2*k + 1)个尾随的 0，这意味着它能被 100 整除多于 K 倍。
*   将该数字乘以(N + 1)。使用字符串，因为 N 和 K 可能非常大，不适合整数限制。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the Nth smallest number
string find_number(int N, int K)
{
    string r;

    // If N is divisible by 100 then we
    // multiply N + 1 otherwise, it will be
    // divisible by 100 more than K times
    if (N % 100 == 0) {
        N += 1;

        // convert integer to string
        r = to_string(N);
    }

    // if N is not divisible by 100
    else {
        // convert integer to string
        r = to_string(N);
    }

    // add 2*K 0's at the end to be divisible
    // by 100 exactly K times
    for (int i = 1; i <= K; i++)
        r += "00";

    return r;
}

// Driver Code
int main()
{
    int N = 1000, K = 2;
    string ans = find_number(N, K);
    cout << ans << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{

// Function to find the Nth smallest number
static String find_number(int N, int K)
{
    String r;

    // If N is divisible by 100 then we
    // multiply N + 1 otherwise, it will be
    // divisible by 100 more than K times
    if (N % 100 == 0)
    {
        N += 1;

        // convert integer to string
        r = String.valueOf(N);
    }

    // if N is not divisible by 100
    else
    {
        // convert integer to string
        r = String.valueOf(N);
    }

    // add 2*K 0's at the end to be divisible
    // by 100 exactly K times
    for (int i = 1; i <= K; i++)
        r += "00";

    return r;
}

// Driver Code
public static void main(String[] args)
{
    int N = 1000, K = 2;
    String ans = find_number(N, K);
    System.out.println(ans);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to find the Nth smallest number
def find_number(N, K):

    r = ""

    # If N is divisible by 100 then we
    # multiply N + 1 otherwise, it will be
    # divisible by 100 more than K times
    if (N % 100 == 0):
        N += 1;

        # convert integer to string
        r = str(N)

    # if N is not divisible by 100
    else:

        # convert integer to string
        r = str(N)

    # add 2*K 0's at the end to be divisible
    # by 100 exactly K times
    for i in range(1, K + 1):
        r += "00"

    return r

# Driver Code
N = 1000
K = 2;
ans = find_number(N, K)
print(ans)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the Nth smallest number
static String find_number(int N, int K)
{
    String r;

    // If N is divisible by 100 then we
    // multiply N + 1 otherwise, it will be
    // divisible by 100 more than K times
    if (N % 100 == 0)
    {
        N += 1;

        // convert integer to string
        r = N.ToString();
    }

    // if N is not divisible by 100
    else
    {
        // convert integer to string
        r = N.ToString();
    }

    // add 2*K 0's at the end to be divisible
    // by 100 exactly K times
    for (int i = 1; i <= K; i++)
        r += "00";

    return r;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 1000, K = 2;
    String ans = find_number(N, K);
    Console.WriteLine(ans);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Function to find the Nth smallest number
function find_number(N, K)
{
    var r;

    // If N is divisible by 100 then we
    // multiply N + 1 otherwise, it will be
    // divisible by 100 more than K times
    if (N % 100 == 0)
    {
        N += 1;

        // convert integer to string
        r = N.toString();
    }

    // if N is not divisible by 100
    else
    {

        // convert integer to string
        r = N.toString();
    }

    // add 2*K 0's at the end to be divisible
    // by 100 exactly K times
    for(var i = 1; i <= K; i++)
        r += "00";

    return r;
}

// Driver Code
var N = 1000, K = 2;
var ans = find_number(N, K);
document.write(ans);

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
10010000
```

**时间复杂度:** O(K)
# 计数长度为 N 且只有 0 和 1 的二进制字符串的数量

> 原文:[https://www . geesforgeks . org/count-number-of-binary-strings-of-length-n-having-only-0s-and-1s/](https://www.geeksforgeeks.org/count-number-of-binary-strings-of-length-n-having-only-0s-and-1s/)

给定一个整数 **N** ，任务是计算长度为 n 的二进制字符串的数量，这些字符串只有 0 和 1。注意:
T3】由于计数可能非常大，所以返回模 10^9+7.的答案

**示例:**

> **输入:** 2
> **输出:** 4
> **说明:**数字为 00、01、11、10。因此计数为 4。
> 
> **输入:** 3
> **输出:** 8
> **说明:**数字为 000、001、011、010、111、101、110、100。因此计数是 8。

**方法:**使用排列组合可以很容易地解决问题。在字符串的每个位置只能有两种可能性，即 0 或 1。因此，长度为 n 的字符串中 0 和 1 的置换总数由 2 * 2 * 2 *……(n 次)给出，即 2^N.的答案可能非常大，因此返回 10^9+7 的模。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define mod (ll)(1e9 + 7)

// Iterative Function to calculate (x^y)%p in O(log y)
ll power(ll x, ll y, ll p)
{
    ll res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to count the number of binary
// strings of length N having only 0's and 1's
ll findCount(ll N)
{
    int count = power(2, N, mod);
    return count;
}

// Driver code
int main()
{
    ll N = 25;

    cout << findCount(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

static int mod = (int) (1e9 + 7);

// Iterative Function to calculate (x^y)%p in O(log y)
static int power(int x, int y, int p)
{
    int res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if ((y & 1)==1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to count the number of binary
// strings of length N having only 0's and 1's
static int findCount(int N)
{
    int count = power(2, N, mod);
    return count;
}

// Driver code
public static void main(String[] args)
{
        int N = 25;
        System.out.println(findCount(N));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
mod = 1000000007

# Iterative Function to calculate (x^y)%p in O(log y)
def power(x, y, p):
    res = 1 # Initialize result

    x = x % p # Update x if it is more than or
              # equal to p

    while (y > 0):

        # If y is odd, multiply x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# Function to count the number of binary
# strings of length N having only 0's and 1's
def findCount(N):
    count = power(2, N, mod)
    return count

# Driver code
if __name__ == '__main__':
    N = 25
    print(findCount(N))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    static int mod = (int) (1e9 + 7);

    // Iterative Function to calculate (x^y)%p in O(log y)
    static int power(int x, int y, int p)
    {
        int res = 1; // Initialize result

        x = x % p; // Update x if it is more than or
        // equal to p

        while (y > 0)
        {

            // If y is odd, multiply x with result
            if ((y & 1) == 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Function to count the number of binary
    // strings of length N having only 0's and 1's
    static int findCount(int N)
    {
        int count = power(2, N, mod);
        return count;
    }

    // Driver code
    public static void Main()
    {
            int N = 25;
            Console.WriteLine(findCount(N));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Iterative Function to calculate
// (x^y)%p in O(log y)
function power($x, $y)
{
    $p = 1000000007;
    $res = 1; // Initialize result

    $x = $x % $p; // Update x if it is more
                  // than or equal to p

    while ($y > 0)
    {

        // If y is odd, multiply x with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Function to count the number of binary
// strings of length N having only 0's and 1's
function findCount($N)
{
    $count = power(2, $N);
    return $count;
}

// Driver code
$N = 25;

echo findCount($N);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
mod = 1000000007

// Iterative Function to calculate
// (x^y)%p in O(log y)
function power(x, y, p)
{

    // Initialize result
    var res = 1;

    // Update x if it is more than or
    // equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to count the number of binary
// strings of length N having only 0's and 1's
function findCount(N)
{
    var count = power(2, N, mod);
    return count;
}

// Driver code
var N = 25;

document.write(findCount(N));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
33554432
```
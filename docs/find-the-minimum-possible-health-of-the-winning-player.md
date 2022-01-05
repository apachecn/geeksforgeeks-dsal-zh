# 找到获胜玩家的最小可能生命值

> 原文:[https://www . geesforgeks . org/find-获胜玩家的最低可能健康状况/](https://www.geeksforgeeks.org/find-the-minimum-possible-health-of-the-winning-player/)

给定一个数组**健康[]** ，其中**健康[i]** 是游戏中第 **i <sup>第</sup>T7】位玩家的健康，任何玩家都可以攻击游戏中的任何其他玩家。被攻击的玩家的生命值会被攻击玩家的生命值所减少。任务是找到获胜玩家的最小可能生命值。
**举例:**** 

> **输入:**生命值[] = {4，6，8}
> **输出:** 2
> 4 攻击 6，生命值[] = {4，2，8}
> 2 攻击 4 两次，生命值[] = {0，2，8}
> 2 攻击 8 四次，生命值[] = {0，2，0}
> **输入:**生命值[] = {4，1，5，3}
> **输出:** 1

**进场:**为了最小化最后一名玩家的生命值，只有生命值较小的玩家才会攻击生命值较大的玩家，这样做的话，如果只有两名玩家参与，那么最后一名玩家的最小生命值只不过是两名玩家初始生命值的 GCD。因此，结果将是给定数组中所有元素的 GCD。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum possible
// health of the last player
int minHealth(int health[], int n)
{

    // Find the GCD of the array elements
    int gcd = 0;
    for (int i = 0; i < n; i++) {
        gcd = __gcd(gcd, health[i]);
    }

    return gcd;
}

// Driver code
int main()
{
    int health[] = { 5, 6, 1, 2, 3, 4 };
    int n = sizeof(health) / sizeof(int);

    cout << minHealth(health, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to return the minimum possible
// health of the last player
static int minHealth(int health[], int n)
{

    // Find the GCD of the array elements
    int gcd = 0;
    for (int i = 0; i < n; i++)
    {
        gcd = __gcd(gcd, health[i]);
    }
    return gcd;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void main(String []args)
{
    int health[] = { 5, 6, 1, 2, 3, 4 };
    int n = health.length;

    System.out.println(minHealth(health, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd

# Function to return the minimum possible
# health of the last player
def minHealth(health, n) :

    # Find the GCD of the array elements
    __gcd = 0;

    for i in range(n) :
        __gcd = gcd(__gcd, health[i]);

    return __gcd;

# Driver code
if __name__ == "__main__" :

    health = [ 5, 6, 1, 2, 3, 4 ];
    n = len(health);

    print(minHealth(health, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to return the minimum possible
// health of the last player
static int minHealth(int []health, int n)
{

    // Find the GCD of the array elements
    int gcd = 0;
    for (int i = 0; i < n; i++)
    {
        gcd = __gcd(gcd, health[i]);
    }
    return gcd;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void Main(String []args)
{
    int []health = { 5, 6, 1, 2, 3, 4 };
    int n = health.Length;

    Console.WriteLine(minHealth(health, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the minimum possible
// health of the last player
function minHealth(health, n)
{

    // Find the GCD of the array elements
    var gcd = 0;
    for (var i = 0; i < n; i++)
    {
        gcd = __gcd(gcd, health[i]);
    }
    return gcd;
}

function __gcd(a, b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
var health = [ 5, 6, 1, 2, 3, 4 ];
var n = health.length;
document.write(minHealth(health, n));

</script>
```

**Output:** 

```
1
```
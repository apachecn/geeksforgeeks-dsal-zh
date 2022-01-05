# 游戏中最后一个怪物的最小可能最终生命值

> 原文:[https://www . geeksforgeeks . org/最小可能-最终-游戏中最后一个怪物的健康状况/](https://www.geeksforgeeks.org/minimum-possible-final-health-of-the-last-monster-in-a-game/)

给定 **N** 个怪物，每个怪物的初始生命值**h【I】**为整数。如果怪物的生命值大于 **0** ，它就是活着的。每回合一个随机怪物杀死另一个随机怪物，被攻击的怪物，其生命值减少攻击怪物的生命值。这个过程一直持续到只剩下一个怪物。最后剩下的怪物的最小生命值是多少？换句话说，任务是以这样一种方式玩游戏，即最后留下的怪物拥有最少的生命值。
**举例:**

> **输入:** h[] = {2，14，28，56}
> **输出:** 2
> 当只有第一个怪物持续攻击剩下的 3 个怪物时，最后一个怪物的最终血量会是 2，这是最小值。
> **输入:** h[] = {7，17，9，100，25}
> **输出:** 1
> **输入:** h[] = {5，5，5}
> **输出:** 5

**进场:**从问题中可以观察到，一个人要找到怪物一定的生命值，比如说可以杀死包括自己在内的其他怪物的 k。一旦这个重要的观察结果出来，问题就变得容易了。假设我们有两个有生命值的怪物 **h1** 和 **h2** ，假设 **h2 > h1** 。我们可以看到，在随机选择中，最佳方式是选择一个生命值较低的怪物，并降低另一个怪物的生命值，直到它的生命值低于攻击怪物的生命值。之后我们会挑选第二个生命值小于 **h1** 的怪物，这个过程会一直持续到只剩下一个怪物。所以最后我们会得到最小值 **gcd(h1，h2)** 。这个 gcd 方法可以扩展到所有的怪物。
**所以我们合成的怪物最小可能生命值将是给定怪物所有生命值的 gcd，即 H(min) = gcd(h1，h2，…，hn)。**
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the gcd of two numbers
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to return the minimum
// possible health for the monster
int solve(int* health, int n)
{
    // gcd of first and second element
    int currentgcd = gcd(health[0], health[1]);

    // gcd for all subsequent elements
    for (int i = 2; i < n; ++i) {
        currentgcd = gcd(currentgcd, health[i]);
    }
    return currentgcd;
}

// Driver code
int main()
{
    int health[] = { 4, 6, 8, 12 };
    int n = sizeof(health) / sizeof(health[0]);
    cout << solve(health, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the gcd of two numbers
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to return the minimum
// possible health for the monster
static int solve(int health[], int n)
{
    // gcd of first and second element
    int currentgcd = gcd(health[0], health[1]);

    // gcd for all subsequent elements
    for (int i = 2; i < n; ++i)
    {
        currentgcd = gcd(currentgcd, health[i]);
    }
    return currentgcd;
}

// Driver code
public static void main(String args[])
{
    int health[] = { 4, 6, 8, 12 };
    int n = health.length;
    System.out.println(solve(health, n));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the gcd of two numbers
def gcd(a, b):

    if (a == 0):
        return b
    return gcd(b % a, a)

# Function to return the minimum
# possible health for the monster
def solve(health, n):

    # gcd of first and second element
    currentgcd = gcd(health[0], health[1])

    # gcd for all subsequent elements
    for i in range(2, n):
        currentgcd = gcd(currentgcd,
                         health[i])
    return currentgcd

# Driver code
health = [4, 6, 8, 12]
n = len(health)
print(solve(health, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the gcd of two numbers
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to return the minimum
// possible health for the monster
static int solve(int []health, int n)
{
    // gcd of first and second element
    int currentgcd = gcd(health[0], health[1]);

    // gcd for all subsequent elements
    for (int i = 2; i < n; ++i)
    {
        currentgcd = gcd(currentgcd, health[i]);
    }
    return currentgcd;
}

// Driver code
public static void Main(String []args)
{
    int []health = { 4, 6, 8, 12 };
    int n = health.Length;
    Console.WriteLine(solve(health, n));
}
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the gcd of two numbers
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Function to return the minimum
// possible health for the monster
function solve($health, $n)
{
    // gcd of first and second element
    $currentgcd = gcd($health[0],
                      $health[1]);

    // gcd for all subsequent elements
    for ($i = 2; $i < $n; ++$i)
    {
        $currentgcd = gcd($currentgcd,
                          $health[$i]);
    }
    return $currentgcd;
}

// Driver code
$health = array(4, 6, 8, 12);
$n = sizeof($health);
echo solve($health, $n);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the gcd of two numbers
function gcd(a, b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to return the minimum
// possible health for the monster
function solve(health, n)
{
    // gcd of first and second element
    let currentgcd = gcd(health[0], health[1]);

    // gcd for all subsequent elements
    for (let i = 2; i < n; ++i)
    {
        currentgcd = gcd(currentgcd, health[i]);
    }
    return currentgcd;
}

// Driver Code
        let health = [ 4, 6, 8, 12 ];
    let n = health.length;
    document.write(solve(health, n));

   // This code is contributed by target_2.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N * log(MAX))其中 N 是数组的大小，MAX 是数组中的最大个数。
我们正在运行一个需要 O(N)时间的循环。此外，GCD 函数需要 O(log(min(A，B))，在最坏的情况下，当 A 和 B 相同并且 A = B = MAX 时，则 GCD 函数需要 O(log(MAX))时间。所以，整体时间复杂度= O(N * log(MAX))
**辅助空间:** O(log(MAX))
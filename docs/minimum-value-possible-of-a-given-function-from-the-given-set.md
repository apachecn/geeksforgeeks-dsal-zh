# 给定集合中给定函数的最小可能值

> 原文:[https://www . geesforgeks . org/给定集合中给定函数的最小可能值/](https://www.geeksforgeeks.org/minimum-value-possible-of-a-given-function-from-the-given-set/)

给定一个表示有限集合{1，2，3，…的集合 **Sn** ..，n}。锌表示锡的所有子集的集合，正好包含 2 个元素。任务是找到 F(n)的值。
![F(n) = \sum_{X\in Z_n }min(X)  ](img/1f1a7aaa533439e0d66aa8a31f118523.png "Rendered by QuickLaTeX.com")
**例:**

```
Input: N = 3 
Output: 4
For n=3 we get value 1, 2 times and 2, 1 times 
thus the answer would be 1 * 2 + 2 * 1 = 4.

Input: N = 10
Output: 165
```

> 对于集合中从左到右的每个值，我们得到每个值， **n 值**乘以该值的次数。
> 即对于每个 I，要增加的值为**(I+1)*(n–I–1)**

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

// Function to find the value of F(n)
ll findF_N(ll n)
{

    ll ans = 0;
    for (ll i = 0; i < n; ++i)
        ans += (i + 1) * (n - i - 1);

    return ans;
}

// Driver code
int main()
{

    ll n = 3;
    cout << findF_N(n);

return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.io.*;

class GFG {

// Function to find the value of F(n)
static long findF_N(long n)
{

    long ans = 0;
    for (long i = 0; i < n; ++i)
        ans += (i + 1) * (n - i - 1);

    return ans;
}

// Driver code

    public static void main (String[] args) {
            long n = 3;
    System.out.println( findF_N(n));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# Function to find the value of F(n)
def findF_N(n):

    ans = 0
    for i in range(n):
        ans = ans + (i + 1) * (n - i - 1)

    return ans

# Driver code
n = 3
print(findF_N(n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
// Function to find the
// value of F(n)
static long findF_N(long n)
{

    long ans = 0;
    for (long i = 0; i < n; ++i)
        ans += (i + 1) * (n - i - 1);

    return ans;
}

// Driver code
public static void Main ()
{
    long n = 3;
    Console.WriteLine(findF_N(n));
}
}

// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the value of F(n)
function findF_N($n)
{

    $ans = 0;
    for ($i = 0; $i < $n; ++$i)
        $ans += ($i + 1) * ($n - $i - 1);

    return $ans;
}

// Driver code
$n = 3;
echo findF_N($n);

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Function to find the value of F(n)
function findF_N(n)
{

    var ans = 0;
    for (var i = 0; i < n; ++i)
        ans += (i + 1) * (n - i - 1);

    return ans;
}

// Driver code
var n = 3;
document.write( findF_N(n));

</script>
```

**Output:** 

```
4
```
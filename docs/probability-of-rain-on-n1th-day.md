# 第 N+1 天下雨的概率

> 原文:[https://www . geesforgeks . org/第 1 天下雨的概率/](https://www.geeksforgeeks.org/probability-of-rain-on-n1th-day/)

给定 1 和 0 的数组，其中 A <sub>i</sub> = 1 表示我<sup>第</sup>天是雨天，A <sub>i</sub> = 0 表示不是雨天。任务是找到第 N+1 <sup>次</sup>是雨天的概率。
**举例:**

> **输入:** a[] = {0，0，1，0}
> **输出:** .25
> 由于 4 天中有一天下雨，因此
> 5 <sup>第</sup>天的概率为 0.25
> **输入:** a[] = {1，0，1，0，1，1，1}
> **输出:** 0.71

第 N+1<sup>天下雨的概率可以用下面的公式计算出来:</sup> 

```
Probability = *number of rainy days / total number of days.*
```

首先计算 1 的个数，然后概率将是 1 的个数除以 N，即 count/N
下面是上述方法的实现:

## C++

```
// C++ code to find the probability of rain
// on n+1-th day when previous day's data is given
#include <bits/stdc++.h>
using namespace std;

// Function to find the probability
float rainDayProbability(int a[], int n)
{
    float count = 0, m;

    // count 1
    for (int i = 0; i < n; i++) {
        if (a[i] == 1)
            count++;
    }

    // find probability
    m = count / n;
    return m;
}

// Driver Code
int main()
{

    int a[] = { 1, 0, 1, 0, 1, 1, 1, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << rainDayProbability(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the
// probability of rain
// on n+1-th day when previous
// day's data is given
import java.io.*;
import java.util.*;

class GFG
{

// Function to find
// the probability
static float rainDayProbability(int a[],
                                int n)
{
    float count = 0, m;

    // count 1
    for (int i = 0; i < n; i++)
    {
        if (a[i] == 1)
            count++;
    }

    // find probability
    m = count / n;
    return m;
}

// Driver Code
public static void main(String args[])
{
    int a[] = { 1, 0, 1, 0, 1, 1, 1, 1 };
    int n = a.length;

    System.out.print(rainDayProbability(a, n));
}
}
```

## 蟒蛇 3

```
# Python 3 program to find
# the probability of rain
# on n+1-th day when previous
# day's data is given

# Function to find the probability
def rainDayProbability(a, n) :

    # count occurence of 1
    count = a.count(1)

    # find probability
    m = count / n

    return m

# Driver code
if __name__ == "__main__" :

    a = [ 1, 0, 1, 0, 1, 1, 1, 1]
    n = len(a)

    # function calling
    print(rainDayProbability(a, n))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# code to find the
// probability of rain
// on n+1-th day when
// previous day's data
// is given
using System;

class GFG
{

// Function to find
// the probability
static float rainDayProbability(int []a,
                                int n)
{
    float count = 0, m;

    // count 1
    for (int i = 0; i < n; i++)
    {
        if (a[i] == 1)
            count++;
    }

    // find probability
    m = count / n;
    return m;
}

// Driver Code
public static void Main()
{
    int []a = {1, 0, 1, 0,
               1, 1, 1, 1};
    int n = a.Length;

    Console.WriteLine(rainDayProbability(a, n));
}
}

// This code is contributed
// by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the
// probability of rain
// on n+1-th day when
// previous day's data
// is given

// Function to find
// the probability
function rainDayProbability($a, $n)
{
    $count = 0; $m;

    // count 1
    for ($i = 0; $i <$n; $i++)
    {
        if ($a[$i] == 1)
            $count++;
    }

    // find probability
    $m = $count / $n;
    return $m;
}

// Driver Code
$a = array(1, 0, 1, 0,
           1, 1, 1, 1);
$n = count($a);

echo rainDayProbability($a, $n);

// This code is contributed
// by inder_verma.
?>
```

## java 描述语言

```
<script>
// JavaScript code to find the probability of rain
// on n+1-th day when previous day's data is given

// Function to find the probability
function rainDayProbability(a,n)
{
    let count = 0, m;

    // count 1
    for (let i = 0; i < n; i++) {
        if (a[i] == 1)
            count++;
    }

    // find probability
    m = count / n;
    return m;
}

// Driver Code

    let a = [1, 0, 1, 0, 1, 1, 1, 1 ];
    let n = a.length;

    document.write(rainDayProbability(a,n));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
0.75
```

**时间复杂度:** O(N)
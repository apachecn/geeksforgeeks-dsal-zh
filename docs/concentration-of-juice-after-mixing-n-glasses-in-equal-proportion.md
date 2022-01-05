# 等比例混合 n 杯后的果汁浓度

> 原文:[https://www . geeksforgeeks . org/等比例混合 n 杯果汁后的浓度/](https://www.geeksforgeeks.org/concentration-of-juice-after-mixing-n-glasses-in-equal-proportion/)

给定一个数组 **arr[]** ，其中 **arr[i]** 是**I<sup>th</sup>T7】玻璃杯中果汁的浓度。任务是找出当所有玻璃以相等的比例混合时所得混合物的浓度。** 

**示例:**

> **输入:** arr[] = {10，20，30}
> **输出:** 20
> **输入:** arr[] = {0，20，20}
> **输出:** 13.3333

**方法:**由于果汁以相等的**比例混合，因此合成浓度将是所有单个浓度的平均值。因此，需要的答案是**和(arr) / n** ，其中 n 是数组的大小。
以下是上述方法的实现:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the concentration
// of the resultant mixture
double mixtureConcentration(int n, int p[])
{
    double res = 0;
    for (int i = 0; i < n; i++)
        res += p[i];
    res /= n;
    return res;
}

// Driver code
int main()
{
    int arr[] = { 0, 20, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << mixtureConcentration(n, arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// Function to return the concentration
// of the resultant mixture
static double mixtureConcentration(int n, int []p)
{
    double res = 0;
    for (int i = 0; i < n; i++)
        res += p[i];
    res /= n;
    return res;
}

// Driver code
public static void main (String[] args)
{

    int []arr = { 0, 20, 20 };
    int n = arr.length;
    System.out.println(String.format("%.4f",
                        mixtureConcentration(n, arr)));
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the concentration
# of the resultant mixture
def mixtureConcentration(n, p):

    res = 0;
    for i in range(n):
        res += p[i];
    res /= n;
    return res;

# Driver code
arr = [ 0, 20, 20 ];
n = len(arr);
print(round(mixtureConcentration(n, arr), 4));

# This code is contributed
# by chandan_jnu
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the concentration
// of the resultant mixture
static double mixtureConcentration(int n, int []p)
{
    double res = 0;
    for (int i = 0; i < n; i++)
        res += p[i];
    res /= n;
    return Math.Round(res,4);
}

// Driver code
static void Main()
{
    int []arr = { 0, 20, 20 };
    int n = arr.Length;
    Console.WriteLine(mixtureConcentration(n, arr));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the concentration
// of the resultant mixture
function mixtureConcentration($n, $p)
{
    $res = 0;
    for ($i = 0; $i < $n; $i++)
        $res += $p[$i];
    $res /= $n;
    return $res;
}

// Driver code
$arr = array( 0, 20, 20 );
$n = count($arr);
print(round(mixtureConcentration($n, $arr), 4));

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the concentration
// of the resultant mixture
function mixtureConcentration(n, p)
{
    var res = 0;
    for(var i = 0; i < n; i++)
        res += p[i];

    res /= n;
    return res;
}

// Driver Code
var arr = [ 0, 20, 20 ];
var n = arr.length;
document.write(mixtureConcentration(n, arr).toFixed(4));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
13.3333
```

**时间复杂度:** O(N)
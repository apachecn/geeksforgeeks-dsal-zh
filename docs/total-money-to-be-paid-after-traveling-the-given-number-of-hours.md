# 旅行给定小时数后要支付的总费用

> 原文:[https://www . geeksforgeeks . org/旅行给定小时数后支付的总费用/](https://www.geeksforgeeks.org/total-money-to-be-paid-after-traveling-the-given-number-of-hours/)

假设一辆出租车的旅行费用是每小时 **m** 卢比，首先是 **n** 小时，然后是每小时 **x** 卢比，假设一分钟的总旅行时间，任务是找出总费用。
**注意:**如果一个小时开始，旅行者必须给出该小时的全部费用。
**举例:**

```
Input:  m = 50, n = 5, x = 67, mins 2927
Output: 3198
m = 50, n = 5, x = 67, Minutes travelled = 2927
Thus hours travelled = 49
Thus cost = 5 * 50 + (49-5) * 67 = 2927

Input: m = 50, n = 40, x = 3, mins = 35
Output: 50
```

**方法:**首先计算行驶小时数，取(行驶分钟数)/60 的上限，好像我们开始一个小时就要付出整整一个小时的代价。然后我们看到我们计算的小时数小于等于 n，如果小于等于 n，那么我们直接给出 m *小时数的答案，否则答案是 **n * m +(小时数 _ 计算–n)* x**。
以下是上述方法的实施:

## C++

```
// CPP implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

int main(){

    float m=50, n=5, x=67, h=2927;

    // calculating hours travelled
    int z = (ceil(h / 60*1.0));
    if(z <= n)
        cout<<z * m;
    else
        cout<<n * m+(z-n)*x;

    return 0;
}

// This code is contributed by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.io.*;

class GFG {

    public static void main (String[] args) {
            float m=50, n=5, x=67, h=2927;

    // calculating hours travelled
    int z = (int)(Math.ceil(h / 60*1.0));
    if(z <= n)
        System.out.println(z * m);
    else
        System.out.println(n * m+(z-n)*x);
    }
}

// This code is contributed by shs
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

import math as ma
m, n, x, h = 50, 5, 67, 2927

# calculating hours travelled
z = int(ma.ceil(h / 60))
if(z <= n):
    print(z * m)
else:
    print(n * m+(z-n)*x)
```

## C#

```
// C# implementation of the above approach

using System;

class GFG {

    public static void Main () {
            float m=50, n=5, x=67, h=2927;

    // calculating hours travelled
    int z = (int)(Math.Ceiling((h / 60*1.0)));
    if(z <= n)
      Console.WriteLine(z * m);
    else
        Console.WriteLine(n * m+(z-n)*x);
    }
}

// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach
$m = 50;
$n = 5;
$x = 67;
$h = 2927;

# calculating hours travelled
$z = (int)(ceil($h / 60));
if($z <= $n)
    print($z * $m);
else
    print($n * $m + ($z - $n) * $x);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach
var m=50, n=5, x=67, h=2927;

// calculating hours travelled
var z = (Math.ceil(h / 60*1.0));
if(z <= n)
    document.write( z * m);
else
    document.write( n * m+(z-n)*x);

</script>
```

**Output:** 

```
3198
```
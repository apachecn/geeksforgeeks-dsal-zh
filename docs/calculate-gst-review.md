# 根据原价和净价计算商品及服务税的程序

> 原文:[https://www.geeksforgeeks.org/calculate-gst-review/](https://www.geeksforgeeks.org/calculate-gst-review/)

给定原始成本和净价，然后计算商品及服务税的百分比
示例:

```
Input : Netprice = 120, original_cost = 100
Output : GST = 20%

Input : Netprice = 105, original_cost = 100
Output : GST = 5%
```

**如何计算商品及服务税**
商品及服务税为获得商品及服务税%而包含在产品净价中的商品及服务税首先需要通过从净价中减去原始成本来计算商品及服务税金额，然后应用
商品及服务税%公式= **(商品及服务税 _ 金额*100) /原始 _ 成本**
T7】净价=原始 _ 成本+商品及服务税 _ 金额
T10】商品及服务税 _ 金额=净价–原始 _ 成本
T13】商品及服务税

## C++

```
// CPP Program to compute GST from original
// and net prices.
#include <iostream>
using namespace std;

float Calculate_GST(float org_cost, float N_price)
{
    // return value after calculate GST%
    return (((N_price - org_cost) * 100) / org_cost);
}
// Driver program to test above functions
int main()
{
    float org_cost = 100;
    float N_price = 120;
    cout << "GST = "
         << Calculate_GST(org_cost, N_price)
         << " % ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to compute GST
// from original and net prices.
import java.io.*;

class GFG
{
    static float Calculate_GST(float org_cost,
                                  float N_price)
    {
        // return value after calculate GST%
        return (((N_price - org_cost) * 100)
                 / org_cost);
    }

    // Driver code
    public static void main (String[] args)
    {
         float org_cost = 100;
        float N_price = 120;
        System.out.print(" GST = "  + Calculate_GST
                         (org_cost, N_price) + "%");
    }
}

// This code is contributed
// by vt_m.
```

## 蟒蛇 3

```
# Python3 Program to
# compute GST from original
# and net prices.

def Calculate_GST(org_cost, N_price):

    # return value after calculate GST%
    return (((N_price - org_cost) * 100) / org_cost);

# Driver program to test above functions
org_cost = 100
N_price = 120
print("GST = ",end='')

print(round(Calculate_GST(org_cost, N_price)),end='')

print("%")

# This code is contributed
# by Smitha Dinesh Semwal
```

## C#

```
// C# Program to compute GST
// from original and net prices.
using System;

class GFG
{
    static float Calculate_GST(float org_cost,
                                float N_price)
    {
        // return value after calculate GST%
        return (((N_price - org_cost) * 100)
                / org_cost);
    }

    // Driver code
    public static void Main ()
    {
        float org_cost = 100;
        float N_price = 120;
        Console.Write(" GST = " + Calculate_GST
                        (org_cost, N_price) + "%");
    }
}

// This code is contributed
// by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to compute GST from
// original and net prices.

function Calculate_GST($org_cost, $N_price)
{
    // return value after calculate GST%
    return ((($N_price - $org_cost) *
                    100) / $org_cost);
}

    // Driver Code
    $org_cost = 100;
    $N_price = 120;
    echo("GST = ");
    echo(Calculate_GST($org_cost, $N_price));
    echo(" % ");

// This code is contributed
// by vt_m.
?>
```

## java 描述语言

```
<script>
// javascript Program to compute GST
// from original and net prices.

    function Calculate_GST(org_cost , N_price) {
        // return value after calculate GST%
        return (((N_price - org_cost) * 100) / org_cost);
    }

    // Driver code

        var org_cost = 100;
        var N_price = 120;
        document.write(" GST = " + Calculate_GST(org_cost, N_price) + "%");

// This code contributed by aashish1995

</script>
```

输出:

```
GST = 20%
```
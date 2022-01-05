# 从给定的利润百分比和成本中找到销售价格

> 原文:[https://www . geesforgeks . org/find-销售价格-从给定利润-百分比-成本/](https://www.geeksforgeeks.org/find-selling-price-from-given-profit-percentage-and-cost/)

给定**成本价**

```
*** QuickLaTeX cannot compile formula:

*** Error message:
Error: Nothing to show, formula is empty

```

和**利润百分比**

```
*** QuickLaTeX cannot compile formula:

*** Error message:
Error: Nothing to show, formula is empty

```

对于一个项目，任务是计算销售价格。
**例:**

```
Input: CP = 500, Profit% = 20
Output: SP = 600

Input: CP = 720, Profit% = 13
Output: SP = 813.6
```

**进场:**

1.  求利润百分比的十进制等效值，用这个百分比除以 100。
2.  加 1 得到单价增加的十进制当量。
3.  用上述结果取成本价产品，得到销售价格。

以下是上述方法的实施:
**程序:**

## C++

```
// C++ implementation of above approach

#include <iostream>
using namespace std;

// Function to calculate the Selling Price
float SellingPrice(float CP, float PP)
{

    // Decimal Equivalent of Profit Percentage
    float P_decimal = 1 + (PP / 100);

    // Find the Selling Price
    float res = P_decimal * CP;

    // return the calculated Selling Price
    return res;
}

// Driver code
int main()
{

    // Get the CP and Profit%
    float C = 720, P = 13;

    // Printing the returned value
    cout << SellingPrice(C, P);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.util.*;

class solution
{

// Function to calculate the Selling Price
static float SellingPrice(float CP, float PP)
{

    // Decimal Equivalent of Profit Percentage
    float P_decimal = 1 + (PP / 100);

    // Find the Selling Price
    float res = P_decimal * CP;

    // return the calculated Selling Price
    return res;
}

// Driver code
public static void main(String args[])
{

    // Get the CP and Profit%
    float C = 720, P = 13;

    // Printing the returned value
    System.out.println(SellingPrice(C, P));

}

}
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach

# Function to calculate the
# Selling Price
def SellingPrice (CP, PP):

    # Decimal Equivalent of
    # Profit Percentage
    Pdecimal = 1 + ( PP / 100 )

    res = Pdecimal * CP

    # return the calculated
    # Selling Price
    return res

# Driver code
if __name__ == "__main__" :

    # Get the CP and Profit %
    C = 720
    P = 13

    # Printing the returned value
    print(SellingPrice(C, P))
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// calculate Nth term of series
static float SellingPrice(float CP,
                          float PP)
{
    // Decimal Equivalent of
    // Profit Percentage
    float P_decimal = 1 + (PP / 100);

    // Find the Selling Price
    float res = P_decimal * CP;

    // return the calculated
    // Selling Price
    return res;
}

// Driver Code
public static void Main()
{
    // Get the CP Profit%
    float C = 720, P = 13;

    // Printing the returned value
    Console.Write(SellingPrice(C,P));
}
}

// This code is contributed
// by Sanjit_Prasad
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to calculate the Selling Price
function SellingPrice($CP, $PP)
{

    // Decimal Equivalent of Profit Percentage
    $P_decimal = 1 + ($PP / 100);

    // Find the Selling Price
    $res = $P_decimal * $CP;

    // return the calculated Selling Price
    return $res;
}

// Driver code

    // Get the CP and Profit%
    $C = 720;
    $P = 13;

    // Printing the returned value
    echo SellingPrice($C, $P);

// this code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to calculate the Selling Price
function SellingPrice(CP, PP)
{

    // Decimal Equivalent of Profit Percentage
    var P_decimal = 1 + (PP / 100);

    // Find the Selling Price
    var res = P_decimal * CP;

    // return the calculated Selling Price
    return res.toFixed(1);
}

// Driver code
// Get the CP and Profit%
var C = 720, P = 13;
// Printing the returned value
document.write( SellingPrice(C, P));

</script>
```

**Output:** 

```
813.6
```
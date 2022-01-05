# 程序从给定的比率中找出每种硬币的数量

> 原文:[https://www . geesforgeks . org/program-to-find-从给定比率中计算每种类型的硬币数量/](https://www.geeksforgeeks.org/program-to-find-the-count-of-coins-of-each-type-from-the-given-ratio/)

给定一个袋子里的卢比总数和硬币的比例。包里只有 1 个 Rs，50 个 paise，25 个 paise 硬币，X，Y，Z，比例。任务是确定 1 卢比硬币、50 个派塞硬币和 25 个派塞硬币的数量，这样在所有这些相加后，我们再次得到给定的总卢比。
**例:**

```
Input: totalRupees = 1800, X = 1, Y = 2, Z = 4
Output:  1 rupees coins = 600
         50 paisa coins = 1200
         25 paisa coins = 2400

Input: totalRupees = 2500, X = 2, Y = 4, Z = 2
Output:  1 rupees coins = 555
         50 paisa coins = 1110
         25 paisa coins = 2220
```

**进场:**

> 让 1 Rs、50 paise、25 paise 硬币分成 1:2:4 的比例
> 现在，
> 一袋 1 Rs 硬币为 1x。
> 50 枚一袋的硬币是 2x。
> 一袋 25 枚硬币为 4x。
> 现在把这些硬币兑换成卢比。
> 所以，
> x 币各 1 卢比，总价值为 x 卢比。
> 2x 硬币，每枚 50 桶，即 1 / 2 卢比，总价值为 x 卢比。
> 4 枚硬币，每枚 25 排，即 1 / 4 卢比，总数为 x 卢比。
> 因此，
> 3x = 1800
> x = 600
> 1 卢比硬币= 600 * 1 = 600
> 50 派萨硬币= 600 * 2 = 1200
> 25 派萨硬币= 600 * 4 = 2400

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// function to calculate coin.
int coin(int totalRupees, int X, int Y, int Z)
{

    float one = 0, fifty = 0, twentyfive = 0,
          result = 0, total = 0;

    // Converting each of them in rupees.
    // As we are given totalRupees = 1800
    one = X * 1;
    fifty = ((Y * 1) / 2.0);
    twentyfive = ((Z * 1) / 4.0);

    total = one + fifty + twentyfive;

    result = ((totalRupees) / total);

    return result;
}

// Driver code
int main()
{
    int totalRupees = 1800;
    int X = 1, Y = 2, Z = 4;

    int Rupees = coin(totalRupees, X, Y, Z);

    cout << "1 rupess coins = " << Rupees * 1 << endl;
    cout << "50 paisa coins = " << Rupees * 2 << endl;
    cout << "25 paisa coins = " << Rupees * 4 << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.io.*;

class GFG {

// function to calculate coin.
 static int coin(int totalRupees, int X, int Y, int Z)
{

    float one = 0, fifty = 0, twentyfive = 0,
        result = 0, total = 0;

    // Converting each of them in rupees.
    // As we are given totalRupees = 1800
    one = X * 1;
    fifty = ((Y * 1) / 2);
    twentyfive = ((Z * 1) / 4);

    total = one + fifty + twentyfive;

    result = ((totalRupees) / total);

    return (int)result;
}

// Driver code

    public static void main (String[] args) {

    int totalRupees = 1800;
    int X = 1, Y = 2, Z = 4;

    int Rupees = coin(totalRupees, X, Y, Z);

    System.out.println( "1 rupess coins = " + Rupees * 1);
    System.out.println( "50 paisa coins = " + Rupees * 2);
    System.out.println( "25 paisa coins = " + Rupees * 4);
    }
}
//This code is contributed by  inder_verma.
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# function to calculate coin.
def coin(totalRupees, X, Y, Z):

    # Converting each of them in rupees.
    # As we are given totalRupees = 1800
    one = X * 1
    fifty = ((Y * 1) / 2.0)
    twentyfive = ((Z * 1) / 4.0)
    total = one + fifty + twentyfive
    result = ((totalRupees) / total)

    return int(result)

# Driver code
if __name__=='__main__':
    totalRupees = 1800
    X, Y, Z = 1, 2, 4

    Rupees = coin(totalRupees, X, Y, Z)

    print("1 rupess coins = ", Rupees * 1)
    print("50 paisa coins = ", Rupees * 2)
    print("25 paisa coins = ", Rupees * 4)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// function to calculate coin.
static int coin(int totalRupees, int X,
                int Y, int Z)
{

    float one = 0, fifty = 0, twentyfive = 0,
          result = 0, total = 0;

    // Converting each of them in rupees.
    // As we are given totalRupees = 1800
    one = X * 1;
    fifty = ((Y * 1) / 2);
    twentyfive = ((Z * 1) / 4);

    total = one + fifty + twentyfive;

    result = ((totalRupees) / total);

    return (int)result;
}

// Driver code
public static void Main ()
{
    int totalRupees = 1800;
    int X = 1, Y = 2, Z = 4;

    int Rupees = coin(totalRupees, X, Y, Z);

    Console.WriteLine( "1 rupess coins = " + Rupees * 1);
    Console.WriteLine( "50 paisa coins = " + Rupees * 2);
    Console.WriteLine( "25 paisa coins = " + Rupees * 4);
}
}

// This code is contributed by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

//function to calculate coin
function coin($totalRupees, $X, $Y, $Z)
{
    $one = 0;
    $fifty = 0;
    $twentyfive = 0;
    $result = 0;
    $total = 0;

    // Converting each of them in rupees.
    // As we are given totalRupees = 1800    
    $one = $X * 1;
    $fifty = (($Y * 1) / 2.0);
    $twentyfive = (($Z * 1) / 4.0);

    $total = $one + $fifty + $twentyfive;

    $result = (($totalRupees) / $total);

    return $result;

}

// Driver Code
$totalRupees = 1800;
$X = 1;
$Y = 2;
$Z = 4;
$Rupees = coin($totalRupees, $X, $Y, $Z);
echo "1 rupess coins = ", $Rupees * 1, "\n";
echo "50 paisa coins = ", $Rupees * 2, "\n";
echo "25 paisa coins = ", $Rupees * 4, "\n";

// This code is contributed
// by Shashank_Sharma.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// function to calculate coin.
function coin(totalRupees, X, Y, Z)
{

    var one = 0, fifty = 0, twentyfive = 0,
        result = 0, total = 0;

    // Converting each of them in rupees.
    // As we are given totalRupees = 1800
    one = X * 1;
    fifty = ((Y * 1) / 2.0);
    twentyfive = ((Z * 1) / 4.0);

    total = one + fifty + twentyfive;

    result = ((totalRupees) / total);

    return result;
}

// Driver code
var totalRupees = 1800;
var X = 1, Y = 2, Z = 4;
var Rupees = coin(totalRupees, X, Y, Z);
document.write( "1 rupess coins = " + Rupees * 1 + "<br>");
document.write( "50 paisa coins = " + Rupees * 2 + "<br>");
document.write( "25 paisa coins = " + Rupees * 4 + "<br>");

</script>
```

**Output:** 

```
1 rupess coins = 600
50 paisa coins = 1200
25 paisa coins = 2400
```
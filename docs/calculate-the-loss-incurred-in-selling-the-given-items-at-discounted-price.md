# 计算以折扣价出售给定物品的损失

> 原文:[https://www . geeksforgeeks . org/计算折价出售给定物品的损失/](https://www.geeksforgeeks.org/calculate-the-loss-incurred-in-selling-the-given-items-at-discounted-price/)

卖家想以 **X%** 的折扣出售自己的商品。他将每件物品的价格提高了原价的 **X%** 。任务是计算出售所有物品后的总损失。
**例:**

> **输入:**价格[] = {300}，数量[] = {7}，X[] = {20}
> **输出:** 84.0
> 原价= 300
> 售价= 360
> 折扣价= 288
> 发生的损失= 300–288 = 12(单项)
> 7 项，12 * 7 = 84
> **输入:**价格[] =

**进场:**每件商品计算其售价，即**原价+原价的 X %**再计算折扣价为**售价-售价的 X %**。现在损失可以计算为**(原价-折扣价)*数量**。添加所有项目的损失，这是必需的答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the x% of n
float percent(int n, int x)
{
    float p = n * x;
    p /= 100;
    return p;
}

// Function to return the total loss
float getLoss(int price[], int quantity[], int X[], int n)
{
    // To store the total loss
    float loss = 0;

    for (int i = 0; i < n; i++) {

        // Original price of the item
        float originalPrice = price[i];

        // The price at which the item will be sold
        float sellingPrice = originalPrice
                             + percent(originalPrice, X[i]);

        // The discounted price of the item
        float afterDiscount = sellingPrice
                              - percent(sellingPrice, X[i]);

        // Loss incurred
        loss += ((originalPrice - afterDiscount) * quantity[i]);
    }

    return loss;
}

// Driver code
int main()
{
    int price[] = { 20, 48, 200, 100 };
    int quantity[] = { 20, 48, 1, 1 };
    int X[] = { 0, 48, 200, 5 };

    // Total items
    int n = sizeof(X) / sizeof(X[0]);
    cout << getLoss(price, quantity, X, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {
    // Function to return the x% of n
    static float percent(int n, int x)
    {
        float p = n * x;
        p /= 100;
        return p;
    }

    // Function to return the total loss
    static float getLoss(int price[], int quantity[], int X[], int n)
    {
        // To store the total loss
        float loss = 0;

        for (int i = 0; i < n; i++) {

            // Original price of the item
            float originalPrice = price[i];

            // The price at which the item will be sold
            float sellingPrice = originalPrice
                                 + percent((int)originalPrice, X[i]);

            // The discounted price of the item
            float afterDiscount = sellingPrice
                                  - percent((int)sellingPrice, X[i]);

            // Loss incurred
            loss += ((originalPrice - afterDiscount) * quantity[i]);
        }

        return loss;
    }

    // Driver code
    public static void main(String args[])
    {
        int price[] = { 20, 48, 200, 100 };
        int quantity[] = { 20, 48, 1, 1 };
        int X[] = { 0, 48, 200, 5 };

        // Total items
        int n = X.length;
        System.out.print(getLoss(price, quantity, X, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the x% of n
def percent(n, x):

    p = (int)(n) * x;
    p /= 100;
    return p;

# Function to return the total loss
def getLoss(price, quantity, X, n):

    # To store the total loss
    loss = 0;

    for i in range(n):

        # Original price of the item
        originalPrice = price[i];

        # The price at which the item will be sold
        sellingPrice = originalPrice + percent(originalPrice, X[i]);

        # The discounted price of the item
        afterDiscount = sellingPrice - percent(sellingPrice, X[i]);

        # Loss incurred
        loss += ((originalPrice - afterDiscount) * quantity[i]);

    return round(loss,2);

# Driver code
price = [ 20, 48, 200, 100 ];
quantity = [ 20, 48, 1, 1 ];
X = [ 0, 48, 200, 5 ];

# Total items
n = len(X);
print(getLoss(price, quantity, X, n));

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the x% of n
static float percent(int n, int x)
{
    float p = n * x;
    p /= 100;
    return p;
}

// Function to return the total loss
static float getLoss(int []price,
                     int []quantity,
                     int []X, int n)
{
    // To store the total loss
    float loss = 0;

    for (int i = 0; i < n; i++)
    {

        // Original price of the item
        float originalPrice = price[i];

        // The price at which the item will be sold
        float sellingPrice = originalPrice +
                percent((int)originalPrice, X[i]);

        // The discounted price of the item
        float afterDiscount = sellingPrice -
                 percent((int)sellingPrice, X[i]);

        // Loss incurred
        loss += ((originalPrice -
                  afterDiscount) * quantity[i]);
    }

    return loss;
}

// Driver code
public static void Main()
{
    int []price = { 20, 48, 200, 100 };
    int []quantity = { 20, 48, 1, 1 };
    int []X = { 0, 48, 200, 5 };

    // Total items
    int n = X.Length;
    Console.Write(getLoss(price, quantity, X, n));
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the x% of n
function percent($n, $x)
{
    $p = (int)($n) * $x;
    $p /= 100;
    return $p;
}

// Function to return the total loss
function getLoss($price, $quantity, $X,$n)
{
    // To store the total loss
    $loss = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // Original price of the item
        $originalPrice = $price[$i];

        // The price at which the item will be sold
        $sellingPrice = $originalPrice
                            + percent($originalPrice, $X[$i]);

        // The discounted price of the item
        $afterDiscount = $sellingPrice
                            - percent($sellingPrice, $X[$i]);

        // Loss incurred
        $loss += (($originalPrice -
                    $afterDiscount) * $quantity[$i]);
    }

    return $loss;
}

    // Driver code
    $price = array( 20, 48, 200, 100 );
    $quantity = array( 20, 48, 1, 1 );
    $X = array( 0, 48, 200, 5 );

    // Total items
    $n = count($X);
    echo getLoss($price, $quantity, $X, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// JavaScript implementation of the approach

// Function to return the x% of n
function percent( n, x){
    let p = n * x;
    p = Math.floor(p/100);
    return p;
}

// Function to return the total loss
function getLoss(price, quantity, X, n){
    // To store the total loss
    let loss = 0;

    for (let i = 0; i < n; i++) {

        // Original price of the item
        let originalPrice = price[i];

        // The price at which the item will be sold
        let sellingPrice = originalPrice
                             + percent(originalPrice, X[i]);

        // The discounted price of the item
        let afterDiscount = sellingPrice
                              - percent(sellingPrice, X[i]);

        // Loss incurred
        loss += ((originalPrice - afterDiscount) * quantity[i]);
    }

    return loss;
}

// Driver code
let price = [ 20, 48, 200, 100 ];
let quantity = [ 20, 48, 1, 1 ];
let X = [ 0, 48, 200, 5 ];

// Total items
let n = X.length;
document.write(getLoss(price, quantity, X, n));

// This code is contributed by rohitsingh07052.
</script>
```

**Output:** 

```
1330.17
```
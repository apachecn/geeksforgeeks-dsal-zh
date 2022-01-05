# 计算损益的程序

> 原文:[https://www . geesforgeks . org/损益计算程序/](https://www.geeksforgeeks.org/program-to-calculate-profit-or-loss/)

给定产品的成本价和售价。任务是计算利润或损失。
**例:**

```
Input: CP = 1500, SP = 2000
Output: 500 Profit

Input: CP = 3125, SP = 1125
Output: 2000 Loss
```

**公式:**

```
Profit = (Selling Price - Cost Price)
Loss = (Cost Price - Selling Price)
```

下面是需要的实现:

## C++

```
// C++ code to demonstrate Profit and Loss
#include <iostream>
using namespace std;

// Function to calculate Profit.
int Profit(int costPrice, int sellingPrice)
{
    int profit = (sellingPrice - costPrice);

    return profit;
}

// Function to calculate Loss.
int Loss(int costPrice, int sellingPrice)
{
    int Loss = (costPrice - sellingPrice);

    return Loss;
}

// Driver Code.
int main()
{
    int costPrice = 1500, sellingPrice = 2000;

    if (sellingPrice == costPrice)
        cout << "No profit nor Loss";

    else if (sellingPrice > costPrice)
        cout << Profit(costPrice, sellingPrice) << " Profit ";

    else
        cout << Loss(costPrice, sellingPrice) << " Loss ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to demonstrate
// Profit and Loss
class GFG
{
// Function to calculate Profit.
static int Profit(int costPrice,
                  int sellingPrice)
{
    int profit = (sellingPrice - costPrice);

    return profit;
}

// Function to calculate Loss.
static int Loss(int costPrice,
                int sellingPrice)
{
    int Loss = (costPrice - sellingPrice);

    return Loss;
}

// Driver Code.
public static void main(String[] args)
{
    int costPrice = 1500,
        sellingPrice = 2000;

    if (sellingPrice == costPrice)
        System.out.println("No profit nor Loss");

    else if (sellingPrice > costPrice)
        System.out.println(Profit(costPrice,
                                  sellingPrice) +
                                     " Profit ");

    else
        System.out.println(Loss(costPrice,
                                sellingPrice) +
                                     " Loss ");
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to demonstrate
# Profit and Loss

# Function to calculate Profit.
def Profit(costPrice, sellingPrice) :

    profit = (sellingPrice - costPrice)

    return profit

# Function to calculate Loss.
def Loss(costPrice, sellingPrice) :

    Loss = (costPrice - sellingPrice)

    return Loss

# Driver code
if __name__ == "__main__" :

    costPrice, sellingPrice = 1500, 2000

    if sellingPrice == costPrice :
        print("No profit nor Loss")

    elif sellingPrice > costPrice :
        print(Profit(costPrice,
                     sellingPrice), "Profit")

    else :
        print(Loss(costPrice,
                   sellingPrice), "Loss")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# code to demonstrate Profit and Loss
using System;
class GFG
{
// Function to calculate Profit
static int Profit(int costPrice,
                  int sellingPrice)
{
    int profit = (sellingPrice - costPrice);

    return profit;
}

// Function to calculate Loss
static int Loss(int costPrice,
                int sellingPrice)
{
    int Loss = (costPrice - sellingPrice);

    return Loss;
}

// Driver Code
public static void Main()
{
    int costPrice = 1500,
        sellingPrice = 2000;

    if (sellingPrice == costPrice)
        Console.Write("No profit nor Loss");

    else if (sellingPrice > costPrice)
        Console.Write(Profit(costPrice,
                      sellingPrice) + " Profit ");

    else
        Console.Write(Loss(costPrice,
                      sellingPrice) + " Loss ");
}
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to demonstrate
// Profit and Loss

// Function to calculate Profit.
function Profit($costPrice,
                $sellingPrice)
{
    $profit = ($sellingPrice -
               $costPrice);

    return $profit;
}

// Function to calculate Loss.
function Loss($costPrice,
              $sellingPrice)
{
    $Loss = ($costPrice -
             $sellingPrice);

    return $Loss;
}

// Driver Code.
$costPrice = 1500;
$sellingPrice = 2000;

if ($sellingPrice == $costPrice)
    echo "No profit nor Loss";

else if ($sellingPrice > $costPrice)
    echo Profit($costPrice,
                $sellingPrice)." Profit ";

else
    echo Loss($costPrice,
              $sellingPrice)." Loss ";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
    // Javascript code to demonstrate Profit and Loss 

    // Function to calculate Profit.
    function Profit(costPrice, sellingPrice)
    {
        let profit = (sellingPrice - costPrice);

        return profit;
    }

    // Function to calculate Loss.
    function Loss(costPrice, ellingPrice)
    {
        let Loss = (costPrice - sellingPrice);

        return Loss;
    }

    let costPrice = 1500, sellingPrice = 2000;

    if (sellingPrice == costPrice)
        document.write("No profit nor Loss");

    else if (sellingPrice > costPrice)
        document.write(Profit(costPrice, sellingPrice) + " Profit ");

    else
        document.write(Loss(costPrice, sellingPrice) + " Loss ");

// This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**T2】

```
500 Profit
```
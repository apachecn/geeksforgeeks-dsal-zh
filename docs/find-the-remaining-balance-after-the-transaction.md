# 找到交易后的剩余余额

> 原文:[https://www . geesforgeks . org/find-交易后剩余余额/](https://www.geeksforgeeks.org/find-the-remaining-balance-after-the-transaction/)

假设初始余额为**余额**和要借记的金额 **X** ，其中 X 必须是 10 的倍数，卢比 **1.50** 将被扣除作为每次成功借记的借记费用。任务是找到交易后剩下的余额，可以成功，也可以不成功。天平的精度为 2 个浮点。
**举例:**

```
Input: X = 50, bal = 100.50
Output: 49.00
Transaction successful

Input: X = 55, bal = 99.00
Output: 99.00
Transaction unsuccessful
```

**进场:**看交易能否成功。

*   在下列情况下，交易可以成功:
    *   x 是 10 的倍数，并且
    *   该人在账户中至少有(X+1.50)卢比，即要提取的钱加上费用。
*   在任何其他情况下，交易都不会成功。
*   如果交易成功，则从余额中扣除(X + 1.50)金额并返还
*   否则就退回余额。

以下是上述方法的实现:

## C++

```
// C++ program to find the remaining balance

#include <bits/stdc++.h>
using namespace std;

// Function to find the balance
void findBalance(int x, float bal)
{

    // Check if the transaction
    // can be successful or not
    if (x % 10 == 0
        && ((float)x + 1.50) <= bal) {

        // Transaction is successful
        cout << fixed << setprecision(2)
             << (bal - x - 1.50) << endl;
    }
    else {

        // Transaction is unsuccessful
        cout << fixed << setprecision(2)
             << (bal) << endl;
    }
}

int main()
{

    int x = 50;
    float bal = 100.50;

    findBalance(x, bal);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the remaining balance
import java.util.*;

class GFG
{

// Function to find the balance
static void findBalance(int x, float bal)
{

    // Check if the transaction
    // can be successful or not
    if (x % 10 == 0 && ((float)x + 1.50) <= bal)
    {

        // Transaction is successful
        System.out.printf("%.2f\n", bal - x - 1.50);
    }
    else
    {

        // Transaction is unsuccessful
        System.out.printf("%.2f\n", bal);
    }
}

// Driver Code
public static void main(String[] args)
{
    int x = 50;
    float bal = (float) 100.50;

    findBalance(x, bal);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the remaining balance

# Function to find the balance
def findBalance(x,bal):

    # Check if the transaction
    # can be successful or not
    if (x % 10 == 0 and (x + 1.50) <= bal):

        #Transaction is successful
        print(round(bal - x - 1.50, 2))
    else:

        # Transaction is unsuccessful
        print(round(bal, 2))

# Driver Code
x = 50
bal = 100.50

findBalance(x, bal)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find the remaining balance
using System;

class GFG
{

// Function to find the balance
static void findBalance(int x, float bal)
{

    // Check if the transaction
    // can be successful or not
    if (x % 10 == 0 && ((float)x + 1.50) <= bal)
    {

        // Transaction is successful
        Console.Write("{0:F2}\n", bal - x - 1.50);
    }
    else
    {

        // Transaction is unsuccessful
        Console.Write("{0:F2}\n", bal);
    }
}

// Driver Code
public static void Main(String[] args)
{
    int x = 50;
    float bal = (float) 100.50;

    findBalance(x, bal);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find the remaining balance

// Function to find the balance
function findBalance(x, bal)
{

    // Check if the transaction
    // can be successful or not
    if (x % 10 == 0
        && (x + 1.50) <= bal) {

        // Transaction is successful
        document.write( (bal - x - 1.50).toFixed(2));
    }
    else {

        // Transaction is unsuccessful
        document.write( (bal).toFixed(2));
    }
}

var x = 50;
var bal = 100.50;
findBalance(x, bal);

</script>
```

**Output:** 

```
49.00
```
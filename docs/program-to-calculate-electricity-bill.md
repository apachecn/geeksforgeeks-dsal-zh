# 电费计算程序

> 原文:[https://www . geesforgeks . org/程序计算电费/](https://www.geeksforgeeks.org/program-to-calculate-electricity-bill/)

给定一个整数 **U** 表示用电量的千瓦时单位，任务是借助以下费用计算电费:

> *   1 to 100 units–![Rs. 10/unit](img/4b7e7264840a7c97450e70b4b6ba6b4f.png "Rendered by QuickLaTeX.com")
> *   100 to 200 units–![Rs. 15/unit](img/89884dd26c32fbe0779aa50327df2715.png "Rendered by QuickLaTeX.com")
> *   200 to 300 units–![Rs. 20/unit](img/69bb53161485e4b3aa45f0cff06a2947.png "Rendered by QuickLaTeX.com")
> *   More than 300 units–![Rs. 25/unit](img/1694a4fbc9e61a2171eaaad5a81192f5.png "Rendered by QuickLaTeX.com")

**例:**

> **输入:** U = 250
> **输出:** 3500
> **说明:**
> 前 100 台收费–10 * 100 = 1000
> 100 至 200 台收费–15 * 100 = 1500
> 200 至 250 台收费–20 * 50 = 1000
> 总电费= 1000 +以上

**做法:**思路是识别其所属的收费条，然后根据上述收费计算账单。以下是步骤说明:

*   检查消耗的单位是否小于等于 100，如果是，则总电费为:

> ![\text{Total Electricity Bill} = (\text{units} * 10) ](img/564d2bf265a766372edf7a099dbbd952.png "Rendered by QuickLaTeX.com")

*   否则，如果检查消耗的单位小于等于 200，如果是，则总电费将为:

> ![\text{Total Electricity Bill} = (100*10) + (\text{units}-100) * 15 ](img/b5a8ce9c4794943112fb337ba88eca69.png "Rendered by QuickLaTeX.com")

*   否则，如果检查消耗的单位小于等于 300，如果是，则总电费将为:

> ![\text{Total Electricity Bill} = (100*10) + (100*15) + (\text{units}-200) * 20 ](img/8cf15e52d9a011802b482e14de4f8600.png "Rendered by QuickLaTeX.com")

*   否则，如果检查消耗的单位大于 300，如果是，总电费将为:

> ![\text{Total Electricity Bill} = (100*10) + (100*15) + (100*20) + (\text{units}-300) * 25 ](img/84c828bd40647523bb31deea989b4ecb.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ implementation to calculate the
// electricity bill
#include<bits/stdc++.h>
using namespace std;

// Function to calculate the
// electricity bill
int calculateBill(int units)
{

    // Condition to find the charges
    // bar in which the units consumed
    // is fall
    if (units <= 100)
    {
        return units * 10;
    }
    else if (units <= 200)
    {
        return (100 * 10) +
               (units - 100) * 15;
    }
    else if (units <= 300)
    {
        return (100 * 10) +
               (100 * 15) +
               (units - 200) * 20;
    }
    else if (units > 300)
    {
        return (100 * 10) +
               (100 * 15) +
               (100 * 20) +
               (units - 300) * 25;
    }
    return 0;
}

// Driver Code
int main()
{
    int units = 250;
    cout << calculateBill(units);
}

// This code is contributed by spp____
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to calculate the
// electricity bill

import java.util.*;

class ComputeElectricityBill {

    // Function to calculate the
    // electricity bill
    public static int calculateBill(int units)
    {

        // Condition to find the charges
        // bar in which the units consumed
        // is fall
        if (units <= 100) {
            return units * 10;
        }
        else if (units <= 200) {
            return (100 * 10)
                + (units - 100)
                      * 15;
        }
        else if (units <= 300) {
            return (100 * 10)
                + (100 * 15)
                + (units - 200)
                      * 20;
        }
        else if (units > 300) {
            return (100 * 10)
                + (100 * 15)
                + (100 * 20)
                + (units - 300)
                      * 25;
        }
        return 0;
    }

    // Driver Code
    public static void main(String args[])
    {
        int units = 250;

        System.out.println(
            calculateBill(units));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to calculate the
# electricity bill

# Function to calculate the
# electricity bill
def calculateBill(units):

    # Condition to find the charges
    # bar in which the units consumed
    # is fall
    if (units <= 100):

        return units * 10;

    elif (units <= 200):

        return ((100 * 10) +
                (units - 100) * 15);

    elif (units <= 300):

        return ((100 * 10) +
                (100 * 15) +
                (units - 200) * 20);

    elif (units > 300):

        return ((100 * 10) +
                (100 * 15) +
                (100 * 20) +
                (units - 300) * 25);

    return 0;

# Driver Code
units = 250;
print(calculateBill(units));

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation to calculate the
// electricity bill
using System;

class ComputeElectricityBill{

// Function to calculate the
// electricity bill
public static int calculateBill(int units)
{

    // Condition to find the charges
    // bar in which the units consumed
    // is fall
    if (units <= 100)
    {
        return units * 10;
    }
    else if (units <= 200)
    {
        return (100 * 10) +
               (units - 100) * 15;
    }
    else if (units <= 300)
    {
        return (100 * 10) +
               (100 * 15) +
               (units - 200) * 20;
    }
    else if (units > 300)
    {
        return (100 * 10) +
               (100 * 15) +
               (100 * 20) +
               (units - 300) * 25;
    }
    return 0;
}

// Driver Code
public static void Main(String []args)
{
    int units = 250;

    Console.WriteLine(calculateBill(units));
}
}

// This code is contributed by spp____
```

## java 描述语言

```
<script>

// Javascript implementation to calculate the
// electricity bill

// Function to calculate the
// electricity bill
function calculateBill(units)
{

    // Condition to find the charges
    // bar in which the units consumed
    // is fall
    if (units <= 100)
    {
        return units * 10;
    }
    else if (units <= 200)
    {
        return (100 * 10)
            + (units - 100)
                  * 15;
    }
    else if (units <= 300)
    {
        return (100 * 10)
            + (100 * 15)
            + (units - 200)
                  * 20;
    }
    else if (units > 300)
    {
        return (100 * 10)
            + (100 * 15)
            + (100 * 20)
            + (units - 300)
                  * 25;
    }
    return 0;
}

// Driver Code
var units = 250;

document.write(calculateBill(units));

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
3500
```

时间复杂度:0(1)

辅助空间:0(1)
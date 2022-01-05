# 利用给定的质量和体积

求出溶液的浓度

> 原文:[https://www . geesforgeks . org/find-使用给定质量和体积的溶液浓度/](https://www.geeksforgeeks.org/find-the-concentration-of-a-solution-using-given-mass-and-volume/)

给定代表溶质质量和溶液体积的两个值 **M** 和 **V** ，任务是计算溶液的浓度。
**例:**

> **输入:** M = 100.00，V = 500.00
> **输出:** 200
> **解释:**
> C = 1000 * (100 / 500)
> 溶液浓度为 200
> **输入:** M = 1.00 V = 1000.00
> **输出:** 1

**方法:**溶液的浓度定义为每升溶液中溶质的质量(克)。
*数学上:*

> **C = 1000 * (M / V)**
> 其中 M =溶质质量，V =溶液体积。

因此，为了解决问题，请遵循以下步骤:

1.  使用公式 **C = 1000* (M / V)** 计算溶液浓度。
2.  打印结果。

以下是上述方法的实现:

## C++

```
// C++ program to find
// concentration of a solution
// using given Mass and Volume

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// concentration from the
// given mass of solute and
// volume of a solution
double get_concentration(double mass,
                         double volume)
{
    if (volume == 0)
        return -1;
    else
        return (mass / volume)
               * 1000;
}

// Driver Program
int main()
{
    double mass, volume;
    mass = 100.00;
    volume = 500.00;
    cout << get_concentration(mass,
                              volume);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find concentration
// of a solution using given Mass
// and Volume
class GFG{

// Function to calculate
// concentration from the
// given mass of solute and
// volume of a solution
static double get_concentration(double mass,
                                double volume)
{
    if (volume == 0)
        return -1;
    else
        return (mass / volume) * 1000;
}

// Driver code
public static void main(String[] args)
{
    double mass, volume;
    mass = 100.00;
    volume = 500.00;

    System.out.println(get_concentration(mass,
                                         volume));
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program to find
# concentration of a solution
# using given Mass and Volume

# Function to calculate
# concentration from the
# given mass of solute and
# volume of a solution
def get_concentration(mass, volume):

    if (volume == 0):
        return -1;
    else:
        return (mass / volume) * 1000;

# Driver code
mass = 100.00;
volume = 500.00;

print(get_concentration(mass, volume))

# This code is contributed by Pratima Pandey
```

## C#

```
// C# program to find concentration
// of a solution using given Mass
// and Volume
using System;
class GFG{

// Function to calculate
// concentration from the
// given mass of solute and
// volume of a solution
static double get_concentration(double mass,
                                double volume)
{
    if (volume == 0)
        return -1;
    else
        return (mass / volume) * 1000;
}

// Driver code
public static void Main()
{
    double mass, volume;
    mass = 100.00;
    volume = 500.00;

    Console.Write(get_concentration(mass,
                                    volume));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>
// javascript program to find
// concentration of a solution
// using given Mass and Volume

// Function to calculate
// concentration from the
// given mass of solute and
// volume of a solution
function get_concentration( mass,
                          volume)
{
    if (volume == 0)
        return -1;
    else
        return (mass / volume)
               * 1000;
}

// Driver Program
    let mass, volume;
    mass = 100.00;
    volume = 500.00;

    document.write(get_concentration(mass, volume));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
200
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*
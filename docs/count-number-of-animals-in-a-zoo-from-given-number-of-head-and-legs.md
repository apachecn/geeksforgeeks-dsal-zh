# 根据给定的头和腿的数量计算动物园中动物的数量

> 原文:[https://www . geeksforgeeks . org/count-动物园中动物的数量-从给定数量的头和腿/](https://www.geeksforgeeks.org/count-number-of-animals-in-a-zoo-from-given-number-of-head-and-legs/)

给定兔子和鸽子的腿和头的总数。任务是计算兔子和鸽子的数量。
**例:**

```
Input: Heads = 200, Legs = 540 
Output: Rabbits = 70, Pigeons = 130

Input: Heads = 100, Legs = 300
Output: Rabbits = 50, Pigeons = 50
```

> 让头部总数= 200，腿部总数= 540。
> 设兔子的头和腿的数量= X，鸽子的头和腿的数量= Y。
> 所以，
> X + Y = 200..**方程 1** (一只兔子和一只鸽子的头数=头总数)
> (因为它们都有一个头)
> 4X+2Y = 540……**方程 2** (兔子和一只鸽子的腿数=腿总数)
> (兔子有 4 条腿，鸽子有 2 条腿)
> 现在，解方程 1 和 2，我们得到，
> 4X = 540–2Y
> 4X = 540–2 *(200–X)
> 4X = 540–400+2X
> 2X = 140 =>X = 70
> X = 70 和 Y = 130。
> 因此，兔子= 70，鸽子= 130

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that calculates Rabbits
int countRabbits(int Heads, int Legs)
{
    int count = 0;

    count = (Legs)-2 * (Heads);
    count = count / 2;

    return count;
}

// Driver code
int main()
{
    int Heads = 100, Legs = 300;

    int Rabbits = countRabbits(Heads, Legs);

    cout << "Rabbits = " << Rabbits << endl;
    cout << "Pigeons = " << Heads - Rabbits << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
import java.lang.*;

class GFG
{
// Function that calculates Rabbits
static int countRabbits(int Heads,
                        int Legs)
{
    int count = 0;

    count = (Legs) - 2 * (Heads);
    count = count / 2;

    return count;
}

// Driver code
public static void main(String args[])
{
    int Heads = 100, Legs = 300;

    int Rabbits = countRabbits(Heads, Legs);

    System.out.println("Rabbits = " +
                        Rabbits);
    System.out.println("Pigeons = " +
                      (Heads - Rabbits));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function that calculates Rabbits
def countRabbits(Heads, Legs):
    count = 0

    count = (Legs) - 2 * (Heads)
    count = count / 2

    return count

# Driver code
if __name__ == '__main__':
    Heads = 100
    Legs = 300

    Rabbits = countRabbits(Heads, Legs)

    print("Rabbits =", Rabbits)
    print("Pigeons =", Heads - Rabbits)

# This code is contributed
# by Surendra_Gangwar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
// Function that calculates Rabbits
static int countRabbits(int Heads,
                        int Legs)
{
    int count = 0;

    count = (Legs) - 2 * (Heads);
    count = count / 2;

    return count;
}

// Driver code
public static void Main()
{
    int Heads = 100, Legs = 300;

    int Rabbits = countRabbits(Heads, Legs);

    Console.WriteLine("Rabbits = " +
                       Rabbits);
    Console.WriteLine("Pigeons = " +
                     (Heads - Rabbits));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function that calculates Rabbits
function countRabbits($Heads, $Legs)
{
    $count = 0;

    $count = ($Legs) - 2 * ($Heads);
    $count = (int) $count / 2;

    return $count;
}

// Driver code
$Heads = 100;
$Legs = 300;
$Rabbits = countRabbits($Heads, $Legs);

echo "Rabbits = " , $Rabbits , "\n";
echo "Pigeons = " , $Heads -
                    $Rabbits, "\n";

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function that calculates Rabbits
function countRabbits(Heads, Legs)
{
    var count = 0;

    count = (Legs)-2 * (Heads);
    count = count / 2;

    return count;
}

// Driver code
var Heads = 100, Legs = 300;
var Rabbits = countRabbits(Heads, Legs);
document.write( "Rabbits = " + Rabbits + "<br>");
document.write( "Pigeons = " + (Heads - Rabbits));

</script>
```

**Output:** 

```
Rabbits = 50
Pigeons = 50
```
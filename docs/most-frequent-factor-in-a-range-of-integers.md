# 整数范围内最频繁的因子

> 原文:[https://www . geesforgeks . org/最频繁整数范围因子/](https://www.geeksforgeeks.org/most-frequent-factor-in-a-range-of-integers/)

给你一个数字范围，从较低的数字到较高的数字(包括两者)。考虑这些数字中除 1 以外的所有因素，任务是找出出现次数最多的因素。如果一个以上的号码有最大频率比打印他们中的任何一个。
**例:**

```
Input : lower=10 higher=14
Output : The factor with maximum frequency is 2.

Input : lower=11 higher=11
Output : The factor with maximum frequency is 11.
```

**解释:**
如果我们有一个数字范围，比如说 10 到 14。那么 1 以外的因素将是:

*   10 => 2, 5, 10

*   11 => 11

*   12 => 2, 3, 4, 6, 12

*   13 => 13

*   14 => 2, 7, 14

在上述情况下，频率(2)= 3，与其他因素相比，这是最大值。
**进场:**
1。如果较低=较高，则所有因子的频率都为 1。所以我们可以打印任何因子的数字，因为每个数字都是自身的因子，所以我们打印相同的数字。
2。否则，我们打印“2”，因为它对于一系列数字总是正确的。

## C++

```
// CPP program to find most common factor
// in a range.
#include <bits/stdc++.h>
using namespace std;

int mostCommon(int lower, int higher)
{
    // Check whether lower number
    // and higher number are same
    if (lower == higher)
        return lower;
    else
        return 2;
}

// Driver Code
int main()
{
    int lower = 10; // Lower number
    int higher = 20; // Higher number

    printf("The most frequent factor %d\n",
               mostCommon(lower, higher));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find most common factor
// in a range.

public class GfG {

    public static int mostCommon(int lower, int higher)
    {
        // Check whether lower number 
        // and higher number are same
        if (lower == higher) 
            return lower;
        else
            return 2;
    }

    // Driver code
    public static void main(String []args) {

        int lower = 10; // Lower number
        int higher = 20; // Higher number
        System.out.println("The most frequent factor " +
                                    mostCommon(lower, higher));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python 3 program to find most
# common factor in a range.
def mostCommon( lower, higher):

    # Check whether lower number
    # and higher number are same
    if (lower == higher):
        return lower
    else:
        return 2

# Driver Code
lower = 10 # Lower number
higher = 20 # Higher number

print("The most frequent factor",
       mostCommon(lower, higher))

# This code is contributed by ash264
```

## C#

```
// C# program to find most common factor
// in a range.
using System;

class GFG
{
static int mostCommon(int lower, int higher)
{
    // Check whether lower number
    // and higher number are same
    if (lower == higher)
        return lower;
    else
        return 2;
}

// Driver Code
public static void Main()
{
    int lower = 10; // Lower number
    int higher = 20; // Higher number

    Console.WriteLine("The most frequent factor " +
                       mostCommon(lower, higher));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find most common
// factor in a range.

function mostCommon($lower, $higher)
{
    // Check whether lower number
    // and higher number are same
    if ($lower == $higher)
        return $lower;
    else
        return 2;
}

// Driver Code
$lower = 10; // Lower number
$higher = 20; // Higher number

echo "The most frequent factor ".
    mostCommon($lower, $higher) . "\n";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript program to find most common factor
// in a range.

function mostCommon(lower , higher)
{
    // Check whether lower number 
    // and higher number are same
    if (lower == higher) 
        return lower;
    else
        return 2;
}

// Driver code

var lower = 10; // Lower number
var higher = 20; // Higher number
document.write("The most frequent factor " +
                            mostCommon(lower, higher));

// This code contributed by Princi Singh
</script>
```

**Output:** 

```
The most frequent factor 2
```

**时间复杂度:** O(1)
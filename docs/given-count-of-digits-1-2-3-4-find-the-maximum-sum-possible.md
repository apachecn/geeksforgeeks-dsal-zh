# 给定数字 1、2、3、4 的个数，求最大可能和

> 原文:[https://www . geesforgeks . org/给定位数-1-2-3-4-找到最大可能总和/](https://www.geeksforgeeks.org/given-count-of-digits-1-2-3-4-find-the-maximum-sum-possible/)

给定数字 1，2，3，4 的计数。使用这些数字，你只能组成数字 234 和 12。任务是找到在形成数字后能得到的最大可能和。

**注**:目的只是最大化总和，即使有些数字没有使用。

**示例:**

```
Input : c1 = 5, c2 = 2, c3 = 3, c4 = 4
Output : 468
Explanation : We can form two 234s

Input : c1 = 5, c2 = 3, c3 = 1, c4 = 5
Output : 258
Explanation : We can form one 234 and two 12s
```

**方法**:一个有效的方法是先试着做 234，234 的可能个数是 c2，c3，c4 的最小值。之后，用剩下的 1 和 2 试着形成 12。

下面是上述方法的实现:

## C++

```
// CPP program to maximum possible sum

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum possible sum
int Maxsum(int c1, int c2, int c3, int c4)
{
    // To store required sum
    int sum = 0;

    // Number of 234's can be formed
    int two34 = min(c2, min(c3, c4));

    // Sum obtained with 234s
    sum = two34 * 234;

    // Remaining 2's
    c2 -= two34;

    // Sum obtained with 12s
    sum += min(c2, c1) * 12;

    // Return the required sum
    return sum;
}

// Driver code
int main()
{
    int c1 = 5, c2 = 2, c3 = 3, c4 = 4;

    cout << Maxsum(c1, c2, c3, c4);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximum possible sum
class GFG
{

// Function to find the maximum possible sum
static int Maxsum(int c1, int c2, int c3, int c4)
{
    // To store required sum
    int sum = 0;

    // Number of 234's can be formed
    int two34 = Math.min(c2,Math.min(c3, c4));

    // Sum obtained with 234s
    sum = two34 * 234;

    // Remaining 2's
    c2 -= two34;

    // Sum obtained with 12s
    sum +=Math.min(c2, c1) * 12;

    // Return the required sum
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int c1 = 5, c2 = 2, c3 = 3, c4 = 4;

    System.out.println(Maxsum(c1, c2, c3, c4));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 program to maximum possible sum

# Function to find the maximum
# possible sum
def Maxsum(c1, c2, c3, c4):

    # To store required sum
    sum = 0

    # Number of 234's can be formed
    two34 = min(c2, min(c3, c4))

    # Sum obtained with 234s
    sum = two34 * 234

    # Remaining 2's
    c2 -= two34
    sum += min(c2, c1) * 12

    # Return the required sum
    return sum

# Driver Code
c1 = 5; c2 = 2; c3 = 3; c4 = 4
print(Maxsum(c1, c2, c3, c4))

# This code is contributed by Shrikant13
```

## C#

```
// C# program to maximum possible sum
using System;

class GFG
{

// Function to find the maximum possible sum
static int Maxsum(int c1, int c2, int c3, int c4)
{
    // To store required sum
    int sum = 0;

    // Number of 234's can be formed
    int two34 = Math.Min(c2, Math.Min(c3, c4));

    // Sum obtained with 234s
    sum = two34 * 234;

    // Remaining 2's
    c2 -= two34;

    // Sum obtained with 12s
    sum +=Math.Min(c2, c1) * 12;

    // Return the required sum
    return sum;
}

// Driver code
public static void Main()
{
    int c1 = 5, c2 = 2, c3 = 3, c4 = 4;

    Console.WriteLine(Maxsum(c1, c2, c3, c4));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to maximum possible sum

// Function to find the maximum possible sum
function Maxsum($c1, $c2, $c3, $c4)
{
    // To store required sum
    $sum = 0;

    // Number of 234's can be formed
    $two34 = min($c2, min($c3, $c4));

    // Sum obtained with 234s
    $sum = $two34 * 234;

    // Remaining 2's
    $c2 -= $two34;

    // Sum obtained with 12s
    $sum += min($c2, $c1) * 12;

    // Return the required sum
    return $sum;
}

// Driver code
$c1 = 5; $c2 = 2;
$c3 = 3; $c4 = 4;

echo Maxsum($c1, $c2, $c3, $c4);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Java Script program to maximum possible sum

// Function to find the maximum possible sum
function Maxsum(c1,c2,c3,c4)
{
    // To store required sum
    let sum = 0;

    // Number of 234's can be formed
    let two34 = Math.min(c2,Math.min(c3, c4));

    // Sum obtained with 234s
    sum = two34 * 234;

    // Remaining 2's
    c2 -= two34;

    // Sum obtained with 12s
    sum +=Math.min(c2, c1) * 12;

    // Return the required sum
    return sum;
}

// Driver code

    let c1 = 5, c2 = 2, c3 = 3, c4 = 4;

    document.write(Maxsum(c1, c2, c3, c4));

// This code is contributed by sravan kumar G
</script>
```

**Output:** 

```
468
```
# 通过选择数字

根据和的绝对差预测比赛的胜负

> 原文:[https://www . geeksforgeeks . org/通过选择数字预测绝对差额赛获胜者/](https://www.geeksforgeeks.org/predict-the-winner-of-the-game-on-the-basis-of-absolute-difference-of-sum-by-selecting-numbers/)

给定一组 **N 个**数字。两个玩家 **X** 和 **Y** 玩一个游戏，每走一步都有一个玩家选择一个号码。一个号码只能选择一次。在所有号码都被选中后，如果 **X** 和 **Y** 收集的号码总和之间的**绝对差**被 **4** 整除，则玩家 **X** 获胜，否则 **Y** 获胜。
**注意:**玩家 X 开始游戏，每一步都是对数字进行优化选择。
**例:**

> **输入:** a[] = {4，8，12，16}
> **输出:** X
> X 选择 4
> Y 选择 12
> X 选择 8
> Y 选择 16
> |(4+8)–(12+16)| = | 12–28 | = 16 可被 4 整除。
> 于是，X 胜
> **输入:** a[] = {7，9，1}
> **输出:** Y

**接近**:可以按照以下步骤解决问题:

*   初始化**计数 0** 、**计数 1** 、**计数 2** 和**计数 3** 至 **0** 。
*   如果 **a[i] % 4 == 0** ， **a[i] % 4 == 1** ， **a[i] % 4 == 2** 或 **a[i] % 4 == 3** ，则迭代数组中的每个数字并相应增加上述计数器。
*   如果 **count0** 、 **count1** 、 **count2** 和 **count3** 均为偶数，则 **X** 获胜，否则 **Y** 将获胜。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to decide the winner
int decideWinner(int a[], int n)
{
    int count0 = 0;
    int count1 = 0;
    int count2 = 0;
    int count3 = 0;

    // Iterate for all numbers in the array
    for (int i = 0; i < n; i++) {

        // Condition to count

        // If mod gives 0
        if (a[i] % 4 == 0)
            count0++;

        // If mod gives 1
        else if (a[i] % 4 == 1)
            count1++;

        // If mod gives 2
        else if (a[i] % 4 == 2)
            count2++;

        // If mod gives 3
        else if (a[i] % 4 == 3)
            count3++;
    }

    // Check the winning condition for X
    if (count0 % 2 == 0
        && count1 % 2 == 0
        && count2 % 2 == 0
        && count3 == 0)
        return 1;
    else
        return 2;
}

// Driver code
int main()
{

    int a[] = { 4, 8, 5, 9 };
    int n = sizeof(a) / sizeof(a[0]);
    if (decideWinner(a, n) == 1)
        cout << "X wins";
    else
        cout << "Y wins";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to decide the winner
static int decideWinner(int []a, int n)
{
    int count0 = 0;
    int count1 = 0;
    int count2 = 0;
    int count3 = 0;

    // Iterate for all numbers in the array
    for (int i = 0; i < n; i++)
    {

        // Condition to count

        // If mod gives 0
        if (a[i] % 4 == 0)
            count0++;

        // If mod gives 1
        else if (a[i] % 4 == 1)
            count1++;

        // If mod gives 2
        else if (a[i] % 4 == 2)
            count2++;

        // If mod gives 3
        else if (a[i] % 4 == 3)
            count3++;
    }

    // Check the winning condition for X
    if (count0 % 2 == 0 && count1 % 2 == 0 &&
        count2 % 2 == 0 && count3 == 0)
        return 1;
    else
        return 2;
}

// Driver code
public static void main(String args[])
{
    int []a = { 4, 8, 5, 9 };
    int n = a.length;
    if (decideWinner(a, n) == 1)
        System.out.print("X wins");
    else
        System.out.print("Y wins");
}
}

// This code is contributed by Akanksha Rai
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to decide the winner
def decideWinner(a, n):
    count0 = 0
    count1 = 0
    count2 = 0
    count3 = 0

    # Iterate for all numbers in the array
    for i in range(n):

        # Condition to count

        # If mod gives 0
        if (a[i] % 4 == 0):
            count0 += 1

        # If mod gives 1
        elif (a[i] % 4 == 1):
            count1 += 1

        # If mod gives 2
        elif (a[i] % 4 == 2):
            count2 += 1

        # If mod gives 3
        elif (a[i] % 4 == 3):
            count3 += 1

    # Check the winning condition for X
    if (count0 % 2 == 0 and count1 % 2 == 0 and
        count2 % 2 == 0 and count3 == 0):
        return 1
    else:
        return 2

# Driver code
a = [4, 8, 5, 9]
n = len(a)
if (decideWinner(a, n) == 1):
    print("X wins")
else:
    print("Y wins")

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to decide the winner
static int decideWinner(int []a, int n)
{
    int count0 = 0;
    int count1 = 0;
    int count2 = 0;
    int count3 = 0;

    // Iterate for all numbers in the array
    for (int i = 0; i < n; i++)
    {

        // Condition to count

        // If mod gives 0
        if (a[i] % 4 == 0)
            count0++;

        // If mod gives 1
        else if (a[i] % 4 == 1)
            count1++;

        // If mod gives 2
        else if (a[i] % 4 == 2)
            count2++;

        // If mod gives 3
        else if (a[i] % 4 == 3)
            count3++;
    }

    // Check the winning condition for X
    if (count0 % 2 == 0 && count1 % 2 == 0 &&
        count2 % 2 == 0 && count3 == 0)
        return 1;
    else
        return 2;
}

// Driver code
public static void Main()
{
    int []a = { 4, 8, 5, 9 };
    int n = a.Length;
    if (decideWinner(a, n) == 1)
        Console.Write("X wins");
    else
        Console.Write("Y wins");
}
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to decide the winner
function decideWinner($a, $n)
{
    $count0 = 0;
    $count1 = 0;
    $count2 = 0;
    $count3 = 0;

    // Iterate for all numbers in the array
    for ($i = 0; $i < $n; $i++)
    {

        // Condition to count

        // If mod gives 0
        if ($a[$i] % 4 == 0)
            $count0++;

        // If mod gives 1
        else if ($a[$i] % 4 == 1)
            $count1++;

        // If mod gives 2
        else if ($a[$i] % 4 == 2)
            $count2++;

        // If mod gives 3
        else if ($a[$i] % 4 == 3)
            $count3++;
    }

    // Check the winning condition for X
    if ($count0 % 2 == 0 && $count1 % 2 == 0 &&
        $count2 % 2 == 0 && $count3 == 0)
        return 1;
    else
        return 2;
}

// Driver code
$a = array( 4, 8, 5, 9 );
$n = count($a);

if (decideWinner($a, $n) == 1)
    echo "X wins";
else
    echo "Y wins";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to decide the winner
    function decideWinner(a , n) {
        var count0 = 0;
        var count1 = 0;
        var count2 = 0;
        var count3 = 0;

        // Iterate for all numbers in the array
        for (i = 0; i < n; i++) {

            // Condition to count

            // If mod gives 0
            if (a[i] % 4 == 0)
                count0++;

            // If mod gives 1
            else if (a[i] % 4 == 1)
                count1++;

            // If mod gives 2
            else if (a[i] % 4 == 2)
                count2++;

            // If mod gives 3
            else if (a[i] % 4 == 3)
                count3++;
        }

        // Check the winning condition for X
        if (count0 % 2 == 0 && count1 % 2 == 0 && count2 % 2 == 0 && count3 == 0)
            return 1;
        else
            return 2;
    }

    // Driver code

        var a = [ 4, 8, 5, 9 ];
        var n = a.length;
        if (decideWinner(a, n) == 1)
            document.write("X wins");
        else
            document.write("Y wins");

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
X wins
```
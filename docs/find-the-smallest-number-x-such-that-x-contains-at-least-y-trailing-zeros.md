# 求最小的数 X 这样 X！至少包含 Y 个尾随零。

> 原文:[https://www . geesforgeks . org/find-最小数字-x-so-x-包含-至少-y-尾随零/](https://www.geeksforgeeks.org/find-the-smallest-number-x-such-that-x-contains-at-least-y-trailing-zeros/)

给定一个整数 Y，求最小的数 X，这样 X！至少包含 Y 个尾随零。
先决条件–[计算一个数的阶乘中的尾随零](https://www.geeksforgeeks.org/count-trailing-zeroes-factorial-number/)

**示例:**

> **输入:**Y = 2
> T3】输出: 10
> 10！= 3628800，有 2 个尾随零。9!= 362880，有 1 个尾随零。因此，10 是正确答案。
> 
> **输入:**Y = 6
> T3】输出: 25
> 25！= 15511210043330985984000000，有 6 个尾随零。24!= 620448401733239439360000，有 4 个尾随零。因此，25 是正确答案。

**方法:**使用**二分搜索法**可以轻松解决问题。N 中尾随零的个数！是由 N 中的因子 5 的计数给出的！。阅读[这篇](https://www.geeksforgeeks.org/count-trailing-zeroes-factorial-number/)文章获取先决条件。countFactor(5，N)函数返回 N 中因子 5 的计数！这等于 N 中尾随零的计数！。最小的数字 X 这样 X！包含至少 Y 个尾随零，可以通过使用此函数在范围[0，5 * Y]上使用二分搜索法来快速计算。

下面是上述方法的实现。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of factors P in X!
int countFactor(int P, int X)
{
    if (X < P)
        return 0;

    return (X / P + countFactor(P, X / P));
}

// Function to find the smallest X such
// that X! contains Y trailing zeros
int findSmallestX(int Y)
{
    int low = 0, high = 5 * Y;
    int N = 0;
    while (low <= high) {
        int mid = (high + low) / 2;

        if (countFactor(5, mid) < Y) {
            low = mid + 1;
        }

        else {
            N = mid;
            high = mid - 1;
        }
    }

    return N;
}

// Driver code
int main()
{
    int Y = 10;

    cout << findSmallestX(Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to count the number
    // of factors P in X!
    static int countFactor(int P, int X)
    {
        if (X < P)
            return 0;

        return (X / P + countFactor(P, X / P));
    }

    // Function to find the smallest X such
    // that X! contains Y trailing zeros
    static int findSmallestX(int Y)
    {
        int low = 0, high = 5 * Y;
        int N = 0;
        while (low <= high)
        {
            int mid = (high + low) / 2;

            if (countFactor(5, mid) < Y)
            {
                low = mid + 1;
            }

            else
            {
                N = mid;
                high = mid - 1;
            }
        }

        return N;
    }

    // Driver code
    public static void main(String args[])
    {
        int Y = 10;

        System.out.println(findSmallestX(Y));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to count the number
# of factors P in X!
def countFactor(P, X):
    if (X < P):
        return 0;

    return (X // P + countFactor(P, X // P));

# Function to find the smallest X such
# that X! contains Y trailing zeros
def findSmallestX(Y):

    low = 0;
    high = 5 * Y;
    N = 0;
    while (low <= high):
        mid = (high + low) // 2;

        if (countFactor(5, mid) < Y):
            low = mid + 1;

        else:
            N = mid;
            high = mid - 1;

    return N;

# Driver code
Y = 10;

print(findSmallestX(Y));

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
class GFG
{

// Function to count the number
// of factors P in X!
static int countFactor(int P, int X)
{
    if (X < P)
        return 0;

    return (X / P + countFactor(P, X / P));
}

// Function to find the smallest X such
// that X! contains Y trailing zeros
static int findSmallestX(int Y)
{
    int low = 0, high = 5 * Y;
    int N = 0;
    while (low <= high)
    {
        int mid = (high + low) / 2;

        if (countFactor(5, mid) < Y)
        {
            low = mid + 1;
        }

        else
        {
            N = mid;
            high = mid - 1;
        }
    }

    return N;
}

// Driver code
static void Main()
{
    int Y = 10;

    System.Console.WriteLine(findSmallestX(Y));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to count the number
// of factors P in X!
function countFactor($P, $X)
{
    if ($X < $P)
        return 0;

    return ((int)($X / $P) +
             countFactor($P, ($X / $P)));
}

// Function to find the smallest X such
// that X! contains Y trailing zeros
function findSmallestX($Y)
{
    $low = 0; $high = 5 * $Y;
    $N = 0;
    while ($low <= $high)
    {
        $mid = (int)(($high + $low) / 2);

        if (countFactor(5, $mid) < $Y)
        {
            $low = $mid + 1;
        }

        else
        {
            $N = $mid;
            $high = $mid - 1;
        }
    }

    return $N;
}

// Driver code
$Y = 10;

echo(findSmallestX($Y));

// This code is contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to count the number
// of factors P in X!
function countFactor(P, X)
{
    if (X < P)
        return 0;

    return (parseInt(X / P) +
    countFactor(P, parseInt(X / P)));
}

// Function to find the smallest X such
// that X! contains Y trailing zeros
function findSmallestX(Y)
{
    let low = 0, high = 5 * Y;
    let N = 0;

    while (low <= high)
    {
        let mid = parseInt((high + low) / 2);

        if (countFactor(5, mid) < Y)
        {
            low = mid + 1;
        }
        else
        {
            N = mid;
            high = mid - 1;
        }
    }
    return N;
}

// Driver code
let Y = 10;

document.write(findSmallestX(Y));

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
45
```
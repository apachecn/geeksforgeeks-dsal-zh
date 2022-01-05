# 以 2 的幂为负数的前 N 个自然数之和

> 原文:[https://www . geesforgeks . org/以 2 的 2 次方为负数的第 n 个自然数之和/](https://www.geeksforgeeks.org/sum-of-first-n-natural-numbers-by-taking-powers-of-2-as-negative-number/)

给定一个数字 n(可能直到 10^9)。任务是求取 2 的幂为负数的前 N 个自然数的和。
**例:**

```
Input: N = 4
Output: -4
- 1 - 2 + 3 - 4 = -4
1, 2, and 4 are the powers of two.

Input: N = 5
Output: 1
```

**方法:**一个有效的解决方案是在一个数组中存储二的幂，然后在另一个数组中存储这个数组的假定。这个数组的大小最多可以是 30。因此，通常搜索幂数组中大于给定数的第一个元素。
以下是上述办法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// to store power of 2
int power[31];

// to store presum of the power of 2's
int pre[31];

// function to find power of 2
void PowerOfTwo()
{
    // to store power of 2
    int x = 1;
    for (int i = 0; i < 31; i++) {
        power[i] = x;
        x *= 2;
    }

    // to store pre sum
    pre[0] = 1;
    for (int i = 1; i < 31; i++)
        pre[i] = pre[i - 1] + power[i];
}

// Function to find the sum
int Sum(int n)
{
    // first store sum of
    // first n natural numbers.
    int ans = n * (n + 1) / 2;

    // find the first greater number than given
    // number then minus double of this
    // from answer
    for (int i = 0; i < 31; i++) {
        if (power[i] > n) {
            ans -= 2 * pre[i - 1];
            break;
        }
    }

    return ans;
}

// Driver code
int main()
{
    // function call
    PowerOfTwo();

    int n = 4;

    // function call
    cout << Sum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG {

// to store power of 2
static int power[] = new int[31];

// to store presum of the power of 2's
static int pre[] = new int[31];

// function to find power of 2
static void PowerOfTwo()
{
    // to store power of 2
    int x = 1;
    for (int i = 0; i < 31; i++) {
        power[i] = x;
        x *= 2;
    }

    // to store pre sum
    pre[0] = 1;
    for (int i = 1; i < 31; i++)
        pre[i] = pre[i - 1] + power[i];
}

// Function to find the sum
static int Sum(int n)
{
    // first store sum of
    // first n natural numbers.
    int ans = n * (n + 1) / 2;

    // find the first greater number than given
    // number then minus double of this
    // from answer
    for (int i = 0; i < 31; i++) {
        if (power[i] > n) {
            ans -= 2 * pre[i - 1];
            break;
        }
    }

    return ans;
}

// Driver code
    public static void main (String[] args) {

    // function call
    PowerOfTwo();

    int n = 4;

    // function call
    System.out.println( Sum(n));
    }
}
 // This code is contributed by ajit
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach

# to store power of 2
power = [0] * 31

# to store presum of the
# power of 2's
pre = [0] * 31

# function to find power of 2
def PowerOfTwo():

    # to store power of 2
    x = 1
    for i in range(31):
        power[i] = x
        x *= 2

    # to store pre sum
    pre[0] = 1
    for i in range(1, 31):
        pre[i] = pre[i - 1] + power[i]

# Function to find the sum
def Sum(n):

    # first store sum of
    # first n natural numbers.
    ans = n * (n + 1) // 2

    # find the first greater number
    # than given number then minus
    # double of this from answer
    for i in range( 31) :
        if (power[i] > n):
            ans -= 2 * pre[i - 1]
            break

    return ans

# Driver code
if __name__ == "__main__":

    # function call
    PowerOfTwo()

    n = 4

    # function call
    print(Sum(n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of
// above approach
using System;
class GFG
{

// to store power of 2
static int[] power = new int[31];

// to store presum of the
// power of 2's
static int[] pre = new int[31];

// function to find power of 2
static void PowerOfTwo()
{
    // to store power of 2
    int x = 1;
    for (int i = 0; i < 31; i++)
    {
        power[i] = x;
        x *= 2;
    }

    // to store pre sum
    pre[0] = 1;
    for (int i = 1; i < 31; i++)
        pre[i] = pre[i - 1] + power[i];
}

// Function to find the sum
static int Sum(int n)
{
    // first store sum of
    // first n natural numbers.
    int ans = n * (n + 1) / 2;

    // find the first greater number
    // than given number then minus
    // double of this from answer
    for (int i = 0; i < 31; i++)
    {
        if (power[i] > n)
        {
            ans -= 2 * pre[i - 1];
            break;
        }
    }

    return ans;
}

// Driver code
public static void Main ()
{

    // function call
    PowerOfTwo();

    int n = 4;

    // function call
    Console.WriteLine(Sum(n));
}
}

// This code is contributed
// by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// to store power of 2
$power = array_fill(0, 31, 0);

// to store presum of the
// power of 2's
$pre = array_fill(0, 31, 0);

// function to find power of 2
function PowerOfTwo()
{
    global $power, $pre;

    // to store power of 2
    $x = 1;
    for ($i = 0; $i < 31; $i++)
    {
        $power[$i] = $x;
        $x *= 2;
        }

    // to store pre sum
    $pre[0] = 1;
    for ($i = 1; $i < 31; $i++)
        $pre[$i] = $pre[$i - 1] + $power[$i];
}

// Function to find the sum
function Sum($n)
{
    global $power, $pre;

    // first store sum of
    // first n natural numbers.
    $ans = $n * ($n + 1) / 2;

    // find the first greater number
    // than given number then minus
    // double of this from answer
    for ($i = 0; $i < 31; $i++)
        if ($power[$i] > $n)
        {
            $ans -= 2 * $pre[$i - 1];
            break;
        }

    return $ans;
}

// Driver code

// function call
PowerOfTwo();

$n = 4;

// function call
print(Sum($n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript implementation of above approach

// to store power of 2
power = Array(31).fill(0);

// to store presum of the power of 2's
pre = Array(31).fill(0);

// function to find power of 2
function PowerOfTwo()
{

    // to store power of 2
    var x = 1;
    for (i = 0; i < 31; i++)
    {
        power[i] = x;
        x *= 2;
    }

    // to store pre sum
    pre[0] = 1;
    for (i = 1; i < 31; i++)
        pre[i] = pre[i - 1] + power[i];
}

// Function to find the sum
function Sum(n)
{

    // first store sum of
    // first n natural numbers.
    var ans = n * (n + 1) / 2;

    // find the first greater number than given
    // number then minus var of this
    // from answer
    for (i = 0; i < 31; i++)
    {
        if (power[i] > n)
        {
            ans -= 2 * pre[i - 1];
            break;
        }
    }
    return ans;
}

// Driver code
// function call
PowerOfTwo();
var n = 4;

// function call
document.write( Sum(n));

// This code is contributed by shikhasingrajput
</script>
```

**Output:** 

```
-4
```
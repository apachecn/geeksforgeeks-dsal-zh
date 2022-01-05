# 计算可以生成的不同数字，使这些数字的总和等于‘n’

> 原文:[https://www . geesforgeks . org/count-differential-numbers-can-generated-digits-sum-equal-n/](https://www.geeksforgeeks.org/count-different-numbers-can-generated-digits-sum-equal-n/)

给定一个正整数 n。计算可以使用数字 1、2、3 和 4 生成的不同数字，使数字总和为数字“n”。**这里数字‘4’将被视为‘1’**。比如
32 = 3+2 = 5
1341 = 1+3+1+1 = 6
441 = 1+1+1 = 3
**注**:回答 mod = **10 <sup>9</sup> +7** 中的数值

```
Input: 2
Output: 5
Explanation
There are only '5' numbers that can 
be made:
11 = 1 + 1 = 2
14 = 1 + 1 = 2
41 = 1 + 1 = 2
44 = 1 + 1 = 2
2  = 2

Input: 3
Output: 13
Explanation
There are only '13' numbers that can 
be made i.e., 111, 114, 141, 144, 411, 
414, 441, 444, 12, 21, 42, 24, 3.
```

方法是使用动态编程。问题与[硬币兑换](https://www.geeksforgeeks.org/dynamic-programming-set-7-coin-change/)和[方式写 n 为两个或两个以上正整数之和](https://www.geeksforgeeks.org/ways-to-write-n-as-sum-of-two-or-more-positive-integers/)问题相同。唯一的区别是，不像问题所说的那样迭代到“n”，而是只从 1 到 3 迭代，只允许 1、2、3 和 4 位数字。但是由于“4”可以用“1”代替，因此迭代 1、2 和 3，并使“1”的计数加倍，以补偿数字“4”。

## C++

```
// C++ program to count ways to write
// 'n' as sum of digits
#include<iostream>
using namespace std;

// Function to count 'num' as sum of
// digits(1, 2, 3, 4)
int countWays(int num)
{
    // Initialize dp[] array
    int dp[num+1];

    const int MOD = 1e9 + 7;
    // Base case
    dp[1] = 2;

    for(int i = 2; i <= num; ++i)
    {
        // Initialize the current dp[]
        // array as '0'
        dp[i] = 0;

        for(int j = 1; j <= 3; ++j)
        {
            /* if i == j then there is only
               one way to write with element
               itself 'i' */
            if(i - j == 0)
               dp[i] += 1;

            /* If j == 1, then there exist
               two ways, one from '1' and
               other from '4' */
            else if (j == 1)
               dp[i] += dp[i-j] * 2;

            /* if i - j is positive then
               pick the element from 'i-j'
               element of dp[] array */
            else if(i - j > 0)
               dp[i] += dp[i-j];

        // Check for modulas
        if(dp[i] >= MOD)
            dp[i] %= MOD;
        }

    }

    // return the final answer
    return dp[num];
}

// Driver code
int main()
{
    int n = 3;
    cout << countWays(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count ways to
// write 'n' as sum of digits
import java.io.*;

public class GFG
{

// Function to count 'num' as
// sum of digits(1, 2, 3, 4)
static int countWays(int num)
{

    // Initialize dp[] array
    int []dp= new int[num + 1];
    int MOD = (int)1E9 + 7;

    // Base case
    dp[1] = 2;

    for(int i = 2; i <= num; ++i)
    {
        // Initialize the current
        // dp[] array as '0'
        dp[i] = 0;

        for(int j = 1; j <= 3; ++j)
        {
            // if i == j then there is
            // only one way to write with
            // element itself 'i'
            if(i - j == 0)
            dp[i] += 1;

            // If j == 1, then there exist
            // two ways, one from '1' and
            // other from '4'
            else if (j == 1)
                dp[i] += dp[i - j] * 2;

            // if i - j is positive then
            // pick the element from 'i-j'
            // element of dp[] array
            else if(i - j > 0)
                dp[i] += dp[i - j];

        // Check for modulas
        if(dp[i] >= MOD)
            dp[i] %= MOD;
        }

    }

    // return the final answer
    return dp[num];
}

    // Driver code
    static public void main (String[] args)
    {
        int n = 3;
        System.out.println(countWays(n));

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 program to count ways to write
# 'n' as sum of digits

# Function to count 'num' as sum of
# digits(1, 2, 3, 4)
def countWays(num):

    # Initialize dp[] array
    dp = [0] * (num + 1);

    MOD = 100000000 + 7;

    # Base case
    dp[1] = 2;

    for i in range(2, num + 1):

        # Initialize the current dp[]
        # array as '0'
        dp[i] = 0;

        for j in range(1, 4):

            # if i == j then there is only
            # one way to write with element
            # itself 'i'
            if(i - j == 0):
                dp[i] += 1;

            # If j == 1, then there exist
            # two ways, one from '1' and
            # other from '4'
            elif (j == 1):
                dp[i] += dp[i - j] * 2;

            # if i - j is positive then
            # pick the element from 'i-j'
            # element of dp[] array
            elif(i - j > 0):
                dp[i] += dp[i - j];

        # Check for modulas
        if(dp[i] >= MOD):
            dp[i] %= MOD;

    # return the final answer
    return dp[num];

# Driver code
n = 3;
print(countWays(n));

# This code is contributed by mits
```

## C#

```
// C# program to count ways to
// write 'n' as sum of digits
using System;

public class GFG
{

// Function to count 'num' as
// sum of digits(1, 2, 3, 4)
static int countWays(int num)
{

    // Initialize dp[] array
    int []dp= new int[num + 1];
    int MOD = (int)1E9 + 7;

    // Base case
    dp[1] = 2;

    for(int i = 2; i <= num; ++i)
    {
        // Initialize the current
        // dp[] array as '0'
        dp[i] = 0;

        for(int j = 1; j <= 3; ++j)
        {
            // if i == j then there is
            // only one way to write with
            // element itself 'i'
            if(i - j == 0)
            dp[i] += 1;

            // If j == 1, then there exist
            // two ways, one from '1' and
            // other from '4'
            else if (j == 1)
                dp[i] += dp[i - j] * 2;

            // if i - j is positive then
            // pick the element from 'i-j'
            // element of dp[] array
            else if(i - j > 0)
                dp[i] += dp[i - j];

        // Check for modulas
        if(dp[i] >= MOD)
            dp[i] %= MOD;
        }

    }

    // return the final answer
    return dp[num];
}

    // Driver code
    static public void Main (String []args)
    {
        int n = 3;
        Console.WriteLine(countWays(n));

    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count ways to write
// 'n' as sum of digits

// Function to count 'num' as sum of
// digits(1, 2, 3, 4)
function countWays($num)
{
    // Initialize dp[] array
    $dp[$num + 1] = array();

    $MOD = 100000000 + 7;

    // Base case
    $dp[1] = 2;

    for($i = 2; $i <= $num; ++$i)
    {
        // Initialize the current dp[]
        // array as '0'
        $dp[$i] = 0;

        for($j = 1; $j <= 3; ++$j)
        {
            /* if i == j then there is only
            one way to write with element
            itself 'i' */
            if($i - $j == 0)
            $dp[$i] += 1;

            /* If j == 1, then there exist
            two ways, one from '1' and
            other from '4' */
            else if ($j == 1)
            $dp[$i] += $dp[$i - $j] * 2;

            /* if i - j is positive then
            pick the element from 'i-j'
            element of dp[] array */
            else if($i - $j > 0)
            $dp[$i] += $dp[$i - $j];

        // Check for modulas
        if($dp[$i] >= $MOD)
            $dp[$i] %= $MOD;
        }
    }

    // return the final answer
    return $dp[$num];
}

// Driver code
$n = 3;
echo countWays($n);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// JavaScript program to count ways to
// write 'n' as sum of digits

// Function to count 'num' as
// sum of digits(1, 2, 3, 4)
function countWays(num)
{

    // Initialize dp[] array
    let dp = [];
    let MOD = 1E9 + 7;

    // Base case
    dp[1] = 2;

    for(let i = 2; i <= num; ++i)
    {

        // Initialize the current
        // dp[] array as '0'
        dp[i] = 0;

        for(let j = 1; j <= 3; ++j)
        {

            // If i == j then there is
            // only one way to write with
            // element itself 'i'
            if (i - j == 0)
                dp[i] += 1;

            // If j == 1, then there exist
            // two ways, one from '1' and
            // other from '4'
            else if (j == 1)
                dp[i] += dp[i - j] * 2;

            // If i - j is positive then
            // pick the element from 'i-j'
            // element of dp[] array
            else if (i - j > 0)
                dp[i] += dp[i - j];

            // Check for modulas
            if (dp[i] >= MOD)
                dp[i] %= MOD;
        }

    }

    // Return the final answer
    return dp[num];
}

// Driver Code
let n = 3;

document.write(countWays(n));

// This code is contributed by susmitakundugoaldanga

</script>
```

**输出**

```
13
```

**时间复杂度:**O(n)
T3】辅助空间:O(n)
T6】注:问于 Directi 编码轮次(2014 年和 2017 年)
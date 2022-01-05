# 求 1 到 n 的整数个数，其中只包含数字 0 和 1

> 原文:[https://www . geesforgeks . org/find-从 1 到 n 的整数个数，其中只包含数字 0 和 1/](https://www.geeksforgeeks.org/find-the-number-of-integers-from-1-to-n-which-contains-digits-0s-and-1s-only/)

给定一个数字 **N** 。任务是找出从 1 到 n 的整数个数，其中只包含数字 0 和 1。

**示例:**

```
Input : N = 15
Output : 3
Explanation : 1, 10, 11 are such integers.

Input : N = 120
Output : 7
Explanation : 1, 10, 11, 100, 101, 110, 111 
are such integers.
```

**方法**:一种有效的方法是只使用从数字 1 开始的递归函数来构建包含 1 和 0 的整数。检查每个数字是否小于 **n** 。

下面是上述方法的实现:

## C++

```
// C++ program to find the number of integers
// from 1 to n which contains digits 0's and 1's only

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of integers
// from 1 to n which contains 0's and 1's only
int countNumbers(int x, int n)
{
    // If number is greater than n
    if (x > n)
        return 0;

    // otherwise add count this number and
    // call two functions
    return 1 + countNumbers(x * 10, n) + countNumbers(x * 10 + 1, n);
}

// Driver code
int main()
{
    int n = 120;

    cout << countNumbers(1, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of integers
// from 1 to n which contains digits 0's and 1's only
class GFG
{

// Function to find the number of integers
// from 1 to n which contains 0's and 1's only
static int countNumbers(int x, int n)
{
    // If number is greater than n
    if (x > n)
        return 0;

    // otherwise add count this number and
    // call two functions
    return 1 + countNumbers(x * 10, n) + countNumbers(x * 10 + 1, n);
}

// Driver code
public static void main (String[] args)
{
    int n = 120;

    System.out.println(countNumbers(1, n));
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 program to find the number of
# integers from 1 to n which contains
# digits 0's and 1's only

# Function to find the number of integers
# from 1 to n which contains 0's and 1's only
def countNumbers(x, n):

    # If number is greater than n
    if x > n :
        return 0

    # otherwise add count this number and
    # call two functions
    return (1 + countNumbers(x * 10, n) +
                countNumbers(x * 10 + 1, n))

# Driver code
if __name__ == '__main__':
    n = 120;

    print(countNumbers(1, n));

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to find the number of integers
// from 1 to n which contains digits 0's and 1's only
using System;

class GFG
{

// Function to find the number of integers
// from 1 to n which contains 0's and 1's only
static int countNumbers(int x, int n)
{
    // If number is greater than n
    if (x > n)
        return 0;

    // otherwise add count this number and
    // call two functions
    return 1 + countNumbers(x * 10, n) +
               countNumbers(x * 10 + 1, n);
}

// Driver code
public static void Main()
{
    int n = 120;

    Console.WriteLine(countNumbers(1, n));
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number of
// integers from 1 to n which contains
// digits 0's and 1's only

// Function to find the number of integers
// from 1 to n which contains 0's and 1's only
function countNumbers($x, $n)
{
    // If number is greater than n
    if ($x > $n)
        return 0;

    // otherwise add count this number and
    // call two functions
    return 1 + countNumbers($x * 10, $n) +
               countNumbers($x * 10 + 1, $n);
}

// Driver code
$n = 120;

echo(countNumbers(1, $n));

// This code is contributed
// by Code_Mech.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the
// number of integers from 1 to n
// which contains digits 0's and 1's only

// Function to find the number of
// integers from 1 to n which
// contains 0's and 1's only
function countNumbers(x, n)
{

    // If number is greater than n
    if (x > n)
        return 0;

    // Otherwise add count this number and
    // call two functions
    return 1 + countNumbers(x * 10, n) +
               countNumbers(x * 10 + 1, n);
}

// Driver code

let n = 120;

document.write(countNumbers(1, n));

// This code is contributed by Manoj.

</script>
```

**Output:** 

```
7
```
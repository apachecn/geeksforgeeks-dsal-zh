# 求一个数的重复位数和为 N 的第 M 个数

> 原文:[https://www . geesforgeks . org/find-m-th-number-其重复数字总和为-n/](https://www.geeksforgeeks.org/find-m-th-number-whose-repeated-sum-of-digits-of-a-number-is-n/)

给定两个正整数 N 和 M，任务是找到第 M 个数字，其数字的[和直到和变成一位数](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)为 N.
**示例:**

```
Input: N = 1, M = 3
Output: 19 
The first two numbers being 1 and 9.

Input: N = 2, M = 5
Output:  38 
The first four numbers being 2, 11, 20 and 29.
```

一种**天真的**方法是对所有数字进行迭代，并保留一个其和返回 n 的数字的计数。
一种**有效的**方法是找到数字的和，直到它变成 O(1)中的个位数，这里已经讨论过。因此，计算第 M 个数字的公式是:

> 第 M <sup>个</sup>号:(M-1)*9 + N

以下是上述方法的实现:

## C++

```
// C++ program to Find m-th number whose
// sum of digits of a number until
// sum becomes single digit is N
#include <bits/stdc++.h>
using namespace std;

// Function to find the M-th
// number whosesum till one digit is N
int findNumber(int n, int m)
{
    int num = (m - 1) * 9 + n;
    return num;
}

// Driver Code
int main()
{

    int n = 2, m = 5;
    cout << findNumber(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find m-th number whose
// sum of digits of a number until
// sum becomes single digit is N
class GFG
{

// Function to find the M-th
// number whosesum till one digit is N
static int findNumber(int n, int m)
{
    int num = (m - 1) * 9 + n;
    return num;
}

// Driver Code
public static void main(String args[])
{
    int n = 2, m = 5;
    System.out.print(findNumber(n, m));
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python3 program to Find m-th number
# whose sum of digits of a number
# until sum becomes single digit is N

# Function to find the M-th
# number whosesum till one digit is N
def findNumber(n, m) :

    num = (m - 1) * 9 + n;
    return num;

# Driver Code
if __name__ == "__main__" :

    n = 2 ;
    m = 5 ;
    print(findNumber(n, m))

# This code is contributed by Ryuga
```

## C#

```
// C# program to Find m-th number whose
// sum of digits of a number until
// sum becomes single digit is N
using System;

class GFG
{

// Function to find the M-th
// number whosesum till one digit is N
static int findNumber(int n, int m)
{
    int num = (m - 1) * 9 + n;
    return num;
}

// Driver Code
public static void Main()
{
    int n = 2, m = 5;
    Console.Write(findNumber(n, m));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Find m-th number whose
// sum of digits of a number until
// sum becomes single digit is N

// number whosesum till one digit is N
function findNumber($n, $m)
{
    $num = ($m - 1) * 9 + $n;
    return $num;
}

// Driver Code
$n = 2; $m = 5;
echo findNumber($n, $m);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript program to Find m-th number whose
// sum of digits of a number until
// sum becomes single digit is N   

    // Function to find the M-th
    // number whosesum till one digit is N
    function findNumber(n , m) {
        var num = (m - 1) * 9 + n;
        return num;
    }

    // Driver Code

        var n = 2, m = 5;
        document.write(findNumber(n, m));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
38
```
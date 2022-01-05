# N 位最小偶数

> 原文:[https://www . geesforgeks . org/n 位数最小偶数/](https://www.geeksforgeeks.org/smallest-even-number-with-n-digits/)

给定一个数字 **N** ，任务是找到 N 位数的最小偶数。
**例:**

```
Input: N = 1
Output: 0

Input: N = 2
Output: 10 
```

**接近** :
**情况 1** :如果 N = 1，则答案为 0。
**情况 2** :如果 N！= 1 那么答案将是(10^(N-1))因为最小偶数的数列将会像这样继续下去， *0，10，100，1000，10000，100000，* …..
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return smallest even
// number with n digits
int smallestEven(int n)
{
    if (n == 1)
        return 0;
    return pow(10, n - 1);
}

// Driver Code
int main()
{

    int n = 4;
    cout << smallestEven(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class Solution {

    // Function to return smallest even
    // number with n digits
    static int smallestEven(int n)
    {
        if (n == 1)
            return 0;
        return Math.pow(10, n - 1);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 4;
        System.out.println(smallestEven(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of
# the approach

# Function to return smallest
# even number with n digits
def smallestEven(n) :

    if (n == 1):
        return 0
    return pow(10, n - 1)

# Driver Code
n = 4
print(smallestEven(n))

# This code is contributed
# by ihritik.
```

## C#

```
// C# implementation of the approach
using System;
class Solution {

    // Function to return smallest even
    // number with n digits
    static int smallestEven(int n)
    {
        if (n == 1)
            return 0;
        return Math.pow(10, n - 1);
    }

    // Driver code
    public static void Main()
    {
        int n = 4;
        Console.Write(smallestEven(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return smallest
// even number with n digits
function smallestEven($n)
{
    if ($n == 1)
        return 0;
    return pow(10, $n - 1);
}

// Driver Code
$n = 4;
echo smallestEven($n);

// This code is contributed
// by ihritik.
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return smallest even
// number with n digits
function smallestEven(n)
{
    if (n == 1)
        return 0;
    return Math.pow(10, n - 1);
}

// Driver Code
var n = 4;
document.write(smallestEven(n));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
1000
```

**时间复杂度:** O(1)。
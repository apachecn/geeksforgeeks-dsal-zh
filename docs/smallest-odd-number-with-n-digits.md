# N 位最小奇数

> 原文:[https://www . geesforgeks . org/最小奇数带 n 位数/](https://www.geeksforgeeks.org/smallest-odd-number-with-n-digits/)

给定一个数字 **N** 。任务是找到最小的 N 位数奇数。
**例:**

```
Input: N = 1
Output: 1

Input: N = 3
Output: 101 
```

**接近**:根据 N 的值可以有两种情况
T3】情况 1 :如果 N = 1，那么答案就是 1。
**情况 2** :如果 N！= 1 那么答案将是(10^(n-1)) + 1，因为最小奇数的数列将像这样继续下去: *1，11，101，1001，10001，100001，* …。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return smallest odd
// with n digits
int smallestOdd(int n)
{
    if (n == 1)
        return 1;

    return pow(10, n - 1) + 1;
}

// Driver Code
int main()
{
    int n = 4;
    cout << smallestOdd(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class Solution {

    // Function to return smallest odd with n digits
    static int smallestOdd(int n)
    {
        if (n == 1)
            return 0;
        return Math.pow(10, n - 1) + 1;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 4;

        System.out.println(smallestOdd(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return smallest even
# number with n digits
def smallestOdd(n) :

    if (n == 1):
        return 1
    return pow(10, n - 1) + 1

# Driver Code
n = 4
print(smallestOdd(n))

# This code is contributed by ihritik.
```

## C#

```
// C# implementation of the approach
using System;
class Solution {

    // Function to return smallest odd with n digits
    static int smallestOdd(int n)
    {
        if (n == 1)
            return 0;

        return Math.pow(10, n - 1) + 1;
    }

    // Driver code
    public static void Main()
    {
        int n = 4;

        Console.Write(smallestOdd(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return smallest even
// number with n digits
function smallestOdd($n)
{
    if ($n == 1)
        return 1;
    return pow(10, $n - 1) + 1;
}

// Driver Code
$n = 4;
echo smallestOdd($n);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

  // Javascript implementation of the above approach

  // Function to return smallest odd
  // with n digits
  function smallestOdd(n) {
    if (n == 1)
      return 1;

    return Math.pow(10, n - 1) + 1;
  }

  // Driver Code
  var n = 4;
  document.write(smallestOdd(n));

  // This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
1001
```

**时间复杂度:** O(1)。
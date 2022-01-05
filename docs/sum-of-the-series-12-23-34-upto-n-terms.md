# 系列(1*2) + (2*3) + (3*4) + ……至 n 项的和

> 原文:[https://www . geesforgeks . org/sum-of-series-12-23-34-up-n-terms/](https://www.geeksforgeeks.org/sum-of-the-series-12-23-34-upto-n-terms/)

给定值 n，任务是求级数(1*2) + (2*3) + (3*4) + ……+ n 项
**例:**

```
Input: n = 2
Output: 8
Explanation:
(1*2) + (2*3)
= 2 + 6
= 8

Input: n = 3
Output: 20
Explanation:
(1*2) + (2*3) + (2*4)
= 2 + 6 + 12
= 20
```

**简单解法**逐个递归添加元素。
以下是实施情况

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return sum
int sum(int n)
{
    if (n == 1) {
        return 2;
    }
    else {
        return (n * (n + 1) + sum(n - 1));
    }
}

// Driver code
int main()
{

    int n = 2;
    cout << sum(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class Solution {

    // Function to return a the required result
    static int sum(int n)
    {
        if (n == 1) {
            return 2;
        }
        else {
            return (n * (n + 1) + sum(n - 1));
        }
    }
    // Driver code
    public static void main(String args[])
    {
        int n = 2;
        System.out.println(sum(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return sum
def sum(n):

    if (n == 1):
        return 2;
    else:
        return (n * (n + 1) + sum(n - 1));

# Driver code

n = 2;
print(sum(n));

# This code is contributed by mits
```

## C#

```
// Csharp implementation of the approach

using System;

class Solution {

    // Function to return a the required result
    static int sum(int n)
    {
        if (n == 1) {
            return 2;
        }
        else {
            return (n * (n + 1) + sum(n - 1));
        }
    }
    // Driver code
    public static void Main()
    {
        int n = 2;
        Console.WrieLine(sum(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return sum
function sum($n)
{
    if ($n == 1)
    {
        return 2;
    }
    else
    {
        return ($n * ($n + 1) +
                  sum($n - 1));
    }
}

// Driver code
$n = 2;
echo sum($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return sum
function sum(n)
{
    if (n == 1) {
        return 2;
    }
    else {
        return (n * (n + 1) + sum(n - 1));
    }
}

// Driver code
n = 2;
document.write(sum(n));

// This code is contributed by rutvik_56.

</script>
```

**Output:** 

```
8
```
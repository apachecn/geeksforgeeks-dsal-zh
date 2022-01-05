# 位数和为偶数的数字

> 原文:[https://www.geeksforgeeks.org/number-even-sum-digits/](https://www.geeksforgeeks.org/number-even-sum-digits/)

如果正整数的位数之和为偶数，则认为它是一个好数。找到第 n 个最小的好数字。
**例:**

```
Input :  n = 1
Output : 2
First good number is smallest positive
number with sum of digits even which is 2.

Input : n = 10
Output : 20
```

一个**简单的解法**就是从 1 开始遍历所有自然数。对于每个数字 x，检查数字的总和是否为偶数。如果偶数递增计数。最后返回第 n 个好数字。
一个**高效的解决方案**是基于答案中的一个模式。让我们列出前 20 个好数字。前 20 个好数字是:2、4、6、8、11、13、15、17、19、20、22、24、26、28、31、33、35、37、39、40。注意，如果 n 的最后一个数字是从 0 到 4，答案是 2*n，如果 n 的最后一个数字是从 5 到 9，答案是 2*n + 1。

## C++

```
// C++ program to find n-th
// Good number.
#include <bits/stdc++.h>
using namespace std;

// Function to find kth good number.
long long int findKthGoodNo(long long int n)
{
    // Find the last digit of n.
    int lastDig = n % 10;

    // If last digit is between
    // 0 to 4 then return 2 * n.
    if (lastDig >= 0 && lastDig <= 4)
        return n << 1;

    // If last digit is between
    // 5 to 9 then return 2*n + 1.
    else
        return (n << 1) + 1;
}

// Driver code
int main()
{
    long long int n = 10;
    cout << findKthGoodNo(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th
// Good number.
class GFG
{

    // Function to find kth good number.
    static int findKthGoodNo(int n)
    {

        // Find the last digit of n.
        int lastDig = n % 10;

        // If last digit is between
        // 0 to 4 then return 2*n.
        if (lastDig >= 0 && lastDig <= 4)
            return n << 1;

        // If last digit is between
        // 5 to 9 then return 2*n + 1.
        else
            return (n << 1) + 1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 10;

        System.out.println(findKthGoodNo(n));
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python 3 program to find
# n-th Good number.

# Function to find kth
# good number.
def findKthGoodNo(n):

    # Find the last digit of n.
    lastDig = n % 10

    # If last digit is between
    # 0 to 4 then return 2 * n.
    if (lastDig >= 0 and lastDig <= 4) :
        return n << 1

    # If last digit is between
    # 5 to 9 then return 2 * n + 1.
    else:
        return (n << 1) + 1

# Driver code
n = 10
print(findKthGoodNo(n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find n-th
// Good number.
using System;

class GFG
{

    // Function to find kth
    // good number
    public static int findKthGoodNo(int n)
    {

        // Find the last digit of n.
        int lastDig = n % 10;

        // If last digit is between
        // 0 to 4 then return 2*n.
        if (lastDig >= 0 && lastDig <= 4)
            return n << 1;

        // If last digit is between
        // 5 to 9 then return 2*n + 1.
        else
            return (n << 1) + 1;
    }

    // Driver code
    static public void Main (string []args)
    {
        int n = 10;
        Console.WriteLine(findKthGoodNo(n));
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th
// Good number.

// Function to find kth
// good number.
function findKthGoodNo($n)
{
    // Find the last digit of n.
    $lastDig = $n % 10;

    // If last digit is between
    // 0 to 4 then return 2*n.
    if ($lastDig >= 0 && $lastDig <= 4)
        return $n << 1;

    // If last digit is between
    // 5 to 9 then return 2*n + 1.
    else
        return ($n << 1) + 1;
}

// Driver code
$n = 10;
echo(findKthGoodNo($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find n-th
// Good number.

    // Function to find kth good number.
    function findKthGoodNo(n)
    {

        // Find the last digit of n.
        let lastDig = n % 10;

        // If last digit is between
        // 0 to 4 then return 2*n.
        if (lastDig >= 0 && lastDig <= 4)
            return n << 1;

        // If last digit is between
        // 5 to 9 then return 2*n + 1.
        else
            return (n << 1) + 1;
    }

// Driver code
        let n = 10;
        document.write(findKthGoodNo(n));

// This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
20
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)
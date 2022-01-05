# 从质因数只有 2 和 3 的范围内计数

> 原文:[https://www . geeksforgeeks . org/count-numbers-from-from-then-prime-factor-only-2-and-3/](https://www.geeksforgeeks.org/count-numbers-from-range-whose-prime-factors-are-only-2-and-3/)

给定两个正整数 **L** 和 **R** ，任务是计算范围**【L，R】**中的元素，其素因子只有 **2** 和 **3** 。
**举例:**

> **输入:** L = 1，R = 10
> **输出:**6
> 2 = 2
> 3 = 3
> 4 = 2 * 2
> 6 = 2 * 3
> 8 = 2 * 2 * 2
> 9 = 3 * 3
> **输入:** L = 100，R = 200
> **输出:** 5

**方法:**从 **L** 到 **R** 开始循环，对于每个元素 **num** :

*   而 **num** 可被 **2** 整除，则被 **2** 整除。
*   而 **num** 被 **3** 整除，则被 **3** 整除。
*   如果 **num = 1** 则增加**计数**为 **num** 只有 **2** 和 **3** 作为其主要因素。

最后打印**计数**。
以下是上述办法的实施情况:

## C++

```
// C++ program to count the numbers within a range
// whose prime factors are only 2 and 3
#include <bits/stdc++.h>
using namespace std;

// Function to count the number within a range
// whose prime factors are only 2 and 3
int findTwoThreePrime(int l, int r)
{
    // Start with 2 so that 1 doesn't get counted
    if (l == 1)
        l++;

    int count = 0;

    for (int i = l; i <= r; i++) {
        int num = i;

        // While num is divisible by 2, divide it by 2
        while (num % 2 == 0)
            num /= 2;

        // While num is divisible by 3, divide it by 3
        while (num % 3 == 0)
            num /= 3;

        // If num got reduced to 1 then it has
        // only 2 and 3 as prime factors
        if (num == 1)
            count++;
    }

    return count;
}

// Driver code
int main()
{
    int l = 1, r = 10;
    cout << findTwoThreePrime(l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to count the numbers within a range
// whose prime factors are only 2 and 3

import java.io.*;

class GFG {

// Function to count the number within a range
// whose prime factors are only 2 and 3
static int findTwoThreePrime(int l, int r)
{
    // Start with 2 so that 1 doesn't get counted
    if (l == 1)
        l++;

    int count = 0;

    for (int i = l; i <= r; i++) {
        int num = i;

        // While num is divisible by 2, divide it by 2
        while (num % 2 == 0)
            num /= 2;

        // While num is divisible by 3, divide it by 3
        while (num % 3 == 0)
            num /= 3;

        // If num got reduced to 1 then it has
        // only 2 and 3 as prime factors
        if (num == 1)
            count++;
    }

    return count;
}

// Driver code
    public static void main (String[] args) {

        int l = 1, r = 10;
        System.out.println (findTwoThreePrime(l, r));
    }
//This code is contributed by ajit   
}
```

## 蟒蛇 3

```
# Python3 program to count the numbers
# within a range whose prime factors
# are only 2 and 3

# Function to count the number within
# a range whose prime factors are only
# 2 and 3
def findTwoThreePrime(l, r) :

    # Start with 2 so that 1
    # doesn't get counted
    if (l == 1) :
        l += 1

    count = 0

    for i in range(l, r + 1) :
        num = i

        # While num is divisible by 2,
        # divide it by 2
        while (num % 2 == 0) :
            num //= 2;

        # While num is divisible by 3,
        # divide it by 3
        while (num % 3 == 0) :
            num //= 3

        # If num got reduced to 1 then it has
        # only 2 and 3 as prime factors
        if (num == 1) :
            count += 1

    return count

# Driver code
if __name__ == "__main__" :

    l = 1
    r = 10

    print(findTwoThreePrime(l, r))

# This code is contributed by Ryuga
```

## C#

```
// C# program to count the numbers
// within a range whose prime factors
// are only 2 and 3
using System;

class GFG
{

// Function to count the number
// within a range whose prime
// factors are only 2 and 3
static int findTwoThreePrime(int l, int r)
{
    // Start with 2 so that 1
    // doesn't get counted
    if (l == 1)
        l++;

    int count = 0;

    for (int i = l; i <= r; i++)
    {
        int num = i;

        // While num is divisible by 2,
        // divide it by 2
        while (num % 2 == 0)
            num /= 2;

        // While num is divisible by 3,
        // divide it by 3
        while (num % 3 == 0)
            num /= 3;

        // If num got reduced to 1 then it 
        // has only 2 and 3 as prime factors
        if (num == 1)
            count++;
    }
    return count;
}

// Driver code
static public void Main ()
{
    int l = 1, r = 10;
    Console.WriteLine(findTwoThreePrime(l, r));
}
}

// This code is contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the numbers
// within a range whose prime factors
// are only 2 and 3

// Function to count the number
// within a range whose prime
// factors are only 2 and 3
function findTwoThreePrime($l, $r)
{
    // Start with 2 so that 1
    // doesn't get counted
    if ($l == 1)
        $l++;

    $count = 0;

    for ($i = $l; $i <= $r; $i++)
    {
        $num = $i;

        // While num is divisible by 2,
        // divide it by 2
        while ($num % 2 == 0)
            $num /= 2;

        // While num is divisible by 3,
        // divide it by 3
        while ($num % 3 == 0)
            $num /= 3;

        // If num got reduced to 1 then it has
        // only 2 and 3 as prime factors
        if ($num == 1)
            $count++;
    }
    return $count;
}

// Driver code
$l = 1;
$r = 10;
echo findTwoThreePrime($l, $r);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to count the numbers
    // within a range whose prime factors
    // are only 2 and 3

    // Function to count the number
    // within a range whose prime
    // factors are only 2 and 3
    function findTwoThreePrime(l, r)
    {
        // Start with 2 so that 1
        // doesn't get counted
        if (l == 1)
            l++;

        let count = 0;

        for (let i = l; i <= r; i++)
        {
            let num = i;

            // While num is divisible by 2,
            // divide it by 2
            while (num % 2 == 0)
                num = parseInt(num / 2, 10);

            // While num is divisible by 3,
            // divide it by 3
            while (num % 3 == 0)
                num = parseInt(num / 3, 10);

            // If num got reduced to 1 then it 
            // has only 2 and 3 as prime factors
            if (num == 1)
                count++;
        }
        return count;
    }

    let l = 1, r = 10;
    document.write(findTwoThreePrime(l, r));

</script>
```

**时间复杂度:** O((r-l)*log2(r-l))

**辅助空间:** O(1)
# 不能被[2，10]

范围内的任何数整除的数

> 原文:[https://www . geesforgeks . org/numbers-不能被 2-10 范围内的任何数字除尽/](https://www.geeksforgeeks.org/numbers-that-are-not-divisible-by-any-number-in-the-range-2-10/)

给定一个整数 **N** 。任务是找出从 **1** 到 **N** 的所有数字的计数，这些数字不能被**【2，10】**范围内的任何数字整除。

**示例:**

> **输入:** N = 12
> **输出:** 2
> 1，11 是[1，12]范围内唯一不能被 2 到 10 的任何数字整除的数字
> 
> **输入:**N = 20
> T3】输出: 5

**趋近:**从 **1** 到 **n** 的不能被 **2** 到 **10** 的任何数整除的总数等于 n 减去从 **2** 到 **10** 的可被某些数整除的数。

从 **2** 到 **10** 的可被某些数整除的数集合，可以看作是从 **1** 到 **n** 的可被 **2** 整除的数集合，可被 **3** 整除的数集合，依此类推，直到 **10** 。

注意:可被 **4** 或 **6** 或 **8** 整除的数集合是可被 **2** 整除的数集合的子集，可被 **6** 或 **9** 整除的数集合是可被 **3** 整除的数集合的子集。所以不需要联合 **9** 套，只联合 **2、3、5、7** 套就够了。

从 **1** 到 **n** 可被 **2、3、5、7** 整除的数字集合的大小，可以用包含-排除原理来计算，该原理说每个单个集合的大小应该相加，两两相交的大小应该相减，三个集合的所有相交的大小应该相加，以此类推。

从 **1** 到 **n** 被 **2** 整除的一组数字的大小等于 **⌊n / 2⌋** ，从 **1** 到 **n** 被 **2 和 3** 整除的一组数字的大小等于 **⌊n / (2 * 3)⌋** 以此类推。

因此，公式是**n-√n/2-√n/3-√n/5-√n/7-√n/(2 * 3)]+√n/(2 * 5)]+√n/(2 * 7)]+√n/(3 * 5)]+√n/(3 * 7)]+√n/(5 * 7)]。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of numbers
// from 1 to N which are not divisible by
// any number in the range [2, 10]
int countNumbers(int n)
{
    return n - n / 2 - n / 3 - n / 5 - n / 7
           + n / 6 + n / 10 + n / 14 + n / 15 + n / 21 + n / 35
           - n / 30 - n / 42 - n / 70 - n / 105 + n / 210;
}

// Driver code
int main()
{
    int n = 20;
    cout << countNumbers(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of numbers
// from 1 to N which are not divisible by
// any number in the range [2, 10]
static int countNumbers(int n)
{
    return n - n / 2 - n / 3 - n / 5 - n / 7
        + n / 6 + n / 10 + n / 14 + n / 15 + n / 21 + n / 35
        - n / 30 - n / 42 - n / 70 - n / 105 + n / 210;
}

// Driver code
public static void main (String[] args)
{
    int n = 20;
    System.out.println(countNumbers(n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of numbers
# from 1 to N which are not divisible by
# any number in the range [2, 10]
def countNumbers(n):
    return (n - n // 2 - n // 3 - n // 5 - n // 7 +
             n // 6 + n // 10 + n // 14 + n // 15 +
             n // 21 + n // 35 - n // 30 - n // 42 -
             n // 70 - n // 105 + n // 210)

# Driver code
if __name__ == '__main__':
    n = 20
    print(countNumbers(n))

# This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of numbers
// from 1 to N which are not divisible by
// any number in the range [2, 10]
static int countNumbers(int n)
{
    return n - n / 2 - n / 3 - n / 5 - n / 7
        + n / 6 + n / 10 + n / 14 + n / 15 + n / 21 + n / 35
        - n / 30 - n / 42 - n / 70 - n / 105 + n / 210;
}

// Driver code
static void Main()
{
    int n = 20;
    Console.WriteLine(countNumbers(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of numbers
// from 1 to N which are not divisible by
// any number in the range [2, 10]
function countNumbers($n)
{
    return (int)($n - $n / 2) - (int)($n / 3 ) -
           (int)($n / 5 ) - (int)($n / 7) +
           (int)($n / 6 ) + (int)($n / 10) +
           (int)($n / 14) + (int)($n / 15) +
           (int)($n / 21) + (int)($n / 35) -
           (int)($n / 30) - (int)($n / 42) -
           (int)($n / 70) - (int)($n / 105) +
           (int)($n / 210);
}

// Driver code
$n = 20;
echo(countNumbers($n));

// This code is contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of numbers
// from 1 to N which are not divisible by
// any number in the range [2, 10]
function countNumbers(n)
{
    return n - parseInt(n / 2, 10) - parseInt(n / 3, 10) -
               parseInt(n / 5, 10) - parseInt(n / 7, 10) +
               parseInt(n / 6, 10) + parseInt(n / 10, 10) +
               parseInt(n / 14, 10) + parseInt(n / 15, 10) +
               parseInt(n / 21, 10) + parseInt(n / 35, 10) -
               parseInt(n / 30, 10) - parseInt(n / 42, 10) -
               parseInt(n / 70, 10) - parseInt(n / 105, 10) +
               parseInt(n / 210, 10);
}

// Driver code
let n = 20;

document.write(countNumbers(n));

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
5
```
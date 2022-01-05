# 求小于等于 N 的正整数中有奇数位数的个数

> 原文:[https://www . geesforgeks . org/find-小于或等于 n 的正整数位数/T1](https://www.geeksforgeeks.org/find-the-number-of-positive-integers-less-than-or-equal-to-n-that-have-an-odd-number-of-digits/)

给定一个整数 **N** ，其中 **1 ≤ N ≤ 10 <sup>5</sup>** ，任务是找出小于或等于 **N** 的正整数个数，其位数为奇数，没有前导零。
**举例:**

> **输入:** N = 11
> **输出:** 9
> 1、2、3、…、8、9 为奇数位数的数字≤ 11
> 。
> **输入:** N = 893
> **输出:** 803

**简单方法:**从 **1** 到 **N** 遍历，检查每个数字是否包含奇数。
**有效方法:**为数值:

*   当 **N < 10** 时，有效数字的计数将为 **N** 。
*   当 **N / 10 < 10** 然后 **9** 时。
*   当 **N / 100 < 10** 然后**9+N–99**时。
*   当 **N / 1000 < 10** 然后 **9 + 900** 时。
*   当 **N / 10000 < 10** 时，则**909+N–9999**。
*   否则 **90909** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of
// positive integers less than or equal
// to N that have odd number of digits
int odd_digits(int n)
{
    if (n < 10)
        return n;
    else if (n / 10 < 10)
        return 9;
    else if (n / 100 < 10)
        return 9 + n - 99;
    else if (n / 1000 < 10)
        return 9 + 900;
    else if (n / 10000 < 10)
        return 909 + n - 9999;
    else
        return 90909;
}

// Driver code
int main()
{
    int n = 893;

    cout << odd_digits(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the number of
// positive integers less than or equal
// to N that have odd number of digits
static int odd_digits(int n)
{
    if (n < 10)
        return n;
    else if (n / 10 < 10)
        return 9;
    else if (n / 100 < 10)
        return 9 + n - 99;
    else if (n / 1000 < 10)
        return 9 + 900;
    else if (n / 10000 < 10)
        return 909 + n - 9999;
    else
        return 90909;
}

// Driver code
public static void main(String []args)
{
    int n = 893;

    System.out.println(odd_digits(n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of
# positive integers less than or equal
# to N that have odd number of digits
def odd_digits(n) :

    if (n < 10) :
        return n;
    elif (n / 10 < 10) :
        return 9;
    elif (n / 100 < 10) :
        return 9 + n - 99;
    elif (n / 1000 < 10) :
        return 9 + 900;
    elif (n / 10000 < 10) :
        return 909 + n - 9999;
    else :
        return 90909;

# Driver code
if __name__ == "__main__" :

    n = 893;

    print(odd_digits(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the number of
// positive integers less than or equal
// to N that have odd number of digits
static int odd_digits(int n)
{
    if (n < 10)
        return n;
    else if (n / 10 < 10)
        return 9;
    else if (n / 100 < 10)
        return 9 + n - 99;
    else if (n / 1000 < 10)
        return 9 + 900;
    else if (n / 10000 < 10)
        return 909 + n - 9999;
    else
        return 90909;
}

// Driver code
public static void Main(String []args)
{
    int n = 893;

    Console.WriteLine(odd_digits(n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Java script implementation of the approach

// Function to return the number of
// positive integers less than or equal
// to N that have odd number of digits
function odd_digits( n)
{
    if (n < 10)
        return n;
    else if (n / 10 < 10)
        return 9;
    else if (n / 100 < 10)
        return 9 + n - 99;
    else if (n / 1000 < 10)
        return 9 + 900;
    else if (n / 10000 < 10)
        return 909 + n - 9999;
    else
        return 90909;
}

// Driver code
let n = 893;

    document.write(odd_digits(n));

// This code is contributed by sravan kumar Gottumukkala
</script>
```

**Output:** 

```
803
```
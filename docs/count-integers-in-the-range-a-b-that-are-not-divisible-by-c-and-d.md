# 计算范围【A，B】内不能被 C 和 D 整除的整数

> 原文:[https://www . geesforgeks . org/count-整数范围内不能被 c 和 d 整除的 a-b/](https://www.geeksforgeeks.org/count-integers-in-the-range-a-b-that-are-not-divisible-by-c-and-d/)

给定四个整数 **A、B、C** 和 **D** 。任务是找出**【A，B】**范围内不能被 **C** 和 **D** 整除的整数个数。
**举例:**

> **输入:** A = 4，B = 9，C = 2，D = 3
> **输出:** 2
> 5 和 7 就是这样的整数。
> **输入:** A = 10，B = 50，C = 4，D = 6
> **输出:** 28

**方法:**首先在要求的答案中包含范围内的所有整数，即**B–A+1**。然后去掉所有能被 **C** 和 **D** 整除的数，最后加上所有能被 **C** 和 **D** 整除的数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// integers from the range [a, b] that
// are not divisible by c and d
int countNums(int a, int b, int c, int d)
{
    // Numbers which are divisible by c
    int x = b / c - (a - 1) / c;

    // Numbers which are divisible by d
    int y = b / d - (a - 1) / d;

    // Find lowest common factor of c and d
    int k = (c * d) / __gcd(c, d);

    // Numbers which are divisible by both c and d
    int z = b / k - (a - 1) / k;

    // Return the required answer
    return b - a + 1 - x - y + z;
}

// Driver code
int main()
{
    int a = 10, b = 50, c = 4, d = 6;

    cout << countNums(a, b, c, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of
// integers from the range [a, b] that
// are not divisible by c and d
static int countNums(int a, int b, int c, int d)
{
    // Numbers which are divisible by c
    int x = b / c - (a - 1) / c;

    // Numbers which are divisible by d
    int y = b / d - (a - 1) / d;

    // Find lowest common factor of c and d
    int k = (c * d) / __gcd(c, d);

    // Numbers which are divisible by both c and d
    int z = b / k - (a - 1) / k;

    // Return the required answer
    return b - a + 1 - x - y + z;
}
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);    
}

// Driver code
public static void main(String []args)
{
    int a = 10, b = 50, c = 4, d = 6;

    System.out.println(countNums(a, b, c, d));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd

# Function to return the count of
# integers from the range [a, b] that
# are not divisible by c and d
def countNums(a, b, c, d) :

    # Numbers which are divisible by c
    x = b // c - (a - 1) // c;

    # Numbers which are divisible by d
    y = b // d - (a - 1) // d;

    # Find lowest common factor of c and d
    k = (c * d) // gcd(c, d);

    # Numbers which are divisible
    # by both c and d
    z = b // k - (a - 1) // k;

    # Return the required answer
    return (b - a + 1 - x - y + z);

# Driver code
if __name__ == "__main__" :

    a = 10; b = 50; c = 4; d = 6;

    print(countNums(a, b, c, d));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// integers from the range [a, b] that
// are not divisible by c and d
static int countNums(int a, int b, int c, int d)
{
    // Numbers which are divisible by c
    int x = b / c - (a - 1) / c;

    // Numbers which are divisible by d
    int y = b / d - (a - 1) / d;

    // Find lowest common factor of c and d
    int k = (c * d) / __gcd(c, d);

    // Numbers which are divisible by both c and d
    int z = b / k - (a - 1) / k;

    // Return the required answer
    return b - a + 1 - x - y + z;
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);    
}

// Driver code
public static void Main(String []args)
{
    int a = 10, b = 50, c = 4, d = 6;

    Console.WriteLine(countNums(a, b, c, d));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// integers from the range [a, b] that
// are not divisible by c and d
function countNums(a, b, c, d)
{
    // Numbers which are divisible by c
    let x = parseInt(b / c) - parseInt((a - 1) / c);

    // Numbers which are divisible by d
    let y = parseInt(b / d) - parseInt((a - 1) / d);

    // Find lowest common factor of c and d
    let k = parseInt((c * d) / __gcd(c, d));

    // Numbers which are divisible by both c and d
    let z = parseInt(b / k) - parseInt((a - 1) / k);

    // Return the required answer
    return b - a + 1 - x - y + z;
}

function __gcd(a, b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);    
}

// Driver code
    let a = 10, b = 50, c = 4, d = 6;

    document.write(countNums(a, b, c, d));

</script>
```

**Output:** 

```
28
```
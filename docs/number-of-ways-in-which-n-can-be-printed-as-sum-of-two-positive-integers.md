# N 可以表示为两个正整数之和的方式数

> 原文:[https://www . geeksforgeeks . org/n 可打印为两个正整数之和的方式数/](https://www.geeksforgeeks.org/number-of-ways-in-which-n-can-be-printed-as-sum-of-two-positive-integers/)

给定一个数字 **N** ，任务是找出 **N** 可以表示为两个正整数之和的唯一方法的数量。
**例:**

> **输入:** N = 7
> **输出:** 3
> (1 + 6)、(2 + 5)和(3 + 4)。
> **输入:** N = 200
> **输出:** 100

**方法:**数可以表示为两个正整数之和的方式有**1+(N–1)、2+(N–2)、……、(N–1)+1**和**(N–2)+2**。系列中有**N–1**个术语，它们成对出现，即 **(X + Y，Y + X)** 。所以需要的计数是 **N / 2** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of
// distinct ways to represent n
// as the sum of two integers
int ways(int n)
{
    return n / 2;
}

// Driver code
int main()
{
    int n = 2;

    cout << ways(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function to return the number of
    // distinct ways to represent n
    // as the sum of two integers
    static int ways(int n)
    {
        return n / 2;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 2;

        System.out.println(ways(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of
# distinct ways to represent n
# as the sum of two integers
def ways(n):
    return n // 2

# Driver code
n = 2

print(ways(n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the number of
// distinct ways to represent n
// as the sum of two integers
static int ways(int n)
{
    return n / 2;
}

// Driver code
public static void Main()
{
    int n = 2;

    Console.WriteLine(ways(n));
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number of
// distinct ways to represent n
// as the sum of two integers
function ways(n)
{
    return parseInt(n / 2);
}

// Driver code
var n = 2;
document.write(ways(n));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1
```
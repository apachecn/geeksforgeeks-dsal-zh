# 祖克曼数字

> 原文:[https://www.geeksforgeeks.org/zuckerman-numbers/](https://www.geeksforgeeks.org/zuckerman-numbers/)

给定一个整数 **N** ，任务是检查 **N** 是否为祖克曼数。

> 祖克曼数是一个可以被其数字的乘积
> 整除的数

**例:**

> **输入:** N = 115
> **输出:**是
> **解释:**
> 1*1*5 = 5 和 115 % 5 = 0
> **输入:** N = 28
> **输出:**否

**方法:**思路是找出 N 的位数乘积，检查 N 是否能被它的位数乘积整除。如果是，那么数字 N 是朱克曼数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation to check if N
// is a Zuckerman number

#include <bits/stdc++.h>
using namespace std;

// Function to get product of digits
int getProduct(int n)
{
    int product = 1;

    while (n != 0) {
        product = product * (n % 10);
        n = n / 10;
    }

    return product;
}

// Function to check if N is an
// Zuckerman number
bool isZuckerman(int n)
{
    return n % getProduct(n) == 0;
}

// Driver code
int main()
{
    int n = 115;
    if (isZuckerman(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if N
// is a Zuckerman number
class GFG{

// Function to get product of digits
static int getProduct(int n)
{
    int product = 1;

    while (n != 0)
    {
        product = product * (n % 10);
        n = n / 10;
    }
    return product;
}

// Function to check if N is an
// Zuckerman number
static boolean isZuckerman(int n)
{
    return n % getProduct(n) == 0;
}

// Driver code
public static void main(String[] args)
{
    int n = 115;

    if (isZuckerman(n))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 implementation to check if N
# is a Zuckerman number

# Function to get product of digits
def getProduct(n):
    product = 1

    while (n > 0):
        product = product * (n % 10)
        n = n // 10

    return product

# Function to check if N is an
# Zuckerman number
def isZuckerman(n):

    return n % getProduct(n) == 0

# Driver code
N = 115
if (isZuckerman(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by Vishal Maurya
```

## C#

```
// C# implementation to check if N
// is a Zuckerman number
using System;
class GFG{

// Function to get product of digits
static int getProduct(int n)
{
    int product = 1;

    while (n != 0)
    {
        product = product * (n % 10);
        n = n / 10;
    }
    return product;
}

// Function to check if N is an
// Zuckerman number
static bool isZuckerman(int n)
{
    return n % getProduct(n) == 0;
}

// Driver code
public static void Main(String[] args)
{
    int n = 115;

    if (isZuckerman(n))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// Javascript implementation to check if N
// is a Zuckerman number

    // Function to get product of digits
    function getProduct( n) {
        let product = 1;

        while (n != 0) {
            product = product * (n % 10);
            n = parseInt(n / 10);
        }
        return product;
    }

    // Function to check if N is an
    // Zuckerman number
    function isZuckerman( n) {
        return n % getProduct(n) == 0;
    }

    // Driver code
    let n = 115;

    if (isZuckerman(n)) {
        document.write("Yes");
    } else {
        document.write("No");
    }

// This code is contributed by todaysgaurav
</script>
```

**Output**

```
Yes
```

**时间复杂度:**O(log<sub>10</sub>n)

**参考文献:** [OEIS](https://oeis.org/A007602)
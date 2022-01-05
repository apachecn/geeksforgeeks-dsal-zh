# 当给出其乘积为 N 的两个因子的位置时，求 N 的因子个数

> 原文:[https://www . geeksforgeeks . org/find-当其两个因子的位置被给定时因子的数量/](https://www.geeksforgeeks.org/find-number-of-factors-of-n-when-location-of-its-two-factors-whose-product-is-n-is-given/)

给定 **a** 和 **b** ，当因子按升序排列时，它们表示乘积等于 N 的 N 的两个因子的位置。任务是找到 N.
的因子总数**示例:**

> **输入:** a = 2，b = 3
> **输出:** 4
> N = 6
> 因子为{1，2，3，6}
> 因子个数为 4
> **输入:** a = 13，b = 36
> **输出:** 48

**方法:**解决方法基于观察。
假设 N = 50 。那么 N 有 6 个因子 1，2，5，10，25 和 50。1 和 50 相乘总会得到 50( N)的值。同样，通过将 2 和 25 相乘得到 N 值，同样通过将 5 和 10 相乘得到 N 值。因此，这里我们可以看到，当以递增顺序排列时，通过将两个因子相乘得到 N 值。乘法必须以这样的方式进行:第一个因子和乘法的最后一个因子得到 N，第二个因子和乘法的最后一个因子得到 N，以此类推。
有了这个模式，我们就能找到计算因子个数的方法。比方说，乘法的第一个和第四个因子给出了 n。这意味着有 4 个因子(第一个、第二个、第三个和第四个)。如果第二个和第三个因子的乘积给出 N，那么我们可以说在第一个位置和第四个位置上一定有一个因子。
因此，因子数将等于**a+b–1**。
以下是上述方法的实施:

## C++

```
// C++ program to implement
// the above problem
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of factors
void findFactors(int a, int b)
{
    int c;
    c = a + b - 1;

    // print the number of factors
    cout << c;
}

// Driver code
int main()
{
    // initialize the factors position
    int a, b;
    a = 13;
    b = 36;

    findFactors(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above problem
class GFG
{

// Function to find the number of factors
static void findFactors(int a, int b)
{
    int c;
    c = a + b - 1;

    // print the number of factors
    System.out.print(c);
}

// Driver code
public static void main(String[] args)
{
    // initialize the factors position
    int a, b;
    a = 13;
    b = 36;

    findFactors(a, b);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above problem

# Function to find the number of factors
def findFactors(a, b):
    c = a + b - 1

    # print the number of factors
    print(c)

# Driver code
if __name__ == '__main__':

    # initialize the factors position
    a = 13
    b = 36
    findFactors(a, b)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to implement
// the above problem
using System;

class GFG
{

// Function to find the number of factors
static void findFactors(int a, int b)
{
    int c;
    c = a + b - 1;

    // print the number of factors
    Console.Write(c);
}

// Driver code
public static void Main(String[] args)
{
    // initialize the factors position
    int a, b;
    a = 13;
    b = 36;

    findFactors(a, b);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above problem

// Function to find the number of factors
function findFactors(a, b)
{
    let c;
    c = a + b - 1;

    // print the number of factors
    document.write(c);
}

// Driver code

// initialize the factors position
let a, b;
a = 13;
b = 36;

findFactors(a, b);

</script>
```

**Output:** 

```
48
```

**时间复杂度:** O(1)
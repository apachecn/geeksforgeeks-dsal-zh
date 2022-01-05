# 给定两个数相加得到的原始比值和新比值的两个数之和

> 原文:[https://www . geeksforgeeks . org/两个数之和-如果给定每个数加上给定的数得到原始比和新比/](https://www.geeksforgeeks.org/sum-of-two-numbers-if-the-original-ratio-and-new-ratio-obtained-by-adding-a-given-number-to-each-number-is-given/)

给定两个未知数的比率 **a : b** 。当两个数字都增加一个给定的整数 **x** 时，比率变成 **c : d** 。任务是找出这两个数的和。
**举例:**

> **输入:** a = 2，b = 3，c = 8，d = 9，x = 6
> **输出:** 5
> 原数为 2 和 3
> 原比值= 2:3
> 加 6 后比值变为 8:9
> 2 + 3 = 5
> **输入:** a = 1，b = 2，c = 9，d = 13，x = 5
> **输出:** 12

**逼近:**让数字之和为 **S** 。那么，数字可以是 **(a * S)/(a + b)** 和 **(b * S)/(a + b)** 。
现在，如给定的:

```
(((a * S) / (a + b)) + x) / (((b * S) / (a + b)) + x) = c / d
or ((a * S) + x * (a + b)) / ((b * S) + x * (a + b)) = c / d
So, S = (x * (a + b) * (c - d)) / (ad - bc)
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of numbers
// which are in the ration a:b and after
// adding x to both the numbers
// the new ratio becomes c:d
double sum(double a, double b, double c, double d, double x)
{
    double ans = (x * (a + b) * (c - d)) / ((a * d) - (b * c));
    return ans;
}

// Driver code
int main()
{
    double a = 1, b = 2, c = 9, d = 13, x = 5;

    cout << sum(a, b, c, d, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the sum of numbers
    // which are in the ration a:b and after
    // adding x to both the numbers
    // the new ratio becomes c:d
    static double sum(double a, double b,
                      double c, double d,
                      double x)
    {
        double ans = (x * (a + b) * (c - d)) /
                         ((a * d) - (b * c));
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        double a = 1, b = 2, c = 9, d = 13, x = 5;

        System.out.println(sum(a, b, c, d, x));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum of numbers
# which are in the ration a:b and after
# adding x to both the numbers
# the new ratio becomes c:d
def sum(a, b, c, d, x):

    ans = ((x * (a + b) * (c - d)) /
               ((a * d) - (b * c)));
    return ans;

# Driver code
if __name__ == '__main__':

    a, b, c, d, x = 1, 2, 9, 13, 5;

    print(sum(a, b, c, d, x));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the sum of numbers
    // which are in the ration a:b and after
    // adding x to both the numbers
    // the new ratio becomes c:d
    static double sum(double a, double b,
                      double c, double d,
                      double x)
    {
        double ans = (x * (a + b) * (c - d)) /
                         ((a * d) - (b * c));
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        double a = 1, b = 2,
               c = 9, d = 13, x = 5;

        Console.WriteLine(sum(a, b, c, d, x));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// javascript implementation of the above approach

// Function to return the sum of numbers
// which are in the ration a:b and after
// adding x to both the numbers
// the new ratio becomes c:d
function sum(a , b, c , d, x)
{
    var ans = (x * (a + b) * (c - d)) /
                     ((a * d) - (b * c));
    return ans;
}

// Driver code

var a = 1, b = 2, c = 9, d = 13, x = 5;

document.write(sum(a, b, c, d, x));

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
12
```
# 小于等于给定整数的 2 的最高幂

> 原文:[https://www . geesforgeks . org/2 的最高次方小于或等于给定整数/](https://www.geeksforgeeks.org/highest-power-of-2-less-than-or-equal-to-given-integer/)

给定一个整数 **N** ，任务是找到小于或等于 **N** 的 2 的最高幂。

**示例:**

> **输入:** N = 9
> **输出:** 8
> **说明:**
> 2 小于 9 的最高幂是 8。
> 
> **输入:** N = -20
> **输出:** -32
> **说明:**
> 2 小于-20 的最高功率为-32。
> 
> **输入:** N = -84
> **输出:** -128

**方法:**思路是用[对数](https://www.geeksforgeeks.org/logarithm/)来解决上述问题。对于任何给定的数字 N，它可以是正的，也可以是负的。对于每种情况，可以执行以下任务:

1.  如果输入为正:**楼层(原木 <sub>2</sub> (N))** 即可计算。
2.  如果输入为负:**可以计算 ceil(log <sub>2</sub> (N))** ，并在该值上加上一个 **-ve** 符号。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the lowest power
// of 2 close to given positive number
int powOfPositive(int n)
{
    // Floor function is used to determine
    // the value close to the number
    int pos = floor(log2(n));
    return pow(2, pos);
}

// Function to return the lowest power
// of 2 close to given negative number
int powOfNegative(int n)
{
    // Ceil function is used for negative numbers
    // as -1 > -4\. It would be opposite
    // to positive numbers where 1 < 4
    int pos = ceil(log2(n));
    return (-1 * pow(2, pos));
}

// Function to find the highest power of 2
void highestPowerOf2(int n)
{

    // To check if the given number
    // is positive or negative
    if (n > 0) {
        cout << powOfPositive(n);
    }
    else {
        // If the number is negative,
        // then the ceil of the positive number
        // is calculated and
        // negative sign is added
        n = -n;
        cout << powOfNegative(n);
    }
}

// Driver code
int main()
{
    int n = -24;
    highestPowerOf2(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the lowest power
    // of 2 close to given positive number
    static int powOfPositive(int n)
    {
        // Floor function is used to determine
        // the value close to the number
        int pos = (int)Math.floor((Math.log(n)/Math.log(2)));
        return (int)Math.pow(2, pos);
    }

    // Function to return the lowest power
    // of 2 close to given negative number
    static int powOfNegative(int n)
    {
        // Ceil function is used for negative numbers
        // as -1 > -4\. It would be opposite
        // to positive numbers where 1 < 4
        int pos = (int)Math.ceil((Math.log(n)/Math.log(2)));
        return (int)(-1 * Math.pow(2, pos));
    }

    // Function to find the highest power of 2
    static void highestPowerOf2(int n)
    {

        // To check if the given number
        // is positive or negative
        if (n > 0)
        {
            System.out.println(powOfPositive(n));
        }
        else
        {
            // If the number is negative,
            // then the ceil of the positive number
            // is calculated and
            // negative sign is added
            n = -n;
            System.out.println(powOfNegative(n));
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = -24;
        highestPowerOf2(n);
    }
}

// This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the lowest power
    // of 2 close to given positive number
    static int powOfPositive(int n)
    {
        // Floor function is used to determine
        // the value close to the number
        int pos = (int)Math.Floor((Math.Log(n)/Math.Log(2)));
        return (int)Math.Pow(2, pos);
    }

    // Function to return the lowest power
    // of 2 close to given negative number
    static int powOfNegative(int n)
    {
        // Ceil function is used for negative numbers
        // as -1 > -4\. It would be opposite
        // to positive numbers where 1 < 4
        int pos = (int)Math.Ceiling((Math.Log(n)/Math.Log(2)));
        return (int)(-1 * Math.Pow(2, pos));
    }

    // Function to find the highest power of 2
    static void highestPowerOf2(int n)
    {

        // To check if the given number
        // is positive or negative
        if (n > 0)
        {
            Console.WriteLine(powOfPositive(n));
        }
        else
        {
            // If the number is negative,
            // then the ceil of the positive number
            // is calculated and
            // negative sign is added
            n = -n;
            Console.WriteLine(powOfNegative(n));
        }
    }

    // Driver code
    public static void Main()
    {
        int n = -24;
        highestPowerOf2(n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from math import floor,ceil,log2

# Function to return the lowest power
# of 2 close to given positive number
def powOfPositive(n) :

    # Floor function is used to determine
    # the value close to the number
    pos = floor(log2(n));
    return 2**pos;

# Function to return the lowest power
# of 2 close to given negative number
def powOfNegative(n) :

    # Ceil function is used for negative numbers
    # as -1 > -4\. It would be opposite
    # to positive numbers where 1 < 4
    pos = ceil(log2(n));

    return (-1 * pow(2, pos));

# Function to find the highest power of 2
def highestPowerOf2(n) :

    # To check if the given number
    # is positive or negative
    if (n > 0) :
        print(powOfPositive(n));

    else :

        # If the number is negative,
        # then the ceil of the positive number
        # is calculated and
        # negative sign is added
        n = -n;
        print(powOfNegative(n));

# Driver code
if __name__ == "__main__" :

    n = -24;
    highestPowerOf2(n);

# This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the lowest power
// of 2 close to given positive number
function powOfPositive(n)
{

    // Floor function is used to determine
    // the value close to the number
    let pos = Math.floor(Math.log2(n));
    return Math.pow(2, pos);
}

// Function to return the lowest power
// of 2 close to given negative number
function powOfNegative(n)
{

    // Ceil function is used for negative numbers
    // as -1 > -4\. It would be opposite
    // to positive numbers where 1 < 4
    let pos = Math.ceil(Math.log2(n));
    return (-1 * Math.pow(2, pos));
}

// Function to find the highest power of 2
function highestPowerOf2(n)
{

    // To check if the given number
    // is positive or negative
    if (n > 0)
    {
        document.write(powOfPositive(n));
    }
    else
    {

        // If the number is negative,
        // then the ceil of the positive number
        // is calculated and
        // negative sign is added
        n = -n;
        document.write(powOfNegative(n));
    }
}

// Driver code
let n = -24;

highestPowerOf2(n);

// This code is contributed by mohit kumar 29

</script>
```

**Output:** 

```
-32
```
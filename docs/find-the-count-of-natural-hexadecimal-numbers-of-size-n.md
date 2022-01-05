# 求 N 大小的自然十六进制数的个数

> 原文:[https://www . geesforgeks . org/find-自然数-十六进制-大小数-n/](https://www.geeksforgeeks.org/find-the-count-of-natural-hexadecimal-numbers-of-size-n/)

给定一个整数 **N** ，任务是用 **N** 位找到自然十六进制数的计数。
**例:**

> **输入:** N = 1
> **输出:** 15
> **输入:** N = 2
> **输出:** 240

**趋近:**可以观察到对于 **N = 1，2，3，…** 的值，会形成一个系列为 **15，240，3840，61440，983040，15728640，…** 这是一个 GP 系列，其公比为 **16** ， **a = 15** 。
因此 **n <sup>第</sup>** 项将为 **15 * pow(16，n–1)**。
所以 **n 位**自然十六进制数的计数将为 **15 *幂(16，n–1)**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of n-digit
// natural hexadecimal numbers
int count(int n)
{
    return 15 * pow(16, n - 1);
}

// Driver code
int main()
{
    int n = 2;
    cout << count(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of n-digit
// natural hexadecimal numbers
static int count(int n)
{
    return (int) (15 * Math.pow(16, n - 1));
}

// Driver code
public static void main(String args[])
{
    int n = 2;
    System.out.println(count(n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the count of n-digit
# natural hexadecimal numbers
def count(n) :

    return 15 * pow(16, n - 1);

# Driver code
if __name__ == "__main__" :

    n = 2;
    print(count(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of n-digit
    // natural hexadecimal numbers
    static int count(int n)
    {
        return (int) (15 * Math.Pow(16, n - 1));
    }

    // Driver code
    public static void Main(String []args)
    {
        int n = 2;
        Console.WriteLine(count(n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to return the count of n-digit
// natural hexadecimal numbers
function count(n)
{
    return 15 * Math.pow(16, n - 1);
}

// Driver code
var n = 2;
document.write(count(n));

</script>
```

**Output:** 

```
240
```

**时间复杂度:** O(1)
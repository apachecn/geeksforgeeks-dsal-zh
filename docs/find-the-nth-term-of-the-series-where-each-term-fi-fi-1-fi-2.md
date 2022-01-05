# 求数列的第 n 项，其中每个项 f[I]= f[I–1]–f[I–2]

> 原文:[https://www . geesforgeks . org/find-the-n-term-of-series-where-每个 term-fi-fi-1-fi-2/](https://www.geeksforgeeks.org/find-the-nth-term-of-the-series-where-each-term-fi-fi-1-fi-2/)

给定三个整数 **X** 、 **Y** 和 **N** ，任务是找到系列**f[I]= f[I–1]–f[I–2]**、 **i > 1** 的 **N <sup>第</sup>** 项，其中 **f[0] = X** 和 **f[1] = Y** 。
**例:**

> **输入:** X = 2，Y = 3，N = 3
> **输出:** -2
> 该系列将为 2 3 1 -2 -3 -1 2 和 f[3] = -2
> **输入:** X = 3，Y = 7，N = 8
> **输出:** 4

**方法:**这里的一个重要观察是，在序列开始自我重复之前，会有 6 个不同的术语。因此，找到该系列的前 6 个术语，然后第 **N <sup>第</sup>T5】术语将与第 **(N % 6) <sup>第</sup>T9】术语相同。
以下是上述方法的实施:**** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the Nth term
// of the given series
int findNthTerm(int x, int y, int n)
{
    int f[6];

    // First and second term of the series
    f[0] = x;
    f[1] = y;

    // Find first 6 terms
    for (int i = 2; i <= 5; i++)
        f[i] = f[i - 1] - f[i - 2];

    // Return the Nth term
    return f[n % 6];
}

// Driver code
int main()
{
    int x = 2, y = 3, n = 3;
    cout << findNthTerm(x, y, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

    // Function to find the nth term of series
    static int findNthTerm(int x, int y, int n)
    {    
        int[] f = new int[6];

        f[0] = x;
        f[1] = y;

        // Loop to add numbers
        for (int i = 2; i <= 5; i++)
            f[i] = f[i - 1] - f[i - 2];

        return f[n % 6];
    }

    // Driver code
    public static void main(String args[])
    {
        int x = 2, y = 3, n = 3;
        System.out.println(findNthTerm(x, y, n));
    }
}

// This code is contributed by mohit kumar 29
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the Nth term
# of the given series
def findNthTerm(x, y, n):

    f = [0] * 6

    # First and second term of
    # the series
    f[0] = x
    f[1] = y

    # Find first 6 terms
    for i in range(2, 6):
        f[i] = f[i - 1] - f[i - 2]

    # Return the Nth term
    return f[n % 6]

# Driver code
if __name__ == "__main__":

    x, y, n = 2, 3, 3
    print(findNthTerm(x, y, n))

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find the nth term of series
    static int findNthTerm(int x, int y, int n)
    {
        int[] f = new int[6];

        f[0] = x;
        f[1] = y;

        // Loop to add numbers
        for (int i = 2; i <= 5; i++)
            f[i] = f[i - 1] - f[i - 2];

        return f[n % 6];
    }

    // Driver code
    public static void Main()
    {
        int x = 2, y = 3, n = 3;
        Console.WriteLine(findNthTerm(x, y, n));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

//PHP implementation of the approach
// Function to find the nth term of series
function findNthTerm($x, $y, $n)
{
    $f = array(6);

    $f[0] = $x;
    $f[1] = $y;

    // Loop to add numbers
    for ($i = 2; $i <= 5; $i++)
        $f[$i] = $f[$i - 1] - $f[$i - 2];

    return $f[$n % 6];
}

// Driver code
$x = 2; $y = 3; $n = 3;
echo(findNthTerm($x, $y, $n));

// This code is contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to return the Nth term
    // of the given series
    function findNthTerm(x, y, n)
    {
        let f = new Array(6);

        // First and second term of the series
        f[0] = x;
        f[1] = y;

        // Find first 6 terms
        for (let i = 2; i <= 5; i++)
            f[i] = f[i - 1] - f[i - 2];

        // Return the Nth term
        return f[n % 6];
    }

    // Driver code

    let x = 2, y = 3, n = 3;
    document.write(findNthTerm(x, y, n));

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
-2
```

**时间复杂度:** O(1)
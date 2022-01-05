# n = x+n⊕x 的解的数量

> 原文:[https://www . geesforgeks . org/n-x-n-x 的解决方案数量/](https://www.geeksforgeeks.org/number-of-solutions-of-n-x-n-x/)

给定一个数 n，我们必须找到 x 的可能值的个数，使得 n = x + n ⊕ x。这里⊕表示 XOR

**例:**

```
Input : n = 3
Output : 4
The possible values of x are 0, 1, 2, and 3.

Input : n = 2
Output : 2
The possible values of x are 0 and 2.
```

**蛮力逼近**:我们可以看到 x 总是等于或小于 n，所以我们可以在[0，n]的范围内迭代，统计满足要求条件的值的个数。这种方法的时间复杂度是 O(n)。

## c++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// solutions of n = n xor x
int numberOfSolutions(int n)
{
    // Counter to store the number
    // of solutions found
    int c = 0;

    for (int x = 0; x <= n; ++x)
        if (n == x + n ^ x)
            ++c;

    return c;
}

// Driver code
int main()
{
    int n = 3;
    cout << numberOfSolutions(n);
    return 0;
}
```

## Java

```
// Java implementation of above approach
import java.util.*;
import java.lang.*;

class GFG
{
// Function to find the number of
// solutions of n = n xor x
static int numberOfSolutions(int n)
{
    // Counter to store the number
    // of solutions found
    int c = 0;

    for (int x = 0; x <= n; ++x)
        if (n == x + (n ^ x))
            ++c;

    return c;
}

// Driver code
public static void main(String args[])
{
    int n = 3;
    System.out.print(numberOfSolutions(n));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## python 3

```
# Python 3 implementation
# of above approach

# Function to find the number of
# solutions of n = n xor x
def numberOfSolutions(n):

    # Counter to store the number
    # of solutions found
    c = 0

    for x in range(n + 1):
        if (n ==( x +( n ^ x))):
            c += 1

    return c

# Driver code
if __name__ == "__main__":
    n = 3
    print(numberOfSolutions(n))

# This code is contributed
# by ChitraNayal
```

## c#

```
// C# implementation of above approach
using System;

class GFG
{
// Function to find the number of
// solutions of n = n xor x
static int numberOfSolutions(int n)
{
    // Counter to store the number
    // of solutions found
    int c = 0;

    for (int x = 0; x <= n; ++x)
        if (n == x + (n ^ x))
            ++c;

    return c;
}

// Driver code
public static void Main()
{
    int n = 3;
    Console.Write(numberOfSolutions(n));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## PHP

```
<?php
// PHP implementation of above approach

// Function to find the number of
// solutions of n = n xor x
function numberOfSolutions($n)
{
    // Counter to store the number
    // of solutions found
    $c = 0;

    for ($x = 0; $x <= $n; ++$x)
        if ($n == $x + $n ^ $x)
            ++$c;

    return $c;
}

// Driver code
$n = 3;
echo numberOfSolutions($n);

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## Javascript

```
<script>

    // Javascript implementation of above approach

    // Function to find the number of
    // solutions of n = n xor x
    function numberOfSolutions(n)
    {

        // Counter to store the number
        // of solutions found
        let c = 0;

        for(let x = 0; x <= n; ++x)
            if (n == x + n ^ x)
                ++c;

        return c;
    }

    let n = 3;
    document.write(numberOfSolutions(n));

    // This code is contributed by divyesh072019.
</script>
```

**输出:**

```
4
```
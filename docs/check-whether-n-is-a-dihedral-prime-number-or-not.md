# 检查 N 是否为二面角素数

> 原文:[https://www . geeksforgeeks . org/check-n-是否是二面角质数/](https://www.geeksforgeeks.org/check-whether-n-is-a-dihedral-prime-number-or-not/)

给定一个整数 **N** ，任务是检查 **N** 是否是二面角素数。二面角质数是一个质数，当在七段显示器中读取时，无论方向和表面如何，它都可以被读取为自身或另一个质数。

**示例:**

> **输入:**N = 108881
> T3】输出:是
> 
> **输入:**N = 789
> T3】输出:否

**方法:**预先计算素数筛，用于素数测试。厄拉多塞的筛可以用 n*logn*logn 时间来计算。对数字及其不同方向进行素性测试。如果数字通过了素性测试，检查是否有任何数字属于排除集[3，4，6，7，9]。如果数字通过了这两个测试，则返回真。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

bool isPrime[int(1e5) + 5];

// Function to return the reverse
// of a number
int reverse(int n)
{
    int temp = n;
    int sum = 0;
    while (temp > 0) {
        int rem = temp % 10;
        sum = sum * 10 + rem;
        temp /= 10;
    }
    return sum;
}

// Function to generate mirror reflection
// of a number
int mirror(int n)
{
    int temp = n;
    int sum = 0;
    while (temp > 0) {
        int rem = temp % 10;
        if (rem == 2)
            rem = 5;
        else if (rem == 5)
            rem = 2;
        sum = sum * 10 + rem;
        temp /= 10;
    }
    return sum;
}

// Function to initialize prime number sieve
bool sieve()
{
    memset(isPrime, true, sizeof isPrime);

    isPrime[0] = isPrime[1] = false;

    for (int i = 2; i <= int(1e5); i++) {
        for (int j = 2; i * j <= int(1e5); j++) {
            isPrime[i * j] = false;
        }
    }
}

// Function that returns true if n is
// Dihedral Prime number
bool isDihedralPrime(int n)
{
    // Check if the orientations of n
    // is also prime
    if (!isPrime[n]
        || !isPrime[mirror(n)]
        || !isPrime[reverse(n)]
        || !isPrime[reverse(mirror(n))])
        return false;

    int temp = n;

    while (temp > 0) {
        int rem = temp % 10;
        if (rem == 3 || rem == 4 || rem == 6
            || rem == 7 || rem == 9)
            return false;
        temp /= 10;
    }

    return true;
}

// Driver code
int main()
{
    sieve();

    int n = 18181;
    if (isDihedralPrime(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    static boolean[] isPrime = new boolean[(int) (1e5) + 5];

    // Function to return the reverse
    // of a number
    static int reverse(int n)
    {
        int temp = n;
        int sum = 0;
        while (temp > 0)
        {
            int rem = temp % 10;
            sum = sum * 10 + rem;
            temp /= 10;
        }
        return sum;
    }

    // Function to generate mirror reflection
    // of a number
    static int mirror(int n)
    {
        int temp = n;
        int sum = 0;
        while (temp > 0)
        {
            int rem = temp % 10;
            if (rem == 2)
            {
                rem = 5;
            }

            else if (rem == 5)
            {
                rem = 2;
            }
            sum = sum * 10 + rem;
            temp /= 10;
        }
        return sum;
    }

    // Function to initialize
    // prime number sieve
    static void sieve()
    {
        Arrays.fill(isPrime, true);

        isPrime[0] = isPrime[1] = false;

        for (int i = 2;
                 i <= (int) 1e5; i++)
        {
            for (int j = 2;
                     i * j <= (int) 1e5; j++)
            {
                isPrime[i * j] = false;
            }
        }
    }

    // Function that returns true if n is
    // Dihedral Prime number
    static boolean isDihedralPrime(int n)
    {

        // Check if the orientations of n
        // is also prime
        if (!isPrime[n] ||
            !isPrime[mirror(n)] ||
            !isPrime[reverse(n)] ||
            !isPrime[reverse(mirror(n))])
        {
            return false;
        }

        int temp = n;

        while (temp > 0)
        {
            int rem = temp % 10;
            if (rem == 3 || rem == 4 ||
                rem == 6 || rem == 7 ||
                rem == 9)
            {
                return false;
            }
            temp /= 10;
        }

        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        sieve();

        int n = 18181;
        if (isDihedralPrime(n))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of the above approach
isPrime = (int(1e5)+5)*[True]

# Function to return the reverse
# of a number
def reverse(n):
    temp = n
    sum = 0
    while temp>0:
        rem = temp % 10
        sum = sum * 10 + rem
        temp//= 10

    return sum

# Function to generate mirror reflection
# of a number
def mirror(n):
    temp = n
    sum = 0
    while temp>0:
        rem = temp % 10
        if rem == 2:
            rem = 5
        elif rem == 5:
            rem = 2
        sum = sum * 10 + rem
        temp//= 10

    return sum

# Function to initialize prime number sieve
def sieve():

    isPrime[0] = isPrime[1] = False

    for i in range(2, int(1e5)+1):
        j = 2
        while i * j<= int(1e5):
            isPrime[i * j] = False
            j+= 1

# Function that returns true if n is
# Dihedral Prime number
def isDihedralPrime(n):

    # Check if the orientations of n is also prime
    if (not isPrime[n]) or (not isPrime[mirror(n)]) \
        or (not isPrime[reverse(n)]) \
        or (not isPrime[reverse(mirror(n))]):
        return False

    temp = n

    while temp>0:
        rem = temp % 10;
        if rem == 3 or rem == 4 or \
            rem == 6 or rem == 7 or rem == 9:
            return False
        temp//= 10

    return True

# Driver code
if __name__ == '__main__':

    sieve()

    n = 18181
    if isDihedralPrime(n):
        print("Yes")
    else :
        print("No")
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static Boolean[] isPrime = new Boolean[(int) (1e5) + 5];

    // Function to return the reverse
    // of a number
    static int reverse(int n)
    {
        int temp = n;
        int sum = 0;
        while (temp > 0)
        {
            int rem = temp % 10;
            sum = sum * 10 + rem;
            temp /= 10;
        }
        return sum;
    }

    // Function to generate mirror reflection
    // of a number
    static int mirror(int n)
    {
        int temp = n;
        int sum = 0;
        while (temp > 0)
        {
            int rem = temp % 10;
            if (rem == 2)
            {
                rem = 5;
            }

            else if (rem == 5)
            {
                rem = 2;
            }
            sum = sum * 10 + rem;
            temp /= 10;
        }
        return sum;
    }

    // Function to initialize
    // prime number sieve
    static void sieve()
    {
        for(int k = 0; k < isPrime.Length; k++)
            isPrime[k] = true;

        isPrime[0] = isPrime[1] = false;

        for (int i = 2;
                 i <= (int) 1e5; i++)
        {
            for (int j = 2;
                     i * j <= (int) 1e5; j++)
            {
                isPrime[i * j] = false;
            }
        }
    }

    // Function that returns true if n is
    // Dihedral Prime number
    static Boolean isDihedralPrime(int n)
    {

        // Check if the orientations of n
        // is also prime
        if (!isPrime[n] ||
            !isPrime[mirror(n)] ||
            !isPrime[reverse(n)] ||
            !isPrime[reverse(mirror(n))])
        {
            return false;
        }

        int temp = n;

        while (temp > 0)
        {
            int rem = temp % 10;
            if (rem == 3 || rem == 4 ||
                rem == 6 || rem == 7 ||
                rem == 9)
            {
                return false;
            }
            temp /= 10;
        }

        return true;
    }

    // Driver code
    public static void Main(String[] args)
    {
        sieve();

        int n = 18181;
        if (isDihedralPrime(n))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
$isPrime = array_fill(0, 25000 , true);

// Function to return the reverse
// of a number
function reverse($n)
{
    $temp = $n;
    $sum = 0;
    while ($temp > 0)
    {
        $rem = $temp % 10;
        $sum = $sum * 10 + $rem;
        $temp = floor($temp / 10);
    }
    return $sum;
}

// Function to generate mirror reflection
// of a number
function mirror($n)
{
    $temp = $n;
    $sum = 0;
    while ($temp > 0)
    {
        $rem = $temp % 10;
        if ($rem == 2)
            $rem = 5;
        else if ($rem == 5)
            $rem = 2;
        $sum = $sum * 10 + $rem;
        $temp = floor($temp / 10);
    }
    return $sum;
}

// Function to initialize prime number sieve
function sieve()
{
    $GLOBALS['isPrime'][0] = $GLOBALS['isPrime'][1] = false;

    for ($i = 2; $i <= floor(1e4); $i++)
    {
        for ($j = 2; $i * $j <= floor(1e4); $j++)
        {
            $GLOBALS['isPrime'][$i * $j] = false;
        }
    }
}

// Function that returns true if n is
// Dihedral Prime number
function isDihedralPrime($n)
{
    // Check if the orientations of n
    // is also prime
    if (!$GLOBALS['isPrime'][$n] ||
        !$GLOBALS['isPrime'][mirror($n)] ||
        !$GLOBALS['isPrime'][reverse($n)] ||
        !$GLOBALS['isPrime'][reverse(mirror($n))])
        return false;

    $temp = $n;

    while ($temp > 0)
    {
        $rem = $temp % 10;
        if ($rem == 3 || $rem == 4 ||
            $rem == 6 || $rem == 7 || $rem == 9)
            return false;

        $temp = floor($temp / 10);
    }

    return true;
}

// Driver code
sieve();

$n = 18181;
if (isDihedralPrime($n))
    echo "Yes";
else
    echo "No";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach
let isPrime = new Array(25000).fill(true);

// Function to return the reverse
// of a number
function reverse(n)
{
    let temp = n;
    let sum = 0;
    while (temp > 0)
    {
        rem = temp % 10;
        sum = sum * 10 + rem;
        temp = Math.floor(temp / 10);
    }
    return sum;
}

// Function to generate mirror reflection
// of a number
function mirror(n)
{
    let temp = n;
    let sum = 0;
    while (temp > 0)
    {
        let rem = temp % 10;
        if (rem == 2)
            rem = 5;
        else if (rem == 5)
            rem = 2;
        sum = sum * 10 + rem;
        temp = Math.floor(temp / 10);
    }
    return sum;
}

// Function to initialize prime number sieve
function sieve()
{
    isPrime[0] = isPrime[1] = false;

    for (let i = 2; i <= Math.floor(1e4); i++)
    {
        for (let j = 2; i * j <= Math.floor(1e4); j++)
        {
            isPrime[i * j] = false;
        }
    }
}

// Function that returns true if n is
// Dihedral Prime number
function isDihedralPrime(n)
{
    // Check if the orientations of n
    // is also prime
    if (!isPrime[n] ||
        !isPrime[mirror(n)] ||
        !isPrime[reverse(n)] ||
        !isPrime[reverse(mirror(n))])
        return false;

    let temp = n;

    while (temp > 0)
    {
        rem = temp % 10;
        if (rem == 3 || rem == 4 ||
            rem == 6 || rem == 7 || rem == 9)
            return false;

        temp = Math.floor(temp / 10);
    }

    return true;
}

// Driver code
sieve();

let n = 18181;
if (isDihedralPrime(n))
    document.write( "Yes");
else
    document.write( "No");

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(n * log(log n))*

***辅助空间:** O(10 <sup>5</sup> )*
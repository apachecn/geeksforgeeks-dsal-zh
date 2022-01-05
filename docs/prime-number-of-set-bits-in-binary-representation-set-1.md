# 二进制表示中集合位的素数|集合 1

> 原文:[https://www . geesforgeks . org/prime-二进制表示的位数集-1/](https://www.geeksforgeeks.org/prime-number-of-set-bits-in-binary-representation-set-1/)

给定两个整数“L”和“R”，编写一个程序，找出在[L，R]范围内二进制表示中具有素数的集合位的总数。

**示例:**

```
Input  : l = 6, r = 10
Output : 4
Explanation  :
6  -> 110  (2 set bits, 2 is prime)
7  -> 111  (3 set bits, 3 is prime)
9  -> 1001 (2 set bits, 2 is prime)
10 -> 1010 (2 set bits, 2 is prime)
Hence count is 4

Input  : l = 10, r = 15
Output : 5
10 -> 1010 (2 set bits, 2 is prime)
11 -> 1011 (3 set bits, 3 is prime)
12 -> 1100 (2 set bits, 2 is prime)
13 -> 1101 (3 set bits, 3 is prime)
14 -> 1110 (3 set bits, 3 is prime)
Hence count is 5
```

**说明:**在这个程序中我们找到一个总数，就是有素数的集合位。所以我们使用一个 CPP 预定义函数[**_ _ builtin _ popcount()**](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)这些函数提供了一个总的设置位数。除了检查总比特是否是素数，如果是素数，我们增加计数器，这些过程重复直到给定的范围。

## C++

```
// C++ program to count total prime
// number of set bits in given range
#include <bits/stdc++.h>
using namespace std;

bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)  return false;
    if (n <= 3)  return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n%2 == 0 || n%3 == 0) return false;

    for (int i=5; i*i<=n; i=i+6)
        if (n%i == 0 || n%(i+2) == 0)
           return false;

    return true;
}

// count number, that contains prime number of set bit
int primeBitsInRange(int l, int r)
{
    // tot_bit store number of bit in number
    int tot_bit, count = 0;

    // iterate loop from l to r
    for (int i = l; i <= r; i++) {

        // use predefined function for finding
        // set bit it is return number of set bit
        tot_bit = __builtin_popcount(i);

        // check tot_bit prime or, not
        if (isPrime(tot_bit))
            count++;
    }
    return count;
}

// Driven Program
int main()
{
    int l = 6, r = 10;   
    cout << primeBitsInRange(l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count total prime
// number of set bits in given range
import java.lang.*;

class GFG{
static boolean isPrime(int n)
{
    // Corner cases
    if (n <= 1) return false;
    if (n <= 3) return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n%2 == 0 || n%3 == 0) return false;

    for (int i=5; i*i<=n; i=i+6)
        if (n%i == 0 || n%(i+2) == 0)
        return false;

    return true;
}

// count number, that contains prime number of set bit
static int primeBitsInRange(int l, int r)
{
    // tot_bit store number of bit in number
    int tot_bit, count = 0;

    // iterate loop from l to r
    for (int i = l; i <= r; i++) {

        // use predefined function for finding
        // set bit it is return number of set bit
        tot_bit = Integer.bitCount(i);

        // check tot_bit prime or, not
        if (isPrime(tot_bit))
            count++;
    }
    return count;
}

// Driven Program
public static void main(String[] args)
{
    int l = 6, r = 10;
    System.out.println(primeBitsInRange(l, r));

}
}
// This code is Contributed by mits
```

## 蟒蛇 3

```
# Python3 program to count total prime
# number of set bits in given range
def isPrime(n):

    # Corner cases
    if (n <= 1): return False;
    if (n <= 3): return True;

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False;

    i = 5;
    while (i * i <= n):
        if(n % i == 0 or n % (i + 2) == 0):
            return False;
        i = i + 6;

    return True;

# count number, that contains
# prime number of set bit
def primeBitsInRange(l, r):

    # tot_bit store number of
    # bit in number
    count = 0;

    # iterate loop from l to r
    for i in range(l, r + 1):

        # use predefined function for finding
        # set bit it is return number of set bit
        tot_bit = bin(i).count('1');

        # check tot_bit prime or, not
        if (isPrime(tot_bit)):
            count += 1;

    return count;

# Driver Code
l = 6;
r = 10;
print(primeBitsInRange(l, r));

# This code is contributed by mits
```

## C#

```
// C# program to count total prime
// number of set bits in given range

class GFG{

    // To count the bits
static int BitCount(int n)
{
    int count = 0;
    while (n != 0)
    {
        count++;
        n &= (n - 1);
    }

    return count;
}

static bool isPrime(int n)
{
    // Corner cases
    if (n <= 1) return false;
    if (n <= 3) return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n%2 == 0 || n%3 == 0) return false;

    for (int i=5; i*i<=n; i=i+6)
        if (n%i == 0 || n%(i+2) == 0)
        return false;

    return true;
}

// count number, that contains prime number of set bit
static int primeBitsInRange(int l, int r)
{
    // tot_bit store number of bit in number
    int tot_bit, count = 0;

    // iterate loop from l to r
    for (int i = l; i <= r; i++) {

        // use predefined function for finding
        // set bit it is return number of set bit
        tot_bit = BitCount(i);

        // check tot_bit prime or, not
        if (isPrime(tot_bit))
            count++;
    }
    return count;
}

// Driven Program
public static void Main()
{
    int l = 6, r = 10;
    System.Console.WriteLine(primeBitsInRange(l, r));

}
}
// This code is Contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count total prime
// number of set bits in given range
function BitCount($n)
{
    $count = 0;
    while ($n != 0)
    {
        $count++;
        $n &= ($n - 1);
    }

    return $count;
}

function isPrime($n)
{
    // Corner cases
    if ($n <= 1) return false;
    if ($n <= 3) return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if ($n % 2 == 0 || $n % 3 == 0)
        return false;

    for ($i = 5; $i * $i <= $n; $i = $i + 6)
        if ($n % $i == 0 ||
            $n % ($i + 2) == 0)
        return false;

    return true;
}

// count number, that contains
// prime number of set bit
function primeBitsInRange($l, $r)
{
    // tot_bit store number of
    // bit in number
    $count = 0;

    // iterate loop from l to r
    for ($i = $l; $i <= $r; $i++)
    {

        // use predefined function for finding
        // set bit it is return number of set bit
        $tot_bit = BitCount($i);

        // check tot_bit prime or, not
        if (isPrime($tot_bit))
            $count++;
    }
    return $count;
}

// Driver Code
$l = 6;
$r = 10;
echo primeBitsInRange($l, $r);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to count total prime
// number of set bits in given range

// To count the bits
function BitCount(n)
{
    count = 0;
    while (n != 0)
    {
        count++;
        n &= (n - 1);
    }

    return count;
}

function isPrime(n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Count number, that contains
// prime number of set bit
function primeBitsInRange(l, r)
{

    // tot_bit store number of bit in number
    var tot_bit, count = 0;

    // Iterate loop from l to r
    for(i = l; i <= r; i++)
    {

        // Use predefined function for finding
        // set bit it is return number of set bit
        tot_bit = BitCount(i);

        // Check tot_bit prime or, not
        if (isPrime(tot_bit))
            count++;
    }
    return count;
}

// Driver code
var l = 6, r = 10;

document.write(primeBitsInRange(l, r));

// This code is contributed by Rajput-Ji

</script>
```

**Output:** 

```
4
```

**时间复杂度:**假设 n = (r-l)
那么整体时间复杂度为 N*sqrt(N)
我们可以使用厄拉多塞的[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)来优化上面的解。
[**二进制表示中集合位的素数|集合 2**](https://www.geeksforgeeks.org/prime-number-of-set-bits-in-binary-representation-set-2/)
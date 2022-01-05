# 当一个数的第一个数字除以它的最后一个数字时求余数

> 原文:[https://www . geeksforgeeks . org/当数字的第一个数字除以其最后一个数字时查找余数/](https://www.geeksforgeeks.org/find-the-remainder-when-first-digit-of-a-number-is-divided-by-its-last-digit/)

给定一个数字 N，当 N 的第一个数字除以它的最后一个数字时，求余数。
**例:**

```
Input: N = 1234
Output: 1
First digit = 1
Last digit = 4
Remainder = 1 % 4 = 1

Input: N = 5223
Output: 2
First digit = 5
Last digit = 3
Remainder = 5 % 3 = 2
```

**逼近:**求数字的第一位和最后一位。当第一个数字除以最后一个数字时，求余数。
以下是上述办法的实施情况:

## C++

```
// C++ program to find the remainder
// when the First digit of a number
// is divided by its Last digit

#include <bits/stdc++.h>
using namespace std;

// Function to find the remainder
void findRemainder(int n)
{
    // Get the last digit
    int l = n % 10;

    // Get the first digit
    while (n >= 10)
        n /= 10;
    int f = n;

    // Compute the remainder
    int remainder = f % l;

    cout << remainder << endl;
}

// Driver code
int main()
{

    int n = 5223;

    findRemainder(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the remainder
// when the First digit of a number
// is divided by its Last digit
class GFG
{

// Function to find the remainder
static void findRemainder(int n)
{
    // Get the last digit
    int l = n % 10;

    // Get the first digit
    while (n >= 10)
        n /= 10;
    int f = n;

    // Compute the remainder
    int remainder = f % l;

    System.out.println(remainder);
}

// Driver code
public static void main(String[] args)
{
    int n = 5223;
    findRemainder(n);
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 program to find the remainder
# when the First digit of a number
# is divided by its Last digit

# Function to find the remainder
def findRemainder(n):

    # Get the last digit
    l = n % 10

    # Get the first digit
    while (n >= 10):
        n //= 10
    f = n

    # Compute the remainder
    remainder = f % l

    print(remainder)

# Driver code
n = 5223

findRemainder(n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find the remainder
// when the First digit of a number
// is divided by its Last digit
using System;

class GFG
{

// Function to find the remainder
static void findRemainder(int n)
{
    // Get the last digit
    int l = n % 10;

    // Get the first digit
    while (n >= 10)
        n /= 10;
    int f = n;

    // Compute the remainder
    int remainder = f % l;

    Console.WriteLine(remainder);
}

// Driver code
public static void Main()
{
    int n = 5223;
    findRemainder(n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

 // Javascript  program to find the remainder
// when the First digit of a number
// is divided by its Last digit

// Function to find the remainder
function findRemainder( n)
{
    // Get the last digit
    let  l = n % 10;

    // Get the first digit
    while (n >= 10)
        n /= 10;
    let f = n;
    // Compute the remainder
    let remainder = f % l;

    document.write(Math.floor(remainder));
}

// Driver code
    let n = 5223;
    findRemainder(n);

// This code is contributed by mohan pavan

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(L)，其中 L 是十进制表示的数字长度

**辅助空间:** O(1)
# 最小奇数位数不小于 N

> 原文:[https://www . geesforgeks . org/最小-奇数-数字-不小于-n/](https://www.geeksforgeeks.org/smallest-odd-digits-number-not-less-than-n/)

给定一个数 N，任务是找到不小于 N 的最小数，它的所有数字都是奇数。
**例:**

```
Input: N = 1345  
Output: 1351
1351 is the smallest number not 
less than N, whose all digits are odd. 

Input: N = 2397 
Output: 3111 
3111 is the smallest number not 
less than N, whose all digits are odd.
```

**天真的方法**:天真的方法是从 N 开始不断迭代，直到我们找到一个所有数字都是奇数的数字。
以下是上述办法的实施情况:

## C++

```
// CPP program to print the smallest
// integer not less than N with all odd digits
#include <bits/stdc++.h>
using namespace std;

// function to check if all digits
// are odd of a given number
int check_digits(int n)
{
    // iterate for all digits
    while (n) {
        if ((n % 10) % 2 == 0) // if digit is even
            return 0;

        n /= 10;
    }

    // all digits are odd
    return 1;
}

// function to return the smallest number
// with all digits odd
int smallest_number(int n)
{
    // iterate till we find a
    // number with all digits odd
    for (int i = n;; i++)
        if (check_digits(i))
            return i;
}

// Driver Code
int main()
{
    int N = 2397;
    cout << smallest_number(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the smallest
// integer not less than N with all odd digits
class Geeks {

// function to check if all digits
// are odd of a given number
static int check_digits(int n)
{
    // iterate for all digits
    while (n > 0) {
        if ((n % 10) % 2 == 0) // if digit is even
            return 0;

        n /= 10;
    }

    // all digits are odd
    return 1;
}

// function to return the smallest number
// with all digits odd
static int smallest_number(int n)
{
    // iterate till we find a
    // number with all digits odd
    for (int i = n;; i++)
        if (check_digits(i) > 0)
            return i;
}

// Driver Code
public static void main(String args[])
{
    int N = 2397;
    System.out.println(smallest_number(N));
}
}

// This code is contributed by Kirti_Mangal
```

## 蟒蛇 3

```
# Python 3 program to print the smallest
# integer not less than N with all odd digits

# function to check if all digits
# are odd of a given number
def check_digits(n):

    # iterate for all digits
    while (n):

        # if digit is even
        if ((n % 10) % 2 == 0):
            return 0

        n = int(n / 10)

    # all digits are odd
    return 1

# function to return the smallest
# number with all digits odd
def smallest_number(n):

    # iterate till we find a
    # number with all digits odd
    i = n
    while(1):
        if (check_digits(i)):
            return i

        i += 1

# Driver Code
if __name__ == '__main__':
    N = 2397
    print(smallest_number(N))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to print the smallest
// integer not less than N with all
// odd digits
using System;

class GFG
{
// function to check if all digits
// are odd of a given number
static int check_digits(int n)
{
    // iterate for all digits
    while (n != 0)
    {
        if ((n % 10) % 2 == 0) // if digit is even
            return 0;

        n /= 10;
    }

    // all digits are odd
    return 1;
}

// function to return the smallest
// number with all digits odd
static int smallest_number(int n)
{
    // iterate till we find a
    // number with all digits odd
    for (int i = n;; i++)
        if (check_digits(i) == 1)
            return i;
}

// Driver Code
static void Main()
{
    int N = 2397;
    Console.WriteLine(smallest_number(N));
}
}

// This code is contributed by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the smallest
// integer not less than N with all
// odd digits

// function to check if all digits
// are odd of a given number
function check_digits($n)
{
    // iterate for all digits
    while ($n > 1)
    {
        // if digit is even
        if (($n % 10) % 2 == 0)
            return 0;

        $n = (int)$n / 10;
    }

    // all digits are odd
    return 1;
}

// function to return the smallest
// number with all digits odd
function smallest_number( $n)
{
    // iterate till we find a
    // number with all digits odd
    for ($i = $n;; $i++)
        if (check_digits($i))
            return $i;
}

// Driver Code
$N = 2397;
echo smallest_number($N);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// java script program to print the smallest
// integer not less than N with all
// odd digits

// function to check if all digits
// are odd of a given number
function check_digits(n)
{

    // iterate for all digits
    while (n > 1)
    {

        // if digit is even
        if ((n % 10) % 2 == 0)
            return 0;

         n = parseInt(n / 10);
    }

    // all digits are odd
    return 1;
}

// function to return the smallest
// number with all digits odd
function smallest_number( n)
{

    // iterate till we find a
    // number with all digits odd
    for (i = n;; i++)
        if (check_digits(i))
            return i;
}

// Driver Code
let N = 2397;
document.write( smallest_number(N));

// This code is contributed by sravan kumar (vignan)
</script>
```

**Output:** 

```
3111
```
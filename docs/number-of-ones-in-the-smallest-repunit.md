# 最小重复单位中的 1 的数量

> 原文:[https://www . geeksforgeeks . org/最小重复单位数/](https://www.geeksforgeeks.org/number-of-ones-in-the-smallest-repunit/)

给定一个正整数 N，其单位的数字是 3。找出最小重复单位中可被给定数字 n 整除的 1 的个数。每个单位的位数为 3 的数都有一个重复单位作为它的倍数。repunit 是一个只有一个的数。它的形式是(10n–1)/9。
**例:**

> **输入:**3
> T3】输出: 3
> As 3 除以 111，111 是该数的最小重复单位
> 倍数。所以 111 中的 1 数是 3。
> **输入:** 13
> **输出:** 6

重发单位是 1，11，111，1111，… **x** 的下一个 repunit 将始终为 x*10+1。如果 **x** repunit 剩下的余数是 **r** ，那么下一个 repunit 剩下的余数总是 **(r*10+1)%n.** 由于 repunit 可以很大，所以不需要找 repunit 编号。简单地数一数就会给我们答案。
所以，找出所有 repunit 数的余数，直到余数变为 0。一旦完成，则为使余数为 0 而进行的迭代次数将为 1 的次数。
下面是上述方法的实现:

## C++

```
// CPP program to print the number of 1s in
// smallest repunit multiple of the number.
#include <bits/stdc++.h>
using namespace std;

// Function to find number of 1s in
// smallest repunit multiple of the number
int countOnes(int n)
{
    // to store number of 1s in smallest
    // repunit multiple of the number.
    int count = 1;

    // initialize rem with 1
    int rem = 1;

    // run loop until rem becomes zero
    while (rem != 0) {

        // rem*10 + 1 here represents
        // the repunit modulo n
        rem = (rem * 10 + 1) % n;
        count++;
    }

    // when remainder becomes 0
    // return count
    return count;
}

// Driver Code
int main()
{
    int n = 13;

    // Calling function
    cout << countOnes(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// number of 1s in smallest
// repunit multiple of the number.
import java.io.*;

class GFG
{
// Function to find number
// of 1s in smallest repunit
// multiple of the number
static int countOnes(int n)
{
    // to store number of 1s
    // in smallest repunit
    // multiple of the number.
    int count = 1;

    // initialize rem with 1
    int rem = 1;

    // run loop until
    // rem becomes zero
    while (rem != 0)
    {

        // rem*10 + 1 here
        // represents the
        // repunit modulo n
        rem = (rem * 10 + 1) % n;
        count++;
    }

    // when remainder becomes
    // 0 return count
    return count;
}

// Driver Code
public static void main (String[] args)
{
int n = 13;

// Calling function
System.out.println(countOnes(n));
}
}

// This code is contributed by akt_mit
```

## 蟒蛇 3

```
# Python3 program to print the
# number of 1s in smallest
# repunit multiple of the number.

# Function to find number
# of 1s in smallest repunit
# multiple of the number
def countOnes(n):

    # to store number of 1s
    # in smallest repunit
    # multiple of the number.
    count = 1;

    # initialize rem with 1
    rem = 1;

    # run loop until
    # rem becomes zero
    while (rem != 0):

        # rem*10 + 1 here represents
        # the repunit modulo n
        rem = (rem * 10 + 1) % n;
        count = count + 1;

    # when remainder becomes
    # 0 return count
    return count;

# Driver Code
n = 13;

# Calling function
print(countOnes(n));

# This code is contributed by mits
```

## C#

```
// C# program to print the
// number of 1s in smallest
// repunit multiple of the number.
using System;

class GFG
{

// Function to find number
// of 1s in smallest repunit
// multiple of the number
static int countOnes(int n)
{
    // to store number of 1s
    // in smallest repunit
    // multiple of the number.
    int count = 1;

    // initialize rem with 1
    int rem = 1;

    // run loop until
    // rem becomes zero
    while (rem != 0)
    {

        // rem*10 + 1 here represents
        // the repunit modulo n
        rem = (rem * 10 + 1) % n;
        count++;
    }

    // when remainder becomes 0
    // return count
    return count;
}

// Driver Code
static public void Main ()
{
int n = 13;

// Calling function
Console.WriteLine (countOnes(n));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the
// number of 1s in smallest
// repunit multiple of the number.

// Function to find number
// of 1s in smallest repunit
// multiple of the number
function countOnes($n)
{
    // to store number of 1s
    // in smallest repunit
    // multiple of the number.
    $count = 1;

    // initialize rem with 1
    $rem = 1;

    // run loop until
    // rem becomes zero
    while ($rem != 0)
    {

        // rem*10 + 1 here represents
        // the repunit modulo n
        $rem = ($rem * 10 + 1) % $n;
        $count++;
    }

    // when remainder becomes
    // 0 return count
    return $count;
}

// Driver Code
$n = 13;

// Calling function
echo countOnes($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to print the
    // number of 1s in smallest
    // repunit multiple of the number.

    // Function to find number
    // of 1s in smallest repunit
    // multiple of the number
    function countOnes(n)
    {
        // to store number of 1s
        // in smallest repunit
        // multiple of the number.
        let count = 1;

        // initialize rem with 1
        let rem = 1;

        // run loop until
        // rem becomes zero
        while (rem != 0)
        {

            // rem*10 + 1 here represents
            // the repunit modulo n
            rem = (rem * 10 + 1) % n;
            count++;
        }

        // when remainder becomes 0
        // return count
        return count;
    }

    let n = 13;

    // Calling function
    document.write(countOnes(n));

  // This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
6
```
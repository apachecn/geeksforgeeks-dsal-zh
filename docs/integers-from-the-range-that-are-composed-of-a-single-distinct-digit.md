# 由单个不同数字组成的范围内的整数

> 原文:[https://www . geesforgeks . org/由单个不同数字组成的范围内的整数/](https://www.geeksforgeeks.org/integers-from-the-range-that-are-composed-of-a-single-distinct-digit/)

给定两个整数 **L** 和 **R** 代表一个范围**【L，R】**，任务是从由单个不同数字组成的范围中找到整数的计数。
**举例:**

```
Input : L = 9, R = 11
Output : 2
Only 9 and 11 have single distinct digit

Input : L = 10, R = 50
Output : 4
11, 22, 33 and 44 are the only valid numbers
```

**天真方法:**遍历所有数字，检查该数字是否仅由一个不同的数字组成。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Boolean function to check
// distinct digits of a number
bool checkDistinct(int x)
{
    // Take last digit
    int last = x % 10;

    // Check if all other digits
    // are same as last digit
    while (x) {
        if (x % 10 != last)
            return false;

        // Remove last digit
        x = x / 10;
    }

    return true;
}

// Function to return the count of integers that
// are composed of a single distinct digit only
int findCount(int L, int R)
{
    int count = 0;

    for (int i = L; i <= R; i++) {

        // If i has single distinct digit
        if (checkDistinct(i))
            count += 1;
    }

    return count;
}

// Driver code
int main()
{
    int L = 10, R = 50;

    cout << findCount(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach

import java.io.*;

class GFG {

// Boolean function to check
// distinct digits of a number
static boolean checkDistinct(int x)
{
    // Take last digit
    int last = x % 10;

    // Check if all other digits
    // are same as last digit
    while (x >0) {
        if (x % 10 != last)
            return false;

        // Remove last digit
        x = x / 10;
    }

    return true;
}

// Function to return the count of integers that
// are composed of a single distinct digit only
static int findCount(int L, int R)
{
    int count = 0;

    for (int i = L; i <= R; i++) {

        // If i has single distinct digit
        if (checkDistinct(i))
            count += 1;
    }

    return count;
}

// Driver code
    public static void main (String[] args) {

        int L = 10, R = 50;
        System.out.println (findCount(L, R));
    }
//This code is contributed by ajit.   
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Boolean function to check
# distinct digits of a number
def checkDistinct(x):

    # Take last digit
    last = x % 10

    # Check if all other digits
    # are same as last digit
    while (x):

        if (x % 10 != last):
            return False

        # Remove last digit
        x = x // 10

    return True

# Function to return the count of
# integers that are composed of a
# single distinct digit only
def findCount(L, R):

    count = 0

    for i in range(L, R + 1):

        # If i has single distinct digit
        if (checkDistinct(i)):
            count += 1

    return count

# Driver code
L = 10
R = 50

print(findCount(L, R))

# This code is contributed
# by saurabh_shukla
```

## C#

```
// C# implementation of the approach
 using System;

class GFG {

// Boolean function to check
// distinct digits of a number
static Boolean checkDistinct(int x)
{
    // Take last digit
    int last = x % 10;

    // Check if all other digits
    // are same as last digit
    while (x >0) {
        if (x % 10 != last)
            return false;

        // Remove last digit
        x = x / 10;
    }

    return true;
}

// Function to return the count of integers that
// are composed of a single distinct digit only
static int findCount(int L, int R)
{
    int count = 0;

    for (int i = L; i <= R; i++) {

        // If i has single distinct digit
        if (checkDistinct(i))
            count += 1;
    }

    return count;
}

// Driver code
    static public void Main (String []args) {

        int L = 10, R = 50;
        Console.WriteLine (findCount(L, R));
    }   
}
//This code is contributed by Arnab Kundu.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Boolean function to check distinct
// digits of a number
function checkDistinct($x)
{
    // Take last digit
    $last = $x % 10;

    // Check if all other digits
    // are same as last digit
    while ($x)
    {
        if ($x % 10 != $last)
            return false;

        // Remove last digit
        $x = floor($x / 10);
    }

    return true;
}

// Function to return the count of integers that
// are composed of a single distinct digit only
function findCount($L, $R)
{
    $count = 0;

    for ($i = $L; $i <= $R; $i++)
    {

        // If i has single distinct digit
        if (checkDistinct($i))
            $count += 1;
    }

    return $count;
}

// Driver code
$L = 10;
$R = 50;

echo findCount($L, $R);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
//javascript implementation of the approach   
// Boolean function to check
    // distinct digits of a number
    function checkDistinct(x) {
        // Take last digit
        var last = x % 10;

        // Check if all other digits
        // are same as last digit
        while (x > 0) {
            if (x % 10 != last)
                return false;

            // Remove last digit
            x = parseInt(x / 10);
        }

        return true;
    }

    // Function to return the count of integers that
    // are composed of a single distinct digit only
    function findCount(L , R) {
        var count = 0;

        for (i = L; i <= R; i++) {

            // If i has single distinct digit
            if (checkDistinct(i))
                count += 1;
        }

        return count;
    }

    // Driver code

        var L = 10, R = 50;
        document.write(findCount(L, R));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
4
```
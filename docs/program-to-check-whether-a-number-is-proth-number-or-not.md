# 检查一个号码是否是原号码的程序

> 原文:[https://www . geesforgeks . org/program-to-check-a-number-is-Prost-number-or-not/](https://www.geeksforgeeks.org/program-to-check-whether-a-number-is-proth-number-or-not/)

给定一个正整数 N，任务是检查它是否是一个 Proth 数。如果给定的号码是原号码，则打印“是”，否则打印“否”。

[**普罗瑟数**](https://en.wikipedia.org/wiki/Proth_number) **:** 在数学中，普罗瑟数是一个正整数的形式

> **n = k * 2 <sup>n</sup> + 1**

其中 *k* 是奇数正整数， *n* 是正整数，使得*2<sup>n</sup>T8】k*。

前几个号码是–

> 3, 5, 9, 13, 17, 25, 33, 41, 49, ……

**示例:**

```
Input: 25
Output: YES
    Taking k= 3 and n= 3, 
    25 can be expressed in the form of 
    (k.2n + 1) as (3.23 + 1) 

Input: 73
Output: NO
    Taking k=9 and n=3
    73 can be expressed in the form of
    (k.2n + 1 ) as  (9.23 + 1)
    But 23 is less than 9 
    (it should be greater than k to be Proth Number) 
```

**接近**

1.  从数字中扣除 1。这将给出一个形式为 *k*2 <sup>n</sup>* 的数字，如果给定的数字是一个原数字。
2.  现在，循环遍历所有从 k=1 到 n/k 的奇数，检查 k 是否能以(n/k)是 2 的幂的方式除 n。
3.  如果找到，打印“是”
4.  如果没有找到这样的 k 值，则打印“否”

以下是上述想法的实现

## C++

```
// CPP program to check Proth number

#include <bits/stdc++.h>
using namespace std;

// Utility function to check power of two
bool isPowerOfTwo(int n)
{
    return (n && !(n & (n - 1)));
}

// Function to check if the
// Given number is Proth number or not
bool isProthNumber(int n)
{

    int k = 1;
    while (k < (n / k)) {

        // check if k divides n or not
        if (n % k == 0) {

            // Check if n/k is power of 2 or not
            if (isPowerOfTwo(n / k))
                return true;
        }

        // update k to next odd number
        k = k + 2;
    }

    // If we reach here means
    // there exists no value of K
    // Such that k is odd number
    // and n/k is a power of 2 greater than k
    return false;
}

// Driver code
int main()
{

    // Get n
    int n = 25;

    // Check n for Proth Number
    if (isProthNumber(n - 1))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check for Proth number

class GFG {

    // Utility function to check power of two
    static boolean isPowerOfTwo(int n)
    {
        return n != 0 && ((n & (n - 1)) == 0);
    }

    // Function to check if the
    // Given number is Proth number or not
    static boolean isProthNumber(int n)
    {

        int k = 1;
        while (k < (n / k)) {

            // check if k divides n or not
            if (n % k == 0) {

                // Check if n/k is power of 2 or not
                if (isPowerOfTwo(n / k))
                    return true;
            }

            // update k to next odd number
            k = k + 2;
        }

        // If we reach here means
        // there exists no value of K
        // Such that k is odd number
        // and n/k is a power of 2 greater than k
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Get n
        int n = 25;

        // Check n for Proth Number
        if (isProthNumber(n - 1))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Python3 program to check for Proth number

# Utility function to Check
# power of two
def isPowerOfTwo(n):

    return (n and (not(n & (n - 1)))) 

# Function to check if the
# Given number is Proth number or not
def isProthNumber( n):

    k = 1

    while(k < (n//k)):

        # check if k divides n or not
        if(n % k == 0):

            # Check if n / k is power of 2 or not
            if(isPowerOfTwo(n//k)):
                    return True

        # update k to next odd number
        k = k + 2      

    # If we reach here means
    # there exists no value of K
    # Such that k is odd number 
    # and n / k is a power of 2 greater than k
    return False

# Driver code

# Get n
    int n = 25;

# Check n for Proth Number
if(isProthNumber(n-1)):
    print("YES");
else:
    print("NO");
```

## C#

```
// C# program to check Proth number

using System;
class GFG {

    // Utility function to check power of two
    static bool isPowerOfTwo(int n)
    {
        return n != 0 && ((n & (n - 1)) == 0);
    }

    // Function to check if the
    // Given number is Proth number or not
    static bool isProthNumber(int n)
    {

        int k = 1;
        while (k < (n / k)) {

            // check if k divides n or not
            if (n % k == 0) {

                // Check if n/k is power of 2 or not
                if (isPowerOfTwo(n / k))
                    return true;
            }

            // update k to next odd number
            k = k + 2;
        }

        // If we reach here means
        // there exists no value of K
        // Such that k is odd number
        // and n/k is a power of 2 greater than k
        return false;
    }

    // Driver code
    public static void Main()
    {

        // Get n
        int n = 25;

        // Check n for Proth Number
        if (isProthNumber(n - 1))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check Proth number

// Utility function to check
// power of two
function isPowerOfTwo($n)
{
    return ($n && !($n & ($n - 1)));
}

// Function to check if the
// Given number is Proth
// number or not
function isProthNumber($n)
{
    $k = 1;
    while ($k < ($n / $k))
    {

        // check if k divides n or not
        if ($n % $k == 0)
        {

            // Check if n/k is power
            // of 2 or not
            if (isPowerOfTwo($n / $k))
                return true;
        }

        // update k to next odd number
        $k = $k + 2;
    }

    // If we reach here means
    // there exists no value of K
    // Such that k is odd number
    // and n/k is a power of 2
    // greater than k
    return false;
}

// Driver code

// Get n
$n = 25;

// Check n for Proth Number
if (isProthNumber($n - 1))
    echo "YES";
else
    echo "NO";

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// Javascript program to check Proth number

// Utility function to check power of two
function isPowerOfTwo(n)
{
    return (n && !(n & (n - 1)));
}

// Function to check if the
// Given number is Proth number or not
function isProthNumber(n)
{
    let k = 1;
    while (k < parseInt(n / k))
    {

        // Check if k divides n or not
        if (n % k == 0)
        {

            // Check if n/k is power of 2 or not
            if (isPowerOfTwo(parseInt(n / k)))
                return true;
        }

        // Update k to next odd number
        k = k + 2;
    }

    // If we reach here means
    // there exists no value of K
    // Such that k is odd number
    // and n/k is a power of 2 greater than k
    return false;
}

// Driver code

// Get n
let n = 25;

// Check n for Proth Number
if (isProthNumber(n - 1))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
YES
```
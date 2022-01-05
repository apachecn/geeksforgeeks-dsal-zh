# 检查一个数的任何排列是否能被 3 整除并且是回文

> 原文:[https://www . geeksforgeeks . org/检查一个数字的任何排列是否可被 3 整除并且是回文/](https://www.geeksforgeeks.org/check-if-any-permutation-of-a-number-is-divisible-by-3-and-is-palindromic/)

给定一个整数![N  ](img/05447a6f3ec73065b361522074101320.png "Rendered by QuickLaTeX.com")。任务是检查它的任何排列是否是回文，是否能被 3 整除。
**示例** :

```
Input : N =  34734
Output : True

Input : N =  34234
Output : False
```

**基本方法:**首先，创建给定整数的所有排列，并针对每个排列检查该排列是否是回文，是否也能被 3 整除。这将花费大量时间来创建所有可能的排列，然后对每个排列检查它是否是回文。这个的时间复杂度是 O(n*n！).
**有效途径:**可以观察到，任何一个数要成为回文，最多一个数字可以有奇数频率，其余数字必须有偶数频率。另外，一个数要能被 3 整除，它的位数之和必须能被 3 整除。所以，计算数字并存储数字的频率，通过计算同样的分析，结果很容易得出。
以下是上述方法的实施:

## C++

```
// C++ program to check if any permutation
// of a number is divisible by 3
// and is Palindromic

#include <bits/stdc++.h>
using namespace std;

// Function to check if any permutation
// of a number is divisible by 3
// and is Palindromic
bool isDivisiblePalindrome(int n)
{
    // Hash array to store frequency
    // of digits of n
    int hash[10] = { 0 };

    int digitSum = 0;

    // traverse the digits of integer
    // and store their frequency
    while (n) {

        // Calculate the sum of
        // digits simultaneously
        digitSum += n % 10;
        hash[n % 10]++;
        n /= 10;
    }

    // Check if number is not
    // divisible by 3
    if (digitSum % 3 != 0)
        return false;

    int oddCount = 0;
    for (int i = 0; i < 10; i++) {
        if (hash[i] % 2 != 0)
            oddCount++;
    }

    // If more than one digits have odd frequency,
    // palindromic permutation not possible
    if (oddCount > 1)
        return false;
    else
        return true;
}

// Driver Code
int main()
{
    int n = 34734;

    isDivisiblePalindrome(n) ?
             cout << "True" :
                  cout << "False";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

public class GFG{

    // Function to check if any permutation
    // of a number is divisible by 3
    // and is Palindromic
    static boolean isDivisiblePalindrome(int n)
    {
        // Hash array to store frequency
        // of digits of n
        int hash[] = new int[10];

        int digitSum = 0;

        // traverse the digits of integer
        // and store their frequency
        while (n != 0) {

            // Calculate the sum of
            // digits simultaneously
            digitSum += n % 10;
            hash[n % 10]++;
            n /= 10;
        }

        // Check if number is not
        // divisible by 3
        if (digitSum % 3 != 0)
            return false;

        int oddCount = 0;
        for (int i = 0; i < 10; i++) {
            if (hash[i] % 2 != 0)
                oddCount++;
        }

        // If more than one digits have odd frequency,
        // palindromic permutation not possible
        if (oddCount > 1)
            return false;
        else
            return true;
    }

    // Driver Code
    public static void main(String []args){

    int n = 34734;

     System.out.print(isDivisiblePalindrome(n)) ;
    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 program to check if
# any permutation of a number
# is divisible by 3 and is Palindromic

# Function to check if any permutation
# of a number is divisible by 3
# and is Palindromic
def isDivisiblePalindrome(n):

    # Hash array to store frequency
    # of digits of n
    hash = [0] * 10

    digitSum = 0

    # traverse the digits of integer
    # and store their frequency
    while (n) :

        # Calculate the sum of
        # digits simultaneously
        digitSum += n % 10
        hash[n % 10] += 1
        n //= 10

    # Check if number is not
    # divisible by 3
    if (digitSum % 3 != 0):
        return False

    oddCount = 0
    for i in range(10) :
        if (hash[i] % 2 != 0):
            oddCount += 1

    # If more than one digits have
    # odd frequency, palindromic
    # permutation not possible
    if (oddCount > 1):
        return False
    else:
        return True

# Driver Code
n = 34734

if (isDivisiblePalindrome(n)):
    print("True")
else:
    print("False")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to check if any permutation
// of a number is divisible by 3
// and is Palindromic
static bool isDivisiblePalindrome(int n)
{
    // Hash array to store frequency
    // of digits of n
    int []hash = new int[10];

    int digitSum = 0;

    // traverse the digits of integer
    // and store their frequency
    while (n != 0)
    {

        // Calculate the sum of
        // digits simultaneously
        digitSum += n % 10;
        hash[n % 10]++;
        n /= 10;
    }

    // Check if number is not
    // divisible by 3
    if (digitSum % 3 != 0)
        return false;

    int oddCount = 0;
    for (int i = 0; i < 10; i++)
    {
        if (hash[i] % 2 != 0)
            oddCount++;
    }

    // If more than one digits have odd frequency,
    // palindromic permutation not possible
    if (oddCount > 1)
        return false;
    else
        return true;
}

// Driver Code
static public void Main ()
{
    int n = 34734;

    Console.WriteLine(isDivisiblePalindrome(n));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if any permutation
// of a number is divisible by 3
// and is Palindromic

// Function to check if any permutation
// of a number is divisible by 3
// and is Palindromic

function isDivisiblePalindrome($n)
{
    // Hash array to store frequency
    // of digits of n
    $hash = array(0 );

    $digitSum = 0;

    // traverse the digits of integer
    // and store their frequency
    while ($n) {

        // Calculate the sum of
        // digits simultaneously
        $digitSum += $n % 10;
        $hash++;
        $n /= 10;
    }

    // Check if number is not
    // divisible by 3
    if ($digitSum % 3 != 0)
        return false;

    $oddCount = 0;
    for ($i = 0; $i < 10; $i++)
    {
        if ($hash % 2 != 0)
            $oddCount++;
    }

    // If more than one digits have odd frequency,
    // palindromic permutation not possible
    if ($oddCount > 1)
        return true;
    else
        return false;
}

// Driver Code
    $n = 34734;

    if(isDivisiblePalindrome($n))
            echo "True" ;
            else
            echo "False";

# This Code is contributed by Tushill.
?>
```

## java 描述语言

```
<script>

// Javascript program to check if any permutation
// of a number is divisible by 3
// and is Palindromic

// Function to check if any permutation
// of a number is divisible by 3
// and is Palindromic
function isDivisiblePalindrome(n)
{
    // Hash array to store frequency
    // of digits of n
    var hash = Array(10).fill(0);

    var digitSum = 0;

    // traverse the digits of integer
    // and store their frequency
    while (n) {

        // Calculate the sum of
        // digits simultaneously
        digitSum += n % 10;
        hash[n % 10]++;
        n = parseInt(n/10);
    }

    // Check if number is not
    // divisible by 3
    if (digitSum % 3 != 0)
        return false;

    var oddCount = 0;
    for (var i = 0; i < 10; i++) {
        if (hash[i] % 2 != 0)
            oddCount++;
    }

    // If more than one digits have odd frequency,
    // palindromic permutation not possible
    if (oddCount > 1)
        return false;
    else
        return true;
}

// Driver Code
var n = 34734;
isDivisiblePalindrome(n) ?
         document.write( "True" ):
              document.write( "False");

</script>
```

**Output:** 

```
True
```

**时间复杂度** : O(n)，其中 n 为给定数字中的位数。
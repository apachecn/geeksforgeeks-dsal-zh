# 检查最小数字的第一个和最后一个数字是否构成质数

> 原文:[https://www . geesforgeks . org/check-如果最小数字的第一个和最后一个数字构成一个质数/](https://www.geeksforgeeks.org/check-if-the-first-and-last-digit-of-the-smallest-number-forms-a-prime/)

给定一个只包含 0 到 9 的数组 arr[]，任务是从给定的数字中形成最小可能的数字，然后检查这样创建的数字的第一个和最后一个数字是否可以重新排列以形成素数。
**例:**

> **输入:** arr[]={2，6，4，9}
> **输出:**最小数:2469
> 素数组合:29
> 第一位和最后一位数字分别为 2 和 9。组合是 29 和 92。只有 29 是质数。
> **输入:** arr[]={2，6，4，3，1，7}
> **输出:**最小数:123467
> 素数组合:17 ^ 71
> 首末数字分别为 1 和 7。组合是 17 和 71，都是素数

**进场:**

1.  创建一个大小为 10 的哈希表，将给定数组中数字的出现次数存储到哈希表中。
2.  从数字 0 开始，以降序打印数字出现的次数。它类似于[通过重新排列给定数字](https://www.geeksforgeeks.org/smallest-number-rearranging-digits-given-number/)的数字而得到的最小数字。
3.  对于质数检查，检查用第一个和最后一个数字组成的数字是否是质数。对它的反面也这样做。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// function to check prime
int isPrime(int n)
{
    int i, c = 0;
    for (i = 1; i < n / 2; i++) {
        if (n % i == 0)
            c++;
    }
    if (c == 1)
        return 1;
    else
        return 0;
}

// Function to generate smallest possible
// number with given digits
void findMinNum(int arr[], int n)
{
    // Declare a hash array of size 10
    // and initialize all the elements to zero
    int first = 0, last = 0, num, rev, i;
    int hash[10] = { 0 };

    // store the number of occurrences of the digits
    // in the given array into the hash table
    for (int i = 0; i < n; i++) {
        hash[arr[i]]++;
    }

    // Traverse the hash in ascending order
    // to print the required number
    cout << "Minimum number: ";
    for (int i = 0; i <= 9; i++) {

        // Print the number of times a digits occurs
        for (int j = 0; j < hash[i]; j++)
            cout << i;
    }

    cout << endl;

    // extracting the first digit
    for (i = 0; i <= 9; i++) {
        if (hash[i] != 0) {
            first = i;
            break;
        }
    }
    // extracting the last digit
    for (i = 9; i >= 0; i--) {
        if (hash[i] != 0) {
            last = i;
            break;
        }
    }

    num = first * 10 + last;
    rev = last * 10 + first;

    // printing the prime combinations
    cout << "Prime combinations: ";
    if (isPrime(num) && isPrime(rev))
        cout << num << " " << rev;

    else if (isPrime(num))
        cout << num;

    else if (isPrime(rev))
        cout << rev;

    else
        cout << "No combinations exist";
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 7, 8};
    findMinNum(arr, 5);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```

// Java implementation of above approach

import java.io.*;

class SmallPrime
{

// function to check prime
static boolean isPrime(int n)
{
    int i, c = 0;
    for (i = 1; i < n / 2; i++)
    {
        if (n % i == 0)
            c++;
    }
    if (c == 1)
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Function to generate smallest possible
// number with given digits
static void findMinNum(int arr[], int n)
{
    // Declare a hash array of size 10
    // and initialize all the elements to zero
    int first = 0, last = 0, num, rev, i;
    int hash[] = new int[10];

    // store the number of occurrences of the digits
    // in the given array into the hash table
    for ( i = 0; i < n; i++)
    {
        hash[arr[i]]++;
    }

    // Traverse the hash in ascending order
    // to print the required number
    System.out.print("Minimum number: ");
    for ( i = 0; i <= 9; i++)
    {

        // Print the number of times a digits occurs
        for (int j = 0; j < hash[i]; j++)
            System.out.print(i);

    }
    System.out.println();

    System.out.println();
    // extracting the first digit
    for (i = 0; i <= 9; i++)
    {
        if (hash[i] != 0)
        {
            first = i;
            break;
        }
    }
    // extracting the last digit
    for (i = 9; i >= 0; i--)
    {
        if (hash[i] != 0)
        {
            last = i;
            break;
        }
    }

    num = first * 10 + last;
    rev = last * 10 + first;

    // printing the prime combinations
    System.out.print( "Prime combinations: ");
    if (isPrime(num) && isPrime(rev))
    {
        System.out.println(num + " " + rev);
    }   
    else if (isPrime(num))
    {
        System.out.println(num);
    }   
    else if (isPrime(rev))
    {
        System.out.println(rev);
    }   

    else
    {
        System.out.println("No combinations exist");
    }
}

// Driver code

    public static void main (String[] args)
    {
       SmallPrime smallprime = new SmallPrime();
       int arr[] = {1, 2, 4, 7, 8};
       smallprime.findMinNum(arr, 5);
    }
}

// This code has been contributed by inder_verma.
```

## 蟒蛇 3

```
# Python3 implementation of above
# approach
import math as mt

# function to check prime
def isPrime(n):
    i, c = 0, 0
    for i in range(1, n // 2):
        if (n % i == 0):
            c += 1

    if (c == 1):
        return 1
    else:
        return 0

# Function to generate smallest possible
# number with given digits
def findMinNum(arr, n):

    # Declare a Hash array of size 10
    # and initialize all the elements to zero
    first, last = 0, 0
    Hash = [0 for i in range(10)]

    # store the number of occurrences of
    # the digits in the given array into
    # the Hash table
    for i in range(n):
        Hash[arr[i]] += 1

    # Traverse the Hash in ascending order
    # to print the required number
    print("Minimum number: ", end = "")
    for i in range(0, 10):

        # Print the number of times
        # a digits occurs
        for j in range(Hash[i]):
            print(i, end = "")

    print()

    # extracting the first digit
    for i in range(10):
        if (Hash[i] != 0):
            first = i
            break

    # extracting the last digit
    for i in range(9, -1, -1):
        if (Hash[i] != 0):
            last = i
            break

    num = first * 10 + last
    rev = last * 10 + first

    # printing the prime combinations
    print("Prime combinations: ", end = "")
    if (isPrime(num) and isPrime(rev)):
        print(num, " ", rev)
    elif (isPrime(num)):
        print(num)
    elif (isPrime(rev)):
        print(rev)
    else:
        print("No combinations exist")

# Driver code
arr = [ 1, 2, 4, 7, 8]
findMinNum(arr, 5)

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// function to check prime
static bool isPrime(int n)
{
    int i, c = 0;
    for (i = 1; i < n / 2; i++)
    {
        if (n % i == 0)
        {
            c++;
        }
    }
    if (c == 1)
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Function to generate smallest
// possible number with given digits
static void findMinNum(int[] arr, int n)
{
    // Declare a hash array of
    // size 10 and initialize
    // all the elements to zero
    int first = 0, last = 0, num, rev, i;
    int[] hash = new int[10];

    // store the number of occurrences
    // of the digits in the given array
    // into the hash table
    for (i = 0; i < n; i++)
    {
        hash[arr[i]]++;
    }

    // Traverse the hash in ascending order
    // to print the required number
    Console.Write("Minimum number: ");
    for (i = 0; i <= 9; i++)
    {

        // Print the number of times
        // a digits occurs
        for (int j = 0; j < hash[i]; j++)
        {
            Console.Write(i);
        }

    }
    Console.WriteLine();

    Console.WriteLine();

    // extracting the first digit
    for (i = 0; i <= 9; i++)
    {
        if (hash[i] != 0)
        {
            first = i;
            break;
        }
    }

    // extracting the last digit
    for (i = 9; i >= 0; i--)
    {
        if (hash[i] != 0)
        {
            last = i;
            break;
        }
    }

    num = first * 10 + last;
    rev = last * 10 + first;

    // printing the prime combinations
    Console.Write("Prime combinations: ");
    if (isPrime(num) && isPrime(rev))
    {
        Console.WriteLine(num + " " + rev);
    }
    else if (isPrime(num))
    {
        Console.WriteLine(num);
    }
    else if (isPrime(rev))
    {
        Console.WriteLine(rev);
    }
    else
    {
        Console.WriteLine("No combinations exist");
    }
}

// Driver code
public static void Main()
{
    int[] arr = {1, 2, 4, 7, 8};
    findMinNum(arr, 5);
}
}

// This code is contributed
// by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// function to check prime
function isPrime($n)
{
    $c = 0;
    for ($i = 1; $i < $n / 2; $i++)
    {
        if ($n % $i == 0)
            $c++;
    }
    if ($c == 1)
        return 1;
    else
        return 0;
}

// Function to generate smallest possible
// number with given digits
function findMinNum($arr, $n)
{
    // Declare a hash array of size 10
    // and initialize all the elements to zero
    $first = 0; $last = 0;
    $num; $rev ; $i;
    $hash = array_fill(0, 20, 0);

    // store the number of occurrences of
    // the digits in the given array into
    // the hash table
    for ($i = 0; $i < $n; $i++)
    {
        $hash[$arr[$i]]++;
    }

    // Traverse the hash in ascending order
    // to print the required number
    echo "Minimum number: ";
    for ( $i = 0; $i <= 9; $i++)
    {

        // Print the number of times a
        // digits occurs
        for ($j = 0; $j < $hash[$i]; $j++)
            echo $i;
    }

    // extracting the first digit
    for ($i = 0; $i <= 9; $i++)
    {
        if ($hash[$i] != 0)
        {
            $first = $i;
            break;
        }
    }

    // extracting the last digit
    for ($i = 9; $i >= 0; $i--)
    {
        if ($hash[$i] != 0)
        {
            $last = $i;
            break;
        }
    }

    $num = $first * 10 + $last;
    $rev = $last * 10 + $first;

    // printing the prime combinations
    echo "\nPrime combinations: ";
    if (isPrime($num) && isPrime($rev))
        echo $num. " " . $rev;

    else if (isPrime($num))
        echo $num;

    else if (isPrime($rev))
        echo $rev;

    else
        echo "No combinations exist";
}

// Driver Code
$arr = array(1, 2, 4, 7, 8);
findMinNum($arr, 5);

// This code is contributed
// by Rajput-Ji
?>
```

## java 描述语言

```
<script>
      // JavaScript implementation of above approach
      // function to check prime
      function isPrime(n) {
        var i,
          c = 0;
        for (i = 1; i < n / 2; i++) {
          if (n % i == 0) c++;
        }
        if (c == 1) return 1;
        else return 0;
      }

      // Function to generate smallest possible
      // number with given digits
      function findMinNum(arr, n) {
        // Declare a hash array of size 10
        // and initialize all the elements to zero
        var first = 0,
          last = 0,
          num,
          rev,
          i;
        var hash = new Array(10).fill(0);

        // store the number of occurrences of the digits
        // in the given array into the hash table
        for (var i = 0; i < n; i++) {
          hash[arr[i]]++;
        }

        // Traverse the hash in ascending order
        // to print the required number
        document.write("Minimum number: ");
        for (var i = 0; i <= 9; i++) {
          // Print the number of times a digits occurs
          for (var j = 0; j < hash[i]; j++) document.write(i);
        }

        document.write("<br>");

        // extracting the first digit
        for (i = 0; i <= 9; i++) {
          if (hash[i] != 0) {
            first = i;
            break;
          }
        }
        // extracting the last digit
        for (i = 9; i >= 0; i--) {
          if (hash[i] != 0) {
            last = i;
            break;
          }
        }

        num = first * 10 + last;
        rev = last * 10 + first;

        // printing the prime combinations
        document.write("Prime combinations: ");
        if (isPrime(num) && isPrime(rev)) document.write(num + " " + rev);
        else if (isPrime(num)) document.write(num);
        else if (isPrime(rev)) document.write(rev);
        else document.write("No combinations exist");
      }

      // Driver code
      var arr = [1, 2, 4, 7, 8];
      findMinNum(arr, 5);
    </script>
```

**Output:** 

```
Minimum number: 12478
Prime combinations: No combinations exist
```
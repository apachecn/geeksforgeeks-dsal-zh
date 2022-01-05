# 检查大数的任何排列是否能被 8 整除

> 原文:[https://www . geeksforgeeks . org/检查大数的任意排列是否可被 8 整除/](https://www.geeksforgeeks.org/check-if-any-permutation-of-a-large-number-is-divisible-by-8/)

给定一个大数 N，任务是检查一个大数的任何排列是否能被 8 整除。
**例:**

```
Input: N = 31462708
Output: Yes
Many of permutation of number N like 
34678120, 34278160 are divisible by 8\. 

Input: 75
Output: No
```

一种**天真的方法**是生成数字 N 的所有排列，并检查是否(N % 8 == 0)，如果任何排列可被 8 整除，则返回 true。
一个**有效的方法**是利用这样一个事实，如果一个数的最后三个数字能被 8 整除，那么这个数也能被 8 整除。以下是所需步骤:

*   使用散列表计算给定数字中所有数字的出现次数。
*   遍历所有可被 8 整除的三位数。
*   检查三位数中的数字是否在哈希表中。
*   如果是，一个数字可以通过置换形成，最后三位数字组合形成三位数字。
*   如果三位数都不能构成，则返回 false。

以下是上述方法的实现:

## C++

```
// C++ program to check if any permutation of
// a large number is divisible by 8 or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if any permutation
// of a large number is divisible by 8
bool solve(string n, int l)
{

    // Less than three digit number
    // can be checked directly.
    if (l < 3) {
        if (stoi(n) % 8 == 0)
            return true;

        // check for the reverse of a number
        reverse(n.begin(), n.end());
        if (stoi(n) % 8 == 0)
            return true;
        return false;
    }

    // Stores the Frequency of characters in the n.
    int hash[10] = { 0 };
    for (int i = 0; i < l; i++)
        hash[n[i] - '0']++;

    // Iterates for all three digit numbers
    // divisible by 8
    for (int i = 104; i < 1000; i += 8) {

        int dup = i;

        // stores the frequency of all single
        // digit in three-digit number
        int freq[10] = { 0 };
        freq[dup % 10]++;
        dup = dup / 10;
        freq[dup % 10]++;
        dup = dup / 10;
        freq[dup % 10]++;

        dup = i;

        // check if the original number has
        // the digit
        if (freq[dup % 10] > hash[dup % 10])
            continue;
        dup = dup / 10;

        if (freq[dup % 10] > hash[dup % 10])
            continue;
        dup = dup / 10;

        if (freq[dup % 10] > hash[dup % 10])
            continue;

        return true;
    }

    // when all are checked its not possible
    return false;
}

// Driver Code
int main()
{
    string number = "31462708";
    int l = number.length();

    if (solve(number, l))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// any permutation of a large
// number is divisible by 8 or not
import java.util.*;

class GFG
{
    // Function to check if any
    // permutation of a large
    // number is divisible by 8
    public static boolean solve(String n, int l)
    {

        // Less than three digit number
        // can be checked directly.
        if (l < 3)
        {
            if (Integer.parseInt(n) % 8 == 0)
                return true;

            // check for the reverse
            // of a number
            n = new String((new StringBuilder()).append(n).reverse());

            if (Integer.parseInt(n) % 8 == 0)
                return true;
            return false;
        }

        // Stores the Frequency of
        // characters in the n.
        int []hash = new int[10];
        for (int i = 0; i < l; i++)
            hash[n.charAt(i) - '0']++;

        // Iterates for all
        // three digit numbers
        // divisible by 8
        for (int i = 104; i < 1000; i += 8)
        {
            int dup = i;

            // stores the frequency of
            // all single digit in
            // three-digit number
            int []freq = new int[10];
            freq[dup % 10]++;
            dup = dup / 10;
            freq[dup % 10]++;
            dup = dup / 10;
            freq[dup % 10]++;

            dup = i;

            // check if the original
            // number has the digit
            if (freq[dup % 10] >
                hash[dup % 10])
                continue;
            dup = dup / 10;

            if (freq[dup % 10] >
                hash[dup % 10])
                continue;
            dup = dup / 10;

            if (freq[dup % 10] >
                hash[dup % 10])
                continue;

            return true;
        }

        // when all are checked
        // its not possible
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String number = "31462708";

        int l = number.length();

        if (solve(number, l))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed
// by Harshit Saini
```

## 蟒蛇 3

```
# Python3 program to check if
# any permutation of a large
# number is divisible by 8 or not

# Function to check if any
# permutation of a large
# number is divisible by 8
def solve(n, l):

    # Less than three digit
    # number can be checked
    # directly.
    if l < 3:
        if int(n) % 8 == 0:
            return True

        # check for the reverse
        # of a number
        n = n[::-1]

        if int(n) % 8 == 0:
            return True
        return False

    # Stores the Frequency of
    # characters in the n.
    hash = 10 * [0]
    for i in range(0, l):
        hash[int(n[i]) - 0] += 1;

    # Iterates for all
    # three digit numbers
    # divisible by 8
    for i in range(104, 1000, 8):
        dup = i

        # stores the frequency
        # of all single digit
        # in three-digit number
        freq = 10 * [0]
        freq[int(dup % 10)] += 1;
        dup = dup / 10
        freq[int(dup % 10)] += 1;
        dup = dup / 10
        freq[int(dup % 10)] += 1;

        dup = i

        # check if the original
        # number has the digit
        if (freq[int(dup % 10)] >
            hash[int(dup % 10)]):
            continue;
        dup = dup / 10;

        if (freq[int(dup % 10)] >
            hash[int(dup % 10)]):
            continue;
        dup = dup / 10

        if (freq[int(dup % 10)] >
            hash[int(dup % 10)]):
            continue;

        return True

    # when all are checked
    # its not possible
    return False

# Driver Code
if __name__ == "__main__":

    number = "31462708"

    l = len(number)

    if solve(number, l):
        print("Yes")
    else:
        print("No")

# This code is contributed
# by Harshit Saini
```

## C#

```
// C# program to check if
// any permutation of a large
// number is divisible by 8 or not
using System;
using System.Collections.Generic;

class GFG
{
    // Function to check if any
    // permutation of a large
    // number is divisible by 8
    public static bool solve(String n, int l)
    {

        // Less than three digit number
        // can be checked directly.
        if (l < 3)
        {
            if (int.Parse(n) % 8 == 0)
                return true;

            // check for the reverse
            // of a number
            n = reverse(n);

            if (int.Parse(n) % 8 == 0)
                return true;
            return false;
        }

        // Stores the Frequency of
        // characters in the n.
        int []hash = new int[10];
        for (int i = 0; i < l; i++)
            hash[n[i] - '0']++;

        // Iterates for all
        // three digit numbers
        // divisible by 8
        for (int i = 104; i < 1000; i += 8)
        {
            int dup = i;

            // stores the frequency of
            // all single digit in
            // three-digit number
            int []freq = new int[10];
            freq[dup % 10]++;
            dup = dup / 10;
            freq[dup % 10]++;
            dup = dup / 10;
            freq[dup % 10]++;

            dup = i;

            // check if the original
            // number has the digit
            if (freq[dup % 10] >
                hash[dup % 10])
                continue;
            dup = dup / 10;

            if (freq[dup % 10] >
                hash[dup % 10])
                continue;
            dup = dup / 10;

            if (freq[dup % 10] >
                hash[dup % 10])
                continue;

            return true;
        }

        // when all are checked
        // its not possible
        return false;
    }

    static String reverse(String input)
    {
        char[] a = input.ToCharArray();
        int l, r = 0;
        r = a.Length - 1;

        for (l = 0; l < r; l++, r--)
        {
            // Swap values of l and r
            char temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return String.Join("",a);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String number = "31462708";

        int l = number.Length;

        if (solve(number, l))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Princi Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
error_reporting(0);
// PHP program to check
// if any permutation of
// a large number is
// divisible by 8 or not

// Function to check if
// any permutation of a
// large number is divisible by 8
function solve($n, $l)
{

    // Less than three digit
    // number can be checked
    // directly.
    if ($l < 3)
    {
        if (intval($n) % 8 == 0)
            return true;

        // check for the
        // reverse of a number
        strrev($n);
        if (intval($n) % 8 == 0)
            return true;
        return false;
    }

    // Stores the Frequency of
    // characters in the n.
    $hash[10] = array(0);
    for ($i = 0; $i < $l; $i++)
        $hash[$n[$i] - '0']++;

    // Iterates for all three
    // digit numbers divisible by 8
    for ($i = 104;
         $i < 1000; $i += 8)
    {

        $dup = $i;

        // stores the frequency of
        // all single digit in
        // three-digit number
        $freq[10] = array(0);
        $freq[$dup % 10]++;
        $dup = $dup / 10;
        $freq[$dup % 10]++;
        $dup = $dup / 10;
        $freq[$dup % 10]++;

        $dup = $i;

        // check if the original
        // number has the digit
        if ($freq[$dup % 10] >
            $hash[$dup % 10])
            continue;
        $dup = $dup / 10;

        if ($freq[$dup % 10] >
            $hash[$dup % 10])
            continue;
        $dup = $dup / 10;

        if ($freq[$dup % 10] >
            $hash[$dup % 10])
            continue;

        return true;
    }

    // when all are checked
    // its not possible
    return false;
}

// Driver Code
$number = "31462708";
$l = strlen($number);

if (solve($number, $l))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>

      // JavaScript program to check if
      // any permutation of a large
      // number is divisible by 8 or not

      // Function to check if any
      // permutation of a large
      // number is divisible by 8
      function solve(n, l) {
        // Less than three digit number
        // can be checked directly.
        if (l < 3) {
          if (parseInt(n) % 8 === 0) return true;

          // check for the reverse
          // of a number
          n = reverse(n);

          if (parseInt(n) % 8 === 0) return true;
          return false;
        }

        // Stores the Frequency of
        // characters in the n.
        var hash = new Array(10).fill(0);
        for (var i = 0; i < l; i++) hash[parseInt(n[i]) - 0]++;

        // Iterates for all
        // three digit numbers
        // divisible by 8
        for (var i = 104; i < 1000; i += 8) {
          var dup = i;

          // stores the frequency of
          // all single digit in
          // three-digit number
          var freq = new Array(10).fill(0);
          freq[parseInt(dup % 10)]++;
          dup = dup / 10;
          freq[parseInt(dup % 10)]++;
          dup = dup / 10;
          freq[parseInt(dup % 10)]++;

          dup = i;

          // check if the original
          // number has the digit
          if (freq[parseInt(dup % 10)] > hash[parseInt(dup % 10)])
          continue;
          dup = dup / 10;

          if (freq[parseInt(dup % 10)] > hash[parseInt(dup % 10)])
          continue;
          dup = dup / 10;

          if (freq[parseInt(dup % 10)] > hash[parseInt(dup % 10)])
          continue;

          return true;
        }

        // when all are checked
        // its not possible
        return false;
      }

      function reverse(input) {
        var a = input.split("");
        var l,
          r = 0;
        r = a.length - 1;

        for (l = 0; l < r; l++, r--) {
          // Swap values of l and r
          var temp = a[l];
          a[l] = a[r];
          a[r] = temp;
        }
        return a.join("");
      }

      // Driver Code
      var number = "31462708";

      var l = number.length;

      if (solve(number, l))
      document.write("Yes");
      else
      document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(L)，其中 L 为数字中的位数。
# 最小和最大 N 位回文

> 原文:[https://www . geesforgeks . org/最小和最大 n 位回文/](https://www.geeksforgeeks.org/smallest-and-largest-palindrome-with-n-digits/)

给定一个数字 **N** 。任务是找到可能的最小和最大的 N 位数回文数。
**例:**

```
Input: N = 4 
Output: 
Smallest Palindrome = 1001
Largest Palindrome = 9999

Input: N = 5
Output: 
Smallest Palindrome = 10001
Largest Palindrome = 99999
```

**最小 N 位回文数**:仔细观察会发现，对于 N = 1，最小回文数为 0。对于 N 的任何其他值，最小的回文的第一个和最后一个数字都是 1，中间的所有数字都是 0。

*   情况 1:如果 N = 1，那么答案将是 0。
*   案例二:如果 N！= 1 则答案为(10 <sup>(N-1)</sup> ) + 1。

**最大 N 位回文数**:和上面的做法类似，可以看到 N 次追加 9 可以得到 N 位可能的最大回文数。因此，最大的 N 位回文数字将是**10<sup>N</sup>–1**。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the smallest and largest
// palindrome with N digits
void printPalindrome(int n)
{
    if (n == 1)
    {
        cout<<"Smallest Palindrome: 0"<<endl;
        cout<<"Largest Palindrome: 9";
    }
    else
    {
        cout<<"Smallest Palindrome: "<<pow(10, n - 1) + 1;
        cout<<"\nLargest Palindrome: "<<pow(10,n) - 1;
    }
}

// Driver Code
int main()
{
    int n = 4;
    printPalindrome(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GfG {

    // Function to print the smallest and largest
    // palindrome with N digits
    static void printPalindrome(int n)
    {
        if (n == 1)
        {
            System.out.println("Smallest Palindrome: 0");
            System.out.println("Largest Palindrome: 9");
        }
        else
        {
            System.out.println("Smallest Palindrome: "
                    + (int)(Math.pow(10, n - 1)) + 1);

            System.out.println("Largest Palindrome: "
                    + ((int)(Math.pow(10,n)) - 1));
        }
    }

    // Driver Code
    public static void main(String[] args) {
        int n = 4;
        printPalindrome(n);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

from math import pow

# Function to print the smallest and largest
# palindrome with N digits
def printPalindrome(n):
    if (n == 1):
        print("Smallest Palindrome: 0")
        print("Largest Palindrome: 9")
    else:
        print("Smallest Palindrome:", int(pow(10, n - 1))+1)
        print("Largest Palindrome:", int(pow(10,n))-1)

# Driver Code
if __name__ == '__main__':
    n = 4
    printPalindrome(n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Function to print the smallest and largest
    // palindrome with N digits
    static void printPalindrome(int n)
    {
        if (n == 1)
        {
            Console.WriteLine("Smallest Palindrome: 0");
            Console.WriteLine("Largest Palindrome: 9");
        }
        else
        {
            Console.WriteLine("Smallest Palindrome: "
                    + (int)(Math.Pow(10, n - 1)) + 1);

            Console.WriteLine("Largest Palindrome: "
                    + ((int)(Math.Pow(10,n)) - 1));
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 4;
        printPalindrome(n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to print the smallest and largest
// palindrome with N digits
function printPalindrome($n)
{
    if ($n == 1)
    {
        echo "Smallest Palindrome: 0\n";
        echo "Largest Palindrome: 9";
    }
    else
    {
        echo "Smallest Palindrome: ",
                 pow(10, $n - 1) + 1;
        echo "\nLargest Palindrome: ",
                      pow(10, $n) - 1;
    }
}

// Driver Code
$n = 4;
printPalindrome($n);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
  <script>
    // Javascript implementation of the above approach

    // Function to print the smallest and largest
    // palindrome with N digits
    function printPalindrome(n)
    {
      if (n == 1)
      {
        document.write("Smallest Palindrome: 0<br>");
        document.write("Largest Palindrome: 9");
      }
      else
      {
        document.write("Smallest Palindrome: " + (parseInt(Math.pow(10, n - 1)) + 1));
        document.write("<br>Largest Palindrome: " + parseInt(Math.pow(10, n) - 1));
      }
    }

    // Driver Code
    var n = 4;
    printPalindrome(n);

// This code is contributed by rrrtnx.
  </script>
```

**Output:** 

```
Smallest Palindrome: 1001
Largest Palindrome: 9999
```

**时间复杂度:** O(1)
# 数组中最大的回文数

> 原文:[https://www . geesforgeks . org/maximum-回文数组中的数字/](https://www.geeksforgeeks.org/largest-palindromic-number-in-an-array/)

给定一个非负整数数组 **arr[]** 。任务是找出数组中最大的一个数，也就是回文。如果没有这样的号码，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {1，232，54545，999991 }；
> T3】产量: 54545
> 
> **输入:** arr[] = {1，2，3，4，5，50 }；
> T3】输出: 5

**方法 1:**

*   [按升序排序](https://www.geeksforgeeks.org/merge-sort/)数组。
*   从末尾开始遍历数组。
*   第一个数字是回文，这是必须的答案。
*   如果没有找到回文编号，则打印 **-1**

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if n is palindrome
bool isPalindrome(int n)
{
    // Find the appropriate divisor
    // to extract the leading digit
    int divisor = 1;
    while (n / divisor >= 10)
        divisor *= 10;

    while (n != 0) {
        int leading = n / divisor;
        int trailing = n % 10;

        // If first and last digits are
        // not same then return false
        if (leading != trailing)
            return false;

        // Removing the leading and trailing
        // digits from the number
        n = (n % divisor) / 10;

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        divisor = divisor / 100;
    }
    return true;
}

// Function to find the largest palindromic number
int largestPalindrome(int A[], int n)
{

    // Sort the array
    sort(A, A + n);

    for (int i = n - 1; i >= 0; --i) {

        // If number is palindrome
        if (isPalindrome(A[i]))
            return A[i];
    }

    // If no palindromic number found
    return -1;
}

// Driver program
int main()
{
    int A[] = { 1, 232, 54545, 999991 };
    int n = sizeof(A) / sizeof(A[0]);

    // print required answer
    cout << largestPalindrome(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.util.*;

class GFG
{
    // Function to check if n is palindrome
    static boolean isPalindrome(int n)
    {
        // Find the appropriate divisor
        // to extract the leading digit
        int divisor = 1;
        while (n / divisor >= 10)
            divisor *= 10;

        while (n != 0) {
            int leading = n / divisor;
            int trailing = n % 10;

            // If first and last digits are
            // not same then return false
            if (leading != trailing)
                return false;

            // Removing the leading and trailing
            // digits from the number
            n = (n % divisor) / 10;

            // Reducing divisor by a factor
            // of 2 as 2 digits are dropped
            divisor = divisor / 100;
        }
        return true;
    }

    // Function to find the largest palindromic number
    static int largestPalindrome(int []A, int n)
    {

        // Sort the array
        Arrays.sort(A);

        for (int i = n - 1; i >= 0; --i) {

            // If number is palindrome
            if (isPalindrome(A[i]))
                return A[i];
        }

        // If no palindromic number found
        return -1;
    }

    // Driver program
    public static void main(String []args)
    {
        int []A = { 1, 232, 54545, 999991 };
        int n = A.length;

        // print required answer
        System.out.println(largestPalindrome(A, n));

    }

}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to check if n is palindrome
def isPalindrome(n) :

    # Find the appropriate divisor
    # to extract the leading digit
    divisor = 1

    while (n / divisor >= 10) :
        divisor *= 10

    while (n != 0) :

        leading = n // divisor
        trailing = n % 10

        # If first and last digits are
        # not same then return false
        if (leading != trailing) :
            return False

        # Removing the leading and trailing
        # digits from the number
        n = (n % divisor) // 10

        # Reducing divisor by a factor
        # of 2 as 2 digits are dropped
        divisor = divisor // 100

    return True

# Function to find the largest
# palindromic number
def largestPalindrome(A, n) :

    # Sort the array
    A.sort()

    for i in range(n - 1, -1, -1) :

        # If number is palindrome
        if (isPalindrome(A[i])) :
            return A[i]

    # If no palindromic number found
    return -1

# Driver Code
if __name__ == "__main__" :

    A = [ 1, 232, 54545, 999991 ]
    n = len(A)

    # print required answer
    print(largestPalindrome(A, n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of above approach

using System;

class GFG
{
    // Function to check if n is palindrome
    static bool isPalindrome(int n)
    {
        // Find the appropriate divisor
        // to extract the leading digit
        int divisor = 1;
        while (n / divisor >= 10)
            divisor *= 10;

        while (n != 0) {
            int leading = n / divisor;
            int trailing = n % 10;

            // If first and last digits are
            // not same then return false
            if (leading != trailing)
                return false;

            // Removing the leading and trailing
            // digits from the number
            n = (n % divisor) / 10;

            // Reducing divisor by a factor
            // of 2 as 2 digits are dropped
            divisor = divisor / 100;
        }
        return true;
    }

    // Function to find the largest palindromic number
    static int largestPalindrome(int []A, int n)
    {

        // Sort the array
        Array.Sort(A);

        for (int i = n - 1; i >= 0; --i) {

            // If number is palindrome
            if (isPalindrome(A[i]))
                return A[i];
        }

        // If no palindromic number found
        return -1;
    }

    // Driver program
    public static void Main()
    {
        int []A = { 1, 232, 54545, 999991 };
        int n = A.Length;

        // print required answer
        Console.WriteLine(largestPalindrome(A, n));

    }

}

// This code is contributed
// by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to check if n is palindrome
function isPalindrome($n)
{
    // Find the appropriate divisor
    // to extract the leading digit
    $divisor = 1;
    while ((int)($n / $divisor) >= 10)
        $divisor *= 10;

    while ($n != 0)
    {
        $leading = (int)($n / $divisor);
        $trailing = $n % 10;

        // If first and last digits are
        // not same then return false
        if ($leading != $trailing)
            return false;

        // Removing the leading and trailing
        // digits from the number
        $n = (int)(($n % $divisor) / 10);

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        $divisor = (int)($divisor / 100);
    }
    return true;
}

// Function to find the largest
// palindromic number
function largestPalindrome($A, $n)
{

    // Sort the array
    sort($A);

    for ($i = $n - 1; $i >= 0; --$i)
    {

        // If number is palindrome
        if (isPalindrome($A[$i]))
            return $A[$i];
    }

    // If no palindromic number found
    return -1;
}

// Driver Code
$A = array(1, 232, 54545, 999991);
$n = sizeof($A);

// print required answer
echo largestPalindrome($A, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
//Javascript implementation of above approach

//function for sorting
function ssort(a, n) {
   var i, j, min, temp;
   for (i = 0; i < n - 1; i++) {
      min = i;
      for (j = i + 1; j < n; j++)
      if (a[j] < a[min])
      min = j;
      temp = a[i];
      a[i] = a[min];
      a[min] = temp;
   }
}

// Function to check if n is palindrome
function isPalindrome(n)
{
    // Find the appropriate divisor
    // to extract the leading digit
    var divisor = 1;
    while (parseInt(n / divisor) >= 10)
        divisor *= 10;

    while (n != 0) {
        var leading = parseInt(n / divisor);
        var trailing = n % 10;

        // If first and last digits are
        // not same then return false
        if (leading != trailing)
            return false;

        // Removing the leading and trailing
        // digits from the number
        n = parseInt((n % divisor) / 10);

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        divisor = parseInt(divisor / 100);
    }
    return true;
}

// Function to find the largest palindromic number
function largestPalindrome( A, n)
{

    // Sort the array
    ssort(A,A.length);

    for (var i = n - 1; i >= 0; --i) {

        // If number is palindrome
        if (isPalindrome(A[i]))
            return A[i];
    }

    // If no palindromic number found
    return -1;
}

var  A = [ 1, 232, 54545, 999991 ];
var n = A.length;
 // print required answer
 document.write(largestPalindrome(A, n));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
54545
```

**方法二:**

*   设置一个变量 **currentMax = -1** ，开始遍历数组。
*   如果当前元素**arr【I】>currentMax**和**arr【I】**是回文。
*   然后设置 **currentMax = arr[i]** 。
*   最后打印 **currentMax** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if n is palindrome
bool isPalindrome(int n)
{
    // Find the appropriate divisor
    // to extract the leading digit
    int divisor = 1;
    while (n / divisor >= 10)
        divisor *= 10;

    while (n != 0) {
        int leading = n / divisor;
        int trailing = n % 10;

        // If first and last digits are
        // not same then return false
        if (leading != trailing)
            return false;

        // Removing the leading and trailing
        // digits from the number
        n = (n % divisor) / 10;

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        divisor = divisor / 100;
    }
    return true;
}

// Function to find the largest palindromic number
int largestPalindrome(int A[], int n)
{
    int currentMax = -1;

    for (int i = 0; i < n; i++) {

        // If a palindrome larger than the currentMax is found
        if (A[i] > currentMax && isPalindrome(A[i]))
            currentMax = A[i];
    }

    // Return the largest palindromic number from the array
    return currentMax;
}

// Driver program
int main()
{
    int A[] = { 1, 232, 54545, 999991 };
    int n = sizeof(A) / sizeof(A[0]);

    // print required answer
    cout << largestPalindrome(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.util.*;

class GFG
{
    // Function to check if n is palindrome
    static boolean isPalindrome(int n)
    {
        // Find the appropriate divisor
        // to extract the leading digit
        int divisor = 1;
        while (n / divisor >= 10)
            divisor *= 10;

        while (n != 0) {
            int leading = n / divisor;
            int trailing = n % 10;

            // If first and last digits are
            // not same then return false
            if (leading != trailing)
                return false;

            // Removing the leading and trailing
            // digits from the number
            n = (n % divisor) / 10;

            // Reducing divisor by a factor
            // of 2 as 2 digits are dropped
            divisor = divisor / 100;
        }
        return true;
    }

    // Function to find the largest palindromic number
    static int largestPalindrome(int []A, int n)
    {
        int currentMax = -1;

        for (int i = 0; i < n; i++) {

            // If a palindrome larger than the currentMax is found
            if (A[i] > currentMax && isPalindrome(A[i]))
                currentMax = A[i];
        }

        // Return the largest palindromic number from the array
        return currentMax;
    }

    // Driver program
    public static void main(String []args)
    {
        int []A = { 1, 232, 54545, 999991 };
        int n = A.length;

        // print required answer
        System.out.println(largestPalindrome(A, n));

    }

}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to check if n is palindrome
def isPalindrome(n):

    # Find the appropriate divisor
    # to extract the leading digit
    divisor = 1
    while (int(n / divisor) >= 10):
        divisor *= 10

    while (n != 0):
        leading = int(n / divisor)
        trailing = n % 10

        # If first and last digits are
        # not same then return false
        if (leading != trailing):
            return False

        # Removing the leading and trailing
        # digits from the number
        n = int((n % divisor) / 10)

        # Reducing divisor by a factor
        # of 2 as 2 digits are dropped
        divisor = int(divisor / 100)
    return True

# Function to find the largest
# palindromic number
def largestPalindrome(A, n):
    currentMax = -1

    for i in range(0, n, 1):

        # If a palindrome larger than
        # the currentMax is found
        if (A[i] > currentMax and isPalindrome(A[i])):
            currentMax = A[i]

    # Return the largest palindromic
    # number from the array
    return currentMax

# Driver Code
if __name__ == '__main__':
    A = [1, 232, 54545, 999991]
    n = len(A)

    # print required answer
    print(largestPalindrome(A, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of above approach

using System;

class GFG
{
    // Function to check if n is palindrome
    static bool isPalindrome(int n)
    {
        // Find the appropriate divisor
        // to extract the leading digit
        int divisor = 1;
        while (n / divisor >= 10)
            divisor *= 10;

        while (n != 0) {
            int leading = n / divisor;
            int trailing = n % 10;

            // If first and last digits are
            // not same then return false
            if (leading != trailing)
                return false;

            // Removing the leading and trailing
            // digits from the number
            n = (n % divisor) / 10;

            // Reducing divisor by a factor
            // of 2 as 2 digits are dropped
            divisor = divisor / 100;
        }
        return true;
    }

    // Function to find the largest palindromic number
    static int largestPalindrome(int []A, int n)
    {
        int currentMax = -1;

        for (int i = 0; i < n; i++) {

            // If a palindrome larger than the currentMax is found
            if (A[i] > currentMax && isPalindrome(A[i]))
                currentMax = A[i];
        }

        // Return the largest palindromic number from the array
        return currentMax;
    }

    // Driver program
    public static void Main()
    {
        int []A = { 1, 232, 54545, 999991 };
        int n = A.Length;

        // print required answer
        Console.WriteLine(largestPalindrome(A, n));

    }

}

// This code is contributed
// by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to check if n is palindrome
function isPalindrome($n)
{
    // Find the appropriate divisor
    // to extract the leading digit
    $divisor = 1;
    while ((int)($n / $divisor) >= 10)
        $divisor *= 10;

    while ($n != 0)
    {
        $leading = (int)($n / $divisor);
        $trailing = $n % 10;

        // If first and last digits are
        // not same then return false
        if ($leading != $trailing)
            return false;

        // Removing the leading and trailing
        // digits from the number
        $n = ($n % $divisor) / 10;

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        $divisor = $divisor / 100;
    }
    return true;
}

// Function to find the largest
// palindromic number
function largestPalindrome($A, $n)
{
    $currentMax = -1;

    for ($i = 0; $i < $n; $i++)
    {

        // If a palindrome larger than
        // the currentMax is found
        if ($A[$i] > $currentMax &&
            isPalindrome($A[$i]))
            $currentMax = $A[$i];
    }

    // Return the largest palindromic
    // number from the array
    return $currentMax;
}

// Driver Code
$A = array(1, 232, 54545, 999991);
$n = sizeof($A);

// print required answer
echo(largestPalindrome($A, $n));

// This code is contributed
// by Mukul Singh
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to check if n is palindrome
function isPalindrome(n)
{

    // Find the appropriate divisor
    // to extract the leading digit
    var divisor = 1;
    while (parseInt(n / divisor) >= 10)
        divisor *= 10;

    while (n != 0)
    {
        var leading = parseInt(n / divisor);
        var trailing = n % 10;

        // If first and last digits are
        // not same then return false
        if (leading != trailing)
            return false;

        // Removing the leading and trailing
        // digits from the number
        n = parseInt((n % divisor) / 10);

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        divisor = parseInt(divisor / 100);
    }
    return true;
}

// Function to find the largest palindromic number
function largestPalindrome(A, n)
{
    var currentMax = -1;

    for(var i = 0; i < n; i++)
    {

        // If a palindrome larger than the
        // currentMax is found
        if (A[i] > currentMax && isPalindrome(A[i]))
            currentMax = A[i];
    }

    // Return the largest palindromic
    // number from the array
    return currentMax;
}

// Driver code
var A = [ 1, 232, 54545, 999991 ];
var n = A.length;

// Print required answer
document.write( largestPalindrome(A, n));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
54545
```
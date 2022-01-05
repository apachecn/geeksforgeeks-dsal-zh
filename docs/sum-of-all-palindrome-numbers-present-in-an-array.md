# 数组中所有回文数字的总和

> 原文:[https://www . geeksforgeeks . org/all-sum-回文-numbers-in-a-array/](https://www.geeksforgeeks.org/sum-of-all-palindrome-numbers-present-in-an-array/)

给定一个正整数的数组 arr[]。任务是找出数组中所有回文数字的和。打印总和。

回文数是反转后等于初始数的数。例:121 是回文(逆序(121) = 121)，123 不是回文(逆序(123) = 321)。

**注**:计算总和时考虑长度大于 1 的回文数。

**示例:**

```
Input : arr[] ={12, 313, 11, 44, 9, 1} 
Output : 368

Input : arr[] = {12, 11, 121}
Output : 132
```

**方法:**思路是实现一个[反转功能，将一个数字](https://www.geeksforgeeks.org/write-a-program-to-reverse-digits-of-a-number/)从右向左反转。实现一个[函数，检查回文数字](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)，最后遍历数组，计算所有回文元素的和。

下面是上述方法的实现:

## C++

```
// C++ program to calculate the sum of all
// palindromic numbers in array
#include<bits/stdc++.h>
using namespace std;

// Function to reverse a number n
int reverse(int n)
{
    int d = 0, s = 0;

    while (n > 0)
    {
        d = n % 10;
        s = s * 10 + d;
        n = n / 10;
    }

    return s;
}

// Function to check if a number n is
// palindrome
bool isPalin(int n)
{
    // If n is equal to the reverse of n
    // it is a palindrome
    return n == reverse(n);
}

// Function to calculate sum of all array
// elements which are palindrome
int sumOfArray(int arr[], int n)
{
    int s = 0;

    for (int i = 0; i < n; i++)
    {
        if ((arr[i] > 10) && isPalin(arr[i]))
        {

            // summation of all palindrome numbers
            // present in array
            s += arr[i];
        }
    }
    return s;
}

// Driver Code
int main()
{
    int n = 6;

    int arr[] = { 12, 313, 11, 44, 9, 1 };

    cout << sumOfArray(arr, n);
    return 0;
}

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the sum of all
// palindromic numbers in array

class GFG {

    // Function to reverse a number n
    static int reverse(int n)
    {
        int d = 0, s = 0;

        while (n > 0) {
            d = n % 10;
            s = s * 10 + d;
            n = n / 10;
        }

        return s;
    }

    // Function to check if a number n is
    // palindrome
    static boolean isPalin(int n)
    {
        // If n is equal to the reverse of n
        // it is a palindrome
        return n == reverse(n);
    }

    // Function to calculate sum of all array
    // elements which are palindrome
    static int sumOfArray(int[] arr, int n)
    {
        int s = 0;

        for (int i = 0; i < n; i++) {
            if ((arr[i] > 10) && isPalin(arr[i])) {

                // summation of all palindrome numbers
                // present in array
                s += arr[i];
            }
        }

        return s;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 6;

        int[] arr = { 12, 313, 11, 44, 9, 1 };

        System.out.println(sumOfArray(arr, n));
    }
}
```

## C#

```
// C# program to calculate the sum of all
// palindromic numbers in array
using System;

class GFG
{

    // Function to reverse a number n
    static int reverse(int n)
    {
        int d = 0, s = 0;

        while (n > 0)
        {
            d = n % 10;
            s = s * 10 + d;
            n = n / 10;
        }

        return s;
    }

    // Function to check if a number n is
    // palindrome
    static bool isPalin(int n)
    {
        // If n is equal to the reverse of n
        // it is a palindrome
        return n == reverse(n);
    }

    // Function to calculate sum of all array
    // elements which are palindrome
    static int sumOfArray(int[] arr, int n)
    {
        int s = 0;

        for (int i = 0; i < n; i++)
        {
            if ((arr[i] > 10) && isPalin(arr[i]))
            {

                // summation of all palindrome numbers
                // present in array
                s += arr[i];
            }
        }

        return s;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 6;

        int[] arr = { 12, 313, 11, 44, 9, 1 };

        Console.WriteLine(sumOfArray(arr, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to calculate the sum of all
# palindromic numbers in array

# Function to reverse a number n
def reverse(n) :

    d = 0; s = 0;

    while (n > 0) :

        d = n % 10;
        s = s * 10 + d;
        n = n // 10;

    return s;

# Function to check if a number n is
# palindrome
def isPalin(n) :

    # If n is equal to the reverse of n
    # it is a palindrome
    return n == reverse(n);

# Function to calculate sum of all array
# elements which are palindrome
def sumOfArray(arr, n) :
    s = 0;

    for i in range(n) :
        if ((arr[i] > 10) and isPalin(arr[i])) :

            # summation of all palindrome numbers
            # present in array
            s += arr[i];

    return s;

# Driver Code
if __name__ == "__main__" :

    n = 6;

    arr = [ 12, 313, 11, 44, 9, 1 ];

    print(sumOfArray(arr, n));

    # This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to calculate the
// sum of all palindromic numbers in array

// Function to reverse a number n
function reverse( n)
{
    let d = 0, s = 0;

    while (n > 0)
    {
        d = n % 10;
        s = s * 10 + d;
        n = Math.floor(n / 10);
    }
    return s;
}

// Function to check if a number n is
// palindrome
function isPalin(n)
{

    // If n is equal to the reverse of n
    // it is a palindrome
    return n == reverse(n);
}

// Function to calculate sum of all array
// elements which are palindrome
function sumOfArray( arr, n)
{
    let s = 0;

    for(let i = 0; i < n; i++)
    {
        if ((arr[i] > 10) && isPalin(arr[i]))
        {

            // Summation of all palindrome
            // numbers present in array
            s += arr[i];
        }
    }
    return s;
}

// Driver Code
let n = 6;
let arr = [ 12, 313, 11, 44, 9, 1 ];

document.write(sumOfArray(arr, n));

// This code is contributed by jana_sayantan

</script>
```

**Output:** 

```
368
```
# 求数组前半部分和后半部分的素数

> 原文:[https://www . geesforgeks . org/find-质数-数组的前半部分和后半部分/](https://www.geeksforgeeks.org/find-prime-numbers-in-the-first-half-and-second-half-of-an-array/)

给定一个大小为 **N** 的数组 **arr** 。任务是找出数组前半部分(直到索引 **N/2** )和后半部分(所有剩余元素)的素数。
**示例:**

> **输入:** arr[] = {2，5，10，15，17，21，23 }
> **输出:** 2 5 和 17 23
> 数组前半部分的素数是 2，5，后半部分是 17，23
> **输入:** arr[] = {31，35，40，43}
> **输出:** 31 和 43

**方法:**
首先遍历数组直到 **N/2** 并检查所有元素是否为质数并打印[质数](https://www.geeksforgeeks.org/prime-numbers/)号。然后遍历数组从 **N/2** 第一个元素到 **N** 找到元素是否为素数，打印所有为素数的元素。
以下是上述方法的实施:

## C++

```
// C++ program to print the prime numbers in the
// first half and second half of an array
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number is prime or not
bool prime(int n)
{
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function to find whether elements are prime or not
void prime_range(int start, int end, int* a)
{
    // Traverse in the given range
    for (int i = start; i < end; i++) {

        // Check if a number is prime or not
        if (prime(a[i]))
            cout << a[i] << " ";
    }
}

// Function to print the prime numbers in the
// first half and second half of an array
void Print(int arr[], int n)
{

    cout << "Prime numbers in the first half are ";
    prime_range(0, n / 2, arr);
    cout << endl;

    cout << "Prime numbers in the second half are ";
    prime_range(n / 2, n, arr);
    cout << endl;
}

// Driver Code
int main()
{

    int arr[] = { 2, 5, 10, 15, 17, 21, 23 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    Print(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the prime numbers in the
// first half and second half of an array
import java.util.*;

class GFG
{

// Function to check if
// a number is prime or not
static boolean prime(int n)
{
    for(int i = 2; i * i <= n; i++)
        if(n % i == 0)
            return false;

    return true;
}

// Function to find whether elements
// are prime or not
static void prime_range(int start,
                        int end, int[] a)
{
    // Traverse in the given range
    for (int i = start; i < end; i++)
    {

        // Check if a number is prime or not
        if(prime(a[i]))
            System.out.print(a[i] + " ");
    }
}

// Function to print the prime numbers in the
// first half and second half of an array
static void Print(int arr[], int n)
{

    System.out.print("Prime numbers in the first half are ");
    prime_range(0, n / 2, arr);
    System.out.println();

    System.out.print("Prime numbers in the second half are ");
    prime_range(n / 2, n, arr);
    System.out.println();
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 5, 10, 15, 17, 21, 23 };

    int n = arr.length;

    // Function call
    Print(arr, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to print the
# prime numbers in the first half
# and second half of an array

# Function to check if
# a number is prime or not
def prime(n):

    for i in range(2, n):
        if i * i > n:
            break
        if(n % i == 0):
            return False;

    return True

# Function to find whether
# elements are prime or not
def prime_range(start, end, a):

    # Traverse in the given range
    for i in range(start, end):

        # Check if a number is prime or not
        if(prime(a[i])):
            print(a[i], end = " ")

# Function to print the
# prime numbers in the first half
# and second half of an array
def Print(arr, n):

    print("Prime numbers in the",
          "first half are ", end = "")
    prime_range(0, n // 2, arr)
    print()

    print("Prime numbers in the",
          "second half are ", end = "")
    prime_range(n // 2, n, arr)
    print()

# Driver Code
arr = [2, 5, 10, 15, 17, 21, 23]

n = len(arr)

# Function call
Print(arr, n)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to print the prime numbers in the
// first half and second half of an array
using System;

class GFG
{

// Function to check if
// a number is prime or not
static Boolean prime(int n)
{
    for(int i = 2; i * i <= n; i++)
        if(n % i == 0)
            return false;

    return true;
}

// Function to find whether elements
// are prime or not
static void prime_range(int start,
                        int end, int[] a)
{
    // Traverse in the given range
    for (int i = start; i < end; i++)
    {

        // Check if a number is prime or not
        if(prime(a[i]))
            Console.Write(a[i] + " ");
    }
}

// Function to print the prime numbers in the
// first half and second half of an array
static void Print(int []arr, int n)
{

    Console.Write("Prime numbers in the first half are ");
    prime_range(0, n / 2, arr);
    Console.WriteLine();

    Console.Write("Prime numbers in the second half are ");
    prime_range(n / 2, n, arr);
    Console.WriteLine();
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 5, 10, 15, 17, 21, 23 };

    int n = arr.Length;

    // Function call
    Print(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to print the prime numbers in the
// first half and second half of an array

// Function to check if a number is prime or not
function prime(n)
{
    for (let i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function to find whether elements are prime or not
function prime_range(start, end, a)
{

    // Traverse in the given range
    for (let i = start; i < end; i++) {

        // Check if a number is prime or not
        if (prime(a[i]))
            document.write(a[i] + " ");
    }
}

// Function to print the prime numbers in the
// first half and second half of an array
function Print(arr, n)
{

    document.write("Prime numbers in the first half are ");
    prime_range(0, parseInt(n / 2), arr);
    document.write("<br>");

    document.write("Prime numbers in the second half are ");
    prime_range(parseInt(n / 2), n, arr);
    document.write("<br>");
}

// Driver Code
let arr = [ 2, 5, 10, 15, 17, 21, 23 ];
let n = arr.length;

// Function call
Print(arr, n);

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
Prime numbers in the first half are 2 5
Prime numbers in the second half are 17 23
```

***时间复杂度:** O(n * sqrt(n))*

***辅助空间:** O(1)*
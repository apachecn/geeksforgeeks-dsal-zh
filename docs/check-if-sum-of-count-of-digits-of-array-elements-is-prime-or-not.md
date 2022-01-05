# 检查数组元素位数之和是否为质数

> 原文:[https://www . geesforgeks . org/check-如果数组元素的位数总和是质数或非质数/](https://www.geeksforgeeks.org/check-if-sum-of-count-of-digits-of-array-elements-is-prime-or-not/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**，任务是检查每个数组元素中的数字的[个数之和是否为](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)[素数](https://www.geeksforgeeks.org/prime-numbers/)。

**示例:**

> **输入:** A[] = {1，11，12}
> **输出:**是
> **说明:**A[0]、A[1]和 A[2]的位数分别为 1、2、2。因此，位数总和= 1 + 2 + 2 = 5，即为素数。
> 
> **输入:** A[] = {1，11，123 }
> T3】输出:否

**方法:**按照以下步骤解决问题:

1.  初始化一个变量 **sum，**存储数组元素位数的和。
2.  [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)和[将每个数组元素转换为它的等价字符串](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)
3.  将每根弦的[长度加到**和**上。](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/)
4.  在完成阵列的[遍历后，检查**和**的值，](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)是否为[质数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。
5.  如果发现为真，打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// a number is prime or not
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // If given number is a
    // multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if sum
// of count of digits of all
// array elements is prime or not
void CheckSumPrime(int A[], int N)
{
    // Initialize sum with 0
    int sum = 0;

    // Traverse over the array
    for (int i = 0; i < N; i++) {

        // Convert array element to string
        string s = to_string(A[i]);

        // Add the count of
        // digits to sum
        sum += s.length();
    }

    // Print the result
    if (isPrime(sum)) {

        cout << "Yes" << endl;
    }
    else {

        cout << "No" << endl;
    }
}

// Drive Code
int main()
{

    int A[] = { 1, 11, 12 };

    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    CheckSumPrime(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check whether
// a number is prime or not
static boolean isPrime(int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // If given number is a
    // multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if sum
// of count of digits of all
// array elements is prime or not
static void CheckSumPrime(int[] A, int N)
{

    // Initialize sum with 0
    int sum = 0;

    // Traverse over the array
    for(int i = 0; i < N; i++)
    {

        // Convert array element to string
        String s = Integer.toString(A[i]);

        // Add the count of
        // digits to sum
        sum += s.length();
    }

    // Print the result
    if (isPrime(sum) == true)
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}

// Drive Code
public static void main(String[] args)
{
    int[] A = { 1, 11, 12 };

    int N = A.length;

    // Function call
    CheckSumPrime(A, N);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check whether
# a number is prime or not
def isPrime(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # If given number is a
    # multiple of 2 or 3
    if (n % 2 == 0 or n % 3 == 0):
        return False

    for i in range(5, int(math.sqrt(n) + 1), 6):
        if (n % i == 0 or n % (i + 2) == 0):
            return False

    return True

# Function to check if sum
# of count of digits of all
# array elements is prime or not
def CheckSumPrime(A, N):

    # Initialize sum with 0
    sum = 0

    # Traverse over the array
    for i in range(0, N):

        # Convert array element to string
        s = str(A[i])

        # Add the count of
        # digits to sum
        sum += len(s)

    # Print the result
    if (isPrime(sum) == True):
        print("Yes")
    else:
        print("No")

# Drive Code
if __name__ == '__main__':

    A = [ 1, 11, 12 ]

    N = len(A)

    # Function call
    CheckSumPrime(A, N)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check whether
// a number is prime or not
static bool isPrime(int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // If given number is a
    // multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if sum
// of count of digits of all
// array elements is prime or not
static void CheckSumPrime(int[] A, int N)
{

    // Initialize sum with 0
    int sum = 0;

    // Traverse over the array
    for(int i = 0; i < N; i++)
    {

        // Convert array element to string
        String s = A[i].ToString();

        // Add the count of
        // digits to sum
        sum += s.Length;
    }

    // Print the result
    if (isPrime(sum) == true)
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}

// Drive Code
public static void Main()
{
    int[] A = { 1, 11, 12 };

    int N = A.Length;

    // Function call
    CheckSumPrime(A, N);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check whether
// a number is prime or not
function isPrime(n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // If given number is a
    // multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (let i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if sum
// of count of digits of all
// array elements is prime or not
function CheckSumPrime(A, N)
{
    // Initialize sum with 0
    let sum = 0;

    // Traverse over the array
    for (let i = 0; i < N; i++) {

        // Convert array element to string
        let s = new String(A[i]);

        // Add the count of
        // digits to sum
        sum += s.length;
    }

    // Print the result
    if (isPrime(sum)) {

        document.write("Yes" + "<br>");
    }
    else {

        document.write("No" + "<br>");
    }
}

// Drive Code
    let A = [ 1, 11, 12 ];

    let N = A.length

    // Function call
    CheckSumPrime(A, N);

    // This code is contributed by gfgking

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>3/2</sup>)*
***辅助空间:** O(1)*
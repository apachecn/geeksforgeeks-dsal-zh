# 最大子阵列的长度，其所有元素都是强数字

> 原文:[https://www . geeksforgeeks . org/最大子阵列长度-其所有元素-强大-数字/](https://www.geeksforgeeks.org/length-of-largest-subarray-whose-all-elements-powerful-number/)

给定一个整数元素的数组 **arr[]** ，任务是找到 **arr[]** 的最大子数组的长度，使得子数组的所有元素都是 [**强子数**](https://www.geeksforgeeks.org/powerful-number/) 。

> 如果一个数 n 的每一个质因数 p，p <sup>2</sup> 也对其进行除法运算，那么这个数 n 就被称为**强数**。

**例:**

> **输入:** arr[] = {1，7，36，4，6，28，4}
> **输出:** 2
> 所有元素为强力数的最大长度子阵为{36，4}
> **输入:** arr[] = {25，100，2，3，9，1}
> **输出:** 2
> 所有元素为强力数的最大长度子阵为{25，100

**接近** :

*   从左到右遍历数组。用 0 初始化一个**最大长度**和**当前长度**变量。
*   如果当前元素是一个[](https://www.geeksforgeeks.org/powerful-number/)**的强大数，那么增加 **current_length** 变量并继续。否则，设置**电流 _ 长度= 0** 。**
*   **在每一步，将最大长度指定为**最大长度=最大(当前长度，最大长度)**。**
*   **最后打印**最大 _ 长度**的值。**

## **C++**

```
// C++ program to find the length of the
// largest sub-array of an array every
// element of whose is a powerful number

#include <bits/stdc++.h>
using namespace std;

// Function to check if the
// number is powerful
bool isPowerful(int n)
{
    // First divide the number repeatedly by 2
    while (n % 2 == 0) {
        int power = 0;
        while (n % 2 == 0) {
            n /= 2;
            power++;
        }

        // If only 2^1 divides n
        // (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // If n is not a power of 2
    // then this loop will execute
    // repeat above process
    for (int factor = 3;
         factor <= sqrt(n);
         factor += 2) {

        // Find highest power of "factor"
        // that divides n
        int power = 0;
        while (n % factor == 0) {
            n = n / factor;
            power++;
        }

        // If only factor^1 divides n
        // (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // n must be 1 now
    // if it is not a prime number.
    // Since prime numbers are not powerful,
    // we return false if n is not 1.
    return (n == 1);
}

// Function to return the length of the
// largest sub-array of an array every
// element of whose is a powerful number
int contiguousPowerfulNumber(int arr[], int n)
{

    int current_length = 0;
    int max_length = 0;

    for (int i = 0; i < n; i++) {

        // If arr[i] is
        // a Powerful number
        if (isPowerful(arr[i]))
            current_length++;
        else
            current_length = 0;

        max_length = max(max_length,
                         current_length);
    }

    return max_length;
}

// Driver code
int main()
{
    int arr[] = { 1, 7, 36, 4, 6, 28, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << contiguousPowerfulNumber(arr, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find the length of the
// largest sub-array of an array every
// element of whose is a powerful number
import java.util.*;

class solution{

// Function to check if the
// number is powerful
static boolean isPowerful(int n)
{
    // First divide the number repeatedly by 2
    while (n % 2 == 0) {
        int power = 0;
        while (n % 2 == 0) {
            n /= 2;
            power++;
        }

        // If only 2^1 divides n
        // (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // If n is not a power of 2
    // then this loop will execute
    // repeat above process
    for (int factor = 3;
        factor <= Math.sqrt(n);
         factor += 2) {

        // Find highest power of "factor"
        // that divides n
        int power = 0;
        while (n % factor == 0) {
            n = n / factor;
            power++;
        }

        // If only factor^1 divides n
        // (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // n must be 1 now
    // if it is not a prime number.
    // Since prime numbers are not powerful,
    // we return false if n is not 1.
    return (n == 1);
}

// Function to return the length of the
// largest sub-array of an array every
// element of whose is a powerful number
static int contiguousPowerfulNumber(int[] arr, int n)
{

    int current_length = 0;
    int max_length = 0;

    for (int i = 0; i < n; i++) {

        // If arr[i] is
        // a Powerful number
        if (isPowerful(arr[i]))
            current_length++;
        else
            current_length = 0;

        max_length = Math.max(max_length,
                        current_length);
    }

    return max_length;
}

// Driver code
public static void main(String args[])
{
    int []arr = { 1, 7, 36, 4, 6, 28, 4 };
    int n = arr.length;

    System.out.println(contiguousPowerfulNumber(arr, n));

}
}

// This code is contributed by Bhupendra_Singh
```

## **蟒蛇 3**

```
# Python 3 program to find the length of
# the largest sub-array of an array every
# element of whose is a powerful number

import math

# function to check if
# the number is powerful
def isPowerful(n):

    # First divide the number repeatedly by 2
    while (n % 2 == 0):

        power = 0
        while (n % 2 == 0):

            n = n//2
            power = power + 1

        # If only 2 ^ 1 divides
        # n (not higher powers),
        # then return false
        if (power == 1):
            return False

    # If n is not a power of 2
    # then this loop will execute
    # repeat above process
    for factor in range(3, int(math.sqrt(n))+1, 2):

        # Find highest power of
        # "factor" that divides n
        power = 0
        while (n % factor == 0):

            n = n//factor
            power = power + 1

        # If only factor ^ 1 divides
        # n (not higher powers),
        # then return false
        if (power == 1):
            return false

     # n must be 1 now if it
     # is not a prime numenr.
     # Since prime numbers are
     # not powerful, we return
     # false if n is not 1.
    return (n == 1)

# Function to return the length of the
# largest sub-array of an array every
# element of whose is a powerful number
def contiguousPowerfulNumber(arr, n):
    current_length = 0
    max_length = 0

    for i in range(0, n, 1):

        # If arr[i] is a
        # Powerful number
        if (isPowerful(arr[i])):
            current_length += 1
        else:
            current_length = 0

        max_length = max(max_length,
                        current_length)

    return max_length

# Driver code
if __name__ == '__main__':
    arr = [1, 7, 36, 4, 6, 28, 4]
    n = len(arr)

    print(contiguousPowerfulNumber(arr, n))
```

## **C#**

```
// C# program to find the length of the
// largest sub-array of an array every
// element of whose is a powerful number
using System;

class solution{

// Function to check if the
// number is powerful
static bool isPowerful(int n)
{

    // First divide the number repeatedly by 2
    while (n % 2 == 0) {
        int power = 0;
        while (n % 2 == 0) {
            n /= 2;
            power++;
        }

        // If only 2^1 divides n
        // (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // If n is not a power of 2
    // then this loop will execute
    // repeat above process
    for (int factor = 3;
             factor <= Math.Sqrt(n);
             factor += 2) {

        // Find highest power of "factor"
        // that divides n
        int power = 0;
        while (n % factor == 0) {
            n = n / factor;
            power++;
        }

        // If only factor^1 divides n
        // (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // n must be 1 now
    // if it is not a prime number.
    // Since prime numbers are not powerful,
    // we return false if n is not 1.
    return (n == 1);
}

// Function to return the length of the
// largest sub-array of an array every
// element of whose is a powerful number
static int contiguousPowerfulNumber(int[] arr, int n)
{
    int current_length = 0;
    int max_length = 0;
    for (int i = 0; i < n; i++) {

        // If arr[i] is
        // a Powerful number
        if (isPowerful(arr[i]))
            current_length++;
        else
            current_length = 0;

        max_length = Math.Max(max_length,
                              current_length);
    }
    return max_length;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 7, 36, 4, 6, 28, 4 };
    int n = arr.Length;
    Console.WriteLine(contiguousPowerfulNumber(arr, n));
}
}

// This code is contributed by gauravrajput1
```

## **java 描述语言**

```
<script>

// Javascript program to find the length of the
// largest sub-array of an array every
// element of whose is a powerful number

// Function to check if the
// number is powerful
function isPowerful(n)
{
    // First divide the number repeatedly by 2
    while (n % 2 == 0) {
        let power = 0;
        while (n % 2 == 0) {
            n /= 2;
            power++;
        }

        // If only 2^1 divides n
        // (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // If n is not a power of 2
    // then this loop will execute
    // repeat above process
    for (let factor = 3;
        factor <= Math.sqrt(n);
         factor += 2) {

        // Find highest power of "factor"
        // that divides n
        let power = 0;
        while (n % factor == 0) {
            n = n / factor;
            power++;
        }

        // If only factor^1 divides n
        // (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // n must be 1 now
    // if it is not a prime number.
    // Since prime numbers are not powerful,
    // we return false if n is not 1.
    return (n == 1);
}

// Function to return the length of the
// largest sub-array of an array every
// element of whose is a powerful number
function contiguousPowerfulNumber(arr, n)
{

    let current_length = 0;
    let max_length = 0;

    for (let i = 0; i < n; i++) {

        // If arr[i] is
        // a Powerful number
        if (isPowerful(arr[i]))
            current_length++;
        else
            current_length = 0;

        max_length = Math.max(max_length,
                        current_length);
    }

    return max_length;
} 

// Driver Code

    let arr = [ 1, 7, 36, 4, 6, 28, 4 ];
    let n = arr.length;

    document.write(contiguousPowerfulNumber(arr, n));

</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:** O(N×√N)*
***辅助空间复杂度:** O(1)***
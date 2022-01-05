# 所有元素都是完全数的最大子阵列的长度

> 原文:[https://www . geeksforgeeks . org/最大子阵列长度-其所有元素都是完美数字/](https://www.geeksforgeeks.org/length-of-largest-subarray-whose-all-elements-are-perfect-number/)

给定整数元素的数组 **arr[]** ，任务是找到 **arr[]** 的最大子数组的长度，使得子数组的所有元素都是 [**完全数**](https://www.geeksforgeeks.org/perfect-number/) 。

> 一个 [**完全数**](https://www.geeksforgeeks.org/perfect-number/) 是一个正整数，等于其[适当因子](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/)之和。

**例:**

> **输入:** arr[] = {1，7，36，4，6，28，4}
> **输出:** 2
> **解释:**
> 以所有元素为完全数的最大长度子阵为{6，28}。
> **输入:** arr[] = {25，100，2，3，9，1}
> **输出:** 0
> **解释:**
> 没有一个数字是完全数

**进场:**

*   [从左到右遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，初始化一个*最大长度*和*当前长度*变量为 0。
*   如果当前元素是一个完全数，那么增加 current_length 变量并继续这个过程。否则，将 current_length 设置为 0。
*   在每一步，将最大长度指定为**最大长度=最大(当前长度，最大长度)**。
*   最后打印 max_length 的值，因为它将存储所需的结果。

以下是上述方法的实现:

## C++

```
// C++ program to find the length of the
// largest sub-array of an array every
// element of whose is a perfect number

#include <bits/stdc++.h>
using namespace std;

// Function that returns true if n is perfect
bool isPerfect(long long int n)
{
    // Variable to store sum of divisors
    long long int sum = 1;

    // Find all divisors and add them
    for (long long int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            if (i * i != n)
                sum = sum + i + n / i;
            else
                sum = sum + i;
        }
    }
    // Check if sum of divisors is equal to
    // n, then n is a perfect number
    if (sum == n && n != 1)
        return true;

    return false;
}

// Function to return the length of the
// largest sub-array of an array every
// element of whose is a perfect number
int contiguousPerfectNumber(int arr[], int n)
{

    int current_length = 0;
    int max_length = 0;

    for (int i = 0; i < n; i++) {

        // Check if arr[i] is a perfect number
        if (isPerfect(arr[i]))
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

    cout << contiguousPerfectNumber(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of the
// largest sub-array of an array every
// element of whose is a perfect number

import java.util.*;    

class GFG
{
    // Function that returns true if n is perfect
    static boolean isPerfect(int n)
    {
        // Variable to store sum of divisors
        int sum = 1;
        int i;

        // Find all divisors and add them
        for ( i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                if (i * i != n)
                    sum = sum + i + n / i;
                else
                    sum = sum + i;
            }
        }

        // Check if sum of divisors is equal to
        // n, then n is a perfect number
        if (sum == n && n != 1)
            return true;

        return false;
    }

    // Function to return the length of the
    // largest sub-array of an array every
    // element of whose is a perfect number
    static int contiguousPerfectNumber(int arr[], int n)
    {

        int current_length = 0;
        int max_length = 0;
        int i;
        for (i = 0; i < n; i++) {

            // Check if arr[i] is a perfect number
            if (isPerfect(arr[i]))
                current_length++;
            else
                current_length = 0;

            max_length = Math.max(max_length,
                            current_length);
        }

        return max_length;
    }

    // Driver code
    public static void main(String []args)
    {
        int arr[] = { 1, 7, 36, 4, 6, 28, 4 };
        int n = arr.length;

        System.out.print(contiguousPerfectNumber(arr, n));

    }
}

//This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python 3 program to find the length of
# the largest sub-array of an array every
# element of whose is a perfect number

# Function that returns true if n is perfect
def isPerfect( n ):

    # To store sum of divisors
    sum = 1

    # Find all divisors and add them
    i = 2
    while i * i <= n:
        if n % i == 0:
            sum = sum + i + n / i
        i += 1

    # check if the sum of divisors is equal to
    # n, then n is a perfect number

    return (True if sum == n and n != 1 else False)

# Function to return the length of the
# largest sub-array of an array every
# element of whose is a perfect number
def contiguousPerfectNumber(arr, n):
    current_length = 0
    max_length = 0

    for i in range(0, n, 1):

        # check if arr[i] is a perfect number
        if (isPerfect(arr[i])):
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

    print(contiguousPerfectNumber(arr, n))
```

## C#

```
// C# program to find the length of the
// largest sub-array of an array every
// element of whose is a perfect number
using System;

class GFG{

// Function that returns true if n is perfect
static bool isPerfect(int n)
{

    // Variable to store sum of divisors
    int sum = 1;
    int i;

    // Find all divisors and add them
    for(i = 2; i * i <= n; i++)
    {
       if (n % i == 0)
       {
           if (i * i != n)
               sum = sum + i + n / i;
           else
               sum = sum + i;
       }
    }

    // Check if sum of divisors is equal to
    // n, then n is a perfect number
    if (sum == n && n != 1)
    {
        return true;
    }
    return false;
}

// Function to return the length of the
// largest sub-array of an array every
// element of whose is a perfect number
static int contiguousPerfectNumber(int []arr,
                                   int n)
{
    int current_length = 0;
    int max_length = 0;
    int i;
    for(i = 0; i < n; i++)
    {

       // Check if arr[i] is a perfect number
       if (isPerfect(arr[i]))
       {
           current_length++;
       }
       else
       {
           current_length = 0;
       }
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

    Console.Write(contiguousPerfectNumber(arr, n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find the length of the
// largest sub-array of an array every
// element of whose is a perfect number

    // Function that returns true if n is perfect
    function isPerfect(n)
    {
        // Variable to store sum of divisors
        let sum = 1;
        let i;

        // Find all divisors and add them
        for ( i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                if (i * i != n)
                    sum = sum + i + n / i;
                else
                    sum = sum + i;
            }
        }

        // Check if sum of divisors is equal to
        // n, then n is a perfect number
        if (sum == n && n != 1)
            return true;

        return false;
    }

    // Function to return the length of the
    // largest sub-array of an array every
    // element of whose is a perfect number
    function contiguousPerfectNumber(arr, n)
    {

        let current_length = 0;
        let max_length = 0;
        let i;
        for (i = 0; i < n; i++) {

            // Check if arr[i] is a perfect number
            if (isPerfect(arr[i]))
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

    document.write(contiguousPerfectNumber(arr, n));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N×√N)*
***辅助空间复杂度:** O(1)*
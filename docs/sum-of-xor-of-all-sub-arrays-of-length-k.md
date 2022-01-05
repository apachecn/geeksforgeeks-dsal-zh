# 长度为 K 的所有子阵列的异或之和

> 原文:[https://www . geeksforgeeks . org/长度为 k 的所有子数组的异或之和/](https://www.geeksforgeeks.org/sum-of-xor-of-all-sub-arrays-of-length-k/)

给定一个长度为 n ( n > k)的数组，我们必须求出长度为 k 的子数组中所有元素的异或和。
**例:**

> **输入:** arr[]={1，2，3，4}，k=2
> **输出:**sum = 11
> sum = 1^2+2^3+3^4 = 3+1+7 = 11
> **输入:** arr[]={1，2，3，4}，k=3
> **输出:**sum = 5
> sum = 1^2^3+2^3^4 = 0+5 = 5

**天真解:**思路是遍历所有长度为 K 的子阵，求子阵所有元素的 xor 并求和，求一个阵列所有 K 长度子阵的 XOR 之和。
*时间复杂度* : O(N <sup>2</sup> )
**高效解:**高效解是遍历数组，找到长度为 k 的所有子数组，即(0 到 k-1)，(1 到 k)，(2 到 k+1)，…。，(n-k+1 至 n)。
我们将通过形成一个预 xor 数组，找到并存储从 0 到 I 的元素的 xor(在数组 x[])。
现在，子数组从 l 到 r 的 xor 等于 x[l-1] ^ x[r],因为 x[r]将给出所有元素的 xor 直到 r，x[l-1]将给出所有元素的 xor 直到 l-1。当我们将这两个值进行异或运算时，直到 0 到 l-1 的元素将被重复。当 a^a = 0 时，重复的值对净值的贡献为零，我们得到从 l 到 r 的 xor 子阵列的值。
下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <iostream>
using namespace std;

// Sum of XOR of all K length
// sub-array of an array
int FindXorSum(int arr[], int k, int n)
{
    // If the length of the array is less than k
    if (n < k)
        return 0;

    // Array that will store xor values of
    // subarray from 1 to i
    int x[n] = { 0 };
    int result = 0;

    // Traverse through the array
    for (int i = 0; i < n; i++) {

        // If i is greater than zero, store
        // xor of all the elements from 0 to i
        if (i > 0)
            x[i] = x[i - 1] ^ arr[i];

        // If it is the first element
        else
            x[i] = arr[i];

        // If i is greater than k
        if (i >= k - 1) {
            int sum = 0;

            // Xor of values from 0 to i
            sum = x[i];

            // Now to find subarray of length k
            // that ends at i, xor sum with x[i-k]
            if (i - k > -1)
                sum ^= x[i - k];

            // Add the xor of elements from i-k+1 to i
            result += sum;
        }
    }

    // Return the resultant sum;
    return result;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4 };

    int n = 4, k = 2;

    cout << FindXorSum(arr, k, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Sum of XOR of all K length
// sub-array of an array
static int FindXorSum(int arr[], int k, int n)
{
    // If the length of the array is less than k
    if (n < k)
        return 0;

    // Array that will store xor values of
    // subarray from 1 to i
    int []x = new int[n];
    int result = 0;

    // Traverse through the array
    for (int i = 0; i < n; i++)
    {

        // If i is greater than zero, store
        // xor of all the elements from 0 to i
        if (i > 0)
            x[i] = x[i - 1] ^ arr[i];

        // If it is the first element
        else
            x[i] = arr[i];

        // If i is greater than k
        if (i >= k - 1)
        {
            int sum = 0;

            // Xor of values from 0 to i
            sum = x[i];

            // Now to find subarray of length k
            // that ends at i, xor sum with x[i-k]
            if (i - k > -1)
                sum ^= x[i - k];

            // Add the xor of elements from i-k+1 to i
            result += sum;
        }
    }

    // Return the resultant sum;
    return result;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4 };

    int n = 4, k = 2;

    System.out.println(FindXorSum(arr, k, n));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of above approach

# Sum of XOR of all K length
# sub-array of an array
def FindXorSum(arr, k, n):

    # If the length of the array is less than k
    if (n < k):
        return 0;

    # Array that will store xor values of
    # subarray from 1 to i
    x = [0]*n;
    result = 0;

    # Traverse through the array
    for i in range(n):

        # If i is greater than zero, store
        # xor of all the elements from 0 to i
        if (i > 0):
            x[i] = x[i - 1] ^ arr[i];

        # If it is the first element
        else:
            x[i] = arr[i];

        # If i is greater than k
        if (i >= k - 1):
            sum = 0;

            # Xor of values from 0 to i
            sum = x[i];

            # Now to find subarray of length k
            # that ends at i, xor sum with x[i-k]
            if (i - k > -1):
                sum ^= x[i - k];

            # Add the xor of elements from i-k+1 to i
            result += sum;

    # Return the resultant sum;
    return result;

# Driver code
arr = [ 1, 2, 3, 4 ];

n = 4; k = 2;

print(FindXorSum(arr, k, n));

# This code has been contributed by 29AjayKumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Sum of XOR of all K length
    // sub-array of an array
    static int FindXorSum(int []arr, int k, int n)
    {
        // If the length of the array is less than k
        if (n < k)
            return 0;

        // Array that will store xor values of
        // subarray from 1 to i
        int []x = new int[n];
        int result = 0;

        // Traverse through the array
        for (int i = 0; i < n; i++)
        {

            // If i is greater than zero, store
            // xor of all the elements from 0 to i
            if (i > 0)
                x[i] = x[i - 1] ^ arr[i];

            // If it is the first element
            else
                x[i] = arr[i];

            // If i is greater than k
            if (i >= k - 1)
            {
                int sum = 0;

                // Xor of values from 0 to i
                sum = x[i];

                // Now to find subarray of length k
                // that ends at i, xor sum with x[i-k]
                if (i - k > -1)
                    sum ^= x[i - k];

                // Add the xor of elements from i-k+1 to i
                result += sum;
            }
        }

        // Return the resultant sum;
        return result;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 3, 4 };

        int n = 4, k = 2;

        Console.WriteLine(FindXorSum(arr, k, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Sum of XOR of all K length
// sub-array of an array
function FindXorSum(arr, k, n)
{
    // If the length of the array is less than k
    if (n < k)
        return 0;

    // Array that will store xor values of
    // subarray from 1 to i
    let x = new Array(n).fill(0);
    let result = 0;

    // Traverse through the array
    for (let i = 0; i < n; i++) {

        // If i is greater than zero, store
        // xor of all the elements from 0 to i
        if (i > 0)
            x[i] = x[i - 1] ^ arr[i];

        // If it is the first element
        else
            x[i] = arr[i];

        // If i is greater than k
        if (i >= k - 1) {
            let sum = 0;

            // Xor of values from 0 to i
            sum = x[i];

            // Now to find subarray of length k
            // that ends at i, xor sum with x[i-k]
            if (i - k > -1)
                sum ^= x[i - k];

            // Add the xor of elements from i-k+1 to i
            result += sum;
        }
    }

    // Return the resultant sum;
    return result;
}

// Driver code
    let arr = [ 1, 2, 3, 4 ];

    let n = 4, k = 2;

    document.write(FindXorSum(arr, k, n));

</script>
```

**Output:** 

```
11
```

**时间复杂度** : O(N)
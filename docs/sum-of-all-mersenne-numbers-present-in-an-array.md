# 数组中所有梅森数的总和

> 原文:[https://www . geesforgeks . org/sum-all-mersenne-numbers-in-a-array/](https://www.geeksforgeeks.org/sum-of-all-mersenne-numbers-present-in-an-array/)

给定一个整数数组 **arr[]** ，任务是从数组中找出所有梅森数的和。如果一个数大于 0，并且比 2 的某个幂小 1，则该数是梅森数。前几个梅森数字是 **1，3，7，15，31，63，127，…**

**示例:**

> **输入:** arr[] = {17，6，7，63，3}
> **输出:** 73
> 只有 7，63 和 3 是梅森数，即 7 + 63 + 3 = 73
> 
> **输入:** arr[] = {1，3，11，45}
> 输出: 4

**方法:**初始化 **sum = 0** 并开始遍历数组的所有元素，如果当前元素比 2 的某个幂小 1 且大于 0，则更新 **sum = sum + arr[i]** 。最后打印**和**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns true
// if n is a Mersenne number
int isMersenne(int n)
{
    while (n != 0)
    {
        int r = n % 2;
        if (r == 0)
            return false;
        n /= 2;
    }
    return true;
}

// Function to return the sum of all the
// Mersenne numbers from the given array
int sumOfMersenne(int arr[], int n)
{

    // To store the required sum
    int sum = 0;
    for (int i = 0; i < n; i++)
    {

        // If current element is a Mersenne number
        if (arr[i] > 0 && isMersenne(arr[i]))
        {
            sum += arr[i];
        }
    }
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 17, 6, 7, 63, 3 };
    int n = sizeof(arr) / sizeof(int);
    cout << (sumOfMersenne(arr, n));
    return 0;
}

// This code is contributed by jit_t
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that returns true
    // if n is a Mersenne number
    static boolean isMersenne(int n)
    {
        while (n != 0) {
            int r = n % 2;
            if (r == 0)
                return false;
            n /= 2;
        }
        return true;
    }

    // Function to return the sum of all the
    // Mersenne numbers from the given array
    static int sumOfMersenne(int[] arr, int n)
    {

        // To store the required sum
        int sum = 0;
        for (int i = 0; i < n; i++) {

            // If current element is a Mersenne number
            if (arr[i] > 0 && isMersenne(arr[i])) {
                sum += arr[i];
            }
        }
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 17, 6, 7, 63, 3 };
        int n = arr.length;
        System.out.print(sumOfMersenne(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true
# if n is a Mersenne number
def isMersenne(n) :
    while (n != 0) :
        r = n % 2;
        if (r == 0) :
            return False;
        n //= 2;

    return True;

# Function to return the sum of all the
# Mersenne numbers from the given array
def sumOfMersenne(arr, n) :
    # To store the required sum
    sum = 0;
    for i in range(n) :

        # If current element is a Mersenne number
        if (arr[i] > 0 and isMersenne(arr[i])) :
            sum += arr[i];

    return sum;

# Driver code
if __name__ == "__main__" :

    arr = [17, 6, 7, 63, 3 ];
    n = len(arr);
    print(sumOfMersenne(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
//C# implementation of the approach
using System;

class GFG
{
    // Function that returns true
    // if n is a Mersenne number
    static bool isMersenne(int n)
    {
        while (n != 0)
        {
            int r = n % 2;
            if (r == 0)
                return false;
            n /= 2;
        }
        return true;
    }

    // Function to return the sum of all the
    // Mersenne numbers from the given array
    static int sumOfMersenne(int[] arr, int n)
    {

        // To store the required sum
        int sum = 0;
        for (int i = 0; i < n; i++)
        {

            // If current element is a Mersenne number
            if (arr[i] > 0 && isMersenne(arr[i]))
            {
                sum += arr[i];
            }
        }
        return sum;
    }

    // Driver code
    static public void Main ()
    {
        int[] arr = { 17, 6, 7, 63, 3 };
        int n = arr.Length;
        Console.WriteLine(sumOfMersenne(arr, n));
    }
}

// This code is contributed by jit_t
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true
// if n is a Mersenne number
function isMersenne( n)
{
    while (n != 0)
    {
        let r = n % 2;
        if (r == 0)
            return false;

        n = Math.floor(n / 2);
    }
    return true;
}

// Function to return the sum of all the
// Mersenne numbers from the given array
function sumOfMersenne(arr, n)
{

    // To store the required sum
    let sum = 0;
    for(let i = 0; i < n; i++)
    {

        // If current element is a Mersenne number
        if (arr[i] > 0 && isMersenne(arr[i]))
        {
            sum += arr[i];
        }
    }
    return sum;
}

// Driver Code
let arr = [ 17, 6, 7, 63, 3 ];
let n = arr.length;

document.write(sumOfMersenne(arr, n));

// This code is contributed by jana_sayantan

</script>
```

**Output:** 

```
73
```
# 给定数组中素数位置的 0 和 1 的个数

> 原文:[https://www . geesforgeks . org/给定数组中素数为 0 和 1 的个数/](https://www.geeksforgeeks.org/number-of-0s-and-1s-at-prime-positions-in-the-given-array/)

给定一个大小为 **N** 的数组 **arr[]** ，其中每个元素要么是 **0** 要么是 **1** 。任务是找出位于质数索引处的 0 和 1 的计数。

**示例:**

> **输入:** arr[] = {1，0，1，0，1}
> **输出:**
> 0 的个数= 1
> 1 的个数= 1
> 
> **输入:** arr[] = {1，0，1，1}
> **输出:**
> 0 的个数= 0
> 1 的个数= 2

**方法:**遍历数组，如果当前索引是质数，则每遇到一个 0，就更新 0 的计数，并更新所有处于质数索引的 1 的计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function that returns true
// if n is prime
bool isPrime(int n)
{
    if (n <= 1)
        return false;

    // Check from 2 to n
    for(int i = 2; i < n; i++)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Function to find the count
// of 0s and 1s at prime indices
void countPrimePosition(int arr[], int n)
{

    // To store the count of 0s and 1s
    int c0 = 0, c1 = 0;
    for(int i = 0; i < n; i++)
    {

        // If current 0 is at
        // prime position
        if (arr[i] == 0 && isPrime(i))
            c0++;

        // If current 1 is at
        // prime position
        if (arr[i] == 1 && isPrime(i))
            c1++;
    }
    cout << "Number of 0s = " << c0 << endl;
    cout << "Number of 1s = " << c1;
}

// Driver code
int main()
{
    int arr[] = { 1, 0, 1, 0, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    countPrimePosition(arr, n);
    return 0;
}

// This code is contributed by noob2000
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that returns true
    // if n is prime
    static boolean isPrime(int n)
    {
        if (n <= 1)
            return false;

        // Check from 2 to n
        for (int i = 2; i < n; i++) {
            if (n % i == 0)
                return false;
        }
        return true;
    }

    // Function to find the count
    // of 0s and 1s at prime indices
    static void countPrimePosition(int arr[])
    {

        // To store the count of 0s and 1s
        int c0 = 0, c1 = 0;
        int n = arr.length;
        for (int i = 0; i < n; i++) {

            // If current 0 is at
            // prime position
            if (arr[i] == 0 && isPrime(i))
                c0++;

            // If current 1 is at
            // prime position
            if (arr[i] == 1 && isPrime(i))
                c1++;
        }
        System.out.println("Number of 0s = " + c0);
        System.out.println("Number of 1s = " + c1);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 1, 0, 1, 0, 1 };
        countPrimePosition(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true
# if n is prime
def isPrime(n) :

    if (n <= 1) :
        return False;

    # Check from 2 to n
    for i in range(2, n) :
        if (n % i == 0) :
            return False;

    return True;

# Function to find the count
# of 0s and 1s at prime indices
def countPrimePosition(arr) :

    # To store the count of 0s and 1s
    c0 = 0; c1 = 0;
    n = len(arr);

    for i in range(n) :

        # If current 0 is at
        # prime position
        if (arr[i] == 0 and isPrime(i)) :
            c0 += 1;

        # If current 1 is at
        # prime position
        if (arr[i] == 1 and isPrime(i)) :
            c1 += 1;

    print("Number of 0s =", c0);
    print("Number of 1s =", c1);

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 0, 1, 0, 1 ];
    countPrimePosition(arr);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true
    // if n is prime
    static bool isPrime(int n)
    {
        if (n <= 1)
            return false;

        // Check from 2 to n
        for (int i = 2; i < n; i++)
        {
            if ((n % i) == 0)
                return false;
        }
        return true;
    }

    // Function to find the count
    // of 0s and 1s at prime indices
    static void countPrimePosition(int []arr)
    {

        // To store the count of 0s and 1s
        int c0 = 0, c1 = 0;
        int n = arr.Length;
        for (int i = 0; i < n; i++)
        {

            // If current 0 is at
            // prime position
            if ((arr[i] == 0) && (isPrime(i)))
                c0++;

            // If current 1 is at
            // prime position
            if ((arr[i] == 1) && (isPrime(i)))
                c1++;
        }
        Console.WriteLine("Number of 0s = " + c0);
        Console.WriteLine("Number of 1s = " + c1);
    }

    // Driver code
    static public void Main ()
    {

        int[] arr = { 1, 0, 1, 0, 1 };
        countPrimePosition(arr);
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns true
// if n is prime
function isPrime(n) {
    if (n <= 1)
        return false;

    // Check from 2 to n
    for (let i = 2; i < n; i++) {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Function to find the count
// of 0s and 1s at prime indices
function countPrimePosition(arr, n) {

    // To store the count of 0s and 1s
    let c0 = 0, c1 = 0;

    for (let i = 0; i < n; i++) {

        // If current 0 is at
        // prime position
        if (arr[i] == 0 && isPrime(i))
            c0++;

        // If current 1 is at
        // prime position
        if (arr[i] == 1 && isPrime(i))
            c1++;
    }
    document.write("Number of 0s = " + c0 + "<br>");
    document.write("Number of 1s = " + c1);
}

// Driver code
let arr = [1, 0, 1, 0, 1];

let n = arr.length;
countPrimePosition(arr, n);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
Number of 0s = 1
Number of 1s = 1
```

时间复杂度:O(n <sup>2</sup> )

辅助空间:0(1)
# 满足给定条件的给定数组中的对的绝对差之和

> 原文:[https://www . geesforgeks . org/满足给定条件的给定数组对的绝对差之和/](https://www.geeksforgeeks.org/sum-of-absolute-differences-of-pairs-from-the-given-array-that-satisfy-the-given-condition/)

给定一个由 **N** 元素组成的数组 **arr[]** ，任务是找出所有对 **(arr[i]，arr[j])** 之间的绝对差之和，使得 **i < j** 和**(j–I)为** [**质数**](https://www.geeksforgeeks.org/prime-numbers/) 。
**例:**

> **输入:** arr[] = {1，2，3，5，7，12}
> **输出:** 45
> 所有有效指数对为:
> (5，0)—>ABS(12–1)= 11
> (3，0)—>ABS(5–1)= 4
> (2，0)—>ABS(3–1)= 2
> (4，1)—>ABS(7–7) 2)->ABS(12–3)= 9
> (4，2)->ABS(7–3)= 4
> (5，3)->ABS(12–5)= 7
> 11+4+2+5+3+9+4+7 = 45
> **输入:** arr[] = {2，5，6，7}
> **输出:** 11

**方法:**初始化 **sum = 0** 并运行两个嵌套循环，对于每对 **arr[i]，arr[j]** 为**(j–I)**为素数，然后将 sum 更新为 sum = sum + abs(arr[i]，arr[j])。最后打印**总和**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns true
// if n is prime
bool isPrime(int n)
{

    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to n-1
    for (int i = 2; i < n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function to return the absolute
// differences of the pairs which
// satisfy the given condition
int findSum(int arr[], int n)
{

    // To store the required sum
    int sum = 0;

    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++)

            // If difference between the indices
            // is prime
            if (isPrime(j - i)) {

                // Update the sum with the absolute
                // difference of the pair elements
                sum = sum + abs(arr[i] - arr[j]);
            }
    }

    // Return the sum
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 5, 7, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function that returns true
    // if n is prime
    static boolean isPrime(int n)
    {

        // Corner case
        if (n <= 1)
        {
            return false;
        }

        // Check from 2 to n-1
        for (int i = 2; i < n; i++)
        {
            if (n % i == 0)
            {
                return false;
            }
        }
        return true;
    }

    // Function to return the absolute
    // differences of the pairs which
    // satisfy the given condition
    static int findSum(int arr[], int n)
    {

        // To store the required sum
        int sum = 0;

        for (int i = 0; i < n - 1; i++)
        {
            // If difference between the indices is prime
            for (int j = i + 1; j < n; j++)
            {
                if (isPrime(j - i))
                {

                    // Update the sum with the absolute
                    // difference of the pair elements
                    sum = sum + Math.abs(arr[i] - arr[j]);
                }
            }
        }

        // Return the sum
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 3, 5, 7, 12};
        int n = arr.length;

        System.out.println(findSum(arr, n));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true
# if n is prime
def isPrime(n) :

    # Corner case
    if (n <= 1) :
        return False;

    # Check from 2 to n-1
    for i in range(2, n) :
        if (n % i == 0) :
            return False;

    return True;

# Function to return the absolute
# differences of the pairs which
# satisfy the given condition
def findSum(arr, n) :

    # To store the required sum
    sum = 0;

    for i in range(n - 1) :
        for j in range(i + 1, n) :

            # If difference between the indices
            # is prime
            if (isPrime(j - i)) :

                # Update the sum with the absolute
                # difference of the pair elements
                sum = sum + abs(arr[i] - arr[j]);

    # Return the sum
    return sum;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 5, 7, 12 ];
    n = len(arr);

    print(findSum(arr, n));

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

        // Corner case
        if (n <= 1)
        {
            return false;
        }

        // Check from 2 to n-1
        for (int i = 2; i < n; i++)
        {
            if (n % i == 0)
            {
                return false;
            }
        }
        return true;
    }

    // Function to return the absolute
    // differences of the pairs which
    // satisfy the given condition
    static int findSum(int []arr, int n)
    {

        // To store the required sum
        int sum = 0;

        for (int i = 0; i < n - 1; i++)
        {
            // If difference between the indices is prime
            for (int j = i + 1; j < n; j++)
            {
                if (isPrime(j - i))
                {

                    // Update the sum with the absolute
                    // difference of the pair elements
                    sum = sum + Math.Abs(arr[i] - arr[j]);
                }
            }
        }

        // Return the sum
        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {1, 2, 3, 5, 7, 12};
        int n = arr.Length;

        Console.WriteLine(findSum(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JS implementation of the approach

// Function that returns true
// if n is prime
function isPrime(n)
{

    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to n-1
    for (let i = 2; i < n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function to return the absolute
// differences of the pairs which
// satisfy the given condition
function findSum( arr, n)
{

    // To store the required sum
    let sum = 0;

    for (let i = 0; i < n - 1; i++) {
        for (let j = i + 1; j < n; j++)

            // If difference between the indices
            // is prime
            if (isPrime(j - i)) {

                // Update the sum with the absolute
                // difference of the pair elements
                sum = sum + Math.abs(arr[i] - arr[j]);
            }
    }

    // Return the sum
    return sum;
}

// Driver code
let arr = [ 1, 2, 3, 5, 7, 12 ];
let n = arr.length;
document.write(findSum(arr, n));
</script>
```

**Output**

```
45
```

**时间复杂度** : O(N <sup>3</sup>

**辅助空间:** O(1)
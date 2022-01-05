# 数组中所有完全数的总和

> 原文:[https://www . geesforgeks . org/所有完全数之和-数组中出现/](https://www.geeksforgeeks.org/sum-of-all-perfect-numbers-present-in-an-array/)

给定一个包含正整数 **N** 的数组 **arr[]** 。任务是从数组中找出所有完全数的和。
如果一个数等于它的适当除数之和，即除去数本身的正除数之和，那么这个数就是完美的。

**示例:**

> **输入:** arr[] = {3，6，9}
> **输出:**6
> 3 = 1 的适当除数和
> 6 = 1+2+3 = 6 的适当除数和
> 9 = 1+3 = 4 的适当除数和
> **输入:** arr[] = {17，6，10，6，4}
> **输出:** 12

**方法:**初始化**和= 0** 对于数组的每个元素，找到其适当因子的和，比如**和因子**。如果 **arr[i] = sumFactors** ，则更新结果总和为**总和=总和+ arr[i]** 。最后打印**总和**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to return the sum of
// all the proper factors of n
int sumOfFactors(int n)
{
    int sum = 0;
    for (int f = 1; f <= n / 2; f++)
    {

        // f is the factor of n
        if (n % f == 0)
        {
            sum += f;
        }
    }
    return sum;
}

// Function to return the required sum
int getSum(int arr[], int n)
{

    // To store the sum
    int sum = 0;
    for (int i = 0; i < n; i++)
    {

        // If current element is non-zero and equal
        // to the sum of proper factors of itself
        if (arr[i] > 0 &&
            arr[i] == sumOfFactors(arr[i]))
        {
            sum += arr[i];
        }
    }
    return sum;
}

// Driver code
int main()
{
    int arr[10] = { 17, 6, 10, 6, 4 };

    int n = sizeof(arr) / sizeof(arr[0]);
    cout << (getSum(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {

    // Function to return the sum of
    // all the proper factors of n
    static int sumOfFactors(int n)
    {
        int sum = 0;
        for (int f = 1; f <= n / 2; f++) {

            // f is the factor of n
            if (n % f == 0) {
                sum += f;
            }
        }
        return sum;
    }

    // Function to return the required sum
    static int getSum(int[] arr, int n)
    {

        // To store the sum
        int sum = 0;
        for (int i = 0; i < n; i++) {

            // If current element is non-zero and equal
            // to the sum of proper factors of itself
            if (arr[i] > 0 && arr[i] == sumOfFactors(arr[i])) {
                sum += arr[i];
            }
        }
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 17, 6, 10, 6, 4 };
        int n = arr.length;
        System.out.print(getSum(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the sum of
# all the proper factors of n
def sumOfFactors(n):

    sum = 0
    for f in range(1, n // 2 + 1):

        # f is the factor of n
        if (n % f == 0):
            sum += f

    return sum

# Function to return the required sum
def getSum(arr, n):

    # To store the sum
    sum = 0
    for i in range(n):

        # If current element is non-zero and equal
        # to the sum of proper factors of itself
        if (arr[i] > 0 and
            arr[i] == sumOfFactors(arr[i])) :
            sum += arr[i]

    return sum

# Driver code
arr = [17, 6, 10, 6, 4]

n = len(arr)
print(getSum(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the sum of
    // all the proper factors of n
    static int sumOfFactors(int n)
    {
        int sum = 0;
        for (int f = 1; f <= n / 2; f++)
        {

            // f is the factor of n
            if (n % f == 0)
            {
                sum += f;
            }
        }
        return sum;
    }

    // Function to return the required sum
    static int getSum(int[] arr, int n)
    {

        // To store the sum
        int sum = 0;
        for (int i = 0; i < n; i++)
        {

            // If current element is non-zero and equal
            // to the sum of proper factors of itself
            if (arr[i] > 0 && arr[i] == sumOfFactors(arr[i]))
            {
                sum += arr[i];
            }
        }
        return sum;
    }

    // Driver code
    static public void Main ()
    {
        int[] arr = { 17, 6, 10, 6, 4 };
        int n = arr.Length;
        Console.WriteLine(getSum(arr, n));
    }
}

// This code is contributed by @ajit_0023
```

## java 描述语言

```
<script>
// Java  script implementation of the above approach

    // Function to return the sum of
    // all the proper factors of n
    function sumOfFactors( n)
    {
        let sum = 0;
        for (let f = 1; f <= n / 2; f++) {

            // f is the factor of n
            if (n % f == 0) {
                sum += f;
            }
        }
        return sum;
    }

    // Function to return the required sum
    function getSum( arr,  n)
    {

        // To store the sum
        let sum = 0;
        for (let i = 0; i < n; i++) {

            // If current element is non-zero and equal
            // to the sum of proper factors of itself
            if (arr[i] > 0 && arr[i] == sumOfFactors(arr[i])) {
                sum += arr[i];
            }
        }
        return sum;
    }

    // Driver code
        let arr = [ 17, 6, 10, 6, 4 ];
        let  n = arr.length;
        document.write(getSum(arr, n));

//contributed by bobby

</script>
```

**Output:** 

```
12
```
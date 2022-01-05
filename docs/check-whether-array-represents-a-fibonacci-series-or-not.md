# 检查数组是否代表斐波那契数列

> 原文:[https://www . geesforgeks . org/check-array-是否表示-a-fibonacci-series-or-not/](https://www.geeksforgeeks.org/check-whether-array-represents-a-fibonacci-series-or-not/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是检查是否可以使用所有数组元素形成一个 [**斐波那契数列**](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/) 。如果可能，打印“是”。否则，打印“否”。
**举例:**

> **输入:** arr[] = { 8，3，5，13 }
> **输出:**是
> **解释:**
> 将给定数组重新排列为{3，5，8，13 }，这些数字组成斐波那契数列。
> **输入:** arr[] = { 2，3，5，11 }
> **输出:**否
> **说明:**
> 给定的数组元素不构成斐波那契数列。

**进场:**
为了解决上述问题，主要思路是 [**排序**](https://www.geeksforgeeks.org/sort-c-stl/) 给定阵。排序后，检查每个元素是否等于前两个元素的总和。如果是这样，那么数组元素就形成了斐波那契数列。
以下是上述方法的实施:

## C++

```
// C++ program to check if the
// elements of a given array
// can form a Fibonacci Series

#include <bits/stdc++.h>
using namespace std;

// Returns true if a permutation
// of arr[0..n-1] can form a
// Fibonacci Series
bool checkIsFibonacci(int arr[], int n)
{
    if (n == 1 || n == 2)
        return true;

    // Sort array
    sort(arr, arr + n);

    // After sorting, check if every
    // element is equal to the
    // sum of previous 2 elements

    for (int i = 2; i < n; i++)
        if ((arr[i - 1] + arr[i - 2])
            != arr[i])
            return false;

    return true;
}

// Driver Code
int main()
{
    int arr[] = { 8, 3, 5, 13 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (checkIsFibonacci(arr, n))
        cout << "Yes" << endl;
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the elements of
// a given array can form a Fibonacci Series
import java. util. Arrays;

class GFG{

// Returns true if a permutation
// of arr[0..n-1] can form a
// Fibonacci Series
public static boolean checkIsFibonacci(int arr[],
                                       int n)
{
    if (n == 1 || n == 2)
        return true;

    // Sort array
    Arrays.sort(arr);

    // After sorting, check if every
    // element is equal to the sum
    // of previous 2 elements
    for(int i = 2; i < n; i++)
    {
       if ((arr[i - 1] + arr[i - 2]) != arr[i])
           return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 8, 3, 5, 13 };
    int n = arr.length;

    if (checkIsFibonacci(arr, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to check if the
# elements of a given array
# can form a Fibonacci Series

# Returns true if a permutation
# of arr[0..n-1] can form a
# Fibonacci Series
def checkIsFibonacci(arr, n) :

    if (n == 1 or n == 2) :
        return True;

    # Sort array
    arr.sort()

    # After sorting, check if every
    # element is equal to the
    # sum of previous 2 elements

    for i in range(2, n) :
        if ((arr[i - 1] +
             arr[i - 2])!= arr[i]) :
            return False;

    return True;

# Driver Code
if __name__ == "__main__" :

    arr = [ 8, 3, 5, 13 ];
    n = len(arr);

    if (checkIsFibonacci(arr, n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to check if the elements of
// a given array can form a fibonacci series
using System;

class GFG{

// Returns true if a permutation
// of arr[0..n-1] can form a
// fibonacci series
public static bool checkIsFibonacci(int []arr,
                                    int n)
{
    if (n == 1 || n == 2)
        return true;

    // Sort array
    Array.Sort(arr);

    // After sorting, check if every
    // element is equal to the sum
    // of previous 2 elements
    for(int i = 2; i < n; i++)
    {
       if ((arr[i - 1] + arr[i - 2]) != arr[i])
           return false;
    }
    return true;
}

// Driver code
public static void Main(string[] args)
{
    int []arr = { 8, 3, 5, 13 };
    int n = arr.Length;

    if (checkIsFibonacci(arr, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to check if the elements of
// a given array can form a Fibonacci Series

    // Returns true if a permutation
    // of arr[0..n-1] can form a
    // Fibonacci Series
    function checkIsFibonacci(arr , n)
    {
        if (n == 1 || n == 2)
            return true;

        // Sort array
        arr.sort((a, b) => a - b);

        // After sorting, check if every
        // element is equal to the sum
        // of previous 2 elements
        for (i = 2; i < n; i++) {
            if ((arr[i - 1] + arr[i - 2]) != arr[i])
                return false;
        }
        return true;
    }

    // Driver code

        var arr = [ 8, 3, 5, 13 ];
        var n = arr.length;

        if (checkIsFibonacci(arr, n))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**T2【O(N Log N)T4】
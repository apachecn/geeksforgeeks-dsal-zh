# 检查是否存在总和大于给定阵列的子阵列

> 原文:[https://www . geesforgeks . org/check-if-a-subarray-exists-sum-大于给定数组/](https://www.geeksforgeeks.org/check-if-a-subarray-exists-with-sum-greater-than-the-given-array/)

给定一个整数数组 **arr** ，任务是检查是否有一个子数组(给定数组除外)，使得其元素之和大于或等于给定数组的元素之和。如果没有这样的子阵列，打印**否**，否则打印**是**。
**举例:**

> **输入:** arr = {5，6，7，8}
> **输出:**否
> **解释:**
> 给定数组中没有任何子数组的元素之和大于或等于给定数组的元素之和。
> **输入:** arr = {-1，7，4}
> **输出:**是
> **说明:**
> 存在一个子阵{7，4}，其和大于给定数组元素的和。

**方法:**只有在两种情况之一
下，子阵列的和大于原始阵列的和才有可能

*   如果给定数组的所有元素之和小于或等于 0
*   如果存在一个前缀或后缀子数组，其和为负

所以检查所有可能的前缀和后缀子数组的和是否小于或等于零，答案是肯定的。否则答案是否定的
下面是上述方法的实现

## C++

```
// C++ program to check if a subarray exists
// with sum greater than the given Array
#include <bits/stdc++.h>
using namespace std;

// Function to check whether there exists
// a subarray whose sum is greater than
// or equal to sum of given array elements
int subarrayPossible(int arr[], int n)
{
    // Initialize sum with 0
    int sum = 0;

    // Checking possible prefix subarrays.
    // If sum of them is less than or equal
    // to zero, then return 1
    for (int i = 0; i < n; i++) {
        sum += arr[i];

        if (sum <= 0)
            return 1;
    }

    // again reset sum to zero
    sum = 0;

    // Checking possible suffix subarrays.
    // If sum of them is less than or equal
    // to zero, then return 1
    for (int i = n - 1; i >= 0; i--) {
        sum += arr[i];

        if (sum <= 0)
            return 1;
    }

    // Otherwise return 0
    return 0;
}

// Driver Code
int main()
{
    int arr[] = { 10, 5, -12, 7, -10, 20,
                  30, -10, 50, 60 };

    int size = sizeof(arr) / sizeof(arr[0]);

    if (subarrayPossible(arr, size))
        cout << "Yes"
             << "\n";
    else
        cout << "No"
             << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a subarray exists
// with sum greater than the given Array
import java.util.*;

class GFG{

    // Function to check whether there exists
    // a subarray whose sum is greater than
   // or equal to sum of given array elements
    static boolean subarrayPossible(int arr[], int n)
    {
        // Initialize sum with 0
        int sum = 0;

        // Checking possible prefix subarrays.
        // If sum of them is less than or equal
        // to zero, then return 1
        for (int i = 0; i < n; i++) {
            sum += arr[i];

            if (sum <= 0)
                return true;
        }

        // again reset sum to zero
        sum = 0;

        // Checking possible suffix subarrays.
        // If sum of them is less than or equal
        // to zero, then return 1
        for (int i = n - 1; i >= 0; i--) {
            sum += arr[i];

            if (sum <= 0)
                return true;
        }

        // Otherwise return 0
        return false;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 10, 5, -12, 7, -10, 20, 30, -10, 50, 60 };

        int size = arr.length;

        if (subarrayPossible(arr, size))
            System.out.print("Yes"+"\n");
        else
            System.out.print("No"+"\n");
    }
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 program to check if a subarray exists
# with sum greater than the given Array

# Function to check whether there exists
# a subarray whose sum is greater than
# or equal to sum of given array elements
def subarrayPossible(arr, n):
    # Initialize sum with 0
    sum = 0;

    # Checking possible prefix subarrays.
    # If sum of them is less than or equal
    # to zero, then return 1
    for i in range(n):
        sum += arr[i];

        if (sum <= 0):
            return True;

    # again reset sum to zero
    sum = 0;

    # Checking possible suffix subarrays.
    # If sum of them is less than or equal
    # to zero, then return 1
    for i in range(n-1, -1,-1):
        sum += arr[i];

        if (sum <= 0):
            return True;

    # Otherwise return 0
    return False;

# Driver Code
if __name__ == '__main__':
    arr = [ 10, 5, -12, 7, -10, 20, 30, -10, 50, 60 ];

    size = len(arr);

    if (subarrayPossible(arr, size)):
        print("Yes");
    else:
        print("No");

# This code is contributed by Princi Singh
```

## C#

```
// C# program to check if a subarray exists
// with sum greater than the given Array
using System;

class GFG{

// Function to check whether there exists
// a subarray whose sum is greater than
// or equal to sum of given array elements
    static bool subarrayPossible(int []arr, int n)
    {
        // Initialize sum with 0
        int sum = 0;

        // Checking possible prefix subarrays.
        // If sum of them is less than or equal
        // to zero, then return 1
        for (int i = 0; i < n; i++) {
            sum += arr[i];

            if (sum <= 0)
                return true;
        }

        // again reset sum to zero
        sum = 0;

        // Checking possible suffix subarrays.
        // If sum of them is less than or equal
        // to zero, then return 1
        for (int i = n - 1; i >= 0; i--) {
            sum += arr[i];

            if (sum <= 0)
                return true;
        }

        // Otherwise return 0
        return false;
    }

    // Driver Code
    public static void Main(String []args)
    {
        int []arr = { 10, 5, -12, 7, -10, 20, 30, -10, 50, 60 };

        int size = arr.Length;

        if (subarrayPossible(arr, size))
            Console.Write("Yes"+"\n");
        else
            Console.Write("No"+"\n");
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to check if a subarray exists
// with sum greater than the given Array

    // Function to check whether there exists
    // a subarray whose sum is greater than
   // or equal to sum of given array elements
    function subarrayPossible(arr, n)
    {
        // Initialize sum with 0
        let sum = 0;

        // Checking possible prefix subarrays.
        // If sum of them is less than or equal
        // to zero, then return 1
        for (let i = 0; i < n; i++) {
            sum += arr[i];

            if (sum <= 0)
                return true;
        }

        // again reset sum to zero
        sum = 0;

        // Checking possible suffix subarrays.
        // If sum of them is less than or equal
        // to zero, then return 1
        for (let i = n - 1; i >= 0; i--) {
            sum += arr[i];

            if (sum <= 0)
                return true;
        }

        // Otherwise return 0
        return false;
    }

// Driver Code

    let arr = [ 10, 5, -12, 7, -10, 20, 30, -10, 50, 60 ];

        let size = arr.length;

        if (subarrayPossible(arr, size))
            document.write("Yes"+"<br/>");
        else
           document.write("No"+"<br/>");

</script>
```

**Output:** 

```
Yes
```

**业绩分析** :

*   **时间复杂度**:在上面的方法中，我们对长度为 N 的数组进行了两次迭代，所以时间复杂度为 **O(N)** 。

*   **辅助空间复杂度**:在上面的方法中，我们只使用了几个常量，所以辅助空间复杂度为 **O(1)** 。
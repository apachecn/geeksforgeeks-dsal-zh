# 将数组中的每个元素减少到一半，保持总和为零

> 原文:[https://www . geeksforgeeks . org/将数组中的每个元素减少到其一半，保留零和数/](https://www.geeksforgeeks.org/reduce-every-element-of-the-array-to-its-half-retaining-the-sum-zero/)

给定一个总元素和等于零的 **N** 整数的数组 **arr[]** 。任务是把每一个元素减少到一半，这样总和保持为零。对于数组中的每一个奇数元素 **X** ，它可以减少到 **(X + 1) / 2** 或**(X–1)/2**。
**举例:**

> **输入:** arr[] = {-7，14，-7}
> **输出:** -4 7 -3
> -4 + 7 -3 = 0
> **输入:** arr[] = {-14，14}
> **输出:** -7 7

**方法:**所有偶数元素都可以除以 2，但对于奇数元素，它们必须交替减少到 **(X + 1) / 2** 和**(X–1)/2**，以便在最终数组中保留原始总和(即 0)。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to reduce every
// element to it's half such that
// the total sum remain zero
void half(int arr[], int n)
{
    int i;

    // Flag to switch between alternating
    // odd numbers in the array
    int flag = 0;

    // For every element of the array
    for (i = 0; i < n; i++)
    {

        // If its even then reduce it to half
        if (arr[i] % 2 == 0 )
            cout << arr[i] / 2 << " ";

        // If its odd
        else
        {

            // Reduce the odd elements
            // alternatively
            if (flag == 0)
            {
                cout << arr[i] / 2 - 1 << " ";

                // Switch flag
                flag = 1;
            }
            else
            {
                int q = arr[i] / 2;
                cout<<q <<" ";

                // Switch flag
                flag = 0;
            }
        }
    }
}

// Driver code
int main ()
{
    int arr[] = {-7, 14, -7};
    int len = sizeof(arr)/sizeof(arr[0]);
    half(arr, len) ;
    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to reduce every
// element to it's half such that
// the total sum remain zero
static void half(int arr[], int n)
{
    int i;

    // Flag to switch between alternating
    // odd numbers in the array
    int flag = 0;

    // For every element of the array
    for (i = 0; i < n; i++)
    {

        // If its even then reduce it to half
        if (arr[i] % 2 == 0 )
            System.out.print(arr[i] / 2 + " ");

        // If its odd
        else
        {

            // Reduce the odd elements
            // alternatively
            if (flag == 0)
            {
                System.out.print(arr[i] / 2 - 1 + " ");

                // Switch flag
                flag = 1;
            }
            else
            {
                int q = arr[i] / 2;
                System.out.print(q + " ");

                // Switch flag
                flag = 0;
            }
        }
    }
}

// Driver code
public static void main (String[] args)
{
    int arr[] = {-7, 14, -7};
    int len = arr.length;
    half(arr, len) ;
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to reduce every
# element to it's half such that
# the total sum remain zero
def half(arr, n) :

    # Flag to switch between alternating
    # odd numbers in the array
    flag = 0

    # For every element of the array
    for i in range(n):

        # If its even then reduce it to half
        if arr[i] % 2 == 0 :
            print(arr[i]//2, end =" ")

        # If its odd
        else :

            # Reduce the odd elements
            # alternatively
            if flag == 0:
                print(arr[i]//2, end =" ")

                # Switch flag
                flag = 1
            else :
                q = arr[i]//2
                q+= 1
                print(q, end =" ")

                # Switch flag
                flag = 0

# Driver code
arr = [-7, 14, -7]
half(arr, len(arr))
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to reduce every
// element to it's half such that
// the total sum remain zero
static void half(int []arr, int n)
{
    int i;

    // Flag to switch between alternating
    // odd numbers in the array
    int flag = 0;

    // For every element of the array
    for (i = 0; i < n; i++)
    {

        // If its even then reduce it to half
        if (arr[i] % 2 == 0 )
            Console.Write(arr[i] / 2 + " ");

        // If its odd
        else
        {

            // Reduce the odd elements
            // alternatively
            if (flag == 0)
            {
                Console.Write(arr[i] / 2 - 1 + " ");

                // Switch flag
                flag = 1;
            }
            else
            {
                int q = arr[i] / 2;
                Console.Write(q + " ");

                // Switch flag
                flag = 0;
            }
        }
    }
}

// Driver code
public static void Main ()
{
    int [] arr = {-7, 14, -7};
    int len = arr.Length;
    half(arr, len) ;
}
}

// This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to reduce every
// element to it's half such that
// the total sum remain zero
function half(arr, n)
{
    let i;

    // Flag to switch between alternating
    // odd numbers in the array
    let flag = 0;

    // For every element of the array
    for (i = 0; i < n; i++)
    {

        // If its even then reduce it to half
        if (arr[i] % 2 == 0 )
            document.write(arr[i] / 2 + " ");

        // If its odd
        else
        {

            // Reduce the odd elements
            // alternatively
            if (flag == 0)
            {
                document.write(Math.ceil(arr[i] / 2) - 1 + " ");

                // Switch flag
                flag = 1;
            }
            else
            {
                let q = Math.ceil(arr[i] / 2);
                document.write(q + " ");

                // Switch flag
                flag = 0;
            }
        }
    }
}

// Driver code
    let arr = [-7, 14, -7];
    let len = arr.length;
    half(arr, len) ;

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
-4 7 -3
```
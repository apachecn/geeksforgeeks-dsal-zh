# 所有相邻元素对之和为奇数所需的最小子阵列反转

> 原文:[https://www . geesforgeks . org/minimum-subarray-reverses-required-这样所有相邻元素对的总和就是奇数/](https://www.geeksforgeeks.org/minimum-subarray-reversals-required-such-that-sum-of-all-pairs-of-adjacent-elements-is-odd/)

给定大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，具有相等数量的偶数和奇数，任务是找到使相邻元素对之和为奇数所需的最小数量的[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。

**示例:**

> **输入:** arr[] = {13，2，6，8，3，5，7，10，14，15}
> **输出:** 3
> **解释:**
> **步骤 1:** 反转子阵列[2，4]将阵列修改为{13，2，3，8，6，5，7，10，14，15}
> **步骤 2:** 反转子阵列[2，4] 9]将数组修改为{13，2，3，8，5，6，7，10，15，14}
> 上述反转后，所有相邻元素对的和为奇数。
> 因此，所需的最小反转为 3 次。
> 
> **输入:** arr[] = {1，3，4，5，9，6，8 }
> T3】输出: 2

**方法:**要使相邻元素之和为奇数，其思想是以奇偶或偶奇的方式排列元素。要最小化反转操作的计数，请观察给定数组的以下属性:

*   如果有任何长度为 **M** 的子阵列具有相同奇偶性的所有元素，那么也存在长度为 **M** 的子阵列具有相反奇偶性的所有元素，因为阵列中偶数和奇数元素的计数相同。
*   因此，使长度为 **M** 的子阵列交替奇偶校验所需的反转操作计数为**(M–1)**。

按照以下步骤解决问题:

*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，找到数组中每个连续的相同奇数和偶数元素所需的子数组反转计数。
*   让连续奇数和偶数元素的反转计数分别为**计数奇数**和**计数偶数**。
*   反转的最小计数由最大值**和**给出，因为任务是移除所有连续的相同元素和需要移除的最大连续。****

**下面是上述方法的实现:**

## **C++14**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count reversals to
// separate elements with same parity
int separate(int arr[], int n, int parity)
{
    int count = 1, res = 0;

    // Traverse the given array
    for (int i = 1; i < n; i++) {

        // Count size of subarray having
        // integers with same parity only
        if (((arr[i] + parity) & 1)
            && ((arr[i - 1] + parity) & 1))
            count++;

        // Otherwise
        else {

            // Reversals required is equal
            // to one less than subarray size
            if (count > 1)
                res += count - 1;

            count = 1;
        }
    }

    // Return the total reversals
    return res;
}

// Function to print the array elements
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to count the minimum reversals
// required to make make sum
// of all adjacent elements odd
void requiredOps(int arr[], int N)
{
    // Stores operations required for
    // separating adjacent odd elements
    int res1 = separate(arr, N, 0);

    // Stores operations required for
    // separating adjacent even elements
    int res2 = separate(arr, N, 1);

    // Maximum of two is the return
    cout << max(res1, res2);
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 13, 2, 6, 8, 3, 5,
                  7, 10, 14, 15 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    requiredOps(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count reversals to
// separate elements with same parity
static int separate(int arr[], int n, 
                    int parity)
{
    int count = 1, res = 0;

    // Traverse the given array
    for(int i = 1; i < n; i++)
    {

        // Count size of subarray having
        // integers with same parity only
        if (((arr[i] + parity) & 1) != 0 &&
            ((arr[i - 1] + parity) & 1) != 0)
            count++;

        // Otherwise
        else
        {

            // Reversals required is equal
            // to one less than subarray size
            if (count > 1)
                res += count - 1;

            count = 1;
        }
    }

    // Return the total reversals
    return res;
}

// Function to print the array elements
void printArray(int arr[], int n)
{
    for(int i = 0; i < n; i++)
        System.out.println(arr[i] + " ");
}

// Function to count the minimum reversals
// required to make make sum
// of all adjacent elements odd
static void requiredOps(int arr[], int N)
{

    // Stores operations required for
    // separating adjacent odd elements
    int res1 = separate(arr, N, 0);

    // Stores operations required for
    // separating adjacent even elements
    int res2 = separate(arr, N, 1);

    // Maximum of two is the return
    System.out.print(Math.max(res1, res2));
}

// Driver Code
public static void main(String args[])
{

    // Given array arr[]
    int arr[] = { 13, 2, 6, 8, 3, 5,
                  7, 10, 14, 15 };

    // Size of array
    int N = arr.length;

    // Function Call
    requiredOps(arr, N);
}
}

// This code is contributed by ipg2016107
```

## **蟒蛇 3**

```
# Python3 program for the
# above approach

# Function to count reversals
# to separate elements with
# same parity
def separate(arr, n, parity):

    count = 1
    res = 0

    # Traverse the given array
    for i in range(1, n):

        # Count size of subarray
        # having integers with
        # same parity only
        if (((arr[i] + parity) & 1) and
            ((arr[i - 1] + parity) & 1)):
            count += 1

        # Otherwise
        else:

            # Reversals required is
            # equal to one less than
            # subarray size
            if (count > 1):
                res += count - 1

            count = 1

    # Return the total
    # reversals
    return res

# Function to print the
# array elements
def printArray(arr, n):

    for i in range(n):
        print(arr[i],
              end = " ")

# Function to count the minimum
# reversals required to make
# make sum of all adjacent
# elements odd
def requiredOps(arr, N):

    # Stores operations required
    # for separating adjacent
    # odd elements
    res1 = separate(arr, N, 0)

    # Stores operations required
    # for separating adjacent
    # even elements
    res2 = separate(arr, N, 1)

    # Maximum of two is the
    # return
    print(max(res1, res2))

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [13, 2, 6, 8, 3, 5,
           7, 10, 14, 15]

    # Size of array
    N = len(arr)

    # Function Call
    requiredOps(arr, N)

# This code is contributed by Chitranayal
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to count reversals to
// separate elements with same parity
static int separate(int[] arr, int n, 
                    int parity)
{
    int count = 1, res = 0;

    // Traverse the given array
    for(int i = 1; i < n; i++)
    {

        // Count size of subarray having
        // integers with same parity only
        if (((arr[i] + parity) & 1) != 0 &&
            ((arr[i - 1] + parity) & 1) != 0)
            count++;

        // Otherwise
        else
        {

            // Reversals required is equal
            // to one less than subarray size
            if (count > 1)
                res += count - 1;

            count = 1;
        }
    }

    // Return the total reversals
    return res;
}

// Function to print the array elements
void printArray(int[] arr, int n)
{
    for(int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Function to count the minimum reversals
// required to make make sum
// of all adjacent elements odd
static void requiredOps(int[] arr, int N)
{

    // Stores operations required for
    // separating adjacent odd elements
    int res1 = separate(arr, N, 0);

    // Stores operations required for
    // separating adjacent even elements
    int res2 = separate(arr, N, 1);

    // Maximum of two is the return
    Console.Write(Math.Max(res1, res2));
}

// Driver code
public static void Main()
{

    // Given array arr[]
    int[] arr = { 13, 2, 6, 8, 3, 5,
                  7, 10, 14, 15 };

    // Size of array
    int N = arr.Length;

    // Function Call
    requiredOps(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## **java 描述语言**

```
<script>

// JavaScript program to implement
// the above approach

// Function to count reversals to
// separate elements with same parity
function separate(arr, n, parity)
{
    let count = 1, res = 0;

    // Traverse the given array
    for(let i = 1; i < n; i++)
    {

        // Count size of subarray having
        // integers with same parity only
        if (((arr[i] + parity) & 1) != 0 &&
            ((arr[i - 1] + parity) & 1) != 0)
            count++;

        // Otherwise
        else
        {

            // Reversals required is equal
            // to one less than subarray size
            if (count > 1)
                res += count - 1;

            count = 1;
        }
    }

    // Return the total reversals
    return res;
}

// Function to print the array elements
function printArray(arr, n)
{
    for(let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Function to count the minimum reversals
// required to make make sum
// of all adjacent elements odd
function requiredOps( arr, N)
{

    // Stores operations required for
    // separating adjacent odd elements
    let res1 = separate(arr, N, 0);

    // Stores operations required for
    // separating adjacent even elements
    let res2 = separate(arr, N, 1);

    // Maximum of two is the return
    document.write(Math.max(res1, res2));
}

// Driver Code

    // Given array arr[]
    let arr = [ 13, 2, 6, 8, 3, 5,
                  7, 10, 14, 15 ];

    // Size of array
    let N = arr.length;

    // Function Call
    requiredOps(arr, N);

</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**
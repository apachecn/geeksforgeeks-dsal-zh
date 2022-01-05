# 一个阵列的所有子阵列的逐位“与”的逐位“或”

> 原文:[https://www . geeksforgeeks . org/数组的所有子数组的逐位或运算/](https://www.geeksforgeeks.org/bitwise-or-of-bitwise-and-of-all-subarrays-of-an-array/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到给定数组的所有[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> ***输入:** arr[] = {1，2，3}*
> ***输出:** 3*
> ***解释:***
> *以下是所有可能的子阵列的按位 AND:*
> 
> 1.  *{1}，按位“与”为 1。*
> 2.  *{1，2}，按位“与”为 0。*
> 3.  *{1，2，3}，按位“与”为 0。*
> 4.  *{2}，按位“与”为 2。*
> 5.  *{2，3}，按位“与”为 2。*
> 6.  *{3}，按位“与”为 3。*
> 
> *上述所有值的按位“或”为 3。*
> 
> ***输入:** arr[] = {1，4，2，10}*
> ***输出:** 15*

**天真法:**解决给定问题最简单的方法是[生成给定阵列的所有可能子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，然后找到所有生成子阵列的所有位“与”的位“或”作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the Bitwise OR
// of Bitwise AND of all subarrays
void findbitwiseOR(int* a, int n)
{
    // Stores the required result
    int res = 0;

    // Generate all the subarrays
    for (int i = 0; i < n; i++) {

        // Store the current element
        int curr_sub_array = a[i];

        // Find the Bitwise OR
        res = res | curr_sub_array;

        for (int j = i; j < n; j++) {

            // Update the result
            curr_sub_array = curr_sub_array
                             & a[j];
            res = res | curr_sub_array;
        }
    }

    // Print the result
    cout << res;
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3 };
    int N = sizeof(A) / sizeof(A[0]);
    findbitwiseOR(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to find the Bitwise OR
    // of Bitwise AND of all subarrays
    static void findbitwiseOR(int[] a, int n)
    {
        // Stores the required result
        int res = 0;

        // Generate all the subarrays
        for (int i = 0; i < n; i++) {

            // Store the current element
            int curr_sub_array = a[i];

            // Find the Bitwise OR
            res = res | curr_sub_array;

            for (int j = i; j < n; j++) {

                // Update the result
                curr_sub_array = curr_sub_array & a[j];
                res = res | curr_sub_array;
            }
        }

        // Print the result
        System.out.println(res);
    }
    // Driver code
    public static void main(String[] args)
    {
        int A[] = { 1, 2, 3 };
        int N = A.length;
        findbitwiseOR(A, N);
    }
}
// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the Bitwise OR
# of Bitwise AND of all subarrays
def findbitwiseOR(a, n):

    # Stores the required result
    res = 0

    # Generate all the subarrays
    for i in range(n):

        # Store the current element
        curr_sub_array = a[i]

        # Find the Bitwise OR
        res = res | curr_sub_array

        for j in range(i, n):

            # Update the result
            curr_sub_array = curr_sub_array & a[j]
            res = res | curr_sub_array

    # Print the result
    print (res)

# Driver Code
if __name__ == '__main__':

    A = [ 1, 2, 3 ]
    N = len(A)

    findbitwiseOR(A, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Function to find the Bitwise OR
    // of Bitwise AND of all subarrays
    static void findbitwiseOR(int[] a, int n)
    {
        // Stores the required result
        int res = 0;

        // Generate all the subarrays
        for (int i = 0; i < n; i++) {

            // Store the current element
            int curr_sub_array = a[i];

            // Find the Bitwise OR
            res = res | curr_sub_array;

            for (int j = i; j < n; j++) {

                // Update the result
                curr_sub_array = curr_sub_array & a[j];
                res = res | curr_sub_array;
            }
        }

        // Print the result
        Console.Write(res);
    }

// Driver code
static void Main()
{
    int[] A = { 1, 2, 3 };
        int N = A.Length;
        findbitwiseOR(A, N);

}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find the Bitwise OR
    // of Bitwise AND of all subarrays
    function findbitwiseOR(a, n)
    {
        // Stores the required result
        let res = 0;

        // Generate all the subarrays
        for (let i = 0; i < n; i++) {

            // Store the current element
            let curr_sub_array = a[i];

            // Find the Bitwise OR
            res = res | curr_sub_array;

            for (let j = i; j < n; j++) {

                // Update the result
                curr_sub_array = curr_sub_array & a[j];
                res = res | curr_sub_array;
            }
        }

        // Print the result
        document.write(res);
    }

// Driver Code

        let A = [ 1, 2, 3 ];
        let N = A.length;
        findbitwiseOR(A, N);

</script>  
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以基于任何子阵列的[位与总是小于或等于子阵列中的第一个元素的观察来优化。因此，最大可能值是子阵列的位“与”，子阵列本身就是元素。因此，任务简化为查找所有数组元素的**位“或”**作为结果。](https://www.geeksforgeeks.org/find-bitwise-and-of-all-possible-sub-arrays/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the Bitwise OR of
// Bitwise AND of all consecutive
// subsets of the array
void findbitwiseOR(int* a, int n)
{
    // Stores the required result
    int res = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++)
        res = res | a[i];

    // Print the result
    cout << res;
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3 };
    int N = sizeof(A) / sizeof(A[0]);
    findbitwiseOR(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the Bitwise OR of
// Bitwise AND of all consecutive
// subsets of the array
static void findbitwiseOR(int[] a, int n)
{

    // Stores the required result
    int res = 0;

    // Traverse the given array
    for(int i = 0; i < n; i++)
        res = res | a[i];

    // Print the result
    System.out.println(res);
}

// Driver Code
public static void main(String[] args)
{
    int[] A = { 1, 2, 3 };
    int N = A.length;

    findbitwiseOR(A, N);
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the Bitwise OR of
# Bitwise AND of all consecutive
# subsets of the array
def findbitwiseOR(a, n):

    # Stores the required result
    res = 0

    # Traverse the given array
    for i in range(n):
        res = res | a[i]

    # Print the result
    print(res)

# Driver Code
if __name__ == '__main__':

    A = [ 1, 2, 3 ]
    N = len(A)

    findbitwiseOR(A, N)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the Bitwise OR of
// Bitwise AND of all consecutive
// subsets of the array
static void findbitwiseOR(int[] a, int n)
{

    // Stores the required result
    int res = 0;

    // Traverse the given array
    for(int i = 0; i < n; i++)
        res = res | a[i];

    // Print the result
    Console.Write(res);
}

// Driver Code
public static void Main()
{
    int[] A = { 1, 2, 3 };
    int N = A.Length;

    findbitwiseOR(A, N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the Bitwise OR of
// Bitwise AND of all consecutive
// subsets of the array
function findbitwiseOR(a, n)
{
    // Stores the required result
    var res = 0;

    var i;
    // Traverse the given array
    for (i = 0; i < n; i++)
        res = res | a[i];

    // Print the result
    document.write(res);
}

// Driver Code
    var A = [1, 2, 3];
    var N = A.length;
    findbitwiseOR(A, N);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
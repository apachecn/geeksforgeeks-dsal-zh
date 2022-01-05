# 通过交换相邻元素来打乱每个数组元素的位置

> 原文:[https://www . geeksforgeeks . org/通过交换相邻元素来洗牌每个数组元素的位置/](https://www.geeksforgeeks.org/shuffle-the-position-of-each-array-element-by-swapping-adjacent-elements/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过交换相邻元素来重新排列数组元素，使得交换后没有元素保持在相同的位置。

**示例:**

> **输入:** arr[] = { 1，2，3，4，5 }
> **输出:** 2 1 5 3 4
> **解释:**
> 相邻元素互换如下:
> (1，2 - > 2，1)
> (3，4，5 - > 5，3，4)
> **输入:** arr[] = {1，2，3，4}
> 【T15

**方法:**问题中的关键观察是，数组可以有两种情况来交换数组元素:

*   如果数组的长度是偶数，那么我们可以很容易地[交换 2 个变量，而不用为每对连续的元素使用第三个变量](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)。
*   如果数组的长度是奇数，那么我们可以像上面一样，但是最后 3 个元素不会形成一对，所以我们可以很容易地[交换这 3 个变量，而不使用第 4 个变量](https://www.geeksforgeeks.org/swap-three-variables-without-using-temporary-variable/)。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the array
void print(int a[], int n)
{
    // Loop to iterate over the
    // elements of array
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
}

// Function to swap two variables without
// using the third variable
void swapTwo(int& x, int& y)
{
    // Store XOR of all in x
    x = x ^ y;

    // After this, y has value of x
    y = x ^ y;

    // After this, x has value of y
    x = x ^ y;
}

// Function to swap three variables
// without using fourth variable
void swapThree(int& a, int& b, int& c)
{
    // Store XOR of all in a
    a = a ^ b ^ c;

    // After this, b has value of a
    b = a ^ b ^ c;

    // After this, c has value of b
    c = a ^ b ^ c;

    // After this, a has value of c
    a = a ^ b ^ c;
}

// Function that swaps n integers
void rearrangeArray(int a[], int n)
{
    if (n % 2 == 0) {

        for (int i = 0; i < n - 1; i += 2) {
            // Swap 2 variables without
            // using 3rd variable
            swapTwo(a[i], a[i + 1]);
        }
    }
    else {
        for (int i = 0; i < n - 3; i += 2) {
            // Swap 2 variables without
            // using 3rd variable
            swapTwo(a[i], a[i + 1]);
        }

        // The last 3 elements will not form
        // pair if n is odd
        // Hence, swapp 3 variables without
        // using 4th variable
        swapThree(a[n - 1], a[n - 2], a[n - 3]);
    }

    // Print the array elements
    print(a, n);
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    rearrangeArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to print the array
static void print(int a[], int n)
{

    // Loop to iterate over the
    // elements of array
    for(int i = 0; i < n; i++)
        System.out.print(a[i] + " ");
}

// Function to swap two variables without
// using the third variable
static void swapTwo(int x, int y, int[] a)
{

    // Store XOR of all in x
    a[x] = a[x] ^ a[y];

    // After this, y has value of x
    a[y] = a[x] ^ a[y];

    // After this, x has value of y
    a[x] = a[x] ^ a[y];
}

// Function to swap three variables
// without using fourth variable
static void swapThree(int x, int y,
                      int z, int[] a)
{

    // Store XOR of all in a
    a[x] = a[x] ^ a[y] ^ a[z];

    // After this, b has value of a
    a[y] = a[x] ^ a[y] ^ a[z];

    // After this, c has value of b
    a[z] = a[x] ^ a[y] ^ a[z];

    // After this, a has value of c
    a[x] = a[x] ^ a[y] ^ a[z];
}

// Function that swaps n integers
static void rearrangeArray(int a[], int n)
{
    if (n % 2 == 0)
    {
        for(int i = 0; i < n - 1; i += 2)
        {

            // Swap 2 variables without
            // using 3rd variable
            swapTwo(i, i + 1, a);
        }
    }
    else
    {
        for(int i = 0; i < n - 3; i += 2)
        {

            // Swap 2 variables without
            // using 3rd variable
            swapTwo(i, i + 1, a);
        }

        // The last 3 elements will not form
        // pair if n is odd
        // Hence, swapp 3 variables without
        // using 4th variable
        swapThree(n - 1, n - 2, n - 3, a);
    }

    // Print the array elements
    print(a, n);
}

// Driver code
public static void main (String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = arr.length;

    // Function call
    rearrangeArray(arr, n);    
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the array
def print1(a, n):

    # Loop to iterate over the
    # elements of array
    for i in range(n):
        print(a[i], end = " ")

# Function to swap two variables without
# using the third variable
def swapTwo(x, y):

    # Store XOR of all in x
    x = x ^ y

    # After this, y has value of x
    y = x ^ y

    # After this, x has value of y
    x = x ^ y

    return x, y

# Function to swap three variables
# without using fourth variable
def swapThree(a, b, c):

    # Store XOR of all in a
    a = a ^ b ^ c

    # After this, b has value of a
    b = a ^ b ^ c

    # After this, c has value of b
    c = a ^ b ^ c

    # After this, a has value of c
    a = a ^ b ^ c

    return a , b , c

# Function that swaps n integers
def rearrangeArray(a, n):

    if (n % 2 == 0):
        for i in range (0, n - 1, 2):

            # Swap 2 variables without
            # using 3rd variable
            a[i], a[i + 1] = swapTwo(a[i], a[i + 1])

    else:
        for i in range(0, n - 3, 2):

            # Swap 2 variables without
            # using 3rd variable
            a[i], a[i + 1] = swapTwo(a[i], a[i + 1])

        # The last 3 elements will not form
        # pair if n is odd
        # Hence, swapp 3 variables without
        # using 4th variable
        a[n - 1], a[n - 2], a[n - 3] = swapThree(a[n - 1],
                                                 a[n - 2],
                                                 a[n - 3])

    # Print the array elements
    print1(a, n)

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [1, 2, 3, 4, 5 ]
    n = len(arr)

    # Function call
    rearrangeArray(arr, n)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print the array
static void print(int []a, int n)
{

    // Loop to iterate over the
    // elements of array
    for(int i = 0; i < n; i++)
        Console.Write(a[i] + " ");
}

// Function to swap two variables without
// using the third variable
static void swapTwo(ref int x, ref int y)
{

    // Store XOR of all in x
    x = x ^ y;

    // After this, y has value of x
    y = x ^ y;

    // After this, x has value of y
    x = x ^ y;
}

// Function to swap three variables
// without using fourth variable
static void swapThree(ref int a, ref int b,
                      ref int c)
{

    // Store XOR of all in a
    a = a ^ b ^ c;

    // After this, b has value of a
    b = a ^ b ^ c;

    // After this, c has value of b
    c = a ^ b ^ c;

    // After this, a has value of c
    a = a ^ b ^ c;
}

// Function that swaps n integers
static void rearrangeArray(int []a, int n)
{
    if (n % 2 == 0)
    {
        for(int i = 0; i < n - 1; i += 2)
        {

            // Swap 2 variables without
            // using 3rd variable
            swapTwo(ref a[i], ref a[i + 1]);
        }
    }
    else
    {
        for(int i = 0; i < n - 3; i += 2)
        {

            // Swap 2 variables without
            // using 3rd variable
            swapTwo(ref a[i], ref a[i + 1]);
        }

        // The last 3 elements will not form
        // pair if n is odd
        // Hence, swapp 3 variables without
        // using 4th variable
        swapThree(ref a[n - 1], ref a[n - 2],
                  ref a[n - 3]);
    }

    // Print the array elements
    print(a, n);
}

// Driver Code
public static void Main(string []s)
{

    // Given array arr[]
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.Length;

    // Function call
    rearrangeArray(arr, n);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the array
function print( a, n)
{
    // Loop to iterate over the
    // elements of array
    for (var i = 0; i < n; i++)
        document.write( a[i] + " ");
}

// Function that swaps n integers
function rearrangeArray( a, n)
{
    if (n % 2 == 0) {

        for (var i = 0; i < n - 1; i += 2) {
            // Swap 2 variables without
            // using 3rd variable
            // Store XOR of all in x
            a[i] = a[i] ^ a[i + 1];

            // After this, y has value of x
            a[i + 1] = a[i] ^ a[i + 1];

            // After this, x has value of y
            a[i] = a[i] ^ a[i + 1];
        }
    }
    else {
        for (var i = 0; i < n - 3; i += 2) {
            // Swap 2 variables without
            // using 3rd variable
            // Store XOR of all in x
            a[i] = a[i] ^ a[i + 1];

            // After this, y has value of x
            a[i + 1] = a[i] ^ a[i + 1];

            // After this, x has value of y
            a[i] = a[i] ^ a[i + 1];
        }

        // The last 3 elements will not form
        // pair if n is odd
        // Hence, swapp 3 variables without
        // using 4th variable
        // Store XOR of all in a
        a[n-1] = a[n-1] ^ a[n - 2] ^ a[n - 3];

        // After this, b has value of a
        a[n - 2] = a[n-1] ^ a[n - 2] ^ a[n - 3];

        // After this, c has value of b
        a[n - 3] = a[n-1] ^ a[n - 2] ^ a[n - 3];

        // After this, a has value of c
        a[n-1] = a[n-1] ^ a[n - 2] ^ a[n - 3];
    }

    // Print the array elements
    print(a, n);
}

// Driver Code
// Given array arr[]
var arr = [ 1, 2, 3, 4, 5 ];
var n = arr.length;
// Function Call
rearrangeArray(arr, n);

</script>
```

**Output:** 

```
2 1 4 5 3
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*
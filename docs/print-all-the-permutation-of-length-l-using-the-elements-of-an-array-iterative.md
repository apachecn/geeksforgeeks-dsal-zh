# 使用数组元素打印长度 L 的所有排列|迭代

> 原文:[https://www . geesforgeks . org/print-all-of-length-l-use-elements-of-array-iterative/](https://www.geeksforgeeks.org/print-all-the-permutation-of-length-l-using-the-elements-of-an-array-iterative/)

给定一个由**个唯一元素**组成的数组，我们必须使用数组的元素找到所有长度的排列 **L** 。允许重复元素。
**例:**

> **输入:** arr = { 1，2 }，L=3
> **输出:**
> 111
> 211
> 121
> 221
> 112
> 212
> 122
> 222
> **输入:** arr = { 1，2，3 }，L=2
> **输出:**
> 11

**进场:**

*   为了用 **N** 个元素形成长度为 **L** 的序列，已知序列的第**I**个元素可以用 **N** 种方式填充。所以会有![N^{L} ](img/c5627381f18f9843a991966f875b978e.png "Rendered by QuickLaTeX.com")序列
*   我们将运行一个从 0 到![(N^{L} - 1) ](img/4843f979c662b119300aa230f38f8e6a.png "Rendered by QuickLaTeX.com")的循环，对于每个 **i** ，我们将把 **i** 从基地 **10** 转换为基地 **N** 。转换后的数字将代表数组的索引
*   我们可以通过这种方式打印所有的![N^{L} ](img/c5627381f18f9843a991966f875b978e.png "Rendered by QuickLaTeX.com")序列。

以下是实施办法:

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// Convert the number to Lth
// base and print the sequence
void convert_To_Len_th_base(int n,
                            int arr[],
                            int len,
                            int L)
{
    // Sequence is of length L
    for (int i = 0; i < L; i++) {
        // Print the ith element
        // of sequence
        cout << arr[n % len];
        n /= len;
    }
    cout << endl;
}

// Print all the permuataions
void print(int arr[],
           int len,
           int L)
{
    // There can be (len)^l
    // permutations
    for (int i = 0; i < (int)pow(len, L); i++) {
        // Convert i to len th base
        convert_To_Len_th_base(i, arr, len, L);
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3 };
    int len = sizeof(arr) / sizeof(arr[0]);
    int L = 2;

    // function call
    print(arr, len, L);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for above approach
import java.io.*;

class GFG
{

// Convert the number to Lth
// base and print the sequence
static void convert_To_Len_th_base(int n, int arr[],
                                   int len, int L)
{
    // Sequence is of length L
    for (int i = 0; i < L; i++)
    {
        // Print the ith element
        // of sequence
        System.out.print(arr[n % len]);
        n /= len;
    }
    System.out.println();
}

// Print all the permuataions
static void print(int arr[], int len, int L)
{
    // There can be (len)^l
    // permutations
    for (int i = 0;
             i < (int)Math.pow(len, L); i++)
    {
        // Convert i to len th base
        convert_To_Len_th_base(i, arr, len, L);
    }
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 3 };
    int len = arr.length;
    int L = 2;

    // function call
    print(arr, len, L);
}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python3 implementation for the above approach

# Convert the number to Lth
# base and print the sequence
def convert_To_Len_th_base(n, arr, Len, L):

    # Sequence is of Length L
    for i in range(L):

        # Print the ith element
        # of sequence
        print(arr[n % Len], end = "")
        n //= Len
    print()

# Print all the permuataions
def printf(arr, Len, L):

    # There can be (Len)^l permutations
    for i in range(pow(Len, L)):

        # Convert i to Len th base
        convert_To_Len_th_base(i, arr, Len, L)

# Driver code
arr = [1, 2, 3]
Len = len(arr)
L = 2

# function call
printf(arr, Len, L)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation for above approach
using System;

class GFG
{

// Convert the number to Lth
// base and print the sequence
static void convert_To_Len_th_base(int n, int []arr,
                                   int len, int L)
{
    // Sequence is of length L
    for (int i = 0; i < L; i++)
    {
        // Print the ith element
        // of sequence
        Console.Write(arr[n % len]);
        n /= len;
    }
    Console.WriteLine();
}

// Print all the permuataions
static void print(int []arr, int len, int L)
{
    // There can be (len)^l
    // permutations
    for (int i = 0;
            i < (int)Math.Pow(len, L); i++)
    {
        // Convert i to len th base
        convert_To_Len_th_base(i, arr, len, L);
    }
}

// Driver code
public static void Main (String[] args)
{
    int []arr = { 1, 2, 3 };
    int len = arr.Length;
    int L = 2;

    // function call
    print(arr, len, L);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation

// Convert the number to Lth
// base and print the sequence
function convert_To_Len_th_base( n, arr, len, L)
{
    // Sequence is of length L
    for ( i = 0; i < L; i++) {
        // Print the ith element
        // of sequence
        document.write(parseInt(arr[n % len]));
        n = parseInt(n / len);
    }
   document.write("<br>");
}

// Print all the permuataions
function print( arr, len, L)
{
    // There can be (len)^l
    // permutations
    for (var i = 0; i < parseInt(Math.pow(len, L)); i++) {
        // Convert i to len th base
        convert_To_Len_th_base(i, arr, len, L);
    }
}

var arr = [ 1, 2, 3 ];
var len = arr.length;
var L = 2;

// function call
print(arr, len, L);

//This code is contributed by SoumikModnal
</script>
```

**Output:** 

```
11
21
31
12
22
32
13
23
33
```
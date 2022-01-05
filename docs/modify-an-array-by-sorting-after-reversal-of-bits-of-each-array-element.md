# 在每个数组元素的位反转后通过排序修改数组

> 原文:[https://www . geesforgeks . org/按每个数组元素的位反转后的排序修改数组/](https://www.geeksforgeeks.org/modify-an-array-by-sorting-after-reversal-of-bits-of-each-array-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过将每个数组元素替换为通过反转它们各自的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)和[获得的数字来修改数组，对修改后的数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序。

**示例:**

> **输入:** arr[ ] = {43，422，132}
> **输出:** 33 53 203
> **解释** :
> 数组元素的二进制表示为{101011，110100110，10000100}。
> 反向二进制表示为{110101，011001011，0010000}。
> 反向二进制表示的等效数值为{53，203，33}。
> 这些元素的排序顺序为{33，53，203}。
> 
> **输入:** arr[ ] ={ 98，43，66，83 }
> T3】输出: 33 35 53 101

**方法:**按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，将每个数组元素转换为其等价的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)，并以[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)的形式存储。
*   反转这些二进制字符串，并将反转的二进制字符串转换为等效的十进制。
*   [对修改后的数组](https://www.geeksforgeeks.org/sort-c-stl/)进行排序。
*   打印排序后的数组。

下面是上述方法的实现:

## C++14

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to convert binary
// number to equivalent decimal
int binaryToDecimal(string n)
{
    string num = n;
    int dec_value = 0;

    // Set base value to 1, i.e 2^0
    int base = 1;

    int len = num.length();
    for (int i = len - 1; i >= 0; i--) {
        if (num[i] == '1')
            dec_value += base;
        base = base * 2;
    }

    return dec_value;
}

// Function to convert a decimal
// to equivalent binary representation
string decimalToBinary(int n)
{
    // Stores the binary representation
    string binstr = "";

    while (n > 0) {

        // Since ASCII value of
        // '0', '1' are 48 and 49
        binstr += (n % 2 + 48);
        n = n / 2;
    }

    // As the string is already reversed,
    // no further reversal is required
    return binstr;
}

// Function to convert the reversed binary
// representation to equivalent integer
int reversedBinaryDecimal(int N)
{
    // Stores reversed binary
    // representation of given decimal
    string decimal_to_binar
        = decimalToBinary(N);

    // Stores equivalent decimal
    // value of the binary representation
    int binary_to_decimal
        = binaryToDecimal(decimal_to_binar);

    // Return the resultant integer
    return binary_to_decimal;
}

// Utility function to print the sorted array
void printSortedArray(int arr[], int size)
{
    // Sort the array
    sort(arr, arr + size);

    // Traverse the array
    for (int i = 0; i < size; i++)

        // Print the array elements
        cout << arr[i] << " ";

    cout << endl;
}

// Utility function to reverse the
// binary representations of all
// array elements and sort the modified array
void modifyArray(int arr[], int size)
{
    // Traverse the array
    for (int i = 0; i < size; i++) {

        // Passing array elements to
        // reversedBinaryDecimal function
        arr[i] = reversedBinaryDecimal(
            arr[i]);
    }

    // Pass the array to
    // the sorted array
    printSortedArray(arr, size);
}

// Driver Code
int main()
{
    int arr[] = { 98, 43, 66, 83 };
    int n = sizeof(arr) / sizeof(arr[0]);

    modifyArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to convert binary
// number to equivalent decimal
static int binaryToDecimal(String n)
{
    String num = n;
    int dec_value = 0;

    // Set base value to 1, i.e 2^0
    int base = 1;

    int len = num.length();
    for(int i = len - 1; i >= 0; i--)
    {
        if (num.charAt(i) == '1')
            dec_value += base;

        base = base * 2;
    }
    return dec_value;
}

// Function to convert a decimal
// to equivalent binary representation
static String decimalToBinary(int n)
{

    // Stores the binary representation
    String binstr = "";

    while (n > 0)
    {

        // Since ASCII value of
        // '0', '1' are 48 and 49
        binstr += (char)(n % 2 + 48);
        n = n / 2;
    }

    // As the string is already reversed,
    // no further reversal is required
    return binstr;
}

// Function to convert the reversed binary
// representation to equivalent integer
static int reversedBinaryDecimal(int N)
{

    // Stores reversed binary
    // representation of given decimal
    String decimal_to_binar = decimalToBinary(N);

    // Stores equivalent decimal
    // value of the binary representation
    int binary_to_decimal = binaryToDecimal(
        decimal_to_binar);

    // Return the resultant integer
    return binary_to_decimal;
}

// Utility function to print the sorted array
static void printSortedArray(int arr[], int size)
{

    // Sort the array
    Arrays.sort(arr);

    // Traverse the array
    for(int i = 0; i < size; i++)

        // Print the array elements
        System.out.print(arr[i] + " ");

    System.out.println();
}

// Utility function to reverse the
// binary representations of all
// array elements and sort the modified array
static void modifyArray(int arr[], int size)
{

    // Traverse the array
    for(int i = 0; i < size; i++)
    {

        // Passing array elements to
        // reversedBinaryDecimal function
        arr[i] = reversedBinaryDecimal(arr[i]);
    }

    // Pass the array to
    // the sorted array
    printSortedArray(arr, size);
}

// Driver Code

public static void main(String[] args)
{
    int arr[] = { 98, 43, 66, 83 };
    int n = arr.length;

    modifyArray(arr, n);
}
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to convert binary
# number to equivalent decimal
def binaryToDecimal(n):

    num = n
    dec_value = 0

    # Set base value to 1, i.e 2^0
    base = 1

    length = len(num)

    for i in range(length - 1, -1, -1):
        if (num[i] == '1'):
            dec_value += base

        base = base * 2

    return dec_value

# Function to convert a decimal
# to equivalent binary representation
def decimalToBinary(n):

    # Stores the binary representation
    binstr = ""

    while (n > 0):

        # Since ASCII value of
        # '0', '1' are 48 and 49
        binstr += chr(n % 2 + 48)
        n = n // 2

    # As the string is already reversed,
    # no further reversal is required
    return binstr

# Function to convert the reversed binary
# representation to equivalent integer
def reversedBinaryDecimal(N):

    # Stores reversed binary
    # representation of given decimal
    decimal_to_binar = decimalToBinary(N)

    # Stores equivalent decimal
    # value of the binary representation
    binary_to_decimal = binaryToDecimal(
        decimal_to_binar)

    # Return the resultant integer
    return binary_to_decimal

# Utility function to print the sorted array
def printSortedArray(arr, size):

    # Sort the array
    arr.sort()

    # Traverse the array
    for i in range(size):

        # Print the array elements
        print(arr[i], end=" ")

    print()

# Utility function to reverse the
# binary representations of all
# array elements and sort the modified array
def modifyArray(arr, size):

    # Traverse the array
    for i in range(size):

        # Passing array elements to
        # reversedBinaryDecimal function
        arr[i] = reversedBinaryDecimal(arr[i])

    # Pass the array to
    # the sorted array
    printSortedArray(arr, size)

# Driver Code
if __name__ == "__main__":

    arr = [ 98, 43, 66, 83 ]
    n = len(arr)

    modifyArray(arr, n)

# This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Function to convert binary
// number to equivalent decimal
function binaryToDecimal(n)
{
    let num = n;
    let dec_value = 0;

    // Set base value to 1, i.e 2^0
    let base = 1;

    let len = num.length;
    for(let i = len - 1; i >= 0; i--)
    {
        if (num[i] == '1')
            dec_value += base;

        base = base * 2;
    }
    return dec_value;
}

// Function to convert a decimal
// to equivalent binary representation
function decimalToBinary(n)
{

    // Stores the binary representation
    let binstr = "";

    while (n > 0)
    {

        // Since ASCII value of
        // '0', '1' are 48 and 49
        binstr += String.fromCharCode(n % 2 + 48);
        n = Math.floor(n / 2);
    }

    // As the string is already reversed,
    // no further reversal is required
    return binstr;
}

// Function to convert the reversed binary
// representation to equivalent integer
function reversedBinaryDecimal(N)
{

    // Stores reversed binary
    // representation of given decimal
    let decimal_to_binar = decimalToBinary(N);

    // Stores equivalent decimal
    // value of the binary representation
    let binary_to_decimal = binaryToDecimal(
        decimal_to_binar);

    // Return the resultant integer
    return binary_to_decimal;
}

// Utility function to print the sorted array
function printSortedArray(arr, size)
{

    // Sort the array
    arr.sort(function(a, b){return a - b;});

    // Traverse the array
    for(let i = 0; i < size; i++)

        // Print the array elements
        document.write(arr[i] + " ");

    document.write("<br>")
}

// Utility function to reverse the
// binary representations of all
// array elements and sort the modified array
function modifyArray(arr, size)
{

    // Traverse the array
    for(let i = 0; i < size; i++)
    {

        // Passing array elements to
        // reversedBinaryDecimal function
        arr[i] = reversedBinaryDecimal(
            arr[i]);
    }

    // Pass the array to
    // the sorted array
    printSortedArray(arr, size);
}

// Driver Code
let arr = [ 98, 43, 66, 83 ];
let n = arr.length;

modifyArray(arr, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
33 35 53 101
```

***时间复杂度** : O(NlogN)*
***辅助空间:** O(log <sub>2</sub> M)，其中 M 表示数组中存在的最大元素。*
# 使用给定的按位“与”、“或”和“异或”构造数组

> 原文:[https://www . geeksforgeeks . org/使用给定的按位与或与异或构造数组/](https://www.geeksforgeeks.org/construct-the-array-using-given-bitwise-and-or-and-xor/)

给定由 a、b、c 表示的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)的 **N 个**元素的按位**和**、**或**和**异或**，任务是找到数组的元素。如果不存在这样的数组，则打印“-1”。
**示例:**

> **输入:** N = 3，a = 4，b = 6，c = 6。
> **输出:** {4，4，6}
> **解释:**
> 数组的按位 and = 4&4&6 = 4
> 数组的按位 or = 4 | 4 | 6 = 6
> 数组的按位 xor = 4 ^ 4 ^ 6 = 6
> **输入:** N = 2，a = 4，b = 6，c = 6。
> **输出:** -1

**进场:**

1.  对于按位与**，如果在**中设置了 i <sup>第</sup>位，那么在数组中每个元素必须设置有 **i <sup>第</sup>位**，因为如果即使一个元素的 **i <sup>第</sup>位**是 **0** ，那么数组的按位与将导致 i <sup>第</sup>位为 0。
2.  其次，如果第 I<sup>位没有在 a 中置位，则需要同时处理 OR 和 XOR 值。**如果在 b** 中设置了 i <sup>第</sup>位，则至少有一个元素必须设置了 i <sup>第</sup>位。因此，在数组的第一个元素中设置第 i <sup>位。</sup></sup>
3.  现在，如果 **i <sup>第</sup>位**设置在 **b** 中，那么 **i <sup>第</sup>位**必须在 **c** 中检查。如果在 c 中设置了**位，那么没有问题，因为第一个元素的 i <sup>第</sup>位已经被设置，所以 1 ^ 0 = 1。如果该位未在 c 中设置，则设置第二个元件的第 **i <sup>位</sup>位**。现在，b 不会有任何影响，对于 c 来说， **1 ^ 1 将是 0** 。**
4.  然后，只需计算数组的按位“与”、“或”和“异或”来检查它是否相等。如果结果不相等，那么数组是不可能的，否则给定数组就是答案。

以下是实施办法:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the array
void findArray(int n, int a, int b, int c)
{
    int arr[n + 1] = {};

    // Loop through all bits in number
    for (int bit = 30; bit >= 0; bit--) {

        // If bit is set in AND
        // then set it in every element
        // of the array
        int set = a & (1 << bit);
        if (set) {
            for (int i = 0; i < n; i++)
                arr[i] |= set;
        }

        // If bit is not set in AND
        else {

            // But set in b(OR)
            if (b & (1 << bit)) {

                // Set bit position
                // in first element
                arr[0] |= (1 << bit);

                // If bit is not set in c
                // then set it in second
                // element to keep xor as
                // zero for bit position
                if (!(c & (1 << bit))) {
                    arr[1] |= (1 << bit);
                }
            }
        }
    }

    int aa = INT_MAX, bb = 0, cc = 0;

    // Calculate AND, OR
    // and XOR of array
    for (int i = 0; i < n; i++) {
        aa &= arr[i];
        bb |= arr[i];
        cc ^= arr[i];
    }

    // Check if values are equal or not
    if (a == aa && b == bb && c == cc) {
        for (int i = 0; i < n; i++)
            cout << arr[i] << " ";
    }

    // If not, then array
    // is not possible
    else
        cout << "-1";
}

// Driver Code
int main()
{
    // Given Bitwise AND, OR, and XOR
    int n = 3, a = 4, b = 6, c = 6;

    // Function Call
    findArray(n, a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the array
static void findArray(int n, int a,
                      int b, int c)
{
    int arr[] = new int[n + 1];

    // Loop through all bits in number
    for(int bit = 30; bit >= 0; bit--)
    {

       // If bit is set in AND
       // then set it in every element
       // of the array
       int set = a & (1 << bit);
       if (set != 0)
       {
           for(int i = 0; i < n; i++)
              arr[i] |= set;
       }

       // If bit is not set in AND
       else
       {

           // But set in b(OR)
           if ((b & (1 << bit)) != 0)
           {

               // Set bit position
               // in first element
               arr[0] |= (1 << bit);

               // If bit is not set in c
               // then set it in second
               // element to keep xor as
               // zero for bit position
               if ((c & (1 << bit)) == 0)
               {
                   arr[1] |= (1 << bit);
               }
           }
       }
    }
    int aa = Integer.MAX_VALUE, bb = 0, cc = 0;

    // Calculate AND, OR
    // and XOR of array
    for(int i = 0; i < n; i++)
    {
       aa &= arr[i];
       bb |= arr[i];
       cc ^= arr[i];
    }

    // Check if values are equal or not
    if (a == aa && b == bb && c == cc)
    {
        for(int i = 0; i < n; i++)
           System.out.print(arr[i] + " ");
    }

    // If not, then array
    // is not possible
    else
        System.out.println("-1");
}

// Driver code
public static void main(String[] args)
{

    // Given Bitwise AND, OR, and XOR
    int n = 3, a = 4, b = 6, c = 6;

    // Function Call
    findArray(n, a, b, c);
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
import sys

# Function to find the array
def findArray(n, a, b, c):

    arr = [0] * (n + 1)

    # Loop through all bits in number
    for bit in range (30, -1, -1):

        # If bit is set in AND
        # then set it in every element
        # of the array
        set = a & (1 << bit)
        if (set):
            for i in range (n):
                arr[i] |= set

        # If bit is not set in AND
        else :

            # But set in b(OR)
            if (b & (1 << bit)):

                # Set bit position
                # in first element
                arr[0] |= (1 << bit)

                # If bit is not set in c
                # then set it in second
                # element to keep xor as
                # zero for bit position
                if (not (c & (1 << bit))):
                    arr[1] |= (1 << bit)

    aa = sys.maxsize
    bb = 0
    cc = 0

    # Calculate AND, OR
    # and XOR of array
    for i in range (n):
        aa &= arr[i]
        bb |= arr[i]
        cc ^= arr[i]

    # Check if values are equal or not
    if (a == aa and b == bb and c == cc):
        for i in range (n):
            print (arr[i], end = " ")

    # If not, then array
    # is not possible
    else:
        print ("-1")

# Driver Code
if __name__ =="__main__":

    # Given Bitwise AND, OR, and XOR
    n = 3
    a = 4
    b = 6
    c = 6

    # Function Call
    findArray(n, a, b, c)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the array
static void findArray(int n, int a,
                      int b, int c)
{
    int []arr = new int[n + 1];

    // Loop through all bits in number
    for(int bit = 30; bit >= 0; bit--)
    {

       // If bit is set in AND
       // then set it in every element
       // of the array
       int set = a & (1 << bit);
       if (set != 0)
       {
           for(int i = 0; i < n; i++)
              arr[i] |= set;
       }

       // If bit is not set in AND
       else
       {

           // But set in b(OR)
           if ((b & (1 << bit)) != 0)
           {

               // Set bit position
               // in first element
               arr[0] |= (1 << bit);

               // If bit is not set in c
               // then set it in second
               // element to keep xor as
               // zero for bit position
               if ((c & (1 << bit)) == 0)
               {
                   arr[1] |= (1 << bit);
               }
           }
       }
    }
    int aa = int.MaxValue, bb = 0, cc = 0;

    // Calculate AND, OR
    // and XOR of array
    for(int i = 0; i < n; i++)
    {
       aa &= arr[i];
       bb |= arr[i];
       cc ^= arr[i];
    }

    // Check if values are equal or not
    if (a == aa && b == bb && c == cc)
    {
        for(int i = 0; i < n; i++)
           Console.Write(arr[i] + " ");
    }

    // If not, then array
    // is not possible
    else
        Console.WriteLine("-1");
}

// Driver code
public static void Main(String[] args)
{

    // Given Bitwise AND, OR, and XOR
    int n = 3, a = 4, b = 6, c = 6;

    // Function Call
    findArray(n, a, b, c);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the array
function findArray(n, a, b, c) {
    let arr = new Array(n + 1);

    // Loop through all bits in number
    for (let bit = 30; bit >= 0; bit--) {

        // If bit is set in AND
        // then set it in every element
        // of the array
        let set = a & (1 << bit);
        if (set) {
            for (let i = 0; i < n; i++)
                arr[i] |= set;
        }

        // If bit is not set in AND
        else {

            // But set in b(OR)
            if (b & (1 << bit)) {

                // Set bit position
                // in first element
                arr[0] |= (1 << bit);

                // If bit is not set in c
                // then set it in second
                // element to keep xor as
                // zero for bit position
                if (!(c & (1 << bit))) {
                    arr[1] |= (1 << bit);
                }
            }
        }
    }

    let aa = Number.MAX_SAFE_INTEGER, bb = 0, cc = 0;

    // Calculate AND, OR
    // and XOR of array
    for (let i = 0; i < n; i++) {
        aa &= arr[i];
        bb |= arr[i];
        cc ^= arr[i];
    }

    // Check if values are equal or not
    if (a == aa && b == bb && c == cc) {
        for (let i = 0; i < n; i++)
            document.write(arr[i] + " ");
    }

    // If not, then array
    // is not possible
    else
        document.write("-1");
}

// Driver Code

// Given Bitwise AND, OR, and XOR
let n = 3, a = 4, b = 6, c = 6;

// Function Call
findArray(n, a, b, c);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
6 4 4
```

**时间复杂度:** *O(31*N)*
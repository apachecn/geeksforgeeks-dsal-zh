# 生成具有前一个和下一个元素的按位“与”的数组

> 原文:[https://www . geeksforgeeks . org/生成具有前一个和下一个元素的按位和的数组/](https://www.geeksforgeeks.org/generate-an-array-having-bitwise-and-of-the-previous-and-the-next-element/)

给定一个整数数组**arr[]****N**元素，任务是生成另一个数组，该数组具有上一个和下一个元素的(按位)与，但有以下例外。

1.  第一个元素是第一个和第二个元素的按位“与”。
2.  最后一个元素是最后一个和倒数第二个元素的按位“与”。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6}
> **输出:** 0 1 0 1 4 4
> 新数组将为{1 & 2，1 & 3，2 & 4，3 & 5，4 & 6，5 & 6}
> 
> **输入:** arr[] = {9，8，7}
> **输出:** 8 1 0

**方法:**新数组的第一个和第二个元素可以分别计算为 **arr[0] & arr[1]** 和**arr[N–1]&arr[N–2]**。其余元素可计算为**arr[I–1]&arr[I+1]**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to generate the array that
// satisfies the given condition
void generateArr(int arr[], int n)
{

    // If there is only a single element
    // in the array
    if (n == 1) {
        cout << arr[0];
        return;
    }

    // To store the generated array
    int barr[n];

    // First element
    barr[0] = arr[0] & arr[1];

    // Last element
    barr[n - 1] = arr[n - 1] & arr[n - 2];

    // Rest of the elements
    for (int i = 1; i < n - 1; i++)
        barr[i] = arr[i - 1] & arr[i + 1];

    // Print the generated array
    for (int i = 0; i < n; i++)
        cout << barr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    generateArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java .io.*;

class GFG
{
static void generateArr(int[] arr, int n)
{
    // Nothing to do when array size is 1
    if (n <= 1)
        return;

    // store current value of arr[0]
    // and update it
    int prev = arr[0];
    arr[0] = arr[0] & arr[1];

    // Update rest of the array elements
    for (int i = 1; i < n - 1; i++)
    {
        // Store current value of
        // next interation
        int curr = arr[i];

        // Update current value using
        // previous value
        arr[i] = prev & arr[i + 1];

        // Update previous value
        prev = curr;
    }

    // Update last array element separately
    arr[n - 1] = prev & arr[n - 1];
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };
    int n = arr.length;

    generateArr(arr, n);

    // Print the modified array
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}
}

// This code is contributed by Nikhil
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to generate the array that
# satisfies the given condition
def generateArr(arr, n):

    # If there is only a single element
    # in the array
    if (n == 1):
        print(arr[0]);
        return;

    # To store the generated array
    barr = [0] * n;

    # First element
    barr[0] = arr[0] & arr[1];

    # Last element
    barr[n - 1] = arr[n - 1] & arr[n - 2];

    # Rest of the elements
    for i in range(1, n - 1):
        barr[i] = arr[i - 1] & arr[i + 1];

    # Print the generated array
    for i in range(n):
        print(barr[i], end = " ");

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6];
    n = len(arr);

    generateArr(arr, n);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{
static void generateArr(int[] arr, int n)
{
    // Nothing to do when array size is 1
    if (n <= 1)
        return;

    // store current value of arr[0]
    // and update it
    int prev = arr[0];
    arr[0] = arr[0] & arr[1];

    // Update rest of the array elements
    for (int i = 1; i < n - 1; i++)
    {
        // Store current value of
        // next interation
        int curr = arr[i];

        // Update current value using
        // previous value
        arr[i] = prev & arr[i + 1];

        // Update previous value
        prev = curr;
    }

    // Update last array element separately
    arr[n - 1] = prev & arr[n - 1];
}

// Driver Code
static public void Main ()
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };
    int n = arr.Length;

    generateArr(arr, n);

    // Print the modified array
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to generate the array that
    // satisfies the given condition
    function generateArr(arr, n)
    {

        // If there is only a single element
        // in the array
        if (n == 1) {
            document.write(arr[0]);
            return;
        }

        // To store the generated array
        let barr = new Array(n);

        // First element
        barr[0] = arr[0] & arr[1];

        // Last element
        barr[n - 1] = arr[n - 1] & arr[n - 2];

        // Rest of the elements
        for (let i = 1; i < n - 1; i++)
            barr[i] = arr[i - 1] & arr[i + 1];

        // Print the generated array
        for (let i = 0; i < n; i++)
            document.write(barr[i] + " ");
    }

    let arr = [ 1, 2, 3, 4, 5, 6 ];
    let n = arr.length;

    generateArr(arr, n);

</script>
```

**Output:** 

```
0 1 0 1 4 4
```

**时间复杂度:** O(N)
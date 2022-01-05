# 从其对积

构建一个数组

> 原文:[https://www . geeksforgeeks . org/从配对产品构建阵列/](https://www.geeksforgeeks.org/construct-an-array-from-its-pair-product/)

给定一个对积数组**对[]** ，任务是找到原始数组。一个数组的对积数组 **arr[]** 是包含有序形式的所有对的积的数组，即 **{(arr[0] * arr[1])、(arr[0] * arr[2])、…、(arr[1] * arr[2])、(arr[1] * arr[3])、…、(arr[n–2]* arr[n–1])}**。
**举例:**

> **输入:**对[] = {2，3，6}
> **输出:** 1 2 3
> **输入:**对[] = {48，18，24，24，32，12}
> **输出:** 6 8 3 4

**方法:**首先从给定的对积数组中找到所需数组的大小。假设原阵的大小为 **N** ，对积阵的大小为 **X** 。因此，通过求解**(N *(N–1))/2 = X**， **N** 的值可以计算为**N =(1+(int)sqrt(1+8 * X))/2**。
现在让我们用一个例子来看看解决方案，假设**【A，B，C，D】**的对积数组是**arr【AB，AC，AD，BC，BD，CD】**然后通过取**sqrt((arr[0]* arr[1])/arr[n–1])**->**sqrt((AB * AC)/BC)**将给出值 **A
一旦恢复了第一个元素的值，那么对积数组的所有剩余元素都可以除以它，得到原始数组的剩余元素。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <iostream>
#include <math.h>
using namespace std;

// Utility function to print the array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to generate the original
// array from the pair-product array
void constructArr(int pair[], int n)
{
    int size = (1 + (int)sqrt(1 + 8 * n)) / 2;
    int arr[size];

    // First element of the resulting array
    arr[0] = sqrt((pair[0] * pair[1]) / pair[size - 1]);

    // Find all the other elements
    for (int i = 1; i < size; i++)
        arr[i] = pair[i - 1] / arr[0];

    // Print the elements of the generated array
    printArr(arr, size);
}

// Driver code
int main()
{
    int pair[] = { 48, 18, 24, 24, 32, 12 };
    int n = sizeof(pair) / sizeof(int);

    constructArr(pair, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Utility function to print the array
static void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Function to generate the original
// array from the pair-product array
static void constructArr(int pair[], int n)
{
    int size = (1 + (int)Math.sqrt(1 + 8 * n)) / 2;
    int []arr = new int[size];

    // First element of the resulting array
    arr[0] = (int) Math.sqrt((pair[0] * pair[1]) /
                                        pair[size - 1]);

    // Find all the other elements
    for (int i = 1; i < size; i++)
        arr[i] = pair[i - 1] / arr[0];

    // Print the elements of the generated array
    printArr(arr, size);
}

// Driver code
public static void main(String[] args)
{
    int pair[] = { 48, 18, 24, 24, 32, 12 };
    int n = pair.length;

    constructArr(pair, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Utility function to print the array
def printArr(arr, n) :

    for i in range(n) :
        print(arr[i], end = " ");

# Function to generate the original
# array from the pair-product array
def constructArr(pair, n) :

    size = int((1 + sqrt(1 + 8 * n)) // 2);
    arr = [0] * (size);

    # First element of the resulting array
    arr[0] = int(sqrt((pair[0] * pair[1]) /
                       pair[size - 1]));

    # Find all the other elements
    for i in range(1, size) :
        arr[i] = pair[i - 1] // arr[0];

    # Print the elements of the generated array
    printArr(arr, size);

# Driver code
if __name__ == "__main__" :

    pair = [ 48, 18, 24, 24, 32, 12 ];
    n = len(pair);

    constructArr(pair, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Utility function to print the array
static void printArr(int []arr, int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Function to generate the original
// array from the pair-product array
static void constructArr(int []pair, int n)
{
    int size = (1 + (int)Math.Sqrt(1 + 8 * n)) / 2;
    int []arr = new int[size];

    // First element of the resulting array
    arr[0] = (int) Math.Sqrt((pair[0] * pair[1]) /
                                        pair[size - 1]);

    // Find all the other elements
    for (int i = 1; i < size; i++)
        arr[i] = pair[i - 1] / arr[0];

    // Print the elements of the generated array
    printArr(arr, size);
}

// Driver code
public static void Main(String[] args)
{
    int []pair = { 48, 18, 24, 24, 32, 12 };
    int n = pair.Length;

    constructArr(pair, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Utility function to print the array
function printArr(arr, n) {
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Function to generate the original
// array from the pair-product array
function constructArr(pair, n) {
    let size = Math.floor((1 + Math.sqrt(1 + 8 * n)) / 2);
    let arr = new Array(size);

    // First element of the resulting array

    arr[0] =
    Math.floor(Math.sqrt((pair[0] * pair[1]) / pair[size - 1]));

    // Find all the other elements
    for (let i = 1; i < size; i++)
        arr[i] = Math.floor(pair[i - 1] / arr[0]);

    // Print the elements of the generated array
    printArr(arr, size);
}

// Driver code

let pair = [48, 18, 24, 24, 32, 12];
let n = pair.length;
constructArr(pair, n);

</script>
```

**Output:** 

```
6 8 3 4
```

**时间复杂度** : O(N)。
**辅助空间** : O(N)。
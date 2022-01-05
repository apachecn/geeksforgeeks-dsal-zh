# 重新排列数组元素，使得前 N–1 个元素的按位“与”等于最后一个元素

> 原文:[https://www . geeksforgeeks . org/rearray-array-elements-这样第一个 n-1 个元素的按位和等于最后一个元素/](https://www.geeksforgeeks.org/rearrange-array-elements-such-that-bitwise-and-of-first-n-1-elements-is-equal-to-last-element/)

给定一个正整数数组**arr【】****N**，任务是找到一个排列，使得第一个**N–1**元素的按位“与”等于最后一个元素。如果没有这样的安排，那么输出将是 **-1** 。
**举例:**

> **输入:** arr[] = {1，5，3，3}
> **输出:** 3 5 3 1
> (3 & 5 & 3) = 1 等于最后一个元素。
> **输入:** arr[] = {2，3，7}
> **输出:** -1
> 不可能这样安排。

**进场:**

*   让 **p = x & y** 然后 **p ≤ min(x，y)** ，这意味着按位 AND 是非递增函数。如果对某些元素执行按位“与”，则该值将减少或保持不变。
*   因此，很明显，将最小的元素放在最后一个**索引处，然后检查最后一个元素是否等于第一个**N–1**元素的按位“与”。如果是，则打印所需的排列，否则打印 **-1** 。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print
// the elements of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to find the required arrangement
void findArrangement(int arr[], int n)
{

    // There has to be atleast 2 elements
    if (n < 2) {
        cout << "-1";
        return;
    }

    // Minimum element from the array
    int minVal = *min_element(arr, arr + n);

    // Swap any occurrence of the minimum
    // element with the last element
    for (int i = 0; i < n; i++) {
        if (arr[i] == minVal) {
            swap(arr[i], arr[n - 1]);
            break;
        }
    }

    // Find the bitwise AND of the
    // first (n - 1) elements
    int andVal = arr[0];
    for (int i = 1; i < n - 1; i++) {
        andVal &= arr[i];
    }

    // If the bitwise AND is equal
    // to the last element then
    // print the arrangement
    if (andVal == arr[n - 1])
        printArr(arr, n);
    else
        cout << "-1";
}

// Driver code
int main()
{
    int arr[] = { 1, 5, 3, 3 };
    int n = sizeof(arr) / sizeof(int);

    findArrangement(arr, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Utility function to print
// the elements of an array
static void printArr(int []arr, int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Function to find the required arrangement
static void findArrangement(int arr[], int n)
{

    // There has to be atleast 2 elements
    if (n < 2)
    {
        System.out.print("-1");
        return;
    }

    // Minimum element from the array
    int minVal = Arrays.stream(arr).min().getAsInt();

    // Swap any occurrence of the minimum
    // element with the last element
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == minVal)
        {
            swap(arr, i, n - 1);
            break;
        }
    }

    // Find the bitwise AND of the
    // first (n - 1) elements
    int andVal = arr[0];
    for (int i = 1; i < n - 1; i++)
    {
        andVal &= arr[i];
    }

    // If the bitwise AND is equal
    // to the last element then
    // print the arrangement
    if (andVal == arr[n - 1])
        printArr(arr, n);
    else
        System.out.print("-1");
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 1, 5, 3, 3 };
    int n = arr.length;

    findArrangement(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 implementation of the approach

# Utility function to print
# the elements of an array
def printArr(arr, n) :

    for i in range(n) :
        print(arr[i], end = " ");

# Function to find the required arrangement
def findArrangement(arr, n) :

    # There has to be atleast 2 elements
    if (n < 2) :
        print("-1", end = "");
        return;

    # Minimum element from the array
    minVal = min(arr);

    # Swap any occurrence of the minimum
    # element with the last element
    for i in range(n) :
        if (arr[i] == minVal) :
            arr[i], arr[n - 1] = arr[n - 1], arr[i];
            break;

    # Find the bitwise AND of the
    # first (n - 1) elements
    andVal = arr[0];
    for i in range(1, n - 1) :
        andVal &= arr[i];

    # If the bitwise AND is equal
    # to the last element then
    # print the arrangement
    if (andVal == arr[n - 1]) :
        printArr(arr, n);
    else :
        print("-1");

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 5, 3, 3 ];
    n = len(arr);

    findArrangement(arr, n);

# This code is contributed by AnkitRai01
```

## **C#**

```
// C# implementation of the approach
using System;   
using System.Linq;

class GFG
{

// Utility function to print
// the elements of an array
static void printArr(int []arr, int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Function to find the required arrangement
static void findArrangement(int []arr, int n)
{

    // There has to be atleast 2 elements
    if (n < 2)
    {
        Console.Write("-1");
        return;
    }

    // Minimum element from the array
    int minVal = arr.Min();

    // Swap any occurrence of the minimum
    // element with the last element
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == minVal)
        {
            swap(arr, i, n - 1);
            break;
        }
    }

    // Find the bitwise AND of the
    // first (n - 1) elements
    int andVal = arr[0];
    for (int i = 1; i < n - 1; i++)
    {
        andVal &= arr[i];
    }

    // If the bitwise AND is equal
    // to the last element then
    // print the arrangement
    if (andVal == arr[n - 1])
        printArr(arr, n);
    else
        Console.Write("-1");
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 5, 3, 3 };
    int n = arr.Length;

    findArrangement(arr, n);
}
}

// This code is contributed by PrinciRaj1992
```

## **java 描述语言**

```
<script>

// Javascript implementation of the approach

// Utility function to print
// the elements of an array
function printArr(arr, n)
{
    for (var i = 0; i < n; i++)
        document.write( arr[i] + " ");
}

// Function to find the required arrangement
function findArrangement(arr, n)
{

    // There has to be atleast 2 elements
    if (n < 2) {
        document.write( "-1");
        return;
    }

    // Minimum element from the array
    var minVal =  arr.reduce((a,b)=> Math.min(a,b));

    // Swap any occurrence of the minimum
    // element with the last element
    for (var i = 0; i < n; i++) {
        if (arr[i] == minVal) {
            [arr[i], arr[n-1]] = [arr[n-1], arr[i]];
            break;
        }
    }

    // Find the bitwise AND of the
    // first (n - 1) elements
    var andVal = arr[0];
    for (var i = 1; i < n - 1; i++) {
        andVal &= arr[i];
    }

    // If the bitwise AND is equal
    // to the last element then
    // print the arrangement
    if (andVal == arr[n - 1])
        printArr(arr, n);
    else
        document.write( "-1");
}

// Driver code
var arr = [1, 5, 3, 3];
var n = arr.length;
findArrangement(arr, n);

// This code is contributed by rrrtnx.
</script>
```

****Output:** 

```
3 5 3 1
```** 

****时间复杂度:** O(N)**

****辅助空间:** O(1)**
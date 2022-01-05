# 在随机整数数组中，将所有 0 移动到开始，将所有 1 移动到结束

> 原文:[https://www . geeksforgeeks . org/将随机整数数组中的所有 0 移动到开头，将所有 1 移动到结尾/](https://www.geeksforgeeks.org/move-all-zeros-to-start-and-ones-to-end-in-an-array-of-random-integers/)

给定一个随机整数的数组 **arr[]** ，任务是将数组中的所有 0 推到数组的开始，将所有 1 推到数组的末尾。请注意，所有其他元素的顺序应该相同。
**例:**

> **输入:** arr[] = {1，2，0，4，3，0，5，0}
> **输出:**0 0 2 4 3 5 1
> T6】输入: arr[] = {1，2，0，0，0，3，6 }；
> **输出:**0 0 2 3 6 1

**方法:**从左到右遍历数组，移动所有不等于开头的 **1** 的元素，然后将 **1 的**放入数组末尾的其余索引中。现在，找到最后一个不等于 **1** 的元素的索引，说 **lastInd** 然后从这个索引开始到数组的开头，把最后所有不等于 **0** 的元素推到 **lastInd** 然后把 **0 的**放在开头。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Utility function to print
// the contents of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function that pushes all the zeros
// to the start and ones to the end of an array
void pushBinaryToBorder(int arr[], int n)
{

    // To store the count of elements
    // which are not equal to 1
    int count1 = 0;

    // Traverse the array and calculate
    // count of elements which are not 1
    for (int i = 0; i < n; i++)
        if (arr[i] != 1)
            arr[count1++] = arr[i];

    // Now all non-ones elements have been shifted to
    // front and 'count1' is set as index of first 1.
    // Make all elements 1 from count to end.
    while (count1 < n)
        arr[count1++] = 1;

    // Initialize lastNonBinary position to zero
    int lastNonOne = 0;

    // Traverse the array and pull non-zero
    // elements to the required indices
    for (int i = n - 1; i >= 0; i--) {

        // Ignore the 1's
        if (arr[i] == 1)
            continue;
        if (!lastNonOne) {

            // Mark the position Of
            // last NonBinary integer
            lastNonOne = i;
        }

        // Place non-zero element to
        // their required indices
        if (arr[i] != 0)
            arr[lastNonOne--] = arr[i];
    }

    // Put zeros to start of array
    while (lastNonOne >= 0)
        arr[lastNonOne--] = 0;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 0, 0, 0, 3, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    pushBinaryToBorder(arr, n);
    printArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Utility function to print
// the contents of an array
static void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(arr[i]+" ");
}

// Function that pushes all the zeros
// to the start and ones to the end of an array
static void pushBinaryToBorder(int arr[], int n)
{

    // To store the count of elements
    // which are not equal to 1
    int count1 = 0;

    // Traverse the array and calculate
    // count of elements which are not 1
    for (int i = 0; i < n; i++)
        if (arr[i] != 1)
            arr[count1++] = arr[i];

    // Now all non-ones elements have been shifted to
    // front and 'count1' is set as index of first 1.
    // Make all elements 1 from count to end.
    while (count1 < n)
        arr[count1++] = 1;

    // Initialize lastNonBinary position to zero
    int lastNonOne = 0;

    // Traverse the array and pull non-zero
    // elements to the required indices
    for (int i = n - 1; i >= 0; i--)
    {

        // Ignore the 1's
        if (arr[i] == 1)
            continue;
        if (lastNonOne == 0)
        {

            // Mark the position Of
            // last NonBinary integer
            lastNonOne = i;
        }

        // Place non-zero element to
        // their required indices
        if (arr[i] != 0)
            arr[lastNonOne--] = arr[i];
    }

    // Put zeros to start of array
    while (lastNonOne >= 0)
        arr[lastNonOne--] = 0;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 2, 0, 0, 0, 3, 6 };
    int n = arr.length;
    pushBinaryToBorder(arr, n);
    printArr(arr, n);

}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print
# the contents of an array
def printArr(arr, n) :

    for i in range(n) :
        print(arr[i],end=" ")

# Function that pushes all the zeros
# to the start and ones to the end of an array
def pushBinaryToBorder(arr, n) :

    # To store the count of elements
    # which are not equal to 1
    count1 = 0

    # Traverse the array and calculate
    # count of elements which are not 1
    for i in range(n) :
        if (arr[i] != 1) :
            arr[count1] = arr[i]
            count1 += 1

    # Now all non-ones elements have been shifted to
    # front and 'count1' is set as index of first 1.
    # Make all elements 1 from count to end.
    while (count1 < n) :
        arr[count1] = 1
        count1 += 1

    # Initialize lastNonBinary position to zero
    lastNonOne = 0

    # Traverse the array and pull non-zero
    # elements to the required indices
    for i in range(n - 1, -1, -1) :

        # Ignore the 1's
        if (arr[i] == 1) :
            continue

        if (not lastNonOne) :

            # Mark the position Of
            # last NonBinary integer
            lastNonOne = i

        # Place non-zero element to
        # their required indices
        if (arr[i] != 0) :
            arr[lastNonOne] = arr[i]
            lastNonOne -= 1

    # Put zeros to start of array
    while (lastNonOne >= 0) :
        arr[lastNonOne] = 0
        lastNonOne -= 1

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 0, 0, 0, 3, 6 ];
    n = len(arr);
    pushBinaryToBorder(arr, n)
    printArr(arr, n)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Utility function to print
// the contents of an array
static void printArr(int []arr, int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Function that pushes all the zeros
// to the start and ones to the end of an array
static void pushBinaryToBorder(int [] arr, int n)
{

    // To store the count of elements
    // which are not equal to 1
    int count1 = 0;

    // Traverse the array and calculate
    // count of elements which are not 1
    for (int i = 0; i < n; i++)
        if (arr[i] != 1)
            arr[count1++] = arr[i];

    // Now all non-ones elements have been shifted to
    // front and 'count1' is set as index of first 1.
    // Make all elements 1 from count to end.
    while (count1 < n)
        arr[count1++] = 1;

    // Initialize lastNonBinary position to zero
    int lastNonOne = 0;

    // Traverse the array and pull non-zero
    // elements to the required indices
    for (int i = n - 1; i >= 0; i--)
    {

        // Ignore the 1's
        if (arr[i] == 1)
            continue;
        if (lastNonOne == 0)
        {

            // Mark the position Of
            // last NonBinary integer
            lastNonOne = i;
        }

        // Place non-zero element to
        // their required indices
        if (arr[i] != 0)
            arr[lastNonOne--] = arr[i];
    }

    // Put zeros to start of array
    while (lastNonOne >= 0)
        arr[lastNonOne--] = 0;
}

// Driver code
public static void Main()
{
    int []arr = { 1, 2, 0, 0, 0, 3, 6 };
    int n = arr.Length;
    pushBinaryToBorder(arr, n);
    printArr(arr, n);
}
}

// This code is contributed by Mohit kumar 29.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Utility function to print
// the contents of an array
function printArr(arr, n)
{
    for (var i = 0; i < n; i++)
        document.write( arr[i] + " ");
}

// Function that pushes all the zeros
// to the start and ones to the end of an array
function pushBinaryToBorder(arr, n)
{

    // To store the count of elements
    // which are not equal to 1
    var count1 = 0;

    // Traverse the array and calculate
    // count of elements which are not 1
    for (var i = 0; i < n; i++)
        if (arr[i] != 1)
            arr[count1++] = arr[i];

    // Now all non-ones elements have been shifted to
    // front and 'count1' is set as index of first 1.
    // Make all elements 1 from count to end.
    while (count1 < n)
        arr[count1++] = 1;

    // Initialize lastNonBinary position to zero
    var lastNonOne = 0;

    // Traverse the array and pull non-zero
    // elements to the required indices
    for (var i = n - 1; i >= 0; i--) {

        // Ignore the 1's
        if (arr[i] == 1)
            continue;
        if (!lastNonOne) {

            // Mark the position Of
            // last NonBinary integer
            lastNonOne = i;
        }

        // Place non-zero element to
        // their required indices
        if (arr[i] != 0)
            arr[lastNonOne--] = arr[i];
    }

    // Put zeros to start of array
    while (lastNonOne >= 0)
        arr[lastNonOne--] = 0;
}

// Driver code
var arr = [ 1, 2, 0, 0, 0, 3, 6 ];
var n = arr.length;
pushBinaryToBorder(arr, n);
printArr(arr, n);

</script>
```

**Output:** 

```
0 0 0 2 3 6 1
```
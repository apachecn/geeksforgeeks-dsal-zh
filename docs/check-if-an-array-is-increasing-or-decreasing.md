# 检查数组是增加还是减少

> 原文:[https://www . geesforgeks . org/check-如果一个数组正在增加或减少/](https://www.geeksforgeeks.org/check-if-an-array-is-increasing-or-decreasing/)

给定一个由 **N** 元素组成的数组 **arr[]** ，其中 **N ≥ 2** ，任务是检查数组的类型是否为:

1.  不断增加。
2.  正在减少。
3.  先增后减。
4.  先减少后增加。

**注意**给定数组肯定是给定类型之一。
**例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:**增加
> **输入:** arr[] = {1，2，4，3}
> **输出:**增加然后减少

**进场:**以下条件必须满足:

1.  **递增数组:**前两个和后两个元素必须按递增顺序排列。
2.  **递减数组:**前两个和后两个元素必须按递减顺序排列。
3.  **先增后减数组:**前两个元素必须按递增顺序排列，后两个元素必须按递减顺序排列。
4.  **先减后增数组:**前两个元素必须按降序排列，后两个元素必须按升序排列。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to check the type of the array
void checkType(int arr[], int n)
{

    // If the first two and the last two elements
    // of the array are in increasing order
    if (arr[0] <= arr[1] && arr[n - 2] <= arr[n - 1])
        cout << "Increasing";

    // If the first two and the last two elements
    // of the array are in decreasing order
    else if (arr[0] >= arr[1] && arr[n - 2] >= arr[n - 1])
        cout << "Decreasing";

    // If the first two elements of the array are in
    // increasing order and the last two elements
    // of the array are in decreasing order
    else if (arr[0] <= arr[1] && arr[n - 2] >= arr[n - 1])
        cout << "Increasing then decreasing";

    // If the first two elements of the array are in
    // decreasing order and the last two elements
    // of the array are in increasing order
    else
        cout << "Decreasing then increasing";
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    checkType(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.math.*;

class GFG
{

    // Function to check the type of the array
    public static void checkType(int arr[], int n)
    {

        // If the first two and the last two elements
        // of the array are in increasing order
        if (arr[0] <= arr[1] &&
            arr[n - 2] <= arr[n - 1])
            System.out.println("Increasing");

        // If the first two and the last two elements
        // of the array are in decreasing order
        else if (arr[0] >= arr[1] &&
                 arr[n - 2] >= arr[n - 1])
            System.out.println("Decreasing");

        // If the first two elements of the array are in
        // increasing order and the last two elements
        // of the array are in decreasing order
        else if (arr[0] <= arr[1] &&
                 arr[n - 2] >= arr[n - 1])
            System.out.println("Increasing then decreasing");

        // If the first two elements of the array are in
        // decreasing order and the last two elements
        // of the array are in increasing order
        else
            System.out.println("Decreasing then increasing");
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = new int[]{ 1, 2, 3, 4 };

        int n = arr.length;

        checkType(arr, n);
    }
}

// This code is contributed by Naman_Garg
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to check the type of the array
def checkType(arr, n):

    # If the first two and the last two elements
    # of the array are in increasing order
    if (arr[0] <= arr[1] and
        arr[n - 2] <= arr[n - 1]) :
        print("Increasing");

    # If the first two and the last two elements
    # of the array are in decreasing order
    elif (arr[0] >= arr[1] and
          arr[n - 2] >= arr[n - 1]) :
        print("Decreasing");

    # If the first two elements of the array are in
    # increasing order and the last two elements
    # of the array are in decreasing order
    elif (arr[0] <= arr[1] and
          arr[n - 2] >= arr[n - 1]) :
        print("Increasing then decreasing");

    # If the first two elements of the array are in
    # decreasing order and the last two elements
    # of the array are in increasing order
    else :
        print("Decreasing then increasing");

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4 ];
    n = len(arr);

    checkType(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    // Function to check the type of the array
    public static void checkType(int []arr, int n)
    {

        // If the first two and the last two elements
        // of the array are in increasing order
        if (arr[0] <= arr[1] &&
            arr[n - 2] <= arr[n - 1])
            Console.Write("Increasing");

        // If the first two and the last two elements
        // of the array are in decreasing order
        else if (arr[0] >= arr[1] &&
                 arr[n - 2] >= arr[n - 1])
            Console.Write("Decreasing");

        // If the first two elements of the array are in
        // increasing order and the last two elements
        // of the array are in decreasing order
        else if (arr[0] <= arr[1] &&
                 arr[n - 2] >= arr[n - 1])
            Console.Write("Increasing then decreasing");

        // If the first two elements of the array are in
        // decreasing order and the last two elements
        // of the array are in increasing order
        else
            Console.Write("Decreasing then increasing");
    }

    // Driver code
    static public void Main ()
    {
        int[] arr = new int[]{ 1, 2, 3, 4 };

        int n = arr.Length;

        checkType(arr, n);
    }
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to check the type of the array
function checkType(arr, n)
{

    // If the first two and the last two elements
    // of the array are in increasing order
    if (arr[0] <= arr[1] && arr[n - 2] <= arr[n - 1])
        document.write("Increasing");

    // If the first two and the last two elements
    // of the array are in decreasing order
    else if (arr[0] >= arr[1] && arr[n - 2] >= arr[n - 1])
        document.write("Decreasing");

    // If the first two elements of the array are in
    // increasing order and the last two elements
    // of the array are in decreasing order
    else if (arr[0] <= arr[1] && arr[n - 2] >= arr[n - 1])
        document.write("Increasing then decreasing");

    // If the first two elements of the array are in
    // decreasing order and the last two elements
    // of the array are in increasing order
    else
        document.write("Decreasing then increasing");
}

// Driver code
    let arr = [ 1, 2, 3, 4 ];
    let n = arr.length;

    checkType(arr, n);

</script>
```

**Output:** 

```
Increasing
```
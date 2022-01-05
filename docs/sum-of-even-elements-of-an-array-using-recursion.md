# 使用递归对数组的偶数元素求和

> 原文:[https://www . geeksforgeeks . org/使用递归的数组偶素之和/](https://www.geeksforgeeks.org/sum-of-even-elements-of-an-array-using-recursion/)

给定一个整数数组 **arr[]** ，任务是从数组中找出偶数元素的和。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6，7，8}
> **输出:** 20
> 2 + 4 + 6 + 8 = 20
> **输入:** arr[] = {4，1，3，6}
> **输出:** 10
> 4 + 6 = 10

**方法:**编写一个递归函数，将数组作为参数，用 sum 变量存储所考虑元素的和和索引。如果所需索引处的当前元素被添加到 sum 中，则不要更新 sum，并再次为下一个索引调用相同的方法。终止条件将是当没有剩余元素需要考虑时，即传递的索引超出了给定数组的界限，打印总和，并在这种情况下返回。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Recursive function to find the sum of
// even elements from the array
void SumOfEven(int arr[], int i, int sum)
{

    // If current index is invalid i.e. all
    // the elements of the array
    // have been traversed
    if (i < 0) {

        // Print the sum
        cout << sum;
        return;
    }

    // If current element is even
    if ((arr[i]) % 2 == 0) {

        // Add it to the sum
        sum += (arr[i]);
    }

    // Recursive call for the next element
    SumOfEven(arr, i - 1, sum);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int sum = 0;

    SumOfEven(arr, n - 1, sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Recursive function to find the sum of
// even elements from the array
static void SumOfEven(int arr[],   
                      int i, int sum)
{

    // If current index is invalid i.e. all
    // the elements of the array
    // have been traversed
    if (i < 0)
    {

        // Print the sum
        System.out.print(sum);
        return;
    }

    // If current element is even
    if ((arr[i]) % 2 == 0)
    {

        // Add it to the sum
        sum += (arr[i]);
    }

    // Recursive call for the next element
    SumOfEven(arr, i - 1, sum);
}

// Driver code
public static void main (String[] args)
              throws java.lang.Exception
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8 };
    int n = arr.length;
    int sum = 0;

    SumOfEven(arr, n - 1, sum);
}
}

// This code is contributed by nidhiva
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Recursive function to find the sum of
# even elements from the array
def SumOfEven(arr, i, sum):

    # If current index is invalid i.e.
    # all the elements of the array
    # have been traversed
    if (i < 0):

        # Print the sum
        print(sum);
        return;

    # If current element is even
    if ((arr[i]) % 2 == 0):

        # Add it to the sum
        sum += (arr[i]);

    # Recursive call for the next element
    SumOfEven(arr, i - 1, sum);

# Driver code
if __name__ == '__main__':
    arr = [ 1, 2, 3, 4, 5, 6, 7, 8 ];
    n = len(arr);
    sum = 0;

    SumOfEven(arr, n - 1, sum);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Recursive function to find the sum of
// even elements from the array
static void SumOfEven(int []arr,
                      int i, int sum)
{

    // If current index is invalid i.e. all
    // the elements of the array
    // have been traversed
    if (i < 0)
    {

        // Print the sum
        Console.Write(sum);
        return;
    }

    // If current element is even
    if ((arr[i]) % 2 == 0)
    {

        // Add it to the sum
        sum += (arr[i]);
    }

    // Recursive call for the next element
    SumOfEven(arr, i - 1, sum);
}

// Driver code
public static void Main (String[] args)
{
    int []arr = { 1, 2, 3, 4, 5, 6, 7, 8 };
    int n = arr.Length;
    int sum = 0;

    SumOfEven(arr, n - 1, sum);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Java script implementation of the approach

// Recursive function to find the sum of
// even elements from the array
function SumOfEven(arr,i,sum)
{

    // If current index is invalid i.e. all
    // the elements of the array
    // have been traversed
    if (i < 0)
    {

        // Print the sum
        document.write(sum);
        return;
    }

    // If current element is even
    if ((arr[i]) % 2 == 0)
    {

        // Add it to the sum
        sum += (arr[i]);
    }

    // Recursive call for the next element
    SumOfEven(arr, i - 1, sum);
}

// Driver code

    let arr = [ 1, 2, 3, 4, 5, 6, 7, 8 ];
    let n = arr.length;
    let sum = 0;

    SumOfEven(arr, n - 1, sum);
    //contributed by bobby
    </script>
```

**Output:** 

```
20
```
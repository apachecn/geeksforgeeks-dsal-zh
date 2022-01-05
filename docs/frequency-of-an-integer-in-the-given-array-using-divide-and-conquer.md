# 使用分治法给定数组中整数的频率

> 原文:[https://www . geesforgeks . org/给定数组中整数的频率使用分治法/](https://www.geeksforgeeks.org/frequency-of-an-integer-in-the-given-array-using-divide-and-conquer/)

给定一个未排序的数组 **arr[]** 和一个整数 **K** ，任务是使用[分治](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/)方法计算给定数组中 **K** 的出现次数。

**示例:**

> **输入:** arr[] = {1，1，2，2，2，2，3}，K = 1
> **输出:** 2
> 
> **输入:** arr[] = {1，1，2，2，2，2，3}，K = 4
> **输出:** 0

**方法:**思路是将数组分成大小相等的两部分，统计每一半出现 **K** 的次数，然后相加。

*   将数组分成两部分，直到数组中只剩下一个元素。
*   检查数组中单个元素是否为 **K** 。如果是 **K** 则返回 **1** 否则 **0** 。
*   将每个元素的返回值相加，找到整个数组中出现的 **K** 。

下面是上述方法的实现:

## C++

```
// C++ implrmrntation of the approach

#include <iostream>
using namespace std;

// Function to return the frequency of x
// in the subarray arr[low...high]
int count(int arr[], int low, int high, int x)
{

    // If the subarray is invalid or the
    // element is not found
    if ((low > high)
        || (low == high && arr[low] != x))
        return 0;

    // If there's only a single element
    // which is equal to x
    if (low == high && arr[low] == x)
        return 1;

    // Divide the array into two parts and
    // then find the count of occurrences
    // of x in both the parts
    return count(arr, low,
                 (low + high) / 2, x)
           + count(arr, 1 + (low + high) / 2,
                   high, x);
}

// Driver code
int main()
{
    int arr[] = { 30, 1, 42, 5, 56, 3, 56, 9 };
    int n = sizeof(arr) / sizeof(int);
    int x = 56;

    cout << count(arr, 0, n - 1, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implrmrntation of the approach

class GFG {

    // Function to return the frequency of x
    // in the subarray arr[low...high]
    static int count(int arr[], int low,
                     int high, int x)
    {

        // If the subarray is invalid or the
        // element is not found
        if ((low > high)
            || (low == high && arr[low] != x))
            return 0;

        // If there's only a single element
        // which is equal to x
        if (low == high && arr[low] == x)
            return 1;

        // Divide the array into two parts and
        // then find the count of occurrences
        // of x in both the parts
        return count(arr, low,
                     (low + high) / 2, x)
            + count(arr, 1 + (low + high) / 2,
                    high, x);
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 30, 1, 42, 5, 56, 3, 56, 9 };
        int n = arr.length;
        int x = 56;
        System.out.print(count(arr, 0, n - 1, x));
    }
}
```

## 蟒蛇 3

```
# Python3 implrmrntation of the approach

# Function to return the frequency of x
# in the subarray arr[low...high]
def count(arr, low, high, x):

    # If the subarray is invalid or the
    # element is not found
    if ((low > high) or (low == high and arr[low] != x)):
        return 0;

    # If there's only a single element
    # which is equal to x
    if (low == high and arr[low] == x):
        return 1;

    # Divide the array into two parts and
    # then find the count of occurrences
    # of x in both the parts
    return count(arr, low, (low + high) // 2, x) +\
    count(arr, 1 + (low + high) // 2, high, x);

# Driver code
if __name__ == '__main__':
    arr = [ 30, 1, 42, 5, 56, 3, 56, 9];
    n = len(arr);
    x = 56;
    print(count(arr, 0, n - 1, x));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implrmrntation of the approach
using System;

class GFG
{

    // Function to return the frequency of x
    // in the subarray arr[low...high]
    static int count(int []arr, int low,
                    int high, int x)
    {

        // If the subarray is invalid or the
        // element is not found
        if ((low > high)
            || (low == high && arr[low] != x))
            return 0;

        // If there's only a single element
        // which is equal to x
        if (low == high && arr[low] == x)
            return 1;

        // Divide the array into two parts and
        // then find the count of occurrences
        // of x in both the parts
        return count(arr, low,
                    (low + high) / 2, x)
            + count(arr, 1 + (low + high) / 2,
                    high, x);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 30, 1, 42, 5, 56, 3, 56, 9 };
        int n = arr.Length;
        int x = 56;
        Console.Write(count(arr, 0, n - 1, x));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implrmrntation of the approach
// Function to return the frequency of x
// in the subarray arr[low...high]

function count(arr, low, high, x) {

    // If the subarray is invalid or the
    // element is not found
    if ((low > high)
        || (low == high && arr[low] != x))
        return 0;

    // If there's only a single element
    // which is equal to x
    if (low == high && arr[low] == x)
        return 1;

    // Divide the array into two parts and
    // then find the count of occurrences
    // of x in both the parts
    return count(arr, low,
        Math.floor((low + high) / 2), x)
        + count(arr, 1 + Math.floor((low + high) / 2),
            high, x);
}

// Driver code

let arr = [30, 1, 42, 5, 56, 3, 56, 9];
let n = arr.length;
let x = 56;

document.write(count(arr, 0, n - 1, x));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(NlogN)
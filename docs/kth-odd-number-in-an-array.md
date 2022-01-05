# 数组中的第 Kth 个奇数

> 原文:[https://www.geeksforgeeks.org/kth-odd-number-in-an-array/](https://www.geeksforgeeks.org/kth-odd-number-in-an-array/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是从给定的数组中找到 **K <sup>第</sup>** 个奇数元素。
**举例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 2
> **输出:** 3
> 3 是来自给定数组
> **的 2 <sup>nd</sup> 奇数元素输入:** arr[] = {2，4，6，18}，K = 5
> **输出:** -1
> 给定数组中没有奇数元素。

**方法:**逐元素遍历数组元素，对于遇到的每个奇数元素，将值 **k** 递减 **1** 。如果 **k** 的值等于 **0** ，则打印当前元素。否则遍历完整数组后，如果 **k** 的值为 **> 0** ，则打印 **-1** ，因为数组中奇数元素的总数为 **< k** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the kth odd element
// from the array
int kthOdd(int arr[], int n, int k)
{

    // Traverse the array
    for (int i = 0; i <= n; i++)
    {

        // If current element is odd
        if ((arr[i] % 2) == 1)
            k--;

        // If kth odd element is found
        if (k == 0)
            return arr[i];
    }

    // Total odd elements in the array are < k
    return -1;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr)/sizeof(arr[0]);
    int k = 2;
    cout << (kthOdd(arr, n, k));
    return 0;
}

// This code is contributed by jit_t
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to return the kth odd element
    // from the array
    static int kthOdd(int arr[], int n, int k)
    {

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // If current element is odd
            if (arr[i] % 2 == 1)
                k--;

            // If kth odd element is found
            if (k == 0)
                return arr[i];
        }

        // Total odd elements in the array are < k
        return -1;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int n = arr.length;
        int k = 2;
        System.out.print(kthOdd(arr, n, k));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the kth odd
# element from the array
def kthOdd (arr, n, k):

    # Traverse the array
    for i in range(n):

        # If current element is odd
        if (arr[i] % 2 == 1):
            k -= 1;

        # If kth odd element is found
        if (k == 0):
            return arr[i];

    # Total odd elements in the
    # array are < k
    return -1;

# Driver code
arr = [ 1, 2, 3, 4, 5 ];
n = len(arr);
k = 2;
print(kthOdd(arr, n, k));

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the kth odd element
    // from the array
    static int kthOdd(int []arr, int n, int k)
    {

        // Traverse the array
        for (int i = 0; i < n; i++)
        {

            // If current element is odd
            if (arr[i] % 2 == 1)
                k--;

            // If kth odd element is found
            if (k == 0)
                return arr[i];
        }

        // Total odd elements in the array are < k
        return -1;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 3, 4, 5 };
        int n = arr.Length;
        int k = 2;
        Console.WriteLine(kthOdd(arr, n, k));
    }
}

// This code is contributed by SoM15242
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the kth odd
// element from the array
function kthOdd ($arr, $n, $k)
{

    // Traverse the array
    for ($i = 0; $i < $n; $i++)
    {

        // If current element is odd
        if ($arr[$i] % 2 == 1)
            $k--;

        // If kth odd element is found
        if ($k == 0)
            return $arr[$i];
    }

    // Total odd elements in the
    // array are < k
    return -1;
}

// Driver code
$arr = array( 1, 2, 3, 4, 5 );
$n = sizeof($arr);
$k = 2;
echo (kthOdd($arr, $n, $k));

// This code is contributed by ajit..
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to return the kth odd element
    // from the array
    function kthOdd(arr , n , k) {

        // Traverse the array
        for (i = 0; i < n; i++) {

            // If current element is odd
            if (arr[i] % 2 == 1)
                k--;

            // If kth odd element is found
            if (k == 0)
                return arr[i];
        }

        // Total odd elements in the array are < k
        return -1;
    }

    // Driver code

        var arr = [ 1, 2, 3, 4, 5 ];
        var n = arr.length;
        var k = 2;
        document.write(kthOdd(arr, n, k));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
3
```
# 将这样的数组划分为最大增加段

> 原文:[https://www . geesforgeks . org/partition-a-array-as-to-max-递增-segments/](https://www.geeksforgeeks.org/partition-an-array-such-into-maximum-increasing-segments/)

给我们一个由 N 个整数组成的数组，我们需要把这个数组分成段，这样一个段的每一个元素都大于前一个段的每一个元素。换句话说，如果我们对这些单独的段进行排序，整个数组就会被排序。我们需要找到一个子阵数最大的有效分区。
**例:**

> arr[] = {3 1 2 4 100 7 9}
> 输出:3
> 您应该将数组划分为以下子数组:(3，1，2)，(4)和(100，7，9)。
> 输入:arr[]= { 2 1 2 3 4 3 }
> 输出:5

**方法**贪婪的方法非常有效，因为它会产生以下算法。找到最短的前缀，使前缀中的所有元素都小于或等于数组其余部分中的元素。
将此前缀视为分区的第一个子数组。对数组的其余部分递归调用相同的算法。实现方面，我们可以为每个前缀预处理一个最大值数组，为每个后缀预处理另一个最小值数组。通过这种方式，我们可以很容易地检查给定的前缀是否是分区子阵列的可行候选。
以下是上述办法的实施:

## C++

```
// C++ program to divide into maximum number of segments

#include <iostream>
using namespace std;

    // Returns the maximum number of sorted subarrays
    // in a valid partition
    int sorted_partitions(int arr[],int n)
    {

        int right_min[n + 1];
        right_min[n] = INT8_MAX;
        for (int i = n - 1; i >= 0; i--) {
            right_min[i] = min(right_min[i + 1], arr[i]);
        }

        // Finding the shortest prefix such that all the elements
        // in the prefix are less than or equal to the elements
        // in the rest of the array.
        int partitions = 0;
        for (int current_max = arr[0], i = 0; i < n; i++) {
            current_max = max(current_max, arr[i]);

            // if current max is less than the right prefix min,
            // we increase number of partitions.
            if (current_max <= right_min[i + 1])
                partitions++;
        }

        return partitions;
    }

    // Driver code
    int main()
    {
        int arr[] = { 3, 1, 2, 4, 100, 7, 9 };
        // Find minimum value from right for every index
        int n = sizeof(arr)/sizeof(arr[0]);

        int ans = sorted_partitions(arr,n);
        cout << ans << endl;
        return 0;

    // This code is contributed by ANKITRAI1
    }
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to divide into maximum number of segments
import java.util.Arrays;

class GFG {

    // Returns the maximum number of sorted subarrays
    // in a valid partition
    static int sorted_partitions(int arr[])
    {
        // Find minimum value from right for every index
        int n = arr.length;
        int[] right_min = new int[n + 1];
        right_min[n] = Integer.MAX_VALUE;
        for (int i = n - 1; i >= 0; i--) {
            right_min[i] = Math.min(right_min[i + 1], arr[i]);
        }

        // Finding the shortest prefix such that all the elements
        // in the prefix are less than or equal to the elements
        // in the rest of the array.
        int partitions = 0;
        for (int current_max = arr[0], i = 0; i < n; i++) {
            current_max = Math.max(current_max, arr[i]);

            // if current max is less than the right prefix min,
            // we increase number of partitions.
            if (current_max <= right_min[i + 1])
                partitions++;
        }

        return partitions;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = new int[] { 3, 1, 2, 4, 100, 7, 9 };
        int ans = sorted_partitions(arr);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to divide into
# maximum number of segments
import sys

# Returns the maximum number of sorted
# subarrays in a valid partition
def sorted_partitions( arr, n):

    right_min = [0] * (n + 1)
    right_min[n] = sys.maxsize
    for i in range(n - 1, -1, -1):
        right_min[i] = min(right_min[i + 1], arr[i])

    # Finding the shortest prefix such that
    # all the elements in the prefix are less
    # than or equal to the elements in the
    # rest of the array.
    partitions = 0
    current_max = arr[0]
    for i in range(n):
        current_max = max(current_max, arr[i])

        # if current max is less than the right
        # prefix min, we increase number of partitions.
        if (current_max <= right_min[i + 1]):
            partitions += 1

    return partitions

# Driver code
arr = [ 3, 1, 2, 4, 100, 7, 9 ]

# Find minimum value from right
# for every index
n = len(arr)
ans = sorted_partitions(arr, n)
print(ans)

# This code is contributed by ita_c
```

## C#

```
// C# program to divide into maximum number of segments
using System;

class GFG {

    // Returns the maximum number of sorted subarrays
    // in a valid partition
    static int sorted_partitions(int []arr)
    {
        // Find minimum value from right for every index
        int n = arr.Length;
        int[] right_min = new int[n + 1];
        right_min[n] =  int.MaxValue;
        for (int i = n - 1; i >= 0; i--) {
            right_min[i] = Math.Min(right_min[i + 1], arr[i]);
        }

        // Finding the shortest prefix such that all the elements
        // in the prefix are less than or equal to the elements
        // in the rest of the array.
        int partitions = 0;
        for (int current_max = arr[0], i = 0; i < n; i++) {
            current_max = Math.Max(current_max, arr[i]);

            // if current max is less than the right prefix min,
            // we increase number of partitions.
            if (current_max <= right_min[i + 1])
                partitions++;
        }

        return partitions;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 3, 1, 2, 4, 100, 7, 9 };
        int ans = sorted_partitions(arr);
        Console.WriteLine(ans);
    }
}
// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to divide into maximum
// number of segments

// Returns the maximum number of
// sorted subarrays in a valid partition
function sorted_partitions($arr, $n)
{

    $right_min[$n + 1] = array();
    $right_min[$n] = PHP_INT_MAX;
    for ( $i = $n - 1; $i >= 0; $i--)
    {
        $right_min[$i] = min($right_min[$i + 1],
                                        $arr[$i]);
    }

    // Finding the shortest prefix such
    // that all the elements in the prefix
    // are less than or equal to the elements
    // in the rest of the array.
    $partitions = 0;
    for ($current_max = $arr[0],
                        $i = 0; $i < $n; $i++)
    {
        $current_max = max($current_max, $arr[$i]);

        // if current max is less than the
        // right prefix min, we increase
        // number of partitions.
        if ($current_max <= $right_min[$i + 1])
            $partitions++;
    }

    return $partitions;
}

// Driver code
$arr = array( 3, 1, 2, 4, 100, 7, 9 );

// Find minimum value from
// right for every index
$n = sizeof($arr);

$ans = sorted_partitions($arr, $n);
echo $ans, "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to divide into maximum number of segments

    // Returns the maximum number of sorted subarrays
    // in a valid partition
    function sorted_partitions(arr)
    {
        // Find minimum value from right for every index
        let n = arr.length;
        let right_min = new Array(n + 1);
        right_min.fill(0);
        right_min[n] =  Number.MAX_VALUE;
        for (let i = n - 1; i >= 0; i--) {
            right_min[i] = Math.min(right_min[i + 1], arr[i]);
        }

        // Finding the shortest prefix such that all the elements
        // in the prefix are less than or equal to the elements
        // in the rest of the array.
        let partitions = 0;
        for (let current_max = arr[0], i = 0; i < n; i++) {
            current_max = Math.max(current_max, arr[i]);

            // if current max is less than the right prefix min,
            // we increase number of partitions.
            if (current_max <= right_min[i + 1])
                partitions++;
        }

        return partitions;
    }

    let arr = [ 3, 1, 2, 4, 100, 7, 9 ];
    let ans = sorted_partitions(arr);
    document.write(ans);

</script>
```

**Output:** 

```
3
```
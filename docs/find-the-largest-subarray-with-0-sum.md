# 求和为 0 的最大子阵长度

> 原文:[https://www . geeksforgeeks . org/find-0-sum-最大的子阵列/](https://www.geeksforgeeks.org/find-the-largest-subarray-with-0-sum/)

给定一个整数数组，求和等于 0 的最长子数组的长度。

**示例:**

```
Input: arr[] = {15, -2, 2, -8, 1, 7, 10, 23};
Output: 5
Explanation: The longest sub-array with 
elements summing up-to 0 is {-2, 2, -8, 1, 7}

Input: arr[] = {1, 2, 3}
Output: 0
Explanation:There is no subarray with 0 sum

Input:  arr[] = {1, 0, 3}
Output:  1
Explanation: The longest sub-array with 
elements summing up-to 0 is {0}
```

**<u>天真方法</u> :** 这涉及到使用两个嵌套循环时使用蛮力。外环用于固定子阵列的起始位置，内环用于子阵列的结束位置，如果元素之和等于零，则增加计数。

**算法:**

1.  逐一考虑所有子阵列，并检查每个子阵列的总和。
2.  运行两个循环:外部循环选择起点 I，内部循环尝试从 I 开始的所有子数组。

**实施:**

## C++

```
/* A simple C++ program to find
largest subarray with 0 sum */
#include <bits/stdc++.h>
using namespace std;

// Returns length of the largest
// subarray with 0 sum
int maxLen(int arr[], int n)
{
    // Initialize result
    int max_len = 0;

    // Pick a starting point
    for (int i = 0; i < n; i++) {

        // Initialize currr_sum for
        // every starting point
        int curr_sum = 0;

        // try all subarrays starting with 'i'
        for (int j = i; j < n; j++) {
            curr_sum += arr[j];

            // If curr_sum becomes 0,
            // then update max_len
            // if required
            if (curr_sum == 0)
                max_len = max(max_len, j - i + 1);
        }
    }
    return max_len;
}

// Driver Code
int main()
{
    int arr[] = { 15, -2, 2, -8, 1, 7, 10, 23 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Length of the longest 0 sum subarray is "
         << maxLen(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the largest subarray
// with 0 sum
class GFG {
    // Returns length of the largest subarray
    // with 0 sum
    static int maxLen(int arr[], int n)
    {
        int max_len = 0;

        // Pick a starting point
        for (int i = 0; i < n; i++) {
            // Initialize curr_sum for every
            // starting point
            int curr_sum = 0;

            // try all subarrays starting with 'i'
            for (int j = i; j < n; j++) {
                curr_sum += arr[j];

                // If curr_sum becomes 0, then update
                // max_len
                if (curr_sum == 0)
                    max_len = Math.max(max_len, j - i + 1);
            }
        }
        return max_len;
    }

    public static void main(String args[])
    {
        int arr[] = { 15, -2, 2, -8, 1, 7, 10, 23 };
        int n = arr.length;
        System.out.println("Length of the longest 0 sum "
                           + "subarray is " + maxLen(arr, n));
    }
}
// This code is contributed by Kamal Rawal
```

## 计算机编程语言

```
# Python program to find the length of largest subarray with 0 sum

# returns the length
def maxLen(arr):

    # initialize result
    max_len = 0

    # pick a starting point
    for i in range(len(arr)):

        # initialize sum for every starting point
        curr_sum = 0

        # try all subarrays starting with 'i'
        for j in range(i, len(arr)):

            curr_sum += arr[j]

            # if curr_sum becomes 0, then update max_len
            if curr_sum == 0:
                max_len = max(max_len, j-i + 1)

    return max_len

# test array
arr = [15, -2, 2, -8, 1, 7, 10, 13]

print "Length of the longest 0 sum subarray is % d" % maxLen(arr)
```

## C#

```
// C# code to find the largest
// subarray with 0 sum
using System;

class GFG {
    // Returns length of the
    // largest subarray with 0 sum
    static int maxLen(int[] arr, int n)
    {
        int max_len = 0;

        // Pick a starting point
        for (int i = 0; i < n; i++) {
            // Initialize curr_sum
            // for every starting point
            int curr_sum = 0;

            // try all subarrays
            // starting with 'i'
            for (int j = i; j < n; j++) {
                curr_sum += arr[j];

                // If curr_sum becomes 0,
                // then update max_len
                if (curr_sum == 0)
                    max_len = Math.Max(max_len,
                                       j - i + 1);
            }
        }
        return max_len;
    }

    // Driver code
    static public void Main()
    {
        int[] arr = { 15, -2, 2, -8,
                      1, 7, 10, 23 };
        int n = arr.Length;
        Console.WriteLine("Length of the longest 0 sum "
                          + "subarray is " + maxLen(arr, n));
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to find
// largest subarray with 0 sum

// Returns length of the
// largest subarray with 0 sum
function maxLen($arr, $n)
{
    $max_len = 0; // Initialize result

    // Pick a starting point
    for ($i = 0; $i < $n; $i++)
    {
        // Initialize currr_sum
        // for every starting point
        $curr_sum = 0;

        // try all subarrays
        // starting with 'i'
        for ($j = $i; $j < $n; $j++)
        {
            $curr_sum += $arr[$j];

            // If curr_sum becomes 0,
            // then update max_len
            // if required
            if ($curr_sum == 0)
            $max_len = max($max_len,
                           $j - $i + 1);
        }
    }
    return $max_len;
}

// Driver Code
$arr = array(15, -2, 2, -8,
              1, 7, 10, 23);
$n = sizeof($arr);
echo "Length of the longest 0 " .
              "sum subarray is ",
                maxLen($arr, $n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
    // Javascript code to find the largest
    // subarray with 0 sum

    // Returns length of the
    // largest subarray with 0 sum
    function maxLen(arr, n)
    {
        let max_len = 0;

        // Pick a starting point
        for (let i = 0; i < n; i++) {
            // Initialize curr_sum
            // for every starting point
            let curr_sum = 0;

            // try all subarrays
            // starting with 'i'
            for (let j = i; j < n; j++) {
                curr_sum += arr[j];

                // If curr_sum becomes 0,
                // then update max_len
                if (curr_sum == 0)
                    max_len = Math.max(max_len, j - i + 1);
            }
        }
        return max_len;
    }

    let arr = [ 15, -2, 2, -8, 1, 7, 10, 23 ];
    let n = arr.length;
    document.write("Length of the longest 0 sum " + "subarray is " + maxLen(arr, n));

</script>
```

**输出:**

```
Length of the longest 0 sum subarray is 5
```

**复杂度分析:**

*   **时间复杂度** : O(n^2)由于嵌套循环的使用。
*   **空间复杂度** : O(1)因为没有使用额外的空间。

**<u>高效方法</u> :** 蛮力解决方案是计算每个子数组的和，并检查和是否为零。现在，让我们尝试通过占用额外的“n”长度空间来提高时间复杂度。新数组将存储该索引之前所有元素的总和。总和索引对将存储在*散列图*中。一个 [**哈希映射**](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 允许在恒定时间内插入和删除键值对。因此，时间复杂性不受影响。因此，如果同一个值在数组中出现两次，就可以保证特定的数组是零和子数组。

**数学证明:**

> 前缀(i) = arr[0] + arr[1] +…+ arr[i]
> 前缀(j) = arr[0] + arr[1] +…+ arr[j]，j > i
> 如果前缀(i) ==前缀(j)，那么前缀(j)–前缀(i) = 0 表示 *arr[i+1] +..+ arr[j] = 0* ，所以一个子阵列有零和，这个子阵列的长度是 j-i+1

**算法:**

1.  创建一个额外的空间，一个由长度 n(前缀)、*一个变量(和)*、*长度(max_len)* 和*一个哈希映射(hm)* 组成的数组，将和索引对存储为键值对。
2.  沿着输入数组从头到尾移动。
3.  对于每个索引，更新 *sum = sum + array[i]的值。*
4.  检查每个索引，无论当前总和是否出现在哈希映射中。
5.  如果存在，将 *max_len* 的值更新为两个索引(当前索引和散列图中的索引)和 *max_len 的最大差值。*
6.  否则，将值 *(sum)* 放入哈希映射中，索引作为键值对。
7.  打印最大长度 *(max_len)。*

以下是上述方法的模拟运行:

![](img/136535deffc59cf545279cdc295aa236.png)

**实施:**

## C++

```
// C++ program to find the length of largest subarray
// with 0 sum
#include <bits/stdc++.h>
using namespace std;

// Returns Length of the required subarray
int maxLen(int arr[], int n)
{
    // Map to store the previous sums
    unordered_map<int, int> presum;

    int sum = 0; // Initialize the sum of elements
    int max_len = 0; // Initialize result

    // Traverse through the given array
    for (int i = 0; i < n; i++) {
        // Add current element to sum
        sum += arr[i];

        if (arr[i] == 0 && max_len == 0)
            max_len = 1;
        if (sum == 0)
            max_len = i + 1;

        // Look for this sum in Hash table
        if (presum.find(sum) != presum.end()) {
            // If this sum is seen before, then update max_len
            max_len = max(max_len, i - presum[sum]);
        }
        else {
            // Else insert this sum with index in hash table
            presum[sum] = i;
        }
    }

    return max_len;
}

// Driver Code
int main()
{
    int arr[] = { 15, -2, 2, -8, 1, 7, 10, 23 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Length of the longest 0 sum subarray is "
         << maxLen(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find maximum length subarray with 0 sum
import java.util.HashMap;

class MaxLenZeroSumSub {

    // Returns length of the maximum length subarray with 0 sum
    static int maxLen(int arr[])
    {
        // Creates an empty hashMap hM
        HashMap<Integer, Integer> hM = new HashMap<Integer, Integer>();

        int sum = 0; // Initialize sum of elements
        int max_len = 0; // Initialize result

        // Traverse through the given array
        for (int i = 0; i < arr.length; i++) {
            // Add current element to sum
            sum += arr[i];

            if (arr[i] == 0 && max_len == 0)
                max_len = 1;

            if (sum == 0)
                max_len = i + 1;

            // Look this sum in hash table
            Integer prev_i = hM.get(sum);

            // If this sum is seen before, then update max_len
            // if required
            if (prev_i != null)
                max_len = Math.max(max_len, i - prev_i);
            else // Else put this sum in hash table
                hM.put(sum, i);
        }

        return max_len;
    }

    // Drive method
    public static void main(String arg[])
    {
        int arr[] = { 15, -2, 2, -8, 1, 7, 10, 23 };
        System.out.println("Length of the longest 0 sum subarray is "
                           + maxLen(arr));
    }
}
```

## 计算机编程语言

```
# A python program to find maximum length subarray
# with 0 sum in o(n) time

# Returns the maximum length
def maxLen(arr):

    # NOTE: Dictonary in python in implemented as Hash Maps
    # Create an empty hash map (dictionary)
    hash_map = {}

    # Initialize result
    max_len = 0

    # Initialize sum of elements
    curr_sum = 0

    # Traverse through the given array
    for i in range(len(arr)):

        # Add the current element to the sum
        curr_sum += arr[i]

        if arr[i] is 0 and max_len is 0:
            max_len = 1

        if curr_sum is 0:
            max_len = i + 1

        # NOTE: 'in' operation in dictionary to search
        # key takes O(1). Look if current sum is seen
        # before
        if curr_sum in hash_map:
            max_len = max(max_len, i - hash_map[curr_sum] )
        else:

            # else put this sum in dictionary
            hash_map[curr_sum] = i

    return max_len

# test array
arr = [15, -2, 2, -8, 1, 7, 10, 13]

print "Length of the longest 0 sum subarray is % d" % maxLen(arr)
```

## C#

```
// C# program to find maximum
// length subarray with 0 sum
using System;
using System.Collections.Generic;

public class MaxLenZeroSumSub {

    // Returns length of the maximum
    // length subarray with 0 sum
    static int maxLen(int[] arr)
    {
        // Creates an empty hashMap hM
        Dictionary<int, int> hM = new Dictionary<int, int>();

        int sum = 0; // Initialize sum of elements
        int max_len = 0; // Initialize result

        // Traverse through the given array
        for (int i = 0; i < arr.GetLength(0); i++) {
            // Add current element to sum
            sum += arr[i];

            if (arr[i] == 0 && max_len == 0)
                max_len = 1;

            if (sum == 0)
                max_len = i + 1;

            // Look this sum in hash table
            int prev_i = 0;
            if (hM.ContainsKey(sum)) {
                prev_i = hM[sum];
            }

            // If this sum is seen before, then update max_len
            // if required
            if (hM.ContainsKey(sum))
                max_len = Math.Max(max_len, i - prev_i);
            else {
                // Else put this sum in hash table
                if (hM.ContainsKey(sum))
                    hM.Remove(sum);

                hM.Add(sum, i);
            }
        }

        return max_len;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 15, -2, 2, -8, 1, 7, 10, 23 };
        Console.WriteLine("Length of the longest 0 sum subarray is "
                          + maxLen(arr));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program to find maximum length subarray with 0 sum

    // Returns length of the maximum length subarray with 0 sum
    function maxLen(arr)
    {
        // Creates an empty hashMap hM
        let hM = new Map();

        let sum = 0; // Initialize sum of elements
        let max_len = 0; // Initialize result

        // Traverse through the given array
        for (let i = 0; i < arr.length; i++) {
            // Add current element to sum
            sum += arr[i];

            if (arr[i] == 0 && max_len == 0)
                max_len = 1;

            if (sum == 0)
                max_len = i + 1;

            // Look this sum in hash table
            let prev_i = hM.get(sum);

            // If this sum is seen before, then update max_len
            // if required
            if (prev_i != null)
                max_len = Math.max(max_len, i - prev_i);
            else // Else put this sum in hash table
                hM.set(sum, i);
        }

        return max_len;
    }

// Driver program

     let arr = [ 15, -2, 2, -8, 1, 7, 10, 23 ];
     document.write("Length of the longest 0 sum subarray is "
                           + maxLen(arr));

</script>
```

**输出:**

```
Length of the longest 0 sum subarray is 5
```

**复杂度分析:**

*   **时间复杂度:** O(n)作为良好散列函数的使用，将允许在 O(1)时间内进行插入和检索操作。
*   **空间复杂度:** O(n)，用于使用额外空间存储前缀数组和 hashmap。
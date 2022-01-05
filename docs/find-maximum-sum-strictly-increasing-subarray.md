# 求最大和严格递增子阵

> 原文:[https://www . geesforgeks . org/find-最大和-严格递增-subarray/](https://www.geeksforgeeks.org/find-maximum-sum-strictly-increasing-subarray/)

给定一个正整数数组。求严格递增子阵的最大和。注意这个问题不同于[最大子阵和](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)和[最大和增子序列](https://www.geeksforgeeks.org/dynamic-programming-set-14-maximum-sum-increasing-subsequence/)问题。

**示例:**

> **输入:** arr[] = {1，2，3，2，5，1，7}
> **输出:** 8
> **解释:**一些严格递增的子阵是
> {1，2，3}和= 6，
> {2，5}和= 7，
> {1，7}和 8
> 最大和= 8
> 
> **输入:** arr[] = {1，2，2，4}
> **输出:** 6
> **说明:**最大和递增子阵为 6。

一个**简单的解决方案**是生成所有可能的子阵，对于每个子阵检查子阵是否严格增加。如果子阵是严格递增的，那么我们计算 sum &更新 max_sum。时间复杂度 O(n <sup>2</sup> )。

这个问题的有效解决方案需要 0(n)时间。其思想是跟踪最大和与当前和。对于每个元素 arr[i]，如果它大于 arr[i-1]，那么我们把它加到当前和上。否则 arr[i]是另一个最大和增量子阵潜在候选的起点，所以我们将当前和更新为数组。但是在更新当前总和之前，如果需要，我们会更新最大总和。

```
Let input array be 'arr[]' and size of array be 'n'

Initialize : 
max_sum = arr[0]// because if array size is 1 than it would return that element.
 // used to store the maximum sum 
current_sum = arr[0] // used to compute current sum 

// Traverse array starting from second element
i goes from 1 to n-1

    // Check if it is strictly increasing then we 
    // update current_sum.
    current_sum = current_sum + arr[i]
    max_sum = max(max_sum, current_sum)// Also needed for subarray having last element.
    // else strictly increasing subarray breaks and 
    // arr[i] is starting point of next potential
    // subarray
    max_sum = max(max_sum, current_sum)
    current_sum = arr[i]

return max(max_sum, current_sum)    
```

以下是上述想法的实现。

## C++

```
// C/C++ program to find the maximum sum of strictly
// increasing subarrays
#include <iostream>
using namespace std;

// Returns maximum sum of strictly increasing
// subarrays
int maxsum_SIS(int arr[], int n)
{
    // Initialize max_sum be 0
    int max_sum = arr[0];

    // Initialize current sum be arr[0]
    int current_sum = arr[0];

    // Traverse array elements after first element.
    for (int i = 1; i < n; i++)
    {
        // update current_sum for
        // strictly increasing subarray
        if (arr[i - 1] < arr[i])
        {
            current_sum = current_sum + arr[i];
            max_sum = max(max_sum, current_sum);
        }

        else // strictly increasing subarray break
        {
            // update max_sum and current_sum ;
            max_sum = max(max_sum, current_sum);
            current_sum = arr[i];
        }
    }

    return max(max_sum, current_sum);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Maximum sum : " << maxsum_SIS(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// maximum sum of strictly increasing subarrays

public class GFG {

    // Returns maximum sum
    // of strictly increasing subarrays
    static int maxsum_SIS(int arr[], int n)
    {
        // Initialize max_sum be 0
        int max_sum = arr[0];

        // Initialize current sum be arr[0]
        int current_sum = arr[0];

        // Traverse array elements after first element.
        for (int i = 1; i < n; i++)
        {
            // update current_sum
            // for strictly increasing subarray
            if (arr[i - 1] < arr[i])
            {
                current_sum = current_sum + arr[i];
                max_sum = Math.max(max_sum, current_sum);
            }
            else // strictly increasing subarray break
            {
                // update max_sum and current_sum ;
                max_sum = Math.max(max_sum, current_sum);
                current_sum = arr[i];
            }
        }

        return Math.max(max_sum, current_sum);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 2, 4 };
        int n = arr.length;
        System.out.println("Maximum sum : "
                           + maxsum_SIS(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the maximum sum of strictly
# increasing subarrays

# Returns maximum sum of strictly increasing
# subarrays

def maxsum_SIS(arr, n):
    # Initialize max_sum be 0
    max_sum = arr[0]

    # Initialize current sum be arr[0]
    current_sum = arr[0]

    # Traverse array elements after first element.
    for i in range(1, n):
        # update current_sum for strictly increasing subarray
        if (arr[i-1] < arr[i]):
            current_sum = current_sum + arr[i]
            max_sum = max(max_sum, current_sum)

        else:
            # strictly increasing subarray break
            # update max_sum and current_sum
            max_sum = max(max_sum, current_sum)
            current_sum = arr[i]

    return max(max_sum, current_sum)

# Driver code

def main():
    arr = [1, 2, 2, 4]
    n = len(arr)

    print("Maximum sum : ", maxsum_SIS(arr, n)),

if __name__ == '__main__':
    main()

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find the maximum sum of strictly
// increasing subarrays
using System;
public class GFG {

    // Returns maximum sum of strictly increasing
    // subarrays
    static int maxsum_SIS(int[] arr, int n)
    {
        // Initialize max_sum be 0
        int max_sum = arr[0];

        // Initialize current sum be arr[0]
        int current_sum = arr[0];

        // Traverse array elements after first element.
        for (int i = 1; i < n; i++) {
            // update current_sum for strictly increasing
            // subarray
            if (arr[i - 1] < arr[i]) {
                current_sum = current_sum + arr[i];
                max_sum = Math.Max(max_sum, current_sum);
            }
            else // strictly increasing subarray break
            {
                // update max_sum and current_sum ;
                max_sum = Math.Max(max_sum, current_sum);
                current_sum = arr[i];
            }
        }

        return Math.Max(max_sum, current_sum);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 2, 2, 4 };
        int n = arr.Length;
        Console.WriteLine("Maximum sum : "
                          + maxsum_SIS(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum sum of
// strictly increasing subarrays

// Returns maximum sum of strictly
// increasing subarrays
function maxsum_SIS($arr , $n)
{
    // Initialize max_sum be 0
    $max_sum = $arr[0];

    // Initialize current sum be arr[0]
    $current_sum = $arr[0];

    // Traverse array elements after
    // first element.
    for ($i = 1; $i < $n ; $i++)
    {
        // update current_sum for strictly
        // increasing subarray
        if ($arr[$i - 1] < $arr[$i]){
            $current_sum = $current_sum + $arr[$i];
            $max_sum = max($max_sum, $current_sum);
    }

        else // strictly increasing
             // subarray break
        {
            // update max_sum and current_sum ;
            $max_sum = max($max_sum, $current_sum);
            $current_sum = $arr[$i];
        }
    }

    return max($max_sum, $current_sum);
}

// Driver Code
$arr = array(1, 2, 2, 4);
$n = sizeof($arr);

echo "Maximum sum : ",
      maxsum_SIS($arr , $n);

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>

// Javascript program to find the maximum sum of strictly
// increasing subarrays

// Returns maximum sum of strictly increasing
// subarrays
function maxsum_SIS(arr, n)
{
    // Initialize max_sum be 0
    var max_sum = arr[0];

    // Initialize current sum be arr[0]
    var current_sum = arr[0];

    // Traverse array elements after first element.
    for (var i = 1; i < n; i++)
    {
        // update current_sum for
        // strictly increasing subarray
        if (arr[i - 1] < arr[i])
        {
            current_sum = current_sum + arr[i];
            max_sum = Math.max(max_sum, current_sum);
        }

        else // strictly increasing subarray break
        {
            // update max_sum and current_sum ;
            max_sum = Math.max(max_sum, current_sum);
            current_sum = arr[i];
        }
    }

    return Math.max(max_sum, current_sum);
}

// Driver code
var arr = [ 1, 2, 2, 4 ];
var n = arr.length;
document.write( "Maximum sum : " + maxsum_SIS(arr, n));

// This code is contributed by itsok.
</script>
```

**Output**

```
Maximum sum : 6
```

***时间复杂度:**O(n)*
T5**辅助空间:** O(1)

本文由 [**尼尚特·辛格(平图)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿，由萨姆拉杰·辛格·索兰基编辑。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
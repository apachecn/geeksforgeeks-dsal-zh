# 给定数组中满足给定条件的最小索引

> 原文:[https://www . geesforgeks . org/满足给定条件的给定数组中的最小索引/](https://www.geeksforgeeks.org/smallest-index-in-the-given-array-that-satisfies-the-given-condition/)

给定一个大小为 **N** 的数组 **arr[]** 和一个整数 **K** ，任务是找到数组中的最小索引，使得:

> **地板(arr[i] / 1) +地板(arr[i + 1] / 2) +地板(arr[i + 2] / 2) + …..+地板(arr[n-1]/n-I)≤K**

如果没有找到这样的索引，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {6，5，4，2}，K = 8
> **输出:**1
> (6/1)+(5/2)+(4/3)+(2/4)= 6+2+1+0 = 9 也就是>K
> (5/1)+(4/2)+(2/3)= 5+2+0 = 7<K
> 因此 i = 1 是必需的指标。
> **输入:** arr[] = {5，4，2，3，9，1，8，7}，K = 7
> **输出:** 5

**逼近:**对于每个指数 **i** 从 **0** 开始，求给定序列的和，给定和大于等于 **K** 的第一个指数就是我们需要的指数。如果没有这样的索引，则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required index
int getIndex(int arr[], int n, int K)
{

    // Check all the indices, the first index
    // satisfying the condition is
    // the required index
    for (int i = 0; i < n; i++) {

        // To store the sum of the series
        int sum = 0;

        // Denominator for the sum series
        int den = 1;

        // Find the sum of the series
        for (int j = i; j < n; j++) {
            sum += (arr[j] / den);

            // Increment the denominator
            den++;

            // If current sum is greater than K
            // no need to execute loop further
            if (sum > K)
                break;
        }

        // Found the first valid index
        if (sum <= K)
            return i;
    }

    return -1;
}

// Driver code
int main()
{
    int arr[] = { 6, 5, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 8;
    cout << getIndex(arr, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the required index
    static int getIndex(int arr[], int n, int K)
    {

        // Check all the indices, the first index
        // satisfying the condition is
        // the required index
        for (int i = 0; i < n; i++) {

            // To store the sum of the series
            int sum = 0;

            // Denominator for the sum series
            int den = 1;

            // Find the sum of the series
            for (int j = i; j < n; j++) {
                sum += (arr[j] / den);

                // Increment the denominator
                den++;

                // If current sum is greater than K
                // no need to execute loop further
                if (sum > K)
                    break;
            }

            // Found the first valid index
            if (sum <= K)
                return i;
        }

        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 6, 5, 4, 2 };
        int n = arr.length;
        int K = 8;
        System.out.print(getIndex(arr, n, K));
    }
}
```

## 计算机编程语言

```
# Python3 implementation of the approach
def getIndex(array, k):
  n = len(array)
  for ind in range(n):
    sum = 0
    div = 1
    for item in array:
      sum += item//div
      div += 1
      if sum > k:
        break
    if sum <= k:
      return ind

  return -1

# Driver code
arr = [6, 5, 4, 2]
K = 8
print(getIndex(arr, K))

arr = [5, 4, 2, 3, 9, 1, 8, 7]
K = 7
print(getIndex(arr, K))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the required index
    static int getIndex(int []arr, int n, int K)
    {

        // Check all the indices, the first index
        // satisfying the condition is
        // the required index
        for (int i = 0; i < n; i++) 
        {

            // To store the sum of the series
            int sum = 0;

            // Denominator for the sum series
            int den = 1;

            // Find the sum of the series
            for (int j = i; j < n; j++) 
            {
                sum += (arr[j] / den);

                // Increment the denominator
                den++;

                // If current sum is greater than K
                // no need to execute loop further
                if (sum > K)
                    break;
            }

            // Found the first valid index
            if (sum <= K)
                return i;
        }

        return -1;
    }

    // Driver code
    static public void Main ()
    {

        int []arr = { 6, 5, 4, 2 };
        int n = arr.Length;
        int K = 8;
        Console.WriteLine(getIndex(arr, n, K));
    }
}

// This Code is contributed by ajit. 
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the required index
function getIndex($arr, $n, $K)
{
    // Check all the indices, the first 
    // index satisfying the condition is
    // the required index
    for ($i = 0; $i < $n; $i++) 
    {

        // To store the sum of the series
        $sum = 0;

        // Denominator for the sum series
        $den = 1;

        // Find the sum of the series
        for ($j = $i; $j < $n; $j++) 
        {
            $sum += floor($arr[$j] / $den);

            // Increment the denominator
            $den++;

            // If current sum is greater than K
            // no need to execute loop further
            if ($sum > $K)
                break;
        }

        // Found the first valid index
        if ($sum <= $K)
            return $i;
    }

    return -1;
}

// Driver code
$arr = array( 6, 5, 4, 2 );
$n = sizeof($arr);
$K = 8;

echo getIndex($arr, $n, $K);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach 

    // Function to return the required index
    function getIndex(arr, n, K)
    {

        // Check all the indices, the first index
        // satisfying the condition is
        // the required index
        for (let i = 0; i < n; i++) 
        {

            // To store the sum of the series
            let sum = 0;

            // Denominator for the sum series
            let den = 1;

            // Find the sum of the series
            for (let j = i; j < n; j++) 
            {
                sum += parseInt((arr[j] / den), 10);

                // Increment the denominator
                den++;

                // If current sum is greater than K
                // no need to execute loop further
                if (sum > K)
                    break;
            }

            // Found the first valid index
            if (sum <= K)
                return i;
        }

        return -1;
    }

    let arr = [ 6, 5, 4, 2 ];
    let n = arr.length;
    let K = 8;
    document.write(getIndex(arr, n, K));

</script>
```

**Output:** 

```
1
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)
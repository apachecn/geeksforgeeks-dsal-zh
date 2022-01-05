# 最接近 K 的子阵列的按位“与”

> 原文:[https://www . geeksforgeeks . org/按位和子数组-最接近 k/](https://www.geeksforgeeks.org/bitwise-and-of-sub-array-closest-to-k/)

给定一个大小为 **N** 的整数数组 **arr[]** 和一个整数 **K** ，任务是找到子数组**arr【I】。j]** 其中 **i ≤ j** 并计算所有子数组元素的按位 and 比如 **X** 然后打印 **X** 所有可能值中的最小值**| K–X |**。

**示例:**

> **输入:** arr[] = {1，6}，K = 3
> **输出:** 2
> 
> <figure class="table">
> 
> | 子阵列 | 按位“与” | &#124; K–X &#124; |
> | --- | --- | --- |
> | {1} | one | Two |
> | {6} | six | three |
> | {1, 6} | one | Two |
> 
> **输入:** arr[] = {4，7，10}，K = 2
> T3】输出: 0
> 
> </figure>

**方法 1:**
求所有可能子数组的按位 AND，并跟踪**| K–X |**的最小可能值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum possible value
// of |K - X| where X is the bitwise AND of
// the elements of some sub-array
int closetAND(int arr[], int n, int k)
{
    int ans = INT_MAX;

    // Check all possible sub-arrays
    for (int i = 0; i < n; i++) {

        int X = arr[i];
        for (int j = i; j < n; j++) {
            X &= arr[j];

            // Find the overall minimum
            ans = min(ans, abs(k - X));
        }
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 4, 7, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    cout << closetAND(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.io.*;

class GFG {

    // Function to return the minimum possible value
    // of |K - X| where X is the bitwise AND of
    // the elements of some sub-array
    static int closetAND(int arr[], int n, int k)
    {
        int ans = Integer.MAX_VALUE;

        // Check all possible sub-arrays
        for (int i = 0; i < n; i++) {

            int X = arr[i];
            for (int j = i; j < n; j++) {
                X &= arr[j];

                // Find the overall minimum
                ans = Math.min(ans, Math.abs(k - X));
            }
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 4, 7, 10 };
        int n = arr.length;
        int k = 2;
        System.out.println(closetAND(arr, n, k));
    }
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the minimum possible value
# of |K - X| where X is the bitwise AND of
# the elements of some sub-array
def closetAND(arr, n, k):

    ans = 10**9

    # Check all possible sub-arrays
    for i in range(n):

        X = arr[i]

        for j in range(i,n):
            X &= arr[j]

            # Find the overall minimum
            ans = min(ans, abs(k - X))

    return ans

# Driver code
arr = [4, 7, 10]
n = len(arr)
k = 2;
print(closetAND(arr, n, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum possible value
    // of |K - X| where X is the bitwise AND of
    // the elements of some sub-array
    static int closetAND(int []arr, int n, int k)
    {
        int ans = int.MaxValue;

        // Check all possible sub-arrays
        for (int i = 0; i < n; i++)
        {

            int X = arr[i];
            for (int j = i; j < n; j++)
            {
                X &= arr[j];

                // Find the overall minimum
                ans = Math.Min(ans, Math.Abs(k - X));
            }
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 4, 7, 10 };
        int n = arr.Length;
        int k = 2;

        Console.WriteLine(closetAND(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum possible value
// of |K - X| where X is the bitwise AND of
// the elements of some sub-array
function closetAND(&$arr, $n, $k)
{
    $ans = PHP_INT_MAX;

    // Check all possible sub-arrays
    for ($i = 0; $i < $n; $i++)
    {

        $X = $arr[$i];
        for ($j = $i; $j < $n; $j++)
        {
            $X &= $arr[$j];

            // Find the overall minimum
            $ans = min($ans, abs($k - $X));
        }
    }
    return $ans;
}

    // Driver code
    $arr = array( 4, 7, 10 );
    $n = sizeof($arr) / sizeof($arr[0]);
    $k = 2;
    echo closetAND($arr, $n, $k);

    return 0;

    // This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum possible value
// of |K - X| where X is the bitwise AND of
// the elements of some sub-array
function closetAND(arr, n, k)
{
    let ans = Number.MAX_VALUE;

    // Check all possible sub-arrays
    for(let i = 0; i < n; i++)
    {
        let X = arr[i];
        for(let j = i; j < n; j++)
        {
            X &= arr[j];

            // Find the overall minimum
            ans = Math.min(ans, Math.abs(k - X));
        }
    }
    return ans;
}

// Driver code
let arr = [4, 7, 10 ];
let n = arr.length;
let k = 2;

document.write(closetAND(arr, n, k));

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
0
```

**时间复杂度:** O(n <sup>2</sup>

**辅助空间:** O(1)

**方法二:**
可以观察到，在子阵列中执行 AND 运算时， **X** 的值可以保持不变或减小，但永远不会增加。
因此，我们将从子数组的第一个元素开始，进行按位“与”运算，并将**| K–X |**与当前最小差值进行比较，直到 **X ≤ K** 为止，因为在此之后**| K–X |**将开始增加。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum possible value
// of |K - X| where X is the bitwise AND of
// the elements of some sub-array
int closetAND(int arr[], int n, int k)
{
    int ans = INT_MAX;

    // Check all possible sub-arrays
    for (int i = 0; i < n; i++) {

        int X = arr[i];
        for (int j = i; j < n; j++) {
            X &= arr[j];

            // Find the overall minimum
            ans = min(ans, abs(k - X));

            // No need to perform more AND operations
            // as |k - X| will increase
            if (X <= k)
                break;
        }
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 4, 7, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    cout << closetAND(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum possible value
// of |K - X| where X is the bitwise AND of
// the elements of some sub-array
static int closetAND(int arr[], int n, int k)
{
    int ans = Integer.MAX_VALUE;

    // Check all possible sub-arrays
    for (int i = 0; i < n; i++)
    {

        int X = arr[i];
        for (int j = i; j < n; j++)
        {
            X &= arr[j];

            // Find the overall minimum
            ans = Math.min(ans, Math.abs(k - X));

            // No need to perform more AND operations
            // as |k - X| will increase
            if (X <= k)
                break;
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 7, 10 };
    int n = arr.length;
    int k = 2;
    System.out.println(closetAND(arr, n, k));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python implementation of the approach
import sys

# Function to return the minimum possible value
# of |K - X| where X is the bitwise AND of
# the elements of some sub-array
def closetAND(arr, n, k):
    ans = sys.maxsize;

    # Check all possible sub-arrays
    for i in range(n):

        X = arr[i];
        for j in range(i,n):
            X &= arr[j];

            # Find the overall minimum
            ans = min(ans, abs(k - X));

            # No need to perform more AND operations
            # as |k - X| will increase
            if (X <= k):
                break;
    return ans;

# Driver code
arr = [4, 7, 10 ];
n = len(arr);
k = 2;
print(closetAND(arr, n, k));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;    

class GFG
{

// Function to return the minimum possible value
// of |K - X| where X is the bitwise AND of
// the elements of some sub-array
static int closetAND(int []arr, int n, int k)
{
    int ans = int.MaxValue;

    // Check all possible sub-arrays
    for (int i = 0; i < n; i++)
    {

        int X = arr[i];
        for (int j = i; j < n; j++)
        {
            X &= arr[j];

            // Find the overall minimum
            ans = Math.Min(ans, Math.Abs(k - X));

            // No need to perform more AND operations
            // as |k - X| will increase
            if (X <= k)
                break;
        }
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 7, 10 };
    int n = arr.Length;
    int k = 2;
    Console.WriteLine(closetAND(arr, n, k));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>   
    // Javascript implementation of the approach

    // Function to return the minimum possible value
    // of |K - X| where X is the bitwise AND of
    // the elements of some sub-array
    function closetAND(arr, n, k)
    {
        let ans = Number.MAX_VALUE;

        // Check all possible sub-arrays
        for (let i = 0; i < n; i++)
        {

            let X = arr[i];
            for (let j = i; j < n; j++)
            {
                X &= arr[j];

                // Find the overall minimum
                ans = Math.min(ans, Math.abs(k - X));

                // No need to perform more AND operations
                // as |k - X| will increase
                if (X <= k)
                    break;
            }
        }
        return ans;
    }

    let arr = [ 4, 7, 10 ];
    let n = arr.length;
    let k = 2;
    document.write(closetAND(arr, n, k));

</script>
```

**Output:** 

```
0
```

**时间复杂度:** O(n <sup>2</sup>

**辅助空间:** O(1)
# 计算绝对差值不超过 K 的数组的最大元素数

> 原文:[https://www . geeksforgeeks . org/count-一个绝对差不超过-k 的数组的最大元素数/](https://www.geeksforgeeks.org/count-maximum-elements-of-an-array-whose-absolute-difference-does-not-exceed-k/)

给定一个数组 **A** 和正整数 **K** 。任务是找出任何一对的绝对差值不超过 **K** 的元素的最大数量。
**举例:**

> **输入:** A[] = {1，26，17，12，15，2}，K = 5
> **输出:** 3
> 有最大 **3** 值，因此每对
> 的绝对差值不超过 K(K=5) ie。，{12，15，17}
> **输入:** A[] = {1，2，5，10，8，3}，K = 4
> **输出:** 4
> 有最大 **4** 值，这样每对
> 的绝对差值不超过 K(K=4) ie。，{1，2，3，5}

**进场:**

1.  给定数组按升序排序。
2.  从索引 i = 0 迭代到 n。
3.  对于每一个 A[i]，计算在 A[i]到 A[i] + K
    范围内的数值。，A[i] < = A[j] < = A[i]+K
4.  返回最大计数

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum elements
// in which absolute difference of any pair
// does not exceed K
int maxCount(int A[], int N, int K)
{
    int maximum = 0;
    int i = 0, j = 0;
    int start = 0;
    int end = 0;

    // Sort the Given array
    sort(A, A + N);

    // Find max elements
    for (i = 0; i < N; i++) {

        // Count all elements which are in range
        // A[i] to A[i] + K
        while (j < N && A[j] <= A[i] + K)
            j++;
        if (maximum < (j - i)) {
            maximum = (j - i);
            start = i;
            end = j;
        }
    }

    // Return the max count
    return maximum;
}

// Driver code
int main()
{
    int A[] = { 1, 26, 17, 12, 15, 2 };
    int N = sizeof(A) / sizeof(A[0]);
    int K = 5;
    cout << maxCount(A, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the maximum elements
// in which absolute difference of any pair
// does not exceed K
static int maxCount(int A[], int N, int K)
{
    int maximum = 0;
    int i = 0, j = 0;
    int start = 0;
    int end = 0;

    // Sort the Given array
    Arrays.sort(A);

    // Find max elements
    for (i = 0; i < N; i++)
    {

        // Count all elements which are in range
        // A[i] to A[i] + K
        while (j < N && A[j] <= A[i] + K)
            j++;
        if (maximum < (j - i))
        {
            maximum = (j - i);
            start = i;
            end = j;
        }
    }

    // Return the max count
    return maximum;
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 1, 26, 17, 12, 15, 2 };
    int N = A.length;
    int K = 5;
    System.out.println(maxCount(A, N, K));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

def maxCount(A, N, K):

    maximum = 0
    start = 0
    end = 0
    j = 0

    # Sort the Array
    A.sort()

    # Find max elements
    for i in range(0, N):
        while(j < N and A[j] <= A[i] + K):
            j += 1
        if maximum < (j - i ):
            maximum = (j - i)
            start = i;
            end = j;

    # Return the maximum
    return maximum

# Driver code
A = [1, 26, 17, 12, 15, 2]
N = len(A)
K = 5

print(maxCount(A, N, K))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum elements
// in which absolute difference of any pair
// does not exceed K
static int maxCount(int []A, int N, int K)
{
    int maximum = 0;
    int i = 0, j = 0;
    int start = 0;
    int end = 0;

    // Sort the Given array
    Array.Sort(A);

    // Find max elements
    for (i = 0; i < N; i++)
    {

        // Count all elements which are in range
        // A[i] to A[i] + K
        while (j < N && A[j] <= A[i] + K)
            j++;
        if (maximum < (j - i))
        {
            maximum = (j - i);
            start = i;
            end = j;
        }
    }

    // Return the max count
    return maximum;
}

// Driver code
public static void Main()
{
    int []A = { 1, 26, 17, 12, 15, 2 };
    int N = A.Length;
    int K = 5;
    Console.Write(maxCount(A, N, K));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return the maximum
// elements in which absolute difference
// of any pair does not exceed K
function maxCount($A, $N, $K)
{
    $maximum = 0;
    $i = 0;
    $j = 0;
    $start = 0;
    $end = 0;

    // Sort the Given array
    sort($A);

    // Find max elements
    for ($i = 0; $i < $N; $i++)
    {

        // Count all elements which
        // are in range A[i] to A[i] + K
        while ($j < $N &&
               $A[$j] <= $A[$i] + $K)
            $j++;
        if ($maximum < ($j - $i))
        {
            $maximum = ($j - $i);
            $start = $i;
            $end = $j;
        }
    }

    // Return the max count
    return $maximum;
}

// Driver code
$A = array( 1, 26, 17, 12, 15, 2 );
$N = Count($A);
$K = 5;
echo maxCount($A, $N, $K);

// This code is contributed
// by Arnab Kundu
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to return the maximum elements
// in which absolute difference of any pair
// does not exceed K
function maxCount(A, N, K)
{
    var maximum = 0;
    var i = 0, j = 0;
    var start = 0;
    var end = 0;

    // Sort the Given array
    A.sort((a,b)=> a-b)

    // Find max elements
    for (i = 0; i < N; i++) {

        // Count all elements which are in range
        // A[i] to A[i] + K
        while (j < N && A[j] <= A[i] + K)
            j++;
        if (maximum < (j - i)) {
            maximum = (j - i);
            start = i;
            end = j;
        }
    }

    // Return the max count
    return maximum;
}

// Driver code
var A = [1, 26, 17, 12, 15, 2 ];
var N = A.length;
var K = 5;
document.write( maxCount(A, N, K));

</script>
```

**Output:** 

```
3
```
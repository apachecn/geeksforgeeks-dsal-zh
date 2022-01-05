# 位置数，使得元素的 K 值大于所有其他元素的总和

> 原文:[https://www . geeksforgeeks . org/position-number-to-element-add-k 大于所有其他元素的总和/](https://www.geeksforgeeks.org/number-of-positions-such-that-adding-k-to-the-element-is-greater-than-sum-of-all-other-elements/)

给定一个数组 **arr[]** 和一个数字 **K** 。任务是找出有效位置 **i** 的数量，使得 **(arr[i] + K)** *大于除 arr[i] 之外的数组* **所有元素的和。
**示例:**** 

```
Input: arr[] = {2, 1, 6, 7} K = 4
Output: 1
Explanation: There is only 1 valid position i.e 4th. 
After adding 4 to the element at 4th position 
it is greater than the sum of all other 
elements of the array.

Input: arr[] = {2, 1, 5, 4} K = 2
Output: 0
Explanation: There is no valid position.
```

**进场:**

1.  首先找到数组中所有元素的和，存储在一个变量中，比如 **sum** 。
2.  现在，遍历数组，对于每个位置 **i** 检查条件**(arr[I]+K)>(sum–arr[I])**是否成立。
3.  如果是，则增加计数器，最后打印计数器的值。

以下是上述方法的实现:

## C++

```
// C++ program to implement above approach

#include <bits/stdc++.h>
using namespace std;

// Function that will find out
// the valid position
int validPosition(int arr[], int N, int K)
{
    int count = 0, sum = 0;

    // find sum of all the elements
    for (int i = 0; i < N; i++) {
        sum += arr[i];
    }

    // adding K to the element and check
    // whether it is greater than sum of
    // all other elements
    for (int i = 0; i < N; i++) {
        if ((arr[i] + K) > (sum - arr[i]))
            count++;
    }

    return count;
}

// Driver code
int main()
{
    int arr[] = { 2, 1, 6, 7 }, K = 4;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << validPosition(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that will find out
// the valid position
static int validPosition(int arr[], int N, int K)
{
    int count = 0, sum = 0;

    // find sum of all the elements
    for (int i = 0; i < N; i++)
    {
        sum += arr[i];
    }

    // adding K to the element and check
    // whether it is greater than sum of
    // all other elements
    for (int i = 0; i < N; i++)
    {
        if ((arr[i] + K) > (sum - arr[i]))
            count++;
    }

    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 1, 6, 7 }, K = 4;
    int N = arr.length;
    System.out.println(validPosition(arr, N, K));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to implement
# above approach

# Function that will find out
# the valid position
def validPosition(arr, N, K):
    count = 0; sum = 0;

    # find sum of all the elements
    for i in range(N):
        sum += arr[i];

    # adding K to the element and check
    # whether it is greater than sum of
    # all other elements
    for i in range(N):
        if ((arr[i] + K) > (sum - arr[i])):
            count += 1;

    return count;

# Driver code
arr = [2, 1, 6, 7 ];
K = 4;
N = len(arr);

print(validPosition(arr, N, K));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that will find out
// the valid position
static int validPosition(int []arr, int N, int K)
{
    int count = 0, sum = 0;

    // find sum of all the elements
    for (int i = 0; i < N; i++)
    {
        sum += arr[i];
    }

    // adding K to the element and check
    // whether it is greater than sum of
    // all other elements
    for (int i = 0; i < N; i++)
    {
        if ((arr[i] + K) > (sum - arr[i]))
            count++;
    }

    return count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 1, 6, 7 };int K = 4;
    int N = arr.Length;
    Console.WriteLine(validPosition(arr, N, K));
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement above approach

// Function that will find out
// the valid position
function validPosition($arr, $N, $K)
{
    $count = 0; $sum = 0;

    // find sum of all the elements
    for ($i = 0; $i < $N; $i++)
    {
        $sum += $arr[$i];
    }

    // adding K to the element and check
    // whether it is greater than sum of
    // all other elements
    for ($i = 0; $i < $N; $i++)
    {
        if (($arr[$i] + $K) > ($sum - $arr[$i]))
            $count++;
    }

    return $count;
}

    // Driver code
    $arr = array( 2, 1, 6, 7 );
    $K = 4;
    $N = count($arr) ;

    echo validPosition($arr, $N, $K);

    // This code is contributed by AnkitRai01

?>
```

## java 描述语言

```
<script>

// Javascript program to implement above approach

// Function that will find out
// the valid position
function validPosition(arr, N, K)
{
    var count = 0, sum = 0;

    // find sum of all the elements
    for (var i = 0; i < N; i++) {
        sum += arr[i];
    }

    // adding K to the element and check
    // whether it is greater than sum of
    // all other elements
    for (var i = 0; i < N; i++) {
        if ((arr[i] + K) > (sum - arr[i]))
            count++;
    }

    return count;
}

// Driver code
var arr = [ 2, 1, 6, 7 ], K = 4;
var N = arr.length;
document.write( validPosition(arr, N, K));

</script>
```

**Output:** 

```
1
```
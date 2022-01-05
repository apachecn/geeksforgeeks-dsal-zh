# 所有子阵列异或|集合 1

> 哎哎哎:# t0]https://www . geeksforgeeks . org/xorg-subarray-xorg/

给定一个整数数组，我们需要得到所有子数组 XOR 的总 XOR，其中子数组 XOR 可以通过 XORing 它的所有元素来获得。
**例:**

```
Input : arr[] = [3, 5, 2, 4, 6]
Output : 7
Total XOR of all subarray XORs is,
(3) ^ (5) ^ (2) ^ (4) ^ (6)
(3^5) ^ (5^2) ^ (2^4) ^ (4^6)
(3^5^2) ^ (5^2^4) ^ (2^4^6)
(3^5^2^4) ^ (5^2^4^6) ^
(3^5^2^4^6) = 7     

Input : arr[] = {1, 2, 3}
Output : 2

Input : arr[] = {1, 2, 3, 4}
Output : 0
```

一个**简单的解决方案**是生成所有的子阵，并计算所有子阵的异或。以下是上述想法的实现:

## C++

```
// C++ program to get total xor of all subarray xors
#include <bits/stdc++.h>
using namespace std;

// Returns XOR of all subarray xors
int getTotalXorOfSubarrayXors(int arr[], int N)
{
    //  initialize result by 0 as (a xor 0 = a)
    int res = 0;

    // select the starting element
    for (int i=0; i<N; i++)

        // select the eNding element
        for (int j=i; j<N; j++)

            // Do XOR of elements in current subarray
            for (int k=i; k<=j; k++)
                res = res ^ arr[k];

    return res;
}

// Driver code to test above methods
int main()
{
    int arr[] = {3, 5, 2, 4, 6};
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << getTotalXorOfSubarrayXors(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to get total XOR
// of all subarray xors
public class GFG {

    // Returns XOR of all subarray xors
    static int getTotalXorOfSubarrayXors(
                          int arr[], int N)
    {

        // initialize result by
        // 0 as (a xor 0 = a)
        int res = 0;

        // select the starting element
        for (int i = 0; i < N; i++)

            // select the eNding element
            for (int j = i; j < N; j++)

            // Do XOR of elements
            // in current subarray
            for (int k = i; k <= j; k++)
                res = res ^ arr[k];

        return res;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = {3, 5, 2, 4, 6};
        int N = arr.length;

        System.out.println(
            getTotalXorOfSubarrayXors(arr, N));
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# python program to get total xor
# of all subarray xors

# Returns XOR of all subarray xors
def getTotalXorOfSubarrayXors(arr, N):

    # initialize result by 0 as
    # (a xor 0 = a)
    res = 0

    # select the starting element
    for i in range(0, N):

        # select the eNding element
        for j in range(i, N):

            # Do XOR of elements in
            # current subarray
            for k in range(i, j + 1):
                res = res ^ arr[k]

    return res

# Driver code to test above methods
arr = [3, 5, 2, 4, 6]
N = len(arr)

print(getTotalXorOfSubarrayXors(arr, N))

# This code is contributed by Sam007.
```

## C#

```
// C# program to get total XOR
// of all subarray xors
using System;

class GFG {

// Returns XOR of all subarray xors
static int getTotalXorOfSubarrayXors(int []arr,
                                     int N)
{

// initialize result by
// 0 as (a xor 0 = a)
int res = 0;

// select the starting element
for (int i = 0; i < N; i++)

    // select the eNding element
    for (int j = i; j < N; j++)

        // Do XOR of elements
        // in current subarray
        for (int k = i; k <= j; k++)
            res = res ^ arr[k];

return res;
}

// Driver Code
static void Main()
{
    int []arr = {3, 5, 2, 4, 6};
    int N = arr.Length;
    Console.Write(getTotalXorOfSubarrayXors(arr, N));
}
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get total
// xor of all subarray xors

// Returns XOR of all subarray xors
function getTotalXorOfSubarrayXors($arr, $N)
{

    // initialize result by
    // 0 as (a xor 0 = a)
    $res = 0;

    // select the starting element
    for($i = 0; $i < $N; $i++)

        // select the eNding element
        for($j = $i; $j < $N; $j++)

            // Do XOR of elements in
            // current subarray
            for($k = $i; $k <= $j; $k++)
                $res = $res ^ $arr[$k];

    return $res;
}

    // Driver code
    $arr = array(3, 5, 2, 4, 6);
    $N = sizeof($arr);
    echo getTotalXorOfSubarrayXors($arr, $N);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Returns XOR of all subarray xors
    function getTotalXorOfSubarrayXors(
                          arr, N)
    {

        // initialize result by
        // 0 as (a xor 0 = a)
        let res = 0;

        // select the starting element
        for (let i = 0; i < N; i++)

            // select the eNding element
            for (let j = i; j < N; j++)

            // Do XOR of elements
            // in current subarray
            for (let k = i; k <= j; k++)
                res = res ^ arr[k];

        return res;
    }

// Driver Code

    // Both a[] and b[] must be of same size.
    let arr = [3, 5, 2, 4, 6];
    let N = arr.length;

    document.write(getTotalXorOfSubarrayXors(arr, N));

// This code is contributed by code_hunt.
</script>
```

输出:

```
7
```

时间复杂度:O(N <sup>3</sup> )
一个**高效的解决方案**是基于枚举所有子阵的思想，我们可以统计每个元素在所有子阵中总共出现的频率，如果一个元素的频率是奇数，那么它就会包含在最终的结果中，否则不会。

```
As in above example, 
3 occurred 5 times,
5 occurred 8 times,
2 occurred 9 times,
4 occurred 8 times,
6 occurred 5 times
So our final result will be xor of all elements which occurred odd number of times
i.e. 3^2^6 = 7

From above occurrence pattern we can observe that number at i-th index will have 
(i + 1) * (N - i) frequency. 
```

所以我们可以对所有元素迭代一次，计算它们的频率，如果它是奇数，那么我们可以将它与结果进行异或运算，从而将其包含在最终结果中。
解的总时间复杂度为 O(N)

## C++

```
// C++ program to get total
// xor of all subarray xors
#include <bits/stdc++.h>
using namespace std;

// Returns XOR of all subarray xors
int getTotalXorOfSubarrayXors(int arr[],
                              int N)
{
    // initialize result by 0
    // as (a XOR 0 = a)
    int res = 0;

    // loop over all elements once
    for (int i = 0; i < N; i++)
    {
        // get the frequency of
        // current element
        int freq = (i + 1) * (N - i);

        // Uncomment below line to print
        // the frequency of arr[i]
        // cout << arr[i] << " " << freq << endl;

        // if frequency is odd, then
        // include it in the result
        if (freq % 2 == 1)
            res = res ^ arr[i];
    }

    // return the result
    return res;
}

// Driver Code
int main()
{
    int arr[] = {3, 5, 2, 4, 6};
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << getTotalXorOfSubarrayXors(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to get total xor
// of all subarray xors
import java.io.*;

public class GFG {

    // Returns XOR of all subarray
    // xors
    static int getTotalXorOfSubarrayXors(
                          int arr[], int N)
    {

        // initialize result by 0
        // as (a XOR 0 = a)
        int res = 0;

        // loop over all elements once
        for (int i = 0; i < N; i++)
        {
            // get the frequency of
            // current element
            int freq = (i + 1) * (N - i);

            // Uncomment below line to print
            // the frequency of arr[i]

            // if frequency is odd, then
            // include it in the result
            if (freq % 2 == 1)
                res = res ^ arr[i];
        }

        // return the result
        return res;
    }

    public static void main(String[] args)
    {

        int arr[] = {3, 5, 2, 4, 6};
        int N = arr.length;
        System.out.println(
            getTotalXorOfSubarrayXors(arr, N));
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python3 program to get total
# xor of all subarray xors

# Returns XOR of all
# subarray xors
def getTotalXorOfSubarrayXors(arr, N):

    # initialize result by 0
    # as (a XOR 0 = a)
    res = 0

    # loop over all elements once
    for i in range(0, N):

        # get the frequency of
        # current element
        freq = (i + 1) * (N - i)

        # Uncomment below line to print
        # the frequency of arr[i]

        # if frequency is odd, then
        # include it in the result
        if (freq % 2 == 1):
            res = res ^ arr[i]

    # return the result
    return res

# Driver Code
arr = [3, 5, 2, 4, 6]
N = len(arr)
print(getTotalXorOfSubarrayXors(arr, N))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to get total xor
// of all subarray xors
using System;

class GFG
{
// Returns XOR of all subarray xors
static int getTotalXorOfSubarrayXors(int []arr,
                                     int N)
{
    // initialize result by 0
    // as (a XOR 0 = a)
    int res = 0;

    // loop over all elements once
    for (int i = 0; i < N; i++)
    {
        // get the frequency of
        // current element
        int freq = (i + 1) * (N - i);

        // Uncomment below line to print
        // the frequency of arr[i]

        // if frequency is odd, then
        // include it in the result
        if (freq % 2 == 1)
            res = res ^ arr[i];
    }

    // return the result
    return res;
}

    // Driver Code
    public static void Main()
    {
    int []arr = {3, 5, 2, 4, 6};
    int N = arr.Length;

    Console.Write(getTotalXorOfSubarrayXors(arr, N));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get total
// xor of all subarray xors

// Returns XOR of all subarray xors
function getTotalXorOfSubarrayXors($arr,
                                   $N)
{

    // initialize result by 0
    // as (a XOR 0 = a)
    $res = 0;

    // loop over all elements once
    for ($i = 0; $i < $N; $i++)
    {

        // get the frequency of
        // current element
        $freq = ($i + 1) * ($N - $i);

        // if frequency is odd, then
        // include it in the result
        if ($freq % 2 == 1)
            $res = $res ^ $arr[$i];
    }

    // return the result
    return $res;
}

    // Driver Code
    $arr = array(3, 5, 2, 4, 6);
    $N = count($arr);

    echo getTotalXorOfSubarrayXors($arr, $N);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to get total
// xor of all subarray xors

// Returns XOR of all subarray xors
function getTotalXorOfSubarrayXors(arr, N)
{
    // initialize result by 0
    // as (a XOR 0 = a)
    let res = 0;

    // loop over all elements once
    for (let i = 0; i < N; i++)
    {
        // get the frequency of
        // current element
        let freq = (i + 1) * (N - i);

        // Uncomment below line to print
        // the frequency of arr[i]
        // cout << arr[i] << " " << freq << endl;

        // if frequency is odd, then
        // include it in the result
        if (freq % 2 == 1)
            res = res ^ arr[i];
    }

    // return the result
    return res;
}

// Driver Code
    let arr = [3, 5, 2, 4, 6];
    let N = arr.length;

    document.write(getTotalXorOfSubarrayXors(arr, N));

</script>
```

**输出:**

```
7
```

**时间复杂度:** O(N)
本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
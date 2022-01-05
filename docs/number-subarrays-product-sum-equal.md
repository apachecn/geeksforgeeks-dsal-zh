# 积和相等的子阵个数

> 原文:[https://www . geesforgeks . org/number-subarrays-product-sum-equal/](https://www.geeksforgeeks.org/number-subarrays-product-sum-equal/)

给定一组 n 个数字。我们需要计算元素的乘积和和相等的子阵的数量

示例:

```
Input  : arr[] = {1, 3, 2}
Output : 4
The subarrays are :
[0, 0] sum = 1, product = 1,
[1, 1] sum = 3, product = 3,
[2, 2] sum = 2, product = 2 and 
[0, 2] sum = 1+3+2=6, product = 1*3*2 = 6

Input : arr[] = {4, 1, 2, 1}
Output : 5
```

想法很简单，我们检查每个子阵列的元素的乘积和和是否相等。如果是，则将计数器变量增加 1

## C++

```
// C++ program to count subarrays with
// same sum and product.
#include<bits/stdc++.h>
using namespace std;

// returns required number of subarrays
int numOfsubarrays(int arr[] , int n)
{
    int count = 0; // Initialize result

    // checking each subarray
    for (int i=0; i<n; i++)
    {
        int product = arr[i];
        int sum = arr[i];
        for (int j=i+1; j<n; j++)
        {
            // checking if product is equal
            // to sum or not
            if (product==sum)
                count++;

            product *= arr[j];
            sum += arr[j];
        }

        if (product==sum)
            count++;
    }
    return count;
}

// driver function
int main()
{
    int arr[] = {1,3,2};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << numOfsubarrays(arr , n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count subarrays with
// same sum and product.

class GFG
{
    // returns required number of subarrays
    static int numOfsubarrays(int arr[] , int n)
    {
        int count = 0; // Initialize result

        // checking each subarray
        for (int i=0; i<n; i++)
        {
            int product = arr[i];
            int sum = arr[i];
            for (int j=i+1; j<n; j++)
            {
                // checking if product is equal
                // to sum or not
                if (product==sum)
                    count++;

                product *= arr[j];
                sum += arr[j];
            }

            if (product==sum)
                count++;
        }
        return count;
    }

    // Driver function
    public static void main(String args[])
    {
        int arr[] = {1,3,2};
        int n = arr.length;
        System.out.println(numOfsubarrays(arr , n));
    }
}
```

## 蟒蛇 3

```
# python program to
# count subarrays with
# same sum and product.

# returns required
# number of subarrays
def numOfsubarrays(arr,n):

    count = 0 # Initialize result

    # checking each subarray
    for i in range(n):

        product = arr[i]
        sum = arr[i]
        for j in range(i+1,n):

            # checking if product is equal
            # to sum or not
            if (product==sum):
                count+=1

            product *= arr[j]
            sum += arr[j]

        if (product==sum):
            count+=1

    return count

# Driver code

arr = [1,3,2]
n =len(arr)
print(numOfsubarrays(arr , n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count subarrays
// with same sum and product.
using System;
class GFG {

    // returns required number
    // of subarrays
    static int numOfsubarrays(int []arr ,
                              int n)
    {

        // Initialize result
        int count = 0;

        // checking each subarray
        for (int i = 0; i < n; i++)
        {
            int product = arr[i];
            int sum = arr[i];
            for (int j = i + 1; j < n; j++)
            {

                // checking if product is
                // equal to sum or not
                if (product == sum)
                    count++;

                product *= arr[j];
                sum += arr[j];
            }

            if (product == sum)
                count++;
        }
        return count;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1,3,2};
        int n = arr.Length;
        Console.Write(numOfsubarrays(arr , n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count subarrays
// with same sum and product.

// function returns required
// number of subarrays
function numOfsubarrays($arr , $n)
{
    // Initialize result
    $count = 0;

    // checking each subarray
    for ($i = 0; $i < $n; $i++)
    {
        $product = $arr[$i];
        $sum = $arr[$i];
        for ($j = $i + 1; $j < $n; $j++)
        {

            // checking if product is
            // equal to sum or not
            if ($product == $sum)
                $count++;

            $product *= $arr[$j];
            $sum += $arr[$j];
        }

        if ($product == $sum)
            $count++;
    }
    return $count;
}

// Driver Code
$arr = array(1, 3, 2);
$n = sizeof($arr);
echo(numOfsubarrays($arr, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to count subarrays
// with same sum and product.

// Returns required number
// of subarrays
function numOfsubarrays(arr, n)
{

    // Initialize result
    let count = 0;

    // Checking each subarray
    for(let i = 0; i < n; i++)
    {
        let product = arr[i];
        let sum = arr[i];

        for(let j = i + 1; j < n; j++)
        {

            // Checking if product is
            // equal to sum or not
            if (product == sum)
                count++;

            product *= arr[j];
            sum += arr[j];
        }

        if (product == sum)
            count++;
    }
    return count;
}

// Driver code
let arr = [ 1, 3, 2 ];
let n = arr.length;

document.write(numOfsubarrays(arr, n));

// This code is contributed by decode2207

</script>
```

输出:

```
4
```

时间复杂度:O(n <sup>2</sup> )

本文由 **Ayush Jha** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
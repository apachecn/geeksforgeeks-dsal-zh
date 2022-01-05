# 所有子阵列异或|集合 2

> 原文:[https://www.geeksforgeeks.org/xor-subarray-xors-set-2/](https://www.geeksforgeeks.org/xor-subarray-xors-set-2/)

给定一个整数数组，我们需要得到所有子阵异或，其中子阵异或可以通过异或它的所有元素来获得。

**示例:**

```
Input : arr[] = [3, 5, 2, 4, 6]
Output : 7
Total XOR of all subarray XORs is,
(3) ^ (5) ^ (2) ^ (4) ^ (6)
(3^5) ^ (5^2) ^ (2^4) ^ (4^6)
(3^5^2) ^ (5^2^4) ^ (2^4^6)
(3^5^2^4) ^ (5^2^4^6) ^
(3^5^2^4^6) = 7     

Input : arr[] = {1, 2, 3, 4}
Output : 0
Total XOR of all subarray XORs is,
(1) ^ (2) ^ (3) ^ (4) ^
(1^2) ^ (2^3) ^ (3^4) ^ 
(1^2^3) ^ (2^3^4) ^
(1^2^3^4) = 0
```

我们已经在下面的帖子中讨论了一个 O(n)解决方案。
[所有子阵列 XOR 的 XOR | Set 1](https://www.geeksforgeeks.org/xor-subarray-xors/)
如上文中所述，第 I 个索引处的元素频率由(i+1)*(N-i)给出，其中 N 是阵列的大小

有 4 种可能的情况:
**情况 1: i 为奇数，N 为奇数**
设 i = 2k+1，N = 2m+1
freq[I]=((2k+1)+1)*((2m+1)-(2k+1))= 4(m-k)(k+1)=偶数
**情况 2: i 为奇数，N 为偶数**
设 i = 2k+1，N = 2m
freq[i] = ((2k+1 N = 2m+1
freq[I]=((2k)+1)*((2m+1)-(2k))= 2k(2m-2k+1)+(2m-2k)+1 =奇数
**情况 4: i 为偶数，N 为偶数**
设 i = 2k，N = 2m
freq[I]=((2k)+1)*((2m)-(2k))= 2(m-k)(2k+1)=偶数

由此我们可以得出结论，如果数组中元素的总数是偶数，那么任何位置的元素频率都是偶数。所以总异或将为 0。如果元素总数为奇数，则偶数位置的元素频率为奇数，奇数位置的元素频率为偶数。所以我们只需要求偶数位置元素的异或。

以下是上述想法的实现:

## C++

```
// C++ program to get total xor of all subarray xors
#include <bits/stdc++.h>
using namespace std;

// Returns XOR of all subarray xors
int getTotalXorOfSubarrayXors(int arr[], int N)
{
    // if even number of terms are there, all
    // numbers will appear even number of times.
    // So result is 0.
    if (N % 2 == 0)
       return 0;

    // else initialize result by 0 as (a xor 0 = a)
    int res = 0;
    for (int i = 0; i<N; i+=2)
        res ^= arr[i];

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
// Java program to get total
// xor of all subarray xors
import java.io.*;

class GFG
{
    // Returns XOR of all
    // subarray xors
    static int getTotalXorOfSubarrayXors(int arr[],
                                         int N)
    {

    // if even number of terms are
    // there, all numbers will appear
    // even number of times. So result is 0.
    if (N % 2 == 0)
    return 0;

    // else initialize result
    // by 0 as (a xor 0 = a)
    int res = 0;
    for (int i = 0; i < N; i += 2)
        res ^= arr[i];

    return res;
    }

    // Driver Code
    public static void main (String[] args)
    {
    int arr[] = {3, 5, 2, 4, 6};
    int N = arr.length;

    System.out.println(
            getTotalXorOfSubarrayXors(arr, N));
    }
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python 3 program to get total xor
# of all subarray xors

# Returns XOR of all subarray xors
def getTotalXorOfSubarrayXors(arr, N):

    # if even number of terms are there,
    # all numbers will appear even number
    # of times. So result is 0.
    if (N % 2 == 0):
        return 0

    # else initialize result by 0
    # as (a xor 0 = a)
    res = 0
    for i in range(0, N, 2):
        res ^= arr[i]

    return res

# Driver code
if __name__ == "__main__":

    arr = [3, 5, 2, 4, 6]
    N = len(arr)
    print(getTotalXorOfSubarrayXors(arr, N))

# This code is contributed by ita_c
```

## C#

```
// C# program to get total
// xor of all subarray xors
using System;

class GFG
{

    // Returns XOR of all
    // subarray xors
    static int getTotalXorOfSubarrayXors(int []arr,
                                         int N)
    {

    // if even number of terms
    // are there, all numbers
    // will appear even number
    // of times. So result is 0.
    if (N % 2 == 0)
    return 0;

    // else initialize result
    // by 0 as (a xor 0 = a)
    int res = 0;
    for (int i = 0; i < N; i += 2)
        res ^= arr[i];

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

// This code is contributed by aj_36
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get total
// xor of all subarray xors

// Returns XOR of all subarray xors
function getTotalXorOfSubarrayXors($arr, $N)
{

    // if even number of terms
    // are there, all numbers
    // will appear even number
    // of times. So result is 0.
    if ($N % 2 == 0)
    return 0;

    // else initialize result
    // by 0 as (a xor 0 = a)
    $res = 0;
    for ($i = 0; $i < $N; $i += 2)
        $res ^= $arr[$i];

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

    // Returns XOR of all
    // subarray xors
    function getTotalXorOfSubarrayXors(arr,N)
    {
        // if even number of terms are 
        // there, all numbers will appear
        // even number of times. So result is 0.
        if (N % 2 == 0)
            return 0;

        // else initialize result
        // by 0 as (a xor 0 = a)
        let  res = 0;
        for (let i = 0; i < N; i += 2)
        {
            res ^= arr[i];
        }
        return res;
    }

    // Driver Code
    let arr=[3, 5, 2, 4, 6];
    let N = arr.length;
    document.write(getTotalXorOfSubarrayXors(arr, N));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
7
```

本文由**里沙布·拉杰·贾**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
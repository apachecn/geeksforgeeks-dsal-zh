# 所有可能子集的异或之和

> 原文:[https://www.geeksforgeeks.org/sum-xor-possible-subsets/](https://www.geeksforgeeks.org/sum-xor-possible-subsets/)

给定一个大小为 n 的数组 arr[]，我们需要找到所有值的总和，这些值来自对子集的所有元素进行异或运算。

```
Input :  arr[] = {1, 5, 6}
Output : 28
Total Subsets = 23
1 = 1
5 = 5
6 = 6
1 ^ 5 = 4
1 ^ 6 = 7
5 ^ 6 = 3
1 ^ 5 ^ 6 = 2
0(empty subset)
Now SUM of all these XORs = 1 + 5 + 6 + 4 +
                            7 + 3 + 2 + 0
                          = 28

Input : arr[] = {1, 2}
Output : 6

```

一种简单的方法是对数组[]元素的所有可能组合进行异或运算，然后对所有值求和。**这种方法的时间复杂度**呈指数增长，因此对于大的 n 值来说不是更好的方法。
一种**高效的**方法是找到关于异或属性的模式。现在再次考虑二进制形式的子集，如:

```
    1 = 001
    5 = 101
    6 = 110
1 ^ 5 = 100
1 ^ 6 = 111
5 ^ 6 = 011
1^5^6 = 010
```

因此，如果我们分析 xor 的所有这些二进制数，我们可以观察到，出现在 i(0 到 n-1)的所有位置的 set 位将正好贡献 2 <sup>n</sup> 的一半。因此，我们可以很容易地将这两个条件强加在 i.
的每个这样的位置上

*   如果 arr[]的任何值已经设置了第 i <sup>个</sup>位集，那么正好一半的 2 <sup>n</sup> 子集将是该形式，因此它们将贡献给 2 <sup>n-1+i</sup> 到最终总和。
*   如果第 i <sup>个</sup>位集没有 arr[]的值，那么我们可以说在所有具有第 i <sup>个</sup>位集的子集中没有项。

以上观点的证明如下:
**例 1:**
假设数组中有 k 个元素，i <sup>第</sup>位置位，k 不为零。
因此，要在 xor 中设置一个带有第 I 位的子集，我们需要它具有奇数个带有第 i <sup>位的元素。
I<sup>th</sup>位未置位选择元素的方式数= 2<sup>(n-k)</sup>
I<sup>th</sup>位置位选择元素的方式数=<sup>k</sup>C<sub>1</sub>+<sup>k</sup>C<sub>3</sub>+<sup>k</sup>C<sub>5</sub>…。= 2 <sup>(k-1)</sup>
总路数= 2 <sup>(n-1)</sup>
这样，对总和的贡献变成，2 <sup>(n+i-1)</sup>
**情况 2:**
如果没有元素设置 i <sup>第</sup>位，即 k = 0，i <sup>第</sup>位对总和的贡献保持为 0。
现在问题归结为检查 arr[]的元素的哪个位置将被设置或不被设置。但是这里有一些技巧，我们不会逐个迭代所有元素，尽管我们可以简单地取所有这些值的或，然后乘以 2 <sup>n-1</sup> ，例如:-</sup> 

```
Take a OR of all arr[] elements, we get 
= 1 | 5 | 6
= 001 | 101 | 110
= 111

Now to find final summation, we can write it down as:-
= 1*2n-1+2 + 1*2n-1+1 + 1*2n-1+0
= 2n-1 * (1*22 + 1*21 + 1*20 )
= 2n-1 * (1112)
= 2n-1 * 7

Put n = 3,  we get
= 28
```

所以最后对于 n 和数组元素的任意值，我们可以简单的说最终的和将是 2 <sup>n-1</sup> 乘以所有输入的按位 or。

## C++

```
// Below is C++ approach to finding the XOR_SUM
#include<bits/stdc++.h>
using namespace std;

// Returns sum of XORs of all subsets
int xorSum(int arr[], int n)
{
    int bits = 0;

    // Finding bitwise OR of all elements
    for (int i=0; i < n; ++i)
        bits |= arr[i];

    int ans = bits * pow(2, n-1);

    return ans;
}

// Driver code
int main()
{
    int arr[] = {1, 5, 6};
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << xorSum(arr, size);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java approach to finding the XOR_SUM
class GFG {

    // Returns sum of XORs of all subsets
    static int xorSum(int arr[], int n)
    {

        int bits = 0;

        // Finding bitwise OR of all elements
        for (int i = 0; i < n; ++i)
            bits |= arr[i];

        int ans = bits * (int)Math.pow(2, n-1);

        return ans;
    }

    // Driver method
    public static void main(String[] args)
    {

        int arr[] = {1, 5, 6};
        int size = arr.length;

        System.out.print(xorSum(arr, size));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 approach to finding the XOR_SUM

# Returns sum of XORs of all subsets
def xorSum(arr, n):

    bits = 0

    # Finding bitwise OR of all elements
    for i in range(n):
        bits |= arr[i]

    ans = bits * pow(2, n-1)

    return ans

# Driver Code
arr = [1, 5, 6]
size = len(arr)
print(xorSum(arr, size))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# approach to finding the XOR_SUM
using System;

class GFG {

    // Returns sum of XORs of all subsets
    static int xorSum(int []arr, int n)
    {

        int bits = 0;

        // Finding bitwise OR of all elements
        for (int i = 0; i < n; ++i)
            bits |= arr[i];

        int ans = bits * (int)Math.Pow(2, n - 1);

        return ans;
    }

    // Driver code
    public static void Main()
    {

        int []arr = {1, 5, 6};
        int size = arr.Length;

        Console.Write(xorSum(arr, size));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to finding the XOR_SUM
// Returns sum of XORs of all subsets

function xorSum($arr, $n)
{
    $bits = 0;

    // Finding bitwise OR
    // of all elements
    for ($i = 0; $i < $n; ++$i)
        $bits |= $arr[$i];

    $ans = $bits * pow(2, $n - 1);

    return $ans;
}

    // Driver code
    $arr = array(1, 5, 6);
    $size = sizeof($arr);
    echo xorSum($arr, $size);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// Below is JavaScript approach to finding the XOR_SUM

// Returns sum of XORs of all subsets
function xorSum(arr, n)
{
    let bits = 0;

    // Finding bitwise OR of all elements
    for (let i=0; i < n; ++i)
        bits |= arr[i];

    let ans = bits * Math.pow(2, n-1);

    return ans;
}

// Driver code

    let arr = [1, 5, 6];
    let size = arr.length;
    document.write(xorSum(arr, size));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
 28
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
**相关问题:**
[给定一个集合，求所有子集的异或。](https://www.geeksforgeeks.org/given-a-set-find-xor-of-the-xors-of-all-subsets/)
[求所有子序列之和的和](https://www.geeksforgeeks.org/find-sum-sum-sub-sequences/)
**参考:**
[http://math . stackexchange . com/questions/712487/求所有子集的异或？newreg = 293 dec 5b 7614 b7fa 4c 50 B4 E4 d 710 a4b](http://math.stackexchange.com/questions/712487/finding-xor-of-all-subsets?newreg=293ddec5b7614b7fa4c50b4e4d710a4b)
本文由[舒巴姆·班萨尔](https://www.facebook.com/banalshubham)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
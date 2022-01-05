# 所有子集的最大元素之和

> 原文:[https://www.geeksforgeeks.org/sum-maximum-elements-subsets/](https://www.geeksforgeeks.org/sum-maximum-elements-subsets/)

给定一个整数数组，我们需要找到所有可能子集的最大数量之和。
**例:**

```
Input  : arr = {3, 2, 5}
Output : 28
Explanation : 
Subsets and their maximum are,
{}            maximum = 0
{3}             maximum = 3
{2}            maximum = 2
{5}            maximum = 5
{3, 2}            maximum = 3
{3, 5}            maximum = 5
{2, 5}            maximum = 5
{3, 2, 5}        maximum = 5
Sum of maximum will be, 0 + 3 + 2 + 5 + 3 + 5 + 5 + 5 = 28,
which will be our answer.
```

一个**简单的解决方案**是迭代数组的所有子集，找到所有子集的最大值，然后在我们的答案中添加它们，但是这种方法会导致我们的时间复杂度呈指数级。
一个**有效的解决方案**是基于一件事，数组的多少个子集有一个特定的元素作为它们的最大值。如上例所示，四个子集的最大值为 5，两个子集的最大值为 3，一个子集的最大值为 2。其思想是计算这些频率对应于阵列的每个元素。一旦我们有了频率，我们就可以将它们与数组值相乘，并将它们相加，这将导致我们的最终结果。
为了找到频率，首先我们按非递增顺序对数组进行排序，当我们站在 a[i]处时，我们知道从 a[i + 1]到 a[N-1]的所有元素都小于 a[i]，因此由这些元素组成的任何子集都将选择 a[i]作为其最大值，因此对应于 a[i]的这些子集的数量将为，2^(n–I–1(由 a[i + 1]到 a[N]的数组元素组成的总子集)。如果对数组的所有元素应用相同的过程，我们将得到我们的最终答案为，
RES = a[0]*2^(n-1)+a[1]*2^(n-2)..+ a[i]*2^(N-i-1) + …..+ a[N-1]*2^(0)
现在，如果我们按原样求解上述方程，在每个指数上计算 2 的幂将需要时间，相反，我们可以改造类似于[霍纳规则](https://www.geeksforgeeks.org/horners-method-polynomial-evaluation/)的方程以简化，
RES = a[n]+2 *(a[n-1]+2 *(a[n-2]+2 *(2 *(a[2]+2 * a[1])…..))))
上述解的总复杂度为 O(N*log(N))

## C++

```
// C/C++ code to find sum of maximum of all subsets of array
#include <bits/stdc++.h>
using namespace std;

// Method returns sum of maximum of all subsets
int sumOfMaximumOfSubsets(int arr[], int N)
{
    //    sorting array in decreasing order
    sort(arr, arr + N, greater<int>());

    //    initializing sum with first element
    int sum = arr[0];
    for (int i = 1; i < N; i++)
    {
        // calculating evaluation similar to horner's rule
        sum = 2 * sum + arr[i];
    }

    return sum;
}

// Driver code to test above methods
int main()
{
    int arr[] = {3, 2, 5};
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << sumOfMaximumOfSubsets(arr, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;
import java.util.Collections;

// Java code to find sum of
// maximum of all subsets of array
class GFG
{

    // Method returns sum of maximum of all subsets
    static int sumOfMaximumOfSubsets(Integer arr[], int N)
    {
        // sorting array in decreasing order
        Arrays.sort(arr, Collections.reverseOrder());

        // initializing sum with first element
        int sum = arr[0];
        for (int i = 1; i < N; i++)
        {
            // calculating evaluation similar to horner's rule
            sum = 2 * sum + arr[i];
        }

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        Integer arr[] = {3, 2, 5};
        int N = arr.length;
        System.out.println(sumOfMaximumOfSubsets(arr, N));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 code to find sum
# of maximum of all subsets
# of array

# Method returns sum of
# maximum of all subsets
def sumOfMaximumOfSubsets(arr, N):

    # sorting array in
    # decreasing order
    arr.sort(reverse = True)

    # initializing sum
    # with first element
    sum = arr[0]
    for i in range(1, N):

        # calculating evaluation
        # similar to horner's rule
        sum = 2 * sum + arr[i]

    return sum

# Driver code
arr = [3, 2, 5]
N = len(arr)
print(sumOfMaximumOfSubsets(arr, N))

# This code is contributed
# by Smitha
```

## C#

```
// C# code to find sum of
// maximum of all subsets of array
using System;

class GFG
{

    // Method returns sum of maximum of all subsets
    static int sumOfMaximumOfSubsets(int []arr, int N)
    {
        // sorting array in decreasing order
        Array.Sort(arr);
        Array.Reverse(arr);

        // initializing sum with first element
        int sum = arr[0];
        for (int i = 1; i < N; i++)
        {
            // calculating evaluation
            // similar to horner's rule
            sum = 2 * sum + arr[i];
        }

        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {3, 2, 5};
        int N = arr.Length;
        Console.WriteLine(sumOfMaximumOfSubsets(arr, N));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find sum of maximum of
// all subsets of array

// Method returns sum of maximum of all subsets
function sumOfMaximumOfSubsets($arr, $N)
{
    // sorting array in decreasing order
    rsort($arr);

    // initializing sum with first element
    $sum = $arr[0];
    for ( $i = 1; $i < $N; $i++)
    {
        // calculating evaluation similar
        // to horner's rule
        $sum = 2 * $sum + $arr[$i];
    }

    return $sum;
}

// Driver Code
$arr = array(3, 2, 5);
$N = count($arr);
echo sumOfMaximumOfSubsets($arr, $N);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>

// JavaScript code to find sum of
// maximum of all subsets of array

// Method returns sum of maximum of all subsets
function sumOfMaximumOfSubsets(arr,N)
{
    // sorting array in decreasing order

    arr.sort((a,b)=>a-b);
    arr.reverse();
    // initializing sum with first element
    let sum = arr[0];
    for (let i = 1; i < N; i++)
    {
        // calculating evaluation similar to horner's rule
        sum = 2 * sum + arr[i];
    }

    return sum;
}

    let arr= [3, 2, 5];
    let N = arr.length;
    document.write(sumOfMaximumOfSubsets(arr, N));

</script>
```

**输出:**

```
28
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
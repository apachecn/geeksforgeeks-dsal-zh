# 两个阵列中 GCD 最大的一对

> 原文:[https://www.geeksforgeeks.org/pair-maximum-gcd-two-arrays/](https://www.geeksforgeeks.org/pair-maximum-gcd-two-arrays/)

给定 n 个整数的两个数组，数组的值很小(值从不超过一个小数字，比如 100)。找出最大 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 的对(x，y)。x 和 y 不能属于同一个数组。如果多个对具有相同的 gcd，那么考虑具有最大和的对。
**例:**

```
Input : a[] = {3, 1, 4, 2, 8}
        b[] = {5, 2, 12, 8, 3}
Output : 8 8
Explanation: The maximum gcd is 8 which is 
of pair(8, 8).  

Input: a[] = {2, 3, 5}
       b[] = {7, 11, 13}
Output: 5 13
Explanation: Every pair has a gcd of 1.
The maximum sum pair with GCD 1 is (5, 13)
```

一种简单的方法是对两个数组中的每一对进行迭代，找出最大可能的 gcd。
一个**高效(只有元素小的时候)**就是应用[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)属性，为此，我们需要预先计算以下事情。

1.  一个 **cnt** 数组，用于标记数组元素的存在。
2.  我们检查从 1 到 N 的所有数字，对于每个倍数，我们检查如果该数字存在，则存储先前存在的数字或当前存在的倍数的最大值。
3.  对另一个阵列也重复步骤 1 和 2。
4.  最后，我们检查第一个和第二个数组中常见的最大倍数，以获得最大 GCD，在的位置存储元素，在第一个数组中存储元素，在第二个数组中存储 b 数组的元素，因此我们打印该对。

以下是上述方法的实施

## C++

```
// CPP program to find maximum GCD pair
// from two arrays
#include <bits/stdc++.h>
using namespace std;

// Find the maximum GCD pair with maximum
// sum
void gcdMax(int a[], int b[], int n, int N)
{
    // array to keep a count of existing elements
    int cnt[N] = { 0 };

    // first[i] and second[i] are going to store
    // maximum multiples of i in a[] and b[]
    // respectively.
    int first[N] = { 0 }, second[N] = { 0 };

    // traverse through the first array to
    // mark the elements in cnt
    for (int i = 0; i < n; ++i)
        cnt[a[i]] = 1;

    // Find maximum multiple of every number
    // in first array
    for (int i = 1; i < N; ++i)
        for (int j = i; j < N; j += i)
            if (cnt[j])
                first[i] = max(first[i], j);

    // Find maximum multiple of every number
    // in second array
    // We re-initialise cnt[] and traverse
    // through the second array to mark the
    // elements in cnt
    memset(cnt, 0, sizeof(cnt));
    for (int i = 0; i < n; ++i)
        cnt[b[i]] = true;
    for (int i = 1; i < N; ++i)
        for (int j = i; j < N; j += i)

            // if the multiple is present in the
            // second array then store the  max
            // of number or the  pre-existing
            // element
            if (cnt[j])
                second[i] = max(second[i], j);

    // traverse for every elements and checks
    // the maximum N that is present in both
    // the arrays
    int i;
    for (i = N - 1; i >= 0; i--)
        if (first[i] && second[i])
            break;

    cout << "Maximum GCD pair with maximum "
            "sum is " << first[i] << " "
         << second[i] << endl;
}

// driver program to test the above function
int main()
{
    int a[] = { 3, 1, 4, 2, 8 };
    int b[] = { 5, 2, 12, 8, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    // Maximum possible value of elements
    // in both arrays.
    int N = 20;

    gcdMax(a, b, n, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// GCD pair from two arrays
class GFG
{

// Find the maximum GCD
// pair with maximum sum
static void gcdMax(int[] a, int[] b,
                   int n, int N)
{
    // array to keep a count
    // of existing elements
    int[] cnt = new int[N];

    // first[i] and second[i]
    // are going to store
    // maximum multiples of
    // i in a[] and b[]
    // respectively.
    int[] first = new int[N];
    int[] second = new int[N];

    // traverse through the
    // first array to mark
    // the elements in cnt
    for (int i = 0; i < n; ++i)
        cnt[a[i]] = 1;

    // Find maximum multiple
    // of every number in
    // first array
    for (int i = 1; i < N; ++i)
        for (int j = i; j < N; j += i)
            if (cnt[j] > 0)
                first[i] = Math.max(first[i], j);

    // Find maximum multiple
    // of every number in second
    // array. We re-initialise
    // cnt[] and traverse through
    // the second array to mark
    // the elements in cnt
    cnt = new int[N];
    for (int i = 0; i < n; ++i)
        cnt[b[i]] = 1;
    for (int i = 1; i < N; ++i)
        for (int j = i; j < N; j += i)

            // if the multiple is present
            // in the second array then
            // store the max of number or
            // the pre-existing element
            if (cnt[j] > 0)
                second[i] = Math.max(second[i], j);

    // traverse for every
    // elements and checks
    // the maximum N that
    // is present in both
    // the arrays
    int x;
    for (x = N - 1; x >= 0; x--)
        if (first[x] > 0 &&
            second[x] > 0)
            break;

    System.out.println(first[x] + " " +
                            second[x]);
}

// Driver Code
public static void main(String[] args)
{
    int[] a = { 3, 1, 4, 2, 8 };
    int[] b = { 5, 2, 12, 8, 3 };
    int n = a.length;

    // Maximum possible
    // value of elements
    // in both arrays.
    int N = 20;

    gcdMax(a, b, n, N);
}
}

// This code is contributed
// by mits
```

## 蟒蛇 3

```
# Python 3 program to find maximum GCD pair
# from two arrays

# Find the maximum GCD pair with maximum
# sum
def gcdMax(a, b, n, N):

    # array to keep a count of existing elements
    cnt = [0]*N

    # first[i] and second[i] are going to store
    # maximum multiples of i in a[] and b[]
    # respectively.
    first = [0]*N
    second = [0]*N

    # traverse through the first array to
    # mark the elements in cnt
    for i in range(n):
        cnt[a[i]] = 1

    # Find maximum multiple of every number
    # in first array
    for i in range(1,N):
        for j in range(i,N,i):
            if (cnt[j]):
                first[i] = max(first[i], j)

    # Find maximum multiple of every number
    # in second array
    # We re-initialise cnt[] and traverse
    # through the second array to mark the
    # elements in cnt
    cnt = [0]*N
    for i in range(n):
        cnt[b[i]] = 1
    for i in range(1,N):
        for j in range(i,N,i):

            # if the multiple is present in the
            # second array then store the max
            # of number or the pre-existing
            # element
            if (cnt[j]>0):
                second[i] = max(second[i], j)

    # traverse for every elements and checks
    # the maximum N that is present in both
    # the arrays

    i = N-1
    while i>= 0:
        if (first[i]>0 and second[i]>0):
            break
        i -= 1

    print( str(first[i]) + " " + str(second[i]))

# driver program to test the above function
if __name__ == "__main__":
    a = [ 3, 1, 4, 2, 8 ]
    b = [ 5, 2, 12, 8, 3 ]
    n = len(a)

    # Maximum possible value of elements
    # in both arrays.
    N = 20
    gcdMax(a, b, n, N)

# this code is contributed by ChitraNayal
```

## C#

```
// C# program to find
// maximum GCD pair
// from two arrays
using System;

class GFG
{
// Find the maximum GCD
// pair with maximum sum
static void gcdMax(int[] a, int[] b,
                   int n, int N)
{
    // array to keep a count
    // of existing elements
    int[] cnt = new int[N];

    // first[i] and second[i]
    // are going to store
    // maximum multiples of
    // i in a[] and b[]
    // respectively.
    int[] first = new int[N];
    int[] second = new int[N];

    // traverse through the
    // first array to mark
    // the elements in cnt
    for (int i = 0; i < n; ++i)
        cnt[a[i]] = 1;

    // Find maximum multiple
    // of every number in
    // first array
    for (int i = 1; i < N; ++i)
        for (int j = i; j < N; j += i)
            if (cnt[j] > 0)
                first[i] = Math.Max(first[i], j);

    // Find maximum multiple
    // of every number in second
    // array. We re-initialise
    // cnt[] and traverse through
    // the second array to mark
    // the elements in cnt
    cnt = new int[N];
    for (int i = 0; i < n; ++i)
        cnt[b[i]] = 1;
    for (int i = 1; i < N; ++i)
        for (int j = i; j < N; j += i)

            // if the multiple is present
            // in the second array then
            // store the max of number or
            // the pre-existing element
            if (cnt[j] > 0)
                second[i] = Math.Max(second[i], j);

    // traverse for every
    // elements and checks
    // the maximum N that
    // is present in both
    // the arrays
    int x;
    for (x = N - 1; x >= 0; x--)
        if (first[x] > 0 &&
            second[x] > 0)
            break;

    Console.WriteLine(first[x] +
                      " " + second[x]);
}

// Driver Code
static int Main()
{
    int[] a = { 3, 1, 4, 2, 8 };
    int[] b = { 5, 2, 12, 8, 3 };
    int n = a.Length;

    // Maximum possible
    // value of elements
    // in both arrays.
    int N = 20;

    gcdMax(a, b, n, N);
    return 0;
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// maximum GCD pair
// from two arrays

// Find the maximum GCD
// pair with maximum
// sum
function gcdMax($a, $b, $n, $N)
{
    // array to keep a count
    // of existing elements
    $cnt = array_fill(0, $N, 0);

    // first[i] and second[i] are
    // going to store maximum
    // multiples of i in a[] and
    // b[] respectively.
    $first = array_fill(0, $N, 0);
    $second = array_fill(0, $N, 0);

    // traverse through the first
    // array to mark the elements
    // in cnt
    for ($i = 0; $i < $n; ++$i)
        $cnt[$a[$i]] = 1;

    // Find maximum multiple
    // of every number in
    // first array
    for ($i = 1; $i < $N; ++$i)
        for ($j = $i; $j < $N; $j += $i)
            if ($cnt[$j])
                $first[$i] = max($first[$i], $j);

    // Find maximum multiple of every
    // number in second array
    // We re-initialise cnt[] and
    // traverse through the second
    // array to mark the elements in cnt
    $cnt = array_fill(0, $N, 0);
    for ($i = 0; $i < $n; $i++)
        $cnt[$b[$i]] = 1;
    for ($i = 1; $i < $N; $i++)
        for ($j = $i; $j < $N; $j += $i)

            // if the multiple is present
            // in the second array then
            // store the max of number or
            // the pre-existing element
            if ($cnt[$j])
                $second[$i] = max($second[$i], $j);

    // traverse for every elements
    // and checks the maximum N
    // that is present in both
    // the arrays
    $x = $N - 1;
    for (; $x >= 0; $x--)
        if ($first[$x] && $second[$x])
            break;

        echo $first[$x] . " " .
             $second[$x] . "\n";
}

// Driver code
$a = array(3, 1, 4, 2, 8);
$b = array(5, 2, 12, 8, 3);
$n = sizeof($a);

// Maximum possible value
// of elements in both arrays.
$N = 20;

gcdMax($a, $b, $n, $N);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum
// GCD pair from two arrays

// Find the maximum GCD
// pair with maximum sum
function gcdMax(a, b, n, N)
{
    // array to keep a count
    // of existing elements
    let cnt = Array.from({length: N},
             (_, i) => 0);

    // first[i] and second[i]
    // are going to store
    // maximum multiples of
    // i in a[] and b[]
    // respectively.
    let first = Array.from({length: N}, (_, i) => 0);
    let second = Array.from({length: N}, (_, i) => 0);

    // traverse through the
    // first array to mark
    // the elements in cnt
    for (let i = 0; i < n; ++i)
        cnt[a[i]] = 1;

    // Find maximum multiple
    // of every number in
    // first array
    for (let i = 1; i < N; ++i)
        for (let j = i; j < N; j += i)
            if (cnt[j] > 0)
                first[i] = Math.max(first[i], j);

    // Find maximum multiple
    // of every number in second
    // array. We re-initialise
    // cnt[] and traverse through
    // the second array to mark
    // the elements in cnt
    cnt = Array.from({length: N}, (_, i) => 0);
    for (let i = 0; i < n; ++i)
        cnt[b[i]] = 1;
    for (let i = 1; i < N; ++i)
        for (let j = i; j < N; j += i)

            // if the multiple is present
            // in the second array then
            // store the max of number or
            // the pre-existing element
            if (cnt[j] > 0)
                second[i] = Math.max(second[i], j);

    // traverse for every
    // elements and checks
    // the maximum N that
    // is present in both
    // the arrays
    let x;
    for (x = N - 1; x >= 0; x--)
        if (first[x] > 0 &&
            second[x] > 0)
            break;

    document.write(first[x] + " " +
                            second[x]);
}

// driver program

    let a = [ 3, 1, 4, 2, 8 ];
    let b = [ 5, 2, 12, 8, 3 ];
    let n = a.length;

    // Maximum possible
    // value of elements
    // in both arrays.
    let N = 20;

    gcdMax(a, b, n, N);

</script>
```

**输出:**

```
8 8
```

**时间复杂度:** O(N Log N + n)。注意 N + (N/2) + (N/3) + …..+1 = N log N .
T3】辅助空间: O(N)
本文由 [**Raj**](https://www.facebook.com/raja.vikramaditya.7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
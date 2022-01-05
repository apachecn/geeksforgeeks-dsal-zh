# 将数组最佳分割为四个部分

> 原文:[https://www . geeksforgeeks . org/将阵列最佳分割为四个部分/](https://www.geeksforgeeks.org/optimal-partition-of-an-array-into-four-parts/)

给定 n 个非负整数的数组。从数组中选择三个索引，即**(0<= index _ 1<= index _ 2<= index _ 3<= n)**，组成四个子集，使得术语 **sum(0，index _ 1)–sum(index _ 1，index_2) + sum(index_2，index _ 3)–sum(index _ 3，n)** 最大可能。
这里，两个指数说 l 和 r 的意思是，和(l，r)将是从 l 到 r 不包含的位置上的子集的所有数字的和(第 l 个元素不计算，第 r 个元素计算)。例如，如果 arr = {-5，3，9，4}，那么从 0 到 4 的每个 I 的 sum(0，1) = -5，sum(0，2) = -2，sum(1，4) = 16 和 sum(i，i) = 0。对于索引 l 和 r 保持 0 < = l < = r < = n。数组中的索引从 0 开始编号。
**例:**

```
Input : arr = {-1, 2, 3}
Output : 0 1 3   
Here, sum(0, 0) = 0
      sum(0, 1) = -1
      sum(1, 3) = 2 + 3 = 5
      sum(3, 3) = 0
Therefore , sum(0, 0) - sum(0, 1) + sum(1, 3) - sum(3, 3) = 4
which is maximum.

Input : arr = {0, 0, -1, 0}
Output : 0 0 0
Here, sum(0, 0) - sum(0, 0) + sum(0, 0) - sum(0, 0) = 0
which is maximum possible.
```

想象同样的任务，但是没有第一项。由于数组的和是固定的，最好的第二段应该是和最大的那一段。这可以在 O(n)中用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来解决。当调用结束于位置 I 的最佳段时，取从 0 到 I(包括 0 和 I)的最小前缀和(从你想要减去最低数字的总和)。
现在让我们迭代第一个片段的所有可能的结尾，并在没有这个片段的数组上解决上面的任务。

## C++

```
// CPP program to find three indices
#include <bits/stdc++.h>
#define max 50009
using namespace std;

// Function to find required indices.
void find_Indices(int arr[], int n){
    int sum[max], k;
    int index_1, index_2, index_3, index;

    // calculating prefix sum from
    // 1 to i for each i.
    for (int i = 1, k = 0; i <= n; i++)
        sum[i] = sum[i-1] + arr[k++];   

    long long ans = -(1e15);
    index_1 = index_2 = index_3 = -1;

    // iterating the loop from 0 to n
    // for all possibilities.
    for (int l = 0; l <= n; l++) {
        int index = 0;
        long long vmin = (1e15);

        // Here, we recalling the best
        // segment to end at position i.
        for (int r = l; r <= n; r++) {

            // taking the minimal prefix
            // sum from 0 to i inclusive.
            if (sum[r] < vmin) {
                vmin = sum[r];
                index = r;
            }

            // calculating the indices.
            if (sum[l] + sum[r] - vmin > ans)
            {
                ans = sum[l] + sum[r] - vmin;
                index_1 = l;
                index_2 = index;
                index_3 = r;
            }
        }
    }

    // Required indices.
    printf("%d %d %d", index_1, index_2, index_3);
}

// Driver function
int main() {
    int arr[] = {-1, 2, 3};
    int n = sizeof(arr)/sizeof(arr[0]);
    find_Indices(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find three indices
class GFG {

    static final int max = 50009;

    // Function to find required indices.
    static void find_Indices(int arr[], int n)
    {

        int sum[] = new int[max];
        int index_1, index_2, index_3, index;
        int k, i;

        // calculating prefix sum from
        // 1 to i for each i.
        for (i = 1, k = 0; i <= n; i++)
            sum[i] = sum[i - 1] + arr[k++];

        double ans = -(1e15);
        index_1 = index_2 = index_3 = -1;

        // iterating the loop from 0 to n
        // for all possibilities.
        for (int l = 0; l <= n; l++) {
            index = 0;
            double vmin = (1e15);

            // Here, we recalling the best
            // segment to end at position i.
            for (int r = l; r <= n; r++) {

                // taking the minimal prefix
                // sum from 0 to i inclusive.
                if (sum[r] < vmin)
                {
                    vmin = sum[r];
                    index = r;
                }

                // calculating the indices.
                if (sum[l] + sum[r] - vmin > ans)
                {
                    ans = sum[l] + sum[r] - vmin;
                    index_1 = l;
                    index_2 = index;
                    index_3 = r;
                }
            }
        }

        // Required indices.
        System.out.print(index_1 + " " + index_2 +
                                    " " + index_3);
    }

    // Driver function.
    public static void main(String[] args)
    {
        int arr[] = { -1, 2, 3 };
        int n = arr.length;

        find_Indices(arr, n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to
# find three indices

max = 50009

# Function to find
# required indices.
def find_Indices(arr, n):

    sum=[0 for i in range(max)]

    # calculating prefix sum from
    # 1 to i for each i.
    k=0
    for i in range(1,n+1):
        sum[i] = sum[i-1] + arr[k];
        k+=1

    ans = -(1e15)
    index_1 = index_2 = index_3 = -1

    # iterating the loop from 0 to n
    # for all possibilities.
    for l in range(n+1):
        index = 0
        vmin = (1e15)

        # Here, we recalling the best
        # segment to end at position i.
        for r in range(l,n+1):

            # taking the minimal prefix
            # sum from 0 to i inclusive.
            if (sum[r] < vmin):
                vmin = sum[r]
                index = r

            # calculating the indices.
            if (sum[l] + sum[r] - vmin > ans):

                ans = sum[l] + sum[r] - vmin
                index_1 = l
                index_2 = index
                index_3 = r

    # Required indices.
    print(index_1," ", index_2," ", index_3)

# Driver function

arr = [-1, 2, 3]
n = len(arr)
find_Indices(arr, n)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find three indices
using System;

class GFG {

    static int max = 50009;

    // Function to find required indices.
    static void find_Indices(int []arr, int n)
    {

        int []sum = new int[max];
        int index_1, index_2, index_3, index;
        int k, i;

        // calculating prefix sum from
        // 1 to i for each i.
        for (i = 1, k = 0; i <= n; i++)
            sum[i] = sum[i - 1] + arr[k++];

        double ans = -(1e15);
        index_1 = index_2 = index_3 = -1;

        // iterating the loop from 0 to n
        // for all possibilities.
        for (int l = 0; l <= n; l++) {
            index = 0;
            double vmin = (1e15);

            // Here, we recalling the best
            // segment to end at position i.
            for (int r = l; r <= n; r++) {

                // taking the minimal prefix
                // sum from 0 to i inclusive.
                if (sum[r] < vmin)
                {
                    vmin = sum[r];
                    index = r;
                }

                // calculating the indices.
                if (sum[l] + sum[r] - vmin > ans)
                {
                    ans = sum[l] + sum[r] - vmin;
                    index_1 = l;
                    index_2 = index;
                    index_3 = r;
                }
            }
        }

        // Required indices.
        Console.WriteLine(index_1 + " " + index_2 +
                                    " " + index_3);
    }

    // Driver function.
    public static void Main()
    {
        int []arr = { -1, 2, 3 };
        int n = arr.Length;

        find_Indices(arr, n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to
// find three indices
$max = 50009;

// Function to find
// required indices.
function find_Indices($arr, $n)
{

    global $max;
    $sum = array(); $k = 0;
    $sum[0] = 0;

    // calculating prefix sum
    // from 1 to i for each i.
    for ($i = 1, $k = 0;
         $i <= $n; $i++)
        $sum[$i] = $sum[$i - 1] +
                   $arr[$k++];

    $ans = -(1000000000000000);
    $index_1 = $index_2 = $index_3 = -1;

    // iterating the loop from
    // 0 to n for all possibilities.
    for ($l = 0; $l <= $n; $l++)
    {
        $index = 0;
        $vmin = (1000000000000000);

        // Here, we recalling the
        // best segment to end at
        // position i.
        for ($r = $l; $r <= $n; $r++)
        {

            // taking the minimal prefix
            // sum from 0 to i inclusive.
            if ($sum[$r] < $vmin)
            {
                $vmin = $sum[$r];
                $index = $r;
            }

            // calculating the indices.
            if ($sum[$l] + $sum[$r] -
                $vmin > $ans)
            {
                $ans = $sum[$l] +
                       $sum[$r] - $vmin;
                $index_1 = $l;
                $index_2 = $index;
                $index_3 = $r;
            }
        }
    }

    // Required indices.
    echo($index_1." ".$index_2.
                  " ".$index_3." ");
}

// Driver Code
$arr = array(-1, 2, 3);
$n = count($arr);
find_Indices($arr, $n);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>
// Javascript program to
// find three indices
let max = 50009;

// Function to find
// required indices.
function find_Indices(arr, n)
{

    let sum = new Array(); k = 0;
    sum[0] = 0;

    // calculating prefix sum
    // from 1 to i for each i.
    for (let i = 1, k = 0;
        i <= n; i++)
        sum[i] = sum[i - 1] +
                arr[k++];

    let ans = -(1000000000000000);
    let index_1 = index_2 = index_3 = -1;

    // iterating the loop from
    // 0 to n for all possibilities.
    for (let l = 0; l <= n; l++)
    {
        let index = 0;
        let vmin = (1000000000000000);

        // Here, we recalling the
        // best segment to end at
        // position i.
        for (let r = l; r <= n; r++)
        {

            // taking the minimal prefix
            // sum from 0 to i inclusive.
            if (sum[r] < vmin)
            {
                vmin = sum[r];
                index = r;
            }

            // calculating the indices.
            if (sum[l] + sum[r] -
                vmin > ans)
            {
                ans = sum[l] +
                    sum[r] - vmin;
                index_1 = l;
                index_2 = index;
                index_3 = r;
            }
        }
    }

    // Required indices.
    document.write(index_1 + " " + index_2 +" " + index_3 + " ");
}

// Driver Code
let arr = new Array(-1, 2, 3);
let n = arr.length;
find_Indices(arr, n);

// This code is contributed by
// _saurabh_jaiswal
</script>
```

**输出:**

```
0 1 3
```

**时间复杂度:** ![O(n^2).   ](img/656eeeac09f83129db1347c44a822577.png "Rendered by QuickLaTeX.com")
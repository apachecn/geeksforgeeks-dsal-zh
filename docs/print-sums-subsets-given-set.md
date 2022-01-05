# 打印给定集合的所有子集的总和

> 原文:[https://www.geeksforgeeks.org/print-sums-subsets-given-set/](https://www.geeksforgeeks.org/print-sums-subsets-given-set/)

给定一个整数数组，打印其中所有子集的和。输出总和可以以任何顺序打印。

**示例:**

```
Input : arr[] = {2, 3}
Output: 0 2 3 5

Input : arr[] = {2, 4, 5}
Output : 0 2 4 5 6 7 9 11
```

**方法 1(递归)**
我们可以递归解决这个问题。总共有 2 个 <sup>n 个</sup>子集。对于每个元素，我们考虑两个选择，我们将它包含在一个子集中，而不将其包含在一个子集中。以下是基于这一思想的递归解决方案。

## C++

```
// C++ program to print sums of all possible
// subsets.
#include <bits/stdc++.h>
using namespace std;

// Prints sums of all subsets of arr[l..r]
void subsetSums(int arr[], int l, int r, int sum = 0)
{
    // Print current subset
    if (l > r) {
        cout << sum << " ";
        return;
    }

    // Subset including arr[l]
    subsetSums(arr, l + 1, r, sum + arr[l]);

    // Subset excluding arr[l]
    subsetSums(arr, l + 1, r, sum);
}

// Driver code
int main()
{
    int arr[] = { 5, 4, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    subsetSums(arr, 0, n - 1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print sums
// of all possible subsets.
import java.io.*;

class GFG {

    // Prints sums of all
    // subsets of arr[l..r]
    static void subsetSums(int[] arr, int l, int r, int sum)
    {

        // Print current subset
        if (l > r) {
            System.out.print(sum + " ");
            return;
        }

        // Subset including arr[l]
        subsetSums(arr, l + 1, r, sum + arr[l]);

        // Subset excluding arr[l]
        subsetSums(arr, l + 1, r, sum);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 5, 4, 3 };
        int n = arr.length;

        subsetSums(arr, 0, n - 1, 0);
    }
}

// This code is contributed by anuj_67
```

## 蟒蛇 3

```
# Python3 program to print sums of
# all possible subsets.

# Prints sums of all subsets of arr[l..r]

def subsetSums(arr, l, r, sum=0):

    # Print current subset
    if l > r:
        print(sum, end=" ")
        return

    # Subset including arr[l]
    subsetSums(arr, l + 1, r, sum + arr[l])

    # Subset excluding arr[l]
    subsetSums(arr, l + 1, r, sum)

# Driver code
arr = [5, 4, 3]
n = len(arr)
subsetSums(arr, 0, n - 1)

# This code is contributed by Shreyanshi Arun.
```

## C#

```
// C# program to print sums of all possible
// subsets.
using System;

class GFG {

    // Prints sums of all subsets of
    // arr[l..r]
    static void subsetSums(int[] arr, int l, int r, int sum)
    {

        // Print current subset
        if (l > r) {
            Console.Write(sum + " ");
            return;
        }

        // Subset including arr[l]
        subsetSums(arr, l + 1, r, sum + arr[l]);

        // Subset excluding arr[l]
        subsetSums(arr, l + 1, r, sum);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 5, 4, 3 };
        int n = arr.Length;

        subsetSums(arr, 0, n - 1, 0);
    }
}

// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print sums
// of all possible subsets.

// Prints sums of all
// subsets of arr[l..r]
function subsetSums($arr, $l,
                    $r, $sum = 0)
{
    // Print current subset
    if ($l > $r)
    {
        echo $sum , " ";
        return;
    }

    // Subset including arr[l]
    subsetSums($arr, $l + 1, $r,
               $sum + $arr[$l]);

    // Subset excluding arr[l]
    subsetSums($arr, $l + 1, $r, $sum);
}

// Driver code
$arr = array(5, 4, 3);
$n = count($arr);

subsetSums($arr, 0, $n - 1);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to program to print
// sums of all possible subsets.

// Prints sums of all
// subsets of arr[l..r]
function subsetSums(arr, l, r, sum)
{

    // Print current subset
    if (l > r)
    {
        document.write(sum + " ");
        return;
    }

    // Subset including arr[l]
    subsetSums(arr, l + 1, r,
               sum + arr[l]);

    // Subset excluding arr[l]
    subsetSums(arr, l + 1, r, sum);
}

// Driver code
let arr = [5, 4, 3];
let n = arr.length;

subsetSums(arr, 0, n - 1, 0);

// This code is contributed by code_hunt

</script>
```

**输出:**

```
12 9 8 5 7 4 3 0
```

**这个解的时间复杂度是 O(2^n)，空间复杂度是 O(2^n).**

**方法 2(迭代)**
如上所述，总共有 2 个 <sup>n 个</sup>子集。想法是生成从 0 到 2<sup>n</sup>–1 的循环。对于每个数字，选择当前数字的二进制表示中对应于 1 的所有数组元素。

## C++

```
// Iterative C++ program to print sums of all
// possible subsets.
#include <bits/stdc++.h>
using namespace std;

// Prints sums of all subsets of array
void subsetSums(int arr[], int n)
{
    // There are totoal 2^n subsets
    long long total = 1 << n;

    // Consider all numbers from 0 to 2^n - 1
    for (long long i = 0; i < total; i++) {
        long long sum = 0;

        // Consider binary representation of
        // current i to decide which elements
        // to pick.
        for (int j = 0; j < n; j++)
            if (i & (1 << j))
                sum += arr[j];

        // Print sum of picked elements.
        cout << sum << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 5, 4, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    subsetSums(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java program to print sums of all
// possible subsets.
import java.util.*;

class GFG {

    // Prints sums of all subsets of array
    static void subsetSums(int arr[], int n)
    {

        // There are totoal 2^n subsets
        int total = 1 << n;

        // Consider all numbers from 0 to 2^n - 1
        for (int i = 0; i < total; i++) {
            int sum = 0;

            // Consider binary representation of
            // current i to decide which elements
            // to pick.
            for (int j = 0; j < n; j++)
                if ((i & (1 << j)) != 0)
                    sum += arr[j];

            // Print sum of picked elements.
            System.out.print(sum + " ");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = new int[] { 5, 4, 3 };
        int n = arr.length;

        subsetSums(arr, n);
    }
}

// This code is contributed by spp____
```

## 蟒蛇 3

```
# Iterative Python3 program to print sums of all possible subsets

# Prints sums of all subsets of array
def subsetSums(arr, n):
    # There are totoal 2^n subsets
    total = 1 << n

    # Consider all numbers from 0 to 2^n - 1
    for i in range(total):
       Sum = 0

       # Consider binary representation of
       # current i to decide which elements
       # to pick.
       for j in range(n):
          if ((i & (1 << j)) != 0):
              Sum += arr[j]

       # Print sum of picked elements.
       print(Sum, "", end = "")

arr = [ 5, 4, 3 ]
n = len(arr)

subsetSums(arr, n);

# This code is contributed by mukesh07.
```

## C#

```
// Iterative C# program to print sums of all
// possible subsets.
using System;
class GFG {

    // Prints sums of all subsets of array
    static void subsetSums(int[] arr, int n)
    {

        // There are totoal 2^n subsets
        int total = 1 << n;

        // Consider all numbers from 0 to 2^n - 1
        for (int i = 0; i < total; i++) {
            int sum = 0;

            // Consider binary representation of
            // current i to decide which elements
            // to pick.
            for (int j = 0; j < n; j++)
                if ((i & (1 << j)) != 0)
                    sum += arr[j];

            // Print sum of picked elements.
            Console.Write(sum + " ");
        }
    }

  static void Main() {
    int[] arr = { 5, 4, 3 };
    int n = arr.Length;

    subsetSums(arr, n);
  }
}

// This code is contributed by divyesh072019.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Iterative PHP program to print
// sums of all possible subsets.

// Prints sums of all subsets of array
function subsetSums($arr, $n)
{

        // There are totoal 2^n subsets
        $total = 1 << $n;

    // Consider all numbers
    // from 0 to 2^n - 1
    for ($i = 0; $i < $total; $i++)
    {
        $sum = 0;

        // Consider binary representation of
        // current i to decide which elements
        // to pick.
        for ($j = 0; $j < $n; $j++)
            if ($i & (1 << $j))
                $sum += $arr[$j];

        // Print sum of picked elements.
        echo $sum , " ";
    }
}

    // Driver code
    $arr = array(5, 4, 3);
    $n = sizeof($arr);
    subsetSums($arr, $n);

// This Code is Contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Iterative Javascript program to print sums of all
    // possible subsets.

    // Prints sums of all subsets of array
    function subsetSums(arr, n)
    {

        // There are totoal 2^n subsets
        let total = 1 << n;

        // Consider all numbers from 0 to 2^n - 1
        for(let i = 0; i < total; i++)
        {
           let sum = 0;

           // Consider binary representation of
           // current i to decide which elements
           // to pick.
           for(let j = 0; j < n; j++)
              if ((i & (1 << j)) != 0)
                  sum += arr[j];

           // Print sum of picked elements.
           document.write(sum + " ");
        }
    }

    let arr = [ 5, 4, 3 ];
    let n = arr.length;

    subsetSums(arr, n);

</script>
```

**输出:**

```
0 5 4 9 3 8 7 12 
```

**时间复杂度:** O( ![N * 2^N    ](img/46ee797c418a3e9d3bae5d6864ec571f.png "Rendered by QuickLaTeX.com") )
**辅助空间:** O(1)
感谢 cfh 在评论中提出上述迭代解。
注意:我们实际上并没有创建子集来寻找它们的和，而是使用递归来寻找给定集合的非连续子集的和。

上述技术可用于对子集执行各种操作，如乘法、除法、异或等，而无需实际创建和存储子集，从而使程序存储器高效。
本文由 [**阿迪亚·古普塔**](https://practice.geeksforgeeks.org/user-profile.php?user=Aditya%20Gupta%204) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。不正确，或者你想分享更多关于上面讨论的话题的信息
# 集合中不同子集的数量

> 原文:[https://www.geeksforgeeks.org/number-distinct-subsets-set/](https://www.geeksforgeeks.org/number-distinct-subsets-set/)

给定 n 个不同元素的数组，计算子集的总数。
示例:

```
Input : {1, 2, 3}
Output : 8
Explanation
the array contain total 3 element.its subset 
are {}, {1}, {2}, {3}, {1, 2}, {2, 3}, {3, 1}, {1, 2, 3}.
so the output is 8..
```

我们知道大小为 n 的集合的子集数是 **2 <sup>n</sup>**
**这个公式是如何工作的？**
对于每一个元素，我们都有两个选择，要么挑，要么不挑。所以我们总共有 2 * 2 *……(n 次)选择，即 **2 <sup>n</sup>**
另一种解释是:
大小为 0 的子集数量=<sup>n</sup>C<sub>0</sub>T18】大小为 1 的子集数量= <sup>n</sup> C <sub>1</sub>
大小为 2 的子集数量=<sup>n</sup>C<sub>2【T20..
子集总数=<sup>n</sup>C<sub>0</sub>+<sup>n</sup>C<sub>1</sub>+<sup>n</sup>C<sub>2</sub>+…。+<sup>n</sup>C<sub>n</sub>=**2<sup>n</sup>**
详见[二项式系数之和](https://www.geeksforgeeks.org/sum-binomial-coefficients/)。</sub> 

## C++

```
// CPP program to count number of distinct
// subsets in an array of distinct numbers
#include <bits/stdc++.h>
using namespace std;

// Returns 2 ^ n
int subsetCount(int arr[], int n)
{
    return 1 << n;
}

/* Driver program to test above function */
int main()
{
    int A[] = { 1, 2, 3 };
    int n = sizeof(A) / sizeof(A[0]);

    cout << subsetCount(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of distinct
// subsets in an array of distinct numbers

class GFG {

    // Returns 2 ^ n
    static int subsetCount(int arr[], int n)
    {
        return 1 << n;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int A[] = { 1, 2, 3 };
        int n = A.length;

        System.out.println(subsetCount(A, n));
    }
}

// This code is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Python3 program to count number
# of distinct subsets in an
# array of distinct numbers
import math

# Returns 2 ^ n
def subsetCount(arr, n):

    return 1 << n

# driver code
A = [ 1, 2, 3 ]
n = len(A)
print(subsetCount(A, n))

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to count number of distinct
// subsets in an array of distinct numbers
using System;

class GFG {

    // Returns 2 ^ n
    static int subsetCount(int []arr, int n)
    {
        return 1 << n;
    }

    // Driver program
    public static void Main()
    {
        int []A = { 1, 2, 3 };
        int n = A.Length;

        Console.WriteLine(subsetCount(A, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// number of distinct
// subsets in an array
// of distinct numbers

// Returns 2 ^ n
function subsetCount($arr, $n)
{
    return 1 << $n;
}

// Driver Code
$A = array( 1, 2, 3 );
$n = sizeof($A);
echo(subsetCount($A, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript  program to count number of distinct
// subsets in an array of distinct numbers

// Returns 2 ^ n
    function subsetCount(arr, n)
    {
        return 1 << n;
    }

// Driver code

       let A = [ 1, 2, 3 ];
        let n = A.length;

        document.write(subsetCount(A, n));

</script>
```

**Output:** 

```
8
```
# 通过从数组中选择最少的对进行最小求和

> 原文:[https://www . geesforgeks . org/minimum-sum-choice-minimum-pairs-array/](https://www.geeksforgeeks.org/minimum-sum-choosing-minimum-pairs-array/)

给定一个由 n 个元素组成的数组 A[]。我们需要选择两个相邻的元素，删除其中较大的元素，并将较小的元素存储到另一个数组中，比如 B[]。我们需要执行这个操作，直到数组 A[]只包含一个元素。最后，我们必须以这样的方式构造数组 B[]，即其元素的总和最小。打印数组 B[]的总和。
示例:

```
Input : A[] = {3, 4} 
Output : 3

Input : A[] = {2, 4, 1, 3}
Output : 3
```

有一个简单的技巧可以解决这个问题，那就是总是选择数组 A[]及其相邻的最小元素，删除相邻的元素，并将最小的一个复制到数组 B[]。同样，对于下一次迭代，我们有相同的最小元素和任何要删除的随机相邻元素。在 n-1 次运算后，除了最小的元素外，A[]的所有元素都被删除，同时数组 B[]包含“n-1”个元素，并且都等于数组 A[]的最小元素。
因此数组 B[]的总和等于**最小* (n-1)** 。

## C++

```
// CPP program to minimize the cost
// of array minimization
#include <bits/stdc++.h>
using namespace std;

// Returns minimum possible sum in
// array B[]
int minSum(int A[], int n)
{
    int min_val = *min_element(A, A+n);
    return (min_val * (n-1));
}

// driver function
int main()
{
    int A[] = { 3, 6, 2, 8, 7, 5};
    int n = sizeof(A)/ sizeof (A[0]);
    cout << minSum(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to minimize the
// cost of array minimization
import java.util.Arrays;

public class GFG {

// Returns minimum possible
// sum in array B[]
    static int minSum(int[] A, int n) {
        int min_val = Arrays.stream(A).min().getAsInt();
        return (min_val * (n - 1));
    }

    // Driver Code
    static public void main(String[] args) {
        int[] A = {3, 6, 2, 8, 7, 5};
        int n = A.length;
        System.out.println((minSum(A, n)));

    }
}
// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python code for minimum cost of
# array minimization

# Function definition for minCost
def minSum(A):

    # find the minimum element of A[]
    min_val = min(A);

    # return the answer
    return min_val * (len(A)-1)

# driver code
A = [7, 2, 3, 4, 5, 6]
print (minSum(A))
```

## C#

```
// C# program to minimize the
// cost of array minimization
using System;
using System.Linq;

public class GFG
{

// Returns minimum possible
// sum in array B[]
static int minSum(int []A, int n)
{
    int min_val = A.Min();
    return (min_val * (n - 1));
}

    // Driver Code
    static public void Main()
    {
        int []A = {3, 6, 2, 8, 7, 5};
        int n = A.Length;
        Console.WriteLine(minSum(A, n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to minimize the
// cost of array minimization

// Returns minimum possible
// sum in array B[]
function minSum($A, $n)
{
    $min_val = min($A);
    return ($min_val * ($n - 1));
}

    // Driver Code
    $A = array(3, 6, 2, 8, 7, 5);
    $n = count($A);
    echo minSum($A, $n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// JavaScript program to minimize the cost
// of array minimization

// Returns minimum possible sum in
// array B[]
function minSum(A, n)
{
    let min_val = Math.min(...A);
    return (min_val * (n-1));
}

// driver function

    let A = [3, 6, 2, 8, 7, 5];
    let n = A.length;
    document.write(minSum(A, n));

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
10
```

**时间复杂度:**求数组最小元素的 O(n)。
本文由 [**希瓦姆·普拉丹(anuj_charm)**](https://www.facebook.com/anuj.charm) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
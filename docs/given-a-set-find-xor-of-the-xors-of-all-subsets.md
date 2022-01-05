# 给定一个集合，求所有子集的异或。

> 原文:[https://www . geeksforgeeks . org/给定一组所有子集的异或运算/](https://www.geeksforgeeks.org/given-a-set-find-xor-of-the-xors-of-all-subsets/)

问题是找出所有子集的异或。即如果集合是{1，2，3}。所有子集都是:[{1}、{2}、{3}、{1，2}、{1，3}、{2，3}、{1，2，3}]。求每个子集的异或，然后求每个子集结果的异或。
**我们强烈建议你尽量减少浏览器，先自己试试这个。**
如果我们把第一步(也是唯一一步)做对了，这是一个很简单的问题要解决。解决方法是 n > 1 时异或始终为 0，n 为 1 时置位[0]。

## C++

```
// C++ program to find XOR of XOR's of all subsets
#include <bits/stdc++.h>
using namespace std;

// Returns XOR of all XOR's of given subset
int findXOR(int Set[], int n)
{
    // XOR is 1 only when n is 1, else 0
    if (n == 1)
       return Set[0];
    else
       return 0;
}

// Driver program
int main()
{
    int Set[] = {1, 2, 3};
    int n = sizeof(Set)/sizeof(Set[0]);
    cout << "XOR of XOR's of all subsets is "
         << findXOR(Set, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find XOR of
// XOR's of all subsets
import java.util.*;

class GFG {

// Returns XOR of all XOR's of given subset
static int findXOR(int Set[], int n) {

    // XOR is 1 only when n is 1, else 0
    if (n == 1)
    return Set[0];
    else
    return 0;
}

// Driver code
public static void main(String arg[])
{
    int Set[] = {1, 2, 3};
    int n = Set.length;
    System.out.print("XOR of XOR's of all subsets is " +
                                        findXOR(Set, n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# XOR of XOR's of all subsets

# Returns XOR of all
# XOR's of given subset
def findXOR(Set, n):

    # XOR is 1 only when
    # n is 1, else 0
    if (n == 1):
         return Set[0]
    else:
         return 0

# Driver code

Set = [1, 2, 3]
n = len(Set)

print("XOR of XOR's of all subsets is ",
         findXOR(Set, n));

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find XOR of
// XOR's of all subsets
using System;

class GFG {

// Returns XOR of all
// XOR's of given subset
static int findXOR(int []Set, int n)
{

    // XOR is 1 only when n
    // is 1, else 0
    if (n == 1)
    return Set[0];
    else
    return 0;
}

// Driver code
public static void Main()
{
    int []Set = {1, 2, 3};
    int n = Set.Length;
    Console.Write("XOR of XOR's of all subsets is " +
                                    findXOR(Set, n));
}
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find XOR
// of XOR's of all subsets

// Returns XOR of all
// XOR's of given subset
function findXOR($Set, $n)
{

    // XOR is 1 only when
    // n is 1, else 0
    if ($n == 1)
        return $Set[0];
    else
        return 0;
}

    // Driver Code
    $Set = array(1, 2, 3);
    $n = count($Set);
    echo "XOR of XOR's of all subsets is "
         , findXOR($Set, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find XOR of XOR's of all subsets

// Returns XOR of all XOR's of given subset
function findXOR(Set, n)
{
    // XOR is 1 only when n is 1, else 0
    if (n == 1)
        return Set[0];
    else
        return 0;
}

// Driver program

    let Set = [1, 2, 3];
    let n = Set.length;
    document.write("XOR of XOR's of all subsets is "
        + findXOR(Set, n));

// This code is contributed by Surbhi Tyagi

</script>
```

输出:

```
XOR of XOR's of all subsets is 0
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**相关问题:**
[所有可能子集的异或之和](https://www.geeksforgeeks.org/sum-xor-possible-subsets/)
**这是如何工作的？**
逻辑很简单。让我们考虑第 n 个元素，它可以包含在剩余(n-1)个元素的所有子集中。(n-1)个元素的子集数等于 2 <sup>(n-1)</sup> ，n > 1 时总是偶数。因此，在异或结果中，每个元素被包括偶数次，并且任何数量的偶数出现的异或为 0。
本文由 [**Ekta Goel**](https://www.linkedin.com/pub/ekta-goel/75/12a/3a6) 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上述主题的信息
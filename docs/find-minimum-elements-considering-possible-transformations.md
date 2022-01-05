# 考虑所有可能的变换后找到最小元素

> 原文:[https://www . geeksforgeeks . org/find-minimum-elements-考虑可能的转换/](https://www.geeksforgeeks.org/find-minimum-elements-considering-possible-transformations/)

给定三种颜色的数组。数组元素有一个特殊的属性。每当两种不同颜色的元素彼此相邻时，它们就会合并成第三种颜色的元素。在考虑了所有可能的变换后，数组中可以有多少最小数量的元素。
**例:**

```
Input : arr[] = {R, G}
Output : 1
G B -> {G B} R -> R

Input : arr[] = {R, G, B}
Output : 2
Explanation : 
R G B -> [R G] B ->  B B
OR
R G B -> R {G B} ->  R R 
```

**场景**

在你急于解决之前，我们建议你尝试不同的例子，看看你是否能找到任何模式。

```
Let us see few more scenarios:
  1. R R R, Output 3
  2. R R G B -> R [R G] B -> [R B] B -> [G B] -> R, Output 1
  3. R G R G -> [R G] R G -> [B R] G ->G G, Output 2
  4. R G B B G R -> R [G B] B G R ->R [R B] G R ->[R G] G R 
                    -> [B G] R ->R R, Output 2
  5. R R B B G -> R [R B] [B G] -> R [G R] -> [R B] -> G,
                     Output 1
```

你在输出中发现什么模式了吗？

**可能的模式**

设 n 为数组中元素的个数。不管输入是什么，我们总是以三种输出结束:

*   **n:** 完全不能发生转化的时候
*   **2:** 当每种颜色的元素个数都是奇数或偶数时
*   **1:** 当每种颜色的元素数量混合为奇数和偶数时

**步骤:**

```
1) Count the number of elements of each color.
2) Then only one out of the following four cases can happen:
......1) There are elements of only one color, return n.
......2) There are even number of elements of each color, return 2.
......3) There are odd number of elements of each color, return 2.
......4) In every other case, return 1.
        (The elements will combine with each other repeatedly until 
         only one of them is left)
```

下面是上述算法的实现。

## C++

```
// C++ program to find count of minimum elements
// after considering all possible transformations.
#include <iostream>
using namespace std;

// Returns minimum possible elements after considering
// all possible transformations.
int findMin(char arr[], int n)
{
    // Initialize counts of all colors as 0
    int b_count = 0, g_count = 0, r_count = 0;

    // Count number of elements of different colors
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == 'B') b_count++;
        if (arr[i] == 'G') g_count++;
        if (arr[i] == 'R') r_count++;
    }

    // Check if elements are of same color
    if (b_count==n || g_count==n || r_count==n)
        return n;

    // If all are odd, return 2
    if ((r_count&1 && g_count&1 && b_count&1) )
        return 2;

    // If all are even, then also return 2
    if (!(r_count & 1) && !(g_count & 1) &&
        !(b_count & 1) )
        return 2;

    // If none above the cases are true, return 1
    return 1;
}

// Driver code
int main()
{
    char arr[] = {'R', 'G', 'B', 'R'};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << findMin(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

// Java program to find count of minimum elements
// after considering all possible transformations.
class solution
{

// Returns minimum possible elements after considering
// all possible transformations.
static int findMin(char arr[], int n)
{
    // Initialize counts of all colors as 0
    int b_count = 0, g_count = 0, r_count = 0;

    // Count number of elements of different colors
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == 'B') b_count++;
        if (arr[i] == 'G') g_count++;
        if (arr[i] == 'R') r_count++;
    }

    // Check if elements are of same color
    if (b_count==n || g_count==n || r_count==n)
        return n;

    // If all are odd, return 2
    if((r_count&1) == 1)    {
     if((g_count&1) == 1)     {
      if((b_count&1) == 1)
        return 2;
     }
    }

    // If all are even, then also return 2
    if((r_count & 1) == 0)
    {
      if ((g_count & 1) == 0)
      {
          if ((b_count & 1) == 0)
                return 2;
      }
    }

    // If none above the cases are true, return 1
    return 1;
}

// Driver code
public static void main(String args[])
{
    char arr[] = {'R', 'G', 'B', 'R'};
    int n = arr.length;
    System.out.println(findMin(arr, n));

}
}
// This code is contributed byte
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python 3 program to find count of minimum elements
# after considering all possible transformations.

# Returns minimum possible elements after
# considering all possible transformations.
def findMin(arr, n):

    # Initialize counts of all
    # colors as 0
    b_count = 0
    g_count = 0
    r_count = 0

    # Count number of elements of
    # different colors
    for i in range(n):
        if (arr[i] == 'B'):
            b_count += 1
        if (arr[i] == 'G'):
            g_count += 1
        if (arr[i] == 'R'):
            r_count += 1

    # Check if elements are of same color
    if (b_count == n or
        g_count == n or r_count == n):
        return n

    # If all are odd, return 2
    if ((r_count&1 and
         g_count&1 and b_count&1)):
        return 2

    # If all are even, then also return 2
    if (not (r_count & 1) and not
            (g_count & 1) and not (b_count & 1)):
        return 2

    # If none above the cases
    # are true, return 1
    return 1

# Driver code
if __name__ == "__main__":

    arr = ['R', 'G', 'B', 'R']
    n = len(arr)
    print(findMin(arr, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find count of minimum elements
// after considering all possible transformations.
using System;

class GFG
{

// Returns minimum possible elements after
// considering all possible transformations.
static int findMin(char []arr, int n)
{
    // Initialize counts of all colors as 0
    int b_count = 0, g_count = 0, r_count = 0;

    // Count number of elements of different colors
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == 'B') b_count++;
        if (arr[i] == 'G') g_count++;
        if (arr[i] == 'R') r_count++;
    }

    // Check if elements are of same color
    if (b_count == n || g_count == n || r_count == n)
        return n;

    // If all are odd, return 2
    if((r_count&1) == 1)
    {
        if((g_count&1) == 1)   
        {
            if((b_count&1) == 1)
                return 2;
        }
    }

    // If all are even, then also return 2
    if((r_count & 1) == 0)
    {
        if ((g_count & 1) == 0)
        {
            if ((b_count & 1) == 0)
                    return 2;
        }
    }

    // If none above the cases are true,
    // return 1
    return 1;
}

// Driver code
public static void Main()
{
    char []arr = {'R', 'G', 'B', 'R'};
    int n = arr.Length;
    Console.WriteLine(findMin(arr, n));
}
}

// This code is contributed byte
// nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count of minimum elements
// after considering all possible transformations.

// Returns minimum possible elements after
// considering all possible transformations.
function findMin($arr, $n)
{
    // Initialize counts of all colors as 0
    $b_count = 0; $g_count = 0; $r_count = 0;

    // Count number of elements of
    // different colors
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] == 'B') $b_count++;
        if ($arr[$i] == 'G') $g_count++;
        if ($arr[$i] == 'R') $r_count++;
    }

    // Check if elements are of same color
    if ($b_count == $n || $g_count == $n ||
                          $r_count == $n)
        return $n;

    // If all are odd, return 2
    if (($r_count & 1 && $g_count & 1 &&
                         $b_count & 1))
        return 2;

    // If all are even, then also return 2
    if (!($r_count & 1) && !($g_count & 1) &&
        !($b_count & 1) )
        return 2;

    // If none above the cases are
    // true, return 1
    return 1;
}

// Driver code
$arr = array('R', 'G', 'B', 'R');
$n = count($arr);
echo findMin($arr, $n);

// This code is contributed by 29AjayKumar
?>
```

## java 描述语言

```
<script>
// Javascript program to find count of minimum elements
// after considering all possible transformations.

    // Returns minimum possible elements after considering
    // all possible transformations.
    function findMin(arr,n)
    {

        // Initialize counts of all colors as 0
        let b_count = 0, g_count = 0, r_count = 0;

        // Count number of elements of different colors
        for (let i = 0; i < n; i++)
        {
            if (arr[i] == 'B') b_count++;
            if (arr[i] == 'G') g_count++;
            if (arr[i] == 'R') r_count++;
        }

        // Check if elements are of same color
        if (b_count==n || g_count==n || r_count==n)
            return n;

        // If all are odd, return 2
        if((r_count&1) == 1)    {
         if((g_count&1) == 1)     {
          if((b_count&1) == 1)
            return 2;
         }
        }

        // If all are even, then also return 2
        if((r_count & 1) == 0)
        {
          if ((g_count & 1) == 0)
          {
              if ((b_count & 1) == 0)
                    return 2;
          }
        }

        // If none above the cases are true, return 1
        return 1;
    }

    // Driver code
    let arr=['R', 'G', 'B', 'R'];
    let n = arr.length;
    document.write(findMin(arr, n));

    // This code is contributed by rag2127.
</script>
```

**输出:**

```
1
```

**时间复杂度:**O(n)
T3】辅助空间:O(1)
T6】练习:T8】

1.  上述问题需要多少次变换？
2.  可以打印元素变换的顺序吗？如果是，将采取什么方法？讨论时间和空间的复杂性

本文由 [**阿施·巴恩瓦尔**](https://www.facebook.com/barnwal.aashish?fref=ts) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
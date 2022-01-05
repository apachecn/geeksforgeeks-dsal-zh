# 排序 3 个整数，不使用 if 条件或仅使用 max()函数

> 原文:[https://www . geesforgeks . org/sort-3-整数-不使用-条件-使用-max-function/](https://www.geeksforgeeks.org/sort-3-integers-without-using-condition-using-max-function/)

给定三个整数，使用 if 条件按排序顺序打印它们。
**例:**

```
Input  : a = 3, b = 2, c = 9
Output : 2 3 9

Input  : a = 4, b = 1, c = 9
Output : 1 4 9
```

**进场:**
1。用 max()函数求 a，b，c 的最大值。
3。将所有整数乘以–1。再次使用 max()函数找到–a、–b、–c 的最小值。
4。将上述步骤中的最大值和最小值相加，并将总和细分为(a+b+c)。它给了我们中间的元素。
对负数也有效。

## C++

```
// C++ program to print three numbers
// in sorted order using max function
#include<bits/stdc++.h>
using namespace std;

void printSorted(int a, int b, int c)
{
    // Find maximum element
    int get_max = max(a, max(b, c));

    // Find minimum element
    int get_min = -max(-a, max(-b, -c));

    int get_mid = (a + b + c)
                 - (get_max + get_min);

    cout << get_min << " " << get_mid
        << " " << get_max;
}

// Driver code
int main()
{
    int a = 4, b = 1, c = 9;
    printSorted(a, b, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print three numbers
// in sorted order using max function
class GFG
{

    static void printSorted(int a, int b, int c)
    {
        // Find maximum element
        int get_max = Math.max(a, Math.max(b, c));

        // Find minimum element
        int get_min = -Math.max(-a, Math.max(-b, -c));

        int get_mid = (a + b + c)
                      - (get_max + get_min);

        System.out.print(get_min + " " + get_mid
                                + " " + get_max);
    }

    // Driver code
    public static void main(String[] args)
    {

        int a = 4, b = 1, c = 9;

        printSorted(a, b, c);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to print three numbers
# in sorted order using max function

def printSorted(a, b, c):

    # Find maximum element
    get_max = max(a, max(b, c))

    # Find minimum element
    get_min = -max(-a, max(-b, -c))

    get_mid = (a + b + c) - (get_max + get_min)

    print(get_min, " " , get_mid, " " , get_max)

# Driver Code
a, b, c = 4, 1, 9
printSorted(a, b, c)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to print three numbers
// in sorted order using max function
using System;

class GFG {

    static void printSorted(int a, int b, int c)
    {
        // Find maximum element
        int get_max = Math.Max(a, Math.Max(b, c));

        // Find minimum element
        int get_min = -Math.Max(-a, Math.Max(-b, -c));

        int get_mid = (a + b + c) -
                      (get_max + get_min);

    Console.Write(get_min + " " + get_mid
                          + " " + get_max);
    }

    // Driver code
    public static void Main()
    {
        int a = 4, b = 1, c = 9;

        printSorted(a, b, c);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print three numbers
// in sorted order using max function

function printSorted($a, $b, $c)
{

    // Find maximum element
    $get_max = max($a, max($b, $c));

    // Find minimum element
    $get_min = -max(-$a, max(-$b, -$c));

    $get_mid = ($a + $b + $c) -
               ($get_max + $get_min);

    echo $get_min , " " , $get_mid, " " , $get_max;
}

    // Driver Code
    $a = 4;
    $b = 1;
    $c = 9;
    printSorted($a, $b,$c);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
function printSorted(a, b, c)
    {

        // Find maximum element
        let get_max = Math.max(a, Math.max(b, c));

        // Find minimum element
        let get_min = -Math.max(-a, Math.max(-b, -c));

        let get_mid = (a + b + c) 
                      - (get_max + get_min);

        document.write(get_min + " " + get_mid
                                + " " + get_max);
    }

// Driver Code

     let a = 4, b = 1, c = 9;        
     printSorted(a, b, c);

// This code is contributed by splevel62.
</script>
```

输出:

```
 1 4 9
```

本文由 [**拉克什·库马尔**](https://www.facebook.com/Rakesh2raj) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
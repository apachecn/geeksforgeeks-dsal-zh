# 在只允许 2 位数(4 和 7)的序列中找到第 n 个元素

> 原文:[https://www . geesforgeks . org/find-n-th-element-series-2-digits-4-7-允许/](https://www.geeksforgeeks.org/find-n-th-element-series-2-digits-4-7-allowed/)

考虑一系列仅由数字 4 和 7 组成的数字。数列中的前几个数字是 4，7，44，47，74，44744，..等等。给定一个数 n，我们需要找到数列中的第 n 个数。
示例:

```
Input : n = 2
Output : 7

Input : n = 3
Output : 44

Input  : n = 5
Output : 74

Input  : n = 6
Output : 77
```

这个想法是基于这样一个事实，即最后一个数字的值在序列中交替。例如，如果第 I 个数字的最后一位是 4，那么第(i-1)个和第(i+1)个数字的最后一位必须是 7。
我们创建一个大小为(n+1)的数组，并将 4 和 7(这两个总是系列的前两个元素)推给它。对于更多的元素，我们检查
1)如果 I 是奇数，
arr[I]= arr[I/2]* 10+4；
2)如果是偶数，
arr[I]= arr[(I/2)-1]* 10+7；
最后返回 arr[n]。

## C++

```
// C++ program to find n-th number in a series
// made of digits 4 and 7
#include <bits/stdc++.h>
using namespace std;

// Return n-th number in series made of 4 and 7
int printNthElement(int n)
{
    // create an array of size (n+1)
    int arr[n+1];
    arr[1] = 4;
    arr[2] = 7;

    for (int i=3; i<=n; i++)
    {
        // If i is odd
        if (i%2 != 0)
            arr[i] = arr[i/2]*10 + 4;
        else
            arr[i] = arr[(i/2)-1]*10 + 7;
    }
    return arr[n];
}

// Driver code
int main()
{
    int n = 6;
    cout << printNthElement(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th number in a series
// made of digits 4 and 7

class FindNth
{
    // Return n-th number in series made of 4 and 7
    static int printNthElement(int n)
    {
        // create an array of size (n+1)
        int arr[] = new int[n+1];
        arr[1] = 4;
        arr[2] = 7;

        for (int i=3; i<=n; i++)
        {
            // If i is odd
            if (i%2 != 0)
                arr[i] = arr[i/2]*10 + 4;
            else
                arr[i] = arr[(i/2)-1]*10 + 7;
        }
        return arr[n];
    }   

    // main function
    public static void main (String[] args)
    {
        int n = 6;
        System.out.println(printNthElement(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find n-th number
# in a series made of digits 4 and 7

# Return n-th number in series made
# of 4 and 7
def printNthElement(n) :

    # create an array of size (n + 1)
    arr =[0] * (n + 1);
    arr[1] = 4
    arr[2] = 7

    for i in range(3, n + 1) :
        # If i is odd
        if (i % 2 != 0) :
            arr[i] = arr[i // 2] * 10 + 4
        else :
            arr[i] = arr[(i // 2) - 1] * 10 + 7

    return arr[n]

# Driver code
n = 6
print(printNthElement(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find n-th number in a series
// made of digits 4 and 7
using System;

class GFG
{
    // Return n-th number in series made of 4 and 7
    static int printNthElement(int n)
    {
        // create an array of size (n+1)
        int []arr = new int[n+1];
        arr[1] = 4;
        arr[2] = 7;

        for (int i = 3; i <= n; i++)
        {
            // If i is odd
            if (i % 2 != 0)
                arr[i] = arr[i / 2] * 10 + 4;
            else
                arr[i] = arr[(i / 2) - 1] * 10 + 7;
        }
        return arr[n];
    }

    // Driver code
    public static void Main ()
    {
        int n = 6;
        Console.Write(printNthElement(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th
// number in a series
// made of digits 4 and 7

// Return n-th number in
// series made of 4 and 7
function printNthElement($n)
{

    // create an array
    // of size (n+1)
    $arr[1] = 4;
    $arr[2] = 7;

    for ($i = 3; $i <= $n; $i++)
    {

        // If i is odd
        if ($i % 2 != 0)
            $arr[$i] = $arr[$i / 2] *
                               10 + 4;
        else
            $arr[$i] = $arr[($i / 2) - 1] *
                                    10 + 7;
    }
    return $arr[$n];
}

// Driver code
$n = 6;
echo(printNthElement($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript program to find n-th number in a series
// made of digits 4 and 7

    // Return n-th number in series made of 4 and 7
    function printNthElement(n) {
        // create an array of size (n+1)
        var arr = Array(n + 1).fill(0);
        arr[1] = 4;
        arr[2] = 7;

        for (var i = 3; i <= n; i++) {
            // If i is odd
            if (i % 2 != 0)
                arr[i] = arr[i / 2] * 10 + 4;
            else
                arr[i] = arr[(i / 2) - 1] * 10 + 7;
        }
        return arr[n];
    }

    // main function

        var n = 6;
        document.write(printNthElement(n));

// This code is contributed by Princi Singh
</script>
```

输出:

```
77
```

[在只允许 2 位数(4 和 7)的数列中寻找第 n 个元素|集合 2 (log(n)方法)](https://www.geeksforgeeks.org/find-n-th-element-series-2-digits-4-7-allowed-set-2-logn-method/)
本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
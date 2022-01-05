# 查找一个数是否能被列表中的每个数整除

> 原文:[https://www . geeksforgeeks . org/find-number-除尽-每一个数字-list/](https://www.geeksforgeeks.org/find-number-divisible-every-number-list/)

给定一个列表和一个数字，任务是找出被列表中每个元素除的数字。
**例:**

```
Input : List   = [1, 2, 3, 4, 5]
        Number = 3
Output : No

Input : List   = [4, 8, 12, 16, 20]
        Number = 4
Output : Yes
```

**算法:**

```
1\. Run a loop till length of the list
2\. Divide every element with the given number
3\. If number is not divided by any element, 
   return 0.
4\. Return 1.
```

## C++

```
// C++ program which check is a number
// divided with every element in list or not
#include <bits/stdc++.h>
using namespace std;

// Function which check is a number
// divided with every element in list or not
bool findNoIsDivisibleOrNot(int a[], int n, int l)
{
    for (int i = 0; i < l; i++) {
        if (a[i] % n != 0)
            return false;
    }
    return true;
}

// driver program
int main()
{
    int a[] = {14, 12, 4, 18};
    int n = 2;
    int l = (sizeof(a) / sizeof(a[0]));
    if (findNoIsDivisibleOrNot(a, n, l))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}

// This code is contributed by Sam007
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program which check is a number
// divided with every element in list
// or not

class GFG {

    // Function which check is a number
    // divided with every element in list or not
    static boolean findNoIsDivisibleOrNot(int a[], int n)
    {
        for (int i = 0; i < a.length; i++) {
            if (a[i] % n != 0)
                return false;
        }
        return true;
    }

    // driver program
    public static void main(String[] args)
    {
        int a[] = {14, 12, 4, 18};
        int n = 2;
        if (findNoIsDivisibleOrNot(a, n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Pramod Kumar
```

## 计算机编程语言

```
# Python program which check is a number
# divided with every element in list
# or not
def findNoIsDivisibleOrNot(n, l =[]):

    # Checking if a number is divided
    # by every element or not
    for i in range(0, len(l)):
        if l[i]% n != 0:
            return 0
    return 1

# Driver code
l = [14, 12, 4, 18]
n = 2
if findNoIsDivisibleOrNot(n, l) == 1:
    print "Yes"
else:
    print "No"
```

## C#

```
// C# program which check is a number
// divided with every element in list or no
using System;

class GFG {

    // Function which check is a number
    // divided with every element in list or not
    static bool findNoIsDivisibleOrNot(int[] a, int n)
    {
        for (int i = 0; i < a.Length; i++) {
            if (a[i] % n != 0)
                return false;
        }
        return true;
    }

    // driver program
    public static void Main()
    {
        int[] a = {14, 12, 4, 18};
        int n = 2;
        if (findNoIsDivisibleOrNot(a, n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program which
// check is a number
// divided with every
// element in list or not

// Function which check
// is a number divided
// with every element
// in list or not
function findNoIsDivisibleOrNot($a, $n, $l)
{
    for ($i = 0; $i < $l; $i++)
    {
        if ($a[$i] % $n != 0)
            return false;
    }
    return true;
}

    // Driver Code
    $a = array(14, 12, 4, 18);
    $n = 2;
    $l = sizeof($a);
    if (findNoIsDivisibleOrNot($a, $n, $l))
        echo "Yes";
    else
        echo "No";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program which check is a number
// divided with every element in list or not

// Function which check is a number
// divided with every element in list or not
function findNoIsDivisibleOrNot(a, n, l)
{
    for (let i = 0; i < l; i++) {
        if (a[i] % n != 0)
            return false;
    }
    return true;
}

// driver program
    let a = [14, 12, 4, 18];
    let n = 2;
    let l = a.length;
    if (findNoIsDivisibleOrNot(a, n, l))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**输出:**

```
Yes
```

本文由**萨赫勒拉杰普特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
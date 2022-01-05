# 查找是否可以将页面旋转一个角度。

> 原文:[https://www . geesforgeks . org/find-可能-旋转-页面-角度-非/](https://www.geeksforgeeks.org/find-possible-rotate-page-angle-not/)

你在一页上有三个点 a，b，c。查找是否可以将页面围绕该点旋转一个角度，使得“a”的新位置与“b”的旧位置相同，“b”的新位置与“c”的旧位置相同。如果存在这样的角度，打印“是”，否则打印“否”。
**例:**

```
Input : a1 = 0, a2 = 1, b1 = 1, b2 =  1,
        c1 = 1, c2 = 0
Output : Yes
Explanation : Rotate the page by 90 degree.

Input : a1 = 1, a2 = 1, b1 = 0, b2 = 0,
        c1 = 1000, c2 = 1000
Output : No
```

只有当“a”点和“b”点之间的距离等于“b”点和“c”点之间的距离时，才能将页面旋转一定角度。但是如果这些点在同一条直线上，那么在 b 点就没有旋转。当' a '，' b '，' c '在同一行或 **dis(a，b)时问题无解！= dis(b，c)**

## C++

```
// C++ program to find if its possible
// to rotate page or not
#include<bits/stdc++.h>
using namespace std;

// function to find if it's possible
// to rotate page or not
void possibleOrNot(long long a1, long long a2,
                   long long b1, long long b2,
                   long long c1, long long c2){

    // Calculating distance b/w points
    long long dis1 = pow(b1 - a1, 2) +
                      pow(b2 - a2, 2);
    long long dis2 = pow(c1 - b1, 2) +
                      pow(c2 - b2, 2);

    // If distance is not equal
    if(dis1 != dis2)
        cout << "No";

    // If the points are in same line
    else if (b1 == ((a1 + c1) / 2.0) && b2 ==
                          ((a2 + c2) / 2.0))
        cout << "No";
    else
        cout << "Yes";
}

// Driver Code
int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    // Points a, b, and c
    long long a1 = 1, a2 = 0, b1 = 2,
             b2 = 0, c1 = 3, c2 = 0;
    possibleOrNot(a1, a2, b1, b2, c1, c2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find if its possible
// to rotate page or not
import java.util.Arrays;

class GFG {

    // function to find if it's possible
    // to rotate page or not
    static void possibleOrNot(long a1,long a2,
                              long b1,long b2,
                              long c1,long c2)
    {

        // Calculating distance b/w points
        long dis1 = (long)Math.pow(b1 - a1, 2) +
                    (long) Math.pow(b2 - a2, 2);

        long dis2 = (long)Math.pow(c1 - b1, 2) +
                     (long)Math.pow(c2 - b2, 2);

        // If distance is not equal
        if(dis1 != dis2)
            System.out.print("No");

        // If the points are in same line
        else if (b1 == ((a1 + c1) / 2.0) &&
                       b2 == ((a2 + c2) / 2.0))
            System.out.print("No");
        else
            System.out.print("Yes");
    }

    // Driver method
    public static void main(String[] args)
    {

        // Points a, b, and c
        long a1 = 1, a2 = 0, b1 = 2,
                b2 = 0, c1 = 3, c2 = 0;

        possibleOrNot(a1, a2, b1, b2, c1, c2);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to fill an
# array with frequencies.

# Function to find if it's possible
# to rotate page or not
def possibleOrNot(a1, a2, b1, b2, c1, c2):

    # Calculating distance b/w points
    dis1 = (pow(b1 - a1, 2) +
            pow(b2 - a2, 2))
    dis2 = (pow(c1 - b1, 2) +
            pow(c2 - b2, 2))

    # If distance is not equal
    if(dis1 != dis2):
        print("No")

    # If the points are in same line
    elif (b1 == ((a1 + c1) // 2.0) and
          b2 == ((a2 + c2) // 2.0)):
        print("No")
    else:
        print("Yes")

# Driver Code

# Points a, b, and c
a1, b1, c1 = 1, 2, 3
a2 = b2 = c2 = 0
possibleOrNot(a1, a2, b1, b2, c1, c2)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to fill an array with frequencies.
using System;

class GFG
{
    // function to find if it's possible
    // to rotate page or not
    static void possibleOrNot(long a1,long a2,
                              long b1,long b2,
                              long c1,long c2)
    {

        // Calculating distance b/w points
        long dis1 = (long)Math.Pow(b1 - a1, 2) +
                    (long) Math.Pow(b2 - a2, 2);
        long dis2 = (long)Math.Pow(c1 - b1, 2) +
                    (long)Math.Pow(c2 - b2, 2);

        // If distance is not equal
        if(dis1 != dis2)
            Console.Write("No");

        // If the points are in same line
        else if (b1 == ((a1 + c1) / 2.0) && b2 ==
                       ((a2 + c2) / 2.0))
            Console.Write("No");
        else
            Console.Write("Yes");
    }

    // Driver method
    public static void Main()
    {
        // Points a, b, and c
        long  a1 = 1, a2 = 0, b1 = 2,
                 b2 = 0, c1 = 3, c2 = 0;
        possibleOrNot(a1, a2, b1, b2, c1, c2);
    }
}
// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to fill
// an array with frequencies.

// function to find if
// it's possible to
// rotate page or not
function possibleOrNot($a1, $a2, $b1,
                       $b2, $c1, $c2)
{

    // Calculating distance
    // b/w points
    $dis1 = pow($b1 - $a1, 2) +
            pow($b2 - $a2, 2);
    $dis2 = pow($c1 - $b1, 2) +
            pow($c2 - $b2, 2);

    // If distance
    // is not equal
    if($dis1 != $dis2)
        echo "No";

    // If the points
    // are in same line
    else if ($b1 == (($a1 + $c1) / 2.0) &&
             $b2 == (($a2 + $c2) / 2.0))
        echo "No";
    else
        echo "Yes";
}

// Driver Code

// Points a, b, and c
$a1 = 1;
$a2 = 0;
$b1 = 2;
$b2 = 0;
$c1 = 3;
$c2 = 0;
possibleOrNot($a1, $a2, $b1,
              $b2, $c1, $c2);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// javascript program to fill an array with frequencies.

    // function to find if it's possible
    // to rotate page or not

    function possibleOrNot( a1, a2, b1, b2, c1, c2)
    {

        // Calculating distance b/w points
        var dis1 = Math.pow(b1 - a1, 2) +  Math.pow(b2 - a2, 2);

        var dis2 = Math.pow(c1 - b1, 2) +  Math.pow(c2 - b2, 2);

        // If distance is not equal
        if(dis1 != dis2)
            document.write("No");

        // If the points are in same line
        else if (b1 == ((a1 + c1) / 2.0) && b2 == ((a2 + c2) / 2.0))
            document.write("No");
        else
            document.write("Yes");
    }

    // Driver method

        // Points a, b, and c

        var  a1 = 1, a2 = 0, b1 = 2, b2 = 0, c1 = 3, c2 = 0;

        possibleOrNot(a1, a2, b1, b2, c1, c2);

</script>
```

**输出:**

```
No
```

本文由 [**沙钦·毕斯特**](https://www.linkedin.com/in/sachin-bisht-984b5013a/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
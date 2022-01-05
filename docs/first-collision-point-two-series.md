# 两个系列的第一个碰撞点

> 原文:[https://www . geesforgeks . org/first-碰撞点-两个系列/](https://www.geeksforgeeks.org/first-collision-point-two-series/)

给定五个数字 a、b、c、d 和 n(其中 a、b、c、d、n > 0)。这些值代表两个系列的 n 项。这四个数字组成的两个数列是 b，b+a，b+2a…b+(n-1)a 和 d，d+c，d+2c，…..d+(n-1)c
当在任一点上两个系列的求和值完全相同时，这两个系列将发生碰撞。打印碰撞点。

```
Example:
Input : a = 20, b = 2, 
        c = 9, d = 19, 
        n = 100
Output: 82
Explanation: 
Series1 = (2, 22, 42, 62, 82, 102...)  
Series2 = (28, 37, 46, 55, 64, 73, 82, 91..) 
So the first collision point is 82\.   
```

一种**天真的方法**是计算两个不同数组中的两个序列，然后通过运行两个嵌套循环来检查每个元素是否发生碰撞
*时间复杂度* : O(n * n)
*辅助空间* : O(n)
**解决上述问题的一种有效方法**是:
*生成第一个序列的所有元素。设当前元素为 x.
*如果 x 也是第二个数列的元素，则应满足以下条件。
…..a) x 应大于或等于第二系列的第一个元素。
…..a)x 和第一个元素之间的差应能被 c 整除。
*如果满足上述条件，则第 I 个值是所需的交点。
以下是上述问题的实现:

## C++

```
// CPP program to calculate the colliding
// point of two series
#include<bits/stdc++.h>
using namespace std;

void point(int a, int b, int c, int d, int n)
{
    int x , flag = 0;

    // Iterating through n terms of the
    // first series
    for (int i = 0; i < n; i++)
    {

        // x is i-th term of first series
        x = b + i * a;    

        // d is first element of second
        // series and c is common difference
        // for second series.
        if ((x - d) % c == 0 and x - d >= 0)
        {
            cout << x << endl ;
            flag = 1;
            break;
        }

    }

    // If no term of first series is found    
    if(flag == 0)
    {
            cout << "No collision point" << endl;
    }

}

// Driver function
int main()
{
    int a = 20 ;
    int b = 2 ;
    int c = 9;
    int d = 19;
    int n = 20;
    point(a, b, c, d, n);
    return 0;
}

// This code is contributed by  'saloni1297'.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the colliding
// point of two series
import java.io.*;

class GFG
{
    static void point(int a, int b, int c, int d, int n)
    {
        int x , flag = 0;

        // Iterating through n terms of the
        // first series
        for (int i = 0; i < n; i++)
        {

            // x is i-th term of first series
            x = b + i * a;

            // d is first element of second
            // series and c is common difference
            // for second series.
            if ((x - d) % c == 0 && x - d >= 0)
            {
                System.out.println( x ) ;
                flag = 1;
                break;
            }

        }

        // If no term of first series is found
        if(flag == 0)
        {
            System.out.println ("No collision point");
        }

    }

    // Driver function
    public static void main (String[] args)
    {
        int a = 20 ;
        int b = 2 ;
        int c = 9;
        int d = 19;
        int n = 20;
        point(a, b, c, d, n);  

    }
}
// This code is contributed by vt_m
```

## 计算机编程语言

```
# Function to calculate the colliding point
# of two series
def point(a, b, c, d, n):

    # Iterating through n terms of the
    # first series
    for i in range(n):

        # x is i-th term of first series
        x = b + i*a    

        # d is first element of second
        # series and c is common difference
        # for second series.
        if (x-d)%c == 0 and x-d >= 0:
            print x
            return

    # If no term of first series is found     
    else:
        print "No collision point"   

# Driver code
a = 20
b = 2
c = 9
d = 19
n = 20
point(a, b, c, d, n)
```

## C#

```
// C# program to calculate the colliding
// point of two series
using System;

class GFG {

    static void point(int a, int b, int c,
                             int d, int n)
    {
        int x, flag = 0;

        // Iterating through n terms of the
        // first series
        for (int i = 0; i < n; i++) {

            // x is i-th term of first series
            x = b + i * a;

            // d is first element of second
            // series and c is common difference
            // for second series.
            if ((x - d) % c == 0 && x - d >= 0) {
                Console.WriteLine(x);
                flag = 1;
                break;
            }
        }

        // If no term of first series is found
        if (flag == 0) {
            Console.WriteLine("No collision point");
        }
    }

    // Driver function
    public static void Main()
    {
        int a = 20;
        int b = 2;
        int c = 9;
        int d = 19;
        int n = 20;
        point(a, b, c, d, n);
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// the colliding point of
// two series

function point($a, $b, $c, $d, $n)
{
    $x ; $flag = 0;

    // Iterating through
    // n terms of the
    // first series
    for ($i = 0; $i < $n; $i++)
    {

        // x is i-th term
        // of first series
        $x = $b + $i * $a;

        // d is first element of
        // second series and c is
        // common difference for
        // second series.
        if (($x - $d) % $c == 0 and
                      $x - $d >= 0)
        {
            echo $x;
            $flag = 1;
            break;
        }

    }

    // If no term of first
    // series is found
    if($flag == 0)
    {
            echo "No collision po{content}quot;;
    }

}

    // Driver Code
    $a = 20 ;
    $b = 2 ;
    $c = 9;
    $d = 19;
    $n = 20;
    point($a, $b, $c, $d, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to calculate
// the colliding point of
// two series

function point(a, b, c, d, n)
{
    let x ;
    let flag = 0;

    // Iterating through
    // n terms of the
    // first series
    for (let i = 0; i < n; i++)
    {

        // x is i-th term
        // of first series
        x = b + i * a;

        // d is first element of
        // second series and c is
        // common difference for
        // second series.
        if ((x - d) % c == 0 &&
                      x - d >= 0)
        {
            document.write(x);
            flag = 1;
            break;
        }

    }

    // If no term of first
    // series is found
    if(flag == 0)
    {
            document.write("No collision po");
    }

}

    // Driver Code
    let a = 20 ;
    let b = 2 ;
    let c = 9;
    let d = 19;
    let n = 20;
    point(a, b, c, d, n);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
82
```

时间复杂度:O(n)
本文由 [**钿巴贾杰**](https://www.facebook.com/profile.php?id=100008562932368) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
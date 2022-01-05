# 装配货架问题

> 原文:[https://www.geeksforgeeks.org/fitting-shelves-problem/](https://www.geeksforgeeks.org/fitting-shelves-problem/)

给定墙的长度 w 和两个长度 m 和 n 的架子，找出要使用的每种架子的数量和最优解中的剩余空白空间，使空白空间最小。两个架子中较大的一个更便宜，所以它是首选。然而，成本是第二位的，第一位的是尽量减少墙上的空白。

**示例:**

```
Input : w = 24 m = 3 n = 5
Output : 3 3 0
We use three units of both shelves
and 0 space is left.
3 * 3 + 3 * 5 = 24
So empty space  = 24 - 24 = 0
Another solution could have been 8 0 0
but since the larger shelf of length 5
is cheaper the former will be the answer.

Input : w = 29 m = 3 n = 9 
Output : 0 3 2
0 * 3 + 3 * 9 = 27
29 - 27 = 2

Input : w = 24 m = 4 n = 7 
Output : 6 0 0
6 * 4 + 0 * 7 = 24
24 - 24 = 0
```

一个简单有效的方法是尝试所有适合墙壁长度的搁板组合。
为了实现这种方法以及较大的货架比较小的货架成本低的约束，从 0 开始，我们不增加较大类型的货架，直到它们能够被安装。对于每种情况，我们计算空白空间，并最终存储使空白空间最小的值。如果两种情况下的空闲空间相同，我们更喜欢有更多大货架的那种。

下面是它的实现。

## C++

```
// C++ program to find minimum space and units
// of two shelves to fill a wall.
#include <bits/stdc++.h>
using namespace std;

void minSpacePreferLarge(int wall, int m, int n)
{
    // for simplicity, Assuming m is always smaller than n
    // initializing output variables
    int num_m = 0, num_n = 0, min_empty = wall;

    // p and q are no of shelves of length m and n
    // rem is the empty space
    int p = wall/m, q = 0, rem=wall%m;
      num_m=p;
      num_n=q;
      min_empty=rem;
    while (wall >= n) {
        // place one more shelf of length n
        q += 1;
        wall = wall - n;
          // place as many shelves of length m
        // in the remaining part
        p = wall / m;
        rem = wall % m;

        // update output variablse if curr
        // min_empty <= overall empty
        if (rem <= min_empty) {
            num_m = p;
            num_n = q;
            min_empty = rem;
        }
    }

    cout << num_m << " " << num_n << " "
         << min_empty << endl;
}

// Driver code
int main()
{
    int wall = 29, m = 3, n = 9;
    minSpacePreferLarge(wall, m, n);

    wall = 76, m = 1, n = 10;
    minSpacePreferLarge(wall, m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all rotation
// divisible by 4.

public class GFG {
    static void minSpacePreferLarge(int wall, int m, int n)
    {
        // For simplicity, Assuming m is always smaller than n
        // initializing output variables
        int num_m = 0, num_n = 0, min_empty = wall;

        // p and q are no of shelves of length m and n
        // rem is the empty space
        int p = wall/m, q = 0, rem=wall%m;
          num_m=p;
          num_n=q;
          min_empty=rem;
        while (wall >= n) {
            q += 1;
            wall = wall - n;
            // place as many shelves of length m
            // in the remaining part
            p = wall / m;
            rem = wall % m;

            // update output variablse if curr
            // min_empty <= overall empty
            if (rem <= min_empty) {
                num_m = p;
                num_n = q;
                min_empty = rem;
            }

            // place one more shelf of length n
            q += 1;
            wall = wall - n;
        }
        System.out.println(num_m + " " + num_n + " " + min_empty);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int wall = 24, m = 3, n = 5;
        minSpacePreferLarge(wall, m, n);

        wall = 24;
        m = 4;
        n = 7;
        minSpacePreferLarge(wall, m, n);
    }
}

// This code is contributed by Saket Kumar
```

## 计算机编程语言

```
def minSpacePreferLarge(w, m, n):

    # initialize result variables
    num_m = 0
    num_n = 0
    rem = w

    # p and q are no of shelves of length m &
    # n respectively. r is the remainder uncovered
    # wall length
    p = wall//m
    q = 0
    rem=wall%m;
      num_m=p;
      num_n=q;
      min_empty=rem;
    while (w >= n):
        q += 1;
        wall = wall - n;
        p = w // m
        r = w % m
        if (r <= rem):
            num_m = p
            num_n = q
            rem = r
        q += 1
        w -= n
    print( str(int(num_m)) + " " + str(num_n) + " " + str(rem))

# Driver code
w = 24
m = 3
n = 5
minSpacePreferLarge(w, m, n)

w = 24
m = 4
n = 7
minSpacePreferLarge(w, m, n)
```

## C#

```
// C# program to count all rotation
// divisible by 4.
using System;

class GFG {
    static void minSpacePreferLarge(int wall, int m, int n)
    {
        // For simplicity, Assuming m is always smaller than n
        // initializing output variables
        int num_m = 0, num_n = 0, min_empty = wall;

        // p and q are no of shelves of length m and n
        // rem is the empty space
        int p = wall/m, q = 0, rem=wall%m;
          num_m=p;
          num_n=q;
          min_empty=rem;

        while (wall >= n) {

            q += 1;
            wall = wall - n;
            // place as many shelves of length m
            // in the remaining part

            p = wall / m;
            rem = wall % m;

            // update output variablse if curr
            // min_empty <= overall empty
            if (rem <= min_empty) {
                num_m = p;
                num_n = q;
                min_empty = rem;
            }

            // place one more shelf of length n
            q += 1;
            wall = wall - n;
        }
        Console.WriteLine(num_m + " " + num_n + " " + min_empty);
    }

    // Driver code
    static public void Main()
    {
        int wall = 24, m = 3, n = 5;
        minSpacePreferLarge(wall, m, n);

        wall = 24;
        m = 4;
        n = 7;
        minSpacePreferLarge(wall, m, n);
    }
}

// This code is contributed by Tushil.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum space and units
// of two shelves to fill a wall.

function minSpacePreferLarge($wall, $m, $n)
{
    // for simplicity, Assuming m is always smaller than n
    // initializing output variables
    $num_m = 0;
    $num_n = 0;
    $min_empty = $wall;

    // p and q are no of shelves of length m and n
    // rem is the empty space
    $p = $wall/$m
    $q = 0
    $rem=$wall%$m;
      $num_m=$p;
      $num_n=$q;
      $min_empty=$rem;

    while ($wall >= $n)
    {
        $q += 1;
        $wall = $wall - $n;
        // place as many shelves of length m
        // in the remaining part
        $p = $wall / $m;
        $rem = $wall % $m;

        // update output variablse if curr
        // min_empty <= overall empty
        if ($rem <= $min_empty)
        {
            $num_m = $p;
            $num_n = $q;
            $min_empty = $rem;
        }

        // place one more shelf of length n
        $q += 1;
        $wall = $wall - $n;
    }

    echo $num_m , " ", $num_n , " ",
        $min_empty ,"\n";
}

    // Driver code
    $wall = 24;
    $m = 3;
    $n = 5;
    minSpacePreferLarge($wall, $m, $n);

    $wall = 24;
    $m = 4;
    $n = 7;
    minSpacePreferLarge($wall, $m, $n);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to count all rotation divisible by 4.

    function minSpacePreferLarge(wall, m, n)
    {
        // for simplicity, Assuming m is always smaller than n
        // initializing output variables
        let num_m = 0, num_n = 0, min_empty = wall;

        // p and q are no of shelves of length m and n
        // rem is the empty space
        let p = parseInt(wall/m, 10), q = 0, rem=wall%m;
        num_m=p;
        num_n=q;
        min_empty=rem;
        while (wall >= n) {
            // place one more shelf of length n
            q += 1;
            wall = wall - n;
              // place as many shelves of length m
            // in the remaining part
            p = parseInt(wall / m, 10);
            rem = wall % m;

            // update output variablse if curr
            // min_empty <= overall empty
            if (rem <= min_empty) {
                num_m = p;
                num_n = q;
                min_empty = rem;
            }
        }

        document.write(num_m + " " + num_n + " " + min_empty + "</br>");
    }

    let wall = 29, m = 3, n = 9;
    minSpacePreferLarge(wall, m, n);

    wall = 76, m = 1, n = 10;
    minSpacePreferLarge(wall, m, n);

</script>
```

**Output**

```
0 3 2
6 7 0
```

**参考文献**:sumatory 实习问题
本文由 **Aditi Sharma** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
# 给定一个数字 n，计算集合{1，2，3，… n}中 3 和/或 5 的所有倍数

> 原文:[https://www . geesforgeks . org/给定-number-n-count-multiples-3-and 和-5-set-1-2-3-n/](https://www.geeksforgeeks.org/given-number-n-count-multiples-3-andor-5-set-1-2-3-n/)

给定一个数字 n，计算从 1 到 n 的一组数字中 3 和/或 5 的所有倍数。
示例:

```
Input: n = 6
Output: 3
There are three multiples of 3 and/or 5 in {1, 2, 3, 4, 5, 6}

Input: n = 16
Output: 7
There are two multiples of 7 and/or 5 in {1, 2, .. 16}
The multiples are 3, 5, 6, 9, 10, 12, 15
```

**强烈建议尽量减少浏览器，先自己试试这个。**
n/3 的值给我们数 3 的倍数，n/5 的值给我们数 5 的倍数。但重要的一点是，可能有一些常见的倍数是 3 和 5 的倍数。我们可以用 n/15 得到这样的倍数。下面是计算倍数的程序。

## C++

```
// C++ program to find count of multiples of 3 and 5 in {1, 2, 3, ..n}
#include <iostream>
using namespace std;

unsigned countOfMultiples(unsigned n)
{
   // Add multiples of 3 and 5.  Since common multiples are
   // counted twice in n/3 + n/15, subtract common multiples
   return (n/3 + n/5 - n/15);
}

// Driver program to test above function
int main()
{
   cout << countOfMultiples(6) << endl;
   cout << countOfMultiples(16) << endl;
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of multiples
// of 3 and 5 in {1, 2, 3, ..n}
import java .io.*;
class GFG {

    static long countOfMultiples(long n)
    {

        // Add multiples of 3 and 5.
        // Since common multiples are
        // counted twice in n/3 + n/15,
        // subtract common multiples
        return (n/3 + n/5 - n/15);
    }

    // Driver Code
    static public void main (String[] args)
    {
        System.out.println(countOfMultiples(6));
        System.out.println(countOfMultiples(16));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# python program to find count
# of multiples of 3 and 5 in
# {1, 2, 3, ..n}

def countOfMultiples(n):
    # Add multiples of 3 and 5.
    # Since common multiples are
    # counted twice in n/3 + n/15,
    # subtract common multiples
    return (int(n/3) + int(n/5) - int(n/15));

# Driver program to test
# above function
print(countOfMultiples(6))
print(countOfMultiples(16))

# This code is contributed by Sam007.
```

## C#

```
// C# program to find count of multiples
// of 3 and 5 in {1, 2, 3, ..n}
using System;

public class GFG {

    static uint countOfMultiples(uint n)
    {
        // Add multiples of 3 and 5.
        // Since common multiples are
        // counted twice in n/3 + n/15,
        // subtract common multiples
        return (n/3 + n/5 - n/15);
    }

    // Driver program to test above
    // function
    static public void Main ()
    {
        Console.WriteLine(countOfMultiples(6));

        Console.WriteLine(countOfMultiples(16)) ;
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count of
// multiples of 3 and 5 in
// {1, 2, 3, ..n}

function countOfMultiples($n)
{

    // Add multiples of 3 and 5.
    // Since common multiples are
    // counted twice in n/3 + n/15,
    // subtract common multiples
    return floor(floor($n / 3) +
                 floor($n / 5) -
                 floor($n / 15));
}

// Driver Code
echo countOfMultiples(6),"\n" ;
echo countOfMultiples(16);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
    // Javascript program to find count of multiples
    // of 3 and 5 in {1, 2, 3, ..n}

    function countOfMultiples(n)
    {
        // Add multiples of 3 and 5.
        // Since common multiples are
        // counted twice in n/3 + n/15,
        // subtract common multiples
        return (parseInt(n/3, 10) + parseInt(n/5, 10) - parseInt(n/15, 10));
    }

    document.write(countOfMultiples(6) + "</br>");

      document.write(countOfMultiples(16) + "</br>") ;

</script>
```

输出:

```
3
7
```

时间复杂度:0(1)

辅助空间:0(1)

本文由 **Asif** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息
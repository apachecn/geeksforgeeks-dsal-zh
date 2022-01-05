# 系列 5+55+555+之和..多达 n 个术语

> 原文:[https://www.geeksforgeeks.org/sum-series-555555-n-terms/](https://www.geeksforgeeks.org/sum-series-555555-n-terms/)

求序列中最多 n 项的和:5+55+555+……最多 n.
**例:**

```
Input : 2
Output: 60

Input : 3
Output: 595
```

**方法:**上述问题可以用以下公式解决:

> 总和= 5 + 55 + 555 + …。n 项。
> = 5/9[9 + 99 + 999 + …。n 项]
> = 5/9[(10–1)+(100–1)+(1000–1)+…n 项]
> = 5/9[10 + 100 + 1000 …..–(1+1+…1)]
> = 5/9[10(10<sup>n</sup>–1)/(10–1)+(1+1+…n 次))
> = 50/81(10<sup>n</sup>–1)–5n/9

下面是求给定数列之和的实现:

## C++

```
// C++ program for sum of the
// series 5 + 55 + 555.....n
#include <bits/stdc++.h>
using namespace std;

// function which return the
// the sum of series
int sumOfSeries(int n)
{
    return 0.6172 *
           (pow(10, n) - 1) -
                    0.55 * n;

}

// Driver code
int main()
{
    int n = 2;
    cout << sumOfSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for sum of the
// series 5 + 55 + 555.....n

class GFG
{

    // function which return the
    // the sum of series
    static int sumOfSeries(int n)
    {
        return (int) (0.6172 *
                     (Math.pow(10, n) - 1) -
                                0.55 * n);
    }

    // Driver code
    public static void main(String []args)
    {
        int n = 2;
        System.out.println(sumOfSeries(n));
    }
}

// This code is contributed by UPENDRA BARTWAL.
```

## 蟒蛇 3

```
# python program for sum of the
# series 5 + 55 + 555.....n

def sumOfSeries(n):
    return (int) (0.6172 *
                 (pow(10, n) - 1) -
                        0.55 * n)

# Driver Code
n = 2
print(sumOfSeries(n))

# This code is contributed
# by Upendra Singh Bartwal
```

## C#

```
// C# program for sum of the
// series 5 + 55 + 555.....n
using System;

class GFG
{

    // Function which return the
    // the sum of series
    static int sumOfSeries(int n)
    {
        return (int)(0.6172 *
                    (Math.Pow(10, n) - 1) -
                                 0.55 * n);
    }

    // Driver code
    public static void Main()
    {
        int n = 2;
        Console.Write(sumOfSeries(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for sum of the
//  series 5 + 55 + 555.....n

// function which return the
// the sum of series
function sumOfSeries($n)
{
    return (int)(0.6172 *
                (pow(10, $n) - 1) -
                        0.55 * $n);
}

// Driver code
$n = 2;
echo(sumOfSeries($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript program for sum of the
// series 5 + 55 + 555.....n

    // function which return the
    // the sum of series
    function sumOfSeries(n) {
        return parseInt( (0.6172 * (Math.pow(10, n) - 1) - 0.55 * n));
    }

    // Driver code   
    var n = 2;
    document.write(sumOfSeries(n));

// This code is contributed by aashish1995
</script>
```

**输出:**

```
60
```
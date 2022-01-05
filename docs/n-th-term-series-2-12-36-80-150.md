# 系列 2、12、36、80、150…中的第 n 项。

> 原文:[https://www . geesforgeks . org/n-th-term-series-2-12-36-80-150/](https://www.geeksforgeeks.org/n-th-term-series-2-12-36-80-150/)

给定系列 2、12、36、80、150..求数列的第 n 项。
**例:**

```
Input : 2
Output : 12

Input : 4
Output : 80 
```

如果我们仔细看，我们可以注意到数列是自然数(1，4，9，16，25，…)的平方和立方的和..) + (1, 8, 27, 64, 125, ….).
因此该系列的第 n 个号码是**n^2+n^3**T3

## C++

```
// CPP program to find n-th term of
// the series  2, 12, 36, 80, 150, ..
#include <iostream>
using namespace std;

// Returns n-th term of the series
// 2, 12, 36, 80, 150
int nthTerm(int n)
{
    return (n * n) + (n * n * n);
}

// driver code
int main()
{
    int n = 4;
    cout << nthTerm(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//java program to find n-th term of
// the series 2, 12, 36, 80, 150, ..
import java.util.*;

class GFG
{
    // Returns n-th term of the series
    // 2, 12, 36, 80, 150
    public static int nthTerm(int n)
    {
        return (n * n) + (n * n * n);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4;
        System.out.print(nthTerm(n));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 code to find n-th term of
# the series 2, 12, 36, 80, 150, ..

# Returns n-th term of the series
# 2, 12, 36, 80, 150
def nthTerm( n ):
    return (n * n) + (n * n * n)

# driver code
n = 4
print( nthTerm(n))

# This code is contributed
# by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find n-th term of
// the series 2, 12, 36, 80, 150, ..
using System;

class GFG
{
    // Returns n-th term of the series
    // 2, 12, 36, 80, 150
    public static int nthTerm(int n)
    {
        return (n * n) + (n * n * n);
    }

    // Driver code
    public static void Main()
    {
        int n = 4;
        Console.WriteLine(nthTerm(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th term of
// the series 2, 12, 36, 80, 150, ..

// Returns n-th term of the series
// 2, 12, 36, 80, 150
function nthTerm($n)
{
    return ($n * $n) + ($n * $n * $n);
}

// driver code
$n = 4;
echo(nthTerm($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to find n-th term of
// the series 2, 12, 36, 80, 150, ..

// Returns n-th term of the series
// 2, 12, 36, 80, 150
function nthTerm(n)
{
    return (n * n) + (n * n * n);
}

// driver code
let n = 4;
document.write(nthTerm(n));

// This code is contributed by gfgking
</script>
```

**输出:**

```
80
```
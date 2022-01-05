# 数组乘积程序

> 原文:[https://www.geeksforgeeks.org/program-for-product-of-array/](https://www.geeksforgeeks.org/program-for-product-of-array/)

给定一个数组，求所有数组元素的乘积。
**例:**

```
Input  : ar[] = {1, 2, 3, 4, 5}
Output : 120
Product of array elements is 1 x 2
x 3 x 4 x 5 = 120.

Input  : ar[] = {1, 6, 3}
Output : 18
```

## C

```
// C program to find product of array
// elements.
#include <stdio.h>

int product(int ar[], int n)
{
    int result = 1;
    for (int i = 0; i < n; i++)
        result = result * ar[i];
    return result;
}

// driver code for the above program
int main()
{
    int ar[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(ar) / sizeof(ar[0]);
    printf("%d", product(a, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product of array
// elements.
class GFG{

    static int product(int ar[], int n)
    {
        int result = 1;
        for (int i = 0; i < n; i++)
            result = result * ar[i];
        return result;
    }

    // driver code for the above program
    public static void main(String[] args)
    {
        int ar[] = { 1, 2, 3, 4, 5 };
        int n = ar.length;
        System.out.printf("%d", product(ar, n));
    }
}

// This code is contributed by Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 program to find
# product of array elements.
def product(ar, n):

    result = 1
    for i in range(0, n):
        result = result * ar[i]
    return result

# Driver Code
ar = [ 1, 2, 3, 4, 5 ]
n = len(ar)

print(product(ar, n))

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to find product of array
// elements.
using System;

class GFG {

    static int product(int []ar, int n)
    {
        int result = 1;

        for (int i = 0; i < n; i++)
            result = result * ar[i];

        return result;
    }

    // driver code for the above program
    public static void Main()
    {
        int []ar = { 1, 2, 3, 4, 5 };
        int n = ar.Length;

        Console.WriteLine(product(ar, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find product
// of array elements.

function product($ar, $n)
{
    $result = 1;
    for ($i = 0; $i < $n; $i++)
        $result = $result * $ar[$i];
    return $result;
}

// Driver Code
$ar = array( 1, 2, 3, 4, 5 );
$n = count($ar);
print((int)product($ar, $n));

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to find product of array
// elements.
function product(ar,n)
    {
        let result = 1;
        for (let i = 0; i < n; i++)
            result = result * ar[i];
        return result;
    }

    // driver code for the above program
        let ar = [ 1, 2, 3, 4, 5 ];
        let n = ar.length;
        document.write(parseInt(product(ar, n)));       

    // This code is Contributed by sravan kumar

</script>
```

**输出:**

```
120
```

上述代码可能会导致溢出。因此，总是希望在模下计算乘积。它工作的原因是模的简单分配性质。

```
( a * b) % c = ( ( a % c ) * ( b % c ) ) % c
```

下面是一个程序，用来查找并打印这个数组中所有数字的乘积[模(10^9 +7)](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

## C

```
// C code for above program to find product
// under modulo.
#include <stdio.h>

const int MOD = 1000000007;

int product(int ar[], int n)
{
    int result = 1;
    for (int i = 0; i < n; i++)
        result = (result * ar[i]) % MOD;
    return result;
}

// driver code for the above program
int main()
{
    int ar[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(ar) / sizeof(ar[0]);
    printf("%d", product(ar, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above program to find product
// under modulo.
class GFG {

    static final int MOD = 1000000007;

    static int product(int ar[], int n)
    {
        int result = 1;
        for (int i = 0; i < n; i++)
            result = (result * ar[i]) % MOD;

        return result;
    }

    // driver code for the above program
    public static void main(String[] args)
    {
        int ar[] = { 1, 2, 3, 4, 5 };
        int n = ar.length;

        System.out.printf("%d", product(ar, n));
    }
}

// This code is contributed by  Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# Python 3 code for above
# program to find product
# under modulo.

MOD = 1000000007

def product(ar, n):

    result = 1
    for i in range(0, n):
        result = (result * ar[i]) % MOD
    return result

# driver code for the
# above program
ar = [1, 2, 3, 4, 5]
n = len(ar)

print(product(ar, n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
  // C# code for above program to find product
// under modulo.
using System;
class GFG {

    static  int MOD = 1000000007;

    static int product(int []ar, int n)
    {
        int result = 1;
        for (int i = 0; i < n; i++)
            result = (result * ar[i]) % MOD;

        return result;
    }

    // driver code for the above program
    public static void Main()
    {
        int []ar = { 1, 2, 3, 4, 5 };
        int n = ar.Length;

        Console.WriteLine(product(ar, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for above program
// to find product under modulo.

function product($ar, $n)
{
    $result = 1;
    for ($i = 0; $i < $n; $i++)
        $result = ($result *
                   $ar[$i]) % 1000000007;
    return $result;
}

// Driver Code
$ar = array( 1, 2, 3, 4, 5 );
$n = count($ar);
print(product($ar, $n));

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript code for above program to find product under modulo.

    let MOD = 1000000007;

    function product(ar, n)
    {
        let result = 1;
        for (let i = 0; i < n; i++)
            result = (result * ar[i]) % MOD;

        return result;
    }

    let ar = [ 1, 2, 3, 4, 5 ];
    let n = ar.length;

    document.write(product(ar, n));

</script>
```

**输出:**

```
120
```

本文由**希瓦尼·巴盖尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
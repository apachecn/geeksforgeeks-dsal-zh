# 等概率生成 1 到 7 的整数

> 原文:[https://www . geesforgeks . org/generate-integer-从 1 到 7 等概率/](https://www.geeksforgeeks.org/generate-integer-from-1-to-7-with-equal-probability/)

给定一个以相等概率返回 1 到 5 之间的整数的函数 foo()，只使用 foo()编写一个以相等概率返回 1 到 7 之间的整数的函数。尽量减少对 foo()方法的调用次数。此外，不允许使用任何其他库函数，也不允许使用浮点运算。
**解:**
我们知道 foo()返回 1 到 5 的整数。我们如何保证 1 到 7 的整数以相等的概率出现？
如果我们以某种方式以相等的概率生成从 1 到 7 的倍数(如 7、14、21、…)的整数，我们可以使用 7 的模除，然后加上 1，以相等的概率得到从 1 到 7 的数字。
我们可以使用以下表达式以相等的概率生成 1 到 21。

```
 5*foo() + foo() -5 
```

让我们看看如何使用上面的表达式。
1。对于第一个 foo()的每个值，第二个 foo()的值可以有 5 种可能的组合。总共有 25 种可能的组合。
2。上式返回的值的范围是 1 到 25，每个整数恰好出现一次。
3。如果方程的值小于 22，返回模除以 7，然后加 1。否则，再次递归调用该方法。因此，返回每个整数的概率变成 1/7。
下面的程序显示，表达式将从 1 到 25 的每个整数精确地返回一次。

## C++

```
#include <stdio.h>

int main()
{
    int first, second;
    for ( first=1; first<=5; ++first )
        for ( second=1; second<=5; ++second )
            printf ("%d \n", 5*first + second - 5);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to demonstrate
// expression returns each integer
// from 1 to 25 exactly once

class GFG {
    public static void main(String[] args)
    {
        int first, second;
        for ( first=1; first<=5; ++first )
            for ( second=1; second<=5; ++second )
            System.out.printf ("%d \n", 5*first + second - 5);
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 code to demonstrate
# expression returns each integer
# from 1 to 25 exactly once

if name == '__main__':

    for first in range(1, 6):
        for second in range(1, 6):
                print(5 * first + second - 5)

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# code to demonstrate expression returns
// each integer from 1 to 25 exactly once
using System;

class GFG {

    public static void Main()
    {
        int first, second;

        for ( first = 1; first <= 5; ++first )
            for ( second = 1; second <= 5; ++second )
                Console.WriteLine ( 5*first + second - 5);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Generate integer
// from 1 to 7 with equal probability

    $first;
    $second;
    for ( $first = 1; $first <= 5; ++$first )
        for ( $second = 1; $second <= 5; ++$second )
            echo 5 * $first + $second - 5, "\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript Program to demonstrate
// expression returns each integer
// from 1 to 25 exactly once

// Driver Code

    let first, second;
    for ( first=1; first<=5; ++first )
        for ( second=1; second<=5; ++second ) {
             document.write( 5*first + second - 5);
             document.write("<br />");
        }

</script>
```

**输出:**

```
1
2
.
.
24
25
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

下面的程序描述了我们如何使用 foo()以相等的概率返回 1 到 7。

## C++

```
// C++ program to Generate integer from
// 1 to 5 with equal probability
#include <stdio.h>

// given method that returns 1 to 5 with equal probability
int foo()
{
    // some code here
}

int my_rand() // returns 1 to 7 with equal probability
{
    int i;
    i = 5*foo() + foo() - 5;
    if (i < 22)
        return i%7 + 1;
    return my_rand();
}
// Driver code
int main()
{
    printf ("%d ", my_rand());
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Generate integer from
// 1 to 5 with equal probability
class GfG
{

// given method that returns 1 to 5 with equal probability
static int foo()
{
    // some code here
    return 0;
}

// returns 1 to 7 with equal probability
public static int my_rand() 
{
    int i;
    i = 5*foo() + foo() - 5;
    if (i < 22)
        return i%7 + 1;
    return my_rand();
}

// Driver code
public static void main (String[] args) {

    System.out.println(my_rand());
}
}
```

## 蟒蛇 3

```
# Python3 program to Generate integer
# from 1 to 5 with equal probability
# given method that returns 1 to 5
# with equal probability
def foo():

    # some code here
    return 0;

# returns 1 to 7 with equal probability
def my_rand():
    i = 0;
    i = (5 * foo()) + (foo() - 5);
    if (i < 22):
        if(i < 0):
            return (i % 7 - 7) + 1;
        else:
            return (i % 7) + 1;

    return my_rand();

# Driver code
if __name__ == '__main__':
    print(my_rand());

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program to Generate integer from
// 1 to 5 with equal probability
using System;
class GfG
{

// given method that returns 1 to 5 with equal probability
static int foo()
{
    // some code here
    return 0;
}

// returns 1 to 7 with equal probability
public static int my_rand() 
{
    int i;
    i = 5*foo() + foo() - 5;
    if (i < 22)
        return i%7 + 1;
    return my_rand();
}

// Driver code
public static void Main () {

    Console.Write(my_rand()+"\n");
}
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Generate integer from
// 1 to 5 with equal probability
// given method that returns 1 to 5
// with equal probability
function foo()
{
    // some code here
}

// returns 1 to 7 with equal probability
function my_rand()
{
    $i;
    $i = 5 * foo() + foo() - 5;
    if ($i < 22)
        return $i % 7 + 1;
    return my_rand();
}

// Driver code
echo my_rand();

// This code is contributed by Tushil.
?>
```

## java 描述语言

```
<script>

// Javascript program to Generate integer from
// 1 to 5 with equal probability

    // given method that returns 1 to 5 with equal probability
    function foo()
    {
        // some code here
        return 0;
    }

    // returns 1 to 7 with equal probability
    function my_rand()
    {
        let i;
        i = 5*foo() + foo() - 5;
        if (i < 22)
            return i%7 + 1;
        return my_rand();
    }

    // Driver code
    document.write(my_rand());

    // This code is contributed by rag2127

</script>
```

**输出:**

```
-4
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

本文由**aashis Barnwal**编辑，GeeksforGeeks 团队审核。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息
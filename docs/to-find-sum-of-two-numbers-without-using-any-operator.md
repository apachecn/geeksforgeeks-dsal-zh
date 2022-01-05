# 不使用任何运算符求两个数的和

> 原文:[https://www . geesforgeks . org/to-find-sum-of-two-numbers-无需使用任何运算符/](https://www.geeksforgeeks.org/to-find-sum-of-two-numbers-without-using-any-operator/)

写一个程序，不用任何运算符就能求出正整数的和。只允许使用 printf()。不能使用其他库函数。

**解**
这是个恶作剧问题。我们可以使用 printf()来求两个数的和，因为 printf()返回打印的字符数。printf() 中的[宽度字段可以用来求两个数的和。我们可以使用“*”来表示输出的最小宽度。例如，在语句“printf(“% * d”，width，num)；”，指定的“宽度”将代替*，而“数字”将在指定的最小宽度内打印。如果“num”中的位数小于指定的“width”，则输出会用空格填充。如果位数较多，输出按原样打印(不截断)。在下面的程序中，add()返回 x 和 y 的总和。它在使用 x 和 y 指定的宽度内打印 2 个空格。因此打印的字符总数等于 x 和 y 的总和。这就是 add()返回 x+y 的原因。](http://www.cplusplus.com/reference/clibrary/cstdio/printf/)

## C++

```
#include <iostream>
using namespace std;

int add(int x, int y)
{
    return printf("%*c%*c", x, ' ', y, ' ');
}

// Driver code
int main()
{
    printf("Sum = %d", add(3, 4));
    return 0;
}

// This code is contributed by shubhamsingh10
```

## C

```
#include <stdio.h>

int add(int x, int y)
{
    return printf("%*c%*c", x, ' ', y, ' ');
}

// Driver code
int main()
{
    printf("Sum = %d", add(3, 4));
    return 0;
}
```

**输出:**

```
       Sum = 7
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

输出是七个空格，后跟“Sum = 7”。我们可以通过回车来避免前导空格。感谢 **krazyCoder** 和 **Sandeep** 的建议。以下程序打印输出时没有任何前导空格。

## C++

```
#include <iostream>
using namespace std;

int add(int x, int y)
{
    return printf("%*c%*c", x, '\r', y, '\r');
}

// Driver code
int main()
{
    printf("Sum = %d", add(3, 4));
    return 0;
}

// This code is contributed by shubhamsingh10
```

## C

```
#include <stdio.h>

int add(int x, int y)
{
    return printf("%*c%*c", x, '\r', y, '\r');
}

// Driver code
int main()
{
    printf("Sum = %d", add(3, 4));
    return 0;
}
```

**输出:**

```
      Sum = 7
```

**时间复杂度:** O(1)

**辅助空间:** O(1)

另一种方法:

## C++

```
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 5;
    if (b > 0) {
        while (b > 0) {
            a++;
            b--;
        }
    }
    if (b < 0) { // when 'b' is negative
        while (b < 0) {
            a--;
            b++;
        }
    }
    cout << "Sum = " << a;
    return 0;
}

// This code is contributed by SHUBHAMSINGH10
// This code is improved & fixed by Abhijeet Soni.
```

## C

```
#include <stdio.h>

int main()
{
    int a = 10, b = 5;
    if (b > 0) {
        while (b > 0) {
            a++;
            b--;
        }
    }
    if (b < 0) { // when 'b' is negative
        while (b < 0) {
            a--;
            b++;
        }
    }
    printf("Sum = %d", a);
    return 0;
}

// This code is contributed by Abhijeet Soni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code
class GfG {

    public static void main(String[] args)
    {
        int a = 10, b = 5;
        if (b > 0) {
            while (b > 0) {
                a++;
                b--;
            }
        }
        if (b < 0) { // when 'b' is negative
            while (b < 0) {
                a--;
                b++;
            }
        }
        System.out.println("Sum is: " + a);
    }
}

// This code is contributed by Abhijeet Soni
```

## 蟒蛇 3

```
# Python 3 Code

if __name__ == '__main__':

    a = 10
    b = 5

    if b > 0:
        while b > 0:
            a = a + 1
            b = b - 1
    if b < 0:
        while b < 0:
            a = a - 1
            b = b + 1

    print("Sum is: ", a)

# This code is contributed by Akanksha Rai
# This code is improved & fixed by Abhijeet Soni
```

## C#

```
// C# code
using System;

class GFG {
    static public void Main()
    {
        int a = 10, b = 5;
        if (b > 0) {
            while (b > 0) {
                a++;
                b--;
            }
        }
        if (b < 0) { // when 'b' is negative
            while (b < 0) {
                a--;
                b++;
            }
        }
        Console.Write("Sum is: " + a);
    }
}

// This code is contributed by Tushil
// This code is improved & fixed by Abhijeet Soni.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code
$a = 10;
$b = 5;

if ($b > 0) {
while($b > 0)
{
    $a++;
    $b--;
}
}

if ($b < 0) {
while($b < 0)
{
    $a--;
    $b++;
}
}

echo "Sum is: ", $a;

// This code is contributed by Dinesh
// This code is improved & fixed by Abhijeet Soni.
?>
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Driver Code

    let a = 10, b = 5;
    if (b > 0) {
        while (b > 0) {
            a++;
            b--;
        }
    }
    if (b < 0) { // when 'b' is negative
        while (b < 0) {
            a--;
            b++;
        }
    }
    document.write("Sum = " + a);

</script>
```

**输出:**

```
sum = 15
```

***时间复杂度:** O(b)*

***辅助空间:** O(1)*

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息
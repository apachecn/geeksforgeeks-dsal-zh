# 编程难题(赋值时不含任何控制语句)

> 原文:[https://www . geesforgeks . org/programming-拼图-赋值-不带控制-语句/](https://www.geeksforgeeks.org/programming-puzzle-assign-value-without-control-statement/)

给定四个整数' a '，' b '，' y '和' x '，其中' x '只能是零或一。你的任务如下:

*   如果“x”为零，则为变量“y”赋值“a”
*   如果“x”是一个，则为变量“y”赋值“b”。

不允许使用任何条件运算符(包括三元运算符)。
**例:**

```
Input  : a = 3, b = 7,  x = 1
Output : y = 7

Input : a = 3, b = 7, x = 0
Output : y = 3
```

想法是创建一个大小为 2 的数组，其中第一个元素是“a”，第二个元素是“b”。我们使用 x 作为数组中的索引。

## C++

```
// CPP program to pick a value among two
// according to value of a third variable.
#include <iostream>
using namespace std;

// Returns a if x is 0 and returns
// b if x is 1.
int assignValue(int a, int b, bool x)
{
    int arr[] = {a, b};

    return(arr[x]);
}

// Driver code
int main()
{
    int y = assignValue(3, 7, 0);
    cout << y;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to pick a value among two
// according to value of a third variable.
class GFG {

    // Returns a if x is 0 and returns
    // b if x is 1.
    static int assignValue(int a, int b, int x)
    {
        int arr[] = {a, b};

        return (arr[x]);
    }

    // Driver code
    public static void main(String[] args)
    {
        int y = assignValue(3, 7, 0);
        System.out.println(y);
    }
}

// This code is contributed by  Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# Python 3 program to
# pick a value among two
# according to value
# of a third variable.

# Returns a if x
# is 0 and returns
# b if x is 1.
def assignValue(a, b, x):

    arr = [a, b]
    return(arr[x])

# Driver code
y = assignValue(3, 7, 0)

print(y)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to pick a value among two
// according to value of a third variable.
using System;

public class GFG {

    // Returns a if x is 0 and returns
    // b if x is 1.
    static int assignValue(int a, int b, int x)
    {
        int []arr = {a, b};

        return (arr[x]);
    }

    // Driver code
    public static void Main()
    {
        int y = assignValue(3, 7, 0);
        Console.WriteLine(y);
    }
}
// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to pick a value
// among two according to value
// of a third variable.

// Returns a if x is 0 and
// returns b if x is 1.

function assignValue($a, $b, $x)
{
    $arr = array($a, $b);

    return($arr[$x]);
}

// Driver code
$y = assignValue(3, 7, 0);
echo $y;

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript program to pick a value among two
// according to value of a third variable.   
// Returns a if x is 0 and returns
    // b if x is 1.
    function assignValue(a , b , x) {
        var arr = [ a, b ];

        return (arr[x]);
    }

    // Driver code

        var y = assignValue(3, 7, 0);
        document.write(y);

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
 3
```

**备选方案:**

## C++

```
// C++ program to pick a value among two
// according to value of a third variable.
#include <iostream>
using namespace std;

// Returns a if x is 0 and returns
// b if x is 1.
int assignValue(int a, int b, bool x)
{  
    return (1 - x)*a + x*b;
}

// Driver code
int main()
{
    int y = assignValue(3, 7, 0);
    cout << y;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to pick a value among two
// according to value of a third variable.
import java.io.*;

class GFG {

// Returns a if x is 0 and returns
// b if x is 1.
static int assignValue(int a, int b, int x)
{
    return (1 - x) * a + x * b;
}

// Driver code
public static void main (String[] args)
{
    int y = assignValue(3, 7, 0);

    System.out.println(y);
}
}

// This code is contributed by ShubhamCoder
```

## 蟒蛇 3

```
# Python3 program to pick a value among two
# according to the value of a third variable.

# Returns a if x is 0 and returns
# b if x is 1.
def assignValue(a, b, x):

    return (1 - x) * a + x * b

# Driver code
y = assignValue(3, 7, 0)
print(y)

# This code is contributed by ShubhamCoder
```

## C#

```
// C# program to pick a value among two
// according to value of a third variable.
using System;

class GFG {

// Returns a if x is 0 and returns
// b if x is 1.
static int assignValue(int a, int b, int x)
{
    return (1 - x) * a + x * b;
}

// Driver code
public static void Main()
{
    int y = assignValue(3, 7, 0);

    Console.WriteLine(y);
}
}

// This code is contributed by ShubhamCoder
```

## java 描述语言

```
<script>

// Javascript program to pick a value among two
// according to value of a third variable.

    // Returns a if x is 0 and returns
    // b if x is 1.
    function assignValue(a , b , x) {
        return (1 - x) * a + x * b;
    }

    // Driver code

        var y = assignValue(3, 7, 0);

        document.write(y);

// This code contributed by Rajput-Ji

</script>
```

**输出:**

```
3
```

**时间复杂度:** O(1)
感谢福里斯特·史密斯提出上述解决方案。
本文由 [**马吉德·巴希尔**](https://auth.geeksforgeeks.org/profile.php?user=Maajid Bashir) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
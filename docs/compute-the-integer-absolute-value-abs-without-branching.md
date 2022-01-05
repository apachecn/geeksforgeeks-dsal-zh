# 计算无分支的整数绝对值(ABS)

> 原文:[https://www . geesforgeks . org/compute-the-integer-绝对值-ABS-不带分支/](https://www.geeksforgeeks.org/compute-the-integer-absolute-value-abs-without-branching/)

如果一个数字是正数，我们就不需要做任何事情。我们只想改变负数。由于负数以 [2 的补码](http://en.wikipedia.org/wiki/Two%27s_complement)形式存储，为了得到负数的绝对值，我们必须切换该数的位，并在结果上加 1。
例如，8 位系统中的-2 存储如下:1 1 1 1 1 1 0，其中最左边的位是符号位。为了得到负数的绝对值，我们必须切换所有的位，并将 1 加到切换的数字上，即 0 0 0 0 0 0 1 + 1 将给出绝对值 1 1 1 1 1 1 1 0。还要记住，只有当数字为负(符号位被设置)时，我们才需要执行这些操作。
**方法 1**
1)将掩码设置为整数右移 31(假设使用 32 位存储整数)。

```
 mask = n>>31 
```

2)对于负数，上述步骤将掩码设置为 1 1 1 1 1 1 1，对于正数设置为 0 0 0 0 0 0 0。给定的数字加上掩码。

```
 mask + n 
```

3)掩码+n 与掩码的异或给出绝对值。

```
 (mask + n)^mask 
```

实施:

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define CHARBIT 8

/* This function will return absolute value of n*/
unsigned int getAbs(int n)
{
    int const mask = n >> (sizeof(int) * CHARBIT - 1);
    return ((n + mask) ^ mask);
}

/* Driver program to test above function */
int main()
{
    int n = -6;
    cout << "Absolute value of " << n << " is " << getAbs(n);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>
#define CHAR_BIT 8

/* This function will return absolute value of n*/
unsigned int getAbs(int n)
{
    int const mask = n >> (sizeof(int) * CHAR_BIT - 1);
    return ((n + mask) ^ mask);
}

/* Driver program to test above function */
int main()
{
    int n = -6;
    printf("Absolute value of %d is %u", n, getAbs(n));

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG {

    static final int CHAR_BIT = 8;
    static final int SIZE_INT = 8;

    /* This function will return absolute value of n*/
    static int getAbs(int n)
    {
        int mask = n >> (SIZE_INT * CHAR_BIT - 1);
        return ((n + mask) ^ mask);
    }

    /* Driver code */
    public static void main(String[] args)
    {
        int n = -6;
        System.out.print("Absolute value of " + n + " is " + getAbs(n));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of above approach
CHARBIT = 8;
SIZE_INT = 8;

# This function will return
# absolute value of n
def getAbs(n):
    mask = n >> (SIZE_INT * CHARBIT - 1);
    return ((n + mask) ^ mask);

# Driver Code
n = -6;
print("Absolute value of",n,"is",getAbs(n));

# This code is contributed by mits
```

## C#

```
// C# implementation of above approach
using System;

class GFG {

    static int CHAR_BIT = 8;
    static int SIZE_INT = 8;

    /* This function will return absolute value of n*/
    static int getAbs(int n)
    {
        int mask = n >> (SIZE_INT * CHAR_BIT - 1);
        return ((n + mask) ^ mask);
    }

    /* Driver code */
    static void Main()
    {
        int n = -6;
        Console.Write("Absolute value of " + n + " is " + getAbs(n));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach
$CHARBIT = 8;
$SIZE_INT = 8;

// This function will return
// absolute value of n
function getAbs($n)
{
    global $SIZE_INT, $CHARBIT;
    $mask = $n >> ($SIZE_INT * $CHARBIT - 1);
    return (($n + $mask) ^ $mask);
}

// Driver Code
$n = -6;
echo "Absolute value of " . $n .
            " is " . getAbs($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript implementation of above approach   
var CHAR_BIT = 8;
var SIZE_INT = 8;

    /* This function will return absolute value of n */
    function getAbs(n)
    {
        var mask = n >> (SIZE_INT * CHAR_BIT - 1);
        return ((n + mask) ^ mask);
    }

    /* Driver code */
        var n = -6;
        document.write("Absolute value of " + n + " is " + getAbs(n));

// This code is contributed by shikhasingrajput
</script>
```

**输出:**

```
Absolute value of -6 is 6
```

**方法 2:**
1)将掩码设置为整数右移 31(假设使用 32 位存储整数)。

```
 mask = n>>31 
```

2)将掩码与数字
异或

```
 mask ^ n 
```

3)从步骤 2 的结果中减去掩码并返回结果。

```
 (mask^n) - mask 
```

实施:

## c

```
/* This function will return absolute value of n*/
unsigned int getAbs(int n)
{
    int const mask = n >> (sizeof(int) * CHAR_BIT - 1);
    return ((n ^ mask) - mask);
}
```

在分支昂贵的机器上，上面的表达式可以比显而易见的方法更快，关于以上两种方法的更多细节，请参见[本](http://graphics.stanford.edu/~seander/bithacks.html#IntegerAbs)。
如发现以上任何解释/算法不正确，或有更好的方法解决同一问题，请写评论。
**参考文献:**
[http://graphics . Stanford . edu/~ seander/bithacks . html # integerabas](http://graphics.stanford.edu/~seander/bithacks.html#IntegerAbs)
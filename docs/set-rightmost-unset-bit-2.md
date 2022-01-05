# 设置最右边的未设置位

> 原文:[https://www.geeksforgeeks.org/set-rightmost-unset-bit-2/](https://www.geeksforgeeks.org/set-rightmost-unset-bit-2/)

给定一个非负数 n .问题是设置 n 的二进制表示中最右边的未设置位
**示例:**

```
Input : 21
Output : 23
(21)10 = (10101)2
Rightmost unset bit is at position 2(from right) as 
highlighted in the binary representation of 21.
(23)10 = (10111)2
The bit at position 2 has been set.

Input : 2
Output : 3
```

一种方法在这篇[文章](https://www.geeksforgeeks.org/set-rightmost-unset-bit/)
中讨论，这篇文章讨论另一种方法。
让输入数为 n。n+1 将使所有位翻转到最右边的未设置位(包括未设置位)之后。所以，做 n|(n+1)会得到我们需要的结果。

## C++

```
#include <stdio.h>

// sets the rightmost unset bit
// of n and returns the result
int fun(unsigned int n)
{
    return n | (n + 1);
}

// Driver Code
int main()
{
    int n = 5;
    printf("The number after setting the");
    printf(" rightmost unset bit %d", fun(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {

    // sets the rightmost unset bit
    // of n and returns the result
    static int fun(int n)
    {
        return n | (n + 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        System.out.printf("The number "
                  + "after setting the");
        System.out.printf(" rightmost "
              + " unset bit %d", fun(n));
    }
}

// This code is contributed by Smitha
```

## 蟒蛇 3

```
# sets the rightmost unset bit
# of n and returns the result
def fun(n):

    return n | (n + 1)

# Driver Code
n = 5
print("The number after setting the", end="")
print(" rightmost unset bit ", fun(n))

# This code is contributed by Smitha
```

## C#

```
using System;

class GFG {

    // sets the rightmost unset bit
    // of n and returns the result
    static int fun(int n)
    {
        return n | (n + 1);
    }

    // Driver Code
    public static void Main()
    {
        int n = 5;
        Console.Write("The number "
            + "after setting the");
        Console.Write(" rightmost "
           + "unset bit "+ fun(n));
    }
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Set the rightmost
// unset bit

// sets the rightmost unset bit
// of n and returns the result
function fun($n)
{
    return $n | ($n + 1);
}

    // Driver Code
    $n = 5;
    echo "The number after setting the";
    echo " rightmost unset bit ", fun($n);

// This code is contributed m_kit
?>
```

## java 描述语言

```
<script>
// sets the rightmost unset bit
// of n and returns the result
function fun(n)
{
    return n | (n + 1);
}

// Driver Code
    let n = 5;
    document.write("The number after setting the");
    document.write(" rightmost unset bit ", fun(n));

// This code is contributed by Manoj.
</script>
```

输出:

```
The number after setting the rightmost unset bit 7
```

**时间复杂度:** O(1)

**辅助空间:** O(1)
# 给定数除以二的最高幂

> 原文:[https://www . geeksforgeeks . org/给定数字的最高二次幂/](https://www.geeksforgeeks.org/highest-power-of-two-that-divides-a-given-number/)

给定一个数 n，求除以 n 的 2 的最高幂。
**例:**

> **输入:n = 48**
> **输出:16**
> **2 除以 48 的最高幂是 16。**
> **输入:n = 5**
> **输出:1**
> **2 除以 5 的最高幂是 1。**

一个**简单的解决方法**就是从 1 开始逐个尝试 2 的所有次方，然后是 2，然后是 4，以此类推。
一个**高效解决方案**基于[位魔法](https://www.geeksforgeeks.org/category/algorithm/bit-magic/)。如果我们仔细看看，我们可以注意到，我们基本上需要找到最右边的位设置在与 n 相同的位置，所有其他位都为 0 的数字。比如 n = 5 (10 **1** ，我们的输出是 00 **1** 。对于 n = 48 (1 **1** 0000)，我们的输出是 0 **1** 0000
*如何找到一个最右置位和所有其他位都为 0 的数字？*
我们按照以下步骤进行。
设 n = 48(00110000)
n 减 1，即我们做 **n-1** 。我们得到 47(00101111)
做(n-1)的否定，即我们做 **~(n-1)** 。我们得到(11010000)。
做 n & **(~(n-1))** ，我们得到 00010000，值 16。
以下是上述方法的实施:

## C++

```
// CPP program to find highest power
// of 2 that divides n.
#include<iostream>
using namespace std;

int highestPowerOf2(int n)
{
    return (n & (~(n - 1)));
}

int main()
{
    int n = 48;
    cout << highestPowerOf2(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find highest power
// of 2 that divides n.

class GFG
{

static int highestPowerOf2(int n)
{
    return (n & (~(n - 1)));
}

public static void main(String []args)
{
    int n = 48;
    System.out.println(highestPowerOf2(n));
}
}
```

## 蟒蛇 3

```
# Python3 program to find highest power
# of 2 that divides n.

def highestPowerOf2(n):

    return (n & (~(n - 1)))

#Driver code
if __name__=='__main__':
    n = 48
    print(highestPowerOf2(n))

# this code is contributed
# by ash264
```

## C#

```
// C# program to find highest power
// of 2 that divides n.
using System;

class GFG
{

static int highestPowerOf2(int n)
{
    return (n & (~(n - 1)));
}

public static void Main()
{
    int n = 48;
    Console.Write(highestPowerOf2(n));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find highest power
// of 2 that divides n.

function highestPowerOf2($n)
{
    return ($n & (~($n - 1)));
}

// Driver Code
$n = 48;
echo highestPowerOf2($n);

// This code is contributed
// by Sach_Code..
?>
```

## java 描述语言

```
<script>

// javascript program to find highest power
// of 2 that divides n.

function highestPowerOf2(n)
{
    return (n & (~(n - 1)));
}

var n = 48;
document.write(highestPowerOf2(n));

// This code is contributed by 29AjayKumar

</script>
```

**Output**

```
16
```

**方法–2:**这也是一种有效的方法，可以使用 C 语言中的预定义函数来处理位，从而找到数字“n”的二次幂的最大除数。也就是[**_ builtin _ ctz(n)**](https://www.geeksforgeeks.org/builtin-functions-gcc-compiler/)**，**这个功能帮助你找到数字的尾随零，然后你就可以看到比特-魔法。

> **输入:n = 48 ~= (110000) <sub>2</sub> //尾随零个数为= 4，所以尾随零个数= 4**
> 
> **输出:1<T3】4 = 16//幂(2，4)= 16 2 除以 48 的最高幂是 16。**
> 
> **输入:n = 21 ~= (10101) <sub>2</sub> //无尾随零，因此尾随零个数= 0**
> 
> **输出:1<T3】0 = 2//pow(2，0)=1**

**注:** [**要详细了解这类位屏蔽功能，可以浏览本文。**](https://www.geeksforgeeks.org/builtin-functions-gcc-compiler/)

## C

```
#include <stdio.h>
int main()
{
    int n = 21;     
    int m = 48;
    printf("for %d is %d ",
           n,(1<< __builtin_ctz(n)));
    printf("\nfor %d is %d ",
           m,(1<< __builtin_ctz(m)));
    return 0;
}
```

**Output**

```
for 21 is 1 
for 48 is 16 
```
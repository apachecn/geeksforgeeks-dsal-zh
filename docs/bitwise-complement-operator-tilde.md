# 按位补码运算符(~颚化符)

> 原文:[https://www . geeksforgeeks . org/bitwise-complex-operator-tilde/](https://www.geeksforgeeks.org/bitwise-complement-operator-tilde/)

**先决条件:**
[C/c++](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)中的按位运算符
[Java 中的按位运算符](https://www.geeksforgeeks.org/bitwise-operators-in-java/)

按位补码运算符是一元运算符 (仅适用于一个操作数)。它取一个数字，然后把它的所有位反转。当按位运算符应用于位时，所有的 1 变成 0，反之亦然。按位补码的运算符是 **~(颚化符)。**

**示例:**

> **输入:**~ 0000 0011
> T3】输出: 1111 1100
> 
> **输入:**1110 0111
> T3】输出: 0001 1000

应谨慎使用按位补码运算符。如果结果存储在无符号变量中，那么~运算符对一个小数字的结果可以是一个大数字。如果结果存储在有符号变量中，则结果可能是负数(假设负数以 2 的补码形式存储，其中最左边的位是符号位)。

> **输入:**
> n = 2
> 二进制形式的 2 = 0010
> 对 2 = ~ 0010
> = 1101
> 1101 的按位补码运算相当于十进制值 13。
> 
> **预期输出:**13
> T3】正确输出: -3
> 
> 编译器返回输入值的 2 的补码。

## C

```
// C program to implement
// the above approach
#include <stdio.h>

// Driver code
int main()
{
  int n = 2;
  printf("Bitwise complement of %d : %d",
          n, ~n);
  return 0;
}
```

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
using namespace std;

// Driver code
int main()
{
  int a = 2;
  cout << "Bitwise complement of " <<
           a << " : " << ~a;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

// Driver code
class GFG
{
    public static void main (String[] args)
    {
        int a = 2;
        System.out.println("Bitwise complement of " +
                            a + " : " + ~a);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Driver code
n = 2
print("Bitwise complement of {n} :",
       ~n)
```

## C#

```
// C# program to implement 
// the above approach
using System;

class GFG{

static public void Main()
{
    int a = 2;

    Console.WriteLine("Bitwise complement of " + a +
                      " : " + ~a);
}
}
```

## java 描述语言

```
<script>

// JavaScript program to implement 
// the above approach

// Driver code
let a = 2;
document.write("Bitwise complement of " +
               a + " : " + ~a);

// This code is contributed by Potta Lokesh

</script>
```

**输出:**

> 2 的按位补码:-3

**解释:**
2(~ 2)的按位补码是-3 而不是 13，但是为什么呢？
当数字以 10 为基数打印时，非运算的结果可能会令人惊讶。特别是正数可以变成负数，反之亦然。

让我们首先找到 2 的按位补码的二进制表示，它是-3

> 负数存储为正数的二进制补码。

**2 的补码:**
2 的补码是对二进制数的运算。一个数的 2 的补码等于该数的补码加 1。

**示例:**

> **2(~ 0010)的逐位补码运算:** 1101
> 
> **计算 3 的 2 的补码:**
> **3 的二进制形式=**0011
> **3 的 1 的补码=** 1100
> **将 1 加 1 的补码=** 1100 +1
> **2 的 3 的补码=** 1101
> 
> **注:**
> 2 的按位补码与-3 的二进制表示相同

因此，从上面的例子可以得出结论-

1.  对于任意整数 n，n 的按位补码将是-(n+1)。
2.  N = ~N 的按位补码(以 2 的补码形式表示)。
3.  ~N= -(~(~N)+1) = -(N+1)的 2’补码。
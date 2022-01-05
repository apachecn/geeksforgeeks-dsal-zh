# 尾部递归

> 原文:[https://www.geeksforgeeks.org/tail-recursion/](https://www.geeksforgeeks.org/tail-recursion/)

**什么是尾部递归？**
当递归调用是函数执行的最后一件事时，递归函数是尾部递归的。例如下面的 C++函数 print()是尾部递归的。

## C

```
// An example of tail recursive function
void print(int n)
{
    if (n < 0)  return;
    cout << " " << n;

    // The last executed statement is recursive call
    print(n-1);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An example of tail recursive function
static void print(int n)
{
    if (n < 0)
      return;

    System.out.print(" " + n);

    // The last executed statement
      // is recursive call
    print(n - 1);
}

// This code is contributed by divyeh072019
```

## 蟒蛇 3

```
# An example of tail recursive function
def prints(n):

    if (n < 0):
        return
    print(str(n), end=' ')

    # The last executed statement is recursive call
    prints(n-1)

    # This code is contributed by Pratham76
    # improved by ashish2021
```

## C#

```
// An example of tail recursive function
static void print(int n)
{
    if (n < 0)
      return;

    Console.Write(" " + n);

    // The last executed statement
      // is recursive call
    print(n - 1);
}

// This code is contributed by divyeshrabadiya07
```

**我们为什么在乎？**
尾部递归函数被认为比非尾部递归函数更好，因为尾部递归可以被编译器优化。编译器通常通过使用**栈**来执行递归过程。这个堆栈包含所有相关信息，包括每个递归调用的参数值。当一个过程被调用时，它的信息被**推到**栈上，当函数终止时，信息被**弹出**栈。因此对于非尾部递归函数来说，**堆栈深度**(编译期间任何时候使用的最大堆栈空间量)更多。编译器优化尾部递归函数的思路很简单，由于递归调用是最后一条语句，当前函数没有什么可做的，所以保存当前函数的栈帧是没有用的(详见[本](https://www.geeksforgeeks.org/tail-call-elimination/))。

**非尾递归函数可以写成尾递归来优化吗？**
考虑以下函数计算 n 的阶乘，它是非尾递归函数。虽然乍一看像是尾部递归。如果我们仔细观察，我们可以看到事实(n-1)返回的值在事实(n)中使用，因此对事实(n-1)的调用不是事实(n)做的最后一件事

## C++

```
#include<iostream>
using namespace std;

// A NON-tail-recursive function.  The function is not tail
// recursive because the value returned by fact(n-1) is used in
// fact(n) and call to fact(n-1) is not the last thing done by fact(n)
unsigned int fact(unsigned int n)
{
    if (n == 0) return 1;

    return n*fact(n-1);
}

// Driver program to test above function
int main()
{
    cout << fact(5);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {

    // A NON-tail-recursive function.
    // The function is not tail
    // recursive because the value
    // returned by fact(n-1) is used
    // in fact(n) and call to fact(n-1)
    // is not the last thing done by
    // fact(n)
    static int fact(int n)
    {
        if (n == 0) return 1;

        return n*fact(n-1);
    }

    // Driver program
    public static void main(String[] args)
    {
        System.out.println(fact(5));
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# A NON-tail-recursive function.
# The function is not tail
# recursive because the value
# returned by fact(n-1) is used
# in fact(n) and call to fact(n-1)
# is not the last thing done by
# fact(n)
def fact(n):

    if (n == 0):
        return 1

    return n * fact(n-1)

# Driver program to test
# above function
print(fact(5))
# This code is contributed by Smitha.
```

## C#

```
using System;

class GFG {

    // A NON-tail-recursive function.
    // The function is not tail
    // recursive because the value
    // returned by fact(n-1) is used
    // in fact(n) and call to fact(n-1)
    // is not the last thing done by
    // fact(n)
    static int fact(int n)
    {
        if (n == 0)
            return 1;

        return n * fact(n-1);
    }

    // Driver program to test
    // above function
    public static void Main()
    {
        Console.Write(fact(5));
    }
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A NON-tail-recursive function.
// The function is not tail
// recursive because the value
// returned by fact(n-1) is used in
// fact(n) and call to fact(n-1) is
// not the last thing done by fact(n)

function fact( $n)
{
    if ($n == 0) return 1;

    return $n * fact($n - 1);
}

    // Driver Code
    echo fact(5);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// A NON-tail-recursive function.
// The function is not tail
// recursive because the value
// returned by fact(n-1) is used
// in fact(n) and call to fact(n-1)
// is not the last thing done by
// fact(n)
function fact(n)
{
    if (n == 0)
        return 1;

    return n * fact(n - 1);
}

// Driver code
document.write(fact(5));

// This code is contributed by divyeshrabadiya07

</script>
```

**Output**

```
120
```
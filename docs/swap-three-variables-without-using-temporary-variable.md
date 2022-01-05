# 不使用临时变量交换三个变量

> 原文:[https://www . geesforgeks . org/swap-三变量-不使用-临时变量/](https://www.geeksforgeeks.org/swap-three-variables-without-using-temporary-variable/)

给定三个变量，a，b 和 c，在没有临时变量的情况下交换它们。
**例:**

```
Input  : a = 10, b = 20 and c = 30
Output : a = 30, b = 10 and c = 20
```

**方法 1(使用算术运算符)**
想法是得到两个给定数字之一的和。然后，可以使用求和和从求和中减去来交换数字。
我们已经讨论了交换两个变量[这里](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)。我们可以扩展相同的方法

## C++

```
// C++ program to swap three variables
// without using temporary variable.
#include <iostream>
using namespace std;

// Assign c's value to a, a's value to b and
// b's value to c.
void swapThree(int &a, int &b, int &c)
{
    // Store sum of all in a
    a = a + b + c;  // (a = 60)

    // After this, b has value of a
    b = a - (b+c);  // (b = 60 – (20+30) =10)

    // After this, c has value of b
    c = a - (b+c);  // (c = 60 – (10 + 30) = 20)

    // After this, a has value of c
    a = a - (b+c);   //(a = 60 – (10 + 20) = 30)
}

// Driver code
int main()
{
    int a = 10, b = 20, c = 30;

    cout << "Before swapping a = " << a << ", b = "
         << b << ", c = " << c << endl;

    swapThree(a, b, c);

    cout << "After swapping a = " << a << ", b = "
         << b << ", c = " << c << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to swap three variables
// without using temporary variable.
class GFG
{
    static int a, b, c;

    // Assign c's value to a, a's value
    // to b and b's value to c.
    static void swapThree()
    {

        // Store sum of all in a
        // (a = 60)
        a = a + b + c;

        // After this, b has value of a
        // (b = 60 - (20 + 30) = 10)
        b = a - (b + c);

        // After this, c has value of b
        // (c = 60 - (10 + 30) = 20)
        c = a - (b + c);

        // After this, a has value of c
        // (a = 60 - (10 + 20) = 30)
        a = a - (b + c);
    }

    // Driver Code
    public static void main(String []args)
    {
        a = 10; b = 20; c = 30;
        System.out.println("Before swapping a = " +
                                 a + ", b = " + b +
                                     ", c = " + c);

        // Calling Function
        swapThree();

        System.out.println("After swapping a = " +
                                a + ", b = " + b +
                                    ", c = " + c);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# python 3 program to swap three variables
# without using temporary variable.

# Assign c's value to a, a's value to b and
# b's value to c.
def swapThree(a, b, c):
    # Store sum of all in a
    a = a + b + c # (a = 60)

    # After this, b has value of a
    b = a - (b+c) # (b = 60 – (20+30) =10)

    # After this, c has value of b
    c = a - (b+c) # (c = 60 – (10 + 30) = 20)

    # After this, a has value of c
    a = a - (b+c) #(a = 60 – (10 + 20) = 30)

    print("After swapping a =",a,", b =",b,", c =",c)

# Driver code
if __name__ == '__main__':
    a = 10
    b = 20
    c = 30

    print("Before swapping a =",a,", b =",b,", c =",c)

    swapThree(a, b, c)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to swap three variables
// without using temporary variable.
using System;

class GFG
{

    // Assign c's value to a, a's value
    // to b and b's value to c.
    static void swapThree(ref int a,
                        ref int b,
                        ref int c)
    {
    // Store sum of all in a
    // (a = 60)
        a = a + b + c;

    // After this, b has value of a
    // (b = 60 – (20 + 30) = 10)
        b = a - (b + c);

    // After this, c has value of b
    // (c = 60 – (10 + 30) = 20)
        c = a - (b + c);

    // After this, a has value of c
    // (a = 60 – (10 + 20) = 30)
        a = a - (b + c);
    }

    // Driver Code
    static void Main(String []args)
    {

        int a = 10, b = 20, c = 30;
        Console.WriteLine("Before swapping a = " +
                                a + ", b = " + b +
                                    ", c = " + c);

        // Calling Function
        swapThree(ref a, ref b,ref c);

        Console.Write("After swapping a = " +
                           a + ", b = " + b +
                               ", c = " + c);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to swap three
// variables without using
// temporary variable.

// Assign c's value to a,
// a's value to b and
// b's value to c.
function swapThree(&$a, &$b, &$c)
{
    // Store sum of all in a
    $a = $a + $b + $c; // (a = 60)

    // After this, b has value of a
    // (b = 60 – (20+30) =10)
    $b = $a - ($b + $c);

    // After this, c has value of b
    // (c = 60 – (10 + 30) = 20)
    $c = $a - ($b + $c);

    // After this, a has value of c
    //(a = 60 – (10 + 20) = 30)
    $a = $a - ($b + $c);
}

// Driver Code
$a = 10; $b = 20; $c = 30;

echo "Before swapping a = " , $a ,
         ", b = ", $b , ", c = " ,
                         $c ,"\n";

swapThree($a, $b, $c);

echo "After swapping a = ",$a ,
                 ", b = ", $b ,
           ", c = ", $c , "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript program to swap three variables
// without using temporary variable.

let a, b, c;

// Assign c's value to a, a's value
// to b and b's value to c.
function swapThree()
{

    // Store sum of all in a
    // (a = 60)
    a = a + b + c;

    // After this, b has value of a
    // (b = 60 - (20 + 30) = 10)
    b = a - (b + c);

    // After this, c has value of b
    // (c = 60 - (10 + 30) = 20)
    c = a - (b + c);

    // After this, a has value of c
    // (a = 60 - (10 + 20) = 30)
    a = a - (b + c);
}

// Driver Code
a = 10; b = 20; c = 30;
document.write("Before swapping a = " +
                         a + ", b = " + b +
                             ", c = " + c);

// Calling Function
swapThree();

document.write("<br>After swapping a = " +
                        a + ", b = " + b +
                            ", c = " + c);

// This code contributed by Princi Singh
</script>
```

**输出:**

```
Before swapping a = 10, b = 20, c = 30
After swapping a = 30, b = 10, c = 20
```

时间复杂度:0(1)

辅助空间:0(1)

感谢**马扎尔·MIK**提出这个方法。
**方法 2(使用按位异或)**
按位异或运算符可用于交换三个变量。这个想法类似于方法 1。我们首先将所有数字的异或存储在“a”中。然后我们通过对这两个数字进行异或运算得到单个数字。

## C++

```
// C++ program to swap three variables
// without using temporary variable
#include <iostream>
using namespace std;

// Assign c's value to a, a's value to b and
// b's value to c.
void swapThree(int &a, int &b, int &c)
{
    // Store XOR of all in a
    a = a ^ b ^ c;

    // After this, b has value of a
    b = a ^ b ^ c;

    // After this, c has value of b
    c = a ^ b ^ c;

    // After this, a has value of c
    a = a ^ b ^ c;
}

// Driver code
int main()
{
    int a = 10, b = 20, c = 30;

    cout << "Before swapping a = " << a << ", b = "
         << b << ", c = " << c << endl;

    swapThree(a, b, c);

    cout << "After swapping a = " << a << ", b = "
         << b << ", c = " << c << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to swap three variables
// without using temporary variable.
class GFG
{
    static int a, b, c;

    // Assign c's value to a, a's value
    // to b and b's value to c.
    static void swapThree()
    {
        // Store XOR of all in a
        a = a ^ b ^ c;

        // After this, b has value of a
        b = a ^ b ^ c;

        // After this, c has value of b
        c = a ^ b ^ c;

        // After this, a has value of c
        a = a ^ b ^ c;
    }

    // Driver Code
    public static void main(String[] args)
    {
        a = 10;
        b = 20;
        c = 30;
        System.out.println("Before swapping a = " + a +
                           ", b = " + b + ",c = " + c);

        // Calling Function
        swapThree();
        System.out.println("After swapping a = " + a +
                           ", b = " + b + ", c = " + c);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to swap three variables
# without using temporary variable

# Assign c's value to a, a's value to b and
# b's value to c.
def swapThree(a, b, c) :

    # Store XOR of all in a
    a[0] = a[0] ^ b[0] ^ c[0]

    # After this, b has value of a[0]
    b[0] = a[0] ^ b[0] ^ c[0]

    # After this, c has value of b
    c[0] = a[0] ^ b[0] ^ c[0]

    # After this, a[0] has value of c
    a[0] = a[0] ^ b[0] ^ c[0]

# Driver code
a, b, c = [10], [20], [30]

print("Before swapping a = ", a[0],
    ", b = ", b[0], ", c = ", c[0])

swapThree(a, b, c)

print("After swapping a = ", a[0],
   ", b = ", b[0], ", c = ", c[0])

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to swap three variables
// without using temporary variable.
using System;

class GFG
{

    // Assign c's value to a, a's value
    // to b and b's value to c.
    static void swapThree(ref int a,
                          ref int b,
                          ref int c)
    {
    // Store XOR of all in a
        a = a ^ b ^ c;

    // After this, b has value of a
        b = a ^ b ^ c;

    // After this, c has value of b
        c = a ^ b ^ c;

    // After this, a has value of c
        a = a ^ b ^ c;
    }

    // Driver Code
    static void Main(String []args)
    {

    int a = 10, b = 20, c = 30;
        Console.WriteLine( "Before swapping a = " +
                            a +", b = " + b +
                               ",c = " + c);

        // Calling Function
        swapThree(ref a, ref b,ref c);

        Console.Write("After swapping a = " +
                       a +", b = " + b +
                       ", c = " + c);

    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to swap three variables
// without using temporary variable

// Assign c's value to a, a's value to b and
// b's value to c.

function swapThree(&$a, &$b, &$c)
{
    // Store XOR of all in a
    $a = $a ^ $b ^ $c;

    // After this, b has value of a
    $b = $a ^ $b ^ $c;

    // After this, c has value of b
    $c = $a ^ $b ^ $c;

    // After this, a has value of c
    $a = $a ^ $b ^ $c;
}

// Driver code

    $a = 10; $b = 20; $c = 30;

    echo  "Before swapping a = " , $a , ", b = ",
         $b , ", c = " , $c ,"\n";

    swapThree($a, $b, $c);

    echo "After swapping a = ", $a , ", b = ",
         $b , ", c = " , $c ,"\n";

#This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// javascript program to swap three variables
// without using temporary variable.

var a, b, c;

// Assign c's value to a, a's value
// to b and b's value to c.
function swapThree()
{
    // Store XOR of all in a
    a = a ^ b ^ c;

    // After this, b has value of a
    b = a ^ b ^ c;

    // After this, c has value of b
    c = a ^ b ^ c;

    // After this, a has value of c
    a = a ^ b ^ c;
}

// Driver Code
a = 10;
b = 20;
c = 30;
document.write("Before swapping a = " + a +
                   ", b = " + b + ", c = " + c);

// Calling Function
swapThree();
document.write("<br>")
document.write("After swapping a = " + a +
                   ", b = " + b + ", c = " + c);

// This code contributed by Princi Singh

</script>
```

**输出:**

```
Before swapping a = 10, b = 20, c = 30
After swapping a = 30, b = 10, c = 20
```

时间复杂度:0(1)

辅助空间:0(1)

方法 1 会导致 a、b 和 c 的大值溢出，而方法 2 不会。
本文由**舒巴姆**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
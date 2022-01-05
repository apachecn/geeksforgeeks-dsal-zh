# 使用三次乘法运算的复数乘积

> 原文:[https://www . geeksforgeeks . org/复数乘积使用三乘法运算/](https://www.geeksforgeeks.org/product-of-complex-numbers-using-three-multiplication-operation/)

给定四个整数 **a、b、c 和 d** ，它们表示形式为 **(a + bi)** 和 **(c + di)** 的两个复数，任务是仅使用三次乘法运算来找到给定复数的[乘积。
**示例:**](https://www.geeksforgeeks.org/multiplication-two-complex-numbers-given-strings/)

> **输入:** a = 2，b = 3，c = 4，d = 5
> **输出:** -7 + 22i
> **说明:**
> 产品给出为:
> (2+3i)*(4+5i)= 2 * 4+4 * 3i+2 * 5i+3 * 5 *(1)
> = 8–15+(12+10)I
> =-7+22i【T10

**天真方法:**天真方法是将给定的两个复数直接相乘，如下所示:

> = >(a+bi)*(c+di)
> =>a(c+di)+b * I(c+di)
> =>a * c+ad * I+b * c * I+b * d * I * I
> =>(a * c–b * d)+(a * d+b * c)* I

上述运算需要四次乘法才能求出两个复数的乘积。
**高效方法:**上述方法需要四次乘法才能找到乘积。可以简化为三次乘法如下:
两个复数的乘法如下:

> (a+bi)*(c+di)= a * c–b * d+(a * d+b * c)I

简化实数部分:

> 实部= a * c–b * d
> 让 prod1 = a*c，prod 2 = b * d
> 因此，**实部= prod 1–prod 2**

将虚部简化如下:

> 虚数部分= a*d + b*c
> 在上面的想象部分中加减 a*c 和 b*d 我们有，
> 虚数部分= a * c–a * c+a * d+b * c+b * d–b * d，
> 关于重新排列我们得到的项，
> =>a * b+ b * c+a * d+b * d–a * c–b * d
> =>(a+b)* c+(a+b)* d–a * c–b * d
> =>(a+b)*(c+d)–a * c–b * d
> 让 prod3 = (a + b)*(c + d)
> 然后虚部由**prod 3 –( prod 1+prod)给出**

因此，我们需要找到 **prod1 = a * c** 、 **prod2 = b * d** 、 **prod3 = ( a + b ) * ( c + d )** 的值。
那么，我们的最终答案将是:

> 实部= prod 1–prod 2
> 虚部= prod 3 –( prod 1+prod 2)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to multiply Complex
// Numbers with just three
// multiplications
void print_product(int a, int b,
                   int c, int d)
{
    // Find value of prod1, prod2 and prod3
    int prod1 = a * c;
    int prod2 = b * d;
    int prod3 = (a + b) * (c + d);

    // Real Part
    int real = prod1 - prod2;

    // Imaginary Part
    int imag = prod3 - (prod1 + prod2);

    // Print the result
    cout << real << " + " << imag << "i";
}

// Driver Code
int main()
{
    int a, b, c, d;

    // Given four Numbers
    a = 2;
    b = 3;
    c = 4;
    d = 5;

    // Function Call
    print_product(a, b, c, d);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to multiply Complex
// Numbers with just three
// multiplications
static void print_product(int a, int b,
                          int c, int d)
{

    // Find value of prod1, prod2 and prod3
    int prod1 = a * c;
    int prod2 = b * d;
    int prod3 = (a + b) * (c + d);

    // Real Part
    int real = prod1 - prod2;

    // Imaginary Part
    int imag = prod3 - (prod1 + prod2);

    // Print the result
    System.out.println(real + " + " +
                       imag + "i");
}

// Driver Code
public static void main(String[] args)
{

    // Given four numbers
    int a = 2;
    int b = 3;
    int c = 4;
    int d = 5;

    // Function call
    print_product(a, b, c, d);
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to multiply Complex
# Numbers with just three
# multiplications
def print_product(a, b, c, d):

    # Find value of prod1, prod2
    # and prod3
    prod1 = a * c
    prod2 = b * d
    prod3 = (a + b) * (c + d)

    # Real part
    real = prod1 - prod2

    # Imaginary part
    imag = prod3 - (prod1 + prod2)

    # Print the result
    print(real, " + ", imag, "i")

# Driver code

# Given four numbers
a = 2
b = 3
c = 4
d = 5

# Function call
print_product(a, b, c, d)

# This code is contributed by Vishal Maurya.
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to multiply Complex
// Numbers with just three
// multiplications
static void print_product(int a, int b,
                          int c, int d)
{
    // Find value of prod1, prod2 and prod3
    int prod1 = a * c;
    int prod2 = b * d;
    int prod3 = (a + b) * (c + d);

    // Real Part
    int real = prod1 - prod2;

    // Imaginary Part
    int imag = prod3 - (prod1 + prod2);

    // Print the result
    Console.Write(real + " + " + imag + "i");
}

// Driver Code
public static void Main()
{
    int a, b, c, d;

    // Given four Numbers
    a = 2;
    b = 3;
    c = 4;
    d = 5;

    // Function Call
    print_product(a, b, c, d);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to multiply Complex
// Numbers with just three
// multiplications
function print_product( a, b, c, d)
{
    // Find value of prod1, prod2 and prod3
    let prod1 = a * c;
    let prod2 = b * d;
    let prod3 = (a + b) * (c + d);

    // Real Part
    let real = prod1 - prod2;

    // Imaginary Part
    let imag = prod3 - (prod1 + prod2);

    // Print the result
    document.write(real + " + " + imag + "i");
}

// Driver Code

let a, b, c, d;

// Given four Numbers
a = 2;
b = 3;
c = 4;
d = 5;

// Function Call
print_product(a, b, c, d);

</script>
```

**Output:** 

```
-7 + 22i
```

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*
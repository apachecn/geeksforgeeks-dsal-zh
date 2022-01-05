# C/c++中两个数相加的 8 种不同方式

> 原文:[https://www . geesforgeks . org/7-不同的添加方式-两个数字-in-c-c/](https://www.geeksforgeeks.org/7-different-ways-to-add-two-numbers-in-c-c/)

给定两个数 **A** 和 **B** ，任务是求给定两个数的和。
**例:**

> **输入:** A = 5，B = 6
> **输出:**和= 11
> **输入:** A = 4，B = 11
> **输出:**和= 15

**方法 1–使用加法运算符:**这里只需在两个数字之间使用加法运算符，并打印数字的总和。

> 总和=甲+乙

下面是上述方法的实现:

## C++

```
// C++ program to add two number
// using addition operator
#include <iostream>
using namespace std;
// Function to return sum
// of two number
int addTwoNumber(int A, int B)
{
    // Return sum of A and B
    return A + B;
}

// Driver Code
int main()
{
    // Given two number
    int A = 4, B = 11;

    // Function call
    cout << "sum = " << addTwoNumber(A, B);
    return 0;
}
```

**Output**

```
sum = 15
```

**方法 2–使用**减法**运算符:**这里只需在两个数字之间使用减法运算符，两次，使减-减相乘并产生+运算符，并返回数字的总和。

> 总和= A –(-B)

以下是上述方法的实现:

## C++

```
// C++ program to add two number
// using subtraction operator
#include <iostream>
using namespace std;
// Function to return sum
// of two number
int addTwoNumber(int A, int B)
{
    // Return sum of A and B
    return A - (-B);
}

// Driver Code
int main()
{
    // Given two number
    int A = 4, B = 11;

    // Function call
    cout << "sum = " << addTwoNumber(A, B);
    return 0;
}
```

**Output**

```
sum = 15
```

**方法 3–使用** [**递增/递减运算符**](https://www.geeksforgeeks.org/difference-between-increment-and-decrement-operators/) **:** 这里使用递增/递减运算符，当一个数递减到零，而在另一个数递增 1 时，当第一个数递减 1 时，返回第二个数。

> 而(B > 0){
> a++；
> B–；

下面是上述方法的实现:

## C++

```
// C++ program to add two number using
// increment/decrement operator
#include <iostream>
using namespace std;

// Function to return sum
// of two number
int addTwoNumber(int A, int B)
{
    // When A is positive
    while (A > 0) {
        A--;
        B++;
    }

    // When A is negative
    while (A < 0) {
        A++;
        B--;
    }

    // Return sum of A and B
    return B;
}

// Driver Code
int main()
{
    // Given two number
    int A = 4, B = 11;

    // Function call
    cout << "sum = " << addTwoNumber(A, B);
    return 0;
}
```

**Output**

```
sum = 15
```

**方法 4–使用** [**printf()**](https://www.geeksforgeeks.org/return-values-of-printf-and-scanf-in-c-cpp/) **方法:**这里**“% * s”**说明符打印一个变量的值，变量的值的次数，以及 printf 返回多少字符打印在屏幕上。

> printf("%*s%*s "，A，""，B，" ")；

下面是上述方法的实现:

## C++

```
// C++ program to add two number
// using printf method
#include <iostream>
using namespace std;
// Function to return sum
// of two number
int addTwoNumber(int A, int B)
{
    // Return sum of A and B
    return printf("%*s%*s", A, "", B, "");
}

// Driver Code
int main()
{
    // Given two number
    int A = 4, B = 11;

    // Function call
    printf("sum = %d", addTwoNumber(A, B));
    return 0;
}
```

**Output**

```
               sum = 15
```

**方法 5–使用** [**半加法器方法**](https://www.geeksforgeeks.org/half-adder-in-digital-logic/) **:** 通过执行两个位的[位 xor(^(T9)可以获得两个位的和。进位位可以通过对两位执行**位“与”(& )** 来获得。
以上是简单的半加法器逻辑，可以用来加 2 个单比特。我们可以把这个逻辑推广到整数。如果 x 和 y 在相同的位置没有设置位，那么 x 和 y 的按位异或(^)给出 x 和 y 的和。为了合并公共设置位，使用按位与(&)。x 和 y 的按位“与”给出所有进位。我们计算(x & y) < < 1，并将其与 x ^ y 相加，得到所需的结果。](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)

> 总和= A&B；
> 进位= x ^ y

下面是上述方法的实现:

## C++

```
// C++ program to add two number
// using half adder method
#include <iostream>
using namespace std;

// Function to return sum
// of two number
int addTwoNumber(int A, int B)
{

    // Iterate till there is no carry
    while (B != 0) {

        // Carry now contains common
        // set bits of A and B
        int carry = A & B;

        // Sum of bits of A and B
        // where at least one of the
        // bits is not set
        A = A ^ B;

        // Carry is shifted by one so
        // that adding it to A gives
        // the required sum
        B = carry << 1;
    }

    return A;
}

// Driver Code
int main()
{
    // Given two number
    int A = 4, B = 11;

    // Function call
    printf("sum = %d", addTwoNumber(A, B));
    return 0;
}
```

**Output**

```
sum = 15
```
# C/c++中的左移和右移运算符

> 原文:[https://www . geesforgeks . org/left-shift-right-shift-operators-c-CPP/](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)

**左移:**

**表示为:< <**

**例:N<T3】I(N:第一个操作数，I:第二个操作数)**

取两个数字，左移第一个操作数的位，第二个操作数决定要移位的位数。或者换句话说，将整数“ **x** ”左移一个整数“ **y** ”表示为“**(x<<y)’**相当于将 **x** 乘以 **2^y** (2 升至 y 次方)。

**例:**取**N = 22**；也就是二进制形式的 **00010110** 。

现在，如果“ *N 左移 2* ，即 **N=N < < 2** ，那么 **N** 将变成 **N=N*(2^2)** 。因此， **N=22*(2^2)=88** 可以被称为 **01011000。**

## C

```
/* C++ Program to demonstrate use of left shift 
   operator */
#include<stdio.h>
int main()
{
    // a = 5(00000101), b = 9(00001001)
    unsigned char a = 5, b = 9; 

    // The result is 00001010 
    printf("a<<1 = %d\n", a<<1);

    // The result is 00010010 
    printf("b<<1 = %d\n", b<<1);  
    return 0;
}
```

## C++

```
/* C++ Program to demonstrate use of left shift 
   operator */
#include <iostream>
using namespace std;

int main()
{
    // a = 5(00000101), b = 9(00001001)
    unsigned char a = 5, b = 9; 

    // The result is 00001010 
    cout <<"a<<1 = "<< (a<<1) << endl;

    // The result is 00010010 
    cout <<"b<<1 = "<< (b<<1) << endl;  
    return 0;
}

// This code is contributed by shivanisinghss2110
```

**Output**

```
a<<1 = 10
b<<1 = 18
```

**右移:**

**表示为:> >**

**例:N>T3】I(N:第一个操作数，I:第二个操作数)**

取两个数字，右移第一个操作数的位，第二个操作数决定移位的位数。换句话说，将整数“ **x** ”右移一个整数“ **y** ”表示为“ **(x > > y)** ”相当于用 2^y.除 x

**例:**取**N = 32**；也就是二进制形式的 **100000** 。

现在，如果“ *N 右移 2*”**，即 N=N > > 2** ，那么 **N** 将变成 **N=N/(2^2)** 。因此， **N=32/(2^2)=8** 可以写成 **1000** 。

## C++

```
/* C++ Program to demonstrate use of right
   shift operator */
#include <iostream>
using namespace std;

int main()
{
    // a = 5(00000101), b = 9(00001001)
    unsigned char a = 5, b = 9;

    // The result is 00000010

    cout <<"a>>1 = "<< (a >> 1)<< endl;

    // The result is 00000100
    cout <<"b>>1 = "<< (b >> 1) << endl;
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
/* C++ Program to demonstrate use of right
   shift operator */
#include <stdio.h>

using namespace std;
int main()
{
    // a = 5(00000101), b = 9(00001001)
    unsigned char a = 5, b = 9;

    // The result is 00000010

    printf("a>>1 = %d\n", a >> 1);

    // The result is 00000100
    printf("b>>1 = %d\n", b >> 1);
    return 0;
}
```

**Output**

```
a>>1 = 2
b>>1 = 4
```

**要点:**

*   左移位和右移位运算符不应用于负数。如果任何操作数是负数，的结果是未定义的行为。例如 1 >> -1 和 1 << -1 的结果都是未定义的。
*   如果数字的移动超过整数的大小，则行为是未定义的。例如，1 << 33 is undefined if integers are stored using 32 bits. For bit shift of larger values 1ULL<<62   **ULL** 用于无符号长 Long，它使用 64 位定义，可以存储大值。
*   左移 1 和右移 1 分别相当于第一项和 2 的乘积与给定元素的幂(1<<3 = 1*pow(2,3)) and division of first term and second term raised to power 2 (1>> 3 = 1/幂(2，3))。
    如第 1 点所述，只有数字为正时，它才起作用。

## C++

```
#include <iostream>
using namespace std;

int main()
{
    int x = 19;
    unsigned long long y = 19;
    cout <<"x << 1 = " << (x << 1) << endl;
    cout <<"x >> 1 = " << (x >> 1) << endl;
    // shift y by 61 bits left
    cout <<"y << 61 = " << (y << 61) << endl;
    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
#include <stdio.h>
int main()
{
    int x = 19;
    unsigned long long y = 19;
    printf("x << 1 = %d\n", x << 1);
    printf("x >> 1 = %d\n", x >> 1);
    // shift y by 61 bits left
    printf("y << 61 = %lld\n", y << 61);
    return 0;
}
```

**Output**

```
x << 1 = 38
x >> 1 = 9
y << 61 = 6917529027641081856
```

*   1 的左移 I 相当于 2 的幂 I。
    如第 1 点所述，它只在数字为正时起作用。

## C++

```
#include <iostream>
using namespace std;

int main()
{ 
   int i = 3;  
   cout <<"pow(2, "<< i << ") = " << (1 << i) << endl;
   i = 4;  
   cout <<"pow(2, "<< i << ") = " << (1 << i) << endl;
   return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
#include<stdio.h>
int main()
{ 
   int i = 3;  
   printf("pow(2, %d) = %d\n", i, 1 << i);
   i = 4;  
   printf("pow(2, %d) = %d\n", i, 1 << i);
   return 0;
}
```

**Output**

```
pow(2, 3) = 8
pow(2, 4) = 16
```

[关于 C 中按位运算符的有趣事实](https://www.geeksforgeeks.org/interesting-facts-bitwise-operators-c/)
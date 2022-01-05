# <complex.h>C 中头文件带示例</complex.h>

> 原文:[https://www . geesforgeks . org/complex-h-header-file-in-c-with-examples/](https://www.geeksforgeeks.org/complex-h-header-file-in-c-with-examples/)

大部分 C 程序都是使用 **complex.h** 头文件来处理[复数](https://www.geeksforgeeks.org/complex-numbers-c-set-1/)运算和操作。这个头文件是在 **C99 标准**中添加的。

C++标准库有一个表头，实现复数作为模板类，**[<【T】>](https://www.geeksforgeeks.org/complex-numbers-c-set-1/)**，不同于 c 中的 **< complex.h >**

**<u>宏与< complex.h ></u>**
相关联 **< complex.h >** 的一些宏如下所示。左侧的值描述了 complex.h 中的宏，右侧描述了 C99 标准中添加了关键字(_ 虚数，_Complex)的宏的扩展。

| 宏名字 | 延伸至 |
| --- | --- |
| 复杂的 | _ 复杂 |
| 虚构的 | _ 虚数 |
| _ 复杂 _ 一 | (常量浮点 _ 复杂)I |
| _ 虚数 _I | (常量浮点 _ 虚数)I |
| 我 | _ 虚数 _I(_ 复数 _I 如果 _ 虚数 _ I 不存在) |

下面的程序有助于创建复数。

**例 1:**

```
// C program to show the working
// of complex.h library

#include <complex.h>
#include <stdio.h>

int main(void)
{
    double real = 1.3,
           imag = 4.9;
    double complex z
        = CMPLX(real, imag);
    printf(
        "z = %.1f% + .1fi\n",
        creal(z), cimag(z));
}
```

**Output:**

```
z = 1.3+4.9i

```

**说明:**

*   **cmplx()** 函数以实部和虚部为参数创建复数对象。这个函数返回复数的对象。
*   **creal()** 函数返回复数的实部
*   **cimag()** 函数返回复数的虚部
*   如果我们的实部和虚部是 float 类型，我们使用 **cmplxf()** 函数来生成复数，为了得到实部和虚部，我们使用 **crealf()** 、 **cimagf()** 函数。
*   如果我们的实部和虚部是长双精度类型，我们使用 **cmplxl()** 函数来生成复数，为了得到实部和虚部，我们使用 **creall()** 、 **cimagl()** 函数。

**示例 2:** 我们也可以使用宏 **I** 创建复数对象。

```
// C program to create a complex
// number using macro I

#include <complex.h>
#include <stdio.h>

int main(void)
{
    double complex
        z
        = 3.2 + 4.1 * I;

    // Creates complex number
    // with 3.2 and 4.1 as
    // real and imaginary parts
    printf(
        "z = %.1f% + .1fi\n",
        creal(z), cimag(z));
}
```

**Output:**

```
z = 3.2+4.1i

```

**<u>与< complex.h ></u>**
关联的函数 **< complex.h >** 头文件还提供了一些内置函数来处理复数。这里的“arg”代表复数对象。

| 功能 | 描述 |
| --- | --- |
| float cabsf(float complex arg)
双 cabs(双 complex arg)
长双 cabsl(长双 complex arg) | 它返回复杂参数的绝对值 |
| float complex cacos SF(float complex arg)
双复合 CaCO(双复合 arg)
长双复合 cacosl(长双复合 arg) | 它返回复变元的复弧余弦值 |
| float complex cacoshf(float complex arg)
双复合 cacosh(双复合 arg)
长双复合 cacoshl(长双复合 arg) | 它返回复变元的复弧双曲余弦值 |
| 浮动货物(浮动复合 arg)
双货物(双复合 arg)
长双货物(长双复合 arg) | 它返回复变元的相位角(以弧度为单位)。 |
| float complex casinf(float complex arg)
双复形 casin(双复形 arg)
长双复形 casinl(长双复形 arg) | 它返回复变元的复反正弦值 |
| float complex casinf(float complex arg)
双复形 casin(双复形 arg)
长双复形 casinl(长双复形 arg) | 它返回复变元的复弧双曲正弦值 |
| 浮动复合物 catanf(浮动复合物 arg)
双复合物 catan(双复合物 arg)
长双复合物 catanl(长双复合物 arg) | 它返回复变元的复反正切值 |
| float complex catanhf(float complex arg)
双复形 catan(双复形 arg)
长双复形 catanl(长双复形 arg) | 它返回复变元的复弧双曲正切值 |
| float complex ccosf(float complex arg)
双复形 ccos(双复形 arg)
长双复形 ccosl(长双复形 arg) | 它返回复变元的复余弦值 |
| float complex cexpf(float complex arg)
双复形 cexp(双复形 arg)
长双复形 cexpl(长双复形 arg) | 它返回复数值 e <sup>arg</sup> ，其中 e 是自然对数基数 |
| float crealf(float complex arg)
double creal(double complex arg)
long double creall(long double complex arg) | 它返回复杂参数的真实部分 |
| float cimagf(float complex arg)
double cimag(double complex arg)
long double cimagl(long double complex arg) | 它返回复变元的虚部 |
| float complex clogf(float complex arg)
double complex clog(double complex arg)
long double complex cimagl(long double complex arg) | 它返回复变元的虚部 |
| float complex conjf(float complex arg)
双复数 conj(双复数 arg)
长双复数 conjl(长双复数 arg) | 它返回复变元的共轭 |
| float complex CP owf(float complex a，long double complex b) | 它返回 a <sup>b</sup> 的复数值 |
| 浮动复合物 csqrtf(浮动复合物 arg)
双复合物 csqrt(双复合物 arg)
长双复合物 csqrtl(长双复合物 arg) | 它返回参数的复数平方根 |

**例 3:** 求复数共轭的程序。

```
#include <complex.h>
#include <stdio.h>

int main(void)
{
    double real = 1.3,
           imag = 4.9;
    double complex z
        = CMPLX(real, imag);
    double complex
        conj_f
        = conjf(z);
    printf("z = %.1f% + .1fi\n",
           creal(conj_f),
           cimag(conj_f));
}
```

**Output:**

```
z = 1.3-4.9i

```

**例 4:** 求复数绝对值的程序。

```
#include <complex.h>
#include <stdio.h>

int main(void)
{
    double real = 1.3,
           imag = 4.9;
    double complex z
        = CMPLX(real, imag);
    printf("Absolute value = %.1f",
           cabsf(z));
}
```

**Output:**

```
Absolute value = 5.1

```

**例 4:** 求复数相角的程序。

```
#include <complex.h>
#include <stdio.h>

int main(void)
{
    double real = 1.3,
           imag = 4.9;
    double complex z
        = CMPLX(real, imag);
    printf(
        "Phase Angle = %.1f radians\n",
        cargf(z));
}
```

**Output:**

```
Phase Angle = 1.3 radians

```
# C/c++中的模运算符(%)，示例

> 原文:[https://www . geeksforgeeks . org/模-运算符-in-c-cpp-with-examples/](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/)

由 **%** 表示的**模运算符**是一个[算术运算符](https://www.geeksforgeeks.org/operators-in-c-set-1-arithmetic-operators/)。
[模除法](https://www.geeksforgeeks.org/modular-division/)运算符产生整数除法的**余数**。

**语法:**如果 x 和 y 是整数，那么表达式:

```
x % y
```

当 x 除以 y 时产生余数。

**返回值:**

*   如果 y 完全除 x，表达式的结果是 0。
*   如果 x 不能被 y 完全整除，那么结果将是[1，x-1]范围内的余数。
*   如果 x 为 0，那么[除以零](https://www.geeksforgeeks.org/handling-the-divide-by-zero-exception-in-c/)就是一个[编译时错误](https://www.geeksforgeeks.org/difference-between-compile-time-errors-and-runtime-errors/)。

**例如:**考虑以下代码:

## C++

```
// Program to illustrate the
// working of modulo operator
#include <iostream>
using namespace std;

int main(void)
{

    // To store two integer values
    int x, y;

    // To store the result of
    // the modulo expression
    int result;

    x = 3;
    y = 4;
    result = x % y;
    cout << result << endl;

    result = y % x;
    cout << result << endl;

    x = 4;
    y = 2;
    result = x % y;
    cout<<result;

    return 0;
}

// This code is contributed by Mayank Tyagi
```

## C

```
// Program to illustrate the
// working of modulo operator

#include <stdio.h>

int main(void)
{

    // To store two integer values
    int x, y;

    // To store the result of
    // the modulo expression
    int result;

    x = 3;
    y = 4;
    result = x % y;
    printf("%d", result);

    result = y % x;
    printf("\n%d", result);

    x = 4;
    y = 2;
    result = x % y;
    printf("\n%d", result);

    return 0;
}
```

**Output**

```
3
1
0
```

**模运算符的限制:**
模运算符有相当多的限制。

1.  %运算符不能应用于[浮点数](https://www.geeksforgeeks.org/introduction-of-floating-point-representation/)，即浮点数或双精度浮点数。如果试图对浮点常量或变量使用模运算符，编译器将产生一个错误:

## C++

```
// Program to illustrate the
// working of modulo operator
#include <iostream>
using namespace std;

int main()
{

    // To store two integer values
    float x, y;

    // To store the result of
    // the modulo expression
    float result;

    x = 2.3;
    y = 1.5;
    result = x % y;
    cout << result;

    return 0;
}

// This code is contributed by Harshit Srivastava
```

## C

```
// Program to illustrate the
// working of modulo operator

#include <stdio.h>

int main(void)
{

    // To store two integer values
    float x, y;

    // To store the result of
    // the modulo expression
    float result;

    x = 2.3;
    y = 1.5;
    result = x % y;
    printf("%f", result);

    return 0;
}
```

**编译错误:**

```
Compilation Error in C code :- prog.c: In function 'main':
prog.c:19:16: error:
 invalid operands to binary % (have 'float' and 'float')
     result = x % y;
                ^           
```

对于负操作数，模运算符结果的符号依赖于机器，因为操作是下溢或上溢的结果。

## C++

```
// Program to illustrate the
// working of the modulo operator
#include <iostream>
using namespace std;

int main(void)
{

    // To store two integer values
    int x, y;

    // To store the result of
    // the modulo expression
    int result;

    x = -3;
    y = 4;
    result = x % y;
    cout << result << endl;

    x = 4;
    y = -2;
    result = x % y;
    cout << result << endl;

    x = -3;
    y = -4;
    result = x % y;
    cout << result;

    return 0;
}

// This code is contributed by Harshit Srivastava
```

## C

```
// Program to illustrate the
// working of the modulo operator

#include <stdio.h>

int main(void)
{

    // To store two integer values
    int x, y;

    // To store the result of
    // the modulo expression
    int result;

    x = -3;
    y = 4;
    result = x % y;
    printf("%d", result);

    x = 4;
    y = -2;
    result = x % y;
    printf("\n%d", result);

    x = -3;
    y = -4;
    result = x % y;
    printf("\n%d", result);

    return 0;
}
```

**Output**

```
-3
0
-3
```

**注意:**有些编译器可能会将表达式的结果显示为 1，有些可能会显示-1。这取决于[编译器](https://www.geeksforgeeks.org/introduction-of-compiler-design/)。
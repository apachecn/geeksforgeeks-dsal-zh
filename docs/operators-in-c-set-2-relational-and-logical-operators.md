# C |集合 2 中的运算符(关系和逻辑运算符)

> 原文:[https://www . geesforgeks . org/operators-in-c-set-2-relational-and-logic-operators/](https://www.geeksforgeeks.org/operators-in-c-set-2-relational-and-logical-operators/)

我们已经讨论了[**【C 中的运算符简介】**](https://www.geeksforgeeks.org/operators-c-c/) ，在这里我们对什么类型的运算符、C 和 C++支持以及它的基本实现有了一个总体的概念。接下来，我们学习了 [**算术运算符**](https://www.geeksforgeeks.org/operators-in-c-set-1-arithmetic-operators/) ，在这里我们详细了解了 C 和 C++中算术运算符的类型和用法。在本文中，让我们尝试理解**关系运算符和逻辑运算符**的类型和用途。

![](img/d26209f0baa51da031433d6ba6e9ac33.png)

**关系运算符**
关系运算符用于比较两个值，以了解一对数字份额的关系类型。例如，小于、大于、等于等。让我们一个一个来看

1.  **等于运算符:**表示为 **'=='** ，等于运算符检查两个给定的操作数是否相等。如果是，它返回真。否则返回假。例如， **5==5** 将返回真。
2.  **不等于运算符:**表示为**’！='** ，不等于运算符检查两个给定的操作数是否相等。如果不是，它返回真。否则返回假。它是**= =“**运算符的精确布尔补码。比如 **5！=5** 将返回 false。
3.  **大于运算符:**表示为 **' > '** ，大于运算符检查第一个操作数是否大于第二个操作数。如果是，它返回真。否则返回假。比如 **6 > 5** 会回真。
4.  小于运算符:表示为 **' < '** ，小于运算符检查第一个操作数是否小于第二个操作数。如果是，它返回真。否则返回假。比如 **6 < 5** 会回假。
5.  **大于或等于运算符:**表示为 **' > ='** ，大于或等于运算符检查第一个操作数是否大于或等于第二个操作数。如果是，它返回真，否则返回假。例如 **5 > =5** 将返回真。
6.  **小于或等于运算符:表示为“<=“**”，小于或等于运算符检查第一个操作数是否小于或等于第二个操作数。如果是，则返回 true，否则返回 false。比如 **5 < =5** 也会回真。

**例:**

## C

```
// C program to demonstrate working of relational operators
#include <stdio.h>

int main()
{
    int a = 10, b = 4;

    // greater than example
    if (a > b)
        printf("a is greater than b\n");
    else
        printf("a is less than or equal to b\n");

    // greater than equal to
    if (a >= b)
        printf("a is greater than or equal to b\n");
    else
        printf("a is lesser than b\n");

    // less than example
    if (a < b)
        printf("a is less than b\n");
    else
        printf("a is greater than or equal to b\n");

    // lesser than equal to
    if (a <= b)
        printf("a is lesser than or equal to b\n");
    else
        printf("a is greater than b\n");

    // equal to
    if (a == b)
        printf("a is equal to b\n");
    else
        printf("a and b are not equal\n");

    // not equal to
    if (a != b)
        printf("a is not equal to b\n");
    else
        printf("a is equal b\n");

    return 0;
}
```

## C++

```
// C++ program to demonstrate working of logical operators
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 4;

    // greater than example
    if (a > b)
        cout << "a is greater than b\n";
    else
        cout << "a is less than or equal to b\n";

    // greater than equal to
    if (a >= b)
        cout << "a is greater than or equal to b\n";
    else
        cout << "a is lesser than b\n";

    // less than example
    if (a < b)
        cout << "a is less than b\n";
    else
        cout << "a is greater than or equal to b\n";

    // lesser than equal to
    if (a <= b)
        cout << "a is lesser than or equal to b\n";
    else
        cout << "a is greater than b\n";

    // equal to
    if (a == b)
        cout << "a is equal to b\n";
    else
        cout << "a and b are not equal\n";

    // not equal to
    if (a != b)
        cout << "a is not equal to b\n";
    else
        cout << "a is equal b\n";

    return 0;
}
```

**Output:** 

```
a is greater than b
a is greater than or equal to b
a is greater than or equal to b
a is greater than b
a and b are not equal
a is not equal to b
```

**逻辑运算符:**
它们用于组合两个或多个条件/约束，或者补充正在考虑的原始条件的评估。它们描述如下:

1.  **逻辑与运算符:****'&&'**运算符在考虑的两个条件都满足时返回真。否则返回假。例如， **a & & b** 在 a 和 b 都为真(即非零)时返回真。
2.  **逻辑或运算符:****' | | '**运算符返回真，即使考虑的一个(或两个)条件得到满足。否则返回假。例如， **a || b** 如果 a 或 b 之一为真(即非零)，则返回真。当然，当 a 和 b 都为真时，它返回真。
3.  **逻辑非运算符:****“！”**如果考虑的条件不满足，运算符返回 true。否则返回假。比如**！如果 a 为假，即当 a=0 时，a** 返回真。

**例:**

## C

```
// C program to demonstrate working of logical operators
#include <stdio.h>

int main()
{
    int a = 10, b = 4, c = 10, d = 20;

    // logical operators

    // logical AND example
    if (a > b && c == d)
        printf("a is greater than b AND c is equal to d\n");
    else
        printf("AND condition not satisfied\n");

    // logical OR example
    if (a > b || c == d)
        printf("a is greater than b OR c is equal to d\n");
    else
        printf("Neither a is greater than b nor c is equal "
               " to d\n");

    // logical NOT example
    if (!a)
        printf("a is zero\n");
    else
        printf("a is not zero");

    return 0;
}
```

## C++

```
// C++ program to demonstrate working of
// logical operators
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 4, c = 10, d = 20;

    // logical operators

    // logical AND example
    if (a > b && c == d)
        cout << "a is greater than b AND c is equal to d\n";
    else
        cout << "AND condition not satisfied\n";

    // logical OR example
    if (a > b || c == d)
        cout << "a is greater than b OR c is equal to d\n";
    else
        cout << "Neither a is greater than b nor c is equal "
                " to d\n";

    // logical NOT example
    if (!a)
        cout << "a is zero\n";
    else
        cout << "a is not zero";

    return 0;
}
```

**Output:** 

```
AND condition not satisfied
a is greater than b OR c is equal to d
a is not zero
```

**逻辑运算符中的短路:**

*   在**逻辑与**的情况下，如果第一个操作数为假，则不计算第二个操作数。例如，下面的程序 1 没有打印“极客 sQuiz”，因为逻辑“与”本身的第一个操作数是假的。

## C

```
#include <stdbool.h>
#include <stdio.h>
int main()
{
    int a = 10, b = 4;
    bool res = ((a == b) && printf("GeeksQuiz"));
    return 0;
}
```

## C++

```
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 4;
    bool res = ((a == b) && cout << "GeeksQuiz");
    return 0;
}
```

**Output:** 

```
No Output
```

*   但是下面的程序打印“极客 sQuiz”作为逻辑“与”的第一个操作数是真的。

## C

```
#include <stdbool.h>
#include <stdio.h>
int main()
{
    int a = 10, b = 4;
    bool res = ((a != b) && printf("GeeksQuiz"));
    return 0;
}
```

## C++

```
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 4;
    bool res = ((a != b) && cout << "GeeksQuiz");
    return 0;
}
```

**Output:** 

```
GeeksQuiz
```

*   在**逻辑或**的情况下，如果第一个操作数为真，则不计算第二个操作数。例如，下面的程序 1 没有打印“极客 sQuiz”，因为逻辑 or 本身的第一个操作数是真的。

## C

```
#include <stdbool.h>
#include <stdio.h>
int main()
{
    int a = 10, b = 4;
    bool res = ((a != b) || printf("GeeksQuiz"));
    return 0;
}
```

## C++

```
#include <stdbool.h>
#include <stdio.h>
int main()
{
    int a = 10, b = 4;
    bool res = ((a != b) || cout << "GeeksQuiz");
    return 0;
}
```

**Output:** 

```
No Output
```

*   但是下面的程序打印“极客 sQuiz”作为逻辑或的第一个操作数是假的。

## C

```
#include <stdbool.h>
#include <stdio.h>
int main()
{
    int a = 10, b = 4;
    bool res = ((a == b) || printf("GeeksQuiz"));
    return 0;
}
```

## C++

```
#include <stdbool.h>
#include <stdio.h>
int main()
{
    int a = 10, b = 4;
    bool res = ((a == b) || cout << "GeeksQuiz");
    return 0;
}
```

**Output:** 

```
GeeksQuiz
```

[C](https://www.geeksforgeeks.org/c-language-2-gq/operators-gq/)
操作员小测验本文由 Ayush Jaggi 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息
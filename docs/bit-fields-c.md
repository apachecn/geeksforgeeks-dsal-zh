# C 中的位域

> 原文:[https://www.geeksforgeeks.org/bit-fields-c/](https://www.geeksforgeeks.org/bit-fields-c/)

在 C 语言中，我们可以指定结构和联合成员的大小(以位为单位)。当我们知道一个字段或一组字段的值永远不会超过限制或在一个小范围内时，我们的想法是有效地使用内存。
例如，考虑以下不使用位字段的日期声明。

## C

```
#include <stdio.h>
// A simple representation of the date
struct date {
    unsigned int d;
    unsigned int m;
    unsigned int y;
};

int main()
{
    printf("Size of date is %lu bytes\n",
           sizeof(struct date));
    struct date dt = { 31, 12, 2014 };
    printf("Date is %d/%d/%d", dt.d, dt.m, dt.y);
}
```

**Output:** 

```
Size of date is 12 bytes
Date is 31/12/2014
```

上面的' date '表示在编译器上需要 12 个字节，而无符号的 int 需要 4 个字节。因为我们知道 d 的值总是从 1 到 31，m 的值是从 1 到 12，所以我们可以使用位字段来优化空间。

但是，如果使用带符号的 int 编写相同的代码，并且字段的值超出了分配给变量的位，就会发生有趣的事情。例如，考虑相同的代码，但有符号整数:

## C

```
#include <stdio.h>

// Space optimized representation of the date
struct date {
    // d has value between 0 and 31, so 5 bits
    // are sufficient
    int d : 5;

    // m has value between 0 and 15, so 4 bits
    // are sufficient
    int m : 4;

    int y;
};

int main()
{
    printf("Size of date is %lu bytes\n",
           sizeof(struct date));
    struct date dt = { 31, 12, 2014 };
    printf("Date is %d/%d/%d", dt.d, dt.m, dt.y);
    return 0;
}
```

**Output:** 

```
Size of date is 8 bytes
Date is -1/-4/2014
```

结果是负的。后面发生的事情是，值 31 存储在等于 11111 的 5 位有符号整数中。MSB 是 1，所以它是负数，你需要计算二进制数的 2 的补码来得到它的实际值，这是内部完成的。通过计算 2 的补码，你将得到值 00001，它相当于十进制数 1，因为它是负数，所以你得到-1。类似的事情发生在 12 上，在这种情况下，你得到 4 位表示为 1100，在计算 2 的补码时，你得到-4 的值。

**以下是关于 C.**
**1)** 中位域的一些有趣的事实，一个大小为 0 的特殊未命名位域被用来强制对齐下一个边界。例如，考虑以下程序。

## C

```
#include <stdio.h>

// A structure without forced alignment
struct test1 {
    unsigned int x : 5;
    unsigned int y : 8;
};

// A structure with forced alignment
struct test2 {
    unsigned int x : 5;
    unsigned int : 0;
    unsigned int y : 8;
};

int main()
{
    printf("Size of test1 is %lu bytes\n",
           sizeof(struct test1));
    printf("Size of test2 is %lu bytes\n",
           sizeof(struct test2));
    return 0;
}
```

**Output:** 

```
Size of test1 is 4 bytes
Size of test2 is 8 bytes
```

**(2)**我们不能有指向位字段成员的指针，因为它们可能不是从字节边界开始的。

## C

```
#include <stdio.h>
struct test {
    unsigned int x : 5;
    unsigned int y : 5;
    unsigned int z;
};
int main()
{
    struct test t;

    // Uncommenting the following line will make
    // the program compile and run
    printf("Address of t.x is %p", &t.x);

    // The below line works fine as z is not a
    // bit field member
    printf("Address of t.z is %p", &t.z);
    return 0;
}
```

**输出:**

```
prog.c: In function 'main':
prog.c:14:1: error: cannot take address of bit-field 'x'
 printf("Address of t.x is %p", &t.x); 
 ^
```

**3)** 为位字段成员分配超范围值是实现定义的。

## C

```
#include <stdio.h>
struct test {
    unsigned int x : 2;
    unsigned int y : 2;
    unsigned int z : 2;
};
int main()
{
    struct test t;
    t.x = 5;
    printf("%d", t.x);
    return 0;
}
```

**输出:**

```
Implementation-Dependent
```

**4)** 在 C++中，我们可以在一个结构/类中有静态成员，但是位域不能是静态的。

## C++

```
// The below C++ program compiles and runs fine
struct test1 {
    static unsigned int x;
};
int main() {}
```

**Output:** 

## C++

```
// But below C++ program fails in the compilation
// as bit fields cannot be static
struct test1 {
    static unsigned int x : 5;
};
int main() {}
```

**输出:**

```
prog.cpp:5:29: error: static member 'x' cannot be a bit-field
     static unsigned int x : 5;
                             ^
```

**5)** 不允许位域数组。例如，下面的程序在编译中失败。

## C

```
struct test {
    unsigned int x[10] : 5;
};

int main()
{
}
```

**输出:**

```
prog.c:3:1: error: bit-field 'x' has invalid type
 unsigned int x[10]: 5; 
 ^
```

**练习:**
预测以下程序的输出。假设无符号 int 需要 4 个字节，long int 需要 8 个字节。
T4【1)

## C++

```
#include <stdio.h>
struct test {
    unsigned int x;
    unsigned int y : 33;
    unsigned int z;
};
int main()
{
    printf("%lu", sizeof(struct test));
    return 0;
}
```

**2)**

## C++

```
#include <stdio.h>
struct test {
    unsigned int x;
    long int y : 33;
    unsigned int z;
};
int main()
{
    struct test t;
    unsigned int* ptr1 = &t.x;
    unsigned int* ptr2 = &t.z;
    printf("%d", ptr2 - ptr1);
    return 0;
}
```

3)

## C++

```
union test {
    unsigned int x : 3;
    unsigned int y : 3;
    int z;
};

int main()
{
    union test t;
    t.x = 5;
    t.y = 4;
    t.z = 1;
    printf("t.x = %d, t.y = %d, t.z = %d",
           t.x, t.y, t.z);
    return 0;
}
```

**【4)**用 C 语言中的位域找出机器是小端还是大端的方法。
**应用–**

*   如果存储空间有限，我们可以选择位域。
*   对于这种情况，当设备传输状态或编码为多位的信息时，位域是最有效的。
*   加密例程需要访问一个字节中的位，在这种情况下，位字段非常有用。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
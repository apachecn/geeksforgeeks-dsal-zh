# C

中迭代数组的行主序和列主序性能分析

> 原文:[https://www . geesforgeks . org/performance-analysis-of-row-main-and-column-main-order-of-storing-in-c-array/](https://www.geeksforgeeks.org/performance-analysis-of-row-major-and-column-major-order-of-storing-arrays-in-c/)

在计算中，行主顺序和列主顺序是将多维数组存储在线性存储器(如随机存取存储器)中的方法。
上述两种方式在元素在存储器中连续存储的顺序方面彼此不同。以行主顺序排列的元素沿行连续排列，以列主顺序排列的元素沿列连续排列。虽然术语暗指二维阵列(即矩阵)的行和列，但是通过注意术语行主和列主分别等同于词典顺序和词典顺序，可以将顺序推广到任何维度的阵列。
在 C 语言(以及许多其他语言，如 C++、Java 等)中，二维数组以行主顺序存储。(尽管帕斯卡和 Fortran 遵循列主顺序)

这个程序并没有说明 C 语言中数组的行主顺序存储比列主顺序存储更有效。

它只表明在 C 语言中，二维数组是以行主顺序存储的，因此以行主顺序迭代它的元素更有效。

在像 Pascal 和 Fortran 这样的语言中，按列主顺序迭代会更有效，因为二维数组在那里是按列主顺序存储的。

这里正确解释了这种情况的原因。

## C

```
#include <stdio.h>
#include <time.h>
int m[999][999];
//Taking both dimensions same so that while running the loops,
//number of operations (comparisons, iterations, initializations)
//are exactly the same. Refer this for more
// https://www.geeksforgeeks.org/a-nested-loop-puzzle/

void main()

{
    int i, j;
    clock_t start, stop;
    double d = 0.0;

    start = clock();
    for (i = 0; i < 999; i++)
        for (j = 0; j < 999; j++)
            m[i][j] = m[i][j] + (m[i][j] * m[i][j]);

    stop = clock();
    d = (double)(stop - start) / CLOCKS_PER_SEC;
    printf("The run-time of row major order is %lf\n", d);

    start = clock();
    for (j = 0; j < 999; j++)
        for (i = 0; i < 999; i++)
            m[i][j] = m[i][j] + (m[i][j] * m[i][j]);

    stop = clock();
    d = (double)(stop - start) / CLOCKS_PER_SEC;
    printf("The run-time of column major order is %lf", d);
}
```

**Output:** 

```
The run-time of row major order is 0.067300
The run-time of column major order is 0.136622
```
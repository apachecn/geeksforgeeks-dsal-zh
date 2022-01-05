# GCC 编译器的内置函数

> 原文:[https://www . geesforgeks . org/builtin-functions-gcc-compiler/](https://www.geeksforgeeks.org/builtin-functions-gcc-compiler/)

这是 GCC 编译器中四个重要的内置函数:

1.  **__builtin_popcount(x):** 此函数用于计算一个整数中的一(设置位)数。
    **例:**

```
if x = 4
binary value of 4 is 100
Output: No of ones is 1.
```

## C

```
// C program to illustrate _builtin_popcount(x)

#include <stdio.h>
int main()
{
    int n = 5;

    printf("Count of 1s in binary of %d is %d ",
           n, __builtin_popcount(n));
    return 0;
}
```

**Output:** 

```
Count of 1s in binary of 5 is 2
```

1.  **注意:**同样，您可以使用 _ _ builtin _ popcountl(x)&_ _ builtin _ popcountl(x)来处理长数据类型和长数据类型。
2.  **_ _ 内建 _ 奇偶校验(x):** 该功能用于检查一个数字的[奇偶校验](https://www.geeksforgeeks.org/program-to-find-parity/)。这个函数返回真(1)，如果这个数字有奇数奇偶校验，否则它返回假(0)为偶数奇偶校验。
    **例:**

```
if x = 7
7 has odd no. of 1's in its binary(111).
Output: Parity of 7 is 1 
```

## C

```
// C program to illustrate _builtin_parity(x)

#include <stdio.h>
int main()
{
    int n = 7;

    printf("Parity of %d is %d ",
           n, __builtin_parity(n));
    return 0;
}
```

**Output:** 

```
Parity of 7 is 1
```

1.  **注意:**同样，您可以使用 _ _ builtin _ parityl(x)&_ _ builtin _ parityl(x)来处理长数据类型和长数据类型。
2.  **__builtin_clz(x):** 此函数用于计算整数的前导零。注意:clz =计算前导零的数量
    **示例:**它计算第一次出现 1(设置位)之前的零的数量。

```
a = 16
Binary form of 16 is 00000000 00000000 00000000 00010000
Output: 27
```

## C

```
// C program to illustrate __builtin_clz(x)
#include <stdio.h>
int main()
{
    int n = 16;

    printf("Count of leading zeros before 1 in %d is %d",
           n, __builtin_clz(n));
    return 0;
}
```

**Output:** 

```
Count of leading zeros before 1 in 16 is 27
```

1.  **注意:** __builtin_clz(x)这个函数只接受无符号的值
    **注意:**同样你可以使用 _ _ builtin _ clzl(x)&_ _ builtin _ clzll(x)来表示长的和长的数据类型。
2.  **__builtin_ctz(x):** 此函数用于计算给定整数的尾随零。注意:ctz =计算尾随零。
    **示例:**从最后一次出现到第一次出现(设置位)计算零的数量。

```
a = 16
Binary form of 16 is 00000000 00000000 00000000 00010000
Output: ctz = 4
```

## C

```
// C program to illustrate __builtin_ctz(x)
#include <stdio.h>
int main()
{
    int n = 16;

    printf("Count of zeros from last to first "
           "occurrence of one is %d",
           __builtin_ctz(n));
    return 0;
}
```

**Output:** 

```
Count of zeros from last to first occurrence of one is 4
```

1.  **注意:**同样，您可以使用 _ _ builtin _ ctzl(x)&_ _ builtin _ ctzl(x)来处理长数据类型和长数据类型。
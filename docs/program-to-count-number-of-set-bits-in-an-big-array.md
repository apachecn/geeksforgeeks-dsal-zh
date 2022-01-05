# 对(大)数组中的设定位数进行计数的程序

> 原文:[https://www . geesforgeks . org/program-to-count-大数组中的位数/](https://www.geeksforgeeks.org/program-to-count-number-of-set-bits-in-an-big-array/)

给定长度为 N 的整数数组(任意大的数)。如何计算数组中设置的位数？
简单的方法是，创建一个有效的方法来计数一个字中的设定位(最显著的大小，通常等于处理器的位长度)，并从数组的单个元素中添加位。
整数的集合位存在多种计数方法，参见[本](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)举例。这些方法在最好的情况下运行，其中 N 是位数。请注意，在一个 N 固定的处理器上，计数可以在 32 位机器上以 O(1)的时间完成，而不考虑总的设置位。总的来说，数组中的位可以在 0(n)时间内计算，其中“n”是数组大小。
然而，当数组大的时候，查表会是更有效的方法。存储可以处理 2 <sup>32</sup> 整数的查表是不切实际的。
下面的代码说明了一个简单的程序，用于对随机生成的 64 K 整数数组中的设置位进行计数。其思想是为前 256 个数字(一个字节)生成一个查找表，并在字节边界处断开数组的每个元素。使用 C/C++预处理器的元程序生成查找表，用于计数一个字节中的设置位。
元程序背后的数学推导从下表中显而易见(将列和行索引相加以获得数字，然后查看表以获得该数字中的设置位。例如，要获取 10 中的设置位，可以从名为 8 的行和名为 2 的列中提取，

```
   0, 1, 2, 3
 0 - 0, 1, 1, 2 -------- GROUP_A(0)
 4 - 1, 2, 2, 3 -------- GROUP_A(1)
 8 - 1, 2, 2, 3 -------- GROUP_A(1)
12 - 2, 3, 3, 4 -------- GROUP_A(2)
16 - 1, 2, 2, 3 -------- GROUP_A(1)
20 - 2, 3, 3, 4 -------- GROUP_A(2)
24 - 2, 3, 3, 4 -------- GROUP_A(2)
28 - 3, 4, 4, 5 -------- GROUP_A(3) ... so on
```

从表中可以看出，无论是在表中还是在组参数中，都出现了 4 的倍数模式。序列可以概括为代码所示。
**复杂度:**
除了迭代数组，所有操作都取 O(1)。时间复杂度为 0(n)，其中“n”是数组的大小。空间复杂度取决于生成查找的元程序。
**代号:**

## C++

```
#include <bits/stdc++.h>
#include <time.h>
using namespace std;

/* Size of array 64 K */
#define SIZE (1 << 16)

/* Meta program that generates set bit count
array of first 256 integers */

/* GROUP_A - When combined with META_LOOK_UP
generates count for 4x4 elements */

#define GROUP_A(x) x, x + 1, x + 1, x + 2

/* GROUP_B - When combined with META_LOOK_UP
generates count for 4x4x4 elements */

#define GROUP_B(x) GROUP_A(x), GROUP_A(x+1), GROUP_A(x+1), GROUP_A(x+2)

/* GROUP_C - When combined with META_LOOK_UP
generates count for 4x4x4x4 elements */

#define GROUP_C(x) GROUP_B(x), GROUP_B(x+1), GROUP_B(x+1), GROUP_B(x+2)

/* Provide appropriate letter to generate the table */

#define META_LOOK_UP(PARAMETER)\
GROUP_##PARAMETER(0),\
GROUP_##PARAMETER(1),\
GROUP_##PARAMETER(1),\
GROUP_##PARAMETER(2)\

int countSetBits(int array[], size_t array_size)
{
int count = 0;

/* META_LOOK_UP(C) - generates a table of 256 integers whose
    sequence will be number of bits in i-th position
    where 0 <= i < 256
*/

    /* A static table will be much faster to access */
    static unsigned char const look_up[] = { META_LOOK_UP(C) };

    /* No shifting funda (for better readability) */
    unsigned char *pData = NULL;

for(size_t index = 0; index < array_size; index++)
{
    /* It is fine, bypass the type system */
    pData = (unsigned char *)&array[index];

    /* Count set bits in individual bytes */
    count += look_up[pData[0]];
    count += look_up[pData[1]];
    count += look_up[pData[2]];
    count += look_up[pData[3]];
}

return count;
}

/* Driver program, generates table of random 64 K numbers */
int main()
{
int index;
int random[SIZE];

/* Seed to the random-number generator */
srand((unsigned)time(0));

/* Generate random numbers. */
for( index = 0; index < SIZE; index++ )
{
    random[index] = rand();
}

cout << "Total number of bits = "<< countSetBits(random, SIZE);
return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

/* Size of array 64 K */
#define SIZE (1 << 16)

/* Meta program that generates set bit count
   array of first 256 integers */

/* GROUP_A - When combined with META_LOOK_UP
   generates count for 4x4 elements */

#define GROUP_A(x) x, x + 1, x + 1, x + 2

/* GROUP_B - When combined with META_LOOK_UP
   generates count for 4x4x4 elements */

#define GROUP_B(x) GROUP_A(x), GROUP_A(x+1), GROUP_A(x+1), GROUP_A(x+2)

/* GROUP_C - When combined with META_LOOK_UP
   generates count for 4x4x4x4 elements */

#define GROUP_C(x) GROUP_B(x), GROUP_B(x+1), GROUP_B(x+1), GROUP_B(x+2)

/* Provide appropriate letter to generate the table */

#define META_LOOK_UP(PARAMETER) \
   GROUP_##PARAMETER(0),  \
   GROUP_##PARAMETER(1),  \
   GROUP_##PARAMETER(1),  \
   GROUP_##PARAMETER(2)   \

int countSetBits(int array[], size_t array_size)
{
   int count = 0;

   /* META_LOOK_UP(C) - generates a table of 256 integers whose
      sequence will be number of bits in i-th position
      where 0 <= i < 256
   */

    /* A static table will be much faster to access */
       static unsigned char const look_up[] = { META_LOOK_UP(C) };

    /* No shifting funda (for better readability) */
    unsigned char *pData = NULL;

   for(size_t index = 0; index < array_size; index++)
   {
      /* It is fine, bypass the type system */
      pData = (unsigned char *)&array[index];

      /* Count set bits in individual bytes */
      count += look_up[pData[0]];
      count += look_up[pData[1]];
      count += look_up[pData[2]];
      count += look_up[pData[3]];
   }

   return count;
}

/* Driver program, generates table of random 64 K numbers */
int main()
{
   int index;
   int random[SIZE];

   /* Seed to the random-number generator */
   srand((unsigned)time(0));

   /* Generate random numbers. */
   for( index = 0; index < SIZE; index++ )
   {
      random[index] = rand();
   }

   printf("Total number of bits = %d\n", countSetBits(random, SIZE));
   return 0;
}
```

**时间复杂度:** O(n)

**辅助空间:** O(大小)

文基**投稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。**
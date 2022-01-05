# 使用按位运算符计算 C/C++中两个整数的最大值

> 原文:[https://www . geeksforgeeks . org/compute-使用按位运算符计算 c-c 中两个整数的最大值/](https://www.geeksforgeeks.org/compute-maximum-of-two-integers-in-c-c-using-bitwise-operators/)

给定两个整数 **A** 和 **B** ，任务是[使用](https://www.geeksforgeeks.org/maximum-of-two-numbers-in-python/)[按位运算符](https://www.geeksforgeeks.org/interesting-facts-bitwise-operators-c/)找到两个数字的最大值。

**示例:**

> **输入:** A = 40，B = 54
> T3】输出: 54
> 
> **输入:** A = -1，B =-10
> T3】输出: -1

**方法:**思路是使用[按位运算符](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)以及[右移运算符](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)来查找两个不同数字之间的最大值，而不使用任何[条件语句](https://www.geeksforgeeks.org/using-else-conditional-statement-with-for-loop-in-python/)(if……)和[三进运算符(？:)](https://www.geeksforgeeks.org/conditional-or-ternary-operator-in-c-c/)。以下是步骤:

*   根据以下表达式找出最大值:

> z = A–B
> I =(z>>31)&1
> max = A–(I * z)

*   减去两个数字，存储在另一个变量 **z** 中。
*   要得到减法运算后得到的数的符号，将 [](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/) [右移](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)到变量 **z** 并将其存储到另一个变量 **i** 中，然后用 **1** 对变量 **i** 执行[逐位与运算](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，得到 **1** 或 **0** 中的值。
*   执行以下表达式，获得两个给定数字中的最大值**max =(a –( I * z))**。

插图:

> A = 40，B = 54
> z =(A–B)= 40–54 =-14
> I =-1&1 = 1
> max = A–(I * z)=(40 –( 1 *-14))= 54

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <stdio.h>

// Function to find the largest number
int findMax(int a, int b)
{
    int z, i, max;

    // Perform the subtraction
    z = a - b;

    // Right shift and Bitwise AND
    i = (z >> 31) & 1;

    // Find the maximum number
    max = a - (i * z);

    // Return the maximum value
    return max;
}

// Driver Code
int main()
{
    int A = 40, B = 54;

    // Function Call
    printf("%d", findMax(A, B));

    return 0;
}
```

## C++

```
// C++ program for above approach
#include <iostream>
using namespace std;

// Function to find the largest number
int findMax(int a, int b)
{
    int z, i, max;

    // Perform the subtraction
    z = a - b;

    // Right shift and Bitwise AND
    i = (z >> 31) & 1;

    // Find the maximum number
    max = a - (i * z);

    // Return the maximum value
    return max;
}

// Driver Code
int main()
{
    int A = 40, B = 54;

    // Function Call
    cout << findMax(A, B);

    return 0;
}
```

**Output:**

```
54

```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)
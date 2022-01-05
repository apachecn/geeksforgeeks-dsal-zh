# C/C++程序寻找给定范围内的素数

> 原文:[https://www . geesforgeks . org/c-CPP-program-to-find-质数-给定区间/](https://www.geeksforgeeks.org/c-cpp-program-to-find-prime-numbers-between-given-range/)

给定两个数字 **L** 和 **R，**的任务是在 **L** 和 **R** 之间找到[质数](https://www.geeksforgeeks.org/prime-numbers/)。

**示例:**

> **输入:** L = 1，R = 10
> **输出:** 2 3 5 7
> **说明:**
> 1 和 10 之间的素数是 2、3、5 和 7
> 
> **输入:** L = 30，R = 40
> T3】输出: 31 37

**方法:**思路是从**【L，R】**范围内迭代，检查给定范围内是否有素数。如果是，那么打印这个数字，并检查下一个数字，直到我们迭代所有的数字。

以下执行上述方法:

## C

```
// C program to find the prime numbers
// between a given interval
#include <stdio.h>

// Function for print prime
// number in given range
void primeInRange(int L, int R)
{
    int i, j, flag;

    // Traverse each number in the
    // interval with the help of for loop
    for (i = L; i <= R; i++) {

        // Skip 0 and 1 as they are
        // neither prime nor composite
        if (i == 1 || i == 0)
            continue;

        // flag variable to tell
        // if i is prime or not
        flag = 1;

        // Iterate to check if i is prime
        // or not
        for (j = 2; j <= i / 2; ++j) {
            if (i % j == 0) {
                flag = 0;
                break;
            }
        }

        // flag = 1 means i is prime
        // and flag = 0 means i is not prime
        if (flag == 1)
            printf("%d ", i);
    }
}

// Driver Code
int main()
{
    // Given Range
    int L = 1;
    int R = 10;

    // Function Call
    primeInRange(L, R);

    return 0;
}
```

## C++

```
// C++ program to find the prime numbers
// between a given interval
#include <bits/stdc++.h>
using namespace std;

// Function for print prime
// number in given range
void primeInRange(int L, int R)
{
    int flag;

    // Traverse each number in the
    // interval with the help of for loop
    for (int i = L; i <= R; i++) {

        // Skip 0 and 1 as they are
        // neither prime nor composite
        if (i == 1 || i == 0)
            continue;

        // flag variable to tell
        // if i is prime or not
        flag = 1;

        // Iterate to check if i is prime
        // or not
        for (int j = 2; j <= i / 2; ++j) {
            if (i % j == 0) {
                flag = 0;
                break;
            }
        }

        // flag = 1 means i is prime
        // and flag = 0 means i is not prime
        if (flag == 1)
            cout << i << " ";
    }
}

// Driver Code
int main()
{
    // Given Range
    int L = 1;
    int R = 10;

    // Function Call
    primeInRange(L, R);

    return 0;
}
```

**Output:** 

```
2 3 5 7
```

**时间复杂度:** *O((R-L)*N)* ，其中 N 为数字，L 和 R 为给定范围。
**辅助空间:** *O(1)*
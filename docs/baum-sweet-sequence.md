# 波姆甜序列

> 原文:[https://www.geeksforgeeks.org/baum-sweet-sequence/](https://www.geeksforgeeks.org/baum-sweet-sequence/)

[波姆甜序列](https://en.wikipedia.org/wiki/Baum%E2%80%93Sweet_sequence)是 0 和 1 的无限二进制序列。如果数字 n 在其二进制表示中没有奇数个连续零，则序列的第 n 项为 1，否则第 n 项为 0。

```
The first few terms of the sequence are:
b1 = 1 (binary of 1 is 1)
b2 = 0 (binary of 2 is 10)
b3 = 1 (binary of 3 is 11)
b4 = 1 (binary of 4 is 100)
b5 = 0 (binary of 5 is 101)
b6 = 0 (binary of 6 is 110)

```

给定一个自然数 **n** 。任务是找到鲍姆甜序列的第 n 项，即检查它是否包含任何奇数长度的连续零块。

```
Input: n = 8
Output: 0
*Explanations:*
Binary representation of 8 is 1000\. It 
contains odd length block of consecutive 0s. 
Therefore B8 is 0.

Input: n = 5
Output: 1

Input: n = 7
Output: 0

```

其思想是在 n 的二进制表示中运行一个循环，并计算存在的所有连续零块的长度。如果至少有一个奇数长度的零块，那么给定输入 n 的第 n 项为 0，否则为 1。

```
// CPP code to find the nth term of the
// Baum Sweet Sequence
#include <bits/stdc++.h>
using namespace std;

int nthBaumSweetSeq(int n)
{
    // bitset stores bitwise representation
    bitset<32> bs(n);

    // len stores the number of bits in the 
    // binary of n. builtin_clz() function gives 
    // number of zeroes present before the 
    // leading 1 in binary of n
    int len = 32 - __builtin_clz(n);

    int baum = 1; // nth term of baum sequence
    for (int i = 0; i < len;) {
        int j = i + 1;

        // enter into a zero block
        if (bs[i] == 0) {
            int cnt = 1;

            // loop to run through each zero block
            // in binary representation of n
            for (j = i + 1; j < len; j++) {

                // counts consecutive zeroes 
                if (bs[j] == 0)                   
                    cnt++;
                else
                    break;
            }

            // check if the number of consecutive
            // zeroes is odd
            if (cnt % 2 == 1)
                baum = 0;
        }
        i = j;
    }

    return baum;
}

// Driver Code
int main()
{
    int n = 8;
    cout << nthBaumSweetSeq(n);
    return 0;
}
```

**Output:**

```
0

```
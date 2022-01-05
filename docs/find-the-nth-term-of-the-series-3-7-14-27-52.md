# 求数列 3，7，14，27，52，.。。

> 原文:[https://www . geesforgeks . org/find-the-n-term-of-series-3-7-14-27-52/](https://www.geeksforgeeks.org/find-the-nth-term-of-the-series-3-7-14-27-52/)

给定正整数 **N** 。任务是找到系列的第 n 个**术语 **3，7，14，27，52…..****

**示例**:

> **输入** : N = 5
> 输出 : 52
> 
> **输入** : N = 1
> 输出 : 3

**进场:**

该序列通过使用以下模式形成。对于任何数值 N-

> **T<sub>N</sub>=(N-1)+3 * 2<sup>N-1</sup>T5】**

插图:

> **输入:** N = 5
> **输出:** 52
> **解释:**
> T<sub>N</sub>=(5–1)+3 * 2<sup>5–1</sup>
> <sup>= 4+3 * 16
> = 52</sup>

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return Nth term
// of the series
int calcNum(int N)
{
    return ((N - 1) + 3 * 
             pow(2, N - 1));
}

// Driver Code
int main()
{
    int N = 5;
    cout << calcNum(N);
    return 0;
}
```

**Output**

```
52
```

***时间复杂度:*** O(1)

***辅助空间:*** O(1)
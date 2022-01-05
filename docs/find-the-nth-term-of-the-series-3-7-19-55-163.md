# 求数列 3、7、19、55、163、.。。

> 原文:[https://www . geesforgeks . org/find-the-n-term-of-series-3-7-19-55-163/](https://www.geeksforgeeks.org/find-the-nth-term-of-the-series-3-7-19-55-163/)

给定正整数 **N** 。任务是找到系列 3，7，19，55，163 的第 n 个术语**..**

**示例**:

> **输入** : N = 5
> 输出 : 163
> 
> **输入** : N = 1
> 输出 : 3

**逼近**:使用以下模式形成序列。对于任何 N 值

> t<sub>N</sub>= 2 * 3<sup>N–1</sup>+1

插图:

> **输入:** N = 5
> **输出:** 163
> **解释:**
> T<sub>N</sub>= 2 * 3<sup>N–1</sup>+1
> = 2 * 3<sup>5–1</sup>+1
> = 2 * 81+1
> = 162+1
> = 163

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
    return 2 * pow(3, N - 1) + 1;
}

// Driver Code
int main()
{
    int N = 5;
    cout << calcNum(N);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return Nth term
# of the series
def calcNum(N):

    return 2 * (3 ** (N - 1)) + 1

# Driver Code
N = 5

print(calcNum(N))

# This code is contributed by gfgking
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to return Nth term
      // of the series
      function calcNum(N) {
          return 2 * Math.pow(3, N - 1) + 1;
      }

      // Driver Code

      let N = 5;
      document.write(calcNum(N));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
163
```

***时间复杂度:*** O(1)

***辅助空间:*** O(1)
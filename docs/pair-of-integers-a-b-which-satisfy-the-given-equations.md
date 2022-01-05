# 满足给定方程的整数对(a，b)

> 原文:[https://www . geesforgeks . org/满足给定方程的整数对 a-b/](https://www.geeksforgeeks.org/pair-of-integers-a-b-which-satisfy-the-given-equations/)

给定方程组 **a <sup>2</sup> + b = n** 和 **a + b <sup>2</sup> = m** 。任务是找出满足给定的 **n** 和 **m** 等式的正整数对 **(a，b)** 的个数。
**举例:**

> **输入:** n = 9，m = 3
> **输出:** 1
> **解释:**
> 满足条件的两个方程只存在一对(3，0)。
> **输入:** n = 4，m = 20
> **输出:** 0
> **说明:**
> 不存在这样的对。

**方法:**
方法是检查所有可能的数字对，并检查该对是否满足两个方程。为此，我们有

```
   a2 + b = n ... (1)
   a + b2 = m ... (2)
For equation (2), 
=> a = m - b2 ... (3)
```

*   现在对于 a 的正值，b 的每个值都必须从 0 到 sqrt(m)。
*   从等式(3)中获得 a 的值。
*   如果配对 **(a，b)** 满足方程(1)，那么配对 **(a，b)** 就是方程组的解。

以下是上述方法的实现:

## C++

```
// C++ program to count the pair of integers(a, b)
// which satisfy the equation
// a^2 + b = n and a + b^2 = m
#include <bits/stdc++.h>
using namespace std;

// Function to count valid pairs
int pairCount(int n, int m)
{
    int cnt = 0, b, a;
    for (b = 0; b <= sqrt(m); b++) {
        a = m - b * b;
        if (a * a + b == n) {
            cnt++;
        }
    }
    return cnt;
}

// Driver code
int main()
{
    int n = 9, m = 3;

    cout << pairCount(n, m) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the pair of integers(a, b)
// which satisfy the equation
// a^2 + b = n and a + b^2 = m
class GFG
{

// Function to count valid pairs
static int pairCount(int n, int m)
{
    int cnt = 0, b, a;
    for (b = 0; b <= Math.sqrt(m); b++)
    {
        a = m - b * b;
        if (a * a + b == n)
        {
            cnt++;
        }
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int n = 9, m = 3;
    System.out.print(pairCount(n, m) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count the pair of integers(a, b)
# which satisfy the equation
# a^2 + b = n and a + b^2 = m

# Function to count valid pairs
def pairCount(n, m):
    cnt = 0;
    for b in range(int(pow(m, 1/2))):
        a = m - b * b;
        if (a * a + b == n):
            cnt += 1;

    return cnt;

# Driver code
if __name__ == '__main__':
    n = 9;
    m = 3;
    print(pairCount(n, m));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to count the pair of integers(a, b)
// which satisfy the equation
// a^2 + b = n and a + b^2 = m
using System;

class GFG
{

// Function to count valid pairs
static int pairCount(int n, int m)
{
    int cnt = 0, b, a;
    for (b = 0; b <= Math.Sqrt(m); b++)
    {
        a = m - b * b;
        if (a * a + b == n)
        {
            cnt++;
        }
    }
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int n = 9, m = 3;
    Console.Write(pairCount(n, m) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to count the pair of integers(a, b)
// which satisfy the equation
// a^2 + b = n and a + b^2 = m

// Function to count valid pairs
function pairCount(n , m)
{
    var cnt = 0, b, a;
    for (b = 0; b <= Math.sqrt(m); b++)
    {
        a = m - b * b;
        if (a * a + b == n)
        {
            cnt++;
        }
    }
    return cnt;
}

// Driver code
var n = 9, m = 3;
document.write(pairCount(n, m));

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(sqrt(min(n，m))
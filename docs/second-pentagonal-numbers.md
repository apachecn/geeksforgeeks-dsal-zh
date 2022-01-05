# 第二个五边形数字

> 原文:[https://www.geeksforgeeks.org/second-pentagonal-numbers/](https://www.geeksforgeeks.org/second-pentagonal-numbers/)

第二个五边形数字是可以以正五边形排列的物体的集合。
第二个五边形系列是:

> 2, 7, 15, 26, 40, 57, 77, 100, 126, … ..

### 求第二个五边形级数的第 N <sup>个</sup>项

给定一个整数 **N** 。任务是找到第二个五边形级数的第 N 项。
**示例** :

> **输入:** N = 1
> **输出:** 2
> **输入:** N = 4
> **输出:** 26

**方法:**其思想是找到级数的一般项，该项可以借助如下观测值计算:

> 系列= 2，7，15，26，40，57，77，100，126，…..
> 差值= 7–2，15–7，26–15，40–26，…。
> = 5，8，11，14 ……这是一个 AP
> 所以给定系列的第 n 项
> 第 n 项= 2 + (5 + 8 + 11 + 14 …… (n-1)项)
> = 2+(n-1)/2 *(2 * 5+(n-1-1)* 3)
> = 2+(n-1)/2 *(10+3n-6)
> = 2+(n-1)*(3n+4)/2【T7

因此，该系列的第 n 项给出为![\frac{n*(3*n+1)}{2}  ](img/4f5e0dc3a911925f624f3d4d51999f6a.png "Rendered by QuickLaTeX.com")
以下是上述方法的实施:

## C++

```
// C++ implementation to
// find N-th term in the series

#include <iostream>
#include <math.h>
using namespace std;

// Function to find N-th term
// in the series
void findNthTerm(int n)
{
    cout << n * (3 * n + 1) / 2
         << endl;
}

// Driver code
int main()
{
    int N = 4;
    findNthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// find N-th term in the series
class GFG{

// Function to find N-th term
// in the series
static void findNthTerm(int n)
{
    System.out.print(n * (3 *
                     n + 1) / 2 + "\n");
}

// Driver code
public static void main(String[] args)
{
    int N = 4;
    findNthTerm(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to
# find N-th term in the series

# Function to find N-th term
# in the series
def findNthTerm(n):

    print(n * (3 * n + 1) // 2, end = " ");

# Driver code
N = 4;
findNthTerm(N);

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation to
// find N-th term in the series
using System;
class GFG{

// Function to find N-th term
// in the series
static void findNthTerm(int n)
{
    Console.Write(n * (3 *
                  n + 1) / 2 + "\n");
}

// Driver code
public static void Main()
{
    int N = 4;
    findNthTerm(N);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation t
// find N-th term in the series

// Function to find N-th term
// in the series
function findNthTerm(n)
{
    document.write(n * (3 * n + 1) / 2);
}

// Driver code
N = 4;
findNthTerm(N);

</script>
```

**Output:** 

```
26
```

**参考:**T2https://oeis.org/A005449
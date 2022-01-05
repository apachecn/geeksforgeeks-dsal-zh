# 中心多边形数

> 原文:[https://www.geeksforgeeks.org/central-polygonal-numbers/](https://www.geeksforgeeks.org/central-polygonal-numbers/)

给定一个数 **N** ，任务是编写一个程序来寻找中心多边形数系列的第 N 项:

> **1，1，3，7，13，21，31，43，57…..**

**示例** :

```
Input: N = 0
Output: 1

Input: N = 3
Output: 7
```

**方法:**第 n 个术语可以形式化为:

> 级数= 1，3，7，13，21，31，43，57……
> 差= 3-1，7-3，13-7，21-13……
> 差= 2、4、6、8 ……这是 AP
> 所以给定系列的第 n 项
> = 1 + (2、4、6、8 …… (n-1)项)
> = 1+(n-1)/2 *(2 * 2+(n-1-1)* 2)
> = 1+(n-1)/2 *(4+2n-4)
> = 1+(n-1)* n
> = n^2–n+1

因此，级数的第 n 项给出为

> ![n^2 - n + 1 ](img/402322828ffc737d608c379f91e886b2.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ program to find N-th term
// in the series
#include <iostream>
#include <math.h>
using namespace std;

// Function to find N-th term
// in the series
void findNthTerm(int n)
{
    cout << n * n - n + 1 << endl;
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
// Java program to find N-th term
// in the series
class GFG{

// Function to find N-th term
// in the series
static void findNthTerm(int n)
{
    System.out.println(n * n - n + 1);
}

// Driver code
public static void main(String[] args)
{
    int N = 4;

    findNthTerm(N);
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program to find N-th term
# in the series

# Function to find N-th term
# in the series
def findNthTerm(n):
    print(n * n - n + 1)

# Driver code
N = 4

# Function Call
findNthTerm(N)

# This code is contributed by Vishal Maurya
```

## C#

```
// C# program to find N-th term
// in the series
using System;
class GFG{

// Function to find N-th term
// in the series
static void findNthTerm(int n)
{
    Console.Write(n * n - n + 1);
}

// Driver code
public static void Main()
{
    int N = 4;

    findNthTerm(N);
}
}

// This code is contributed by nidhi_biet
```

## java 描述语言

```
<script>

// Javascript program to find N-th term
// in the series

// Function to find N-th term
// in the series
function findNthTerm(n)
{
    document.write(n * n - n + 1);
}

// Driver code
N = 4;
findNthTerm(N);

</script>
```

**Output:** 

```
13
```
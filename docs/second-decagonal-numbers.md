# 第二个十边形数字

> 原文:[https://www.geeksforgeeks.org/second-decagonal-numbers/](https://www.geeksforgeeks.org/second-decagonal-numbers/)

第二个十边形数字系列可以表示为

> 7, 22, 45, 76, 115, 162, 217, 280,,… ..

第 N 项
给定一个整数 **N** 。任务是找到给定数列的第 N 项。
T4 举例:

> **输入:**N = 1
> T3】输出: 7
> 
> **输入:**N = 4
> T3】输出: 76

**方法:**想法是找到第二个十边形数的通称。下面是第二个十边形数的一般项的计算:

> 第一项= 1 * (4*1 + 3) = 7
> 第二项= 2 * (4*2 + 3) = 22
> 第三项= 3 * (4*3 + 3) = 45
> 第四项= 4 * (4*4 + 3) = 76
> 。
> 。
> 。
> 第 n 项= n * (4 * n + 3)
> 因此，该系列的第 n 项给出为![N * (4 * N + 3)   ](img/32347b7932eaf2866d126c411691b5e1.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现:

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
    cout << n * (4 * n + 3) << endl;
}

// Driver Code
int main()
{
    int N = 4;
    findNthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find N-th term
// in the series
static void findNthTerm(int n)
{
    System.out.println(n * (4 * n + 3));
}

// Driver code
public static void main(String[] args)
{
    int N = 4;

    findNthTerm(N);
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 implementation to
# find N-th term in the series

# Function to find N-th term
# in the series
def findNthTerm(n):

    print(n * (4 * n + 3))

# Driver Code
N = 4;
findNthTerm(N);

# This code is contributed by Code_Mech
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find N-th term
// in the series
static void findNthTerm(int n)
{
    Console.WriteLine(n * (4 * n + 3));
}

// Driver code
public static void Main(String[] args)
{
    int N = 4;

    findNthTerm(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation to
// find N-th term in the series

// Function to find N-th term
// in the series
function findNthTerm(n)
{
    document.write(n * (4 * n + 3));
}

// Driver Code
let N = 4;
findNthTerm(N);

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
76
```

**时间复杂度:** O(1)

**辅助空间:** O(1)

**参考:**T2】OEIS
# 在给定规则生成的矩阵中找到元素

> 原文:[https://www . geeksforgeeks . org/查找给定规则生成的矩阵中的元素/](https://www.geeksforgeeks.org/find-the-element-in-the-matrix-generated-by-given-rules/)

给定一些规则来生成一个 **N × N** 矩阵 **mat[][]** 和两个整数 **R** 和 **C** ，任务是在**R**行和**C**列找到元素。规则如下:

1.  第一行是以 **1** 和 **d = 1** 开始的 AP 系列(共差)。
2.  对于(I，j)处的所有元素，如 **i > j** ，其值为 **0** 。
3.  其余元素如下，**元素(I，j) =元素(I–1，j) +元素(I–1，j–1)**。

**例:**

> **输入:** N = 4，R = 3，C = 4
> **输出:** 12
> mat[][] =
> {1，2，3，4}，
> {0，3，5，7}，
> {0，0，8，12}，
> {0，0，0，20}
> 第三行第四列的元素为 12。
> **输入:** N = 2，R = 2，C = 2
> **输出:** 3

**进场:**

*   最基本的关键是观察模式，首先观察的是每一行在 **(i，i)** 的元素后都会有一个 AP。行号 **j** 的共同区别是 **pow(2，j–1)**。
*   现在我们需要找到每一行的第一项才能找到任何元素 **(R，C)** 。如果我们只考虑每行的起始元素(即对角线上的元素)，我们可以观察到从 **2** 到 **N** 的每一行 **R** 都等于 **(R + 1) *幂(2，R–2)**。
*   所以，如果 **R > C** 那么元素是 **0** 否则**C–R**是 AP 中所需元素的位置，它存在于 **R <sup>第</sup>** 行中，对于它我们已经知道了起始项和共同的区别。所以，我们可以找到元素为**start+d *(C–R)**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the element in the rth row
// and cth column from the required matrix
int getElement(int N, int r, int c)
{

    // Condition for lower half of matrix
    if (r > c)
        return 0;

    // Condition if element is in first row
    if (r == 1) {
        return c;
    }

    // Starting element of AP in row r
    int a = (r + 1) * pow(2, r - 2);

    // Common difference of AP in row r
    int d = pow(2, r - 1);

    // Position of element to find
    // in AP in row r
    c = c - r;

    int element = a + d * c;

    return element;
}

// Driver Code
int main()
{
    int N = 4, R = 3, C = 4;

    cout << getElement(N, R, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.*;

class GFG
{

// Function to return the element
// in the rth row and cth column
// from the required matrix
static int getElement(int N, int r, int c)
{

    // Condition for lower half of matrix
    if (r > c)
        return 0;

    // Condition if element is in first row
    if (r == 1)
    {
        return c;
    }

    // Starting element of AP in row r
    int a = (r + 1) * (int)(Math.pow(2,(r - 2)));

    // Common difference of AP in row r
    int d = (int)(Math.pow(2,(r - 1)));

    // Position of element to find
    // in AP in row r
    c = c - r;

    int element = a + d * c;

    return element;
}

// Driver Code
public static void main(String[] args)
{
    int N = 4, R = 3, C = 4;

    System.out.println(getElement(N, R, C));
}
}

// This code is contributed by Krikti
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the element in the rth row
# and cth column from the required matrix
def getElement(N, r, c) :

    # Condition for lower half of matrix
    if (r > c) :
        return 0;

    # Condition if element is in first row
    if (r == 1) :
        return c;

    # Starting element of AP in row r
    a = (r + 1) * pow(2, r - 2);

    # Common difference of AP in row r
    d = pow(2, r - 1);

    # Position of element to find
    # in AP in row r
    c = c - r;

    element = a + d * c;

    return element;

# Driver Code
if __name__ == "__main__" :

    N = 4; R = 3; C = 4;

    print(getElement(N, R, C));

# This Code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to return the element
// in the rth row and cth column
// from the required matrix
static int getElement(int N, int r, int c)
{

    // Condition for lower half of matrix
    if (r > c)
        return 0;

    // Condition if element is in first row
    if (r == 1)
    {
        return c;
    }

    // Starting element of AP in row r
    int a = (r + 1) * (int)(Math.Pow(2,(r - 2)));

    // Common difference of AP in row r
    int d = (int)(Math.Pow(2,(r - 1)));

    // Position of element to find
    // in AP in row r
    c = c - r;

    int element = a + d * c;

    return element;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 4, R = 3, C = 4;

    Console.WriteLine(getElement(N, R, C));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Java script implementation of the above approach

// Function to return the element
// in the rth row and cth column
// from the required matrix
function getElement( N,  r,  c)
{

    // Condition for lower half of matrix
    if (r > c)
        return 0;

    // Condition if element is in first row
    if (r == 1)
    {
        return c;
    }

    // Starting element of AP in row r
    let a = (r + 1) * parseInt(Math.pow(2,(r - 2)));

    // Common difference of AP in row r
    let d = parseInt(Math.pow(2,(r - 1)));

    // Position of element to find
    // in AP in row r
    c = c - r;

    let element = a + d * c;

    return element;
}

// Driver Code
    let N = 4, R = 3, C = 4;

    document.write(getElement(N, R, C));

//contributed by bobby

</script>
```

**Output:** 

```
12
```
# 在给定范围内选择一个随机数得到一个完美平方的概率

> 原文:[https://www . geeksforgeeks . org/在给定范围内选择随机数时获得完美平方的概率/](https://www.geeksforgeeks.org/probability-of-getting-a-perfect-square-when-a-random-number-is-chosen-in-a-given-range/)

给定表示一个范围的两个整数 **L** 和 **R** ，任务是当在范围 **L 到 R** 中选择一个随机数时，找到得到一个[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)数的[概率](https://www.geeksforgeeks.org/engineering-mathematics-tutorials/)。
**举例:**

> **输入:** L = 6，R = 20
> **输出:** 0.133333
> **解释:**
> 范围内的完美方块【6，20】= { 9，16} = > 2 完美方块
> 范围内的总数【6，20】= 15
> 概率= 2 / 15 = 0.133333
> **输入:** L = 16

**方法:**这个问题的关键观察是从 0 到一个数范围内的完美平方的计数可以用给定的公式计算:

> //0 到 N 范围内的完美正方形的计数为
> 完美正方形的计数=地板(sqrt(N))

类似地，在给定范围内的完美正方形的计数可以借助于上述公式计算如下:

> 完美正方形的计数[L，R] =地板(sqrt(R))–天花板(sqrt(L)) + 1
> 范围内的总数= R–L+1
> ![\text{Probability of getting perfect square} =\frac{floor(sqrt(R)) - ceil(sqrt(L)) + 1}{R - L + 1}  ](img/9bff7a08b4343e35d8737bfe4caba920.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// probability of getting a
// perfect square number

#include <bits/stdc++.h>
using namespace std;

// Function to return the probability
// of getting a perfect square
// number in a range
float findProb(int l, int r)
{
    // Count of perfect squares
    float countOfPS = floor(sqrt(r)) - ceil(sqrt(l)) + 1;

    // Total numbers in range l to r
    float total = r - l + 1;

    // Calculating probability
    float prob = (float)countOfPS / (float)total;
    return prob;
}

// Driver Code
int main()
{
    int L = 16, R = 25;
    cout << findProb(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// probability of getting a
// perfect square number

class GFG{

// Function to return the probability
// of getting a perfect square
// number in a range
static float findProb(int l, int r)
{

    // Count of perfect squares
    float countOfPS = (float) (Math.floor(Math.sqrt(r)) -
                               Math.ceil(Math.sqrt(l)) + 1);

    // Total numbers in range l to r
    float total = r - l + 1;

    // Calculating probability
    float prob = (float)countOfPS / (float)total;
    return prob;
}

// Driver Code
public static void main(String[] args)
{
    int L = 16, R = 25;
    System.out.print(findProb(L, R));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to find 
# the probability of getting a
# perfect square number
import math

# Function to return the probability
# of getting a perfect square
# number in a range
def findProb(l, r):

    # Count of perfect squares
    countOfPS = (math.floor(math.sqrt(r)) -
                  math.ceil(math.sqrt(l)) + 1)

    # Total numbers in range l to r
    total = r - l + 1

    # Calculating probability
    prob = countOfPS / total

    return prob

# Driver code
if __name__=='__main__':

    L = 16
    R = 25

    print(findProb(L, R))

# This code is contributed by rutvik_56   
```

## C#

```
// C# implementation to find the probability
// of getting a perfect square number
using System;

class GFG{

// Function to return the probability
// of getting a perfect square
// number in a range
static float findProb(int l, int r)
{

    // Count of perfect squares
    float countOfPS = (float)(Math.Floor(Math.Sqrt(r)) -
                            Math.Ceiling(Math.Sqrt(l)) + 1);

    // Total numbers in range l to r
    float total = r - l + 1;

    // Calculating probability
    float prob = (float)countOfPS / (float)total;
    return prob;
}

// Driver Code
public static void Main(String[] args)
{
    int L = 16, R = 25;

    Console.Write(findProb(L, R));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// probability of getting a
// perfect square number

// Function to return the probability
// of getting a perfect square
// number in a range
function findProb(l, r)
{

    // Count of perfect squares
    var countOfPS = (Math.floor(Math.sqrt(r)) -
                     Math.ceil(Math.sqrt(l)) + 1);

    // Total numbers in range l to r
    var total = r - l + 1;

    // Calculating probability
    var prob = countOfPS / total;
    return prob;
}

// Driver code
var L = 16, R = 25;

// Function Call
document.write(findProb(L, R));

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
0.2
```

***时间复杂度:** O(1)*
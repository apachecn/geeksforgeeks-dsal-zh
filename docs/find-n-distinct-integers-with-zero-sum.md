# 求 N 个不同的零和整数

> 原文:[https://www . geesforgeks . org/find-n-distinct-整数带零和/](https://www.geeksforgeeks.org/find-n-distinct-integers-with-zero-sum/)

给定一个**整数 N** ，我们的任务是打印 **N** 个不同的数字，使得它们的和为 0。
**例:**

> **输入:** N = 3
> **输出:** 1，-1，0
> **说明:**
> 将 1 + (-1) + 0 的数字相加，和为 0。
> **输入:** N = 4
> **输出:** 1，-1，2，-2
> **说明:**
> 在加 1 + (-1) + 2 + (-2)的数时，和为 0。

**方法:**解决上述问题的主要思路是将 [**对称对**](https://www.geeksforgeeks.org/given-an-array-of-pairs-find-all-symmetric-pairs-in-it/) 像(+x，-x)一样打印出来，这样和永远为 0。问题的边缘情况是观察到如果**整数 N 为奇数**，则随数字一起打印一个 0，这样总和不受影响。
以下是上述方法的实施:

## C++

```
// C++ implementation to Print N distinct
// numbers such that their sum is 0

#include <bits/stdc++.h>
using namespace std;

// Function to print distinct n
// numbers such that their sum is 0
void findNumbers(int N)
{
    for (int i = 1; i <= N / 2; i++) {

        // Print 2 symmetric numbers
        cout << i << ", " << -i << ", ";
    }

    // print a extra 0 if N is odd
    if (N % 2 == 1)
        cout << 0;
}

// Driver code
int main()
{
    int N = 10;

    findNumbers(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Print N distinct
// numbers such that their sum is 0

class GFG{

// Function to print distinct n
// numbers such that their sum is 0
static void findNumbers(int N)
{
    for (int i = 1; i <= N / 2; i++)
    {
        // Print 2 symmetric numbers
        System.out.print(i + ", " + -i + ", ");
    }

    // Print a extra 0 if N is odd
    if (N % 2 == 1)
        System.out.print(0);
}

// Driver code
public static void main(String[] args)
{
    int N = 10;
    findNumbers(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to print N distinct
# numbers such that their sum is 0

# Function to print distinct n
# numbers such that their sum is 0
def findNumbers(N):

    for i in range(1, N // 2 + 1):

        # Print 2 symmetric numbers
        print(i, end = ', ')
        print(-i, end = ', ')

    # Print a extra 0 if N is odd
    if N % 2 == 1:
        print(0, end = '')

# Driver code
if __name__=='__main__':

    N = 10
    findNumbers(N)

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation to print N distinct
// numbers such that their sum is 0
using System;

class GFG {

// Function to print distinct n
// numbers such that their sum is 0
static void findNumbers(int N)
{
    for(int i = 1; i <= (N / 2); i++)
    {

       // Print 2 symmetric numbers
       Console.Write(i + ", " + -i + ", ");
    }

    // Print a extra 0 if N is odd
    if (N % 2 == 1)
        Console.Write(0);
}

// Driver code
static void Main()
{
    int N = 10;

    findNumbers(N);
}
}

// This code is contributed by divyeshrabadiya07   
```

## java 描述语言

```
<script>

// Javascript implementation to Print N distinct
// numbers such that their sum is 0

// Function to print distinct n
// numbers such that their sum is 0
function findNumbers(N)
{
    for (var i = 1; i <= N / 2; i++) {

        // Print 2 symmetric numbers
        document.write( i + ", " + -i + ", ");
    }

    // print a extra 0 if N is odd
    if (N % 2 == 1)
        document.write( 0);
}

// Driver code
var N = 10;
findNumbers(N);

</script>
```

**Output:** 

```
1, -1, 2, -2, 3, -3, 4, -4, 5, -5,
```

***时间复杂度:**O(N)*T4】
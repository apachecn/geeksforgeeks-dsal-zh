# 找到修改后的斐波那契数列的第 n 个元素

> 原文:[https://www . geeksforgeeks . org/find-修改后的斐波那契数列的第 n 个元素/](https://www.geeksforgeeks.org/find-the-nth-element-of-the-modified-fibonacci-series/)

给定两个整数 **A** 和 **B** ，这是级数的前两项，另一个整数 **N** 。任务是使用斐波那契规则找到 **N <sup>第</sup>** 个数字，即**fib(I)= fib(I–1)+fib(I–2)**
**例:**

> **输入:** A = 2，B = 3，N = 4
> **输出:** 8
> 级数为 2，3，5，8，13，21，…
> 第 4 个元素为 8。
> **输入:** A = 5，B = 7，N = 10
> **输出:** 343

**方法:**初始化变量 **sum = 0** ，存储前两个值的总和。现在，运行从 **i = 2 到 N** 的循环，对于每个索引更新值 **sum = A + B** 和 **A = B，B = sum** 。最后，返回所需的**第 n 个元素**的总和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the Nth number of
// the modified Fibonacci series where
// A and B are the first two terms
int findNthNumber(int A, int B, int N)
{

    // To store the current element which
    // is the sum of previous two
    // elements of the series
    int sum = 0;

    // This loop will terminate when
    // the Nth element is found
    for (int i = 2; i < N; i++) {
        sum = A + B;

        A = B;

        B = sum;
    }

    // Return the Nth element
    return sum;
}

// Driver code
int main()
{
    int A = 5, B = 7, N = 10;

    cout << findNthNumber(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the Nth number of
    // the modified Fibonacci series where
    // A and B are the first two terms
    static int findNthNumber(int A, int B, int N)
    {

        // To store the current element which
        // is the sum of previous two
        // elements of the series
        int sum = 0;

        // This loop will terminate when
        // the Nth element is found
        for (int i = 2; i < N; i++)
        {
            sum = A + B;

            A = B;

            B = sum;
        }

        // Return the Nth element
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int A = 5, B = 7, N = 10;

        System.out.println(findNthNumber(A, B, N));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the Nth number of
# the modified Fibonacci series where
# A and B are the first two terms
def findNthNumber(A, B, N):

    # To store the current element which
    # is the sum of previous two
    # elements of the series
    sum = 0

    # This loop will terminate when
    # the Nth element is found
    for i in range(2, N):
        sum = A + B

        A = B

        B = sum

    # Return the Nth element
    return sum

# Driver code
if __name__ == '__main__':
    A = 5
    B = 7
    N = 10

    print(findNthNumber(A, B, N))

# This code is contributed by Ashutosh450
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the Nth number of
    // the modified Fibonacci series where
    // A and B are the first two terms
    static int findNthNumber(int A, int B, int N)
    {

        // To store the current element which
        // is the sum of previous two
        // elements of the series
        int sum = 0;

        // This loop will terminate when
        // the Nth element is found
        for (int i = 2; i < N; i++)
        {
            sum = A + B;

            A = B;

            B = sum;
        }

        // Return the Nth element
        return sum;
    }

    // Driver code
    public static void Main()
    {
        int A = 5, B = 7, N = 10;

        Console.WriteLine(findNthNumber(A, B, N));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// javascript implementation of the approach

    // Function to return the Nth number of
    // the modified Fibonacci series where
    // A and B are the first two terms
    function findNthNumber(A , B , N) {

        // To store the current element which
        // is the sum of previous two
        // elements of the series
        var sum = 0;

        // This loop will terminate when
        // the Nth element is found
        for (i = 2; i < N; i++) {
            sum = A + B;

            A = B;

            B = sum;
        }

        // Return the Nth element
        return sum;
    }

    // Driver code

        var A = 5, B = 7, N = 10;

        document.write(findNthNumber(A, B, N));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
343
```
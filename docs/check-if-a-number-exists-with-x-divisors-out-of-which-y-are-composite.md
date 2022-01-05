# 检查一个数是否存在 X 除数，其中 Y 是复合的

> 原文:[https://www . geesforgeks . org/check-if-a-number-exists-with-x-dividers-out-y-of-y-composite/](https://www.geeksforgeeks.org/check-if-a-number-exists-with-x-divisors-out-of-which-y-are-composite/)

给定两个整数 **X** 和 **Y** 分别代表除数总数和复合除数，任务是检查是否存在一个整数 **N** ，它正好有 **X** 除数和 **Y** 是复合数。

**示例:**

> **输入:** X = 6，Y = 3
> **输出:** YES
> **说明:**
> N = 18 就是这样一个数字。
> 18 的除数是 1、2、3、6、9 和 18。
> 18 的复合因子是 6、9 和 18。
> **输入:** X = 7，Y = 3
> **输出:** NO
> **解释:**
> 我们看到不存在有 7 个正除数的数，其中 3 个是复合除数。

**进场:**

1.  首先计算一个数的质因数，等于:

**素数除数=除数总数–复合除数–1**

1.  所以，质因数的个数，**C**=**X**–**Y–1**

2.  因为每个数都有 1 作为因子，而 1 既不是质数也不是合数，所以我们不得不把它排除在质因数之外。

3.  如果复合除数的个数小于质因数的个数，那么根本不可能找到这样一个数。

4.  所以如果 **X** 的素因子分解至少包含 **C** 个不同的整数，那么一个解决方案是可能的。否则，我们无法找到满足给定条件的数字 **N** 。

5.  求 **X** 可以分解成的最大值个数，使得每个值都大于 **1** 。换句话说，我们可以找出 **X** 的素因子分解。
6.  如果素数因子分解的项数大于或等于 **C** ，那么这样的数是可能的。

以下是上述方法的实现:

## C++

```
// C++ program to check if a number
// exists having exactly X positive
// divisors out of which Y are
// composite divisors
#include <bits/stdc++.h>
using namespace std;

int factorize(int N)
{
    int count = 0;
    int cnt = 0;

    // Count the number of
    // times 2 divides N
    while ((N % 2) == 0) {
        N = N / 2;
        count++;
    }

    cnt = cnt + count;

    // check for all possible
    // numbers that can divide it
    for (int i = 3; i <= sqrt(N); i += 2) {
        count = 0;
        while (N % i == 0) {
            count++;
            N = N / i;
        }
        cnt = cnt + count;
    }

    // if N at the end
    // is a prime number.
    if (N > 2)
        cnt = cnt + 1;
    return cnt;
}

// Function to check if any
// such number exists
void ifNumberExists(int X, int Y)
{
    int C, dsum;

    C = X - Y - 1;
    dsum = factorize(X);
    if (dsum >= C)
        cout << "YES \n";
    else
        cout << "NO \n";
}

// Driver Code
int main()
{

    int X, Y;
    X = 6;
    Y = 4;

    ifNumberExists(X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number
// exists having exactly X positive
// divisors out of which Y are
// composite divisors
import java.lang.Math;
class GFG{

public static int factorize(int N)
{
    int count = 0;
    int cnt = 0;

    // Count the number of
    // times 2 divides N
    while ((N % 2) == 0)
    {
        N = N / 2;
        count++;
    }

    cnt = cnt + count;

    // Check for all possible
    // numbers that can divide it
    for(int i = 3; i <= Math.sqrt(N); i += 2)
    {
       count = 0;
       while (N % i == 0)
       {
           count++;
           N = N / i;
       }
       cnt = cnt + count;
    }

    // If N at the end
    // is a prime number.
    if (N > 2)
        cnt = cnt + 1;
    return cnt;
}

// Function to check if any
// such number exists
public static void ifNumberExists(int X, int Y)
{
    int C, dsum;
    C = X - Y - 1;
    dsum = factorize(X);

    if (dsum >= C)
        System.out.println("YES");
    else
        System.out.println("NO");
}

// Driver code   
public static void main(String[] args)
{
    int X, Y;
    X = 6;
    Y = 4;

    ifNumberExists(X, Y);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to check if a number exists
# having exactly X positive divisors out of
#  which Y are composite divisors
import math

def factorize(N):

    count = 0
    cnt = 0

    # Count the number of
    # times 2 divides N
    while ((N % 2) == 0):
        N = N // 2
        count+=1

    cnt = cnt + count

    # Check for all possible
    # numbers that can divide it
    sq = int(math.sqrt(N))
    for i in range(3, sq, 2):
        count = 0

        while (N % i == 0):
            count += 1
            N = N // i

        cnt = cnt + count

    # If N at the end
    # is a prime number.
    if (N > 2):
        cnt = cnt + 1
    return cnt

# Function to check if any
# such number exists
def ifNumberExists(X, Y):

    C = X - Y - 1
    dsum = factorize(X)

    if (dsum >= C):
        print ("YES")
    else:
        print("NO")

# Driver Code
if __name__ == "__main__":

    X = 6
    Y = 4

    ifNumberExists(X, Y)

# This code is contributed by chitranayal
```

## C#

```
// C# program to check if a number
// exists having exactly X positive
// divisors out of which Y are
// composite divisors
using System;
class GFG{

public static int factorize(int N)
{
    int count = 0;
    int cnt = 0;

    // Count the number of
    // times 2 divides N
    while ((N % 2) == 0)
    {
        N = N / 2;
        count++;
    }

    cnt = cnt + count;

    // Check for all possible
    // numbers that can divide it
    for(int i = 3; i <= Math.Sqrt(N); i += 2)
    {
        count = 0;
        while (N % i == 0)
        {
            count++;
            N = N / i;
        }
        cnt = cnt + count;
    }

    // If N at the end
    // is a prime number.
    if (N > 2)
        cnt = cnt + 1;
    return cnt;
}

// Function to check if any
// such number exists
public static void ifNumberExists(int X, int Y)
{
    int C, dsum;
    C = X - Y - 1;
    dsum = factorize(X);

    if (dsum >= C)
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}

// Driver code
public static void Main(string[] args)
{
    int X, Y;
    X = 6;
    Y = 4;

    ifNumberExists(X, Y);
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript program to check if a number
// exists having exactly X positive
// divisors out of which Y are
// composite divisors

    function factorize(N) {
        var count = 0;
        var cnt = 0;

        // Count the number of
        // times 2 divides N
        while ((N % 2) == 0) {
            N = N / 2;
            count++;
        }

        cnt = cnt + count;

        // Check for all possible
        // numbers that can divide it
        for (i = 3; i <= Math.sqrt(N); i += 2) {
            count = 0;
            while (N % i == 0) {
                count++;
                N = N / i;
            }
            cnt = cnt + count;
        }

        // If N at the end
        // is a prime number.
        if (N > 2)
            cnt = cnt + 1;
        return cnt;
    }

    // Function to check if any
    // such number exists
    function ifNumberExists(X , Y) {
        var C, dsum;
        C = X - Y - 1;
        dsum = factorize(X);

        if (dsum >= C)
            document.write("YES");
        else
            document.write("NO");
    }

    // Driver code

        var X, Y;
        X = 6;
        Y = 4;

        ifNumberExists(X, Y);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N<sup>1/2</sup>)*
***辅助空间:** O (1)*
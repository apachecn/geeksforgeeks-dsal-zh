# 通过乘以 2 或除以 6 将最小移动次数减少到 1

> 原文:[https://www . geeksforgeeks . org/将最小移动次数减少到 1 次乘以 2 或除以 6/](https://www.geeksforgeeks.org/reduce-n-to-1-in-minimum-moves-by-either-multiplying-by-2-or-dividing-by-6/)

给定一个整数 **N** ，通过以下两个运算找到将 **N 减少到 1** 的最小运算次数:

*   N 乘以 2
*   如果 N 能被 6 整除，用 6 除 N

如果 N 不能减为 1，打印 **-1** 。

**示例:**

> ***输入:** N = 54*
> ***输出:** 5*
> ***解释:**执行以下操作**–***
> 
> *   *N 除以 6，得到 n = 9*
> *   *将 N 乘以 2，得到 n = 18*
> *   *N 除以 6，得到 n = 3*
> *   *将 N 乘以 2，得到 n = 6*
> *   *将 N 除以 6 得到 n = 1*
> 
> *因此，至少需要进行 5 次操作才能将 54 减少到 1*
> 
> ***输入:** N = 12*
> ***输出:** -1*

**方法:**任务可以通过以下观察来解决。

*   如果数字由除 **2** 和 **3** 之外的素数组成，那么答案是 **-1** ，因为 **N** 不能通过上述操作减为 1。
*   否则，让**数 2** 为 n 的**因式**中的**二**数，让**数 3** 为 n 的**因式**中的**三**数。
    *   如果**数 2 >数 3** 那么答案就是 **-1** 因为我们不能把两个都去掉。
    *   否则，答案是**(count 3-count 2)+count 3**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of moves to reduce N to 1
void minOperations(int N)
{
    int count2 = 0, count3 = 0;

    // Number of 2's in the
    // factorization of N
    while (N % 2 == 0) {
        N = N / 2;
        count2++;
    }

    // Number of 3's in the
    // factorization of n
    while (N % 3 == 0) {
        N = N / 3;
        count3++;
    }

    if (N == 1 && (count2 <= count3)) {
        cout << (2 * count3) - count2;
    }

    // If number of 2's are greater
    // than number of 3's or
    // prime factorization of N contains
    // primes other than 2 or 3
    else {
        cout << -1;
    }
}

// Driver Code
int main()
{
    int N = 54;
    minOperations(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum number
// of moves to reduce N to 1
static void minOperations(int N)
{
    int count2 = 0, count3 = 0;

    // Number of 2's in the
    // factorization of N
    while (N % 2 == 0) {
        N = N / 2;
        count2++;
    }

    // Number of 3's in the
    // factorization of n
    while (N % 3 == 0) {
        N = N / 3;
        count3++;
    }

    if (N == 1 && (count2 <= count3)) {
        System.out.print((2 * count3) - count2);
    }

    // If number of 2's are greater
    // than number of 3's or
    // prime factorization of N contains
    // primes other than 2 or 3
    else {
        System.out.print(-1);
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 54;
    minOperations(N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the minimum number
# of moves to reduce N to 1
def minOperations(N):

    count2 = 0
    count3 = 0

    # Number of 2's in the
    # factorization of N
    while (N % 2 == 0):
        N = N // 2
        count2 += 1

        # Number of 3's in the
        # factorization of n
    while (N % 3 == 0):
        N = N // 3
        count3 += 1

    if (N == 1 and (count2 <= count3)):
        print((2 * count3) - count2)

        # If number of 2's are greater
        # than number of 3's or
        # prime factorization of N contains
        # primes other than 2 or 3
    else:
        print(-1)

# Driver Code
if __name__ == "__main__":

    N = 54
    minOperations(N)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the minimum number
    // of moves to reduce N to 1
    static void minOperations(int N)
    {
        int count2 = 0, count3 = 0;

        // Number of 2's in the
        // factorization of N
        while (N % 2 == 0) {
            N = N / 2;
            count2++;
        }

        // Number of 3's in the
        // factorization of n
        while (N % 3 == 0) {
            N = N / 3;
            count3++;
        }

        if (N == 1 && (count2 <= count3)) {
            Console.WriteLine((2 * count3) - count2);
        }

        // If number of 2's are greater
        // than number of 3's or
        // prime factorization of N contains
        // primes other than 2 or 3
        else {
            Console.WriteLine(-1);
        }
    }

    // Driver Code
    public static void Main()
    {
        int N = 54;
        minOperations(N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum number
// of moves to reduce N to 1
function minOperations(N)
{
    let count2 = 0, count3 = 0;

    // Number of 2's in the
    // factorization of N
    while (N % 2 == 0)
    {
        N = Math.floor(N / 2);
        count2++;
    }

    // Number of 3's in the
    // factorization of n
    while (N % 3 == 0)
    {
        N = Math.floor(N / 3);
        count3++;
    }

    if (N == 1 && (count2 <= count3))
    {
        document.write((2 * count3) - count2);
    }

    // If number of 2's are greater
    // than number of 3's or prime
    // factorization of N contains
    // primes other than 2 or 3
    else
    {
        document.write(-1);
    }
}

// Driver Code
let N = 54;

minOperations(N);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
5
```

***时间复杂度:** O(logN)*
***辅助空间:** O(1)*
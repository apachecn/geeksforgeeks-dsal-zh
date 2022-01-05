# 找出一对有差异 K 的连续完美正方形

> 原文:[https://www . geeksforgeeks . org/find-一对连续的有差异的完美正方形-k/](https://www.geeksforgeeks.org/find-pair-of-consecutive-perfect-squares-with-difference-k/)

给定一个整数 **K** ，任务是找到两个连续的[完美方块](https://www.geeksforgeeks.org/find-number-perfect-squares-two-given-numbers/)，其差为 **K** 。如果不存在这样的数字对，则打印 **-1** 。

**示例:**

> **输入:** K = 5
> **输出:** 4 9
> **解释** :
> 所以，4 和 9 是相差 5(= 9–4 = 5)的两个完美正方形。
> 
> **输入:** K = 4
> **输出:** -1

**天真法:**解决给定问题的简单方法是遍历所有的完美正方形，检查是否有 2 个这样的数字，它们的差是 **K** ，如果发现是真的，那么打印那些对。否则，打印 **-1** 。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**有效方法:**上述方法也可以通过观察连续完美正方形之间的差异来优化，如下所示:

> **完美方块:**1 4 9 16 25…
> T3】连续差: 3 5 7 9 …

从上面的观察来看，连续的完美正方形之间的差在[连续奇数](https://www.geeksforgeeks.org/three-times-the-first-of-three-consecutive-odd-integers-is-3-more-than-twice-the-third-what-is-the-third-integer/)的顺序。因此，当差为偶数时，则不存在这样的数对，遂打印 **"-1"** 。否则，两个数由 **(K/2) <sup>2</sup>** 和 **((K + 1)/2) <sup>2</sup>** 给出。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find two consecutive
// perfect square numbers whose
// difference is N
void findPrimeNumbers(int N)
{
    int a, b;
    a = (N / 2) * (N / 2);
    b = ((N + 1) / 2) * ((N + 1) / 2);

    if ((N % 2) == 0)
        cout << "-1";
    else
        cout << a << " " << b;
}

// Driver Code
int main()
{
    int K = 5;
    findPrimeNumbers(K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to find two consecutive
    // perfect square numbers whose
    // difference is N
    static void findPrimeNumbers(int N)
    {
        int a, b;
        a = (N / 2) * (N / 2);
        b = ((N + 1) / 2) * ((N + 1) / 2);

        if ((N % 2) == 0)
            System.out.println("-1");
        else
            System.out.println(a + " " + b);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int K = 5;
        findPrimeNumbers(K);
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find two consecutive
# perfect square numbers whose
# difference is N
def findPrimeNumbers(N):
    a = (N // 2) * (N // 2)
    b = ((N + 1) // 2) * ((N + 1) // 2)

    if ((N % 2) == 0):
        print("-1")
    else:
        print(a, end=" ")
        print(b)

# Driver Code
if __name__ == "__main__":
    K = 5
    findPrimeNumbers(K)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to find two consecutive
    // perfect square numbers whose
    // difference is N
    static void findPrimeNumbers(int N)
    {
        int a, b;
        a = (N / 2) * (N / 2);
        b = ((N + 1) / 2) * ((N + 1) / 2);

        if ((N % 2) == 0)
            Console.WriteLine("-1");
        else
            Console.WriteLine(a + " " + b);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int K = 5;
        findPrimeNumbers(K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find two consecutive
// perfect square numbers whose
// difference is N
function findPrimeNumbers(N)
{
    let a, b;
    a = Math.floor(N / 2) *
        Math.floor(N / 2);
    b = Math.floor((N + 1) / 2) *
        Math.floor((N + 1) / 2);

    if ((N % 2) == 0)
        document.write("-1");
    else
        document.write(a + " " + b);
}

// Driver Code
let K = 5;

findPrimeNumbers(K);

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
4 9
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)
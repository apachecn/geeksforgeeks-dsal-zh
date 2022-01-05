# 按照给定条件

生成数组元素

> 原文:[https://www . geesforgeks . org/generate-elements-of-of-the-array-following-conditions/](https://www.geeksforgeeks.org/generate-elements-of-the-array-following-given-conditions/)

给定一个整数 N，对于范围 **2** 到 **N** 中的每一个整数 **i** ，分配一个正整数![a_i  ](img/a772f049c27678fdffa36f43172a6f1e.png "Rendered by QuickLaTeX.com")，使得以下条件成立:

*   对于任何一对指数 **(i，j)** ，如果 **i** 和 **j** 是[互质](https://en.wikipedia.org/wiki/Coprime_integers)那么![a_i \neq a_j  ](img/b7c884cfc1deee7cca65c599a26a5a3d.png "Rendered by QuickLaTeX.com")。
*   所有![a_i  ](img/a772f049c27678fdffa36f43172a6f1e.png "Rendered by QuickLaTeX.com")的最大值应最小化(即最大值应尽可能小)。

**如果一对整数的 gcd(i，j) = 1，则称其为互质。**
**例:**

> **输入:** N = 4
> **输出:** 1 2 1
> **输入:** N = 10
> **输出:** 1 2 1 3 2 4 1 2 3

**方法:**在给从 **2** 到 **n** 的指数赋值时，我们必须记住两件事。首先，对于任何一对 **(i，j)** ，如果 **i** 和 **j** 是互质的，那么我们不能给这对指数分配相同的值。第二，我们要把分配给每个指标的最大值从 **2** 降到 **n** 。
如果给每个素数分配不同的数，这是可以实现的，因为所有素数都是互质的。然后在所有复合位置赋值，使其与任何质因数相同。这种解决方案适用于任何一对 **(i，j)** ， **i** 被赋予相同的除数， **j** 也被赋予相同的除数，因此如果它们是互质的，它们就不能被赋予相同的数。
这种方式可以通过在搭建厄拉多塞的[筛时做一个小改动来实现。
当我们第一次遇到一个素数时，然后给它和它的所有倍数赋一个唯一的最小值。这样，所有的质数指数都应该有唯一的值，所有的合成指数的值都和它的任何质数一样。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate the required array
void specialSieve(int n)
{

    // Initialize cnt variable for assigning
    // unique value to prime and its multiples
    int cnt = 0;
    int prime[n + 1];

    for (int i = 0; i <= n; i++)
        prime[i] = 0;

    for (int i = 2; i <= n; i++) {

        // When we get a prime for the first time
        // then assign a unique smallest value to
        // it and all of its multiples
        if (!prime[i]) {
            cnt++;
            for (int j = i; j <= n; j += i)
                prime[j] = cnt;
        }
    }

    // Print the generated array
    for (int i = 2; i <= n; i++)
        cout << prime[i] << " ";
}

// Driver code
int main()
{
    int n = 6;

    specialSieve(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to generate the required array
static void specialSieve(int n)
{

    // Initialize cnt variable for assigning
    // unique value to prime and its multiples
    int cnt = 0;
    int prime[] = new int[n+1];

    for (int i = 0; i <= n; i++)
        prime[i] = 0;

    for (int i = 2; i <= n; i++)
    {

        // When we get a prime for the first time
        // then assign a unique smallest value to
        // it and all of its multiples
        if (!(prime[i]>0))
        {
            cnt++;
            for (int j = i; j <= n; j += i)
                prime[j] = cnt;
        }
    }

    // Print the generated array
    for (int i = 2; i <= n; i++)
        System.out.print(prime[i] + " ");
}

// Driver code
public static void main (String[] args)
{
    int n = 6;

specialSieve(n);

}
}

// This code is contrubuted by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to generate the required array
def specialSieve(n) :

    # Initialize cnt variable for assigning
    # unique value to prime and its multiples
    cnt = 0;
    prime = [0]*(n + 1);

    for i in range(2, n + 1) :

        # When we get a prime for the first time
        # then assign a unique smallest value to
        # it and all of its multiples
        if (not prime[i]) :
            cnt += 1;
            for j in range(i, n + 1, i) :
                prime[j] = cnt;

    # Print the generated array
    for i in range(2, n + 1) :
        print(prime[i],end = " ");

# Driver code
if __name__ == "__main__" :

    n = 6;
    specialSieve(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to generate the required array
static void specialSieve(int n)
{

    // Initialize cnt variable for assigning
    // unique value to prime and its multiples
    int cnt = 0;
    int []prime = new int[n+1];

    for (int i = 0; i <= n; i++)
        prime[i] = 0;

    for (int i = 2; i <= n; i++)
    {

        // When we get a prime for the first time
        // then assign a unique smallest value to
        // it and all of its multiples
        if (!(prime[i] > 0))
        {
            cnt++;
            for (int j = i; j <= n; j += i)
                prime[j] = cnt;
        }
    }

    // Print the generated array
    for (int i = 2; i <= n; i++)
        Console.Write(prime[i] + " ");
}

// Driver code
public static void Main ()
{
    int n = 6;

    specialSieve(n);

}
}

// This code is contrubuted by anuj_67..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to generate the required array
function specialSieve(n)
{

    // Initialize cnt variable for assigning
    // unique value to prime and its multiples
    let cnt = 0;
    let prime = new Array(n + 1);

    for (let i = 0; i <= n; i++)
        prime[i] = 0;

    for (let i = 2; i <= n; i++) {

        // When we get a prime for the first time
        // then assign a unique smallest value to
        // it and all of its multiples
        if (!prime[i]) {
            cnt++;
            for (let j = i; j <= n; j += i)
                prime[j] = cnt;
        }
    }

    // Print the generated array
    for (let i = 2; i <= n; i++)
        document.write(prime[i] + " ");
}

// Driver code
    let n = 6;

    specialSieve(n);

</script>
```

**Output:** 

```
1 2 1 3 2
```

**时间复杂度:** O(N Log N)
# 求给定数的合成因子总数

> 原文:[https://www . geeksforgeeks . org/find-给定数字的综合因子总数/](https://www.geeksforgeeks.org/find-the-total-number-of-composite-factor-for-a-given-number/)

给定一个整数 **N** ，任务是求 **N** 的合成因子总数。一个数的复合因子是不是质数的因子。
**例:**

> **输入:** N = 24
> **输出:** 5
> 1、2、3、4、6、8、12、24 是 24 的因子。
> 其中只有 4、6、8、12、24 为复合材料。
> **输入:** N = 100
> **输出:** 6

**进场:**

*   找到 **N** 的所有因子，并将其存储在变量 **totalFactors** 中
*   找到 **N** 的所有质因数，并将其存储在变量**质因数**中
*   现在，总合成因子将是**总因子–质数因子–1**(减去 1，因为 1 既不是质数也不是合成数)。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of prime factors of n
int composite_factors(int n)
{
    int count = 0;
    int i, j;

    // Initialise array with 0
    int a[n + 1] = { 0 };
    for (i = 1; i <= n; ++i) {
        if (n % i == 0) {

            // Stored i value into an array
            a[i] = i;
        }
    }

    // Every non-zero value at a[i] denotes
    // that i is a factor of n
    for (i = 2; i <= n; i++) {
        j = 2;
        int p = 1;

        // Find if i is prime
        while (j < a[i]) {
            if (a[i] % j == 0) {
                p = 0;
                break;
            }
            j++;
        }

        // If i is a factor of n
        // and i is not prime
        if (p == 0 && a[i] != 0) {
            count++;
        }
    }

    return count;
}

// Driver code
int main()
{
    int n = 100;

    cout << composite_factors(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class Gfg
{

// Function to return the count
// of prime factors of n
public static int composite_factors(int n)
{
    int count = 0;
    int i, j;

    // Initialise array with 0
    int[] a=new int[n+1];
    for( i = 0; i < n; i++)
    {
        a[i]=0;
    }
    for (i = 1; i <= n; ++i)
    {
        if (n % i == 0)
        {

            // Stored i value into an array
            a[i] = i;
        }
    }

    // Every non-zero value at a[i] denotes
    // that i is a factor of n
    for (i = 2; i <= n; i++)
    {
        j = 2;
        int p = 1;

        // Find if i is prime
        while (j < a[i])
        {
            if (a[i] % j == 0)
            {
                p = 0;
                break;
            }
            j++;
        }

        // If i is a factor of n
        // and i is not prime
        if (p == 0 && a[i] != 0)
        {
            count++;
        }

}
    return count;
}

// Driver code
public static void main(String[] args)
{
    int n = 100;

    System.out.println(composite_factors(n));

}
}

// This code is contributed by nidhi16bcs2007
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of prime factors of n
def composite_factors(n) :

    count = 0;

    # Initialise array with 0
    a = [0]*(n + 1) ;

    for i in range(1, n + 1) :
        if (n % i == 0) :

            # Stored i value into an array
            a[i] = i;

    # Every non-zero value at a[i] denotes
    # that i is a factor of n
    for i in range(2,n + 1) :
        j = 2;
        p = 1;

        # Find if i is prime
        while (j < a[i]) :
            if (a[i] % j == 0) :
                p = 0;
                break;

            j += 1;

        # If i is a factor of n
        # and i is not prime
        if (p == 0 and a[i] != 0) :
            count += 1;

    return count;

# Driver code
if __name__ == "__main__" :

    n = 100;

    print(composite_factors(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count
// of prime factors of n
static int composite_factors(int n)
{
    int count = 0;
    int i, j;

    // Initialise array with 0
    int[] a = new int[n + 1];
    for( i = 0; i < n; i++)
    {
        a[i]=0;
    }
    for (i = 1; i <= n; ++i)
    {
        if (n % i == 0)
        {

            // Stored i value into an array
            a[i] = i;
        }
    }

    // Every non-zero value at a[i] denotes
    // that i is a factor of n
    for (i = 2; i <= n; i++)
    {
        j = 2;
        int p = 1;

        // Find if i is prime
        while (j < a[i])
        {
            if (a[i] % j == 0)
            {
                p = 0;
                break;
            }
            j+=1;
        }

        // If i is a factor of n
        // and i is not prime
        if (p == 0 && a[i] != 0)
        {
            count += 1;
        }

}
    return count;
}

// Driver code
public static void Main()
{
    int n = 100;

    Console.WriteLine(composite_factors(n));
}
}

// This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of prime factors of n
function composite_factors(n)
{
    var count = 0;
    var i, j;

    // Initialise array with 0
    var a = Array(n + 1).fill(0);
    for (i = 1; i <= n; ++i) {
        if (n % i == 0) {

            // Stored i value into an array
            a[i] = i;
        }
    }

    // Every non-zero value at a[i] denotes
    // that i is a factor of n
    for (i = 2; i <= n; i++) {
        j = 2;
        var p = 1;

        // Find if i is prime
        while (j < a[i]) {
            if (a[i] % j == 0) {
                p = 0;
                break;
            }
            j++;
        }

        // If i is a factor of n
        // and i is not prime
        if (p == 0 && a[i] != 0) {
            count++;
        }
    }

    return count;
}

// Driver code
    var n = 100;

    document.write(composite_factors(n));

</script>
```

**Output:** 

```
6
```
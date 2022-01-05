# 将(2 / N)表示为(1 / m)形式的三个不同正整数之和

> 原文:[https://www . geesforgeks . org/represent-2-n-as-sum-of-3-distinct-正整数-form-1-m/](https://www.geeksforgeeks.org/represent-2-n-as-the-sum-of-three-distinct-positive-integers-of-the-form-1-m/)

给定一个正整数 **N** ，任务是将分数 **2 / N** 表示为形式为 **1 / m** 的三个不同正整数之和，即 **(2 / N) = (1 / x) + (1 / y) + (1 / z)** ，并打印 **x** 、 **y** 和 **z** 。
**举例:**

> **输入:** N = 3
> **输出:**3 4 12
> (1/3)+(1/4)+(1/12)=((4+3+1)/12)
> =(8/12)=(2/3)即 2 / N
> **输入:** N = 28
> **输出:** 28 29 812

**进场:**很容易推断出对于 **N = 1** ，不会有解。对于 **N > 1** ， **(2 / N)** 可以表示为 **(1 / N) + (1 / N)** ，问题归结为表示为两个分数之和。现在，找出 **(1 / N)** 和 **1 / (N + 1)** 的区别，得到分数 **1 / (N * (N + 1))** 。因此，解决方案为**(2/N)=(1/N)+(1/(N+1))+(1/(N *(N+1)))**，其中 **x = N** ， **y = N + 1** ， **z = N * (N + 1)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required fractions
void find_numbers(int N)
{
    // Base condition
    if (N == 1) {
        cout << -1;
    }

    // For N > 1
    else {
        cout << N << " " << N + 1 << " "
             << N * (N + 1);
    }
}

// Driver code
int main()
{
    int N = 5;

    find_numbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find the required fractions
static void find_numbers(int N)
{
    // Base condition
    if (N == 1)
    {
        System.out.print(-1);
    }

    // For N > 1
    else
    {
        System.out.print(N + " " + (N + 1) +
                             " " + (N * (N + 1)));
    }
}

// Driver code
public static void main(String []args)
{
    int N = 5;

    find_numbers(N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the required fractions
def find_numbers(N) :

    # Base condition
    if (N == 1) :
        print(-1, end = "");

    # For N > 1
    else :
        print(N, N + 1 , N * (N + 1));

# Driver code
if __name__ == "__main__" :

    N = 5;

    find_numbers(N);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the required fractions
static void find_numbers(int N)
{
    // Base condition
    if (N == 1)
    {
        Console.Write(-1);
    }

    // For N > 1
    else
    {
        Console.Write(N + " " + (N + 1) +
                          " " + (N * (N + 1)));
    }
}

// Driver code
public static void Main(String []args)
{
    int N = 5;

    find_numbers(N);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to find the required fractions
    function find_numbers(N)
    {

        // Base condition
        if (N == 1) {
            document.write(-1);
        }

        // For N > 1
        else {
            document.write(N + " " + (N + 1) + " " + (N * (N + 1)));
        }
    }

    // Driver code
        var N = 5;
        find_numbers(N);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
5 6 30
```
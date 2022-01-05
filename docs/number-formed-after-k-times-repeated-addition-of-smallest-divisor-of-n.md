# N 的最小除数 K 次重复相加后形成的数

> 原文:[https://www . geesforgeks . org/number-formed-after-k-times-repeat-相加-n 的最小除数/](https://www.geeksforgeeks.org/number-formed-after-k-times-repeated-addition-of-smallest-divisor-of-n/)

给定两个整数 **N** 和 **K** ，任务是生成执行 **K** 操作的最终结果，该操作包括在每一步将 **N** 的当前值的*最小除数*相加，而不是 1。
**例:**

> **输入:** N = 9，K = 4
> **输出:** 18
> **说明:**
> 9 的除数为{1，3，9}
> 第 1 次运算:N = 9 + 3 = 12
> 第 2 次运算:N = 12 + 2 = 14
> 第 3 次运算:N = 14 + 2 = 16
> 第 4 次运算:N = 16 + 2 = 18
> **输入:【T11**

**天真法:**这个问题的蛮力法是执行 K 次运算，然后打印最后一个数字。
**高效方法:**这里的诀窍是，如果给定的 **N** 是 ***甚至*** ，则所有 **K** 运算的最小除数将始终为 2。因此，所需的第 K<sup>号将简单地为</sup> 

> 所需数量= **N + K * 2**

还有**如果 N 是奇数**，最小除数将是奇数。因此，将它们相加将产生一个偶数值(奇数+奇数=偶数)。因此，现在上述技巧可以应用于(K-1)操作，即

> 所需数=**N+N+的最小除数(K–1)* 2**

以下是上述方法的实现:

## C++

```
// C++ program to find the Kth number
// formed after repeated addition of
// smallest divisor of N
#include<bits/stdc++.h>
#include <cmath>
using namespace std;

void FindValue(int N, int K)
{

    // If N is even
    if( N % 2 == 0 )
    {
        N = N + 2 * K;
    }

    // If N is odd
    else
    {
        int i;

        for(i = 2; i < sqrt(N) + 1; i++)
        {
           if(N % i == 0)
              break;
        }

        // Add smallest divisor to N
        N = N + i;

        // Updated N is even
        N = N + 2 * ( K - 1 );
    }
    cout << N << endl;
}

// Driver code
int main()
{
    int N = 9;
    int K = 4;

    FindValue( N, K );
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Kth number
// formed after repeated addition of
// smallest divisor of N
import java.util.*;
class GFG{

static void FindValue(int N, int K)
{

    // If N is even
    if( N % 2 == 0 )
    {
        N = N + 2 * K;
    }

    // If N is odd
    else
    {
        int i;

        for(i = 2; i < Math.sqrt(N) + 1; i++)
        {
            if(N % i == 0)
                break;
        }

        // Add smallest divisor to N
        N = N + i;

        // Updated N is even
        N = N + 2 * ( K - 1 );
    }
    System.out.print(N);
}

// Driver code
public static void main(String args[])
{
    int N = 9;
    int K = 4;

    FindValue( N, K );
}
}

// This code is contributed by Nidhi_biet
```

## 蟒蛇 3

```
# Python3 program to find the
# Kth number formed after
# repeated addition of
# smallest divisor of N

import math

def FindValue(N, K):

    # If N is even
    if( N % 2 == 0 ):
        N = N + 2 * K

    # If N is odd
    else:

        # Find the smallest divisor
        for i in range( 2, (int)(math.sqrt(N))+1 ):
            if( N % i == 0):
                break

        # Add smallest divisor to N
        N = N + i

        # Updated N is even
        N = N + 2 * ( K - 1 )

    print(N)

# Driver code
if __name__ == "__main__":
    N = 9
    K = 4
    FindValue( N, K )
```

## C#

```
// C# program to find the Kth number
// formed after repeated addition of
// smallest divisor of N
using System;
class GFG{

static void FindValue(int N, int K)
{

    // If N is even
    if( N % 2 == 0 )
    {
        N = N + 2 * K;
    }

    // If N is odd
    else
    {
        int i;

        for(i = 2; i < Math.Sqrt(N) + 1; i++)
        {
            if(N % i == 0)
                break;
        }

        // Add smallest divisor to N
        N = N + i;

        // Updated N is even
        N = N + 2 * ( K - 1 );
    }
    Console.WriteLine(N);
}

// Driver code
public static void Main()
{
    int N = 9;
    int K = 4;

    FindValue( N, K );
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// JavaScript program to find the Kth number
// formed after repeated addition of
// smallest divisor of N
function FindValue(N, K)
{

    // If N is even
    if( N % 2 == 0 )
    {
        N = N + 2 * K;
    }

    // If N is odd
    else
    {
        let i;

        for(i = 2; i < Math.sqrt(N) + 1; i++)
        {
        if(N % i == 0)
            break;
        }

        // Add smallest divisor to N
        N = N + i;

        // Updated N is even
        N = N + 2 * ( K - 1 );
    }
    document.write(N + "<br>");
}

// Driver code
let N = 9;
let K = 4;

FindValue( N, K );

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
18
```

***时间复杂度:**O(√N)*T4】
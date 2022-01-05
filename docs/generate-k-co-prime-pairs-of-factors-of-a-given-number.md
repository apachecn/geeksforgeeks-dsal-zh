# 生成给定数目的 K 对同素因子

> 原文:[https://www . geeksforgeeks . org/generate-k-co-prime-对给定数字的因子/](https://www.geeksforgeeks.org/generate-k-co-prime-pairs-of-factors-of-a-given-number/)

给定两个整数 **N** 和 **K** ，任务是找到数量为 N 的 **K** 对因子，使得每对因子的 [**GCD**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 为 1。
**注:** **K** 同素因子对于给定的数
**总是存在的示例:**

> **输入:** N = 6，K = 1
> **输出:** 2 3
> **说明:**
> 因为 2 和 3 都是 6 的因子，gcd(2，3) = 1。
> **输入:** N = 120，K = 4
> **输出:**
> 2 3
> 3 4
> 3 5
> 4 5

**天真方法:**
最简单的方法是检查到 N 的所有数字，并检查这一对的 GCD 是否为 1。
***时间复杂度:**O(N<sup>2</sup>)*
***空间复杂度:** O(1)*
**线性逼近:**
[找到 **N** 的所有可能除数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)并存储在另一个数组中。遍历数组，从数组中搜索所有可能的互质对并打印它们。
***时间复杂度:** O(N)*
***空间复杂度:** O(N)*
**高效途径:**
按照以下步骤解决问题:

*   可以观察到，如果任意数的 GCD，比如说 **x** ，用 1 总是 1，即 **GCD(1，x) = 1** 。
*   由于 1 将始终是 **N** 的因子，因此只需将任何 **N** 的 **K** 因子打印为 1 作为[互质对](https://www.geeksforgeeks.org/find-number-co-prime-pairs-array/)。

下面是上述方法的实现。

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function prints the
// required pairs
void FindPairs(int n, int k)
{
    // First co-prime pair
    cout << 1 << " " << n << endl;

    // As a pair (1 n) has
    // already been Printed
    k--;

    for (long long i = 2;
         i <= sqrt(n); i++) {

        // If i is a factor of N
        if (n % i == 0) {

            cout << 1 << " "
                 << i << endl;
            k--;
            if (k == 0)
                break;

            // Since (i, i) won't form
            // a coprime pair
            if (i != n / i) {
                cout << 1 << " "
                     << n / i << endl;
                k--;
            }
            if (k == 0)
                break;
        }
    }
}

// Driver Code
int main()
{

    int N = 100;
    int K = 5;

    FindPairs(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;

class GFG{

// Function prints the
// required pairs
static void FindPairs(int n, int k)
{

    // First co-prime pair
    System.out.print(1 + " " + n + "\n");

    // As a pair (1 n) has
    // already been Printed
    k--;

    for(long i = 2; i <= Math.sqrt(n); i++)
    {

        // If i is a factor of N
        if (n % i == 0)
        {
            System.out.print(1 + " " + i + "\n");
            k--;
            if (k == 0)
                break;

            // Since (i, i) won't form
            // a coprime pair
            if (i != n / i)
            {
                System.out.print(1 + " " +
                             n / i + "\n");
                k--;
            }
            if (k == 0)
                break;
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 100;
    int K = 5;

    FindPairs(N, K);
}
}

// This code is contributed by princiraj1992
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
from math import sqrt

# Function prints the
# required pairs
def FindPairs(n, k):

    # First co-prime pair
    print(1, n)

    # As a pair (1 n) has
    # already been Printed
    k -= 1

    for i in range(2, int(sqrt(n)) + 1):

        # If i is a factor of N
        if(n % i == 0):
            print(1, i)

            k -= 1
            if(k == 0):
                break

            # Since (i, i) won't form
            # a coprime pair
            if(i != n // i):
                print(1, n // i)
                k -= 1

            if(k == 0):
                break

# Driver Code
if __name__ == '__main__':

    N = 100
    K = 5

    FindPairs(N, K)

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation of
// the above approach
using System;

class GFG{

// Function prints the
// required pairs
static void FindPairs(int n, int k)
{

    // First co-prime pair
    Console.Write(1 + " " + n + "\n");

    // As a pair (1 n) has
    // already been Printed
    k--;

    for(long i = 2; i <= Math.Sqrt(n); i++)
    {

        // If i is a factor of N
        if (n % i == 0)
        {
            Console.Write(1 + " " + i + "\n");
            k--;
            if (k == 0)
                break;

            // Since (i, i) won't form
            // a coprime pair
            if (i != n / i)
            {
                Console.Write(1 + " " +
                          n / i + "\n");
                k--;
            }
            if (k == 0)
                break;
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 100;
    int K = 5;

    FindPairs(N, K);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Function prints the
// required pairs
function FindPairs(n, k)
{
    // First co-prime pair
    document.write(1 + " " + n + "<br>");

    // As a pair (1 n) has
    // already been Printed
    k--;

    for (let i = 2;
        i <= Math.sqrt(n); i++) {

        // If i is a factor of N
        if (n % i == 0) {

            document.write( 1 + " "
                + i + "<br>");
            k--;
            if (k == 0)
                break;

            // Since (i, i) won't form
            // a coprime pair
            if (i != n / i) {
                document.write(1 + " "
                    + n / i + "<br>");
                k--;
            }
            if (k == 0)
                break;
        }
    }
}

// Driver Code

let N = 100;
let K = 5;

FindPairs(N, K);
// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
1 100
1 2
1 50
1 4
1 25
```

***时间复杂度:** O(sqrt(N))*
***辅助空间:** O(1)*
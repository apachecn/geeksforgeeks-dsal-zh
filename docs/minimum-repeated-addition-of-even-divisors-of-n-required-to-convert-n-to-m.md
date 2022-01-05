# 将 N 转换为 M 所需的 N 的偶数因子的最小重复加法

> 原文:[https://www . geeksforgeeks . org/最小重复加 n 的偶数因子将 n 转换为 m/](https://www.geeksforgeeks.org/minimum-repeated-addition-of-even-divisors-of-n-required-to-convert-n-to-m/)

给定两个数字 **N** 和 **M** ，任务是通过将其与除 **N** 之外的所有 **N** 的偶数因子重复相加，找到将 **N** 转换为 **M** 所需的最小运算。如果无法转换，打印 **-1** 。

**示例:**

> **输入:** N = 6，M = 24
> **输出:** 4
> **解释:**
> 第一步:加 2 (2 是偶数除数加 2！= 6)到 6。现在 N 变成了 8。
> 第二步:加 4 (4 是偶数除数，4！= 8)到 8。现在 N 变成了 12。
> 第三步:加 6 (6 是偶数除数，6！=12)到 12。现在 N 变成了 18。
> 第四步:加 6 (6 是偶数除数，6！=18)到 18。现在 N 变成 24 = m
> 因此，需要 4 个步骤。
> 
> **输入:** N = 9，M = 17
> **输出:** -1
> **说明:**
> 9 没有偶数除数可加，所以我们无法将 N 转换为 M

**天真法:**最简单的解决方法是考虑一个数的所有可能的偶[因子，递归地为它们计算答案，最后返回它的最小值。](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// INF is the maximum value
// which indicates Impossible state
const int INF = 1e7;

// Recursive Function that considers
// all possible even divisors of cur
int min_op(int cur, int M)
{
    // Indicates impossible state
    if (cur > M)
        return INF;

    // Return 0 if cur == M
    if (cur == M)
        return 0;

    // op stores the minimum operations
    // required to transform cur to M

    // Initially it is set to INF that
    // means we can't transform cur to M
    int op = INF;

    // Loop to find even divisors of cur
    for (int i = 2; i * i <= cur; i++) {

        // if i is divisor of cur
        if (cur % i == 0) {

            // if i is even
            if (i % 2 == 0) {

                // Finding divisors
                // recursively for cur+i
                op = min(op,
                         1 + min_op(cur + i, M));
            }

            // Check another divisor
            if ((cur / i) != i
                && (cur / i) % 2 == 0) {

                // Find recursively
                // for cur+(cur/i)
                op = min(
                    op,
                    1 + min_op(
                            cur + (cur / i),
                            M));
            }
        }
    }

    // Return the answer
    return op;
}

// Function that finds the minimum
// operation to reduce N to M
int min_operations(int N, int M)
{
    int op = min_op(N, M);

    // INF indicates impossible state
    if (op >= INF)
        cout << "-1";
    else
        cout << op << "\n";
}

// Driver Code
int main()
{
    // Given N and M
    int N = 6, M = 24;

    // Function Call
    min_operations(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// INF is the maximum value
// which indicates Impossible state
static int INF = (int) 1e7;

// Recursive Function that considers
// all possible even divisors of cur
static int min_op(int cur, int M)
{
    // Indicates impossible state
    if (cur > M)
        return INF;

    // Return 0 if cur == M
    if (cur == M)
        return 0;

    // op stores the minimum operations
    // required to transform cur to M

    // Initially it is set to INF that
    // means we can't transform cur to M
    int op = INF;

    // Loop to find even divisors of cur
    for (int i = 2; i * i <= cur; i++)
    {

        // if i is divisor of cur
        if (cur % i == 0)
        {

            // if i is even
            if (i % 2 == 0)
            {

                // Finding divisors
                // recursively for cur+i
                op = Math.min(op, 1 + min_op(cur + i, M));
            }

            // Check another divisor
            if ((cur / i) != i && (cur / i) % 2 == 0)
            {

                // Find recursively
                // for cur+(cur/i)
                op = Math.min(op, 1 + min_op(
                                cur + (cur / i), M));
            }
        }
    }

    // Return the answer
    return op;
}

// Function that finds the minimum
// operation to reduce N to M
static void min_operations(int N, int M)
{
    int op = min_op(N, M);

    // INF indicates impossible state
    if (op >= INF)
        System.out.print("-1");
    else
        System.out.print(op + "\n");
}

// Driver Code
public static void main(String[] args)
{
    // Given N and M
    int N = 6, M = 24;

    // Function Call
    min_operations(N, M);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# INF is the maximum value
# which indicates Impossible state
INF = int(1e7);

# Recursive Function that considers
# all possible even divisors of cur
def min_op(cur, M):

    # Indicates impossible state
    if (cur > M):
        return INF;

    # Return 0 if cur == M
    if (cur == M):
        return 0;

    # op stores the minimum operations
    # required to transform cur to M

    # Initially it is set to INF that
    # means we can't transform cur to M
    op = int(INF);

    # Loop to find even divisors of cur
    for i in range(2, int(cur ** 1 / 2) + 1):

        # If i is divisor of cur
        if (cur % i == 0):

            # If i is even
            if (i % 2 == 0):

                # Finding divisors
                # recursively for cur+i
                op = min(op, 1 + min_op(cur + i, M));

            # Check another divisor
            if ((cur / i) != i and
                (cur / i) % 2 == 0):

                # Find recursively
                # for cur+(cur/i)
                op = min(op, 1 + min_op(
                           cur + (cur // i), M));

    # Return the answer
    return op;

# Function that finds the minimum
# operation to reduce N to M
def min_operations(N, M):

    op = min_op(N, M);

    # INF indicates impossible state
    if (op >= INF):
        print("-1");
    else:
        print(op);

# Driver Code
if __name__ == '__main__':

    # Given N and M
    N = 6;
    M = 24;

    # Function call
    min_operations(N, M);

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // INF is the maximum value
    // which indicates Impossible state
    static int INF = (int)1e7;

    // Recursive Function that considers
    // all possible even divisors of cur
    static int min_op(int cur, int M)
    {
        // Indicates impossible state
        if (cur > M)
            return INF;

        // Return 0 if cur == M
        if (cur == M)
            return 0;

        // op stores the minimum operations
        // required to transform cur to M

        // Initially it is set to INF that
        // means we can't transform cur to M
        int op = INF;

        // Loop to find even divisors of cur
        for (int i = 2; i * i <= cur; i++)
        {

            // if i is divisor of cur
            if (cur % i == 0)
            {

                // if i is even
                if (i % 2 == 0)
                {

                    // Finding divisors
                    // recursively for cur+i
                    op = Math.Min(op,1 +
                                  min_op(cur + i, M));
                }

                // Check another divisor
                if ((cur / i) != i && (cur / i) % 2 == 0)
                {

                    // Find recursively
                    // for cur+(cur/i)
                    op = Math.Min(op, 1 +
                                  min_op(cur +
                                         (cur / i), M));
                }
            }
        }

        // Return the answer
        return op;
    }

    // Function that finds the minimum
    // operation to reduce N to M
    static void min_operations(int N, int M)
    {
        int op = min_op(N, M);

        // INF indicates impossible state
        if (op >= INF)
            Console.Write("-1");
        else
            Console.Write(op + "\n");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Given N and M
        int N = 6, M = 24;

        // Function Call
        min_operations(N, M);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// INF is the maximum value
// which indicates Impossible state
let INF = 1e7;

// Recursive Function that considers
// all possible even divisors of cur
function min_op(cur, M)
{
    // Indicates impossible state
    if (cur > M)
        return INF;

    // Return 0 if cur == M
    if (cur == M)
        return 0;

    // op stores the minimum operations
    // required to transform cur to M

    // Initially it is set to INF that
    // means we can't transform cur to M
    let op = INF;

    // Loop to find even divisors of cur
    for (let i = 2; i * i <= cur; i++)
    {

        // if i is divisor of cur
        if (cur % i == 0)
        {

            // if i is even
            if (i % 2 == 0)
            {

                // Finding divisors
                // recursively for cur+i
                op = Math.min(op, 1 + min_op(cur + i, M));
            }

            // Check another divisor
            if ((cur / i) != i && (cur / i) % 2 == 0)
            {

                // Find recursively
                // for cur+(cur/i)
                op = Math.min(op, 1 + min_op(
                                cur + (cur / i), M));
            }
        }
    }

    // Return the answer
    return op;
}

// Function that finds the minimum
// operation to reduce N to M
function min_operations(N, M)
{
    let op = min_op(N, M);

    // INF indicates impossible state
    if (op >= INF)
        document.write("-1");
    else
       document.write(op + "\n");
}

// Driver Code

         // Given N and M
    let N = 6, M = 24;

    // Function Call
    min_operations(N, M);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效法:**思路是利用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)将[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)状态存储在朴素法中，高效计算答案。按照以下步骤解决问题:

1.  为所有 **N≤i≤M** 初始化一个 [dp 表](https://www.geeksforgeeks.org/tabulation-vs-memoization/) **dp[i] = -1** 。
2.  考虑一个数的所有可能的偶数除数，并从中找出最小值。
3.  最后将结果存入 **dp[]** 返回答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// INF is the maximum value
// which indicates Impossible state
const int INF = 1e7;
const int max_size = 100007;

// Stores the dp states
int dp[max_size];

// Recursive Function that considers
// all possible even divisors of cur
int min_op(int cur, int M)
{
    // Indicates impossible state
    if (cur > M)
        return INF;

    if (cur == M)
        return 0;

    // Check dp[cur] is already
    // calculated or not
    if (dp[cur] != -1)
        return dp[cur];

    // op stores the minimum operations
    // required to transform cur to M

    // Initially it is set to INF that
    // meanswe cur can't be transform to M
    int op = INF;

    // Loop to find even divisors of cur
    for (int i = 2; i * i <= cur; i++) {

        // if i is divisor of cur
        if (cur % i == 0) {

            // if i is even
            if (i % 2 == 0) {

                // Find recursively
                // for cur+i
                op = min(op, 1 + min_op(cur + i, M));
            }

            // Check another divisor
            if ((cur / i) != i && (cur / i) % 2 == 0) {

                // Find recursively
                // for cur+(cur/i)
                op = min(op,
                         1 + min_op(cur + (cur / i), M));
            }
        }
    }

    // Finally store the current state
    // result and return the answer
    return dp[cur] = op;
}

// Function that counts the minimum
// operation to reduce N to M
int min_operations(int N, int M)
{
    // Initialise dp state
    for (int i = N; i <= M; i++) {
        dp[i] = -1;
    }

    // Function Call
    return min_op(N, M);
}

// Driver Code
int main()
{
    // Given N and M
    int N = 6, M = 24;

    // Function Call
    int op = min_operations(N, M);

    // INF indicates impossible state
    if (op >= INF)
        cout << "-1";
    else
        cout << op << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// INF is the maximum value
// which indicates Impossible state
static int INF = (int) 1e7;
static int max_size = 100007;

// Stores the dp states
static int []dp = new int[max_size];

// Recursive Function that considers
// all possible even divisors of cur
static int min_op(int cur, int M)
{

    // Indicates impossible state
    if (cur > M)
        return INF;

    if (cur == M)
        return 0;

    // Check dp[cur] is already
    // calculated or not
    if (dp[cur] != -1)
        return dp[cur];

    // op stores the minimum operations
    // required to transform cur to M

    // Initially it is set to INF that
    // meanswe cur can't be transform to M
    int op = INF;

    // Loop to find even divisors of cur
    for(int i = 2; i * i <= cur; i++)
    {

        // If i is divisor of cur
        if (cur % i == 0)
        {

            // If i is even
            if (i % 2 == 0)
            {

                // Find recursively
                // for cur+i
                op = Math.min(op,
                     1 + min_op(cur + i, M));
            }

            // Check another divisor
            if ((cur / i) != i &&
                (cur / i) % 2 == 0)
            {

                // Find recursively
                // for cur+(cur/i)
                op = Math.min(op,
                     1 + min_op(cur + (cur / i), M));
            }
        }
    }

    // Finally store the current state
    // result and return the answer
    return dp[cur] = op;
}

// Function that counts the minimum
// operation to reduce N to M
static int min_operations(int N, int M)
{

    // Initialise dp state
    for(int i = N; i <= M; i++)
    {
        dp[i] = -1;
    }

    // Function call
    return min_op(N, M);
}

// Driver Code
public static void main(String[] args)
{

    // Given N and M
    int N = 6, M = 24;

    // Function call
    int op = min_operations(N, M);

    // INF indicates impossible state
    if (op >= INF)
        System.out.print("-1");
    else
        System.out.print(op + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# INF is the maximum value
# which indicates Impossible state
INF = 10000007;
max_size = 100007;

# Stores the dp states
dp = [0 for i in range(max_size)];

# Recursive Function
# that considers all
# possible even divisors
# of cur
def min_op(cur, M):

    # Indicates impossible
    # state
    if (cur > M):
        return INF;

    if (cur == M):
        return 0;

    # Check dp[cur] is already
    # calculated or not
    if (dp[cur] != -1):
        return dp[cur];

    # op stores the minimum
    # operations required to
    # transform cur to M

    # Initially it is set
    # to INF that meanswe cur
    # can't be transform to M
    op = INF;

    i = 2

    # Loop to find even
    # divisors of cur
    while(i * i <= cur):

        # if i is divisor of cur
        if (cur % i == 0):

            # if i is even
            if(i % 2 == 0):

                # Find recursively
                # for cur+i
                op = min(op, 1 + min_op(cur +
                                        i, M));           

            # Check another divisor
            if ((cur // i) != i and
                (cur // i) % 2 == 0):

                # Find recursively
                # for cur+(cur/i)
                op = min(op, 1 + min_op(cur +
                        (cur // i), M))

        i += 1    

    # Finally store the current state
    # result and return the answer
    dp[cur] = op;
    return op

# Function that counts the minimum
# operation to reduce N to M
def min_operations(N, M):

    # Initialise dp state
    for i in range(N, M + 1):
        dp[i] = -1;

    # Function Call
    return min_op(N, M);

# Driver code
if __name__ == "__main__":

    # Given N and M
    N = 6
    M = 24

    # Function Call
    op = min_operations(N, M);

    # INF indicates impossible state
    if (op >= INF):
        print(-1)
    else:
        print(op)

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// INF is the maximum value
// which indicates Impossible state
static int INF = (int) 1e7;
static int max_size = 100007;

// Stores the dp states
static int []dp = new int[max_size];

// Recursive Function that considers
// all possible even divisors of cur
static int min_op(int cur, int M)
{

    // Indicates impossible state
    if (cur > M)
        return INF;

    if (cur == M)
        return 0;

    // Check dp[cur] is already
    // calculated or not
    if (dp[cur] != -1)
        return dp[cur];

    // op stores the minimum operations
    // required to transform cur to M

    // Initially it is set to INF that
    // meanswe cur can't be transform to M
    int op = INF;

    // Loop to find even divisors of cur
    for(int i = 2; i * i <= cur; i++)
    {       
        // If i is divisor of cur
        if (cur % i == 0)
        {           
            // If i is even
            if (i % 2 == 0)
            {               
                // Find recursively
                // for cur+i
                op = Math.Min(op, 1 +
                              min_op(cur + i, M));
            }

            // Check another divisor
            if ((cur / i) != i &&
                (cur / i) % 2 == 0)
            {
                // Find recursively
                // for cur+(cur/i)
                op = Math.Min(op, 1 +
                              min_op(cur +
                                     (cur / i), M));
            }
        }
    }

    // Finally store the current state
    // result and return the answer
    return dp[cur] = op;
}

// Function that counts the minimum
// operation to reduce N to M
static int min_operations(int N,
                          int M)
{   
    // Initialise dp state
    for(int i = N; i <= M; i++)
    {
        dp[i] = -1;
    }

    // Function call
    return min_op(N, M);
}

// Driver Code
public static void Main(String[] args)
{   
    // Given N and M
    int N = 6, M = 24;

    // Function call
    int op = min_operations(N, M);

    // INF indicates impossible state
    if (op >= INF)
        Console.Write("-1");
    else
        Console.Write(op + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// INF is the maximum value
// which indicates Impossible state
var INF = 10000000;
var max_size = 100007;

// Stores the dp states
var dp = Array(max_size);

// Recursive Function that considers
// all possible even divisors of cur
function min_op( cur, M)
{
    // Indicates impossible state
    if (cur > M)
        return INF;

    if (cur == M)
        return 0;

    // Check dp[cur] is already
    // calculated or not
    if (dp[cur] != -1)
        return dp[cur];

    // op stores the minimum operations
    // required to transform cur to M

    // Initially it is set to INF that
    // meanswe cur can't be transform to M
    var op = INF;

    // Loop to find even divisors of cur
    for (var i = 2; i * i <= cur; i++) {

        // if i is divisor of cur
        if (cur % i == 0) {

            // if i is even
            if (i % 2 == 0) {

                // Find recursively
                // for cur+i
                op = Math.min(op, 1 + min_op(cur + i, M));
            }

            // Check another divisor
            if ((cur / i) != i && (cur / i) % 2 == 0) {

                // Find recursively
                // for cur+(cur/i)
                op = Math.min(op,
                         1 + min_op(cur + (cur / i), M));
            }
        }
    }

    // Finally store the current state
    // result and return the answer
    return dp[cur] = op;
}

// Function that counts the minimum
// operation to reduce N to M
function min_operations(N, M)
{
    // Initialise dp state
    for ( i = N; i <= M; i++) {
        dp[i] = -1;
    }

    // Function Call
    return min_op(N, M);
}

// Driver Code
// Given N and M
var N = 6, M = 24;

// Function Call
var op = min_operations(N, M);

// INF indicates impossible state
if (op >= INF)
    document.write( "-1");
else
    document.write( op + "<br>");

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*sqrt(N))*
***辅助空间:** O(M)*
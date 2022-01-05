# 有限面额合计 N 的方式数

> 原文:[https://www . geeksforgeeks . org/从有限面额中总结总数 n 的方法数/](https://www.geeksforgeeks.org/number-of-ways-to-sum-up-a-total-of-n-from-limited-denominations/)

给定一个数字 **N** 和两个长度为 4 的数组 **arr1[]** 和 **arr2[]** 。数组 **arr1[]** 分别表示 **1、5、10 和 20** 的面额， **arr2[]** 分别表示 **1、5、10 和 20** 的面额计数。任务是找到一些方法，我们可以用有限的面额将它们加起来总共是 **N** 。

**示例:**

> **输入:** arr1[] = {1，5，10，20}，arr2[] = {6，4，3，5}，N = 123
> **输出:** 5
> **说明:**
> 给定硬币面额有 5 种方式合计 123。
> **输入:** arr1[] = {1，5，10，20}，arr2[] = {1，3，2，1}，N = 50
> **输出:** 1
> **说明:**
> 给定面额的硬币最多加 50 只有 1 种方式。

**天真法:**让面额的计数用 A、B、C、d 表示，天真法是运行嵌套循环。每个循环将涉及每种面额的硬币数量。通过以下等式求出制作 N 所需的每种面额的硬币数量:

> **(A * 1)+(B * 5)+(C * 10)+(D * 20))= = N**
> 其中 0 < = a < = A，0&= T7】= B<= B，0 < = c < = C，0 < = d < = D 和 N 为总金额。

***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(1)*

**更好的方法:**我们可以通过给循环增加一些额外的边界来优化上面的简单方法，这将减少一些计算。通过观察，我们可以通过**从 N 中移除面额为 1** 的硬币，并检查以下不等式是否成立，从而很容易地通过丢弃一个循环来降低复杂性:

> **(N–A)<=(b * 5+c * 10+d * 20)<= N**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// ways to sum up a total of N
// from limited denominations
int calculateWays(int arr1[], int arr2[],
                  int N)
{
    // Store the count of denominations
    int A = arr2[0], B = arr2[1];
    int C = arr2[2], D = arr2[3];

    // Stores the final result
    int ans = 0;

    // As one of the denominations is
    // rupee 1, so we can reduce the
    // computation by checking the
    // equality for N-(A*1) = N-A
    for (int b = 0;
         b <= B && b * 5 <= (N); b++)

        for (int c = 0;
             c <= C
             && b * 5 + c * 10 <= (N);
             c++)

            for (int d = 0;
                 d <= D
                 && b * 5 + c * 10 + d * 20 <= (N);
                 d++)

                if ((b * 5) + (c * 10)
                        + (d * 20)
                    >= (N - A))

                    // Increment the count
                    // for number of ways
                    ans++;
    return ans;
}

// Driver Code
int main()
{
    // Given Denominations
    int N = 123;

    int arr1[] = { 1, 5, 10, 20 };
    int arr2[] = { 6, 4, 3, 5 };

    // Function Call
    cout << calculateWays(arr1, arr2, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the number of
// ways to sum up a total of N
// from limited denominations
static int calculateWays(int arr1[], int arr2[],
                         int N)
{

    // Store the count of denominations
    int A = arr2[0], B = arr2[1];
    int C = arr2[2], D = arr2[3];

    // Stores the final result
    int ans = 0;

    // As one of the denominations is
    // rupee 1, so we can reduce the
    // computation by checking the
    // equality for N-(A*1) = N-A
    for(int b = 0;
            b <= B && b * 5 <= (N); b++)

        for(int c = 0;
                c <= C && b * 5 + c * 10 <= (N);
                c++)

            for(int d = 0;
                    d <= D &&
                    b * 5 + c * 10 + d * 20 <= (N);
                    d++)

                if ((b * 5) + (c * 10) +
                    (d * 20) >= (N - A))

                    // Increment the count
                    // for number of ways
                    ans++;
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given denominations
    int N = 123;

    int arr1[] = { 1, 5, 10, 20 };
    int arr2[] = { 6, 4, 3, 5 };

    // Function call
    System.out.print(calculateWays(arr1, arr2, N));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of
# ways to sum up a total of N
# from limited denominations
def calculateWays(arr1, arr2, N):

    # Store the count of denominations
    A = arr2[0]
    B = arr2[1]
    C = arr2[2]
    D = arr2[3]

    # Stores the final result
    ans, b, c, d = 0, 0, 0, 0

    # As one of the denominations is
    # rupee 1, so we can reduce the
    # computation by checking the
    # equality for N-(A*1) = N-A
    while b <= B and b * 5 <= (N):
        c = 0

        while (c <= C and
               b * 5 + c * 10 <= (N)):
            d = 0

            while (d <= D and
                   b * 5 + c * 10 +
                   d * 20 <= (N)):

                if ((b * 5) + (c * 10) +
                    (d * 20) >= (N - A)):

                    # Increment the count
                    # for number of ways
                    ans += 1
                d += 1
            c += 1
        b += 1

    return ans

# Driver Code
if __name__ == '__main__':

    # Given Denominations
    N = 123

    arr1 = [ 1, 5, 10, 20 ]
    arr2 = [ 6, 4, 3, 5 ]

    # Function Call
    print(calculateWays(arr1, arr2, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the number of
// ways to sum up a total of N
// from limited denominations
static int calculateWays(int []arr1, int []arr2,
                         int N)
{

    // Store the count of denominations
    int A = arr2[0], B = arr2[1];
    int C = arr2[2], D = arr2[3];

    // Stores the readonly result
    int ans = 0;

    // As one of the denominations is
    // rupee 1, so we can reduce the
    // computation by checking the
    // equality for N-(A*1) = N-A
    for(int b = 0;
            b <= B && b * 5 <= (N); b++)

        for(int c = 0;
                c <= C && b * 5 + c * 10 <= (N);
                c++)

            for(int d = 0;
                    d <= D &&
                    b * 5 + c * 10 + d * 20 <= (N);
                    d++)

                if ((b * 5) + (c * 10) +
                    (d * 20) >= (N - A))

                    // Increment the count
                    // for number of ways
                    ans++;

    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given denominations
    int N = 123;

    int []arr1 = { 1, 5, 10, 20 };
    int []arr2 = { 6, 4, 3, 5 };

    // Function call
    Console.Write(calculateWays(arr1, arr2, N));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the number of
// ways to sum up a total of N
// from limited denominations
function calculateWays(arr1, arr2,
                         N)
{

    // Store the count of denominations
    let A = arr2[0], B = arr2[1];
    let C = arr2[2], D = arr2[3];

    // Stores the final result
    let ans = 0;

    // As one of the denominations is
    // rupee 1, so we can reduce the
    // computation by checking the
    // equality for N-(A*1) = N-A
    for(let b = 0;
            b <= B && b * 5 <= (N); b++)

        for(let c = 0;
                c <= C && b * 5 + c * 10 <= (N);
                c++)

            for(let d = 0;
                    d <= D &&
                    b * 5 + c * 10 + d * 20 <= (N);
                    d++)

                if ((b * 5) + (c * 10) +
                    (d * 20) >= (N - A))

                    // Increment the count
                    // for number of ways
                    ans++;
    return ans;
}

// Driver Code

     // Given denominations
    let N = 123;

    let arr1 = [ 1, 5, 10, 20 ];
    let arr2 = [ 6, 4, 3, 5 ];

    // Function call
    document.write(calculateWays(arr1, arr2, N));

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**有效方法:**让面额的计数用 A、B、C 和 D 表示，解决上述问题的有效方法是计算使用 **C** 和 **D** 形成的面额的可能数量。然后我们会找到面值为 **A** 和 **B** 的剩余价值。以下是步骤:

1.  初始化数组**方式【】**存储预计算的 **A** 和 **B** 面额之和。
2.  迭代两个嵌套循环，以 ***方式[]*** 存储由 **A** 和 **B** 面额组成的值组合。
3.  迭代两个嵌套循环，找出所有由 **C** 和 **D** 的面额组成的值组合，并将所有可能的值组合**N –( C * 10+D * 20)**相加，相当于 **(A * 1) + (B * 5)** 。
4.  上述步骤中所有值的总和就是所需的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
int ways[1010];

// Function to find the number of
// ways to sum up a total of N
// from limited denominations
int calculateWays(int arr1[], int arr2[],
                  int N)
{
    // Store the count of denominations
    int A = arr2[0], B = arr2[1];
    int C = arr2[2], D = arr2[3];

    // Stores the final result
    int ans = 0;

    // L1 : Incrementing the values
    // with indices with denomination
    // (a * 1 + b * 5)

    // This will give the number of coins
    // for all combinations of coins
    // with value 1 and 5
    for (int b = 0;
         b <= B && b * 5 <= N; b++) {

        for (int a = 0;
             a <= A
             && a * 1 + b * 5 <= N;
             a++) {
            ways[a + b * 5]++;
        }
    }

    // L2 will sum the values of those
    // indices of ways[] which is equal
    // to (N - (c * 10 + d * 20))
    for (int c = 0;
         c <= C && c * 10 <= (N); c++) {

        for (int d = 0;
             d <= D
             && c * 10 + d * 20 <= (N);
             d++) {
            ans += ways[N - c * 10 - d * 20];
        }
    }

    // Return the final count
    return ans;
}

// Driver Code
int main()
{
    // Given Denominations
    int N = 123;

    int arr1[] = { 1, 5, 10, 20 };
    int arr2[] = { 6, 4, 3, 5 };

    // Function Call
    cout << calculateWays(arr1, arr2, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int []ways = new int[1010];

// Function to find the number of
// ways to sum up a total of N
// from limited denominations
static int calculateWays(int arr1[], int arr2[],
                         int N)
{

    // Store the count of denominations
    int A = arr2[0], B = arr2[1];
    int C = arr2[2], D = arr2[3];

    // Stores the final result
    int ans = 0;

    // L1 : Incrementing the values
    // with indices with denomination
    // (a * 1 + b * 5)

    // This will give the number of coins
    // for all combinations of coins
    // with value 1 and 5
    for(int b = 0;
            b <= B && b * 5 <= N; b++)
    {
        for(int a = 0;
                a <= A && a * 1 + b * 5 <= N;
                a++)
        {
            ways[a + b * 5]++;
        }
    }

    // L2 will sum the values of those
    // indices of ways[] which is equal
    // to (N - (c * 10 + d * 20))
    for(int c = 0;
            c <= C && c * 10 <= (N); c++)
    {
        for(int d = 0;
                d <= D && c * 10 + d * 20 <= (N);
                d++)
        {
            ans += ways[N - c * 10 - d * 20];
        }
    }

    // Return the final count
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given denominations
    int N = 123;

    int arr1[] = { 1, 5, 10, 20 };
    int arr2[] = { 6, 4, 3, 5 };

    // Function call
    System.out.print(calculateWays(arr1, arr2, N));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
ways = [0 for i in range(1010)];

# Function to find the number of
# ways to sum up a total of N
# from limited denominations
def calculateWays(arr1, arr2, N):

    # Store the count of denominations
    A = arr2[0]; B = arr2[1];
    C = arr2[2]; D = arr2[3];

    # Stores the final result
    ans = 0;

    # L1 : Incrementing the values
    # with indices with denomination
    # (a * 1 + b * 5)

    # This will give the number of coins
    # for all combinations of coins
    # with value 1 and 5
    for b in range(0, B + 1):
        if(b * 5 > N):
            break;
        for a in range(0, A + 1):
            if(a + b * 5 > N):
                break;
            ways[a + b * 5] += 5;   

    # L2 will sum the values of those
    # indices of ways which is equal
    # to (N - (c * 10 + d * 20))
    for c in range(0, C):
        if(c * 10 > N):
            break;
        for d in range(0, D):
            if(c * 10 + d * 20 > N):
                break;
            ans += ways[N - c * 10 - d * 20];   

    # Return the final count
    return ans;

# Driver Code
if __name__ == '__main__':

    # Given denominations
    N = 123;

    arr1 = [1, 5, 10, 20];
    arr2 = [6, 4, 3, 5];

    # Function call
    print(calculateWays(arr1, arr2, N));

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int []ways = new int[1010];

// Function to find the number of
// ways to sum up a total of N
// from limited denominations
static int calculateWays(int []arr1, int []arr2,
                         int N)
{

    // Store the count of denominations
    int A = arr2[0], B = arr2[1];
    int C = arr2[2], D = arr2[3];

    // Stores the readonly result
    int ans = 0;

    // L1 : Incrementing the values
    // with indices with denomination
    // (a * 1 + b * 5)

    // This will give the number of coins
    // for all combinations of coins
    // with value 1 and 5
    for(int b = 0;
            b <= B && b * 5 <= N; b++)
    {
        for(int a = 0;
                a <= A && a * 1 + b * 5 <= N;
                a++)
        {
            ways[a + b * 5]++;
        }
    }

    // L2 will sum the values of those
    // indices of ways[] which is equal
    // to (N - (c * 10 + d * 20))
    for(int c = 0;
            c <= C && c * 10 <= (N); c++)
    {
        for(int d = 0;
                d <= D && c * 10 + d * 20 <= (N);
                d++)
        {
            ans += ways[N - c * 10 - d * 20];
        }
    }

    // Return the final count
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given denominations
    int N = 123;

    int []arr1 = { 1, 5, 10, 20 };
    int []arr2 = { 6, 4, 3, 5 };

    // Function call
    Console.Write(calculateWays(arr1, arr2, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach
var ways = Array(1010).fill(0);

// Function to find the number of
// ways to sum up a total of N
// from limited denominations
function calculateWays(arr1, arr2, N)
{
    // Store the count of denominations
    var A = arr2[0], B = arr2[1];
    var C = arr2[2], D = arr2[3];

    // Stores the final result
    var ans = 0;

    // L1 : Incrementing the values
    // with indices with denomination
    // (a * 1 + b * 5)

    // This will give the number of coins
    // for all combinations of coins
    // with value 1 and 5
    for (var b = 0;
         b <= B && b * 5 <= N; b++) {

        for (var a = 0;
             a <= A
             && a * 1 + b * 5 <= N;
             a++) {
            ways[a + b * 5]++;
        }
    }

    // L2 will sum the values of those
    // indices of ways[] which is equal
    // to (N - (c * 10 + d * 20))
    for (var c = 0;
         c <= C && c * 10 <= (N); c++) {

        for (var d = 0;
             d <= D
             && c * 10 + d * 20 <= (N);
             d++) {
            ans += ways[N - c * 10 - d * 20];
        }
    }

    // Return the final count
    return ans;
}

// Driver Code

// Given Denominations
var N = 123;
var arr1 = [1, 5, 10, 20];
var arr2 = [6, 4, 3, 5];

// Function Call
document.write( calculateWays(arr1, arr2, N));

</script>
```

**Output:** 

```
5
```

**时间复杂度:***O(N<sup>2</sup>)*
T7】辅助空间: *O(1)*
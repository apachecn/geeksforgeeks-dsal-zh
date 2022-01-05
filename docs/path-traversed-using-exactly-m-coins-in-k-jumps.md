# 在 K 次跳跃中使用正好 M 个硬币穿过的路径

> 原文:[https://www . geeksforgeeks . org/path-traversed-使用精确的 m-coins-in-k-jumps/](https://www.geeksforgeeks.org/path-traversed-using-exactly-m-coins-in-k-jumps/)

给定三个整数 **N** 、 **K** 和 **M** 分别代表箱子的数量(从 1 到 **N** 水平对齐)、允许跳跃的总数和可用硬币总数，任务是通过在精确 **K** 跳跃中使用精确 **M** 硬币来打印**【1，N】**内可穿越的路径。如果从位置 **X** 跳到位置 **Y** ，则使用**ABS(X–Y)**硬币。如果 **K** 跳跃中无法使用 **M** 硬币，则打印-1。
**举例:**

> **输入:** N = 5，K = 4，M = 12
> **输出:** 5 1 4 5
> **解释:**
> 第一跳:框 1 - >框 5。因此，使用了|1-5| = 4 枚硬币。
> 第二跳:5 号箱->1 号箱因此，|5-1| =使用了 4 枚硬币。
> 第三跳:1 号箱->4 号箱使用 3 枚硬币。
> 第四跳:4 号箱->5 号箱使用 1 枚硬币。
> 因此，正好 12 枚硬币用于 4 次跳跃。
> **输入:** N = 4，K = 3，M = 10
> **输出:** -1

**进场:**

> 我们可以观察到，对于以下两种情况，答案将是-1:
> 
> *   **K > N-1** 或
>     
> *   **K * (N-1) < M** 。

问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)按照下面给出的步骤解决:
重复下面的操作，直到 **K** 变为零。

1.  求 **N-1** 和**M–K-1**的最小值。
2.  根据上述最小值，根据可用性向左或向右移动减少 k。
3.  重复上述步骤，直到 K 变为 0。

以下是上述方法的实现:

## C++

```
// C++ program to print
// the path using exactly
// K jumps and M coins
#include <bits/stdc++.h>
using namespace std;

// Function that print the path
// using exactly K jumps and M coins
void print_path(int N, int jump, int coin)
{
    // If no path exists
    if (jump > coin
        || jump * (N - 1) < coin) {
        cout << "-1" << endl;
    }
    else {
        int pos = 1;
        while (jump > 0) {

            // It decides which
            // box to be jump
            int tmp = min(N - 1,
                          coin - (jump - 1));

            // It decides whether
            // to jump on left side or
            // to jump on right side
            if (pos + tmp <= N) {
                pos += tmp;
            }
            else {
                pos -= tmp;
            }

            // Print the path
            cout << pos << " ";

            coin -= tmp;
            jump -= 1;
        }
    }
}

// Driver Code
int main()
{
    int N = 5, K = 4, M = 12;

    // Function Call
    print_path(N, K, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the path
// using exactly K jumps and M coins
import java.io.*;

class GFG{

// Function that print the path
// using exactly K jumps and M coins
static void print_path(int N, int jump,
                              int coin)
{
    // If no path exists
    if (jump > coin || jump * (N - 1) < coin)
    {
        System.out.println("-1");
    }
    else
    {
        int pos = 1;
        while (jump > 0)
        {

            // It decides which
            // box to be jump
            int tmp = Math.min(N - 1,
                               coin - (jump - 1));

            // It decides whether
            // to jump on left side or
            // to jump on right side
            if (pos + tmp <= N)
            {
                pos += tmp;
            }
            else
            {
                pos -= tmp;
            }

            // Print the path
            System.out.print(pos + " ");;

            coin -= tmp;
            jump -= 1;
        }
    }
}

// Driver Code
public static void main (String[] args)
{
    int N = 5, K = 4, M = 12;

    // Function Call
    print_path(N, K, M);
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 program to print the path 
# using exactly K jumps and M coins

# Function that pr the path
# using exactly K jumps and M coins
def print_path(N, jump, coin):

    # If no path exists
    if (jump > coin or
        jump * (N - 1) < coin):
        print("-1")

    else:
        pos = 1;
        while (jump > 0):

            # It decides which
            # box to be jump
            tmp = min(N - 1,
                      coin - (jump - 1));

            # It decides whether
            # to jump on left side or
            # to jump on right side
            if (pos + tmp <= N):
                pos += tmp;
            else:
                pos -= tmp;

            # Print the path
            print(pos, end = " ")

            coin -= tmp;
            jump -= 1;

# Driver code
N = 5
K = 4
M = 12

# Function call
print_path(N, K, M);

# This code is contributed by grand_master
```

## C#

```
// C# program to print the path
// using exactly K jumps and M coins
using System;

class GFG{

// Function that print the path
// using exactly K jumps and M coins
static void print_path(int N, int jump,
                              int coin)
{

    // If no path exists
    if (jump > coin || jump * (N - 1) < coin)
    {
        Console.WriteLine("-1");
    }

    else
    {
        int pos = 1;
        while (jump > 0)
        {

            // It decides which
            // box to be jump
            int tmp = Math.Min(N - 1,
                            coin - (jump - 1));

            // It decides whether
            // to jump on left side or
            // to jump on right side
            if (pos + tmp <= N)
            {
                pos += tmp;
            }
            else
            {
                pos -= tmp;
            }

            // Print the path
            Console.Write(pos + " ");

            coin -= tmp;
            jump -= 1;
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5, K = 4, M = 12;

    // Function Call
    print_path(N, K, M);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to print the path
// using exactly K jumps and M coins

// Function that print the path
// using exactly K jumps and M coins
function print_path(N, jump, coin)
{
    // If no path exists
    if (jump > coin || jump * (N - 1) < coin)
    {
        document.write("-1");
    }
    else
    {
        let pos = 1;
        while (jump > 0)
        {

            // It decides which
            // box to be jump
            let tmp = Math.min(N - 1,
                               coin - (jump - 1));

            // It decides whether
            // to jump on left side or
            // to jump on right side
            if (pos + tmp <= N)
            {
                pos += tmp;
            }
            else
            {
                pos -= tmp;
            }

            // Print the path
            document.write(pos + " ");;

            coin -= tmp;
            jump -= 1;
        }
    }
} 

// Driver Code

    let N = 5, K = 4, M = 12;

    // Function Call
    print_path(N, K, M);

</script>
```

**Output:**

```
5 1 4 5
```

***时间复杂度:** O(K)*
***辅助空间:** O(1)*
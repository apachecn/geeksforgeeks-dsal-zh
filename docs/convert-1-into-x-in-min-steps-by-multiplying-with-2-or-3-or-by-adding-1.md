# 将 1 乘以 2 或 3 或加 1

以最小步长转换为 X

> 原文:[https://www . geesforgeks . org/convert-1-in-x-in-min-steps-by-乘-2-or-3-or-by-add-1/](https://www.geeksforgeeks.org/convert-1-into-x-in-min-steps-by-multiplying-with-2-or-3-or-by-adding-1/)

给定一个整数 **X，**任务是通过下面给定的操作将 **1** 转换为 **X** :

*   把这个数乘以 2。
*   将数字乘以 3。
*   在数字上加 1。

任务是打印使用这三个操作将 **1** 转换为 **X** 所需的最小操作数，并打印执行的操作顺序。

**示例:**

> **输入:** X **=** 5
> **输出:**
> 3
> 1 3 4 5
> **说明:**
> 在任何操作之前，X = 1
> 第一次操作:将数字 1 乘以 3，因此 X = 3。
> 第二次运算:在数字 3 上加 1，因此 X = 4。
> 第三个操作:在数字 4 上加 1，因此 X = 5。
> 因此，至少需要 3 次操作，顺序为 1 3 4 5。
> 
> **输入:** X **=** 20
> **输出:**
> 4
> 1 3 9 10 20
> **说明:**
> 在任何操作之前，X = 1
> 第一次操作:将数字 1 乘以 3，因此 X = 3。
> 第二次运算:数字 3 乘以 3，因此 X = 9。
> 第三个操作:在数字 9 上加 1，因此 X = 10。
> 第四次运算:数字 10 乘以 2，因此 X = 20。
> 因此，至少需要 4 次操作，顺序为 1 3 9 10 20。

**天真法:**最简单的方法是找到所有可能的操作顺序，将 **1** 转换为 **X** ，返回操作次数最少的那个。
**时间复杂度:*****O(3<sup>N</sup>)*** ****辅助空间:** *O(1)***

****高效方法:**优化上述幼稚方法的思路是利用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)找到最小操作数，然后回溯找到所需的操作序列。以下是步骤:**

1.  **初始化 **dp[]** 以存储每个索引 I 达到 **1 到 i** 的最小操作次数。**
2.  **现在***DP【X】***存储从 **1 开始制作 **X** 所需的最小操作次数。**我们将填充**自下而上方法**中的 **dp[]** 数组。对于任意值 X，我们可以通过以下方式之一减少:

    1.  如果 X 能被 2 整除，那么就用 2 整除，并对这个运算进行计数。
    2.  如果 X 能被 3 整除，那么就用 3 整除，并对这个运算进行计数。
    3.  否则从 x 中减去 1。** 
3.  **根据上述步骤，形成的递归关系由下式给出:**

```
dp[X] = min(dp[X/2] + 1,  // If X is divisible by 2
            dp[X/3] + 1,  // If X is divisible by 3
            dp[X-1] + 1)

Base Condition:
dp[1] = 0  // As no operation required when X = 1
```

1.  **创建***【DP】***数组后，使用数组中存储的值回溯，并将序列存储在列表中。**
2.  **打印列表中存储的最小操作和顺序。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to print the Minimum number
// of operations required to convert 1
// into X by using three given operations
void printMinOperations(int N)
{

    // Initialize a DP array to store
    //min operations for sub-problems
    int dp[N + 1];
    for(int i = 0; i < N + 1; i++)
        dp[i] = N;

    // Base Condition:
    // No operation required
    // when N is 1
    dp[1] = 0;

    for(int i = 2; i < N + 1; i++)
    {

        // Multiply the number by 2
        if (i % 2 == 0 && dp[i] > dp[i / 2] + 1)
            dp[i] = dp[i / 2] + 1;

        // Multiply the number by 3
        if (i % 3 == 0 && dp[i] > dp[i / 3] + 1)
            dp[i] = dp[i / 3] + 1;

        // Add 1 to the number.
        if (dp[i] > dp[i - 1] + 1)
            dp[i] = dp[i - 1] + 1;
    }

    // Print the minimum operations
    cout << dp[N] << endl;

    // Initialize a list to store
    // the sequence
    vector<int>seq;

    // Backtrack to find the sequence
    while (N > 1)
    {
        seq.push_back(N);

        // If add by 1
        if(dp[N - 1] == dp[N] - 1)
            N = N - 1;

        // If multiply by 2
        else if (N % 2 == 0 &&
              dp[N / 2] == dp[N] - 1)
            N = N / 2;

        // If multiply by 3
        else
            N = N / 3;
    }
    seq.push_back(1);

    // Print the sequence of operation
    for(int i = seq.size() - 1; i >= 0; i--)
        cout << seq[i] << " ";

    cout << endl;
}

// Driver code
int main()
{

    // Given number X
    int X = 96234;

    // Function call
    printMinOperations(X);
}

// This code is contributed by Stream_Cipher
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the Minimum number
// of operations required to convert 1
// into X by using three given operations
static void printMinOperations(int N)
{

    // Initialize a DP array to store
    //min operations for sub-problems
    int dp[] = new int[N + 1];
    for(int i = 0; i < N + 1; i++)
        dp[i] = N;

    // Base Condition:
    // No operation required
    // when N is 1
    dp[1] = 0;

    for(int i = 2; i < N + 1; i++)
    {

        // Multiply the number by 2
        if (i % 2 == 0 && dp[i] > dp[i / 2] + 1)
                dp[i] = dp[i / 2] + 1;

        // Multiply the number by 3
        if (i % 3 == 0 && dp[i] > dp[i / 3] + 1)
            dp[i] = dp[i / 3] + 1;

        // Add 1 to the number.
        if (dp[i] > dp[i - 1] + 1)
            dp[i] = dp[i - 1] + 1;
    }

    // Print the minimum operations
    System.out.println(dp[N]);

    // Initialize a list to store
    // the sequence
    Vector<Integer> seq = new Vector<Integer>();

    // Backtrack to find the sequence
    while (N > 1)
    {
        seq.add(N);

        // If add by 1
        if(dp[N - 1] == dp[N] - 1)
            N = N - 1;

        // If multiply by 2
        else if (N % 2 == 0 &&
              dp[N / 2] == dp[N] - 1)
            N = N / 2;

        // If multiply by 3
        else
            N = N / 3;

    }
    seq.add(1);

    // Print the sequence of operation
    for(int i = seq.size() - 1; i >= 0; i--)
        System.out.print(seq.get(i) + " ");
}

// Driver code
public static void main(String args[])
{

    // Given number X
    int X = 96234;

    // Function call
    printMinOperations(X);
}
}

// This code is contributed by Stream_Cipher
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to print the Minimum number
# of operations required to convert 1
# into X by using three given operations

def printMinOperations(N):

    # Initialize a DP array to store
    # min operations for sub-problems
    dp = [N]*(N + 1)

    # Base Condition:
    # No operation required
    # when N is 1
    dp[1] = 0

    for i in range(2, N + 1):

        # Multiply the number by 2
        if (i % 2 == 0 and dp[i] > dp[i//2]+1):
            dp[i] = dp[i//2]+1

        # Multiply the number by 3
        if (i % 3 == 0 and dp[i] > dp[i//3]+1):
            dp[i] = dp[i//3]+1

        # Add 1 to the number.
        if (dp[i] > dp[i-1]+1):
            dp[i] = dp[i-1] + 1

    # Print the minimum operations
    print(dp[N], end ="\n")

    # Initialize a list to store
    # the sequence
    seq = []

    # Backtrack to find the sequence
    while (N > 1):
        seq.append(N)

        # If add by 1
        if dp[N-1] == dp[N] - 1:
            N = N-1

        # If multiply by 2
        elif N % 2 == 0 and dp[N//2] == dp[N] - 1:
            N = N//2

        # If multiply by 3
        else:
            N = N//3
    seq.append(1)

    # Print the sequence of operation
    for i in reversed(seq):
        print(i, end =" ")

# Driver Code

# Given number X
X = 96234

# Function Call
printMinOperations(X)
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the Minimum number
// of operations required to convert 1
// into X by using three given operations
static void printMinOperations(int N)
{

    // Initialize a DP array to store
    //min operations for sub-problems
    int []dp = new int[N + 1];
    for(int i = 0; i < N + 1; i++)
        dp[i] = N;

    // Base Condition:
    // No operation required
    // when N is 1
    dp[1] = 0;

    for(int i = 2; i < N + 1; i++)
    {

        // Multiply the number by 2
        if (i % 2 == 0 && dp[i] > dp[i / 2] + 1)
                dp[i] = dp[i / 2] + 1;

        // Multiply the number by 3
        if (i % 3 == 0 && dp[i] > dp[i / 3] + 1)
            dp[i] = dp[i / 3] + 1;

        // Add 1 to the number.
        if (dp[i] > dp[i - 1] + 1)
            dp[i] = dp[i - 1] + 1;
    }

    // Print the minimum operations
    Console.WriteLine(dp[N]);

    // Initialize a list to store
    // the sequence
    List<int> seq = new List<int>();

    // Backtrack to find the sequence
    while (N > 1)
    {
        seq.Add(N);

        // If add by 1
        if(dp[N - 1] == dp[N] - 1)
            N = N - 1;

        // If multiply by 2
        else if (N % 2 == 0 &&
              dp[N / 2] == dp[N] - 1)
            N = N / 2;

        // If multiply by 3
        else
            N = N / 3;
    }
    seq.Add(1);
    seq.Reverse();

    // Print the sequence of operation
    foreach(var i in seq)
    {
        Console.Write(i + " ");
    }
}

// Driver code
public static void Main()
{

    // Given number X
    int X = 96234;

    // Function call
    printMinOperations(X);
}
}

// This code is contributed by Stream_Cipher
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to print the Minimum number
// of operations required to convert 1
// into X by using three given operations
function printMinOperations(N)
{

    // Initialize a DP array to store
    //min operations for sub-problems
    var dp = Array(N+1)
    for(var i = 0; i < N + 1; i++)
        dp[i] = N;

    // Base Condition:
    // No operation required
    // when N is 1
    dp[1] = 0;

    for(var i = 2; i < N + 1; i++)
    {

        // Multiply the number by 2
        if (i % 2 == 0 && dp[i] > dp[i / 2] + 1)
            dp[i] = dp[i / 2] + 1;

        // Multiply the number by 3
        if (i % 3 == 0 && dp[i] > dp[i / 3] + 1)
            dp[i] = dp[i / 3] + 1;

        // Add 1 to the number.
        if (dp[i] > dp[i - 1] + 1)
            dp[i] = dp[i - 1] + 1;
    }

    // Print the minimum operations
    document.write( dp[N] + "<br>");

    // Initialize a list to store
    // the sequence
    var seq = [];

    // Backtrack to find the sequence
    while (N > 1)
    {
        seq.push(N);

        // If add by 1
        if(dp[N - 1] == dp[N] - 1)
            N = N - 1;

        // If multiply by 2
        else if (N % 2 == 0 &&
              dp[N / 2] == dp[N] - 1)
            N = N / 2;

        // If multiply by 3
        else
            N = N / 3;
    }
    seq.push(1);

    // Print the sequence of operation
    for(var i = seq.length - 1; i >= 0; i--)
        document.write( seq[i] + " ");

    document.write("<br>");
}

// Driver code

// Given number X
var X = 96234;

// Function call
printMinOperations(X);

</script>
```

****Output:**

```
14
1 3 9 10 11 33 99 297 891 2673 8019 16038 16039 48117 96234 
```** 

****时间复杂度:***O(N)*
T5】辅助空间: *O(N)***
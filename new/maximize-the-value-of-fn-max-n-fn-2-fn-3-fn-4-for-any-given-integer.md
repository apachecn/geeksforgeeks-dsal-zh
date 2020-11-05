# 对于任何给定的整数

> 原文：[https://www.geeksforgeeks.org/maximize-the-value-of-fn-max-n-fn-2-fn-3-fn-4-for-any-given-integer/](https://www.geeksforgeeks.org/maximize-the-value-of-fn-max-n-fn-2-fn-3-fn-4-for-any-given-integer/)

，最大化 F（N）= max（N，F（N / 2）+ F（N / 3）+ F（N / 4））的值

给定整数 **N，**的任务是找到由**给定的函数 **F（n）**的最大值 F（N）= max（N，F（N / 2） ）+ F（N / 3）+ F（N / 4））**。

**示例**：

> **输入**：N = 3
> **输出**：3
> **说明**：
> F（3）= max（3，F（1） + F（1）+ F（0）），如 F（0）= 0 和 F（1）= 1
> F（3）= max（3，1 + 1+ 0）
> F（3） = max（3，2）
> 因此，F（3）的最大值是 3。
> 
> **输入**：N = 12
> **输出**：13
> **说明**：
> F（12）= max（12，F（6） + F（4）+ F（3））
> F（6）= max（6，F（3）+ F（2）+ F（1））
> F（3）= max（3， F（1）+ F（1）+ F（0）），如 F（0）= 0 和 F（1）= 1
> F（3）= max（3，1 + 1+ 0）
> F（3）= max（3，2）= 3
> F（2）= max（2，F（1）+ F（0）+ F（0））
> F（2）= max（ 2,1 + 0 + 0）= 2
> F（4）= max（4，F（2）+ F（1）+ F（1）））
> F（4）= max（4，2 + 1 +1）= 4
> F（6）= max（6，3 + 2 +1）= 6
> 现在，F（12）= max（12，6 + 4 + 3）
> F（12）= max（12，13）
> 因此，F（12）的最大值是 13。

**朴素的方法**：最简单的方法是使用[递归](https://www.geeksforgeeks.org/recursion/)计算 **F（N）**的值。 在每个步骤中，分别对值 **N / 2** ， **N / 3** 和 **N / 4** 分别调用三个递归调用，然后返回每个递归调用 **N** 的最大值与这些递归调用返回的值之和。 在所有递归调用结束后，将值打印为结果。

**时间复杂度**：O（3 <sup>N</sup> ）

**辅助空间**：`O(1)`

[**动态规划**](http://www.geeksforgeeks.org/dynamic-programming/) **使用自下而上的方法**：上面的递归调用也可以使用 辅助数组 **dp []** ，并以自下而上的方式计算每个状态的值。 步骤如下：

*   创建大小为 **N** 的辅助数组 **dp []** 。

*   将 **0** 和 **1** 初始化为 **dp [0] = 0** 和 **dp [1] = 1** 。

*   [在范围 **[2，N]** 范围内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **dp []** ，并将每个状态更新为：

> dp [i] = max（i，dp [i / 2] + dp [i / 3] + dp [i / 4]）

*   在上述步骤之后，打印 dp [N]的值作为结果。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to build the auxiliary DP
// array from the start
void build(int dp[], int N)
{
    // Base Case
    dp[0] = 0;
    dp[1] = 1;

// Iterate over the range
    for (int i = 2; i <= N; i++) {

    // Update each state
        dp[i] = max(i, dp[i / 2] 
                    + dp[i / 3] 
                    + dp[i / 4]);
    }
}

// Function to find the maximum value of
// F(n) = max(n, F[n/2] + F[n/3] + F[n/4])
int maxValue(int N)
{
    // Auxuliary DP array
    int dp[N + 1];

    // Function call to build DP array
    build(dp, N);

    // Print the answer
    cout << dp[N];
}

// Driver Code
int main()
{
    // Given N
    int N = 12;

    // Function Call
    maxValue(N);

    return 0;
}

```

## Java

```java

// Java program for the above approach
import java.util.*; 

class GFG{

// Function to build the auxiliary DP
// array from the start
static void build(int dp[], int N)
{

    // Base Case
    dp[0] = 0;
    dp[1] = 1;

    // Iterate over the range
    for(int i = 2; i <= N; i++) 
    {

        // Update each state
        dp[i] = Math.max(i, dp[i / 2] + 
                            dp[i / 3] + 
                            dp[i / 4]);
    }
}

// Function to find the maximum value of
// F(n) = max(n, F[n/2] + F[n/3] + F[n/4])
static void maxValue(int N)
{

    // Auxuliary DP array
    int dp[] = new int[N + 1];

    // Function call to build DP array
    build(dp, N);

    // Print the answer
    System.out.println(dp[N]);
}

// Driver code
public static void main(String[] args)
{

    // Given N
    int N = 12;

    // Function Call
    maxValue(N);
}
}

// This code is contributed by code_hunt

```

## Python3

```py

# Python3 program for the above approach

# Function to build the auxiliary DP
# array from the start
def build(dp, N):

    # Base Case
    dp[0] = 0
    dp[1] = 1

    # Iterate over the range
    for i in range(2, N + 1):

        # Update each state
        dp[i] = max(i, dp[i // 2] +
                    dp[i // 3] +
                    dp[i // 4])

# Function to find the maximum value of
# F(n) = max(n, F[n/2] + F[n/3] + F[n/4])
def maxValue(N):

    # Auxuliary DP array
    dp = [0] * (N + 1)

    # Function call to build DP array
    build(dp, N)

    # Print the answer
    print(dp[N], end = "")

# Driver Code
if __name__ == '__main__':

    # Given N
    N = 12

    # Function Call
    maxValue(N)

# This code is contributed by mohit kumar 29

```

**Output:** 

```
13

```

**时间复杂度**：`O(n)`

***空间复杂度**：`O(n)`*

[**动态规划**](http://www.geeksforgeeks.org/dynamic-programming/) **使用自顶向下方法**：与上述方法一样，[有很多重叠 每个递归调用的子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。 因此，为了优化上述方法，其思想是使用辅助空间[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储在每个递归调用中计算出的值并返回重复的存储状态。 步骤如下：

*   初始化映射**映射**，以存储在每个递归调用中计算的值。

*   **基本情况**：如果 **N** 的值为 **0** 或 **1** ，则结果为 **0** 和 **1** 。 同样，如果存在任何先前计算的状态，则将该值返回为：

> >基本情况：
> if（N < = 1）{
> 返回 N；
> }
> **记忆状态**：
> if（Map.find（N）！= Map.end（））{
> 返回 Map [N];
> }

*   **递归调用**：如果不满足基本条件，则通过递归调用每个状态来找到当前状态的值，如下所示：

> 结果= max（N，递归函数（N / 2）+递归函数（N / 3）+递归函数（N / 4））

*   **返回语句**：在每个递归调用中（基本情况除外），将在上一步中计算出的当前状态存储在映射中，并返回计算出的值作为当前状态的结果 。

> Map [N] =结果；
> 返回结果；

*   完成上述步骤后，将值打印返回到所有递归调用的末尾。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Map used for memoization
map<int, int> mp;

// Function to find maximum value
// of the given recurrence relation
int maxValue(int N)
{
    // Base Case
    if (N <= 1)
        return N;

    // If previously computed
    if (mp[N] != 0)
        return mp[N];

    // Computing value of function
    // when its not already computed
    int ans = max(N, maxValue(N / 2) 
                + maxValue(N / 3)
                + maxValue(N / 4));

    // Storing value for further
    // computation reduction
    mp[N] = ans;

    return ans;
}

// Utility function to find maximum value
// of the given recurrence relation
void maxValueUtil(int N)
{
    // Stores final result
    int result = maxValue(N);

    // Print the result
    cout << result;
}

// Drive Code
int main()
{
    // Given N
    int N = 12;

    // Function Call
    maxValueUtil(N);

    return 0;
}

```

## Java

```java

// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Map used for memoization
static Map<Integer, Integer> mp = new HashMap<>();

// Function to find maximum value
// of the given recurrence relation
static int maxValue(int N)
{

    // Base Case
    if (N <= 1)
        return N;

    // If previously computed
    if (mp.containsKey(N))
        return mp.get(N);

    // Computing value of function
    // when its not already computed
    int ans = Math.max(N, maxValue(N / 2) +
                          maxValue(N / 3) +
                          maxValue(N / 4));

    // Storing value for further
    // computation reduction
    mp.put(N, ans);

    return ans;
}

// Utility function to find maximum value
// of the given recurrence relation
static void maxValueUtil(int N)
{

    // Stores final result
    int result = maxValue(N);

    // Print the result
    System.out.print(result);
}

// Driver code
public static void main (String[] args) 
{

    // Given N
    int N = 12;

    // Function Call
    maxValueUtil(N);
}
}

// This code is contributed by offbeat

```

**Output:** 

```
13

```

**时间复杂度**：`O(log n)`

**辅助空间**：`O(log n)`



* * *

* * *




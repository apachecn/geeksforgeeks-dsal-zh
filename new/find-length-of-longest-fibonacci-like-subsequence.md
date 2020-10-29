# 查找最长斐波那契式子序列

> 原文：[https://www.geeksforgeeks.org/find-length-of-longest-fibonacci-like-subsequence/](https://www.geeksforgeeks.org/find-length-of-longest-fibonacci-like-subsequence/)

的长度

给定**严格增加的**数组 **A** 的正整数，其中，

![1 \leq A[i] \leq 10^{18} ](img/f42ec5ec711971455c7d35ba346286d8.png "Rendered by QuickLaTeX.com")

。 任务是找到 **A** 的最长**斐波那契样子序列**的长度。 如果这样的子序列不存在，则**返回 0** 。

**示例**：

> **输入**：A = [1、3、7、11、12、14、18]
> **输出**：3
> **说明**：
> 类似于斐波那契的最长子序列：[1，11，12]。 其他可能的子序列是[3，11，14]或[7，11，18]。
> 
> **输入**：A = [1、2、3、4、5、6、7、8]
> **输出**：5
> **说明**：
> 类似于斐波那契的最长子序列：[1、2、3、5、8]。

**朴素的方法**：**类斐波那契序列**使得每个序列都有两个相邻的项来确定下一个预期项。

> 例如，对于 1、1，我们希望序列必须继续 2、3、5、8、13 等。

*   使用**设置**或**映射**可以快速确定数组 **A** 中是否存在**斐波那契数列**的下一项。 由于这些术语的**指数增长**，因此每次迭代都只能进行 log（M）搜索以获取下一个元素。

*   对于每个起始对 **A [i]，A [j]** ，我们维持下一个期望值 **y = A [i] + A [j]** 和先前看到的最大值 **x = A [j]** 。 如果数组中有 **y** ，那么我们可以更新这些值**（x，y）->（y，x + y）**，否则我们立即停止。

下面是上述方法的实现：

## C++

```cpp

// CPP implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the max Length of
// Fibonacci subsequence
int LongestFibSubseq(int A[], int n)
{
    // Store all array elements in a hash
    // table
    unordered_set<int> S(A, A + n);

    int maxLen = 0, x, y;

    for (int i = 0; i < n; ++i) {
        for (int j = i + 1; j < n; ++j) {

            x = A[j];
            y = A[i] + A[j];
            int length = 2;

            // check until next fib element is found
            while (S.find(y) != S.end()) {

                // next element of fib subseq
                int z = x + y;
                x = y;
                y = z;
                maxLen = max(maxLen, ++length);
            }
        }
    }

    return maxLen >= 3 ? maxLen : 0;
}

// Driver program
int main()
{
    int A[] = { 1, 2, 3, 4, 5, 6, 7, 8 };
    int n = sizeof(A) / sizeof(A[0]);
    cout << LongestFibSubseq(A, n);
    return 0;
}

// This code is written by Sanjit_Prasad

```

## Java

```java

// Java implementation of above approach 
import java.util.*;
public class GFG {

// Function to return the max Length of 
// Fibonacci subsequence 
    static int LongestFibSubseq(int A[], int n) {
        // Store all array elements in a hash 
        // table 
        TreeSet<Integer> S = new TreeSet<>();
        for (int t : A) {
            // Add each element into the set 
            S.add(t);
        }
        int maxLen = 0, x, y;

        for (int i = 0; i < n; ++i) {
            for (int j = i + 1; j < n; ++j) {

                x = A[j];
                y = A[i] + A[j];
                int length = 3;

                // check until next fib element is found 
                while (S.contains(y) && (y != S.last())) {

                    // next element of fib subseq 
                    int z = x + y;
                    x = y;
                    y = z;
                    maxLen = Math.max(maxLen, ++length);
                }
            }
        }
        return maxLen >= 3 ? maxLen : 0;
    }

// Driver program 
    public static void main(String[] args) {
        int A[] = {1, 2, 3, 4, 5, 6, 7, 8};
        int n = A.length;
        System.out.print(LongestFibSubseq(A, n));
    }
}
// This code is contributed by 29AjayKumar

```

## Python3

```py

# Python3 implementation of the 
# above approach 

# Function to return the max Length 
# of Fibonacci subsequence 
def LongestFibSubseq(A, n): 

    # Store all array elements in 
    # a hash table 
    S = set(A) 
    maxLen = 0

    for i in range(0, n): 
        for j in range(i + 1, n): 

            x = A[j] 
            y = A[i] + A[j] 
            length = 2

            # check until next fib 
            # element is found 
            while y in S: 

                # next element of fib subseq 
                z = x + y 
                x = y 
                y = z
                length += 1
                maxLen = max(maxLen, length) 

    return maxLen if maxLen >= 3 else 0

# Driver Code
if __name__ == "__main__":

    A = [1, 2, 3, 4, 5, 6, 7, 8] 
    n = len(A) 
    print(LongestFibSubseq(A, n)) 

# This code is contributed 
# by Rituraj Jain

```

## C#

```cs

// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG 
{ 

    // Function to return the max Length of 
    // Fibonacci subsequence 
    static int LongestFibSubseq(int []A, int n)
    { 
        // Store all array elements in a hash 
        // table 
        SortedSet<int> S = new SortedSet<int>(); 
        foreach (int t in A) 
        { 
            // Add each element into the set 
            S.Add(t); 
        } 
        int maxLen = 0, x, y; 

        for (int i = 0; i < n; ++i)
        { 
            for (int j = i + 1; j < n; ++j) 
            { 
                x = A[j]; 
                y = A[i] + A[j]; 
                int length = 3; 

                // check until next fib element is found 
                while (S.Contains(y) && y != last(S))
                { 

                    // next element of fib subseq 
                    int z = x + y; 
                    x = y; 
                    y = z; 
                    maxLen = Math.Max(maxLen, ++length); 
                } 
            } 
        } 
        return maxLen >= 3 ? maxLen : 0; 
    } 

    static int last(SortedSet<int> S)
    {
        int ans = 0;
        foreach(int a in S)
            ans = a;
        return ans;
    }

    // Driver Code
    public static void Main(String[] args) 
    { 
        int []A = {1, 2, 3, 4, 5, 6, 7, 8}; 
        int n = A.Length; 
        Console.Write(LongestFibSubseq(A, n)); 
    } 
} 

// This code is contributed by 29AjayKumar

```

**Output**

```
5
```

**时间复杂度**：O（N <sup>2</sup> * log（M）），其中 N 是数组的长度，M 是 max（A）。

**高效方法**：为了优化上述方法，该想法是实现[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。 初始化代表斐波那契序列长度的 dp 表 dp [a，b]以（a，b）结尾。 然后将表更新为 dp [a，b] =（dp [b – a，a] + 1）或 2

下面是上述方法的实现：

## C++

```cpp

// CPP program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the max Length of
// Fibonacci subsequence
int LongestFibSubseq(int A[], int n)
{
    // Initialize the unordered map
    unordered_map<int, int> m;
    int N = n, res = 0;

    // Initialize dp table
    int dp[N][N];

    // Iterate till N
    for (int j = 0; j < N; ++j) {
        m[A[j]] = j;
        for (int i = 0; i < j; ++i) {
            // Check if the current integer
            // forms a finonacci sequence
            int k = m.find(A[j] - A[i]) == m.end()
                        ? -1
                        : m[A[j] - A[i]];

            // Update the dp table
            dp[i][j] = (A[j] - A[i] < A[i] && k >= 0)
                           ? dp[k][i] + 1
                           : 2;
            res = max(res, dp[i][j]);
        }
    }

    // Return the answer
    return res > 2 ? res : 0;
}

// Driver program
int main()
{
    int A[] = { 1, 3, 7, 11, 12, 14, 18 };
    int n = sizeof(A) / sizeof(A[0]);
    cout << LongestFibSubseq(A, n);
    return 0;
}

```

**Output**

```
3
```

**时间复杂度**：O（N <sup>2</sup> ），其中 N 是数组的长度。



* * *

* * *




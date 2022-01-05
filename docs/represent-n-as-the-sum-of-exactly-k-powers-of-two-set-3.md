# 将 N 表示为 2 的 K 次方之和|集合 3

> 原文:[https://www . geeksforgeeks . org/representative-n-as-the-n-as-sum-of-k-power-of-two-set-3/](https://www.geeksforgeeks.org/represent-n-as-the-sum-of-exactly-k-powers-of-two-set-3/)

给定两个整数 **N** 和 **K** ，任务是寻找是否有可能将 **N** 表示为**2**T11】的精确**K**T8】次幂之和。如果可能，则打印 **K** 正整数，使其为 **2** 的幂，且其和正好等于 **N** 。否则，打印“**不可能”**。如果有多个答案，请打印任何一个。

**示例:**

> ***输入:** N = 5，K = 2*
> ***输出:** 4 1*
> ***解释:***
> *将 N 表示为 2 的幂的 K 个数的唯一方式是{4，1}。*
> 
> ***输入:** N = 7，K = 4*
> ***输出:** 4 1 1 1*
> ***解释:***
> *将 N 表示为 2 的 K 次幂的可能方式有{4，1，1，1}和{2，2，1}。*

[**优先级队列**](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/) **基于方法:**参考[这篇](https://www.geeksforgeeks.org/find-k-numbers-which-are-powers-of-2-and-have-sum-n/)文章使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)解决问题。

[**递归**](https://www.geeksforgeeks.org/recursion/) **方法:**参考[这篇](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)文章使用[递归](https://www.geeksforgeeks.org/recursion/)解决问题。

**交替法:**思路是用[贪婪法](https://www.geeksforgeeks.org/greedy-algorithms/)解决这个问题。以下是步骤:

*   初始化一个整数，比如说 **num = 31** ，和一个整数的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说 **res** ，来存储 **K** 数，它们是[的 2 次方](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)。
*   检查 N 中的[位数是否大于 **K** 或者 **N** 是否小于 **K、**，然后打印**“不可能”。**](https://www.geeksforgeeks.org/count-total-bits-number/)
*   当**数≥ 0 且 K > 0:** 时迭代
    *   检查**N–2<sup>num</sup>T3】是否小于**K–1**。如果发现为真，则将**号**减 1，继续。**
    *   否则，将 **K** 减少 1，将 **N** 减少 **2 <sup>num</sup>** 并将 **num** 推入矢量 **res** 。
*   最后，打印矢量 **res** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find K numbers with
// sum N that are powers of 2
void nAsKPowersOfTwo(int N, int K)
{
    // Count the number of set bits
    int x = __builtin_popcount(N);

    // Not-possible condition
    if (K < x || K > N) {
        cout << "Impossible";
        return;
    }

    int num = 31;

    // To store K numbers
    // which are powers of 2
    vector<int> res;

    // Traverse while num >= 0
    while (num >= 0 && K) {

        // Calculate current bit value
        int val = pow(2, num);

        // Check if remaining N
        // can be represented as
        // K-1 numbers that are
        // power of 2
        if (N - val < K - 1) {

            // Decrement num by one
            --num;
            continue;
        }

        // Decrement K by one
        --K;

        // Decrement N by val
        N -= val;

        // Push the num in the
        // vector res
        res.push_back(num);
    }

    // Print the vector res
    for (auto x : res)
        cout << pow(2, x) << " ";
}

// Driver Code
int main()
{
    // Given N & K
    int N = 7, K = 4;

    // Function Call
    nAsKPowersOfTwo(N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find K numbers with
// sum N that are powers of 2
static void nAsKPowersOfTwo(int N, int K)
{

    // Count the number of set bits
    int x = Integer.bitCount(N);

    // Not-possible condition
    if (K < x || K > N)
    {
        System.out.print("Impossible");
        return;
    }

    int num = 31;

    // To store K numbers
    // which are powers of 2
    Vector<Integer> res = new Vector<Integer>();

    // Traverse while num >= 0
    while (num >= 0 && K > 0)
    {

        // Calculate current bit value
        int val = (int) Math.pow(2, num);

        // Check if remaining N
        // can be represented as
        // K-1 numbers that are
        // power of 2
        if (N - val < K - 1)
        {

            // Decrement num by one
            --num;
            continue;
        }

        // Decrement K by one
        --K;

        // Decrement N by val
        N -= val;

        // Push the num in the
        // vector res
        res.add(num);
    }

    // Print the vector res
    for (int i : res)
        System.out.print((int)Math.pow(2, i)+ " ");
}

// Driver Code
public static void main(String[] args)
{
    // Given N & K
    int N = 7, K = 4;

    // Function Call
    nAsKPowersOfTwo(N, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find K numbers with
# sum N that are powers of 2
def nAsKPowersOfTwo(N, K):

    # Count the number of set bits
    x = bin(N).count('1')

    # Not-possible condition
    if (K < x or K > N):
        cout << "Impossible"
        return
    num = 31

    # To store K numbers
    # which are powers of 2
    res = []

    # Traverse while num >= 0
    while (num >= 0 and K):

        # Calculate current bit value
        val = pow(2, num)

        # Check if remaining N
        # can be represented as
        # K-1 numbers that are
        # power of 2
        if (N - val < K - 1):

            # Decrement num by one
            num -= 1
            continue

        # Decrement K by one
        K -= 1

        # Decrement N by val
        N -= val

        # Push the num in the
        # vector res
        res.append(num)

    # Print vector res
    for x in res:
        print(pow(2, x), end = " ")

# Driver Code
if __name__ == '__main__':

    # Given N & K
    N, K = 7, 4

    # Function Call
    nAsKPowersOfTwo(N, K)

# This code is contributed mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find K numbers with
// sum N that are powers of 2
static void nAsKPowersOfTwo(int N, int K)
{

    // Count the number of set bits
    int x = countSetBits(N);

    // Not-possible condition
    if (K < x || K > N)
    {
        Console.Write("Impossible");
        return;
    }

    int num = 31;

    // To store K numbers
    // which are powers of 2
    List<int> res = new List<int>();

    // Traverse while num >= 0
    while (num >= 0 && K > 0)
    {

        // Calculate current bit value
        int val = (int) Math.Pow(2, num);

        // Check if remaining N
        // can be represented as
        // K-1 numbers that are
        // power of 2
        if (N - val < K - 1)
        {

            // Decrement num by one
            --num;
            continue;
        }

        // Decrement K by one
        --K;

        // Decrement N by val
        N -= val;

        // Push the num in the
        // vector res
        res.Add(num);
    }

    // Print the vector res
    foreach (int i in res)
        Console.Write((int)Math.Pow(2, i)+ " ");
}
static int countSetBits(long x)
{
    int setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver Code
public static void Main(String[] args)
{
    // Given N & K
    int N = 7, K = 4;

    // Function Call
    nAsKPowersOfTwo(N, K);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
//Javascript program for
//the above approach

// Function to find K numbers with
// sum N that are powers of 2
function nAsKPowersOfTwo(N, K)
{
    // Count the number of set bits
    var x = countSetBits(N);

    // Not-possible condition
    if (K < x || K > N)
    {
        document.write("Impossible");
        return;
    }

    var num = 31;

    // To store K numbers
    // which are powers of 2
    var res=[];

    // Traverse while num >= 0
    while (num >= 0 && K > 0)
    {

        // Calculate current bit value
        var val = parseInt( Math.pow(2, num));

        // Check if remaining N
        // can be represented as
        // K-1 numbers that are
        // power of 2
        if (N - val < K - 1)
        {

            // Decrement num by one
            --num;
            continue;
        }

        // Decrement K by one
        --K;

        // Decrement N by val
        N -= val;

        // Push the num in the
        // vector res
        res.push(num);
    }

    // Print the vector res
    for(var i = 0;i<res.length;i++){
        document.write(parseInt(Math.pow(2, res[i]))+ " ");
    }
}
function countSetBits(x)
{
    var setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

var N = 7, K = 4;
// Function Call
nAsKPowersOfTwo(N, K);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
4 1 1 1
```

***时间复杂度:**O(32)*
T5**辅助空间:** O(1)
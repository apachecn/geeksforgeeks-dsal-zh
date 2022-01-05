# 生成前 N 个自然数的排列，其唯一相邻差的计数等于 K |集合 2

> 原文:[https://www . geesforgeks . org/generate-a-排列第一个 n 个自然数-有-计数-唯一-相邻-差异-等于-k-set-2/](https://www.geeksforgeeks.org/generate-a-permutation-of-first-n-natural-numbers-having-count-of-unique-adjacent-differences-equal-to-k-set-2/)

给定两个正整数 **N** 和 **K** ，任务是构造第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)的[排列](https://www.geeksforgeeks.org/permutation-and-combination/)，使得相邻元素之间所有可能的绝对差都是 **K** 。

**示例:**

> ***输入:** N = 3，K = 1*
> ***输出:** 1 2 3*
> ***说明:**考虑到排列{1，2，3}，所有可能的相邻元素唯一绝对差为{1}。由于计数为 1(= K)，打印序列{1，2，3}作为结果排列。*
> 
> ***输入:** N = 3，K = 2*
> T5**输出:** 1 3 2

这个问题的天真方法和[两点](https://www.geeksforgeeks.org/two-pointers-technique/)方法已经在[这里](https://www.geeksforgeeks.org/generate-a-permutation-of-first-n-natural-numbers-having-count-of-unique-adjacent-differences-equal-to-k/)讨论过了。本文讨论了一种不同的方法[德清](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)。

**方法:**很容易看出，可以生成**【1，N-1】**之间的 **K** 的所有值的答案。对于这个范围之外的任何 **K** ，都不存在答案。为了解决这个问题，为所有当前元素维护一个[双端队列](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)和一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)来存储序列。此外，保持一个布尔值，这将有助于确定弹出前面或后面的元素。迭代剩余元素，如果 **K** 大于 **1** ，则根据布尔值推元素，将 **K** 减少 **1** 。翻转布尔值，以便所有剩余的差异都有值 **1** 。按照以下步骤解决问题:

*   如果 **K** 大于等于 **N** 或小于 **1，**则打印 **-1** 并返回，因为不存在这样的序列。
*   [初始化一个德格](https://www.geeksforgeeks.org/deque-cpp-stl/) **dq[]** 来维持元素的顺序。
*   [使用变量 **i** 和](https://www.geeksforgeeks.org/range-based-loop-c/)[将 **i** 推入德格**dq【】**](https://www.geeksforgeeks.org/dequefront-dequeback-c-stl/)**的后面，迭代范围**【2，N】**。**
*   将布尔变量**前面的**初始化为**真。**
*   [初始化一个向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **ans[]** 存储答案[将 **1** 推入向量](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/) **ans[]。**
*   如果 **K** 大于 **1，**则从 **K** 和[中减去 **1** ，将**前面的**值与 **1 进行异或。**](http://www.geeksforgeeks.org/calculate-xor-1-n/)
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【2，N】**并检查:
    *   如果**前面**是 **1** ，那么[弹出德格](https://www.geeksforgeeks.org/dequepop_front-dequepop_back-c-stl/)**dq【】**的前面，推入矢量**ans【】**否则[弹出德格](https://www.geeksforgeeks.org/dequepop_front-dequepop_back-c-stl/)的后面**dq【】**推入矢量**ans【】**。另外，如果 **K** 大于，则从 **K** 和[中减去 **1** ，将**前面的**的值与 **1 异或。**](http://www.geeksforgeeks.org/calculate-xor-1-n/)
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**ans【】**并打印其元素。

下面是上述方法的实现。

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the required array
void K_ValuesArray(int N, int K)
{

    // Check for base cases
    if (K < 1 || K >= N) {
        cout << -1;
        return;
    }

    // Maintain a deque to store the
    // elements from [1, N];
    deque<int> dq;
    for (int i = 2; i <= N; i++) {
        dq.push_back(i);
    }

    // Maintain a boolean value which will
    // tell from where to pop the element
    bool front = true;

    // Create a vector to store the answer
    vector<int> ans;

    // Push 1 in the answer initially
    ans.push_back(1);

    // Push the remaining elements
    if (K > 1) {
        front ^= 1;
        K--;
    }

    // Iterate over the range
    for (int i = 2; i <= N; i++) {
        if (front) {
            int val = dq.front();
            dq.pop_front();

            // Push this value in
            // the ans vector
            ans.push_back(val);
            if (K > 1) {
                K--;

                // Flip the boolean
                // value
                front ^= 1;
            }
        }
        else {
            int val = dq.back();
            dq.pop_back();

            // Push value in ans vector
            ans.push_back(val);
            if (K > 1) {
                K--;

                // Flip boolean value
                front ^= 1;
            }
        }
    }

    // Print Answer
    for (int i = 0; i < N; i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    int N = 7, K = 1;
    K_ValuesArray(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;
class GFG{

// Function to calculate the required array
static void K_ValuesArray(int N, int K)
{

    // Check for base cases
    if (K < 1 || K >= N) {
        System.out.print(-1);
        return;
    }

    // Maintain a deque to store the
    // elements from [1, N];
    Deque<Integer> dq = new LinkedList<Integer>();
    for (int i = 2; i <= N; i++) {
        dq.add(i);
    }

    // Maintain a boolean value which will
    // tell from where to pop the element
    boolean front = true;

    // Create a vector to store the answer
    Vector<Integer> ans = new Vector<Integer>();

    // Push 1 in the answer initially
    ans.add(1);

    // Push the remaining elements
    if (K > 1) {
        front ^=true;
        K--;
    }

    // Iterate over the range
    for (int i = 2; i <= N; i++) {
        if (front) {
            int val = dq.peek();
            dq.removeFirst();

            // Push this value in
            // the ans vector
            ans.add(val);
            if (K > 1) {
                K--;

                // Flip the boolean
                // value
                front ^=true;
            }
        }
        else {
            int val = dq.getLast();
            dq.removeLast();

            // Push value in ans vector
            ans.add(val);
            if (K > 1) {
                K--;

                // Flip boolean value
                front ^=true;
            }
        }
    }

    // Print Answer
    for (int i = 0; i < N; i++) {
        System.out.print(ans.get(i)+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 7, K = 1;
    K_ValuesArray(N, K);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python Program for the above approach
from collections import deque

# Function to calculate the required array
def K_ValuesArray(N, K):

    # Check for base cases
    if (K < 1 or K >= N):
        print("-1")
        return

    # Maintain a deque to store the
    # elements from [1, N];
    dq = deque()
    for i in range(2, N + 1):
        dq.append(i)

    # Maintain a boolean value which will
    # tell from where to pop the element
    front = True

    # Create a vector to store the answer
    ans = []

    # Push 1 in the answer initially
    ans.append(1)

    # Push the remaining elements
    if (K > 1):
        front ^= 1
        K -= 1

    # Iterate over the range
    for i in range(2, N+1):
        if (front):
            val = dq.popleft()

            # Push this value in
            # the ans vector
            ans.append(val)
            if (K > 1):
                K -= 1

                # Flip the boolean
                # value
                front ^= 1

        else:
            val = dq.pop()

            # Push value in ans vector
            ans.append(val)
            if (K > 1):
                K -= 1

                # Flip boolean value
                front ^= 1

    # Print Answer
    for i in range(0, N):
        print(ans[i], end=" ")

# Driver Code
if __name__ == "__main__":

    N = 7
    K = 1
    K_ValuesArray(N, K)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# Program for the above approach

using System;
using System.Collections.Generic;
class GFG
{

    // Function to calculate the required array
    static void K_ValuesArray(int N, int K)
    {

        // Check for base cases
        if (K < 1 || K >= N)
        {
            Console.Write(-1);
            return;
        }

        // Maintain a deque to store the
        // elements from [1, N];
        LinkedList<int> dq = new LinkedList<int>();
        for (int i = 2; i <= N; i++)
        {
            dq.AddLast(i);
        }

        // Maintain a boolean value which will
        // tell from where to pop the element
        bool front = true;

        // Create a vector to store the answer
        List<int> ans = new List<int>();

        // Push 1 in the answer initially
        ans.Add(1);

        // Push the remaining elements
        if (K > 1)
        {
            front ^= true;
            K--;
        }

        // Iterate over the range
        for (int i = 2; i <= N; i++)
        {
            if (front)
            {
                int val = dq.First.Value;
                dq.RemoveFirst();

                // Push this value in
                // the ans vector
                ans.Add(val);
                if (K > 1)
                {
                    K--;

                    // Flip the boolean
                    // value
                    front ^= true;
                }
            }
            else
            {
                int val = dq.Last.Value;
                dq.RemoveLast();

                // Push value in ans vector
                ans.Add(val);
                if (K > 1)
                {
                    K--;

                    // Flip boolean value
                    front ^= true;
                }
            }
        }

        // Print Answer
        for (int i = 0; i < N; i++)
        {
            Console.Write(ans[i] + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int N = 7, K = 1;
        K_ValuesArray(N, K);

    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
// Javascript Program for the above approach

// Function to calculate the required array
function K_ValuesArray(N, K) {

    // Check for base cases
    if (K < 1 || K >= N) {
        document.write(-1);
        return;
    }

    // Maintain a deque to store the
    // elements from [1, N];
    let dq = new Array();
    for (let i = 2; i <= N; i++) {
        dq.push(i);
    }

    // Maintain a boolean value which will
    // tell from where to pop the element
    let front = true;

    // Create a vector to store the answer
    let ans = new Array();

    // Push 1 in the answer initially
    ans.push(1);

    // Push the remaining elements
    if (K > 1) {
        front ^= true;
        K--;
    }

    // Iterate over the range
    for (let i = 2; i <= N; i++) {
        if (front) {
            let val = dq[0];
            dq.shift();

            // Push this value in
            // the ans vector
            ans.push(val);
            if (K > 1) {
                K--;

                // Flip the boolean
                // value
                front ^= true;
            }
        }
        else {
            let val = dq.Last.Value;
            dq.pop();

            // Push value in ans vector
            ans.push(val);
            if (K > 1) {
                K--;

                // Flip boolean value
                front ^= true;
            }
        }
    }

    // Prlet Answer
    for (let i = 0; i < N; i++) {
        document.write(ans[i] + " ");
    }
}

// Driver Code
let N = 7, K = 1;
K_ValuesArray(N, K);

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output**

```
1 2 3 4 5 6 7 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
# 所有子阵列的最小元素之和

> 原文:[https://www . geeksforgeeks . org/所有子阵列的最小元素之和/](https://www.geeksforgeeks.org/sum-of-minimum-elements-of-all-subarrays/)

给定一个由 **n** 个整数组成的数组 **A** 。任务是找到 **A** 所有可能(邻接)子阵的最小值之和。
**举例:**

> 输入:A = [3，1，2，4]
> 输出:17
> 说明:子阵为[3]，[1]，[2]，[4]，[3，1]，[1，2]，[2，4]，[3，1，2]，[1，2，4]，[3，1，2，4]。
> 最小值是 3，1，2，4，1，1，2，1，1，1。总和是 17。
> 输入:A = [1，2，3，4]
> 输出:20

**方法:**天真的方法是生成所有可能的(连续的)子阵列，找到它们的最小值，并将其添加到结果中。时间复杂度为 0(N<sup>2</sup>)。
**有效途径:**解决问题的一般直觉是求**和(A[i] * f(i))** ，其中 **f(i)** 是子阵数，其中 **A[i]** 最小。
为了找到**f【I】**，我们需要找出:
**左【I】**、A【I】
**右【I】**左**上严格较大数的长度、A【I】**右**上较大数的长度。
我们制作左[ ]和右[ ]两个数组，使得:
**左[i] + 1** 等于以 **A[i]** 结尾的子阵个数， **A[i]** 只是单个最小值。
同样，**右[i] + 1** 等于以 **A[i]** 开始的子阵个数， **A[i]** 为第一最小值。
最后， **f(i) =(左[i]) *(右[i])** ，其中 **f[i]** 等于子阵总数，其中 **A[i]** 最小. x
以下是上述方法的实现** 

## C++

```
// CPP implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return required minimum sum
int sumSubarrayMins(int A[], int n)
{
    int left[n], right[n];

    stack<pair<int, int> > s1, s2;

    // getting number of element strictly larger
    // than A[i] on Left.
    for (int i = 0; i < n; ++i) {
        int cnt = 1;

        // get elements from stack until element
        // greater than A[i] found
        while (!s1.empty() && (s1.top().first) > A[i]) {
            cnt += s1.top().second;
            s1.pop();
        }

        s1.push({ A[i], cnt });
        left[i] = cnt;
    }

    // getting number of element larger than A[i] on Right.
    for (int i = n - 1; i >= 0; --i) {
        int cnt = 1;

        // get elements from stack until element greater
        // or equal to A[i] found
        while (!s2.empty() && (s2.top().first) >= A[i]) {
            cnt += s2.top().second;
            s2.pop();
        }

        s2.push({ A[i], cnt });
        right[i] = cnt;
    }

    int result = 0;

    // calculating required resultult
    for (int i = 0; i < n; ++i)
        result = (result + A[i] * left[i] * right[i]);

    return result;
}

// Driver program
int main()
{
    int A[] = { 3, 1, 2, 4 };

    int n = sizeof(A) / sizeof(A[0]);

    // function call to get required resultult
    cout << sumSubarrayMins(A, n);

    return 0;
}
// This code is written by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to return required minimum sum
static int sumSubarrayMins(int A[], int n)
{
    int []left = new int[n];
    int []right = new int[n];

    Stack<pair> s1 = new Stack<pair>();
    Stack<pair> s2 = new Stack<pair>();

    // getting number of element strictly larger
    // than A[i] on Left.
    for (int i = 0; i < n; ++i)
    {
        int cnt = 1;

        // get elements from stack until element
        // greater than A[i] found
        while (!s1.isEmpty() &&
               (s1.peek().first) > A[i])
        {
            cnt += s1.peek().second;
            s1.pop();
        }

        s1.push(new pair(A[i], cnt));
        left[i] = cnt;
    }

    // getting number of element larger
    // than A[i] on Right.
    for (int i = n - 1; i >= 0; --i)
    {
        int cnt = 1;

        // get elements from stack until element
        // greater or equal to A[i] found
        while (!s2.isEmpty() &&
               (s2.peek().first) >= A[i])
        {
            cnt += s2.peek().second;
            s2.pop();
        }

        s2.push(new pair(A[i], cnt));
        right[i] = cnt;
    }

    int result = 0;

    // calculating required resultult
    for (int i = 0; i < n; ++i)
        result = (result + A[i] * left[i] *
                                  right[i]);

    return result;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 3, 1, 2, 4 };

    int n = A.length;

    // function call to get required result
    System.out.println(sumSubarrayMins(A, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to return required minimum sum
def sumSubarrayMins(A, n):

    left, right = [None] * n, [None] * n

    # Use list as stack
    s1, s2 = [], []

    # getting number of element strictly
    # larger than A[i] on Left.
    for i in range(0, n):
        cnt = 1

        # get elements from stack until
        # element greater than A[i] found
        while len(s1) > 0 and s1[-1][0] > A[i]:
            cnt += s1[-1][1]
            s1.pop()

        s1.append([A[i], cnt])
        left[i] = cnt

    # getting number of element
    # larger than A[i] on Right.
    for i in range(n - 1, -1, -1):
        cnt = 1

        # get elements from stack until
        # element greater or equal to A[i] found
        while len(s2) > 0 and s2[-1][0] >= A[i]:
            cnt += s2[-1][1]
            s2.pop()

        s2.append([A[i], cnt])
        right[i] = cnt

    result = 0

    # calculating required resultult
    for i in range(0, n):
        result += A[i] * left[i] * right[i]

    return result

# Driver Code
if __name__ == "__main__":

    A = [3, 1, 2, 4]
    n = len(A)

    # function call to get
    # required resultult
    print(sumSubarrayMins(A, n))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to return required minimum sum
static int sumSubarrayMins(int []A, int n)
{
    int []left = new int[n];
    int []right = new int[n];

    Stack<pair> s1 = new Stack<pair>();
    Stack<pair> s2 = new Stack<pair>();

    // getting number of element strictly larger
    // than A[i] on Left.
    for (int i = 0; i < n; ++i)
    {
        int cnt = 1;

        // get elements from stack until element
        // greater than A[i] found
        while (s1.Count!=0 &&
            (s1.Peek().first) > A[i])
        {
            cnt += s1.Peek().second;
            s1.Pop();
        }

        s1.Push(new pair(A[i], cnt));
        left[i] = cnt;
    }

    // getting number of element larger
    // than A[i] on Right.
    for (int i = n - 1; i >= 0; --i)
    {
        int cnt = 1;

        // get elements from stack until element
        // greater or equal to A[i] found
        while (s2.Count != 0 &&
              (s2.Peek().first) >= A[i])
        {
            cnt += s2.Peek().second;
            s2.Pop();
        }

        s2.Push(new pair(A[i], cnt));
        right[i] = cnt;
    }

    int result = 0;

    // calculating required resultult
    for (int i = 0; i < n; ++i)
        result = (result + A[i] * left[i] *
                                  right[i]);

    return result;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 3, 1, 2, 4 };

    int n = A.Length;

    // function call to get required result
    Console.WriteLine(sumSubarrayMins(A, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Function to return required minimum sum
function sumSubarrayMins(A, n)
{
    var left = Array(n), right = Array(n);

    var s1 = [], s2 = [];

    // getting number of element strictly larger
    // than A[i] on Left.
    for (var i = 0; i < n; ++i) {
        var cnt = 1;

        // get elements from stack until element
        // greater than A[i] found
        while (s1.length!=0 && (s1[s1.length-1][0]) > A[i]) {
            cnt += s1[s1.length-1][1];
            s1.pop();
        }

        s1.push([A[i], cnt]);
        left[i] = cnt;
    }

    // getting number of element larger than A[i] on Right.
    for (var i = n - 1; i >= 0; --i) {
        var cnt = 1;

        // get elements from stack until element greater
        // or equal to A[i] found
        while (s2.length!=0 && (s2[s2.length-1][0]) >= A[i]) {
            cnt += s2[s2.length-1][1];
            s2.pop();
        }

        s2.push([A[i], cnt]);
        right[i] = cnt;
    }

    var result = 0;

    // calculating required resultult
    for (var i = 0; i < n; ++i)
        result = (result + A[i] * left[i] * right[i]);

    return result;
}

// Driver program

var A = [3, 1, 2, 4];
var n = A.length;

// function call to get required resultult
document.write( sumSubarrayMins(A, n));

</script>
```

**Output**

```
17
```

**时间复杂度:** O(N)，其中 N 为 a 的长度。
T3】空间复杂度: O(N)。

**另一种方法**:

这是一种**动态编程方法**。

首先，使用堆栈计算每个索引右侧的下一个较小的元素索引。

在任何索引 I 处，dp[i]表示从索引 I 开始的所有子阵列的总和。

为了计算每个指数的答案，将有两种情况:

1.  当前元素是右侧所有元素中最小的元素。所以 ans 会是(**curr _ index * arr[curr _ index]**的范围)。因为它将是从 curr_index 开始的所有子阵列中的**最小元素**。

*   右边有一个元素，比当前元素小。较小元素的答案已经存储在 dp 中。只需计算从当前索引到较小的右索引的答案。
    *   **up _ small**=(right _ index–curr_index)* arr[curr _ index]# #从 curr _ index 求和到 right smaller index。
    *   **curr _ sum**= up _ small+DP[right _ index]

最后，返回总和(dp)。

例如:- **arr = [4，3，6]**

**dp[6]** = 6

**DP[3]**=>(3-1)* 3 =>6 #最小元素

**DP[4]**=(1-0)*(4)+DP[3]=>4+6 =>10

**最终答案** = 6 + 6 + 10= 22

## 蟒蛇 3

```
def sumSubarrayMins(arr, n):

    dp = [0]*(n)

    # calculate right smaller element
    right = [i for i in range(n)] 
    stack = [0]

    for i in range(1,n,1):

        curr = arr[i]
        while(stack and curr < arr[stack[-1]]):

            idx = stack.pop()
            right[idx] = i

        stack.append(i)

    dp[-1] = arr[-1]

    for i in range(n-2,-1,-1):

        right_idx = right[i]    
        if right_idx == i:     # case 1

            curr = (n-i)*arr[i]
            dp[i] = curr

        else:   # case 2

            # sum upto next smaller rhs element
            upto_small = (right_idx-i)*(arr[i])  

            curr_sum = (upto_small + dp[right_idx])
            dp[i] = curr_sum

    return (sum(dp))

# Driver Code
if __name__ == "__main__":
    A = [3, 1, 2, 4]
    n = len(A)

    # function call to get
    # required resultult
    print(sumSubarrayMins(A, n))
```

**Output**

```
17

```

**时空复杂度** := **O(N)**
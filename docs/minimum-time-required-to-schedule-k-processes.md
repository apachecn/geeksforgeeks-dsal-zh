# 安排 K 个流程所需的最短时间

> 原文:[https://www . geeksforgeeks . org/最短时间要求调度 k 进程/](https://www.geeksforgeeks.org/minimum-time-required-to-schedule-k-processes/)

给定一个正整数 **K** 和一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，使得**arr【I】**是处理器可以在 **1 秒**内调度的进程数 **i <sup>th</sup>** 。任务是最小化调度 **K** 过程所需的总时间，使得在由**I<sup>th</sup>T21】处理器调度之后，**arr【I】**减少到[**floor(arr【I】/2)**](https://www.geeksforgeeks.org/find-floor-ceil-unsorted-array/)。**

**示例:**

> **输入:** N = 5，arr[] = {3，1，7，2，4}，K = 15
> **输出:** 4
> **说明:**
> 预定流程顺序如下:
> 
> 1.  首先安排第 3 <sup>次</sup>流程。数组 arr[]修改为{3，1，3，2，4}，因为 arr[2]= floor(arr[2]/2)= floor(7/2)= 3。
> 2.  接下来安排第 5<sup>流程。arr[]数组修改为{3，1，3，2，2}。</sup>
> 3.  接下来安排 1 <sup>st</sup> 流程。arr[]数组修改为{1，1，3，2，2}。
> 4.  接下来安排第二个<sup>和第一个</sup>过程。数组 arr[]修改为{3，0，3，2，4}。
> 
> 所有进程调度的总进程数= 7 + 4 + 3 + 1 = 15(= K)，所需总时间为 4 秒。
> 
> **输入:** N = 4，arr[] = {1，5，8，6}，K = 10
> T3】输出: 2

**天真法:**解决给定问题最简单的方法是[对给定列表进行升序排序](https://www.geeksforgeeks.org/sort-in-python/)选择能力最高的处理器，将 **K** 的值减少该值，从列表中删除该处理器，再将该处理器的一半添加到排序列表中。重复以上过程，直到**至少安排 K 个**过程，并打印安排**至少 K 个**过程后所需的时间。

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)的概念进行优化。按照以下步骤解决问题:

*   初始化给定数组中存在的[最大元素大小的辅助数组 **tmp[]** 。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   初始化一个变量，说**计数**分别存储调度所有进程的最短时间。
*   [从头到尾遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **tmp[]** ，并执行以下步骤:
    *   如果 **tmp[]** 中的电流元素大于 **0** ， **i * tmp[i]** 小于 **K** 。
        *   将 **K** 的值减少**I * tmp【I】**的值。
        *   将 **tmp[i/2]** 增加 **tmp[i]** ，因为处理器的能力会减半。
        *   将**计数**的值增加**tmp【I】**的值。
        *   如果 **K** 的值已经小于或等于 **0** ，则打印**的值计算**作为结果。
    *   如果数组 **tmp[]** 中的当前元素至少为 **0** ，并且 **i * tmp[i]** 的值至少为**K**，则执行以下步骤:
        *   如果 **K** 可被当前指数整除，那么将**计数**的值增加 **K / i** 。
        *   否则，将**计数**的值增加 **K/i +1** 。
*   完成上述步骤后，如果无法安排所有流程，打印 **-1** 。否则，打印**计数**作为所需的最短时间。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum required
// time to schedule all process
int minTime(int A[], int n, int K)
{

    // Stores max element from A[]
    int max_ability = A[0];

    // Find the maximum element
    for(int i = 1; i < n; i++)
    {
        max_ability = max(max_ability, A[i]);
    }

    // Stores frequency of each element
    int tmp[max_ability + 1] = {0};

    // Stores minimum time required
    // to schedule all process
    int count = 0;

    // Count frequencies of elements
    for(int i = 0; i < n; i++)
    {
        tmp[A[i]]++;
    }

    // Find the minimum time
    for(int i = max_ability; i >= 0; i--)
    {
        if (tmp[i] != 0)
        {
            if (tmp[i] * i < K)
            {

                // Decrease the value
                // of K
                K -= (i * tmp[i]);

                // Increment tmp[i/2]
                tmp[i / 2] += tmp[i];

                // Increment the count
                count += tmp[i];

                // Return count, if all
                // process are scheduled
                if (K <= 0)
                {
                    return count;
                }
            }

            else
            {

                // Increment count
                if (K % i != 0)
                {
                    count += (K / i) + 1;
                }
                else
                {
                    count += (K / i);
                }

                // Return the count
                return count;
            }
        }
    }

    // If it is not possible to
    // schedule all process
    return -1;
}

// Driver code
int main()
{
    int arr[] = { 3, 1, 7, 2, 4 };
    int N = 5;
    int K = 15;

    cout << minTime(arr, N, K);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to find minimum required
    // time to schedule all process
    static int minTime(int[] A, int n, int K)
    {
        // Stores max element from A[]
        int max_ability = A[0];

        // Find the maximum element
        for (int i = 1; i < n; i++) {
            max_ability = Math.max(
                max_ability, A[i]);
        }

        // Stores frequency of each element
        int tmp[] = new int[max_ability + 1];

        // Stores minimum time required
        // to schedule all process
        int count = 0;

        // Count frequencies of elements
        for (int i = 0; i < n; i++) {
            tmp[A[i]]++;
        }

        // Find the minimum time
        for (int i = max_ability;
             i >= 0; i--) {

            if (tmp[i] != 0) {

                if (tmp[i] * i < K) {

                    // Decrease the value
                    // of K
                    K -= (i * tmp[i]);

                    // Increment tmp[i/2]
                    tmp[i / 2] += tmp[i];

                    // Increment the count
                    count += tmp[i];

                    // Return count, if all
                    // process are scheduled
                    if (K <= 0) {
                        return count;
                    }
                }

                else {

                    // Increment count
                    if (K % i != 0) {
                        count += (K / i) + 1;
                    }
                    else {
                        count += (K / i);
                    }

                    // Return the count
                    return count;
                }
            }
        }

        // If it is not possible to
        // schedule all process
        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 3, 1, 7, 2, 4 };
        int N = arr.length;
        int K = 15;
        System.out.println(
            minTime(arr, N, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum required
# time to schedule all process
def minTime(A, n, K):

    # Stores max element from A[]
    max_ability = A[0]

    # Find the maximum element
    for i in range(1, n):
        max_ability = max(max_ability, A[i])

    # Stores frequency of each element
    tmp = [0 for i in range(max_ability + 1)]

    # Stores minimum time required
    # to schedule all process
    count = 0

    # Count frequencies of elements
    for i in range(n):
        tmp[A[i]] += 1

    # Find the minimum time
    i = max_ability

    while(i >= 0):
        if (tmp[i] != 0):
            if (tmp[i] * i < K):

                # Decrease the value
                # of K
                K -= (i * tmp[i])

                # Increment tmp[i/2]
                tmp[i // 2] += tmp[i]

                # Increment the count
                count += tmp[i]

                # Return count, if all
                # process are scheduled
                if (K <= 0):
                    return count
            else:

                # Increment count
                if (K % i != 0):
                    count += (K // i) + 1
                else:
                    count += (K // i)

                # Return the count
                return count
        i -= 1

    # If it is not possible to
    # schedule all process
    return -1

# Driver code
if __name__ == '__main__':

    arr = [ 3, 1, 7, 2, 4 ]
    N = 5
    K = 15

    print(minTime(arr, N, K))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find minimum required
// time to schedule all process
static int minTime(int[] A, int n, int K)
{

    // Stores max element from A[]
    int max_ability = A[0];

    // Find the maximum element
    for(int i = 1; i < n; i++)
    {
        max_ability = Math.Max(
            max_ability, A[i]);
    }

    // Stores frequency of each element
    int []tmp = new int[max_ability + 1];

    // Stores minimum time required
    // to schedule all process
    int count = 0;

    // Count frequencies of elements
    for(int i = 0; i < n; i++)
    {
        tmp[A[i]]++;
    }

    // Find the minimum time
    for(int i = max_ability; i >= 0; i--)
    {
        if (tmp[i] != 0)
        {
            if (tmp[i] * i < K)
            {

                // Decrease the value
                // of K
                K -= (i * tmp[i]);

                // Increment tmp[i/2]
                tmp[i / 2] += tmp[i];

                // Increment the count
                count += tmp[i];

                // Return count, if all
                // process are scheduled
                if (K <= 0)
                {
                    return count;
                }
            }

            else
            {

                // Increment count
                if (K % i != 0)
                {
                    count += (K / i) + 1;
                }
                else
                {
                    count += (K / i);
                }

                // Return the count
                return count;
            }
        }
    }

    // If it is not possible to
    // schedule all process
    return -1;
}

// Driver Code
public static void Main(string[] args)
{
    int []arr = { 3, 1, 7, 2, 4 };
    int N = arr.Length;
    int K = 15;

    Console.WriteLine(minTime(arr, N, K));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

    // Function to find minimum required
    // time to schedule all process
    function minTime(A, n, K)
    {
        // Stores max element from A[]
        let max_ability = A[0];

        // Find the maximum element
        for (let i = 1; i < n; i++) {
            max_ability = Math.max(
                max_ability, A[i]);
        }

        // Stores frequency of each element
        let tmp =
        Array.from({length: max_ability + 1}, (_, i) => 0);

        // Stores minimum time required
        // to schedule all process
        let count = 0;

        // Count frequencies of elements
        for (let i = 0; i < n; i++) {
            tmp[A[i]]++;
        }

        // Find the minimum time
        for (let i = max_ability;
             i >= 0; i--) {

            if (tmp[i] != 0) {

                if (tmp[i] * i < K) {

                    // Decrease the value
                    // of K
                    K -= (i * tmp[i]);

                    // Increment tmp[i/2]
                    tmp[(i / 2)] += tmp[i];

                    // Increment the count
                    count += tmp[i];

                    // Return count, if all
                    // process are scheduled
                    if (K <= 0) {
                        return count;
                    }
                }

                else {

                    // Increment count
                    if (K % i != 0) {
                        count += Math.floor(K / i) + 1;
                    }
                    else {
                        count += Math.floor(K / i);
                    }

                    // Return the count
                    return count;
                }
            }
        }

        // If it is not possible to
        // schedule all process
        return -1;
    }

// Driver Code

     let arr = [ 3, 1, 7, 2, 4 ];
     let N = arr.length;
     let K = 15;
     document.write( minTime(arr, N, K));

</script>
```

**Output**

```
4
```

***时间复杂度:** O(M)，其中 M 为* [*阵中最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(M)*

**替代方法(使用 STL):** 在最大堆的帮助下，使用贪婪方法可以解决给定的问题。按照以下步骤解决问题:

*   初始化一个优先级队列，比如 PQ，并将给定数组的所有元素插入 PQ。
*   初始化一个变量，比如 ans 为 0，以存储得到的最大菱形。
*   迭代一个循环，直到优先级队列 PQ 不为空且 K 的值> 0:
    *   弹出优先级队列的顶部元素，并将弹出的元素添加到变量 ans 中。
    *   将弹出的元素除以 2，并将其插入优先级队列 PQ。
    *   将 K 的值减 1。
*   完成上述步骤后，打印 ans 值作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to execute k processes that can be gained in
// minimum amount of time
void executeProcesses(int A[], int N, int K)
{
    // Stores all the array elements
    priority_queue<int> pq;

    // Push all the elements to the
    // priority queue
    for (int i = 0; i < N; i++) {
        pq.push(A[i]);
    }

    // Stores the required result
    int ans = 0;

    // Loop while the queue is not
    // empty and K is positive
    while (!pq.empty() && K > 0) {

        // Store the top element
        // from the pq
        int top = pq.top();

        // Pop it from the pq
        pq.pop();

        // Add it to the answer
        ans ++;

        // Divide it by 2 and push it
        // back to the pq
        K = K - top;
        top = top / 2;
        pq.push(top);
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    int A[] = { 3, 1, 7, 4, 2 };
    int K = 15;
    int N = sizeof(A) / sizeof(A[0]);
    executeProcesses(A, N, K);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to execute k processes that
# can be gained in minimum amount of time
def executeProcesses(A, N, K):

    # Stores all the array elements
    pq = []

    # Push all the elements to the
    # priority queue
    for i in range(N):
        pq.append(A[i])

    # Stores the required result
    ans = 0
    pq.sort()

    # Loop while the queue is not
    # empty and K is positive
    while (len(pq) > 0 and K > 0):

        # Store the top element
        # from the pq
        top = pq.pop()

        # Add it to the answer
        ans += 1

        # Divide it by 2 and push it
        # back to the pq
        K -= top
        top //=2
        pq.append(top)

        pq.sort()

    # Print the answer
    print(ans)

# Driver Code
A = [ 3, 1, 7, 4, 2 ]
K = 15
N=len(A)
executeProcesses(A, N, K)

#  This code is contributed by patel2127
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to execute k processes that
// can be gained in minimum amount of time
function executeProcesses(A, N, K)
{

    // Stores all the array elements
    let pq = [];

    // Push all the elements to the
    // priority queue
    for(let i = 0; i < N; i++)
    {
        pq.push(A[i]);
    }

    // Stores the required result
    let ans = 0;
     pq.sort(function(a, b){return a - b;});

    // Loop while the queue is not
    // empty and K is positive
    while (pq.length > 0 && K > 0)
    {

        // Store the top element
        // from the pq
        let top = pq.pop();

        // Add it to the answer
        ans++;

        // Divide it by 2 and push it
        // back to the pq
        K -= top;
        top = Math.floor(top / 2);
        pq.push(top);

        pq.sort(function(a, b){return a - b;});
    }

    // Print the answer
    document.write(ans)
}

// Driver Code
let A = [ 3, 1, 7, 4, 2 ];
let K = 15;
let N = A.length;

executeProcesses(A, N, K);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
4
```

***时间复杂度*** : *O((N + K)*log N)*

***辅助空间**T3:*O(N)**
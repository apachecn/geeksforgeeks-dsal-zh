# 通过选择 K 个数组元素，然后将它们减 1，可以使总和最大化。

给定[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，该数组由 **N** 个正整数和一个整数 **K** 组成。 在一个操作中，选择一个数组元素，将其添加到总和中，然后将其递减 **1** 。 任务是打印通过执行 **K** 次操作可获得的最大和。

**示例**：

> **输入**：arr [] = {2，5}，K = 4
> **输出**：14
> **说明**：
> 执行以下操作 最大化总和的运算：
> 运算 1：选择 5，然后减少它，以便新数组变成{2，4}。
> 操作 2：选择 4，然后减小它，以便新阵列变成{2，3}。
> 操作 3：选择 3，然后减小它，以便新阵列变成{2，2}。
> 操作 4：选择 2，然后减小它，以便新阵列变成{2，1}。
> 因此，最大和为 5 + 4 + 3 + 2 = 14。
> 
> **输入**：arr [] = {2，8，4，10，6}，K = 2
> **输出**：19
> **说明**：
> 执行以下操作以使总和最大化：
> 操作 1：选择 10，然后将其减小，以便新数组变为{2，8，4，9，6}。
> 操作 2：选择 9，然后减小它，以便新阵列变成{2，8，4，4，8}。
> 因此，最大和为 10 + 9 = 19。

**天真的方法**：最简单的方法是每次使用[最大堆](https://www.geeksforgeeks.org/max-heap-in-java/)选择最大元素。 将最大元素加到总和，然后将其从[最大堆](https://www.geeksforgeeks.org/max-heap-in-java/)中删除，然后添加**（最大元素– 1）**。 执行此操作 **K** 并打印总和。

下面是上述方法的实现：

## C++ 14

```

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum possible
// after adding elements K times and
// decrementing each added value by 1
long maxSum(vector<int> arr, int k)
{

    // Stores the maximum sum
    long max_sum = 0;

    // Create max_heap to get
    // the maximum element
    priority_queue<int> max_heap;

    // Update the max_heap
    for(int t : arr)
        max_heap.push(t);

    // Calculate the max_sum
    while (k-- > 0) 
    {
        int tmp = max_heap.top();
        max_heap.pop();
        max_sum += tmp;
        max_heap.push(tmp - 1);
    }

    // Return the maximum sum
    return max_sum;
}

// Driver code
int main()
{

    // Given an array arr[]
    vector<int> arr = { 2, 5 };

    // Given K
    int K = 4;

    // Function Call
    cout << maxSum(arr, K);
}

// This code is contributed by mohit kumar 29

```

## Java

```java

// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find maximum possible
    // after adding elements K times and
    // decrementing each added value by 1
    public static long maxSum(int[] arr,
                              int k)
    {
        // Stores the maximum sum
        long max_sum = 0;

        // Create max_heap to get
        // the maximum element
        PriorityQueue<Integer> max_heap
            = new PriorityQueue<>(
                Collections.reverseOrder());

        // Update the max_heap
        for (int t : arr)
            max_heap.add(t);

        // Calculate the max_sum
        while (k-- > 0) {
            int tmp = max_heap.poll();
            max_sum += tmp;
            max_heap.add(tmp - 1);
        }

        // Return the maximum sum
        return max_sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given an array arr[]
        int[] arr = { 2, 5 };

        // Given K
        int K = 4;

        // Function Call
        System.out.println(maxSum(arr, K));
    }
}

```

**Output:** 

```
14

```

***时间复杂度**：O（K * log（N）），其中 N 是给定数组的长度，K 是给定的操作数。*
***辅助空间**：O（N）*

**有效方法**：的想法是通过[使用](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)[散列](https://www.geeksforgeeks.org/hashing-data-structure/)概念，存储给定数组的每个元素的频率。 请按照以下步骤解决问题：

*   创建大小为 **M +1** 的 **freq []** ，其中 **M** 是给定数组中存在的最大元素，并存储一个变量 **max_sum** **arr []** 每个元素的频率和最大可能和。
*   [从右到左遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **freq []** ，即从 **i = M** 到 **0** 。
*   将 **max_sum** 增加 **freq [i] * i** ，将 **K** 减少 **freq [i]** 并增加 **freq [i – 1，如果 **K≥freq [i]** ，则**为 **freq [i]** 。
*   否则将 **max_sum** 递增 **i * K** ，并中断循环，因为 **K** 变为 **0** 。
*   返回 **max_sum** 作为最大可能和。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find maximum possible
    // after adding elements K times and
    // decrementing each added value by 1
    public static long maxSum(int[] arr,
                              int k)
    {
        // Stores the maximum sum
        long max_sum = 0;

        // Stores freqency of element
        int[] freq = new int[100000 + 1];

        // Update freqency of array element
        for (int t : arr)
            freq[t]++;

        // Traverse from right to left in
        // freq[] to find maximum sum
        for (int i = 100000; i > 0; i--) {

            if (k >= freq[i]) {

                // Update max_sum
                max_sum += i * freq[i];

                // Decrement k
                k -= freq[i];
                freq[i - 1] += freq[i];
            }

            // Update max_sum and break
            else {
                max_sum += i * k;
                break;
            }
        }

        // Return the maximum sum
        return max_sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int[] arr = { 2, 5 };

        // Given K
        int K = 4;

        // Function Call
        System.out.println(maxSum(arr, K));
    }
}

```

**Output:** 

```
14

```

***时间复杂度**：O（N），其中 N 是给定数组的长度。*
***辅助空间**：O（N）*



* * *

* * *




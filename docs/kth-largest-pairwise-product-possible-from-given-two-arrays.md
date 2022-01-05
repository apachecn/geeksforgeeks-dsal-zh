# 给定两个数组的第 k 个最大成对乘积

> 原文:[https://www . geeksforgeeks . org/kth-最大成对产品-可能来自给定的两个阵列/](https://www.geeksforgeeks.org/kth-largest-pairwise-product-possible-from-given-two-arrays/)

给定两个包含整数的数组 **arr[]** 和 **brr[]** 。任务是找到一对 **(arr[i]，brr[j])** 中的 **K** 最大的产品。

**示例:**

> **输入:** arr[] = {1，-2，3}，brr[] = {3，-4，0}，K = 3
> **输出:** 3
> **说明:**所有产品组合按降序排列为:【9，8，3，0，0，0，-4，-6，-12】，第三大元素为 3。
> 
> **输入:** arr[] = {-1，-5，-3}，brr[] = {-3，-4，0}，K =5
> **输出:** 4
> **说明:**所有产品组合按降序排列为:【20，15，12，9，4，3，0，0，0】第五大元素为 4。

**天真方法:**为数组**中的每个元素生成所有可能的乘积组合，数组**中的每个元素生成所有可能的乘积组合。然后对结果数组进行排序，并返回结果数组的 Kth 元素。****

## 蟒蛇 3

```
# Python program for above approach
def solve(a, b, k):
    ans = []
    n = len(a)
    m = len(b)

    for i in range(n):
        for j in range(m):

            # take product
            prod = a[i]*b[j]
            ans.append(prod)

    # Sort array in descending order
    ans.sort(reverse = True)

    # Finally return (k-1)th index
    # as indexing begans from 0.
    return (ans[k-1])

# Driver Code
arr = [1, -2, 3]
brr = [3, -4, 0]
K = 3

# Function Call
val = solve(arr, brr, K)

print(val)
```

**Output:**

```
3

```

**时间复杂度:**O(N * M+(N+M)* Log(N+M))
T3】辅助空间: O(N+M)

**高效法:**这个问题可以用[贪婪法](https://www.geeksforgeeks.org/greedy-algorithms/)和[堆](https://www.geeksforgeeks.org/heap-sort/)来解决。按照以下步骤解决给定的问题。

*   排序 **brr[]** 数组。
*   在数组**arr【】**中保留较大的数组。
*   创建一个**最大堆**来存储元素及其各自的索引。
*   遍历数组 **arr[]** 中的每个元素。元素可以是正的，也可以是负的。
*   **正**:将来自**arr【】**的当前元素与排序数组**brr【】**的**最大元素**相乘。以确保获得最大的元素。
*   **负**:在这种情况下乘以**最小值**，即数组**中的第一个元素 brr[]** 。这是由于否定的性质，因为较大的值可以通过与最小的值相乘来获得。
*   将**三个值插入堆**中，使得:**(产品，I，j )** 其中 **i & j** 是数组**arr【】**和**brr【】**的索引。
*   现在运行循环 K 次的**，从堆中弹出元素。**
*   现在检查在**arr【I】**出现的值是正还是负
*   **正数**:所以**next _ j =(current _ j–1)**因为使用了最大堆，所有较高的索引可能已经从堆中弹出。
*   **负数**:**next _ j =(current _ j+1)**因为所有产生较大元素的较小值可能已经从堆中弹出。
*   最后，返回答案

**<u>注意:</u>** Max 堆是在 **min-heap 的帮助下实现的，在 Python 中通过否定**值的符号同时**将**值插入堆中。

下面是上述方法的实现。

## 蟒蛇 3

```
# Python program for above approach
from heapq import heappush as push, heappop as pop

def solve(a, b, k):

    # Sorting array b in ascending order
    b.sort()
    n, m = len(a), len(b)

    # Checking if size(a) > size(b)

    if (n < m):

        # Otherwise swap the arrays

        return solve(b, a, k)

    heap = []

    # Tarverse all elements in array a
    for i in range(n):

        curr = a[i]

        # curr element is negative
        if (curr < 0):

            # Product with smallest value
            val = curr * b[0]

            # Pushing negative val due to max heap
            # and i as well jth index
            push(heap, (-val, i, 0))

        else:

            # Product with largest value
            val = curr * b[-1]

            # Pushing negative val due to max heap
            # and i as well jth index
            push(heap, (-val, i, m-1))

    # Subtract 1 due to zero indexing
    k = k-1

    # Remove k-1 largest items from heap
    for _ in range(k):

        val, i, j = pop(heap)
        val = -val

        # if a[i] is negative, increment ith index

        if (a[i] < 0):
            next_j = j + 1

        # if a[i] is positive, decrement jth index
        else:
            next_j = j-1

        # if index is valid
        if (0 <= next_j < m):

            new_val = a[i] * b[next_j]

            # Pushing new_val in the heap
            push(heap, (-new_val, i, next_j))

    # Finally return first val in the heap
    return -(heap[0][0])

# Driver Code
arr = [1, -2, 3]
brr = [3, -4, 0]
K = 3

# Function Call
val = solve(arr, brr, K)

# Print the result
print(val)
```

**Output:**

```
3

```

**时间复杂度:**O(M * Log(M)+K * Log(N))
T3】辅助空间: O(N)
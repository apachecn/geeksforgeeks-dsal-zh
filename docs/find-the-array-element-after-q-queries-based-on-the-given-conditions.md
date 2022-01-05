# 根据给定条件进行 Q 查询后找到数组元素

> 原文:[https://www . geeksforgeeks . org/find-the-array-element-after-q-query-基于给定条件/](https://www.geeksforgeeks.org/find-the-array-element-after-q-queries-based-on-the-given-conditions/)

给定一个长度为 **N** 和 **Q** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，查询 3 种类型(1，2，3)，其操作如下:

*   **类型 1:** 查询输入为 **1** ，任务为[反阵](https://www.geeksforgeeks.org/program-for-array-rotation-continued-reversal-algorithm/)。
*   **类型 2:** 查询输入为 **(2 x)** ，任务为在结果数组中查找 **x** 的索引。
*   **类型 3:** 查询输入为 **(3 x y)** ，任务是交换数组中索引 **x** 和 **y** 处的元素。

任务是打印**类型 2** 的查询结果。

**示例:**

> **输入:** N = 5，arr[] = {3，7，8，1，33}，Q = 4，query[][]= { { 1 }，{2，8}，{3，2，4}，{2，1 }
> T3】输出:2 1
> T6】解释:流程查询方式首先是 1，所以反转列表【33，1，8，7，3】，第二次查询 2 8，所以找到元素 8 的索引，也就是 2，第三次查询是 3 2 4，所以交换 8]现在最后一个查询是 2 1，所以查找元素 1 的索引，它是 1，所以输出 2 1。
> 
> **输入:** N = 6，arr[] = {6，33，9，22，45，4}，Q = 5，query[][]= { {1}，{3，0，4}，{2，33}，{ 1 }，{2，9}}
> **输出:** 0 2

**方法:**对于每个查询，可以基于以下假设来解决给定的问题:

*   使用变量**标志** =1，对于每一个类型为 **1** 的查询，乘以**标志** * **-1** ，对于负数，它表示列表的反转，并以相反的顺序操作计算，而不是直接反转数组，这样可以降低时间复杂度。
*   现在对于类型 **3 x y** 的查询，使用[地图数据结构](https://www.geeksforgeeks.org/hashing-data-structure/)将索引和元素存储为键和值对，并直接交换 **O(1)** 中的值。
*   最后对于 **2 x** 类型的查询，直接取索引。

按照以下步骤解决问题:

*   [初始化一个映射 **mp = {}**](https://www.geeksforgeeks.org/hash-map-in-python/) 将数组中的元素及其索引存储为**键值**对。
*   将变量**标记**初始化为 **1** ，以记录数组反转的次数。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/loops-in-python/)**【0，Q)** ，并执行以下任务:
    *   首先，检查查询的类型，同时将每个查询作为输入。
    *   对于**类型 1** 查询，不要手动反转，这样会增加时间复杂度，将变量**标志**的符号更改为表示数组正常或反转。
    *   对于**类型 2** 查询，[从地图](https://www.geeksforgeeks.org/map-find-function-in-c-stl/)中找到给定值的索引，如果数组没有反转，则打印**m【x】**的值作为结果。否则，打印**(N–m[x]–1)**的值。
    *   对于**类型 3** 查询，首先找到给定索引处的值，然后在列表和映射中分别交换值和索引。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach

# Function to perform the given queries
# and print the result accordingly
def arrayManipulation(n, arr, q, qarr):

    # Stores the index value pair
    mp = {}
    ans = []

    # Flag to indicate reversal
    flg = 1
    for i in range(n):
        mp[arr[i]] = i

    # Processing each query
    for i in range(q):
        a = qarr[i]

        # Type 1 flag multiplied -1
        if(a[0] == 1):
            flg *= -1

        # Type 2 query taking index
        # value acc. to flag sign
        elif(a[0] == 2):
            x = a[1]
            if(flg == -1):
                ans.append(n-mp[x]-1)
            else:
                ans.append(mp[x])

        # Type 3 query swaping value
        # directly in map
        else:
            x = a[1]
            y = a[2]

            # Stores the value to swap
            # and update the array
            x1 = a[1]
            y1 = a[2]
            if(flg == -1):
                y = n-y-1
                x = n-x-1

            # Value swapped and store
            # value to swap and update
            # the map
            y = arr[y]
            x = arr[x]

            # Index swapped
            arr[x1], arr[y1] = arr[y1], arr[x1]
            mp[x], mp[y] = mp[y], mp[x]

    # Print the result for queries
    print(*ans)

# Driver Code
N = 6
arr = [6, 33, 9, 22, 45, 4]
Q = 5
Queries = [[1], [3, 0, 4], [2, 33], [1], [2, 9]]

# Function Call
arrayManipulation(N, arr, Q, Queries)
```

**Output:**

```
0 2

```

***时间复杂度:** O(max(N，Q))*
***辅助空间:** O(N)*
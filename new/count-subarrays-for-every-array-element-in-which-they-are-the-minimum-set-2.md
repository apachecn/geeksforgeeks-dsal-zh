# 为每个最小的数组元素计数子数组| 设置 2

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，该数组由 **N** 个整数组成，任务是创建大小为**的数组 **brr []** N** 其中 **brr [i]** 代表其中 **arr [i]** 是最小元素的子阵列的数量。

**示例：**

> **输入：** arr [] = {3，2，4}
> **输出：** {1，3，1}
> **说明：** ]对于 arr [0]，只有一个子数组，其中 3 是最小的（{3}）。
> 对于 arr [1]，存在三个这样的子数组，其中 2 是最小的（{2}，{3、2}，{2、4}）。
> 对于 arr [2]，只有一个子数组，其中 4 最小（{4}）。
> 
> **输入：** arr [] = {1、2、3、4、5}
> **输出：** {5、4、3、2、1}

[**散列**](http://www.geeksforgeeks.org/hashing-data-structure/) **方法：** [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)找出[所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的最小元素并将其计数存储在 [映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。 请按照以下步骤解决问题：

1.  创建一个[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，以存储每个元素的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量。
2.  遍历所有可能的子数组，找到子数组中的最小元素。
3.  在**映射**中获得的最小元素的**计数**。
4.  最后，为每个数组元素打印在 **Map** 中获得的频率。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate total number
// of sub-arrays for each element
// where that element is occurring
// as the minimum element
void minSubarray(int* arr, int N)
{

    // Map for storing the number of
    // sub-arrays for each element
    unordered_map<int, int> m;

    // Traverse over all possible subarrays
    for (int i = 0; i < N; i++) {

        int mini = INT_MAX;

        for (int j = i; j < N; j++) {

            // Minimum in each subarray
            mini = min(mini, arr[j]);
            m[mini]++;
        }
    }

    // Print the result
    for (int i = 0; i < N; i++) {

        cout << m[arr[i]] << " ";
    }
}

// Driver Code
int main()
{

    int arr[] = { 3, 2, 1, 4 };
    int N = sizeof(arr) / sizeof(int);

    // Function Call
    minSubarray(arr, N);

    return 0;
}

```

## Python3

```py

# Python3 program for 
# the above approach

# Function to calculate total 
# number of sub-arrays for 
# each element where that 
# element is occurring as the 
# minimum element
def minSubarray(arr, N):

    # Map for storing the 
    # number of sub-arrays 
    # for each element
    m = {}

    # Traverse over all 
    # possible subarrays
    for i in range(N):

        mini = 10 ** 9

        for j in range(i, N):

            # Minimum in each subarray
            mini = min(mini, arr[j])
            m[mini] = m.get(mini, 0) + 1

    # Print result
    for i in arr:
        print(m[i], end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [3, 2, 1, 4]
    N = len(arr)

    # Function Call
    minSubarray(arr, N)

# This code is contributed by mohit kumar 29

```

**Output:** 

```
1 2 6 1

```

***时间复杂度：** O（N <sup>2</sup> ）*
***辅助空间：** O（1）*

**有效方法：**此方法基于[下一个较大元素](https://www.geeksforgeeks.org/next-greater-element/)和[前一个较大元素](https://www.geeksforgeeks.org/previous-greater-element/)的概念。 请按照以下步骤解决问题：

1.  为了找到元素的最小值，首先找到 **x** 和 **y** ，其中 **x** 是在左边的严格大于数字的长度。 **arr [i]** 和 **y** 是 **arr [i]** 右边较大数字的长度。
2.  因此， **x * y** 是其中 **arr [i]** 最小的子阵列的总数。
3.  要查找 **x** 和**和**，请使用[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)，其概念为[下一个更大的元素](http://www.geeksforgeeks.org/next-greater-element/)和[上一个更大的元素](https://www.geeksforgeeks.org/previous-greater-element/)。
4.  对于[下一个更大的元素](http://www.geeksforgeeks.org/next-greater-element/)，创建对对的堆栈，并将第一个数组元素和一个计数器压入以将子数组成对计数到堆栈中。
5.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并一个接一个地选取数组元素：
    *   如果当前数组元素大于堆栈 的 [**顶部元素，则对于**堆栈**中的顶部元素，当前元素为**。 下一个更大的元素**。 因此，**](https://www.geeksforgeeks.org/stack-top-c-stl/)**[从堆栈](https://www.geeksforgeeks.org/stack-pop-method-in-java/)的[顶部元素弹出](https://www.geeksforgeeks.org/stack-top-c-stl/)，然后将计数器的值递增到堆栈**的**顶部的计数器值，然后增加下一个顶部堆栈元素 与当前数组元素进行比较，依此类推。**
    *   否则，将带有计数器的当前数组元素推入堆栈，然后将计数器插入结果数组。
6.  对上一个更大的元素重复步骤 4、5。
7.  最后，打印结果。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count subarrays
// for each element where it is
// the minimum
void minSubarray(int* arr, int N)
{
    int result[N];
    stack<pair<int, int> > l, r;

    // For the length of strictly larger
    // numbers on the left of A[i]
    for (int i = 0; i < N; i++) {

        int count = 1;
        while (!l.empty()
               && l.top().first > arr[i]) {

            count += l.top().second;
            l.pop();
        }
        l.push({ arr[i], count });

        // Storing x in result[i]
        result[i] = count;
    }

    // For the length of strictly larger
    // numbers on the right of A[i]
    for (int i = N - 1; i >= 0; i--) {

        int count = 1;
        while (!r.empty()
               && r.top().first >= arr[i]) {

            count += r.top().second;
            r.pop();
        }
        r.push({ arr[i], count });

        // Store x*y in result array
        result[i] *= count;
    }

    // Print the result
    for (int i = 0; i < N; i++) {

        cout << result[i] << " ";
    }
}

// Driver Code
int main()
{

    int arr[] = { 3, 2, 1, 4 };
    int N = sizeof(arr) / sizeof(int);

    // Function Call
    minSubarray(arr, N);

    return 0;
}

```

## Python3

```py

# Python3 program for the 
# above approach

# Function to count subarrays
# for each element where it is
# the minimum
def minSubarray(arr, N):

    result = [0] * N
    l = []
    r = []

    # For the length of strictly 
    # larger numbers on the left 
    # of A[i]
    for i in range(N):
        count = 1;
        while (len(l) != 0 and
               l[-1][0] > arr[i]):
            count += l[-1][1]
            l.pop()

        l.append([arr[i], count])

        # Storing x in result[i]
        result[i] = count;

    # For the length of 
    # strictly larger
    # numbers on the 
    # right of A[i]
    for i in range(N - 1, 
                   -1, -1):
        count = 1;
        while (len(r) != 0 and
               r[-1][0] >= arr[i]):
            count += r[-1][1]
            r.pop();

        r.append([arr[i], count]);

        # Store x*y in result 
        # array
        result[i] *= count

    # Print the result
    for i in range(N):
        print(result[i], 
              end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [3, 2, 1, 4]
    N = len(arr)

    # Function Call
    minSubarray(arr, N)

# This code is contributed by Chitranayal

```

**Output:** 

```
1 2 6 1

```

***时间复杂度：** O（N）*
***辅助空间：** O（N）*



* * *

* * *




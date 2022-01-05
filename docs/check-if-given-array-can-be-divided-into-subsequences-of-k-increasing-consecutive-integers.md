# 检查给定数组是否可以分成 K 个递增的连续整数的子序列

> 原文:[https://www . geeksforgeeks . org/check-if-给定数组-可被分成 k 个连续整数的子序列/](https://www.geeksforgeeks.org/check-if-given-array-can-be-divided-into-subsequences-of-k-increasing-consecutive-integers/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是检查是否有可能将该数组划分为 **K** 个连续整数的递增的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得每个元素只能在单个子序列中起作用。

**例**:

> **输入:** arr[] = {1，2，1，3，2，3}，K = 3
> **输出:**是
> **说明:**给定数组可分为{ **1** ， **2** ，1， **3** ，2，3} = > {1，2，3}和{1，2， **1** ，3，**两个子序列都有 3 个递增顺序的连续整数。**
> 
> **输入:** arr[] = {4，3，1，2}，K = 2
> T3】输出:否

**进场:**以上问题可以使用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决。可以观察到，对于任意整数**arr【I】**，最优选择是选择子阵**arr【I+1，N)** 中**arr【I】+1**的最小索引。根据这一观察，按照以下步骤解决给定的问题:

*   如果 **K** 不是 **N** 的除数，则不存在所需子序列的可能集合。于是，印**号**。
*   将每个整数的索引存储在[集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。使用具有密钥集对结构的[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)可以有效地存储它。
*   维护一个**访问过的**数组，以跟踪已经包含在子序列中的索引。
*   [对范围[0，N)](https://www.geeksforgeeks.org/range-based-loop-c/) 中的每个 I 进行迭代，如果当前索引处的整数尚未被访问，请执行以下步骤:
    *   使用[上限](https://www.geeksforgeeks.org/stdupper_bound-in-cpp/)函数，在范围**【I+1，N】**中找到 **arr[i] + 1** 的最小索引，并用它更新当前子序列最后一个元素的值。
    *   重复上述步骤 **K-1** 多次，直到创建了完整的 **K** 整数子序列。
*   在任何迭代过程中，如果所需的整数不存在，则不存在可能的所需子序列集。因此，打印**否**。否则，打印**是**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the array can
// be divided into subsequences of K
// consecutive integers in increasing order
bool isPossible(vector<int> nums, int K)
{
    int N = nums.size();

    // If N is not divisible by K or
    // K>N, no possible set of required
    // subsequences exist
    if (N % K != 0 || K > N) {
        return false;
    }

    // Stores the indices of each
    // element in a set
    map<int, set<int> > idx;

    // Stores the index of each number
    for (int i = 0; i < nums.size(); i++) {
        idx[nums[i]].insert(i);
    }

    // Stores if the integer at current
    // index is already included in
    // a subsequence
    int visited[N] = { 0 };

    // Stores the count of total
    // visited elements
    int total_visited = 0;

    for (int i = 0; i < nums.size(); i++) {

        // If current integer is already
        // in a subsequence
        if (visited[i]) {
            continue;
        }

        // Stores the value of last element
        // of the current subsequence
        int num = nums[i];

        // Stores the index of last element
        // of the current subsequence
        int last_index = i;

        // Mark Visited
        visited[i] = 1;

        // Increment the visited count
        total_visited++;

        // Find the next K-1 elements of the
        // subsequence starting from index i
        for (int j = num + 1; j < num + K; j++) {

            // No valid index found
            if (idx[j].size() == 0) {
                return false;
            }

            // Find index of j such that it
            // is greater than last_index
            auto it = idx[j].upper_bound(last_index);

            // if no such index found,
            // return false
            if (it == idx[j].end()
                || *it <= last_index) {
                return false;
            }

            // Update last_index
            last_index = *it;

            // Mark current index as visited
            visited[last_index] = 1;

            // Increment total_visited by 1
            total_visited++;

            // Remove the index from set because
            // it has been already used
            idx[j].erase(it);
        }
    }

    // Return the result
    return total_visited == N;
}

// Driver Code
int main()
{
    vector<int> arr = { 4, 3, 1, 2 };
    int K = 2;
    cout << (isPossible(arr, K) ? "Yes" : "No");

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the array can
# be divided into subsequences of K
# consecutive integers in increasing order
def isPossible(nums, K):
    N = len(nums)

    # If N is not divisible by K or
    # K>N, no possible set of required
    # subsequences exist
    if (N % K != 0 or K > N):
        return False

     # Stores the indices of each
    # element in a set
    idx = {}

     # Stores the index of each number
    for i in range(N):
        if nums[i] in idx:
            idx[nums[i]].add(i)
        else:
            idx[nums[i]] = {i}

    # Stores if the integer at current
    # index is already included in
    # a subsequence
    visited = [0]*N

    # Stores the count of total
    # visited elements
    total_visited = 0
    for i in range(N):

        # If current integer is already
        # in a subsequence
        if(visited[i]):
            continue

        # Stores the value of last element
        # of the current subsequence
        num = nums[i]

        # Stores the index of last element
        # of the current subsequence
        last_index = i

        # Marked visited
        visited[i] = 1

         # Increment the visited count
        total_visited += 1

        # Find the next K-1 elements of the
        # subsequence starting from index i
        for j in range(num+1, num+K):

           # No valid index found
            if j not in idx or len(idx[j]) == 0:
                return False
            temp = False

            # Find index of j such that it
            # is greater than last_index
            for it in idx[j]:
                if it > last_index:
                    last_index = it
                    temp = True
                    break
            if(temp == False):
                return False

            # Update last index
            visited[last_index] = 1

            # Mark current index as visited

             # Increment total_visited by 1
            total_visited += 1

            # Remove the index
            idx[j].remove(it)

            # Return the result
    return total_visited == N

# Driver code
arr = [4, 3, 1, 2]
K = 2
if (isPossible(arr, K)):
    print("Yes")
else:
    print("No")

# This code is contributed by parthmanchanda81
```

**Output:** 

```
No
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*
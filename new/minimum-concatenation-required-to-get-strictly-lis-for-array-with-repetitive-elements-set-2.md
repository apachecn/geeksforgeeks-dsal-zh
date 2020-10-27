# 对于具有重复元素的数组，要严格获得 LIS 所需的最小连接| 第 2 组

给定大小为 n 的**数组 A []** ，其中数组中可以包含重复元素。 我们必须找到序列 A 所需的最小串联，才能严格得到最长增长子序列。 对于数组 A []，我们遵循基于 1 的索引。
**范例：**

> **输入：** A = {2，1，2，4，4，3，5}
> **输出：** 2
> **说明：**
> 我们 可以将 A 两次连接为[2，1，2，4，3，5，2，1，1，2，4，4，3，5]，然后输出索引 2、3、5、10、12 的子序列 为 1-> 2-> 3-> 4-> 5.输入
> **：** A = {1、3、2、1、2}
> **输出：** 2
> **说明：**
> 我们可以将 A 两次串联为[1、3、2、1、2、1、1、3、2、1、2 ]，然后输出索引 1、3、7，其子序列为 1-> 2-> 3。

**方法：**
为解决上述问题，第一个观察结果是严格增加的子序列的长度始终等于序列 A []中存在的唯一元素的数量。 因此，子序列的最大长度等于不同元素的数量。 要解决此问题，请执行以下步骤：

*   初始化一个变量，假设*和*设为 1，然后将序列分成两部分，即左子序列和右子序列。 将 leftSeq 初始化为 NULL，并将原始序列复制到 rightSeq 中。
*   在**的右子序列中遍历，找到由变量 *CurrElement* 表示的最小元素**并存储其索引。
*   现在**更新了左右子序列**，其中 leftSeq 用给定序列更新，直到索引将最小元素存储在右边子序列中。 以及从最小索引值到结尾的给定序列的 rightSeq。
*   遍历数组以获取下一个最小元素并更新 CurrElement 的值。 如果 rightSeq 中没有这样的最小值，则必须在 leftSeq 中。 在左子序列中找到该元素的索引并存储其索引。
*   现在**再次更新左右子序列**的值，其中 leftSeq =给定序列直到第 k 个索引，rightSeq =给定序列从第 k 个索引到结束。 重复该过程，直到达到阵列限制。
*   将**和**的值增加 1，并在 CurrElement 等于最高元素时停止。

下面是上述方法的实现：

## C++

```cpp

// CPP implementation to Find the minimum 
// concatenation required to get strictly 
// Longest Increasing Subsequence for the
// given array with repetitive elements
#include <bits/stdc++.h>
using namespace std;

int LIS(int arr[], int n)
{
    // ordered map containing value and 
    // a vector containing index of 
    // it's occurrences
    map<int, vector<int> > m;

    // Mapping index with their values 
    // in ordered map
    for (int i = 0; i < n; i++)
        m[arr[i]].push_back(i);

    // k refers to present minimum index
    int k = n;

    // Stores the number of concatenation 
    // required
    int ans = 0;

    // Iterate over map m
    for (auto it = m.begin(); it != m.end(); 
                                       it++) {
        // it.second refers to the vector
        // containing all corresponding 
        // indexes

        // it.second.back refers to the 
        // last element of corresponding vector

        if (it->second.back() < k) {
            k = it->second[0];
            ans += 1;
        }
        else

            // find the index of next minimum
            // element in the sequence
            k = *lower_bound(it->second.begin(),
                            it->second.end(), k);
    }

    // Return the final answer
    cout << ans << endl;
}

// Driver program
int main()
{
    int arr[] = { 1, 3, 2, 1, 2 };

    int n = sizeof(arr) / sizeof(arr[0]);

    LIS(arr, n);

    return 0;
}

```

## Python3

```py

# Python 3 implementation to 
# Find the minimum concatenation 
# required to get strictly Longest 
# Increasing Subsequence for the
# given array with repetitive elements
from bisect import bisect_left

def LIS(arr, n):

    # ordered map containing 
    # value and a vector containing 
    # index of it's occurrences
    # <int, vector<int> > m;
    m = {}

    # Mapping index with their 
    # values in ordered map
    for i in range(n):
        m[arr[i]] = m.get(arr[i], [])
        m[arr[i]].append(i)

    # k refers to present
    # minimum index
    k = n

    # Stores the number of 
    # concatenation required
    ans = 1

    # Iterate over map m
    for key, value in m.items():

        # it.second refers to the 
        # vector containing all 
        # corresponding indexes

        # it.second.back refers 
        # to the last element of 
        # corresponding vector
        if (value[len(value) - 1] < k):
            k = value[0]
            ans += 1
        else:

            # find the index of next 
            # minimum element in the 
            # sequence
            k = bisect_left(value, k)

    # Return the final 
    # answer
    print(ans)

# Driver code
if __name__ == '__main__':

    arr =  [1, 3, 2, 1, 2]
    n = len(arr)
    LIS(arr, n)

# This code is contributed by bgangwar59

```

**Output:** 

```
2

```

**时间复杂度：** O（n * log n）



* * *

* * *




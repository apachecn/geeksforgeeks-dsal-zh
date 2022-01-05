# 打印最长的子序列，使得相邻元素之间的差值为 K

> 原文:[https://www . geesforgeks . org/print-最长子序列-相邻元素之间的差异-is-k/](https://www.geeksforgeeks.org/print-longest-subsequence-such-that-difference-between-adjacent-elements-is-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，以及整数 **K** 。任务是找到**最长的** [子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，相邻**元素之间的**差**为 **K****

**示例**:

> **输入** : arr[] = { 5，5，5，10，8，6，12，13 }，K = 1
> **输出** : {5，6}
> 
> **输入** : arr[] = {4，6，7，8，9，8，12，14，17，15}，K = 2
> **输出** : {4，6，8}

**逼近**:任务可以借助 [**动态编程**](http://www.geeksforgeeks.org/dynamic-programming/) 解决。数组的每个元素都可以被认为是子序列的最后一个元素。对于每个元素，其思想是将相邻元素 **K** 之间有差异的**最长子序列**的**长度**和当前元素的**前身**存储在该子序列上。遵循下面提到的步骤来实施该方法。

*   创建一个地图，存储每个元素的最后一次出现。
*   创建一个由 dp[] 对组成的**数组，以存储在索引处结束的最长子序列的长度以及该索引的前身。**
*   现在，遍历数组 **arr[]** ，对于每个元素 **arr[i]** :
    *   在地图中搜索 **arr[i]-K** ， **arr[i]+K** 。
    *   如果它们存在，则找出最大长度的子序列，并将长度和前身存储在 **dp[i]** 中。
*   借助存储在数组**DP【】**中的前置序列打印最长的子序列。

下面是上述方法的实现。

## C++

```
// C++ program to iplement above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest subsequence
vector<int> maxSubsequence(vector<int>& arr, int K)
{
    int N = arr.size();

    // Declaring the dp[] array and map
    vector<pair<int, int> > dp(N, { 1, -1 });
    unordered_map<int, int> mp;
    mp[arr[0]] = 1;

    // Initialise variable to store
    // maximum length and last index of
    // the longest subsequence
    int maxlen = 1, ind = 0;

    // Loop to find out the longest
    // subsequence
    for (int i = 1; i < N; i++) {

        // If arr[i]-K is present in the part
        // of array visited till now
        if (mp.count(arr[i] - K)) {
            dp[i] = { dp[mp[arr[i] - K] - 1].first + 1,
                      mp[arr[i] - K] - 1 };
        }

        // If arr[i]+K is present in the part
        // of array visited till now
        if (mp.count(arr[i] + K)) {
            if (dp[i].first
                < dp[mp[arr[i] + K] - 1].first + 1) {
                dp[i].first
                    = dp[mp[arr[i] + K] - 1].first + 1;
                dp[i].second = mp[arr[i] + K] - 1;
            }
        }

        // If maximum length increase store
        // the length and current index as the
        // last index of longest subsequence
        if (maxlen < dp[i].first) {
            maxlen = dp[i].first;
            ind = i;
        }
        mp[arr[i]] = i + 1;
    }

    // Declare vector to store the
    // longest subsequence
    vector<int> v;

    // Loop to generate the subsequence
    while (ind >= 0) {
        v.push_back(arr[ind]);
        ind = dp[ind].second;
    }
    reverse(v.begin(), v.end());
    return v;
}

// Driver code
int main()
{
    vector<int> arr = { 4, 6, 7, 8, 9, 8, 12, 
                       14, 17, 15 };
    int K = 2;

    // Calling function to find
    // longest subsequence
    vector<int> longSubseq =
        maxSubsequence(arr, K);
    for (auto i : longSubseq)
        cout << i << " ";
    cout << endl;

    return 0;
}
```

**Output**

```
4 6 8 

```

***时间复杂度*** : O(N)
***辅助空间*** : O(N)
# 总和大于 k 的最大子阵列

> 原文:[https://www . geesforgeks . org/maximum-subarray-having-sum-大于-k/](https://www.geeksforgeeks.org/largest-subarray-having-sum-greater-than-k/)

给定一个整数数组和值 k，求和大于 k 的最大子数组的长度。

**示例:**

```
Input : arr[] = {-2, 1, 6, -3}, k = 5
Output : 2
Largest subarray with sum greater than
5 is  {1, 6}.

Input : arr[] = {2, -3, 3, 2, 0, -1}, k = 3
Output : 5
Largest subarray with sum greater than
3 is {2, -3, 3, 2, 0}.

```

 [### 推荐:请首先在 IDE 上尝试您的方法，然后查看解决方案。](https://ide.geeksforgeeks.org) 

一个**简单的**解法就是逐个考虑每个子阵，求其和。如果总和大于 k，那么将这个子阵列的长度与目前找到的最大长度进行比较。这个解的时间复杂度为 O(n <sup>2</sup> )。

一个有效的解决方案是使用前缀和和二分搜索法。其思想是遍历数组，并将前缀和以及相应的数组索引存储在一对向量中。找到前缀和后，按照前缀和的递增顺序对向量进行排序，对于前缀和相同的值，按照索引进行排序。创建另一个数组 minInd[]，其中 minInd[i]存储范围[0]内的最小索引值..i]在排序的前缀和向量中。此后，开始遍历数组 arr[]并存储子数组 arr[0]的和..总之。如果和大于 k，那么和大于 k 的最大子阵列是 arr[0..长度为 1+1。如果总和小于或等于 k，则必须将大于或等于 k + 1–总和的值添加到总和中，使其至少为 k+1。让这个值为 x。要将 x 加到 sum，-x 可以从中减去，因为 sum-(-x) = sum + x。所以前缀数组 arr[0..需要发现 j(j<I)的和至多为-x(至多为-x，因为 k+1-和是最小的值，现在取其负值，所以它将是允许的最大值)。合成子阵列 arr[j+1..应该尽可能大。为此，j 的值应该尽可能小。因此，问题简化为找到一个前缀和，其值至多为-x，并且其结束索引应该最小。为了找到前缀和，可以对前缀和向量执行二分搜索法。让索引 ind 表示在前缀和向量中，直到索引 ind 的所有前缀和值都小于或等于-x。范围[0..ind]是 minInd[ind]。如果 minInd[ind]大于 I，则不存在 sum -x 在范围[0..i-1]。否则 arr[minInd[ind]+1..i]的总和大于 k。将它的长度与迄今为止找到的最大长度进行比较。

下面是上述方法的实现:

## C++

```
// CPP program to find largest subarray
// having sum greater than k.
#include <bits/stdc++.h>
using namespace std;

// Comparison function used to sort preSum vector.
bool compare(const pair<int, int>& a, 
             const pair<int, int>& b)
{
    if (a.first == b.first)
        return a.second < b.second;

    return a.first < b.first;
}

// Function to find index in preSum vector upto which
// all prefix sum values are less than or equal to val.
int findInd(vector<pair<int, int> >& preSum, int n,
                                            int val)
{

    // Starting and ending index of search space.
    int l = 0;
    int h = n - 1;
    int mid;

    // To store required index value.
    int ans = -1;

    // If middle value is less than or equal to
    // val then index can lie in mid+1..n
    // else it lies in 0..mid-1.
    while (l <= h) {
        mid = (l + h) / 2;
        if (preSum[mid].first <= val) {
            ans = mid;
            l = mid + 1;
        }
        else
            h = mid - 1;
    }

    return ans;
}

// Function to find largest subarray having sum
// greater than or equal to k.
int largestSub(int arr[], int n, int k)
{
    int i;

    // Length of largest subarray.
    int maxlen = 0;

    // Vector to store pair of prefix sum
    // and corresponding ending index value.
    vector<pair<int, int> > preSum;

    // To store current value of prefix sum.
    int sum = 0;

    // To store minimum index value in range
    // 0..i of preSum vector.
    int minInd[n];

    // Insert values in preSum vector.
    for (i = 0; i < n; i++) {
        sum = sum + arr[i];
        preSum.push_back({ sum, i });
    }

    sort(preSum.begin(), preSum.end(), compare);

    // Update minInd array.
    minInd[0] = preSum[0].second;

    for (i = 1; i < n; i++) {
        minInd[i] = min(minInd[i - 1], preSum[i].second);
    }

    sum = 0;
    for (i = 0; i < n; i++) {
        sum = sum + arr[i];

        // If sum is greater than k, then answer
        // is i+1.
        if (sum > k)
            maxlen = i + 1;

        // If the sum is less than or equal to k, then
        // find if there is a prefix array having sum
        // that needs to be added to the current sum to
        // make its value greater than k. If yes, then
        // compare the length of updated subarray with
        // maximum length found so far.
        else {
            int ind = findInd(preSum, n, sum - k - 1);
            if (ind != -1 && minInd[ind] < i)
                maxlen = max(maxlen, i - minInd[ind]);
        }
    }

    return maxlen;
}

// Driver code.
int main()
{
    int arr[] = { -2, 1, 6, -3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 5;

    cout << largestSub(arr, n, k);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find largest subarray 
# having sum greater than k. 

# Comparison function used to 
# sort preSum vector. 
def compare(a, b): 

    if a[0] == b[0]: 
        return a[1] < b[1] 

    return a[0] < b[0] 

# Function to find index in preSum vector 
# upto which all prefix sum values are less 
# than or equal to val. 
def findInd(preSum, n, val): 

    # Starting and ending index of 
    # search space. 
    l, h = 0, n - 1

    # To store required index value. 
    ans = -1

    # If middle value is less than or equal  
    # to val then index can lie in mid+1..n 
    # else it lies in 0..mid-1. 
    while l <= h: 
        mid = (l + h) // 2
        if preSum[mid][0] <= val: 
            ans = mid 
            l = mid + 1

        else:
            h = mid - 1

    return ans 

# Function to find largest subarray having
# sum greater than or equal to k. 
def largestSub(arr, n, k): 

    # Length of largest subarray. 
    maxlen = 0

    # Vector to store pair of prefix sum 
    # and corresponding ending index value. 
    preSum = [] 

    # To store the current value of prefix sum. 
    Sum = 0

    # To store minimum index value in range 
    # 0..i of preSum vector. 
    minInd = [None] * (n) 

    # Insert values in preSum vector. 
    for i in range(0, n): 
        Sum = Sum + arr[i] 
        preSum.append([Sum, i]) 

    preSum.sort()

    # Update minInd array. 
    minInd[0] = preSum[0][1] 

    for i in range(1, n): 
        minInd[i] = min(minInd[i - 1], 
                        preSum[i][1]) 

    Sum = 0
    for i in range(0, n): 
        Sum = Sum + arr[i] 

        # If sum is greater than k, then 
        # answer is i+1. 
        if Sum > k:
            maxlen = i + 1

        # If sum is less than or equal to k, 
        # then find if there is a prefix array 
        # having sum that needs to be added to
        # current sum to make its value greater 
        # than k. If yes, then compare length 
        # of updated subarray with maximum 
        # length found so far. 
        else:
            ind = findInd(preSum, n, Sum - k - 1) 
            if ind != -1 and minInd[ind] < i: 
                maxlen = max(maxlen, i - minInd[ind]) 

    return maxlen 

# Driver code. 
if __name__ == "__main__":

    arr = [-2, 1, 6, -3] 
    n = len(arr) 

    k = 5

    print(largestSub(arr, n, k)) 

# This code is contributed 
# by Rituraj Jain 
```

**Output:**

```
2

```

**时间复杂度:**O(nlogn)
T3】辅助空间: O(n)
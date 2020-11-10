# 值仅大于`K`的最长子数组

> 原文：[https://www.geeksforgeeks.org/longest-subarray-with-only-one-value-greater-than-k/](https://www.geeksforgeeks.org/longest-subarray-with-only-one-value-greater-than-k/)

给定`N`个数字的数组，请找到最长子数组的长度，以使`K`是插入时第二大的元素。

**示例**：

> **输入**：`a[] = {9, 5, 5, 6, 8}, K = 7`
>
> **输出**：4
>
> 最长的子数组是`{9, 5, 5, 6}`，其中如果插入`K`，它将变成`{9, 5, 5, 6, 7}`，
>
> 7 是数组中的第二大元素
> 
> **输入**：`a[] = {9, 5, 5, 6, 8}, K = 10`
>
> **输出**：0
>
> 由于数组中的最大数目小于`K`的值，因此这是不可能的。
> 
> **输入**：`a[] = {8, 5, 10, 10, 8}, K = 9`
>
> **输出**：5
>
> 9 是整数数组的第二大元素

朴素的方法是对每个可能的子数组进行迭代，并检查在插入`K`时是否成为第二大元素。 朴素的，我们可以存储所有可能的最长子数组的长度。

**时间复杂度**：`O(N ^ 2)`

一种有效的解决方案是使用[两指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)解决上述问题。 以下是解决上述问题的算法。

*   将两个指针`front`和`end`初始化为 0，然后将一个**访问数组**标记为已访问索引。

*   我们需要一个[集合](http://www.geeksforgeeks.org/set-in-cpp-stl/)容器，以便我们可以在`O(log n)`中，决定从集合中删除的任何`end - front`范围的第二大元素，和一个[`unordered_map`](http://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)来计算数组中元素的频率。

*   最初检查是否存在大于`K`的元素，如果不存在这样的元素，则子数组是不可能的。

*   将元素插入集合中的`a[end]`，如果以前没有访问过索引末端，则在映射中增加其频率，以避免多次插入相同的索引。

*   如果该集合仅包含一个元素，则由于我们只有元素，并且由于我们知道至少存在一个**元素> k** ，因此可以插入`K`，因此我们对其进行计数并向前移动结束指针。

*   如果集合中包含一个以上的元素，则[`s.end()`](https://www.geeksforgeeks.org/setbegin-setend-c-stl/)指针指向最后一个元素，因此将其减少两次将向我们提供`end - front`范围的第二大元素。

*   如果第二大元素大于`K`，则此子数组是不可能的，因此我们需要将第一个指针向前移动，但是在执行此操作之前，请检查`a[front]`的频率是否为 1，如果不是，则将其从集合中删除，否则只需将`map`的频率降低 1，因为该元素将存在于任何大于`front`的索引中。 将`front`指针增加一。

*   如果第二大元素不大于`K`，则只需将结束指针增加 1。

*   存储最大长度的`end - front`并将其返回。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the length of the longest 
// subarray such that K is the second largest element 
// on insertion 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find the length of longest subarray 
int lengthOfLongestSubarray(int a[], int n, int k) 
{ 
    bool flag = 0; 

    // Check if any element exists which is 
    // greater than k or not 
    for (int i = 0; i < n; i++) { 
        if (a[i] > k) 
            flag = 1; 
    } 

    if (!flag) { 
        return 0; 
    } 

    // two pointers used 
    int front = 0; 
    int end = 0; 

    // find the maximum length 
    int maxi = 0; 

    // Map used to count frequencies 
    unordered_map<int, int> mpp; 

    // set used to find the second largest 
    // element in range front-end 
    set<int> s; 

    // initialize all index of array as 0 
    bool vis[n]; 
    memset(vis, 0, sizeof vis); 

    // iterate till any of the pointer exceeds N 
    while (front < n && end < n) { 

        // length of longest subarray 
        maxi = max(maxi, end - front); 

        // if the current index has not been 
        // visited previously then insert it 
        // in the set and increase the frequency 
        // and mark it as visited. 
        if (!vis[end]) { 
            mpp[a[end]]++; 
            s.insert(a[end]); 
            vis[end] = 1; 
        } 

        // find the largest element in the set 
        auto it = s.end(); 

        // if only one element is there in set, 
        // then insertion of K is possible which 
        // will include other elements 
        if (s.size() == 1) { 

            // increase the second pointer in order 
            // to include more elements in the subarray 
            end++; 
            continue; 
        } 

        // twice decrease the 
        // iterator as s.end() points to 
        // after the last element 
        it--; 

        // second largest element in set 
        it--; 
        int el = *it; 

        // if the second largest element is greater than the 
        // K, then it is not possible to insert element 
        // in range front-end, and thus decrease the 
        // frequency of a[front] and remove from set 
        // accordingly 
        if (el > k) { 
            if (mpp[a[front]] == 1) { 
                s.erase(a[front]); 
                mpp[a[front]]--; 
            } 
            else
                mpp[a[front]]--; 

            // move ahead the first pointer 
            front++; 
        } 
        else { 

            // increase the second pointer 
            // if the second largest element is smaller 
            // than or equals to K 
            end++; 
        } 
    } 

    // at then end also check for last subarray length 
    maxi = max(maxi, end - front); 

    return maxi; 
} 

// Driver Code 
int main() 
{ 
    int a[] = { 9, 5, 5, 6, 8 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    int k = 7; 

    cout << lengthOfLongestSubarray(a, n, k); 

    return 0; 
} 

```

## Python3

```py

# Python3 program to find the length of  
# the longest subarray such that K is  
# the second largest element on insertion 

# Function to find the length of longest subarray 
def lengthOfLongestSubarray(a, n, k): 
    flag = 0

    # Check if any element exists which is 
    # greater than k or not 
    for i in range(n): 
        if (a[i] > k): 
            flag = 1

    if (flag == 0): 
        return 0

    # two pointers used 
    front = 0
    end = 0

    # find the maximum length 
    maxi = 0

    # Map used to count frequencies 
    mpp = dict() 

    # set used to find the second largest 
    # element in range front-end 
    s = dict() 

    # initialize all index of array as 0 
    vis = [0] * n 

    # iterate till any of the pointer exceeds N 
    while (front < n and end < n): 

        # length of longest subarray 
        maxi = max(maxi, end - front) 

        # if the current index has not been 
        # visited previously then insert it 
        # in the set and increase the frequency 
        # and mark it as visited. 
        if (vis[end] == 0): 
            mpp[a[end]] = mpp.get(a[end], 0) + 1
            s[a[end]] = s.get(a[end], 0) + 1
            vis[end] = 1

        # find the largest element in the set 
        iit = sorted(list(s)) 
        it = len(iit) 

        # if only one element is there in set, 
        # then insertion of K is possible which 
        # will include other elements 
        if (len(s) == 1): 

            # increase the second pointer in order 
            # to include more elements in the subarray 
            end += 1
            continue

        # twice decrease the 
        # iterator as s.end() points to 
        # after the last element 
        it -= 1

        # second largest element in set 
        it -= 1
        el = iit[it] 

        # if the second largest element is greater than the 
        # K, then it is not possible to insert element 
        # in range front-end, and thus decrease the 
        # frequency of a[front] and remove from set 
        # accordingly 
        if (el > k): 
            if (mpp[a[front]] == 1): 
                del s[a[front]] 
                mpp[a[front]] -= 1
            else: 
                mpp[a[front]] -= 1

            # move ahead the first pointer 
            front += 1
        else : 

            # increase the second pointer 
            # if the second largest element is  
            # smaller than or equals to K 
            end += 1

    # at then end also check for  
    # last subarray length 
    maxi = max(maxi, end - front) 

    return maxi 

# Driver Code 
a  = [9, 5, 5, 6, 8] 
n = len(a) 
k = 7

print(lengthOfLongestSubarray(a, n, k)) 

# This code is contributed by Mohit Kumar 

```

**输出**：

```
4

```

时间复杂度：`O(N * log N)`



* * *

* * *




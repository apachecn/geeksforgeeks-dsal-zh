# 计算给定数组中总和存在的不同对的数量

> 原文:[https://www . geesforgeks . org/count-number-distinct-pairs-then-sum-exists-给定-array/](https://www.geeksforgeeks.org/count-number-distinct-pairs-whose-sum-exists-given-array/)

给定一个 N 个正整数的数组。计算给定数组中求和的对的数量。而重复对将不会再次计数。我们不能用相同的位置元素来配对。例:(2，1)和(1，2)将被视为仅一对。
请仔细阅读所有示例。

**示例:**

```
Input : arr[] = {1, 2, 3, 5, 10}
Output : 2
Explanation : Here there are two such pairs:
(1 + 2) = 3, (2 + 3) = 5.
Note : Here we can't take pair (5, 5) as 
we can see 5 is not coming twice

Input : arr[] = {1, 5, 6, 4, -1, 5} 
Output : 4
Explanation : (1 + 5) = 6, (1 + 4) = 5, 
(5 + -1) = 4, (6 + -1) = 5
Note : Here (1, 5) comes twice will be 
considered as only one pair. 

Input : arr[] = {5, 5, 5, 5, 10} 
Output : 1
Explanation : (5 + 5) = 10
Note : Here (5, 5) comes twice will be
considered as only one pair. 

```

想法是[对地图](https://www.geeksforgeeks.org/map-pairs-stl/)寻找独特的元素。我们首先在地图中存储元素及其数量。然后我们遍历数组元素，对于每对元素(arr[i]，arr[j])，我们检查数组中是否存在(arr[i] + arr[j])。如果存在，那么我们使用配对图检查它是否已经被计数。如果还没有计数，那么我们增加计数。

## C++

```
// C++ implementation to find count of unique pairs
// whose sum exists in given array
#include <bits/stdc++.h>
using namespace std;

// Returns number of pairs in arr[0..n-1] with
// sum equal to 'sum'
int getPairsCount(int arr[], int n)
{
    // Store counts of all elements in map m
    // to find pair (arr[i], sum-arr[i])
    // because (arr[i]) + (sum - arr[i]) = sum
    map<int, int> m;
    for (int i = 0; i < n; i++)
        m[arr[i]]++;

    // To remove duplicate items we use result map
    map<pair<int, int>, int> pairs;

    int count = 0; // Initialize result

    // Consider all pairs
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // If sum of current pair exists
            if (m[arr[i] + arr[j]] > 0 && 
                pairs[{ arr[i], arr[j] }] == 0) {
                count++;
            }

            // Insert current pair both ways to avoid
            // duplicates.
            pairs[{ arr[i], arr[j] }]++;
            pairs[{ arr[j], arr[i] }]++;
        }
    }
    return count;
}

// Driver function to test the above function
int main()
{
    int arr[] = { 1, 5, 6, 4, -1, 5, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << getPairsCount(arr, n);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation to find count 
# of unique pairs whose sum exists in
# given array

# Returns number of pairs in arr[0..n-1] 
# with sum equal to 'sum'
def getPairsCount(arr, n):

    # Store counts of all elements in map m
    # to find pair (arr[i], sum-arr[i])
    # because (arr[i]) + (sum - arr[i]) = sum
    m = dict()
    for i in range(n):
        m[arr[i]] = m.get(arr[i], 0) + 1

    # To remove duplicate items 
    # we use result map
    pairs1 = dict()

    count = 0 # Initialize result

    for i in range(n):
        for j in range(i + 1, n):
            l = arr[i] + arr[j]
            tp = (arr[i], arr[j])

            if l in m.keys():

                if tp not in pairs1.keys():

                    count += 1
            pairs1[(arr[i], arr[j])] = 1
            pairs1[(arr[j], arr[i])] = 1

    return count

# Driver Code
arr = [1, 5, 6, 4, -1, 5, 10]
n = len(arr)

print(getPairsCount(arr, n))

# This code is contributed by Mohit Kumar
```

**输出:**

```
6

```

本文由 **Harshit Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
# K 人活动选择问题

> 原文:[https://www . geesforgeks . org/activity-selection-problem-with-k-persons/](https://www.geeksforgeeks.org/activity-selection-problem-with-k-persons/)

给定两个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**S【】**和**E【】**表示商店的开始和结束时间，以及一个整数值 **K** 表示人数，任务是找出如果他们基于以下条件最佳地访问每个商店，他们总共可以访问的商店的最大数量:

*   一家商店只能被一个人光顾
*   一个人不能去另一家商店，如果它的时间与它冲突

**示例:**

> **输入:** S[] = {1，8，3，2，6}，E[] = {5，10，6，5，9}，K = 2
> **输出:** 4
> **解释:**一种可能的解决方案是第一个人参观第一和第五家商店，同时第二个人将参观第四和第二家商店。
> 
> **输入:** S[] = {1，2，3}，E[] = {3，4，5}，K = 2
> **输出:** 3
> **解释:**一种可能的解决方案是第一个人参观第一个和第三个商店，同时第二个人参观第二个商店。

**方法:**这个问题可以用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)称为[活动选择](https://www.geeksforgeeks.org/activity-selection-problem-greedy-algo-1/)和[排序](https://www.geeksforgeeks.org/sorting-algorithms/)来解决。在活动选择问题中，只有一个人执行活动，但是这里 **K** 个人可用于一个活动。为了管理一个人的可用性，使用了[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)。

按照以下步骤解决问题:

1.  初始化一个数组 **a[]** 对，并为每个索引 **i** 存储[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **{S[i]，E[i]}** 。
2.  [根据结束时间排序](https://www.geeksforgeeks.org/sorting-array-according-another-array-using-pair-stl/)阵列**a【】**。
3.  初始化一个[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/) **st** 来存储他们当前正在访问的店铺的结束时间。
4.  用 **0** 初始化变量**和**来存储最终结果。
5.  遍历每对数组 **a[]** ，
    1.  如果某人有空，即**a【I】。首先**大于或等于多集 **st** 中任何人的结束时间，然后将**计数**增加 **1** ，并用新的**a【I】更新该元素的结束时间。第二**。
    2.  否则，继续检查下一对。
6.  最后，将结果打印为**计数**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Comparator
bool compareBy(const pair<int, int>& a,
               const pair<int, int>& b)
{
    if (a.second != b.second)
        return a.second < b.second;
    return a.first < b.first;
}
// Function to find maximum shops
// that can be visited by K persons
int maximumShops(int* opening, int* closing,
                 int n, int k)
{
    // Store opening and closing
    // time of shops
    pair<int, int> a[n];

    for (int i = 0; i < n; i++) {
        a[i].first = opening[i];
        a[i].second = closing[i];
    }

    // Sort the pair of array
    sort(a, a + n, compareBy);

    // Stores the result
    int count = 0;

    // Stores current number of persons visiting
    // some shop with their ending time
    multiset<int> st;

    for (int i = 0; i < n; i++) {

        // Check if current shop can be
        // assigned to a person who's
        // already visiting any other shop
        bool flag = false;

        if (!st.empty()) {

            auto it = st.upper_bound(a[i].first);

            if (it != st.begin()) {
                it--;

                // Checks if there is any person whose
                // closing time <= current shop opening
                // time
                if (*it <= a[i].first) {

                    // Erase previous shop visited by the
                    // person satisfying the condition
                    st.erase(it);

                    // Insert new closing time of current
                    // shop for the person satisfying ṭhe
                    // condition
                    st.insert(a[i].second);

                    // Increment the count by one
                    count++;

                    flag = true;
                }
            }
        }

        // In case if no person have closing
        // time <= current shop opening time
        // but there are some persons left
        if (st.size() < k && flag == false) {
            st.insert(a[i].second);
            count++;
        }
    }

    // Finally print the ans
    return count;
}

// Driver Code
int main()
{

    // Given starting and ending time
    int S[] = { 1, 8, 3, 2, 6 };
    int E[] = { 5, 10, 6, 5, 9 };

    // Given K and N
    int K = 2, N = sizeof(S)
                   / sizeof(S[0]);

    // Function call
    cout << maximumShops(S, E, N, K) << endl;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from bisect import bisect_left

# Function to find maximum shops
# that can be visited by K persons
def maximumShops(opening, closing, n,  k):

    # Store opening and closing
    # time of shops
    a = [[0, 0] for i in range(n)]

    for i in range(n):
        a[i][0] = opening[i]
        a[i][1] = closing[i]

    # Sort the pair of array
    a = sorted(a)

    # Stores the result
    count = 1

    # Stores current number of persons visiting
    # some shop with their ending time
    st = {}
    for i in range(n):

        # Check if current shop can be
        # assigned to a person who's
        # already visiting any other shop
        flag = False

        if (len(st) == 0):
            ar = list(st.keys())

            it = bisect_left(ar, a[i][0])

            if (it != 0):
                it -= 1

                # Checks if there is any person whose
                # closing time <= current shop opening
                # time
                if (ar[it] <= a[i][0]):

                    # Erase previous shop visited by the
                    # person satisfying the condition
                    del st[it]

                    # Insert new closing time of current
                    # shop for the person satisfying ṭhe
                    # condition
                    st[a[i][1]] = 1

                    # Increment the count by one
                    count += 1
                    flag = True

        # In case if no person have closing
        # time <= current shop opening time
        # but there are some persons left
        if (len(st) < k and flag == False):
            st[a[i][1]] = 1
            count += 1

    # Finally pr the ans
    return count

# Driver Code
if __name__ == '__main__':

    # Given starting and ending time
    S = [1, 8, 3, 2, 6]
    E = [5, 10, 6, 5, 9]

    # Given K and N
    K,N = 2, len(S)

    # Function call
    print (maximumShops(S, E, N, K))

    # This code is contributed by mohit kumar 29
```

**Output:** 

```
4
```

***时间复杂度:**O(NlogN)*
T5**辅助空间:** O(N)
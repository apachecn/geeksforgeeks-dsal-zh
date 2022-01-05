# 给定字符串在数组中出现的次数，范围为[l，r]

> 原文:[https://www . geeksforgeeks . org/给定字符串在数组范围内出现的次数-l-r/](https://www.geeksforgeeks.org/number-of-times-the-given-string-occurs-in-the-array-in-the-range-l-r/)

给定一个字符串数组 **arr[]** 和两个整数 **l** 和 **r** ，任务是在范围**【l，r】**(基于 1 的索引)内找到数组中给定字符串 **str** 出现的次数。**注意**字符串只包含小写字母。
**示例:**

> **输入:**arr[]= {“ABC”、“def”、“ABC”}，L = 1，R = 2，str =“ABC”
> **输出:** 1
> **输入:**arr[]= {“ABC”、“def”、“ABC”}，L = 1，R = 3，str =“ghf”
> **输出:** 0

**方法:**想法是使用一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)来存储数组第 I 个字符串出现的索引。如果给定字符串不在映射中，则答案为零，否则对映射中给定字符串的索引执行二分搜索法运算，并找出该字符串在[L，R]范围内出现的次数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of occurrences of
int NumOccurrences(string arr[], int n, string str, int L, int R)
{
    // To store the indices of strings in the array
    unordered_map<string, vector<int> > M;
    for (int i = 0; i < n; i++) {
        string temp = arr[i];
        auto it = M.find(temp);

        // If current string doesn't
        // have an entry in the map
        // then create the entry
        if (it == M.end()) {
            vector<int> A;
            A.push_back(i + 1);
            M.insert(make_pair(temp, A));
        }
        else {
            it->second.push_back(i + 1);
        }
    }

    auto it = M.find(str);

    // If the given string is not
    // present in the array
    if (it == M.end())
        return 0;

    // If the given string is present
    // in the array
    vector<int> A = it->second;
    int y = upper_bound(A.begin(), A.end(), R) - A.begin();
    int x = upper_bound(A.begin(), A.end(), L - 1) - A.begin();

    return (y - x);
}

// Driver code
int main()
{
    string arr[] = { "abc", "abcabc", "abc" };
    int n = sizeof(arr) / sizeof(string);
    int L = 1;
    int R = 3;
    string str = "abc";

    cout << NumOccurrences(arr, n, str, L, R);

    return 0;
}
```

## 蟒蛇 3

```
# Python implementation of the approach
from bisect import bisect_right as upper_bound
from collections import defaultdict

# Function to return the number of occurrences of
def numOccurences(arr: list, n: int, string: str, L: int, R: int) -> int:

    # To store the indices of strings in the array
    M = defaultdict(lambda: list)
    for i in range(n):
        temp = arr[i]

        # If current string doesn't
        # have an entry in the map
        # then create the entry
        if temp not in M:
            A = []
            A.append(i + 1)
            M[temp] = A
        else:
            M[temp].append(i + 1)

    # If the given string is not
    # present in the array
    if string not in M:
        return 0

    # If the given string is present
    # in the array
    A = M[string]
    y = upper_bound(A, R)
    x = upper_bound(A, L - 1)

    return (y - x)

# Driver Code
if __name__ == "__main__":
    arr = ["abc", "abcabc", "abc"]
    n = len(arr)
    L = 1
    R = 3
    string = "abc"

    print(numOccurences(arr, n, string, L, R))

# This code is contributed by
# sanjeev2552
```

**Output:** 

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)
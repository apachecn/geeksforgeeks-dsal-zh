# 求唯一的字典序递增四胞胎，所有元素绝对值之和为 B，GCD 为 1

> 原文:[https://www . geeksforgeeks . org/find-unique-字典序递增-四胞胎-所有元素绝对值之和为 b 和 gcd-is-1/](https://www.geeksforgeeks.org/find-unique-lexicographically-increasing-quadruplets-with-sum-as-b-and-gcd-of-absolute-values-of-all-elements-is-1/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A** 和一个整数 **B，**的任务是找到所有按字典顺序递增顺序排列的唯一四元组，使得每个四元组的元素之和为 **B** ，四元组的所有元素的绝对值的 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 为 1 **。**

**例**:

> **输入:** A = {1，0，-1，0，-2，2}，B = 0
> **输出:**
> -2 -1 1 2
> -1 0 0 1
> **说明:**只有三个唯一的四胞胎的和= 0，它们是{-2，0，0，2}、{-2，-1，1，2 }、{-1，0，0，1}，在这些四胞胎中只有第二个和第三个
> 
> **输入:** A = { 1，5，1，0，6，0 }，B = 7
> T3】输出:T5】0 0 1 6
> 0 1 1 5

**方法:**思想是将每对元素的和存储在一个 [hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 中，然后遍历所有的元素对，然后查找 hashmap 找到对，这样四倍的和等于 **B** ，四倍的所有元素的绝对值的 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 等于 1 **。**在[这篇](https://www.geeksforgeeks.org/find-four-elements-sum-given-value-set-3-hashmap/)文章中已经讨论了使用 hashmap 的详细方法。按照步骤解决问题。

*   将数组中每对元素的和插入到 hashmap **mp 中。**
*   初始化一个集合 **st，**来存储所有的四胞胎。
*   [从 i = 0 到 N-1 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)
    *   从 j = i+1 到 N-1 遍历数组
        *   从 hashmap 中找出所有和等于 **B- A[i]-A[j]的对。**初始化一对向量 **v** 到 **mp[B-A[i]-A[j]]。**
        *   使用变量 **k** 遍历向量 **v**
            *   如果**v【k】。首先**或者**v【k】。第二次**等于 **i** 或者 **j** 然后继续下一次迭代。
            *   将四倍的元素存储在 **temp** 数组中。[整理](https://www.geeksforgeeks.org/sort-c-stl/)**temp**阵列。如果温度数组所有元素的 [gcd 为 1，则将**温度**数组插入**ST**](https://www.geeksforgeeks.org/gcd-two-array-numbers/)
*   [遍历集合](https://www.geeksforgeeks.org/set-in-cpp-stl/) **st** 并打印所有四胞胎。

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find all
// quadruplets with sum B.
void find4Sum(int A[], int N, int B)
{
    // Hashmap to store sum
    // of all pairs
    unordered_map<int,
                  vector<pair<int, int> > >
        mp;

    // Set to store all quadruplets
    set<vector<int> > st;

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {
        // Traverse the array
        for (int j = i + 1; j < N; j++) {
            int sum = A[i] + A[j];
            // Insert sum of
            // current pair into
            // the hashmap
            mp[sum].push_back({ i, j });
        }
    }

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {
        // Traverse the array
        for (int j = i + 1; j < N; j++) {
            int sum = A[i] + A[j];
            // Lookup the hashmap
            if (mp.find(B - sum) != mp.end()) {
                vector<pair<int, int> > v
                    = mp[B - sum];

                for (int k = 0; k < v.size(); k++) {

                    pair<int, int> it = v[k];
                    if (it.first != i && it.second != i
                        && it.first != j
                        && it.second != j) {
                        vector<int> temp;
                        temp.push_back(A[i]);
                        temp.push_back(A[j]);
                        temp.push_back(A[it.first]);
                        temp.push_back(A[it.second]);

                        // Stores the gcd of the
                        // quadrupled
                        int gc = abs(temp[0]);
                        gc = __gcd(abs(temp[1]), gc);
                        gc = __gcd(abs(temp[2]), gc);
                        gc = __gcd(abs(temp[3]), gc);
                        // Arrange in
                        // ascending order
                        sort(temp.begin(), temp.end());
                        // Insert into set if gcd is 1
                        if (gc == 1)
                            st.insert(temp);
                    }
                }
            }
        }
    }
    // Iterate through set
    for (auto it = st.begin(); it != st.end(); it++) {
        vector<int> temp = *it;
        // Print the elements
        for (int i = 0; i < 4; i++) {
            cout << temp[i] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    // Input
    int N = 6;
    int A[6]
        = { 1, 0, -1, 0, -2, 2 };
    int B = 0;

    // Function Call
    find4Sum(A, N, B);
    return 0;
}
```

**Output**

```
-2 -1 1 2 
-1 0 0 1 

```

**时间复杂度** : O(N^3)
**辅助空间:** O(N^2)
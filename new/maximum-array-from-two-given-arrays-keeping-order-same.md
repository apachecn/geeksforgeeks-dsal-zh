# 来自两个给定数组的最大数组，它们保持顺序相同

给定两个相同大小的数组 A []和 B []（两个数组分别包含不同的元素，但可能具有一些公共元素），任务是形成相同大小的第三个（或结果）数组。 所得数组应同时包含两个数组中最多 n 个元素。 它应该先选择 A []的元素，然后再选择 B []的元素，其顺序与原始数组中出现的顺序相同。 如果存在公共元素，则 res []中仅应存在一个元素，并且应将优先级赋予 A []。
**示例：**

```
Input :  A[] =  [ 9 7 2 3 6 ]
         B[] =  [ 7 4 8 0 1 ]
Output : res[] = [9 7 6 4 8]
res[] has maximum n elements of both A[] 
and B[] such that elements of A[] appear
first (in same order), then elements of B[].
Also 7 is common and priority is given to
A's 7.

Input :  A[] = [ 6 7 5 3 ]
         B[] = [ 5 6 2 9 ] 
Output : res[] = [ 6 7 5 9 ]

```

1）创建两个数组的副本，并按降序对副本进行排序。
2）使用散列选择两个数组的唯一 n 个最大元素，将 A []优先。
3）将结果数组初始化为空。
4）遍历 A []，复制哈希中存在的 A []元素。 这样做是为了保持元素的顺序相同。
5）对 B []重复步骤 4。 这次，我们只考虑 A []中不存在的那些元素（不要在哈希中出现两次）。
下面的 C++实现上述想法。

## C++

```cpp

// Make a set of maximum elements from two
// arrays A[] and B[]
#include <bits/stdc++.h>
using namespace std;

void maximizeTheFirstArray(int A[], int B[],
                                    int n)
{
    // Create copies of A[] and B[] and sort
    // the copies in descending order.
    vector<int> temp1(A, A+n);
    vector<int> temp2(B, B+n);
    sort(temp1.begin(), temp1.end(), greater<int>());
    sort(temp2.begin(), temp2.end(), greater<int>());

    // Put maximum n distinct elements of
    // both sorted arrays in a map.
    unordered_map<int, int> m;
    int i = 0, j = 0;
    while (m.size() < n)
    {
         if (temp1[i] >= temp2[j])
         {
            m[temp1[i]]++;
            i++;
         }
         else
         {
            m[temp2[j]]++;
            j++;
         }
    }

    // Copy elements of A[] to that 
    // are present in hash m.
    vector<int> res;
    for (int i = 0; i < n; i++)
        if (m.find(A[i]) != m.end())
           res.push_back(A[i]);

    // Copy elements of B[] to that 
    // are present in hash m. This time
    // we also check if the element did
    // not appear twice.
    for (int i = 0; i < n; i++)
        if (m.find(B[i]) != m.end() &&
            m[B[i]] == 1)
           res.push_back(B[i]);

    // print result
    for (int i = 0; i < n; i++)
        cout << res[i] << " ";
}

// driver program
int main()
{
    int A[] = { 9, 7, 2, 3, 6 };
    int B[] = { 7, 4, 8, 0, 1 };
    int n = sizeof(A) / sizeof(A[0]);
    maximizeTheFirstArray(A, B, n);
    return 0;
}

```

## Python3

```py

# Python3 program to implement the 
# above approach
# Make a set of maximum elements 
# from two arrays A[] and B[]
from collections import defaultdict

def maximizeTheFirstArray(A, B, n):

    # Create copies of A[] and B[] 
    # and sort the copies in 
    # descending order.
    temp1 = A.copy()
    temp2 = B.copy()
    temp1.sort(reverse = True)
    temp2.sort(reverse = True)

    # Put maximum n distinct 
    # elements of both sorted 
    # arrays in a map.
    m = defaultdict(int)
    i = 0
    j = 0;

    while (len(m) < n):
         if (temp1[i] >= temp2[j]):
            m[temp1[i]] += 1
            i += 1       
         else:
            m[temp2[j]] += 1
            j += 1

    # Copy elements of A[] to that 
    # are present in hash m.
    res = []

    for i in range (n):
        if (A[i] in m):
           res.append(A[i])

    # Copy elements of B[] to that 
    # are present in hash m. This time
    # we also check if the element did
    # not appear twice.
    for i in range (n):
        if (B[i] in m and
            m[B[i]] == 1):
           res.append(B[i])

    # Print result
    for i in range (n):
        print (res[i], end = " ")

# Driver code
if __name__ == "__main__":

    A = [9, 7, 2, 3, 6]
    B = [7, 4, 8, 0, 1]
    n = len(A)
    maximizeTheFirstArray(A, B, n);

# This code is contributed by Chitranayal

```

**输出：**

```
 9 7 6 4 8 

```

**时间复杂度：** O（n Log n）



* * *

* * *




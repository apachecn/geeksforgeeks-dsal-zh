# 通过改变每一步中三个元素的顺序对数组进行排序的步骤数

> 原文:[https://www . geesforgeks . org/通过改变每一步中三个元素的顺序对数组进行排序的步骤数/](https://www.geeksforgeeks.org/number-of-steps-to-sort-the-array-by-changing-order-of-three-elements-in-each-step/)

给定由范围**【0，N-1】**中的唯一元素组成的大小为 **N** 的数组 **arr[]** ，任务是找到 **K** ，这是通过选择三个不同的元素并重新排列它们来对给定数组进行排序所需的步骤数。此外，在 k 线中打印在这些 k 线步骤中选择的索引。

> 例如，在数组{5，4，3，2，1，0}中，通过选择三个不同的元素对给定数组进行排序的一种可能方法是选择数字{2，1，0}并将其排序为{0，1，2}，从而组成数组{5，4，3，0，1，2}。同样，执行其余操作，所选的索引({3，4，5}在上述情况下)以单独的行打印。

**例:**

> **输入:** arr[] = {0，5，4，3，2，1}
> **输出:**
> 2
> 1 2 5
> 2 5 4
> **解释:**
> 上述数组可以分两步排序:
> 第一步:我们在索引 1，2，5 处更改元素的顺序，然后数组变成{0，1，5，3，2，4}。
> 第二步:我们再次改变索引 2、5、4 处元素的顺序，然后数组变成{0、1、2、3、4、5}并排序。
> **输入:** arr[] = {0，3，1，6，5，2，4}
> **输出:** -1
> **解释:**
> 以上数组不能按任何步数排序。
> 假设我们选择索引 1、3、2，那么数组变成{0、1、6、3、5、2、4}
> 之后，我们选择索引 2、6、4，那么数组变成{0、1、5、3、4、2、6}。
> 现在只有两个元素没有排序，所以我们不能选择 3 个元素，所以上面的数组不能排序。我们可以尝试任何顺序的索引，我们将总是剩下 2 个元素没有排序。

**方法:**想法是首先统计未排序的元素，并将它们插入到[无序集合](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)中。如果计数为 0，那么我们不需要任何步骤来排序数组，所以我们打印 0 并退出。否则，我们首先从集合中删除 i = A[A[i]]的所有元素，然后执行以下操作，直到集合变空:

*   我们选择所有可能的索引组合(如果有的话)，这样至少有两个元素会被排序。
*   现在，改变元素的顺序，如果 i = A[i]，将它们从集合中删除。
*   然后，我们只剩下 i = A[A[i]]这样的元素，这些元素的计数必须是 4 的倍数，否则无法对元素进行排序。
*   然后，我们选择任意两对并执行两次改变元素顺序。然后所有四个选择的元素将被排序。
*   我们存储向量中涉及元素顺序变化的所有索引，并将其打印为答案。

让我们用一个例子来理解上面的方法。让数组 arr[] = {0，8，9，10，1，7，12，4，3，2，6，5，11}。然后:

*   最初，集合将包含所有 12 个元素，没有 i = A[A[i]]这样的元素。
*   现在，选择{11，5，7}并更改元素的顺序。然后，arr[] = {0，8，9，10，1，5，12，7，3，2，6，4，11}。
*   现在，选择{11，4，1}并更改元素的顺序。然后，arr[] = {0，1，9，10，4，5，12，7，3，2，6，8，11}。
*   现在，选择{11，8，3}并更改元素的顺序。然后，arr[] = {0，1，9，3，4，5，12，7，8，2，6，10，11}。
*   现在，选择{11，10，6}并更改元素的顺序。然后，arr[] = {0，1，9，3，4，5，6，7，8，2，10，12，11}。
*   完成上述步骤后，我们剩下两对未排序的元素，例如 i = A[A[i]]。
*   最后，选择{2，11，9}和{11，9，5}并重新排序。然后，arr[] = {0，1，2，3，4，5，6，7，8，9，10，11，12}进行排序。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to sort the array
// by changing the order of
// three elements

#include <bits/stdc++.h>
using namespace std;

// Function to change the order of
// the elements having a temporary
// vector and the required indices
// as the arguments
void cngorder(vector<int>& v, int i,
              int j, int k)
{
    int temp = v[k];
    v[k] = v[j];
    v[j] = v[i];
    v[i] = temp;
}

// Function to sort the elements having
// the given array and its size.
void sortbyorder3(vector<int>& A, int n)
{

    // Flag to check whether the sorting
    // is possible or not
    bool flag = 0;

    int count = 0;

    // Set that will contains unsorted
    // elements
    unordered_set<int> s;

    // Iterating through the elements
    for (int i = 0; i < n; i++) {

        // Inserting the required elements
        // in the set
        if (i != A[i])
            count++, s.insert(i);
    }

    // When the given array is
    // already sorted
    if (count == 0)
        cout << "0" << endl;

    else {

        // Vector that will contain
        // the answer
        vector<vector<int> > ans;

        // Temporary vector to store
        // the indices
        vector<int> vv;

        int x, y, z;

        count = 0;

        // Loop that will execute till the
        // set becomes empty
        while (!s.empty()) {
            auto it = s.begin();
            int i = *it;

            // Check for the condition
            if (i == A[A[i]]) {
                s.erase(i);
                s.erase(A[i]);
                continue;
            }

            // Case when the minimum two
            // elements will get sorted
            else {
                x = A[i], y = A[A[i]], z = A[A[A[i]]];
                vv.push_back(x), vv.push_back(y),
                    vv.push_back(z);

                // Changing the order of elements
                cngorder(A, x, y, z);

                // Pushing the indices to the
                // answer vector
                ans.push_back(vv);

                // If the third element also
                // gets sorted
                if (vv[0] == A[vv[0]])
                    s.erase(vv[0]);

                // Erasing the two sorted elements
                // from the set
                s.erase(vv[1]), s.erase(vv[2]);
                vv.clear();
            }
        }

        count = 0;

        // The count of the remaining
        // unsorted elements
        for (int i = 0; i < n; i++) {
            if (i != A[i])
                count++;
        }

        // If the count of the left
        // unsorted elements is not
        // a multiple of 4, then
        // sorting is not possible
        if (count % 4 != 0)
            flag = 1;

        // Only the elements such that
        // i = A[A[i]] are left
        // for sorting
        else {

            // Indices of any one element
            // from the two pairs that
            // will be sorted in 2 steps
            int i1 = -1, i2 = -1;
            for (int i = 0; i < n; i++) {

                // Index of any element of
                // the pair
                if (A[i] != i && i1 == -1) {
                    i1 = i;
                }

                // When we find the second
                // pair and the index of
                // any one element is stored
                else if (A[i] != i && i1 != -1
                         && i2 == -1) {
                    if (i1 == A[i])
                        continue;
                    else
                        i2 = i;
                }

                // When we got both the pair
                // of elements
                if (i1 != -1 && i2 != -1) {

                    // Remaining two indices
                    // of the elements
                    int i3 = A[i1], i4 = A[i2];

                    // The first order of indices
                    vv.push_back(i1),
                        vv.push_back(i2),
                        vv.push_back(A[i1]);

                    // Pushing the indices to the
                    // answer vector
                    ans.push_back(vv);
                    vv.clear();

                    // The second order of indices
                    vv.push_back(i2),
                        vv.push_back(A[i1]),
                        vv.push_back(A[i2]);

                    // Pushing the indices to the
                    // answer vector
                    ans.push_back(vv);
                    vv.clear();

                    // Changing the order of the
                    // first combination of
                    // the indices
                    cngorder(A, i1, i2, i3);

                    // Changing the order of the
                    // second combination of
                    // the indices after which all
                    // the 4 elements will be sorted
                    cngorder(A, i2, i3, i4);

                    i1 = -1, i2 = -1;
                }
            }
        }

        // If the flag value is 1
        // the sorting is not possible
        if (flag == 1)
            cout << "-1" << endl;

        else {

            // Printing the required number
            // of steps
            cout << ans.size() << endl;

            // Printing the indices involved
            // in the shifting
            for (int i = 0; i < ans.size(); i++) {
                cout << ans[i][0]
                     << " " << ans[i][1]
                     << " " << ans[i][2]
                     << endl;
            }
        }
    }
}

// Driver code
int main()
{

    int n;
    vector<int> A{ 0, 8, 9, 10, 1, 7, 12,
                   4, 3, 2, 6, 5, 11 };
    n = A.size();

    // Calling the sorting function
    sortbyorder3(A, n);

    return 0;
}
```

**Output:** 

```
6
11 5 7
11 4 1
11 8 3
11 10 6
2 11 9
11 9 12
```

**时间复杂度:** *O(N)* ，其中 N 是数组的大小。
**辅助空间:** O(N)
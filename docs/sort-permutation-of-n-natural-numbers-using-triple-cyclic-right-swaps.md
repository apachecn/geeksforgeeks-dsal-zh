# 使用三重循环右互换对 N 个自然数的排列进行排序

> 原文:[https://www . geeksforgeeks . org/sort-n 个自然数的排列-使用-三重循环-右交换/](https://www.geeksforgeeks.org/sort-permutation-of-n-natural-numbers-using-triple-cyclic-right-swaps/)

给定一个大小为 **N** 的数组 **arr[]** ，该数组包含 N 个自然数的排列，任务是在三重循环右交换的帮助下对 N 个自然数的排列进行排序。

**三重循环右移:**指三重循环右移，其中–

```
arr[i] -> arr[j] -> arr[k] -> arr[i]
```

**示例:**

> **输入:** arr[] = {3，2，4，1}
> **输出:** 1
> 1 3 4
> **解释:**
> 在操作 1 中，选择索引 1，3 和 4，它们被循环移位–
> arr[1]= arr[4]= 1
> arr[3]= arr[1]= 3
> arr[4]= arr[3]= 4
> 因此，最终数组将是{ T0
> 
> **输入:** arr[] = {2，3，1}
> **输出:** 1
> 1 2 3

**方法:**思路是遍历数组，找到数组中不在实际排序位置的元素，可以通过 if ![arr[i] != i   ](img/9fc3d264cbe64041b0e7aee7da8c222c.png "Rendered by QuickLaTeX.com")进行检查。因为数组中只有 N 个自然元素。最后，找出数组中需要的奇数长度循环旋转，得到数组的排序形式。如果需要任何偶数长度的循环旋转，那么就不可能对数组的元素进行排序。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// number of operations required to
// sort the elements of the array

#include <bits/stdc++.h>
using namespace std;
#define ll long long

// Function to sort the permutation
// with the given operations
void sortPermutation(ll arr[], ll n)
{
    vector<pair<ll,
                pair<ll, ll> > >
        ans;
    vector<ll> p;

    // Visited array to check the
    // array element is at correct
    // position or not
    bool visited[200005] = { 0 };

    // Loop to iterate over the elements
    // of the given array
    for (ll i = 1; i <= n; i++) {

        // Condition to check if the
        // elements is at its correct
        // position
        if (arr[i] == i) {
            visited[i] = 1;
            continue;
        }
        else {

            // Condition to check if the
            // element is included in any
            // previous cyclic rotations
            if (!visited[i]) {
                ll x = i;
                vector<ll> v;

                // Loop to find the cyclic
                // rotations in required
                while (!visited[x]) {
                    visited[x] = 1;
                    v.push_back(x);
                    x = arr[x];
                }

                // Condition to check if the
                // cyclic rotation is a
                // valid rotation
                if ((v.size() - 3) % 2 == 0) {
                    for (ll i = 1; i < v.size();
                         i += 2) {

                        ans
                            .push_back(
                                make_pair(
                                    v[0],
                                    make_pair(
                                        v[i], v[i + 1])));
                    }
                    continue;
                }
                p.push_back(v[0]);
                p.push_back(v[v.size() - 1]);

                // Loop to find the index of the
                // cyclic rotation
                // for the current index
                for (ll i = 1; i < v.size() - 1;
                     i += 2) {
                    ans
                        .push_back(
                            make_pair(
                                v[0],
                                make_pair(
                                    v[i], v[i + 1])));
                }
            }
        }
    }

    // Condition to if the cyclic
    // rotation is a valid rotation
    if (p.size() % 4) {
        cout << -1 << "\n";
        return;
    }

    // Loop to find all the valid operations
    // required to sort the permutation
    for (ll i = 0; i < p.size(); i += 4) {
        ans.push_back(
            make_pair(p[i],
                      make_pair(p[i + 1], p[i + 2])));
        ans.push_back(
            make_pair(p[i + 2],
                      make_pair(p[i], p[i + 3])));
    }

    // Total operation required
    cout << ans.size() << "\n";
    for (ll i = 0; i < ans.size(); i++) {
        cout << ans[i].first << " "
             << ans[i].second.first << " "
             << ans[i].second.second << "\n";
    }
}

// Driver Code
int main()
{
    ll arr[] = { 0, 3, 2, 4, 1 };
    ll n = 4;

    // Function Call
    sortPermutation(arr, n);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation to find the
# number of operations required to
# sort the elements of the array

# Function to sort the permutation
# with the given operations
def sortPermutation(arr, n):

    ans = []
    p = []

    # Visited array to check the
    # array element is at correct
    # position or not
    visited = [0] * 200005

    # Loop to iterate over the elements
    # of the given array
    for i in range(1, n + 1):

        # Condition to check if the
        # elements is at its correct
        # position
        if (arr[i] == i):
            visited[i] = 1
            continue

        else:

            # Condition to check if the
            # element is included in any
            # previous cyclic rotations
            if (visited[i]==False):
                x = i
                v = []

                # Loop to find the cyclic
                # rotations in required
                while (visited[x] == False):
                    visited[x] = 1
                    v.append(x)
                    x = arr[x]

                # Condition to check if the
                # cyclic rotation is a
                # valid rotation
                if ((len(v) - 3) % 2 == 0):
                    for i in range(1, len(v), 2):
                        ans.append([v[0], v[i], v[i + 1]])
                    continue

                p.append(v[0])
                p.append(v[len(v) - 1])

                # Loop to find the index of the
                # cyclic rotation
                # for the current index
                for i in range(1, len(v) - 1, 2):
                    ans.append([v[0], v[i], v[i + 1]])

    # Condition to if the cyclic
    # rotation is a valid rotation
    if (len(p) % 4):
        print(-1)
        return

    # Loop to find athe valid operations
    # required to sort the permutation
    for i in range(0, len(p), 4):
        ans.append([p[i], p[i + 1], p[i + 2]])
        ans.append(p[i [+ 2], p[i], p[i + 3]])

    # Total operation required
    print(len(ans))
    for i in ans:
        print(i[0], i[1], i[2])

# Driver Code
if __name__ == '__main__':
    arr=[0, 3, 2, 4, 1]
    n = 4

    # Function Call
    sortPermutation(arr, n)

# This code is contributed by Mohit Kumar
```

**Output:** 

```
1
1 3 4
```
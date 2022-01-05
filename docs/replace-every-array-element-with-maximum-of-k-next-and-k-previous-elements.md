# 用最大 K 个下一个和 K 个前一个元素替换每个数组元素

> 原文:[https://www . geeksforgeeks . org/将每个数组元素替换为最大 k 个下一个和 k 个上一个元素/](https://www.geeksforgeeks.org/replace-every-array-element-with-maximum-of-k-next-and-k-previous-elements/)

给定一个数组 **arr** ，任务是用 K 个下一个和 K 个前一个元素的最大值替换每个数组元素。

**示例:**

> **输入:** arr[] = {12，5，3，9，21，36，17}，K=2
> **输出:** 5 12 21 36 36 21 36
> 
> **输入:** arr[] = { 13，21，19}，K=1
> **输出:** 21，19，21

**天真方法:**按照以下步骤解决这个问题:

1.  遍历数组从 **i=0** 到 **i < N** ，对于每个元素:
    *   运行另一个从 **j=i-K** 到 **j < =i+K** 的循环，并将**arr【I】**更改为 K 个下一个和 K 个前一个元素的最大值。
2.  在上述循环结束后打印数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
#include <limits.h>
#include <math.h>
using namespace std;

// Function to update the array
// arr[i] = maximum of prev K and next K elements.
void updateArray(int arr[], int N, int K)
{

    int start, end;
    for (int i = 0; i < N; i++) {
        int mx = INT_MIN;

        // Start limit is max(i-K, 0)
        start = max(i - K, 0);

        // End limit in min(i+K, N-1)
        end = min(i + K, N - 1);
        for (int j = start; j <= end; j++) {

            // Skipping the current element
            if (j == i) {
                continue;
            }
            mx = max(arr[j], mx);
        }

        cout << mx << ' ';
    }
}

// Driver Code
int main()
{
    int arr[] = { 12, 5, 3, 9, 21, 36, 17 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    updateArray(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to update the array arr[i] = maximum
// of prev K and next K elements.
static void updateArray(int arr[], int N, int K)
{
    int start, end;
    for(int i = 0; i < N; i++)
    {
        int mx = Integer.MIN_VALUE;

        // Start limit is max(i-K, 0)
        start = Math.max(i - K, 0);

        // End limit in min(i+K, N-1)
        end = Math.min(i + K, N - 1);
        for(int j = start; j <= end; j++)
        {

            // Skipping the current element
            if (j == i)
            {
                continue;
            }
            mx = Math.max(arr[j], mx);
        }
        System.out.print(mx + " ");
    }
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 12, 5, 3, 9, 21, 36, 17 };
    int N = arr.length;
    int K = 2;

    updateArray(arr, N, K);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# python3 program for the above approach
INT_MIN = -2147483648

# Function to update the array
# arr[i] = maximum of prev K and next K elements.
def updateArray(arr, N, K):

    for i in range(0, N):
        mx = INT_MIN

        # Start limit is max(i-K, 0)
        start = max(i - K, 0)

        # End limit in min(i+K, N-1)
        end = min(i + K, N - 1)
        for j in range(start, end + 1):

            # Skipping the current element
            if (j == i):
                continue
            mx = max(arr[j], mx)
        print(mx, end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [12, 5, 3, 9, 21, 36, 17]
    N = len(arr)
    K = 2

    updateArray(arr, N, K)

# This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to update the array
       // arr[i] = maximum of prev K and next K elements.
       function updateArray(arr, N, K) {

           let start, end;
           for (let i = 0; i < N; i++) {
               let mx = Number.MIN_VALUE;

               // Start limit is max(i-K, 0)
               start = Math.max(i - K, 0);

               // End limit in min(i+K, N-1)
               end = Math.min(i + K, N - 1);
               for (let j = start; j <= end; j++) {

                   // Skipping the current element
                   if (j == i) {
                       continue;
                   }
                   mx = Math.max(arr[j], mx);
               }

               document.write(mx + ' ')
           }
       }

       // Driver Code
       let arr = [12, 5, 3, 9, 21, 36, 17];
       let N = arr.length;
       let K = 2;

       updateArray(arr, N, K);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
5 12 21 36 36 21 36 
```

**时间复杂度:**O(N * N)
T3】辅助空间: O(1)

**高效方法:**一个[段树](https://www.geeksforgeeks.org/segment-tree-set-2-range-maximum-query-node-update/)可以用来解决这个问题。因此，构建一个最大范围段树，其中:

*   叶节点是输入数组的元素。
*   每个内部节点代表其所有子节点的最大值。

现在，在建立段树之后，找到从 **(i-K)** 到 **(i-1)** 的最大值，说出**左边的**和 **(i+1)** 到 **(i+K)** 的最大值，在这个段树上使用查询说出右边的。将**arr【I】**换成最大的**左**和**右**。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#define MAXN 500001

#include <bits/stdc++.h>
using namespace std;

// Function to build the tree
void buildTree(vector<int>& arr,
               vector<int>& tree, int s,
               int e, int index)
{

    // Leaf Node
    if (s == e) {
        tree[index] = arr[s];
        return;
    }

    // Finding mid
    int mid = (s + e) / 2;

    buildTree(arr, tree, s,
              mid, 2 * index + 1);
    buildTree(arr, tree, mid + 1,
              e, 2 * index + 2);

    // Updating current node
    // by the maximum of its children
    tree[index]
        = max(tree[2 * index + 1],
              tree[2 * index + 2]);
}

// Function to find the maximum
// element in a given range
int query(vector<int>& tree, int s,
          int e, int index, int l,
          int r)
{

    if (l > e or r < s) {
        return INT_MIN;
    }

    if (l <= s and r >= e) {
        return tree[index];
    }

    int mid = (s + e) / 2;

    int left = query(tree, s, mid,
                     2 * index + 1, l, r);
    int right
        = query(tree, mid + 1, e,
                2 * index + 2, l, r);

    return max(left, right);
}

// Function to replace each array element by
// the maximum of K next and K previous elements
void updateArray(vector<int>& arr, int K)
{

    // To store the segment tree
    vector<int> tree(MAXN);

    int N = arr.size();
    buildTree(arr, tree, 0, N - 1, 0);

    for (int i = 0; i < N; ++i) {
        // For 0th index only find
        // the maximum out of 1 to i+K
        if (i == 0) {
            cout << query(tree, 0, N - 1, 0, 1,
                          min(i + K, N - 1))
                 << ' ';
            continue;
        }

        // For (N-1)th index only find
        // the maximum out of 0 to (N-2)
        if (i == N - 1) {
            cout << query(tree, 0, N - 1,
                          0, max(0, i - K),
                          N - 2);
            continue;
        }

        // Maximum from (i-K) to (i-1)
        int left = query(tree, 0, N - 1,
                         0, max(i - K, 0),
                         i - 1);

        // Maximum from (i+1) to (i+K)
        int right = query(tree, 0,
                          N - 1, 0, i + 1,
                          min(i + K, N - 1));

        cout << max(left, right) << ' ';
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 12, 5, 3, 9,
                        21, 36, 17 };
    int K = 2;

    updateArray(arr, K);
}
```

**Output**

```
5 12 21 36 36 21 36
```

**时间复杂度:**O(NlogN)
T3】辅助空间: O(1)
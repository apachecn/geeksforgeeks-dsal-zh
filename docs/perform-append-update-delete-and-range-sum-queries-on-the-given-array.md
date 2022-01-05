# 对给定数组执行追加、更新、删除和范围求和查询

> 原文:[https://www . geesforgeks . org/perform-append-update-delete-and-range-sum-对给定数组进行查询/](https://www.geeksforgeeks.org/perform-append-update-delete-and-range-sum-queries-on-the-given-array/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是回答以下类型的 **Q** 查询:

*   **1 X 0:** 在数组后面追加 **X** 。
*   **2 X Y:** 设置**arr【X】= Y**。
*   **3 X 0:** 删除**arr【X】**。
*   **4 X Y:** 求**【X，Y】**范围内的和。

**注意**在查询类型 **3** 中删除**arr【X】**后，索引 **X** 后的所有元素将左移一个位置。

**示例:**

> **输入:** arr[] = {1，2，5，3，4}，Q[][] = {
> {4，2，4}，
> {3，3，0}，
> {1，6，0}，
> {4，3，5 } }
> T7】输出:
> 10
> 13
> 第一次查询- >和(arr[1]，arr[2]，arr[3])
> 第二次查询
> 
> **输入:** arr[] = {1，2，3，4，5}，Q[][] = {
> {4，1，5}，
> {3，3，0}，
> {1，6，0}，
> {4，3，5}，
> {2，4，10}。
> {4，1，5}}
> **输出:**
> 15
> 15
> 23

**朴素方法:**解决这个问题的朴素方法是直接在给定的数组上执行查询，该数组的时间复杂度为 **O(Q * N)** 。

**高效方法:**

*   因为有一些数据结构，如[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)或[位(分支树)](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)，为每个查询提供**0(logN)**中的点更新和范围总和。
*   帖子用一棵分威克树来做同样的事情，所以强烈建议在分威克树中进行[点更新。](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)
*   但主要问题是执行删除操作(**类型-3 查询**)。表演后需要换挡，最差情况下会再次导致 **O(Q * N)** 。
*   可以使用一个技巧，在删除一个元素后，只需更新 **A[X] = 0** 处的值，并将 **X** 之后的索引映射到**X+X**之前删除的元素数量。
*   为了找到在 **X** 之前删除的元素数量，将使用另一个芬威克树(在实现中为 idx)，并在执行删除操作的索引处继续添加 **1** 。
*   这意味着在提取或获取特定索引时，可以查询 **idx** 树，并将索引 **X** 更新为 **X + sum(X，idx)** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Size of the array (MAX)
const int N = 2e5 + 10;

// To store the sum of
// the array elements
vector<int> bit(N, 0);

// To keep track of how many type 3
// queries have been performed before
// a particular index
vector<int> idx(N, 0);

// Function to perform the point
// update in Fenwick tree
void update(int idx, int val,
            vector<int>& bitt)
{
    while (idx < N) {
        bitt[idx] += val;
        idx += idx & (-idx);
    }
}

// Function to return the sum
// of the elements A[1...idx]
// from BIT
int sum(int idx,
        vector<int>& bitt)
{

    int res = 0;
    while (idx > 0) {
        res += bitt[idx];
        idx -= idx & (-idx);
    }

    return res;
}

// Function to perform the queries and
// return the answer vector
vector<int> peformQueries(vector<int>& A,
                          vector<vector<int> >& B)
{

    // For 1 bases indexing
    // insert 0 in the vector
    A.insert(A.begin(), 0);

    // Updated size of the vector
    int n = (int)A.size();

    // Updating the bit tree
    for (int i = 1; i < n; ++i) {
        update(i, A[i], bit);
    }

    // Vector to store the answers
    // of range sum
    vector<int> ans;

    // Iterating in the query
    // vector
    for (auto i : B) {

        int type = i[0];
        int x = i[1], v = i[2];

        // If the query is of
        // type 1
        if (type == 1) {

            // Updating the tree
            // with x in the last
            update(n, x, bit);

            // Pushing back the value
            // in the original vector
            A.push_back(x);

            // Incrementing the size
            // of the vector by 1
            n++;
        }

        // If the query is of type 2
        else if (type == 2) {

            // Getting the updated index
            // in case of any query of
            // type 3 occured before it
            int id = x + sum(x, idx);

            // Making the effect to that
            // value to 0 by subtracting
            // same value from the tree
            update(id, -A[id], bit);

            // Updating the A[id] to v
            A[id] = v;

            // Now update the
            // bit by v at x
            update(id, v, bit);
        }

        // If the query is of type 3
        else if (type == 3) {

            // Get the current index
            int id = x + sum(x, idx);

            // Remove the effect of that
            // index from the bit tree
            update(id, -A[id], bit);

            // Update the idx tree
            // because one element has
            // been deleted
            update(x, 1, idx);

            // Update the idx val to 0
            A[id] = 0;
        }

        // If the query is of type 4
        else {

            // Get the updated range
            int xx = x + sum(x, idx);
            int vv = v + sum(v, idx);

            // Push_back the value
            ans.push_back(sum(vv, bit)
                          - sum(xx - 1, bit));
        }
    }

    return ans;
}

// Driver code
int main()
{
    vector<int> A = { 1, 2, 5, 3, 4 };

    // Queries
    vector<vector<int> > B = {
        { 4, 2, 4 },
        { 3, 3, 0 },
        { 1, 6, 0 },
        { 4, 3, 5 },
    };

    // Get the answer array
    vector<int> ans = peformQueries(A, B);

    // printing the answer
    for (int i : ans)
        cout << i << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Size of the array (MAX)
    static int N = (int) 2e5 + 10;

    // To store the sum of
    // the array elements
    static int[] bit = new int[N];

    // To keep track of how many type 3
    // queries have been performed before
    // a particular index
    static int[] idx = new int[N];

    // Function to perform the point
    // update in Fenwick tree
    static void update(int idx, int val, int[] bitt) {
        while (idx < N) {
            bitt[idx] += val;
            idx += idx & (-idx);
        }
    }

    // Function to return the sum
    // of the elements A[1...idx]
    // from BIT
    static int sum(int idx, int[] bitt) {

        int res = 0;
        while (idx > 0) {
            res += bitt[idx];
            idx -= idx & (-idx);
        }

        return res;
    }

    // Function to perform the queries and
    // return the answer vector
    static Vector<Integer> peformQueries(Vector<Integer> A, int[][] B) {

        // For 1 bases indexing
        // insert 0 in the vector
        A.insertElementAt(0, 0);

        // Updated size of the vector
        int n = (int) A.size();

        // Updating the bit tree
        for (int i = 1; i < n; ++i) {
            update(i, A.elementAt(i), bit);
        }

        // Vector to store the answers
        // of range sum
        Vector<Integer> ans = new Vector<>();

        // Iterating in the query
        // vector
        for (int[] i : B) {

            int type = i[0];
            int x = i[1], v = i[2];

            // If the query is of
            // type 1
            if (type == 1) {

                // Updating the tree
                // with x in the last
                update(n, x, bit);

                // Pushing back the value
                // in the original vector
                A.add(x);

                // Incrementing the size
                // of the vector by 1
                n++;
            }

            // If the query is of type 2
            else if (type == 2) {

                // Getting the updated index
                // in case of any query of
                // type 3 occured before it
                int id = x + sum(x, idx);

                // Making the effect to that
                // value to 0 by subtracting
                // same value from the tree
                update(id, -A.elementAt(id), bit);

                // Updating the A[id] to v
                A.set(id, v);

                // Now update the
                // bit by v at x
                update(id, v, bit);
            }

            // If the query is of type 3
            else if (type == 3) {

                // Get the current index
                int id = x + sum(x, idx);

                // Remove the effect of that
                // index from the bit tree
                update(id, -A.elementAt(id), bit);

                // Update the idx tree
                // because one element has
                // been deleted
                update(x, 1, idx);

                // Update the idx val to 0
                A.set(id, 0);
            }

            // If the query is of type 4
            else {

                // Get the updated range
                int xx = x + sum(x, idx);
                int vv = v + sum(v, idx);

                // Push_back the value
                ans.add(sum(vv, bit) - sum(xx - 1, bit));
            }
        }

        return ans;
    }

    // Driver Code
    public static void main(String[] args) {
        Integer[] a = { 1, 2, 5, 3, 4 };
        Vector<Integer> A = new Vector<Integer>(Arrays.asList(a));

        // Queries
        int[][] B = { { 4, 2, 4 }, { 3, 3, 0 }, { 1, 6, 0 }, { 4, 3, 5 } };

        // Get the answer array
        Vector<Integer> ans = peformQueries(A, B);

        // printing the answer
        for (int i : ans)
            System.out.println(i);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python implementation of the approach

# Size of the array (MAX)
N = int(2e5) + 10

# To store the sum of
# the array elements
bit = [0] * N

# To keep track of how many type 3
# queries have been performed before
# a particular index
idx = [0] * N

# Function to perform the point
# update in Fenwick tree
def update(index: int, val: int, bitt: list):
    while index < N:
        bitt[index] += val
        index += index & -index

# Function to return the sum
# of the elements A[1...idx]
# from BIT
def summation(index: int, bitt: list) -> int:
    res = 0
    while index > 0:
        res += bitt[index]
        index -= index & -index
    return res

# Function to perform the queries and
# return the answer vector
def performQueries(A: list, B: list) -> list:
    global bit, idx

    # For 1 bases indexing
    # insert 0 in the vector
    A.insert(0, 0)

    # Updated size of the vector
    n = len(A)

    # Updating the bit tree
    for i in range(1, n):
        update(i, A[i], bit)

    # Vector to store the answers
    # of range sum
    ans = []

    # Iterating in the query
    # vector
    for i in B:
        type = i[0]
        x = i[1]
        v = i[2]

        # If the query is of
        # type 1
        if type == 1:

            # Updating the tree
            # with x in the last
            update(n, x, bit)

            # Pushing back the value
            # in the original vector
            A.append(x)

            # Incrementing the size
            # of the vector by 1
            n += 1

        # If the query is of type 2
        elif type == 2:

            # Getting the updated index
            # in case of any query of
            # type 3 occured before it
            id = x + summation(x, idx)

            # Making the effect to that
            # value to 0 by subtracting
            # same value from the tree
            update(id, -A[id], bit)

            # Updating the A[id] to v
            A[id] = v

            # Now update the
            # bit by v at x
            update(id, v, bit)

        # If the query is of type 3
        elif type == 3:

            # Get the current index
            id = x + summation(x, idx)

            # Remove the effect of that
            # index from the bit tree
            update(id, -A[id], bit)

            # Update the idx tree
            # because one element has
            # been deleted
            update(x, 1, idx)

            # Update the idx val to 0
            A[id] = 0

        # If the query is of type 4
        else:

            # Get the updated range
            xx = x + summation(x, idx)
            vv = v + summation(v, idx)

            # Push_back the value
            ans.append(summation(vv, bit) - summation(xx - 1, bit))
    return ans

# Driver Code
if __name__ == "__main__":
    A = [1, 2, 5, 3, 4]

    # Queries
    B = [[4, 2, 4], [3, 3, 0], [1, 6, 0], [4, 3, 5]]

    # Get the answer array
    ans = performQueries(A, B)

    # printing the answer
    for i in ans:
        print(i)

# This code is contributed by
# sanjeev2552
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Size of the array (MAX)
const N = 2e5 + 10;

// To store the sum of
// the array elements
let bit = new Array(N).fill(0);

// To keep track of how many type 3
// queries have been performed before
// a particular index
let idx = new Array(N).fill(0);

// Function to perform the point
// update in Fenwick tree
function update(idx, val, bitt) {
    while (idx < N) {
        bitt[idx] += val;
        idx += idx & (-idx);
    }
}

// Function to return the sum
// of the elements A[1...idx]
// from BIT
function sum(idx, bitt) {

    let res = 0;
    while (idx > 0) {
        res += bitt[idx];
        idx -= idx & (-idx);
    }

    return res;
}

// Function to perform the queries and
// return the answer vector
function peformQueries(A, B) {

    // For 1 bases indexing
    // insert 0 in the vector
    A.unshift(0);

    // Updated size of the vector
    let n = A.length;

    // Updating the bit tree
    for (let i = 1; i < n; ++i) {
        update(i, A[i], bit);
    }

    // Vector to store the answers
    // of range sum
    let ans = new Array();

    // Iterating in the query
    // vector
    for (let i of B) {

        let type = i[0];
        let x = i[1], v = i[2];

        // If the query is of
        // type 1
        if (type == 1) {

            // Updating the tree
            // with x in the last
            update(n, x, bit);

            // Pushing back the value
            // in the original vector
            A.push(x);

            // Incrementing the size
            // of the vector by 1
            n++;
        }

        // If the query is of type 2
        else if (type == 2) {

            // Getting the updated index
            // in case of any query of
            // type 3 occurred before it
            let id = x + sum(x, idx);

            // Making the effect to that
            // value to 0 by subtracting
            // same value from the tree
            update(id, -A[id], bit);

            // Updating the A[id] to v
            A[id] = v;

            // Now update the
            // bit by v at x
            update(id, v, bit);
        }

        // If the query is of type 3
        else if (type == 3) {

            // Get the current index
            let id = x + sum(x, idx);

            // Remove the effect of that
            // index from the bit tree
            update(id, -A[id], bit);

            // Update the idx tree
            // because one element has
            // been deleted
            update(x, 1, idx);

            // Update the idx val to 0
            A[id] = 0;
        }

        // If the query is of type 4
        else {

            // Get the updated range
            let xx = x + sum(x, idx);
            let vv = v + sum(v, idx);

            // Push the value
            ans.push(sum(vv, bit)
                - sum(xx - 1, bit));
        }
    }

    return ans;
}

// Driver code

let A = [1, 2, 5, 3, 4];

// Queries
let B = [
    [4, 2, 4],
    [3, 3, 0],
    [1, 6, 0],
    [4, 3, 5],
];

// Get the answer array
let ans = peformQueries(A, B);

// printing the answer
for (let i of ans)
    document.write(i + "<br>");

// This code is contributed by gfgking
</script>
```

**Output:** 

```
10
13
```

**时间复杂度:**O(Q * logN+NlogN)
T3】辅助空间 : O(N)。
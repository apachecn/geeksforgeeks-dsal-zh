# 对矩阵中的反转对进行计数

> 原文:[https://www.geeksforgeeks.org/count-inversion-pairs-matrix/](https://www.geeksforgeeks.org/count-inversion-pairs-matrix/)

给定一个大小为 **NxN** 的矩阵 **A** ，我们需要找到其中的反转对的数量。矩阵中的求逆计数定义为满足以下条件的对数:

*   x<sub>1</sub>≤x<sub>2</sub>
*   y<sub>1</sub>≤和 <sub>2</sub>
*   A【x<sub>2</sub>【y<sub>2</sub><A【x<sub>1</sub>【y<sub>1</sub>

**约束:**

*   1 ≤ A <sub>i、j</sub> ≤ 10 <sup>9</sup>
*   1 ≤ N ≤ 10 <sup>3</sup>

示例:

```
For simplicity, let's take a 2x2 matrix :
A = {{7, 5},
     {3, 1}};
The inversion pairs are : (7, 5), (3, 1), (7, 3), (5, 1) and (7, 1)
Output : 5

```

要解决这个问题，我们需要知道以下几点:

1.  使用二进制索引树(BIT)
    [在 1D 数组中查找反转对的数量](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit)
2.  2D 比特
    T1

因为，我们需要找到一个矩阵中的逆矩阵对的数量，我们需要做的第一件事是将矩阵的元素存储在另一个数组中，比如 v，并对数组 v 进行排序，这样我们就可以将未排序矩阵的元素与 v 进行比较，并使用 BIT 找到逆矩阵对的数量。但是给定元素的值非常大(10 <sup>9</sup> ，所以我们不能将矩阵中元素的值用作 BIT 中的索引。因此，我们需要使用元素的位置作为 2D 双边投资条约的索引。
我们将对矩阵的每个元素使用元组(-A[i][j]，I，j)，并将其存储在一个数组中，比如“v”。然后我们需要按照-A[i][j]的值按升序对 v 进行排序，这样矩阵的最大元素将存储在索引 0 处，最小元素存储在 v 的最后一个索引处。现在，问题简化为在 1D 数组中查找反转对，唯一的例外是我们将使用 2D BIT。
注意，这里我们使用的是 A[i][j]的负值，只是因为我们要从左向右遍历 v，即从矩阵中最大的数到最小的数(因为这是我们在使用 BIT 寻找 1D 阵列中的反转对时所做的)。也可以使用正值，从右向左遍历 v，最终结果将保持不变。

**算法:**

```
1\. Initialize inv_pair_cnt = 0, which will store the number of inversion pairs.
2\. Store the tuple (-A[i][j], i, j) in an array, say v, where A[i][j] is the
   element of the matrix A at position (i, j).
3\. Sort the array v according to the first element of the tuple, i.e., 
   according to the value of -A[i][j].
4\. Traverse the array v and do the following :
       - Initialize an array, say 'pairs' to store the position (i, j)
         of the tuples of v. 
       - while the current tuple of v and all its adjacent tuples whose 
         first value, i.e., -A[i][j] is same, do 
             - Push the current tuple's position pair (i, j) into 'pairs'.
             - Add to inv_pair_cnt,  the number of elements which are less than 
               the current element(i.e., A[i][j]) and lie on the right side 
               in the sorted array v, by calling the query operation of BIT and 
               passing i and j as arguments.
       - For each position pair (i, j) stored in the array 'pairs', 
         update the position (i, j) in the 2D BIT by 1.
5\. Finally, inv_pair_cnt will contain the number of inversion pairs.

```

下面是实现:

## C++

```
// C++ program to count the number of inversion
// pairs in a 2D matrix
#include <bits/stdc++.h>
using namespace std;

// for simplicity, we are taking N as 4
#define N 4

// Function to update a 2D BIT. It updates the
// value of bit[l][r] by adding val to bit[l][r]
void update(int l, int r, int val, int bit[][N + 1])
{
    for (int i = l; i <= N; i += i & -i)
        for (int j = r; j <= N; j += j & -j)
            bit[i][j] += val;
}

// function to find cumulative sum upto
// index (l, r) in the 2D BIT
long long query(int l, int r, int bit[][N + 1])
{
    long long ret = 0;
    for (int i = l; i > 0; i -= i & -i)
        for (int j = r; j > 0; j -= j & -j)
            ret += bit[i][j];

    return ret;
}

// function to count and return the number
// of inversion pairs in the matrix
long long countInversionPairs(int mat[][N])
{
    // the 2D bit array and initialize it with 0.
    int bit[N+1][N+1] = {0};

    // v will store the tuple (-mat[i][j], i, j)
    vector<pair<int, pair<int, int> > > v;

    // store the tuples in the vector v
    for (int i = 0; i < N; ++i)
        for (int j = 0; j < N; ++j)

            // Note that we are not using the pair
            // (0, 0) because BIT update and query
            // operations are not done on index 0
            v.push_back(make_pair(-mat[i][j],
                        make_pair(i+1, j+1)));

    // sort the vector v according to the
    // first element of the tuple, i.e., -mat[i][j]
    sort(v.begin(), v.end());

    // inv_pair_cnt will store the number of
    // inversion pairs
    long long inv_pair_cnt = 0;

    // traverse all the tuples of vector v
    int i = 0;
    while (i < v.size())
    {
        int curr = i;

        // 'pairs' will store the position of each element,
        // i.e., the pair (i, j) of each tuple of the vector v
        vector<pair<int, int> > pairs;

        // consider the current tuple in v and all its
        // adjacent tuples whose first value, i.e., the
        // value of –mat[i][j] is same
        while (curr < v.size() &&
               (v[curr].first == v[i].first))
        {
            // push the position of the current element in 'pairs'
            pairs.push_back(make_pair(v[curr].second.first,
                                      v[curr].second.second));

            // add the number of elements which are
            // less than the current element and lie on the right
            // side in the vector v
            inv_pair_cnt += query(v[curr].second.first,
                                  v[curr].second.second, bit);

            curr++;
        }

        vector<pair<int, int> >::iterator it;

        // traverse the 'pairs' vector
        for (it = pairs.begin(); it != pairs.end(); ++it)
        {
            int x = it->first;
            int y = it->second;

            // update the position (x, y) by 1
            update(x, y, 1, bit);
        }

        i = curr;
    }

    return inv_pair_cnt;
}

// Driver program
int main()
{
    int mat[N][N] = { { 4, 7, 2, 9 },
                      { 6, 4, 1, 7 },
                      { 5, 3, 8, 1 },
                      { 3, 2, 5, 6 } };

    long long inv_pair_cnt = countInversionPairs(mat);

    cout << "The number of inversion pairs are : "
         << inv_pair_cnt << endl;

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to count the number of inversion
# pairs in a 2D matrix

# for simplicity, we are taking N as 4
N = 4

# Function to update a 2D BIT. It updates the
# value of bit[l][r] by adding val to bit[l][r]
def update(l, r, val, bit):
    i = l
    while(i <= N):
        j = r
        while(j <= N): 
            bit[i][j] += val
            j += j & -j
        i += i & -i

# function to find cumulative sum upto
# index (l, r) in the 2D BIT
def query(l, r, bit):
    ret = 0
    i = l
    while(i > 0):
        j = r
        while(j > 0):
            ret += bit[i][j]
            j -= j & -j
        i -= i & -i

    return ret

# function to count and return the number
# of inversion pairs in the matrix
def countInversionPairs(mat):

    # the 2D bit array and initialize it with 0.
    bit = [[0 for i in range(N + 1)] for j in range(N + 1)]

    # v will store the tuple (-mat[i][j], i, j)
    v = []

    # store the tuples in the vector v
    for i in range(N):
        for j in range(N):

            # Note that we are not using the pair
            # (0, 0) because BIT update and query
            # operations are not done on index 0
            v.append([-mat[i][j], [i + 1, j + 1]])

    # sort the vector v according to the
    # first element of the tuple, i.e., -mat[i][j]
    v.sort()

    # inv_pair_cnt will store the number of
    # inversion pairs
    inv_pair_cnt = 0

    # traverse all the tuples of vector v
    i = 0
    while (i < len(v)):

        curr = i

        # 'pairs' will store the position of each element,
        # i.e., the pair (i, j) of each tuple of the vector v
        pairs = []

        # consider the current tuple in v and all its
        # adjacent tuples whose first value, i.e., the
        # value of –mat[i][j] is same
        while (curr < len(v) and (v[curr][0] == v[i][0])):

            # push the position of the current element in 'pairs'
            pairs.append([v[curr][1][0], v[curr][1][1]])

            # add the number of elements which are
            # less than the current element and lie on the right
            # side in the vector v
            inv_pair_cnt += query(v[curr][1][0], v[curr][1][1], bit)
            curr += 1

        # traverse the 'pairs' vector
        for it in pairs:
            x = it[0]
            y = it[1]

            # update the position (x, y) by 1
            update(x, y, 1, bit)

        i = curr

    return inv_pair_cnt

# Driver code
mat = [[4, 7, 2, 9 ],[ 6, 4, 1, 7 ],
        [ 5, 3, 8, 1 ],[3, 2, 5, 6]]

inv_pair_cnt = countInversionPairs(mat)

print("The number of inversion pairs are :", inv_pair_cnt)

# This code is contributed by shubhamsingh10
```

**Output:**

```
The number of inversion pairs are : 43

```

**时间复杂度** : O(log(NxN))，其中 N 是矩阵的大小
T3】空间复杂度 : O(NxN)

本文由**阿维纳什库马尔锯**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
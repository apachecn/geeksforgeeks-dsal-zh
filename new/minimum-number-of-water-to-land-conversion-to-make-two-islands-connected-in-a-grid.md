# 在一个网格中连接两个岛的最少水土转换数量

> 原文：[https://www.geeksforgeeks.org/minimum-number-of-water-to-land-conversion-to-make-two-islands-connected-in-a-grid/](https://www.geeksforgeeks.org/minimum-number-of-water-to-land-conversion-to-make-two-islands-connected-in-a-grid/)

给定 2D 网格**'W'**和**'L'**的 **arr [] []** ，其中**'W'**表示水，**'L'**表示土地，任务是找到必须更改为土地成分**'L'**的最小水分量**'W'**，以便有两个岛屿 连接。

> **岛**是已连接的**'L'**的集合。

**注意**：只能有两个不相交的岛。

**示例**：

> **输入**：arr [] [] = {{'W'，'L'}，{'L'，'W'}};
> **输出**：1
> **说明**：
> 对于给定的孤岛，如果将 arr [1] [1]更改为“ W”，则将 所有岛屿均已连接。
> 因此，必须将“ W”的最小数目更改为“ L”为 1。
> 
> **输入**：arr [] [] = {{'W'，'L'，'W'}，{'W'，'W'，'W'}，{'W'，'W '，'L'}}
> **输出**：2

**方法**：可以使用 [Floodfill 算法](https://www.geeksforgeeks.org/flood-fill-algorithm-implement-fill-paint/)解决此问题。 步骤如下：

1.  对第一组连接的孤岛使用 Floodfill 算法，使所有孤岛都已访问，并将坐标存储在[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)中（例如 **hash1** ）。

2.  对第二组连接的孤岛使用 Floodfill 算法，使所有孤岛都已访问，并将坐标存储在第二个哈希中（例如 **hash2** ）。

3.  存储在两个哈希中的坐标之间的最小差是必需的结果。

下面是上述方法的实现：

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
[
// Determine the distance between two
// coordinates
int dist(pair< int , int >& p1,
pair< int , int >& p2)
{
return abs (p1.first - p2.first)
+ abs (p2.second - p1.second) - 1;
}
// Function to implement floodfill algorithm
]
void floodfill(set<pair< int , int > >& hash,
int i, int j,
vector<vector< char > >& A)
{
// Base Case
if (i < 0 || i >= A.size() || j < 0
|| j >= A[0].size() || A[i][j] != 'L' ) {
return ;
}
]
// Mark the current node visited
A[i][j] = 'V' ;
// Store the coordinates of in the
// hash set
hash.insert(make_pair(i, j));
// Recursively iterate for the next
// four directions
floodfill(hash, i - 1, j, A);
floodfill(hash, i + 1, j, A);
floodfill(hash, i, j - 1, A);
floodfill(hash, i, j + 1, A);
}
// Funtion to find the minimum 'W' to flipped
void findMinimumW(vector<vector< char > >& A)
{
// Base Case
if (A.size() == 0)
return ;
// Two sets to store the coordinates of
// connected island
set<pair< int , int > > hash1, hash2;
// Traversing the given grid[][]
for ( int i = 0; i < A.size(); i++) {
[
for ( int j = 0; j < A[0].size(); j++) {
// If an island is found
if (A[i][j] == 'L' ) {
// Floodfill Algorithm for
// the first island
if (hash1.empty()) {
floodfill(hash1, i, j, A);
}
// Floodfill Algorithm for
// the second island
if (hash2.empty()
&& !hash1.count({ i, j })) {
floodfill(hash2, i, j, A);
}
}
}
}
// To store the minimum count of 'W'
int ans = INT_MAX;
// Traverse both pairs of hashes
for ] ( auto i : hash1) {
for ( auto j : hash2) {
ans = min(ans, dist(i, j));
}
}
// Print the final answer
cout << ans << endl;
}
// Driver Code
int main() [HT G424]
{
// Given grid of land and water
vector<vector< char > > arr;
arr = { { 'W' , 'L' }, { 'L' , 'W' } };
// Function Call
findMinimumW(arr);
return 0;
}
```

**Output:**

```
1

```

 ***时间复杂度**：`O(N ^ 2)`* 



* * *

* * *




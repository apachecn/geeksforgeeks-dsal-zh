# 不同对边的数量，以便将两棵树划分为相同的节点子集

给定两个树，每个 N 个节点。 删除树的边缘会将树分为两个子集。

求出不同边的最大总数（e1，e2）：第一棵树的 e1 和第二棵树的 e2，以便将这两个树划分为具有相同节点的子集。

**示例：**
![](img/41498ba573c3aac721a100841d46ec7b.png)

> **输入**：与上图相同 N = 6
> 树 1：{（1、2），（2、3），（3、4），（4、5），（5， 6）}
> 树 2：{（1、2），（2、3），（1、6），（6、5），（5、4）}
> **输出：** 1
> 我们可以在第一个图形中删除边 3-4，在第二个图形中删除边 1-6。
> 子集将为{1、2、3}和{4、5、6}。
> 
> **输入：** N = 4
> 树 1：{（1，2），（1，3），（1，4）}
> 树 2：{（1，2），（ 2，4），（1，3）}
> **输出：** 2
> 我们可以在第一个图形中选择边 1-3，在第二个图形中选择边 1-3。
> 这两个图的子集分别为{3}和{1、2、4}。
> 同样，我们可以在第一个图形中选择边 1-4，在第二个图形中选择边 2-4。
> 这两个图的子集分别为{4}和{1、2、3}

**方法：**

*   这个想法是在树上使用散列，我们将两个树都作为节点 1 的根，然后将随机值分配给树的每个节点。
*   我们将在树上执行 dfs，并假设我们在节点 x 上，然后将保留一个变量
    subtree [x]，该变量将在其子树中存储所有节点的哈希值。
*   我们完成了上述两个步骤，剩下的就是为我们得到的两个树存储节点的每个子树的值。
*   我们可以使用无序列图。 最后一步是找到两个树都有多少 subtree [x]的公共值。
*   对于两棵树的 subtree [x]的每个公共值，将不同边缘的计数增加+1。

下面是上述方法的实现：

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const long long p = 97, MAX = 300005;
// This function checks whether
// a node is leaf node or not.
bool leaf1(long long NODE, long long int deg1[])
{
if (deg1[NODE] == 1 and NODE != 1)
return true;
return false;
}
// This function calculates the Hash sum
// of all the children of a
// particular node for subtree 1
void dfs3(long long curr, long long par,
vector<long long int> tree1[],
long long int subtree1[], long long int deg1[],
long long int node[])
{
for (auto& child : tree1[curr]) {
if (child == par)
continue;
dfs3(child, curr, tree1, subtree1, deg1, node);
}
// If the node is leaf node then
// there is no child, so hash sum
// will be same as the
// hash value for the node.
if (leaf1(curr, deg1) == true) {
subtree1[curr] = node[curr];
return;
}
long long sum = 0;
// Else calculate hash sum of all the
// children of a particular node, this is done
// by iterating on all the children of a node.
for (auto& child : tree1[curr]) {
sum = sum + subtree1[child];
}
// store the hash value for
// all the subtree of current node
subtree1[curr] = node[curr] + sum;
return;
}
// This function checks whether
// a node is leaf node or not.
bool leaf2(long long NODE, long long int deg2[])
{
if (deg2[NODE] == 1 and NODE != 1)
return true;
return false;
}
// This function calculates the Hash
// sum of all the children of
// a particular node for subtree 2.
void dfs4(long long curr, long long par,
vector<long long int> tree2[],
long long int subtree2[], long long int deg2[],
long long int node[])
{
for (auto& child : tree2[curr]) {
if (child == par)
continue;
dfs4(child, curr, tree2, subtree2, deg2, node);
}
// If the node is leaf node then
// there is no child, so hash sum will be
// same as the hash value for the node.
if (leaf2(curr, deg2) == true) {
subtree2[curr] = node[curr];
return;
}
long long sum = 0;
// Else calculate hash sum of all
// the children of a particular node, this is
// done by iterating on all the children of a node.
for (auto& child : tree2[curr]) {
sum = sum + subtree2[child];
}
// store the hash value for
// all the subtree of current node
subtree2[curr] = node[curr] + sum;
}
// Calculates x^y in logN time.
long long exp(long long x, long long y)
{
if (y == 0)
return 1;
else if (y & 1)
return x * exp(x, y / 2) * exp(x, y / 2);
else
return exp(x, y / 2) * exp(x, y / 2);
}
// This function helps in building the tree
void Insertt(vector<long long int> tree1[],
vector<long long int> tree2[],
long long int deg1[], long long int deg2[])
{
// Building Tree 1
tree1[1].push_back(2);
tree1[2].push_back(1);
tree1[2].push_back(3);
tree1[3].push_back(2);
tree1[3].push_back(4);
tree1[4].push_back(3);
tree1[4].push_back(5);
tree1[5].push_back(4);
tree1[5].push_back(6);
tree1[6].push_back(5);
// Since 6 is a leaf node for tree 1
deg1[6] = 1;
// Building Tree 2
tree2[1].push_back(2);
tree2[2].push_back(1);
tree2[2].push_back(3);
tree2[3].push_back(2);
tree2[1].push_back(6);
tree2[6].push_back(1);
tree2[6].push_back(5);
tree2[5].push_back(6);
tree2[5].push_back(4);
tree2[4].push_back(5);
// since both 3 and 4 are leaf nodes of tree 2 .
deg2[3] = 1;
deg2[4] = 1;
}
// Function to make the hash values
void TakeHash(long long n, long long int node[])
{
// Take a very high prime
long long p = 97 * 13 * 19;
// Initialize random values to each node .
for (long long i = 1; i <= n; ++i) {
// A good random function is
// choosen for each node .
long long val = (rand() * rand() * rand())
+ rand() * rand() + rand();
node[i] = val * p * rand() + p * 13 * 19 * rand() * rand() * 101 * p;
p *= p;
p *= p;
}
}
// Function that returns the required answer
void solve(long long n, vector<long long int> tree1[],
vector<long long int> tree2[], long long int subtree1[],
long long int subtree2[], long long int deg1[],
long long int deg2[], long long int node[])
{
// Do dfs on both trees to
// get subtree[x] for each node.
dfs3(1, 0, tree1, subtree1, deg1, node);
dfs4(1, 0, tree2, subtree2, deg2, node);
// cnt_tree1 and cnt_tree2 is used
// to store the count of all
// the hashes of every node .
unordered_map<long long, long long>
cnt_tree1, cnt_tree2;
vector<long long> values;
for (long long i = 1; i <= n; ++i) {
long long value1 = subtree1[i];
long long value2 = subtree2[i];
// Store the subtree value of tree 1
// in a vector to compare it later
// with subtree value of tree 2.
values.push_back(value1);
// increment the count of hash
// value for a subtree of a node.
cnt_tree1[value1]++;
cnt_tree2[value2]++;
}
// Stores the sum of all the hash values
// of children for root node of subtree 1.
long long root_tree1 = subtree1[1];
long long root_tree2 = subtree2[1];
// Stores the sum of all the hash values
// of children for root node of subtree 1.
cnt_tree1[root_tree1] = 0;
cnt_tree2[root_tree2] = 0;
long long answer = 0;
for (auto& x : values) {
// Check if for a given hash value for
// tree 1 is there any hash value which
// matches to hash value of tree 2
// If yes, then its possible to divide
// the tree for this hash value
// into two equal subsets.
if (cnt_tree1[x] != 0 and cnt_tree2[x] != 0)
++answer;
}
cout << answer << endl;
}
// Driver Code
int main()
{
vector<long long int> tree1[MAX], tree2[MAX];
long long int node[MAX], deg1[MAX], deg2[MAX];
long long int subtree1[MAX], subtree2[MAX];
long long n = 6;
// To generate a good random function
srand(time(NULL));
Insertt(tree1, tree2, deg1, deg2);
TakeHash(n, node);
solve(n, tree1, tree2, subtree1, subtree2, deg1, deg2, node);
return 0;
}
```

**Output:**

```
1

```

**时间复杂度**：O（N）

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。
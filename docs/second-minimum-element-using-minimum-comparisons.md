# 使用最小比较的第二个最小元素

> 原文:[https://www . geesforgeks . org/second-minimum-element-use-minimum-comparisons/](https://www.geeksforgeeks.org/second-minimum-element-using-minimum-comparisons/)

给定一个整数数组，找到最小(或最大)元素，在不到 2n 次的比较中找到比它大(或小)的元素。给定的数组不必排序。允许额外的空间。

示例:

```
Input: {3, 6, 100, 9, 10, 12, 7, -1, 10}
Output: Minimum: -1, Second minimum: 3

```

我们已经在下面的帖子中讨论了一种方法。
[求数组中最小和第二小的元素](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)

如果数组元素的大小很大，例如很大的字符串，那么数组元素的比较成本很高。我们可以尽量减少上述方法中使用的比较次数。

想法是基于[比武树](https://www.geeksforgeeks.org/tournament-tree-and-binary-heap/)。将给定数组中的每个元素视为叶节点。

![tournamenttree](img/5d61bf5e3b505e05c2e66757ce2cf92a.png)

首先，我们通过建立一个锦标赛开球来找到最小的元素。为了构建树，我们将所有相邻的元素对(叶节点)相互比较。现在我们有 n/2 个元素比它们的对应物小(从每一对中，较小的元素形成叶子上面的层次)。同样，在每对 n/4 中找到较小的元素。继续这个过程，直到树的根被创建。根是最小的。
接下来，我们遍历树，在遍历的同时，我们丢弃根大于最小元素的子树。在丢弃之前，我们更新第二个最小的元素，它将保存我们的结果。这里需要理解的一点是，树的高度是平衡的，我们只需要花费 logn 的时间来遍历所有的元素，这些元素与步骤 1 中的最小值进行了比较。因此，总的时间复杂度是 **n + logn** 。所需的辅助空间是 O(2n)，因为叶节点的数量将大约等于内部节点的数量。

```
// C++ program to find minimum and second minimum
// using minimum number of comparisons
#include <bits/stdc++.h>
using namespace std;

// Tournament Tree node
struct Node
{
    int idx;
    Node *left, *right;
};

// Utility function to create a tournament tree node
Node *createNode(int idx)
{
    Node *t = new Node;
    t->left = t->right = NULL;
    t->idx = idx;
    return t;
}

// This function traverses tree across height to
// find second smallest element in tournament tree.
// Note that root is smallest element of tournament
// tree.
void traverseHeight(Node *root, int arr[], int &res)
{
    // Base case
    if (root == NULL || (root->left == NULL &&
                         root->right == NULL))
        return;

    // If left child is smaller than current result,
    // update result and recur for left subarray.
    if (res > arr[root->left->idx] &&
       root->left->idx != root->idx)
    {
        res = arr[root->left->idx];
        traverseHeight(root->right, arr, res);
    }

    // If right child is smaller than current result,
    // update result and recur for left subarray.
    else if (res > arr[root->right->idx] &&
             root->right->idx != root->idx)
    {
        res = arr[root->right->idx];
        traverseHeight(root->left, arr, res);
    }
}

// Prints minimum and second minimum in arr[0..n-1]
void findSecondMin(int arr[], int n)
{
    // Create a list to store nodes of current
    // level
    list<Node *> li;

    Node *root = NULL;
    for (int i = 0; i < n; i += 2)
    {
        Node *t1 = createNode(i);
        Node *t2 = NULL;
        if (i + 1 < n)
        {
            // Make a node for next element
            t2 = createNode(i + 1);

            // Make smaller of two as root
            root = (arr[i] < arr[i + 1])? createNode(i) :
                                       createNode(i + 1);

            // Make two nodes as children of smaller
            root->left = t1;
            root->right = t2;

            // Add root
            li.push_back(root);
        }
        else
            li.push_back(t1);
    }

    int lsize = li.size();

    // Construct the complete tournament tree from above
    // prepared list of winners in first round.
    while (lsize != 1)
    {
        // Find index of last pair
        int last = (lsize & 1)? (lsize - 2) : (lsize - 1);

        // Process current list items in pair
        for (int i = 0; i < last; i += 2)
        {
            // Extract two nodes from list, make a new
            // node for winner of two
            Node *f1 = li.front();
            li.pop_front();

            Node *f2 = li.front();
            li.pop_front();
            root = (arr[f1->idx] < arr[f2->idx])?
                createNode(f1->idx) : createNode(f2->idx);

            // Make winner as parent of two
            root->left = f1;
            root->right = f2;

            // Add winner to list of next level
            li.push_back(root);
        }
        if (lsize & 1)
        {
            li.push_back(li.front());
            li.pop_front();
        }
        lsize = li.size();
    }

    // Traverse tree from root to find second minimum
    // Note that minimum is already known and root of
    // tournament tree.
    int res = INT_MAX;
    traverseHeight(root, arr, res);
    cout << "Minimum: " << arr[root->idx]
        << ", Second minimum: " << res << endl;
}

// Driver code
int main()
{
    int arr[] = {61, 6, 100, 9, 10, 12, 17};
    int n = sizeof(arr)/sizeof(arr[0]);
    findSecondMin(arr, n);
    return 0;
}
```

输出:

```
Minimum: 6, Second minimum: 9

```

我们可以通过避免创建叶节点来优化上述代码，因为信息存储在数组本身中(我们知道元素是成对比较的)。

本文由 **Dhruv** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
# 以给定的顺序和级别顺序遍历插入 n 元树

> 原文:[https://www . geesforgeks . org/n 进制插入树给定顺序和级别顺序遍历/](https://www.geeksforgeeks.org/insertion-in-n-ary-tree-in-given-order-and-level-order-traversal/)

给定一组父节点，其中数组的索引是每个节点值的子节点，任务是将节点作为一个林(多个树组合在一起)插入，其中每个父节点可以有两个以上的子节点。插入节点后，以排序格式打印每一级。

**示例:**

> **输入:** arr[] = {5，3，-1，2，5，3}
> **输出:**
> -1
> 2
> 3
> 1 5
> **输入:** arr[] = {-1，-1，-1，-1，-1，1}
> **输出:**
> -1
> 0 1 2 3 4
> 5

以下是对上述例子的解释:

*   **例 1:**
    *   在这个给定的数组中，数组的元素将是父节点，数组索引将是子节点。

    *   最初，我们将林的根设置为-1，以供参考。
    *   现在遍历数组，我们将节点插入到林结构中。
    *   最初，我们识别森林中各棵树的根，并将它们插入到森林的根中。

    *   -1 的指数是 2。打印-1 并追加 2 作为子节点。
    *   现在在列表中搜索列表值为 2。索引 3 的值为 2。因此 3 成为 2 的孩子。

    *   现在，值为 3 的索引是 1 和 5。所以 1 和 5 是 3 的孩子。
        *   列表不包含 1，因此忽略 1。
        *   包含 5 的索引是 0 和 4。所以他们变成了孩子。

```
        -1 ---------- root of the forest
       /
      2    ---------- level (0) 
     /
    3       ---------- level (1)
   / \
  1   5     ---------- level (2)
 /     \
0       4       ---------- level (3)

Note: level (0) contains roots of each tree
```

*   **例 2:**
    *   在这种情况下，树的格式为

```
     -1        -------- root of the forest
  / | | | \
 0  1 2 3  4   -------- level (0)
    |
    5          -------- level (1)
Note: level (0) contains roots of each tree
```

**先决条件:** [等级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。
**方法:**想法是递归地在树中插入节点。然而，树的结构大不相同，通常在二叉树的情况下，任何节点最多有两个子节点，但在这种情况下，根节点可以有 **N** 个子节点。-1’被认为是根，根的索引将被认为是子节点。

**示例:**
如果索引 3 中存在-1，则 3 将是-1 的子节点。

```
     -1
    / 
   3
```

将-1 插入队列。现在，如果根为空，则-1 节点成为根。现在将-1 的子节点出列并排队。创建节点并将其附加到根目录。继续这一过程，直到插入所有子节点。

```
Level order Traversal:
     -1
   3   5
 2 4 6   9
The output for level order traversal will be: -1 3 5 2 4 6 9
```

按照级别顺序遍历时，遵循相同的入队和出队方法。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node creation
class Node
{
    public:
        int val;

        // Since n children are possible for a root.
        // A list created to store all the children.
        vector<Node *> child;

        // Constructor
        Node(int data) : val(data) {}
};

// Function to insert
void insert(Node *root, int parent, Node *node)
{

    // Root is empty then the node wil
    // l become the root
    if (!root)
    {
        root = node;
    }
    else
    {
        if (root->val == parent)
        {
        root->child.push_back(node);
        }
        else
        {
            // Recursive approach to
            // insert the child
            int l = root->child.size();

            for(int i = 0; i < l; i++)
            {
                if (root->child[i]->val == parent)
                    insert(root->child[i], parent, node);
                else
                    insert(root->child[i], parent, node);
            }
        }
    }
}

// Function to perform level order traversal
void levelorder(vector<Node *> &prev_level)
{
    vector<Node *> cur_level;
    vector<int> print_data;
    int l = prev_level.size();

    if (l == 0)
    {
        exit(0);
    }

    for(int i = 0; i < l; i++)
    {
        int prev_level_len = prev_level[i]->child.size();

        for(int j = 0; j < prev_level_len; j++)
        {

            // enqueue all the children
            // into cur_level list
            cur_level.push_back(prev_level[i]->child[j]);

            // Copies the entire cur_level
            // list into prev_level
            print_data.push_back(prev_level[i]->child[j]->val);
        }
    }

    prev_level = cur_level;
    for(auto i : print_data)
    {
        cout << i << " ";
    }
    levelorder(prev_level);
}

// Function that calls levelorder method to
// perform level order traversal
void levelorder_root(Node *root)
{
    if (root)
    {
        vector<Node *> level;
        level.push_back(root);
        printf("%d\n", root->val);
        levelorder(level);
    }
}

// Driver code
int main(int argc, char const *argv[])
{

    // -1 is the root element
    int arr[] = {-1, -1, -1, -1, -1};
    Node *root = new Node(-1);
    int l = sizeof(arr) / sizeof(int);
    vector<int> que;

    // Inserting root element to the queue
    que.push_back(-1);

    while (true)
    {
        vector<int> temp;
        for(int i = 0; i < l; i++)
        {
            if (find(que.begin(),
                     que.end(), arr[i]) != que.end())
            {
                // Insert elements into the tree
                insert(root, arr[i], new Node(i));
                temp.push_back(i);
            }
        }

        // Append child nodes into the queue
        // and insert the child
        que = temp;

        if (que.size() == 0)
        {
            break;
        }
    }
    levelorder_root(root);
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Node creation
class Node:

    # Constructor
    def __init__(self, data): 

        self.val = data

        # Since n children are possible for a root.
        # A list created to store all the children.
        self.child = []  

# Function to insert
def insert(root, parent, node):

    # Root is empty then the node will become the root
    if root is None:
        root = node              

    else:
        if root.val == parent:
            root.child.append(node)            
        else:

            # Recursive approach to
            # insert the child
            l = len(root.child)

            for i in range(l):
                if root.child[i].val == parent:
                    insert(root.child[i], parent, node)
                else:
                    insert(root.child[i], parent, node)

# Function that calls levelorder method to
# perform level order traversal
def levelorder_root(root):
    if root:
        level = []
        level.append(root)
        print(root.val)
        levelorder(level)

# Function to perform level order traversal
def levelorder(prev_level):

    cur_level = []
    print_data = []
    l = len(prev_level)

    if l == 0:
        exit()

    for i in range(l):   
        prev_level_len = len(prev_level[i].child)

        for j in range(prev_level_len):

            # enqueue all the children
            # into cur_level list
            cur_level.append(
                   prev_level[i].child[j]) 

            # Copies the entire cur_level
            # list into prev_level
            print_data.append(
                   prev_level[i].child[j].val)

    prev_level = cur_level[:]                
    print(*print_data)
    levelorder(prev_level)

# Driver code

# -1 is the root element   
arr = [-1, -1, -1, -1, -1]
root = Node(-1)
l = len(arr)
que = []

# Inserting root element to the queue
que.append(-1)

while 1:
    temp = []
    for i in range(l):
        if arr[i] in que:

            # Insert elements into the tree
            insert(root, arr[i], Node(i))
            temp.append(i)

    # Append child nodes into the queue
    # and insert the child
    que = temp[:]                     

    if len(que)== 0:
        break

levelorder_root(root)   
```

**Output:**

```
-1
0 1 2 3 4
```

**时间复杂度:** O(N^2).
**辅助空间** : O(N)。
# 二叉树中从源节点到目的节点的分步最短路径

> 原文:[https://www . geeksforgeeks . org/逐步最短路径-从源节点到目标节点-二叉树中的节点/](https://www.geeksforgeeks.org/step-by-step-shortest-path-from-source-node-to-destination-node-in-a-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)的**根**和两个整数**起始值**和**设计值**分别表示起始和结束节点。任务是找到从开始节点到结束节点的最短路径，并以下面给出的方向形式打印路径。

1.  从一个**节点到它的左子** **节点**用字母**‘L’**表示。
2.  从一个**节点到其右子节点**由字母**‘R’**表示。
3.  要从**节点导航到其父节点**，请使用字母**‘U’**。

**示例:**

> **输入：** 根 = [5， 1， 2， 3， 零， 6， 4]， 起始值 = 3， destValue = 6
> 
> 5
> /\
> 1 2
> /\
> 3 6 4
> 
> **输出:**【UURL】
> **说明:**最短路径为:3 → 1 → 5 → 2 → 6。
> 
> **输入:**根=【2，1】，起始值= 2，结束值= 1
> 
> 2
> /
> 1
> 
> **输出:**【L】
> **说明:**最短路径为:2 → 1。

**方法:**解决这个问题最简单的方法是使用二叉树的 [LCA(最低共同祖先)。按照以下步骤解决给定的问题。](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/)

*   应用 **LCA** 获得新根。
*   获取从新根到**起点**和**终点**的路径。
*   连接开始路径和结束路径，并确保用**‘U’**替换开始路径的字符。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <iostream>
using namespace std;

// Structure of Tree
class TreeNode {
public:
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val2)
    {
        val = val2;
        left = NULL;
        right = NULL;
    }
};

// Function to find LCA of two nodes
TreeNode* lca(TreeNode* root,
              int startValue,
              int destValue)
{

    // Base Case
    if (!root)
        return NULL;

    if (root->val == startValue)
        return root;
    if (root->val == destValue)
        return root;
    auto l = lca(root->left,
                 startValue, destValue);
    auto r = lca(root->right,
                 startValue, destValue);

    if (l && r)
        return root;

    return l ? l : r;
}
bool getPath(TreeNode* root,
             int value,
             string& path)
{

    // Base Cases
    if (!root)
        return false;
    if (root->val == value)
        return true;

    path += 'L';
    auto res = getPath(root->left,
                       value, path);
    if (res)
        return true;
    path.pop_back();
    path += 'R';
    res = getPath(root->right,
                  value, path);
    if (res)
        return true;
    path.pop_back();
    return false;
}

// Function to get directions
string getDirections(TreeNode* root,
                     int startValue,
                     int destValue)
{
    // Find the LCA first
    root = lca(root, startValue, destValue);

    string p1, p2;

    // Get the path
    getPath(root, startValue, p1);
    getPath(root, destValue, p2);
    for (auto& c : p1)
        c = 'U';

    // Return the concatenation
    return p1 + p2;
}

// Driver Code
int main()
{

    /*
             5
           /    \
         1       2
        /       /  \
      3        6    4

   */
    TreeNode* root = new TreeNode(5);
    root->left = new TreeNode(1);
    root->right = new TreeNode(2);
    root->left->left = new TreeNode(3);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(4);

    int startValue = 3;
    int endValue = 6;

    // Function Call
    string ans = getDirections(
      root, startValue, endValue);

    // Print answer
    cout << ans;
}
```

## 蟒蛇 3

```
# Python program for above approach

# Structure of Tree
class TreeNode :
    def __init__(self, val2):
        self.val = val2;
        self.left = None;
        self.right = None;

# Function to find LCA of two nodes
def lca(root, startValue, destValue):

    # Base Case
    if (not root):
        return None;

    if (root.val == startValue):
        return root;
    if (root.val == destValue):
        return root;
    l = lca(root.left,
        startValue, destValue);
    r = lca(root.right,
        startValue, destValue);

    if (l and r):
        return root;

    return l if l else r;

def getPath(root, value, path) :

    # Base Cases
    if (not root):
        return False;
    if (root.val == value):
        return True;

    path.append('L');
    res = getPath(root.left, value, path);
    if (res):
        return True;

    path.pop();
    path.append('R');
    res = getPath(root.right, value, path);

    if (res):
        return True;

    path.pop();
    return False;

# Function to get directions
def getDirections(root, startValue, destValue) :

    # Find the LCA first
    root = lca(root, startValue, destValue);

    p1 = []
    p2 = []

    # Get the path
    getPath(root, startValue, p1);
    getPath(root, destValue, p2);
    for i in range(len(p1)):
        p1[i] = 'U';

    # Return the concatenation
    s = ""
    for i in range(len(p1)):
        s += p1[i];
    for i in range(len(p2)):
        s += p2[i];
    return s;

# Driver Code
"""
         5
       /    \
     1       2
    /       /  \
  3        6    4
"""

root = TreeNode(5);
root.left = TreeNode(1);
root.right = TreeNode(2);
root.left.left = TreeNode(3);
root.right.left = TreeNode(6);
root.right.right = TreeNode(4);

startValue = 3;
endValue = 6;

# Function Call
ans = getDirections(root, startValue,
                        endValue);

# Print answer
print(ans)

# self code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Structure of Tree
class TreeNode
{
    constructor(val2)
    {
        this.val = val2;
        this.left = null;
        this.right = null;
    }
};

// Function to find LCA of two nodes
function lca(root, startValue, destValue)
{

    // Base Case
    if (!root)
        return null;

    if (root.val == startValue)
        return root;
    if (root.val == destValue)
        return root;
    let l = lca(root.left,
        startValue, destValue);
    let r = lca(root.right,
        startValue, destValue);

    if (l && r)
        return root;

    return l ? l : r;
}

function getPath(root, value, path)
{

    // Base Cases
    if (!root)
        return false;
    if (root.val == value)
        return true;

    path.push('L');
    let res = getPath(root.left,
                      value, path);
    if (res)
        return true;

    path.pop();
    path.push('R');
    res = getPath(root.right,
                  value, path);

    if (res)
        return true;

    path.pop();
    return false;
}

// Function to get directions
function getDirections(root, startValue,
                       destValue)
{

    // Find the LCA first
    root = lca(root, startValue, destValue);

    let p1 = [], p2 = [];

    // Get the path
    getPath(root, startValue, p1);
    getPath(root, destValue, p2);
    for(let i = 0; i < p1.length; i++)
        p1[i] = 'U';

    // Return the concatenation
    let s = ""
    for(let i = 0; i < p1.length; i++)
    {
        s += p1[i];
    }
    for(let i = 0; i < p2.length; i++)
    {
        s += p2[i];
    }
    return s;
}

// Driver Code
/*
         5
       /    \
     1       2
    /       /  \
  3        6    4

*/
let root = new TreeNode(5);
root.left = new TreeNode(1);
root.right = new TreeNode(2);
root.left.left = new TreeNode(3);
root.right.left = new TreeNode(6);
root.right.right = new TreeNode(4);

let startValue = 3;
let endValue = 6;

// Function Call
let ans = getDirections(root, startValue,
                        endValue);

// Print answer
document.write(ans)

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
UURL
```

**时间复杂度:** O(3N)，因为做了三次遍历。
**辅助空间:** O(1)

**高效方法:**这种方法是基于实现的，但是**生命周期评价**不用于这种方法。按照以下步骤解决给定的问题。

*   从根开始为起点和终点建立方向。
*   假设我们得到**【LLRRL】****【LRR】**。
*   删除公共前缀路径。
*   我们去掉**“L”**，现在出发方向是**“LRRL”**，目的地–**“RR”**
*   将开始方向的所有步骤替换为**“U”**，并添加目的方向。
*   结果是**“uu”+“RR”**。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of Tree
class TreeNode {
public:
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val2)
    {
        val = val2;
        left = NULL;
        right = NULL;
    }
};

// Find Function
bool find(TreeNode* n, int val,
          string& path)
{
    if (n->val == val)
        return true;
    if (n->left && find(n->left,
                        val, path)) {
        path.push_back('L');
        return true;
    }
    if (n->right && find(n->right,
                         val, path)) {
        path.push_back('R');
        return true;
    }
    return false;
}

// Function to keep track
// of directions at any point
string getDirections(TreeNode* root,
                     int startValue,
                     int destValue)
{

    // To store the startPath and destPath
    string s_p, d_p;
    find(root, startValue, s_p);
    find(root, destValue, d_p);

    while (!s_p.empty() && !d_p.empty()
           && s_p.back() == d_p.back()) {
        s_p.pop_back();
        d_p.pop_back();
    }

    for (int i = 0; i < s_p.size(); i++) {
        s_p[i] = 'U';
    }
    reverse(d_p.begin(), d_p.end());
    string ans = s_p + d_p;
    return ans;
}

// Driver Code
int main()
{

    /*
             5
           /    \
         1       2
        /       /  \
      3        6    4

   */

    TreeNode* root = new TreeNode(5);
    root->left = new TreeNode(1);
    root->right = new TreeNode(2);
    root->left->left = new TreeNode(3);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(4);

    int startValue = 3;
    int endValue = 6;

    // Function Call
    string ans = getDirections(
      root, startValue, endValue);

    // Print the result
    cout << ans;
}
```

**Output**

```
UURL
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)，If 递归栈空间如果忽略。
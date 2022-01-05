# 给定二叉树的最频繁子树和

> 原文:[https://www . geesforgeks . org/最频繁子树-给定二叉树的和/](https://www.geeksforgeeks.org/most-frequent-subtree-sum-from-a-given-binary-tree/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是通过将给定树的每个节点视为子树的根，找到可以获得的最频繁子树和。如果存在多个这样的总和，则打印所有这些总和。

**示例:**

> **输入:**
> 5
> / \
> 2 -4
> 
> **输出:** 2 -4 3
> **说明:**
> 考虑 5 为子树根的节点之和为 5+2–4 = 3。
> 考虑 2 为子树根的节点之和为 2 = 2。
> 考虑-4 作为子树根的节点之和为-4 = -4。
> 由于所有和的频率相同，打印所有和。
> 
> **输入:**
> 4
> / \
> 2 -4
> 
> **输出:** 2
> **说明:**
> 考虑 4 为子树根的节点之和为 4+2–4 = 2。
> 考虑 2 为子树根的节点之和为 2 = 2。
> 考虑-4 作为子树根的节点之和为-4 = -4。
> 因为，和 2 具有最大频率(= 2)。因此，打印值 2。

**方法:**对给定的树使用 [DFS 遍历](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)的思想来解决给定的问题。按照以下步骤解决问题:

*   创建两个辅助[哈希图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **M** 和 **F** 其中 **M** 是一组整数键和对应的列表， **F** 会存储每个数字的频率。
*   对给定的树执行 DFS 遍历，并执行以下操作:
    *   如果节点为**空**，则返回 **0** 。
    *   初始化变量**左**和**右**，存储当前节点左右子树节点之和的值。
    *   求**current node . value+left+right**的和，存储在变量 **totalSum** 中。
    *   现在更新地图 **F** 中 **totalSum** 的频率。
    *   将地图 **M** 中 **F【总计】**值更新为**总计**的频率。
    *   将当前递归函数的值返回到 **totalSum** 。
*   完成上述步骤后，打印列表 **M.rbegin()** 的所有元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the vector
void printVector(vector<int> v)
{
    // Traverse vector c
    for (int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }
}

// TreeNode class
class TreeNode {
public:
    int val;
    TreeNode *left, *right;

    // Constructor
    TreeNode(int data)
    {
        val = data;
        left = NULL;
        right = NULL;
    }
};

// Function to insert node in the
// binary tree
void insert(TreeNode** root, int val)
{
    // Initialize Queue
    queue<TreeNode*> q;

    // Push the node root
    q.push(*root);

    // While Q.size() is there
    while (q.size()) {

        // Get the front node
        TreeNode* temp = q.front();
        q.pop();

        // If left is NULL
        if (!temp->left) {
            if (val)
                temp->left = new TreeNode(val);
            else
                temp->left = new TreeNode(0);
            return;
        }
        else {
            q.push(temp->left);
        }

        // If right is NULL
        if (!temp->right) {
            if (val)
                temp->right = new TreeNode(val);
            else
                temp->right = new TreeNode(0);
            return;
        }
        else {
            q.push(temp->right);
        }
    }
}

// Function to make the tree from
// given node values
TreeNode* buildTree(vector<int> v)
{
    TreeNode* root = new TreeNode(v[0]);

    // Traverse and insert node
    for (int i = 1; i < v.size(); i++) {
        insert(&root, v[i]);
    }
    return root;
}

// Utility function to find subtree
// sum with highest frequency of a
// particular node
int findsubTreeSumUtil(
    TreeNode* node, map<int,
                        vector<int> >& mpp,
    map<int, int>& frequency)
{
    if (!node)
        return 0;

    // Recur for the left subtree
    int left = findsubTreeSumUtil(
        node->left, mpp, frequency);

    // Recur for the right subtree
    int right = findsubTreeSumUtil(
        node->right, mpp, frequency);

    // Stores sum of nodes of a subtree
    int totalSum = node->val + left + right;

    // Update the frequency
    if (!frequency.count(totalSum)) {
        mpp[1].push_back(totalSum);
        frequency[totalSum] = 1;
    }
    else {
        frequency[totalSum]++;
        mpp[frequency[totalSum]].push_back(totalSum);
    }

    // Return the total sum
    return totalSum;
}

// Function to find subtree sum with
// highest frequency of given tree
void findsubTreeSum(TreeNode* root)
{
    // Store list of nodes attached to
    // a particular node and frequency
    // of visited nodes
    map<int, vector<int> > mpp;
    map<int, int> frequency;

    // Base Case
    if (!root) {
        printVector({});
        return;
    }

    // DFS function call
    findsubTreeSumUtil(root, mpp, frequency);

    // Print the vector
    printVector(mpp.rbegin()->second);
}

// Driver Code
int main()
{
    // Given nodes of the tree
    vector<int> v = { 5, 2, -4 };

    // Function call to build the tree
    TreeNode* tree = buildTree(v);

    // Function Call
    findsubTreeSum(tree);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

// Importing required classes
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.LinkedList;
import java.util.Queue;
import java.util.TreeMap;

public class GFG {
    // Function to print the list
    static void printVector(ArrayList<Integer> v)
    {
        // Traverse list
        for (int i = 0; i < v.size(); i++) {
            System.out.print(v.get(i) + " ");
        }
    }

    // TreeNode class
    static class TreeNode {
        int val;
        TreeNode left, right;

        // Constructor
        TreeNode(int data)
        {
            val = data;
            left = null;
            right = null;
        }
    }

    // Function to insert node in the
    // binary tree
    static void insert(TreeNode root, int val)
    {
        // Initialize Queue
        Queue<TreeNode> q = new LinkedList<TreeNode>();

        // Push the node root
        q.add(root);

        // While queue is not empty
        while (q.isEmpty() == false) {

            // Get the front node
            TreeNode temp = q.peek();
            q.poll();

            // If left is NULL
            if (temp.left == null) {
                temp.left = new TreeNode(val);
                return;
            }
            else {
                q.add(temp.left);
            }

            // If right is NULL
            if (temp.right == null) {
                temp.right = new TreeNode(val);
                return;
            }
            else {
                q.add(temp.right);
            }
        }
    }

    // Function to make the tree from
    // given node values
    static TreeNode buildTree(ArrayList<Integer> v)
    {
        TreeNode root = new TreeNode(v.get(0));

        // Traverse and insert node
        for (int i = 1; i < v.size(); i++) {
            insert(root, v.get(i));
        }
        return root;
    }

    // Utility function to find subtree
    // sum with highest frequency of a
    // particular node
    static int findsubTreeSumUtil(
        TreeNode node,
        TreeMap<Integer, ArrayList<Integer> > mpp,
        HashMap<Integer, Integer> frequency)
    {
        if (node == null)
            return 0;

        // Recur for the left subtree
        int left
            = findsubTreeSumUtil(node.left, mpp, frequency);

        // Recur for the right subtree
        int right = findsubTreeSumUtil(node.right, mpp,
                                       frequency);

        // Stores sum of nodes of a subtree
        int totalSum = node.val + left + right;

        // Update the frequency
        // If there is no node with sub-tree sum equal to
        // totalSum It is the first occurrence of totalSum
        // value
        if (frequency.get(totalSum) == null) {
            ArrayList<Integer> temp = mpp.get(1);
            // If there is no sum which has occurred only
            // once
            if (temp == null)
                temp = new ArrayList<Integer>();
            temp.add(totalSum);
            mpp.put(1, temp);
            frequency.put(totalSum, 1);
        }
        // There is a node with sub-tree sum equal to
        // totalSum
        else {
            frequency.put(totalSum,
                          frequency.get(totalSum) + 1);
            // Get list of sum values which has
            // occurrence equal to occurrence of totalSum
            ArrayList<Integer> temp
                = mpp.get(frequency.get(totalSum));
            // If there is no sum which has occurrence
            // equal to occurrence of totalSum
            if (temp == null)
                temp = new ArrayList<Integer>();
            temp.add(totalSum);
            mpp.put(frequency.get(totalSum), temp);
        }

        // Return the total sum
        return totalSum;
    }

    // Function to find subtree sum with
    // highest frequency of given tree
    static void findsubTreeSum(TreeNode root)
    {
        // Store list of nodes attached to
        // a particular node and frequency
        // of visited nodes
        TreeMap<Integer, ArrayList<Integer> > mpp
            = new TreeMap<Integer, ArrayList<Integer> >();
        HashMap<Integer, Integer> frequency
            = new HashMap<Integer, Integer>();

        // Base Case
        if (root == null) {
            return;
        }

        // DFS function call
        findsubTreeSumUtil(root, mpp, frequency);

        // Print the list of most-frequent subtree sum
        printVector(mpp.lastEntry().getValue());
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given nodes of the tree
        ArrayList<Integer> v = new ArrayList<Integer>();
        v.addAll(Arrays.asList(5, 2, -4));

        // Function call to build the tree
        TreeNode tree = buildTree(v);

        // Function Call
        findsubTreeSum(tree);
    }
}

// This code is contributed by jainlovely450
```

**Output:** 

```
2 -4 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
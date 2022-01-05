# 从目标节点开始烧二叉树

> 原文:[https://www . geesforgeks . org/burn-the-二叉树-从目标节点开始/](https://www.geeksforgeeks.org/burn-the-binary-tree-starting-from-the-target-node/)

给定二叉树和目标节点。通过将火给予目标节点，火开始在一棵完整的树上蔓延。任务是打印二叉树燃烧节点的序列。
**燃烧节点的规则:**

*   火只会不断蔓延到相连的节点。
*   每个节点燃烧的时间相同。
*   一个节点只能燃烧一次。

**示例:**

```
Input : 
                       12
                     /     \
                   13       10
                          /     \
                       14       15
                      /   \     /  \
                     21   24   22   23
target node = 14

Output :
14
21, 24, 10
15, 12
22, 23, 13

Explanation : First node 14 burns then it gives fire to it's 
neighbors(21, 24, 10) and so on. This process continues until 
the whole tree burns.

Input :
                       12
                     /     \
                  19        82
                 /        /     \
               41       15       95
                 \     /         /  \
                  2   21        7   16
target node = 41

Output :
41
2, 19
12
82
15, 95
21, 7, 16
```

**方法:**
首先在二叉树[中递归搜索目标节点](https://www.geeksforgeeks.org/recursion/)。找到目标节点后，打印它并将它的左子节点(如果存在)和右子节点(如果存在)保存在队列中。然后回来。现在，获取队列的大小并在循环时运行。打印队列中的元素。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to print the sequence
// of burning of nodes of a binary tree
#include <bits/stdc++.h>
using namespace std;

// A Tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Utility function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Utility function to print the sequence of burning nodes
int burnTreeUtil(Node* root, int target, queue<Node*>& q)
{
    // Base condition
    if (root == NULL) {
        return 0;
    }

    // Condition to check whether target
    // node is found or not in a tree
    if (root->key == target) {
        cout << root->key << endl;
        if (root->left != NULL) {
            q.push(root->left);
        }
        if (root->right != NULL) {

            q.push(root->right);
        }

        // Return statements to prevent
        // further function calls
        return 1;
    }

    int a = burnTreeUtil(root->left, target, q);

    if (a == 1) {
        int qsize = q.size();

        // Run while loop until size of queue
        // becomes zero
        while (qsize--) {
            Node* temp = q.front();

            // Printing of burning nodes
            cout << temp->key << " , ";
            q.pop();

            // Check if condition for left subtree
            if (temp->left != NULL)
                q.push(temp->left);

            // Check if condition for right subtree
            if (temp->right != NULL)
                q.push(temp->right);
        }

        if (root->right != NULL)
            q.push(root->right);

        cout << root->key << endl;

        // Return statement it prevents further
        // further function call
        return 1;
    }

    int b = burnTreeUtil(root->right, target, q);

    if (b == 1) {
        int qsize = q.size();
        // Run while loop until size of queue
        // becomes zero

        while (qsize--) {
            Node* temp = q.front();

            // Printing of burning nodes
            cout << temp->key << " , ";
            q.pop();

            // Check if condition for left subtree
            if (temp->left != NULL)
                q.push(temp->left);

            // Check if condition for left subtree
            if (temp->right != NULL)
                q.push(temp->right);
        }

        if (root->left != NULL)
            q.push(root->left);

        cout << root->key << endl;

        // Return statement it prevents further
        // further function call
        return 1;
    }
}

// Function will print the sequence of burning nodes
void burnTree(Node* root, int target)
{
    queue<Node*> q;

    // Function call
    burnTreeUtil(root, target, q);

    // While loop runs unless queue becomes empty
    while (!q.empty()) {
        int qSize = q.size();
        while (qSize > 0) {
            Node* temp = q.front();

            // Printing of burning nodes
            cout << temp->key;
            // Insert left child in a queue, if exist
            if (temp->left != NULL) {
                q.push(temp->left);
            }
            // Insert right child in a queue, if exist
            if (temp->right != NULL) {
                q.push(temp->right);
            }

            if (q.size() != 1)
                cout << " , ";

            q.pop();
            qSize--;
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    /*      10
           /  \
          12  13
              / \
             14 15
            / \ / \
          21 22 23 24

        Let us create Binary Tree as shown
        above */

    Node* root = newNode(10);
    root->left = newNode(12);
    root->right = newNode(13);

    root->right->left = newNode(14);
    root->right->right = newNode(15);

    root->right->left->left = newNode(21);
    root->right->left->right = newNode(22);
    root->right->right->left = newNode(23);
    root->right->right->right = newNode(24);
    int targetNode = 14;

    // Function call
    burnTree(root, targetNode);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.HashMap;
import java.util.HashSet;
import java.util.Map;
import java.util.Set;

// Tree node class

class TreeNode
{
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode() {}
    TreeNode(int val) { this.val = val; }
    TreeNode(int val, TreeNode left, TreeNode right)
    {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}

class Solution {

    // function to print the sequence of burning nodes
    public static int search(TreeNode root,
                              int num,
                              Map<Integer,
                             Set<Integer> > levelOrderMap)
    {
        if (root != null)
        {
            // Condition to check whether target
            // node is found or not in a tree
            if (root.val == num)
            {

                levelOrderStoredInMap(root.left, 1,
                                      levelOrderMap);
                levelOrderStoredInMap(root.right, 1,
                                      levelOrderMap);
                // Return statements to prevent
                // further function calls
                return 1;
            }
            int k = search(root.left, num, levelOrderMap);
            if (k > 0)
            {
                // store root in map with k
                storeRootAtK(root, k, levelOrderMap);
                // store level order for other branch
                levelOrderStoredInMap(root.right, k + 1,
                                      levelOrderMap);
                return k + 1;
            }
            k = search(root.right, num, levelOrderMap);
            if (k > 0)
            {
                // store root in map with k
                storeRootAtK(root, k, levelOrderMap);
                // store level order for other branch
                levelOrderStoredInMap(root.left, k + 1,
                                      levelOrderMap);
                return k + 1;
            }
        }
        return -1; // Base condition
    }

    public static void levelOrderStoredInMap(
        TreeNode root, int k,
        Map<Integer, Set<Integer> > levelOrderMap)
    {
        if (root != null) {
            storeRootAtK(root, k, levelOrderMap);
            levelOrderStoredInMap(root.left, k + 1,
                                  levelOrderMap);
            levelOrderStoredInMap(root.right, k + 1,
                                  levelOrderMap);
        }
    }

    private static void
    storeRootAtK(TreeNode root, int k,
                 Map<Integer, Set<Integer> > levelOrderMap)
    {
        if (levelOrderMap.containsKey(k)) {
            levelOrderMap.get(k).add(root.val);
        }
        else {
            Set<Integer> set = new HashSet<>();
            set.add(root.val);
            levelOrderMap.put(k, set);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        /*  12
           /  \
          13  10
              / \
             14 15
            / \ / \
          21 24 22 23

        Let us create Binary Tree as shown
        above */
        TreeNode root = new TreeNode(12);
        root.left = new TreeNode(13);
        root.right = new TreeNode(10);
        root.right.left = new TreeNode(14);
        root.right.right = new TreeNode(15);
        TreeNode left = root.right.left;
        TreeNode right = root.right.right;
        left.left = new TreeNode(21);
        left.right = new TreeNode(24);
        right.left = new TreeNode(22);
        right.right = new TreeNode(23);

        // Utility map to store the sequence of burning
        // nodes
        Map<Integer, Set<Integer> > levelOrderMap
            = new HashMap<>();

        // search node and store the level order from that
        // node in map
        search(root, 14, levelOrderMap);

        // will print the sequence of burning nodes
        System.out.println(14);
        for (Integer level : levelOrderMap.keySet())
        {
            for (Integer val : levelOrderMap.get(level))
            {
                System.out.print(val + " ");
            }
            System.out.println();
        }
    }

}
// This code is contributed by Niharika Sahai
```

**Output**

```
14
21 , 22 , 13
15 , 10
23 , 24 , 12

```

输出:

```
14
21 24 10 
12 15 
22 23 13 
```

另一种方法:将树转换成无向图，并打印其层次顺序遍历

*   使用树节点作为顶点，父子关系作为边来构建无向图
*   以源顶点为目标做 BFS。

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;

public class GFG {

    /*package whatever //do not write package name here */

    static class TreeNode
    {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode() {}
        TreeNode(int val) { this.val = val; }
        TreeNode(int val, TreeNode left, TreeNode right)
        {
            this.val = val;
            this.left = left;
            this.right = right;
        }
    }

    static  Map<TreeNode, List<TreeNode>> map = new HashMap<>();
        public static void main (String[] args) {
            TreeNode root = new TreeNode(12);
            root.left = new TreeNode(13);
            root.right = new TreeNode(10);
            root.right.left = new TreeNode(14);
            root.right.right = new TreeNode(15);
            TreeNode left = root.right.left;
            TreeNode right = root.right.right;
            left.left = new TreeNode(21);
            left.right = new TreeNode(24);
            right.left = new TreeNode(22);
            right.right = new TreeNode(23);
            // target Node value is 14
            burnTree(root,left);
          System.out.println();
        }
      private static void burnTree(TreeNode root, TreeNode target) {
             List<Integer> res = new ArrayList<Integer> ();
            if (root == null )
              return ;
            buildMap(root, null);
            if (!map.containsKey(target))
            { System.out.println("Target Not found");
              return;
            }
            Set<TreeNode> visited = new HashSet<TreeNode>();
        //BFS traversal
            Queue<TreeNode> q = new LinkedList<TreeNode>();
            q.add(target);
            visited.add(target);
            while (!q.isEmpty()) {
                int size = q.size();

                for (int i = 0; i < size; i++) {
                    TreeNode node = q.poll();
                    System.out.print(node.val+" ");
                    for (TreeNode next : map.get(node)) {
                        if (visited.contains(next))
                          continue;
                        visited.add(next);
                        q.add(next);
                    }
                }
                System.out.println();

            }

    }
        // build undirected graph
      private  static void buildMap(TreeNode node, TreeNode parent) {
            if (node == null)
                return;
            if (!map.containsKey(node)) {

                map.put(node, new ArrayList<TreeNode>());
                if (parent != null)  { map.get(node).add(parent); map.get(parent).add(node) ; }
                buildMap(node.left, node);
                buildMap(node.right, node);
            }
        }   

}
```

**Output**

```
14 
10 21 24 
12 15 
13 22 23 

```

输出:

```
14 
10 21 24 
12 15 
13 22 23  
```
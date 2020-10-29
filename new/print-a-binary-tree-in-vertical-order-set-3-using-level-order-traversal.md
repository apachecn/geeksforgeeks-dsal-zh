# 以垂直顺序打印二叉树| 设置 3（使用级别顺序遍历）

> 原文：[https://www.geeksforgeeks.org/print-a-binary-tree-in-vertical-order-set-3-using-level-order-traversal/](https://www.geeksforgeeks.org/print-a-binary-tree-in-vertical-order-set-3-using-level-order-traversal/)

给定一棵二叉树，垂直打印。 以下示例说明了垂直顺序遍历。

```

           1
         /   \
       2       3
     /  \     /  \
   4     5   6    7
              \    \
               8    9            

The output of print this tree vertically will be:
4
2
1 5 6
3 8
7
9

```

![](img/ca21579b27f438afb3d26b70fe0bf6c1.png)

我们在下面的文章中讨论了一种有效的方法。

[以垂直顺序打印二叉树| 设置 2（基于哈希图的方法）](https://www.geeksforgeeks.org/print-binary-tree-vertical-order-set-2/)

上述解决方案使用预遍历和 Hashmap 来根据水平距离存储节点。 由于上述方法使用了预先遍历，因此垂直线中的节点可能无法按照它们在树中出现的顺序进行排序。 例如，上述解决方案在下面的树中的 9 之前打印 12。 请参阅[和](https://ide.geeksforgeeks.org/TPyOLR)以获取示例运行。

```
             1
          /     \
         2       3
        /  \    /  \
       4    5  6    7
                \  /  \
                 8 10  9 
                     \
                     11
                       \
                        12      
```

如果我们使用[级别顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)，则可以确保如果像 12 这样的节点在同一垂直线上位于下面，则将其打印在像 9 这样的节点在垂直线上位于上方。

```
1\. To maintain a hash for the branch of each node.
2\. Traverse the tree in level order fashion.
3\. In level order traversal, maintain a queue
   which holds, node and its vertical branch.
    * pop from queue.
    * add this node's data in vector corresponding
      to its branch in the hash.
    * if this node hash left child, insert in the 
      queue, left with branch - 1.
    * if this node hash right child, insert in the 
      queue, right with branch + 1.

```

## C++

```cpp

// C++ program for printing vertical order 
// of a given binary tree usin BFS. 
#include <bits/stdc++.h> 

using namespace std; 

// Structure for a binary tree node 
struct Node { 
    int key; 
    Node *left, *right; 
}; 

// A utility function to create a new node 
Node* newNode(int key) 
{ 
    Node* node = new Node; 
    node->key = key; 
    node->left = node->right = NULL; 
    return node; 
} 

// The main function to print vertical oder of a 
// binary tree with given root 
void printVerticalOrder(Node* root) 
{ 
    // Base case 
    if (!root) 
        return; 

    // Create a map and store vertical oder in 
    // map using function getVerticalOrder() 
    map<int, vector<int> > m; 
    int hd = 0; 

    // Create queue to do level order traversal. 
    // Every item of queue contains node and 
    // horizontal distance. 
    queue<pair<Node*, int> > que; 
    que.push(make_pair(root, hd)); 

    while (!que.empty()) { 
        // pop from queue front 
        pair<Node*, int> temp = que.front(); 
        que.pop(); 
        hd = temp.second; 
        Node* node = temp.first; 

        // insert this node's data in vector of hash 
        m[hd].push_back(node->key); 

        if (node->left != NULL) 
            que.push(make_pair(node->left, hd - 1)); 
        if (node->right != NULL) 
            que.push(make_pair(node->right, hd + 1)); 
    } 

    // Traverse the map and print nodes at 
    // every horigontal distance (hd) 
    map<int, vector<int> >::iterator it; 
    for (it = m.begin(); it != m.end(); it++) { 
        for (int i = 0; i < it->second.size(); ++i) 
            cout << it->second[i] << " "; 
        cout << endl; 
    } 
} 

// Driver program to test above functions 
int main() 
{ 
    Node* root = newNode(1); 
    root->left = newNode(2); 
    root->right = newNode(3); 
    root->left->left = newNode(4); 
    root->left->right = newNode(5); 
    root->right->left = newNode(6); 
    root->right->right = newNode(7); 
    root->right->left->right = newNode(8); 
    root->right->right->right = newNode(9); 
    root->right->right->left = newNode(10); 
    root->right->right->left->right = newNode(11); 
    root->right->right->left->right->right = newNode(12); 
    cout << "Vertical order traversal is \n"; 
    printVerticalOrder(root); 
    return 0; 
} 

```

## Python3

```py

# python3 Program to print zigzag traversal of binary tree 
import collections 
# Binary tree node 
class Node: 
    # Constructor to create a new node 
    def __init__(self, data): 
        self.data = data 
        self.left = self.right = None

# function to print vertical order traversal of binary tree 
def verticalTraverse(root): 

    # Base case 
    if root is None: 
        return

    # Create empty queue for level order traversal 
    queue = [] 

    # create a map to store nodes at a particular 
    # horizontal distance 
    m = {} 

    # map to store horizontal distance of nodes 
    hd_node = {} 

    # enqueue root 
    queue.append(root) 
    # store the horizontal distance of root as 0 
    hd_node[root] = 0

    m[0] = [root.data] 

    # loop will run while queue is not empty 
    while len(queue) > 0: 

        # dequeue node from queue 
        temp = queue.pop(0) 

        if temp.left: 
            # Enqueue left child 
            queue.append(temp.left) 

            # Store the horizontal distance of left node 
            # hd(left child) = hd(parent) -1 
            hd_node[temp.left] = hd_node[temp] - 1
            hd = hd_node[temp.left] 

            if m.get(hd) is None: 
                m[hd] = [] 

            m[hd].append(temp.left.data) 

        if temp.right: 
            # Enqueue right child 
            queue.append(temp.right) 

            # store the horizontal distance of right child 
            # hd(right child) = hd(parent) + 1 
            hd_node[temp.right] = hd_node[temp] + 1
            hd = hd_node[temp.right] 

            if m.get(hd) is None: 
                m[hd] = [] 

            m[hd].append(temp.right.data) 

    # Sort the map according to horizontal distance 
    sorted_m = collections.OrderedDict(sorted(m.items())) 

    # Traverse the sorted map and print nodes at each horizontal distance 
    for i in sorted_m.values(): 
        for j in i: 
            print(j, " ", end ="") 
        print() 

# Driver program to check above function 
""" 
Constructed binary tree is  
            1 
        / \ 
        2     3 
    / \ / \ 
    4     5 6     7 
            \ / \ 
            8 10 9 
                \ 
                11 
                    \  
                    12 

"""
root = Node(1) 
root.left = Node(2) 
root.right = Node(3) 
root.left.left = Node(4) 
root.left.right = Node(5) 
root.right.left = Node(6) 
root.right.right = Node(7) 
root.right.left.right = Node(8) 
root.right.right.left = Node(10) 
root.right.right.right = Node(9) 
root.right.right.left.right = Node(11) 
root.right.right.left.right.right = Node(12) 
print("Vertical order traversal is ") 
verticalTraverse(root) 

# This code is contributed by Shweta Singh 

```

## Java

```java

import java.util.ArrayList; 
import java.util.LinkedList; 
import java.util.Map; 
import java.util.Queue; 
import java.util.TreeMap; 

class Node { 
    int key; 
    Node left, right; 
    // A utility function to create a new node 
    Node newNode(int key) 
    { 
        Node node = new Node(); 
        node.key = key; 
        node.left = node.right = null; 
        return node; 
    } 
} 

class Qobj { 
    int hd; 
    Node node; 
    Qobj(int hd, Node node) 
    { 
        this.hd = hd; 
        this.node = node; 
    } 
} 

public class VerticalOrderTraversal { 

    // The main function to print vertical oder of a 
    // binary tree with given root 
    static void printVerticalOrder(Node root) 
    { 
        // Base case 
        if (root == null) 
            return; 

        // Create a map and store vertical oder in 
        // map using function getVerticalOrder() 
        TreeMap<Integer, ArrayList<Integer> > m = new TreeMap<>(); 
        int hd = 0; 

        // Create queue to do level order traversal. 
        // Every item of queue contains node and 
        // horizontal distance. 
        Queue<Qobj> que = new LinkedList<Qobj>(); 
        que.add(new Qobj(0, root)); 

        while (!que.isEmpty()) { 
            // pop from queue front 
            Qobj temp = que.poll(); 
            hd = temp.hd; 
            Node node = temp.node; 

            // insert this node's data in array of hash 
            if (m.containsKey(hd)) { 
                m.get(hd).add(node.key); 
            } 
            else { 
                ArrayList<Integer> al = new ArrayList<>(); 
                al.add(node.key); 
                m.put(hd, al); 
            } 
            if (node.left != null) 
                que.add(new Qobj(hd - 1, node.left)); 
            if (node.right != null) 
                que.add(new Qobj(hd + 1, node.right)); 
        } 

        // Traverse the map and print nodes at 
        // every horizontal distance (hd) 
        for (Map.Entry<Integer, ArrayList<Integer> > entry : m.entrySet()) { 
            ArrayList<Integer> al = entry.getValue(); 
            for (Integer i : al) 
                System.out.print(i + " "); 
            System.out.println(); 
        } 
    } 

    // Driver program to test above functions 
    public static void main(String ar[]) 
    { 
        Node n = new Node(); 
        Node root; 
        root = n.newNode(1); 
        root.left = n.newNode(2); 
        root.right = n.newNode(3); 
        root.left.left = n.newNode(4); 
        root.left.right = n.newNode(5); 
        root.right.left = n.newNode(6); 
        root.right.right = n.newNode(7); 
        root.right.left.right = n.newNode(8); 
        root.right.right.right = n.newNode(9); 
        root.right.right.left = n.newNode(10); 
        root.right.right.left.right = n.newNode(11); 
        root.right.right.left.right.right = n.newNode(12); 
        System.out.println("Vertical order traversal is "); 
        printVerticalOrder(root); 
    } 
} 

```

Output:

```
Vertical order traversal is 
4  
2  
1  5  6  
3  8  10  
7  11  
9  12

```

上述实现的时间复杂度为 O（n Log n）。 请注意，以上实现使用的映射是通过自平衡 BST 实现的。

我们可以使用 unordered_map 将时间复杂度降低到`O(n)`。 为了以期望的顺序打印节点，我们可以有 2 个变量，分别表示最小和最大水平距离。 我们可以简单地从最小到最大水平距离进行迭代，并从 Map 中获取相应的值。 就是`O(n)`

辅助空间：`O(n)`

本文由 [**Sahil Chhabra（akku）**](https://www.facebook.com/sahil.chhabra.965) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。


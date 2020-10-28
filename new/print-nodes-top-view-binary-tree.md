# 二叉树

顶视图中的打印节点

二叉树的顶视图是从顶部查看树时可见的节点集。 给定一棵二叉树，打印它的顶视图。 可以按任何顺序打印输出节点。

如果 x 是其水平距离的最高节点，则输出中将存在一个节点 x。 节点 x 的左子节点的水平距离等于 x 的水平距离减去 1，而右子节点的左孩子的水平距离等于 x 的水平距离加 1。

```
       1
    /     \
   2       3
  /  \    / \
 4    5  6   7
Top view of the above binary tree is
4 2 1 3 7

        1
      /   \
    2       3
      \   
        4  
          \
            5
             \
               6
Top view of the above binary tree is
2 1 3 6
```

这个想法是做类似于[垂直顺序遍历](https://www.geeksforgeeks.org/print-binary-tree-vertical-order-set-2/)的操作。 像[垂直顺序遍历](https://www.geeksforgeeks.org/print-binary-tree-vertical-order-set-2/)一样，我们需要将水平距离相同的节点放在一起。 我们进行水平顺序遍历，以便在其下方具有相同水平距离的任何其他节点之前访问水平节点上的最高节点。 散列用于检查是否看到给定水平距离的节点。

## C++

```cpp

// C++ program to print top 
// view of binary tree 

#include <bits/stdc++.h> 
using namespace std; 

// Structure of binary tree 
struct Node 
{ 
    Node * left; 
    Node* right; 
    int hd; 
    int data; 
}; 

// function to create a new node 
Node* newNode(int key) 
{ 
    Node* node=new Node(); 
    node->left = node->right = NULL; 
    node->data=key; 
    return node; 
} 

// function should print the topView of 
// the binary tree 
void topview(Node* root) 
{ 
    if(root==NULL) 
       return; 
     queue<Node*>q; 
     map<int,int> m;  
     int hd=0; 
     root->hd=hd; 

     // push node and horizontal distance to queue 
    q.push(root); 

    cout<< "The top view of the tree is : \n"; 

    while(q.size()) 
    { 
        hd=root->hd; 

        // count function returns 1 if the container  
        // contains an element whose key is equivalent  
        // to hd, or returns zero otherwise. 
        if(m.count(hd)==0)   
        m[hd]=root->data; 
        if(root->left) 
        { 
            root->left->hd=hd-1; 
            q.push(root->left); 
        } 
        if(root->right) 
        { 
            root->right->hd=hd+1; 
            q.push(root->right); 
        } 
        q.pop(); 
        root=q.front(); 

    } 

     for(auto i=m.begin();i!=m.end();i++) 
    { 
        cout<<i->second<<" "; 
    } 

} 

// Driver Program to test above functions 
int main() 
{ 
    /* Create following Binary Tree  
            1  
        / \  
        2 3  
        \  
            4  
            \  
            5  
            \  
                6*/
   Node* root = newNode(1); 
    root->left = newNode(2); 
    root->right = newNode(3); 
    root->left->right = newNode(4); 
    root->left->right->right = newNode(5); 
    root->left->right->right->right = newNode(6); 
    cout<<"Following are nodes in top view of Binary Tree\n";  
    topview(root); 
    return 0; 
} 
/* This code is contributed by Niteesh Kumar */

```

## Java

```java

// Java program to print top 
// view of binary tree 
import java.util.Queue; 
import java.util.TreeMap; 
import java.util.LinkedList; 
import java.util.Map; 
import java.util.Map.Entry; 

// class to create a node 
class Node { 
    int data; 
    Node left, right; 

    public Node(int data) { 
        this.data = data; 
        left = right = null; 
    } 
} 

// class of binary tree 
class BinaryTree { 
    Node root; 

    public BinaryTree() { 
        root = null; 
    } 

    // function should print the topView of 
    // the binary tree 
    private void TopView(Node root) { 
        class QueueObj { 
            Node node; 
            int hd; 

            QueueObj(Node node, int hd) { 
                this.node = node; 
                this.hd = hd; 
            } 
        } 
        Queue<QueueObj> q = new LinkedList<QueueObj>(); 
        Map<Integer, Node> topViewMap = new TreeMap<Integer, Node>(); 

        if (root == null) { 
            return; 
        } else { 
            q.add(new QueueObj(root, 0)); 
        } 

        System.out.println("The top view of the tree is : "); 

        // count function returns 1 if the container  
        // contains an element whose key is equivalent  
        // to hd, or returns zero otherwise. 
        while (!q.isEmpty()) { 
            QueueObj tmpNode = q.poll(); 
            if (!topViewMap.containsKey(tmpNode.hd)) { 
                topViewMap.put(tmpNode.hd, tmpNode.node); 
            } 

            if (tmpNode.node.left != null) { 
                q.add(new QueueObj(tmpNode.node.left, tmpNode.hd - 1)); 
            } 
            if (tmpNode.node.right != null) { 
                q.add(new QueueObj(tmpNode.node.right, tmpNode.hd + 1)); 
            } 

        } 
        for (Entry<Integer, Node> entry : topViewMap.entrySet()) { 
            System.out.print(entry.getValue().data); 
        } 
    } 

    // Driver Program to test above functions 
    public static void main(String[] args)  
    {  
        /* Create following Binary Tree  
            1  
        / \  
        2 3  
        \  
            4  
            \  
            5  
            \  
                6*/
        BinaryTree tree = new BinaryTree(); 
        tree.root = new Node(1); 
        tree.root.left = new Node(2); 
        tree.root.right = new Node(3); 
        tree.root.left.right = new Node(4); 
        tree.root.left.right.right = new Node(5); 
        tree.root.left.right.right.right = new Node(6); 
        System.out.println("Following are nodes in top view of Binary Tree");  
        tree.TopView(tree.root);  
    }  

} 

```

## Python3

```py

# Python3 program to print top  
# view of binary tree 

# Binary Tree Node  
""" utility that allocates a newNode  
with the given key """
class newNode:  

    # Construct to create a newNode  
    def __init__(self, key):  
        self.data = key 
        self.left = None
        self.right = None
        self.hd = 0

# function should print the topView  
# of the binary tree  
def topview(root) : 

    if(root == None) : 
        return
    q = [] 
    m = dict() 
    hd = 0
    root.hd = hd  

    # push node and horizontal 
    # distance to queue  
    q.append(root)  

    while(len(q)) : 
        root = q[0] 
        hd = root.hd  

        # count function returns 1 if the  
        # container contains an element  
        # whose key is equivalent to hd,  
        # or returns zero otherwise.  
        if hd not in m: 
            m[hd] = root.data  
        if(root.left) :          
            root.left.hd = hd - 1
            q.append(root.left)  

        if(root.right):          
            root.right.hd = hd + 1
            q.append(root.right)  

        q.pop(0) 
    for i in sorted (m): 
        print(m[i], end = "")  

# Driver Code  
if __name__ == '__main__': 

    """ Create following Binary Tree  
            1  
        / \  
        2 3  
        \  
            4  
            \  
            5  
            \  
                6*"""
    root = newNode(1)  
    root.left = newNode(2)  
    root.right = newNode(3)  
    root.left.right = newNode(4)  
    root.left.right.right = newNode(5)  
    root.left.right.right.right = newNode(6)  
    print("Following are nodes in top",  
          "view of Binary Tree")  
    topview(root) 

# This code is contributed by 
# Shubham Singh(SHUBHAMSINGH10) 

```

**Output:**

```
Following are nodes in top view of Binary Tree
2136
```

**另一种方法**：

这种方法不需要队列。 这里我们使用两个变量，一个用于当前节点到根的垂直距离，另一个用于当前节点到根的深度。 我们使用垂直距离进行索引。 如果具有相同垂直距离的一个节点再次出现，我们将检查新节点的深度相对于地图中具有相同垂直距离的当前节点是较低还是较高。 如果新节点的深度较小，则我们将其替换。

## C++

```cpp

#include<bits/stdc++.h> 
using namespace std; 

// Structure of binary tree 
struct Node{ 
    Node * left; 
    Node* right; 
    int data; 
}; 

// function to create a new node 
Node* newNode(int key){ 
    Node* node=new Node(); 
    node->left = node->right = NULL; 
    node->data=key; 
    return node; 
} 

// function to fill the map 
void fillMap(Node* root,int d,int l,map<int,pair<int,int>> &m){ 
    if(root==NULL) return; 

    if(m.count(d)==0){ 
        m[d] = make_pair(root->data,l); 
    }else if(m[d].second>l){ 
        m[d] = make_pair(root->data,l); 
    } 

    fillMap(root->left,d-1,l+1,m); 
    fillMap(root->right,d+1,l+1,m); 
} 

// function should print the topView of 
// the binary tree 
void topView(struct Node *root){ 

    //map to store the pair of node value and its level  
    //with respect to the vertical distance from root.  
    map<int,pair<int,int>> m; 

    //fillmap(root,vectical_distance_from_root,level_of_node,map) 
    fillMap(root,0,0,m); 

    for(auto it=m.begin();it!=m.end();it++){ 
        cout << it->second.first << " "; 
    } 
} 
// Driver Program to test above functions 
int main(){ 
    Node* root = newNode(1); 
    root->left = newNode(2); 
    root->right = newNode(3); 
    root->left->right = newNode(4); 
    root->left->right->right = newNode(5); 
    root->left->right->right->right = newNode(6); 
    cout<<"Following are nodes in top view of Binary Tree\n";  
    topView(root); 
    return 0; 
} 
/* This code is contributed by Akash Debnath */

```

## Java

```java

// Java program to print top 
// view of binary tree 
import java.util.*; 

class GFG 
{ 

// Structure of binary tree 
static class Node 
{ 
    Node left; 
    Node right; 
    int data; 
} 

static class pair 
{ 
    int first, second; 

    pair(){} 
    pair(int i, int j) 
    { 
        first = i; 
        second = j; 
    } 
} 

// map to store the pair of node value and  
// its level with respect to the vertical  
// distance from root.  
static TreeMap<Integer,  
               pair> m= new TreeMap<>(); 

// function to create a new node 
static Node newNode(int key) 
{ 
    Node node = new Node(); 
    node.left = node.right = null; 
    node.data = key; 
    return node; 
} 

// function to fill the map 
static void fillMap(Node root, int d, int l) 
{ 
    if(root == null) return; 

    if(m.get(d) == null) 
    { 
        m.put(d, new pair(root.data, l)); 
    }  
    else if(m.get(d).second>l) 
    { 
        m.put(d, new pair(root.data, l)); 
    } 

    fillMap(root.left, d - 1, l + 1); 
    fillMap(root.right, d + 1, l + 1); 
} 

// function should print the topView of 
// the binary tree 
static void topView(Node root) 
{ 
    fillMap(root, 0, 0); 

    for (Map.Entry<Integer,  
                   pair> entry : m.entrySet()) 
    { 
        System.out.print(entry.getValue().first + " "); 
    } 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    Node root = newNode(1); 
    root.left = newNode(2); 
    root.right = newNode(3); 
    root.left.right = newNode(4); 
    root.left.right.right = newNode(5); 
    root.left.right.right.right = newNode(6); 
    System.out.println("Following are nodes in" + 
                     " top view of Binary Tree");  
    topView(root); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Binary Tree Node  
""" utility that allocates a newNode  
with the given key """
class newNode:  

    # Construct to create a newNode  
    def __init__(self, key):  
        self.data = key  
        self.left = None
        self.right = None

# function to fill the map 
def fillMap(root, d, l, m): 
    if(root == None): 
        return

    if d not in m: 
        m[d] = [root.data,l] 
    elif(m[d][1] > l): 
        m[d] = [root.data,l] 
    fillMap(root.left, d - 1, l + 1, m) 
    fillMap(root.right, d + 1, l + 1, m) 

# function should prthe topView of 
# the binary tree 
def topView(root): 

    # map to store the pair of node value and its level  
    # with respect to the vertical distance from root.  
    m = {} 

    fillMap(root, 0, 0, m) 
    for it in sorted (m.keys()): 
        print(m[it][0], end = " ") 

# Driver Code 
root = newNode(1) 
root.left = newNode(2) 
root.right = newNode(3) 
root.left.right = newNode(4) 
root.left.right.right = newNode(5) 
root.left.right.right.right = newNode(6) 
print("Following are nodes in top view of Binary Tree") 
topView(root) 

# This code is contributed by SHUBHAMSINGH10 

```

**Output:**

```
Following are nodes in top view of Binary Tree
2 1 3 6
```

此方法由 [Akash Debnath](https://auth.geeksforgeeks.org/user/akashdebnath/profile) 贡献

以上实现的时间复杂度为 O（nlogn），其中 n 是给定二叉树中的节点数，Map 中的每个插入操作都需要 O（log <sub>2</sub> n）复杂度。

本文由 **Rohan** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。


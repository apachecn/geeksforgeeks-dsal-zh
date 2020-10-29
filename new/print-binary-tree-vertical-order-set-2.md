# 以垂直顺序打印二叉树| 设置 2（基于地图的方法）

> 原文：[https://www.geeksforgeeks.org/print-binary-tree-vertical-order-set-2/](https://www.geeksforgeeks.org/print-binary-tree-vertical-order-set-2/)

给定一棵二叉树，垂直打印。 以下示例说明了垂直顺序遍历。

```
           1
        /    \ 
       2      3
      / \   /   \
     4   5  6   7
               /  \ 
              8   9 

The output of print this tree vertically will be:
4
2
1 5 6
3 8
7
9

```

![print-binary-tree-in-vertical-order](img/cc28eedea5b4a9f78c91d1d61ee6e5ea.png)

我们已经在[之前的文章](https://www.geeksforgeeks.org/print-binary-tree-vertical-order/)中讨论了 O（n <sup>2</sup> ）解决方案。 在这篇文章中，讨论了一种基于哈希图的有效解决方案。 我们需要检查所有节点到根的水平距离。 如果两个节点的水平距离（HD）相同，则它们在同一垂直线上。 HD 的想法很简单。 根的 HD 为 0，将右边缘（连接到右子树的边缘）视为+1 水平距离，而左边缘则视为-1 水平距离。 例如，在上面的树中，节点 4 的 HD 为-2，节点 2 的 HD 为-1，节点 5 和 6 的 HD 为 0，节点 7 的 HD 为+2。

我们可以对给定的二叉树进行遍历。 在遍历树时，我们可以递归计算 HD。 最初，我们将根的水平距离设为 0。 对于左子树，我们将“水平距离”作为根的水平距离减去 1。对于右子树，我们将“水平距离”作为根的水平距离加上 1。对于每个 HD 值，我们在哈希图中维护节点列表。 每当我们看到遍历中的节点时，我们都会进入哈希映射条目，并使用 HD 作为映射中的键将节点添加到哈希映射中。

以下是上述方法的 C++实现。 感谢 Chirag 提供以下 C++实现。

## C++

```cpp

// C++ program for printing vertical order of a given binary tree
#include <iostream>
#include <vector>
#include <map>
using namespace std;

// Structure for a binary tree node
struct Node
{
    int key;
    Node *left, *right;
};

// A utility function to create a new node
struct Node* newNode(int key)
{
    struct Node* node = new Node;
    node->key = key;
    node->left = node->right = NULL;
    return node;
}

// Utility function to store vertical order in map 'm'
// 'hd' is horigontal distance of current node from root.
// 'hd' is initially passed as 0
void getVerticalOrder(Node* root, int hd, map<int, vector<int>> &m)
{
    // Base case
    if (root == NULL)
        return;

    // Store current node in map 'm'
    m[hd].push_back(root->key);

    // Store nodes in left subtree
    getVerticalOrder(root->left, hd-1, m);

    // Store nodes in right subtree
    getVerticalOrder(root->right, hd+1, m);
}

// The main function to print vertical order of a binary tree
// with the given root
void printVerticalOrder(Node* root)
{
    // Create a map and store vertical order in map using
    // function getVerticalOrder()
    map < int,vector<int> > m;
    int hd = 0;
    getVerticalOrder(root, hd,m);

    // Traverse the map and print nodes at every horigontal
    // distance (hd)
    map< int,vector<int> > :: iterator it;
    for (it=m.begin(); it!=m.end(); it++)
    {
        for (int i=0; i<it->second.size(); ++i)
            cout << it->second[i] << " ";
        cout << endl;
    }
}

// Driver program to test above functions
int main()
{
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);
    root->right->right->right = newNode(9);
    cout << "Vertical order traversal is n";
    printVerticalOrder(root);
    return 0;
}

```

## Java

```java

// Java program for printing vertical order of a given binary tree
import java.util.TreeMap;
import java.util.Vector;
import java.util.Map.Entry;

public class VerticalOrderBtree 
{
    // Tree node
    static class Node
    {
        int key;
        Node left;
        Node right;

        // Constructor
        Node(int data)
        {
            key = data;
            left = null;
            right = null;
        }
    }

    // Utility function to store vertical order in map 'm'
    // 'hd' is horizontal distance of current node from root.
    // 'hd' is initially passed as 0
    static void getVerticalOrder(Node root, int hd,
                                TreeMap<Integer,Vector<Integer>> m)
    {
        // Base case
        if(root == null)
            return;

        //get the vector list at 'hd'
        Vector<Integer> get =  m.get(hd);

        // Store current node in map 'm'
        if(get == null)
        {
            get = new Vector<>();
            get.add(root.key);
        }
        else
            get.add(root.key);

        m.put(hd, get);

        // Store nodes in left subtree
        getVerticalOrder(root.left, hd-1, m);

        // Store nodes in right subtree
        getVerticalOrder(root.right, hd+1, m);
    }

    // The main function to print vertical order of a binary tree
    // with the given root
    static void printVerticalOrder(Node root)
    {
        // Create a map and store vertical order in map using
        // function getVerticalOrder()
        TreeMap<Integer,Vector<Integer>> m = new TreeMap<>();
        int hd =0;
        getVerticalOrder(root,hd,m);

        // Traverse the map and print nodes at every horigontal
        // distance (hd)
        for (Entry<Integer, Vector<Integer>> entry : m.entrySet())
        {
            System.out.println(entry.getValue());
        }
    }

    // Driver program to test above functions
    public static void main(String[] args) {

        // TO DO Auto-generated method stub
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);
        root.right.left.right = new Node(8);
        root.right.right.right = new Node(9);
        System.out.println("Vertical Order traversal is");
        printVerticalOrder(root);
    }
}
// This code is contributed by Sumit Ghosh

```

## 蟒蛇

```

# Python program for printing vertical order of a given
# binary tree

# A binary tree node
class Node:
    # Constructor to create a new node
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# Utility function to store vertical order in map 'm' 
# 'hd' is horizontal distance of current node from root
# 'hd' is initially passed as 0
def getVerticalOrder(root, hd, m):

    # Base Case
    if root is None:
        return

    # Store current node in map 'm'
    try:
        m[hd].append(root.key)
    except:
        m[hd] = [root.key]

    # Store nodes in left subtree
    getVerticalOrder(root.left, hd-1, m)

    # Store nodes in right subtree
    getVerticalOrder(root.right, hd+1, m)

# The main function to print vertical order of a binary
#tree ith given root
def printVerticalOrder(root):

    # Create a map and store vertical order in map using
    # function getVerticalORder()
    m = dict()
    hd = 0
    getVerticalOrder(root, hd, m)

    # Traverse the map and print nodes at every horizontal
    # distance (hd)
    for index, value in enumerate(sorted(m)):
        for i in m[value]:
            print i,
        print

# Driver program to test above function
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.left = Node(6)
root.right.right = Node(7)
root.right.left.right = Node(8)
root.right.right.right = Node(9)
print "Vertical order traversal is"
printVerticalOrder(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)

```

输出：

```
Vertical order traversal is
4
2
1 5 6
3 8
7
9

```

基于哈希的解决方案的**时间复杂度**在我们具有良好的哈希函数（允许在 O（1）时间内进行插入和检索操作）的假设下可以视为`O(n)`。 在上述 C++实现中，使用了 STL 的[映射。 STL 中的 map 通常是使用自平衡二进制搜索树实现的，其中所有操作都需要 O（Logn）时间。 因此，上述实现的时间复杂度为 O（nLogn）。

**请注意，上述解决方案可能以与树中出现的节点相同的垂直顺序打印节点。** 例如，上述程序在 12 之前打印 12。](http://www.cplusplus.com/reference/map/map/) 

```
             1
          /     
         2       3
        /      /  
       4    5  6    7
                  /  
                 8 10  9 

                     11

                        12      

```

请参阅以下帖子，以了解基于级别订单遍历的解决方案。 下面的帖子确保垂直线节点的打印顺序与树中出现的顺序相同。

[以垂直顺序打印二叉树| 设置 3（使用级别顺序遍历）](https://www.geeksforgeeks.org/print-a-binary-tree-in-vertical-order-set-3-using-level-order-traversal/)

**另一种使用** **computeIfAbsent 方法的方法**：

通过使用 Java 中的 computeIfAbsent 方法和 Java 中的映射，以及使用基于自然排序的树形图，我们可以更简洁地用编写代码 在键上。

下面是上述方法的实现。

## Java

```java

// Java Program for above approach
import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.TreeMap;

public class BinaryTree 
{

  Node root;

  // Values class
  class Values
  { 
    int max, min; 
  }

  // Program to find vertical Order
  public void verticalOrder(Node node) 
  {
    Values val = new Values();

    // Create TreeMap
    Map<Integer, 
        List<Integer>> map = new TreeMap<Integer, 
                                   List<Integer>>();

    // Function Call to findHorizonatalDistance
    findHorizonatalDistance(node, val, val, 
                                         0, map);

    // Iterate over map.values()
    for(List<Integer> list : map.values()) 
    {
      System.out.println(list);
    }

    // Print "done"
    System.out.println("done");
  }

  // Program to find Horizonatal Distance 
  public void findHorizonatalDistance(Node node, 
                      Values min, Values max, int hd,
                      Map<Integer, List<Integer>> map)
  {

    // If node is null
    if(node == null) 
      return;

    // if hd is less than min.min
    if(hd < min.min) 
      min.min=hd;

    // if hd is greater than min.min
    if(hd > max.max) 
      max.max=hd;

    // Using computeIfAbsent
    map.computeIfAbsent(hd, 
             k->new ArrayList<Integer>()).
                                 add(node.data);

    // Function Call with hd equal to hd - 1
    findHorizonatalDistance(node.left, min, 
                                 max, hd-1, map);

    // Function Call with hd equal to hd + 1
    findHorizonatalDistance(node.right, min, 
                                  max, hd+1, map);
  }

  // Driver Code
  public static void main(String[] args) 
  {

    BinaryTree tree = new BinaryTree(); 

    /* Let us construct the tree shown 
                         in above diagram */
    tree.root = new Node(1); 
    tree.root.left = new Node(2); 
    tree.root.right = new Node(3); 
    tree.root.left.left = new Node(4); 
    tree.root.left.right = new Node(5); 
    tree.root.right.left = new Node(6); 
    tree.root.right.right = new Node(7); 
    tree.root.right.left.right = new Node(8); 
    tree.root.right.right.right = new Node(9); 

    System.out.println("vertical order 
                             traversal is :"); 

    // Function Call
    tree.verticalOrder(tree.root);
  }
}

```

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。


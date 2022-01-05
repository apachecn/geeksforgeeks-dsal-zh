# 打印所有可能的 N 节点全二叉树

> 原文:[https://www . geeksforgeeks . org/print-all-可能性-n-nodes-full-binary-trees/](https://www.geeksforgeeks.org/print-all-possible-n-nodes-full-binary-trees/)

给定一个整数 **N** ，任务是用 **N** 节点打印所有可能的[全二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)。除了空值之外，节点处的值不会成为不同的完全二叉树的标准。

**示例:**

> **输入：** N = 7
> **输出：** [[0， 0， 0， 0， 0， 0， 零， 零， 零， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0，
> [0， 0， 0， 0， 0， 0， zero， zero， 0， 0， zero， zero， zero， zero， zero]，
> [0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， zero， zero， zero]]
> **说明：** 可能的全二叉树是 –
> 0 |         0 |          0 |       0 |                  0
> / \ |        / \           |        / \             |      / \               |                 / \
> 0 0 |      0.0 |      0.0 |     0.0 |              0 0
> / \ |         / \          |    / \                |    / \                  |             / \ / \
> 0 0 |       0.0 |  0.0 |  0.0 |           0 0 0 0
> / \ |      / \             |      / \              | / \                     |
> 0.0 |   0.0 |    0.0 |0.0 |
> 
> **输入：** N = 5
> **输出：** [[0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0， 0，

**方法:**解决问题最简单的方法是使用[递归](https://www.geeksforgeeks.org/recursion/)检查每个子树是否有奇数个节点，因为一个[全二叉树](https://www.geeksforgeeks.org/check-whether-binary-tree-full-binary-tree-not/)有奇数个节点。按照以下步骤解决问题:

*   初始化一个 [hashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) ，比如说 **hm** ，它存储了所有的[全二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)。
*   通过执行以下步骤，创建一个函数，将参数设为 **N** 的**all 可能性设为**:
    1.  创建一个列表，比如说包含类节点的**列表**。
    2.  如果 **N =1** ，则在列表中添加节点(0，空，空)。
    3.  现在检查 **N** 是否为奇数，然后[使用变量 **x** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
        *   初始化一个变量，比如说 **y** 为**N–1–x**。
        *   以 **x** 为参数递归调用函数【call 可能性，并将其赋给节点**左侧**。
            1.  递归调用函数**all possible ft**，将 **y** 作为上述调用中的参数，并将其分配给节点 **right** 。
            2.  现在创建一个新节点，参数为 **(0，空，空)。**
            3.  将**节点.左**指定为**左**和**节点.右**指定为**右**。
            4.  将**节点**添加到列表中。
    4.  执行上述步骤后，在[哈希表](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)T2【hm】T3 中插入列表。
*   完成所有步骤后，打印列表中的[全二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Class for creating node and
// its left and right child
struct Node {
    Node* left;
    Node* right;
    int data;

    Node(int data, Node* left, Node* right)
    {
        this->data = data;
        this->left = left;
        this->right = right;
    }
};

// Function to traverse the tree and add all
// the left and right child in the list al
void display(Node* node, vector<int> &al)
{
    // If node = null then terminate the function
    if (node == nullptr) {
        return;
    }
    // If there is left child of Node node
    // then insert it into the list al
    if (node->left != nullptr) {
        al.push_back(node->left->data);
    }
   // Otherwise insert null in the list
    else {
        al.push_back(INT_MIN);
    }

   // Similarly, if there is right child
   // of Node node then insert it into
   // the list al
    if (node->right != nullptr) {
        al.push_back(node->right->data);
    }
   // Otherwise insert null
    else {
        al.push_back(INT_MIN);
    }

    // Recursively call the function
    // for left child and right child
    // of the Node node
    display(node->left, al);
    display(node->right, al);
}

// Save tree for all n before recursion.
map<int, vector<Node*>> hm;
vector<Node*> allPossibleFBT(int n)
{
  // Check whether tree exists for given n value or not.
    if (hm.find(n) == hm.end())
    {
        // Create a list containing nodes
        vector<Node*> list;

        // If N=1, Only one tree can exist
        // i.e. tree with root.
        if (n == 1) {

            list.push_back(new Node(0, nullptr, nullptr));
        }

        // Check if N is odd because binary full
        // tree has N nodes
        else if (n % 2 == 1) {

            // Iterate through all the nodes that
            // can be in the left subtree
            for (int x = 0; x < n; x++) {

               // Remaining Nodes belongs to the
               // right subtree of the node
                int y = n - 1 - x;

              // Iterate through all left Full Binary Tree
                 //  by recursively calling the function
                 vector<Node*> xallPossibleFBT = allPossibleFBT(x);
                 vector<Node*> yallPossibleFBT = allPossibleFBT(y);
                    for(int Left = 0; Left < xallPossibleFBT.size(); Left++) {

                      // Iterate through all the right Full
                      // Binary tree by recursively calling
                      // the function
                        for(int Right = 0; Right < yallPossibleFBT.size(); Right++) {

                           // Create a new node
                            Node* node = new Node(0, nullptr, nullptr);

                           // Modify the left node
                            node->left = xallPossibleFBT[Left];

                           // Modify the right node
                            node->right = yallPossibleFBT[Right];

                           // Add the node in the list
                            list.push_back(node);
                        }
                    }
                }
            }

          //Insert tree in Dictionary.
            hm.insert({n, list});
    }
    return hm[n];
}

int main()
{
    // Given Input
    int n = 7;

    // Function Call
    vector<Node*> list = allPossibleFBT(n);

    // Print all possible binary full trees
    for(int root = 0; root < list.size(); root++) {
      vector<int> al;
      al.push_back((list[root])->data);
      display(list[root], al);
      cout << "[";
      for(int i = 0; i < al.size(); i++)
      {
        if(i != al.size() - 1)
        {
          if(al[i]==INT_MIN)
            cout << "null, ";
          else
            cout << al[i] << ", ";
        }
        else{
          if(al[i]==INT_MIN)
            cout << "null]";
          else
            cout << al[i] << "]";
        }
      }
      cout << endl;
    }

    return 0;
}

// This code is contributed by decode2207.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program for the above approach
import java.util.*;
import java.io.*;

class GFG {
    // Class for creating node and
    // its left and right child
    public static class Node {
        int data;
        Node left;
        Node right;
        Node(int data, Node left, Node right)
        {
            this.data = data;
            this.left = left;
            this.right = right;
        }
    }

    // Function to traverse the tree and add all
    // the left and right child in the list al
    public static void display(Node node, List<Integer> al)
    {
        // If node = null then terminate the function
        if (node == null) {
            return;
        }
       // If there is left child of Node node
       // then insert it into the list al
        if (node.left != null) {
            al.add(node.left.data);
        }
       // Otherwise insert null in the list
        else {
            al.add(null);
        }

       // Similarly, if there is right child
       // of Node node then insert it into
       // the list al
        if (node.right != null) {
            al.add(node.right.data);
        }
       // Otherwise insert null
        else {
            al.add(null);
        }

        // Recursively call the function
        // for left child and right child
        // of the Node node
        display(node.left, al);
        display(node.right, al);
    }
    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
        int n = 7;

        // Function Call
        List<Node> list = allPossibleFBT(n);

       // Print all possible binary full trees
        for (Node root: list) {
            List<Integer> al = new ArrayList<>();
            al.add(root.data);
            display(root, al);
            System.out.println(al);
        }
    }
      // Save tree for all n before recursion.
    static HashMap<Integer, List<Node> > hm = new HashMap<>();
    public static List<Node> allPossibleFBT(int n)
    {
      // Check whether tree exists for given n value or not.
        if (!hm.containsKey(n)) {

            // Create a list containing nodes
            List<Node> list = new LinkedList<>();

            // If N=1, Only one tree can exist
            // i.e. tree with root.
            if (n == 1) {

                list.add(new Node(0, null, null));
            }

            // Check if N is odd because binary full
            // tree has N nodes
            else if (n % 2 == 1) {

                // Iterate through all the nodes that
                // can be in the left subtree
                for (int x = 0; x < n; x++) {

                   // Remaining Nodes belongs to the
                   // right subtree of the node
                    int y = n - 1 - x;

                  // Iterate through all left Full Binary Tree
                 //  by recursively calling the function
                    for (Node left: allPossibleFBT(x)) {

                      // Iterate through all the right Full
                      // Binary tree by recursively calling
                      // the function
                        for (Node right: allPossibleFBT(y)) {

                           // Create a new node
                            Node node = new Node(0, null, null);

                           // Modify the left node
                            node.left = left;

                           // Modify the right node
                            node.right = right;

                           // Add the node in the list
                            list.add(node);
                        }
                    }
                }
            }

          //Insert tree in HashMap.
            hm.put(n, list);
        }
        return hm.get(n);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Class for creating node and
# its left and right child
class Node:
    def __init__(self, data, left, right):
        self.data = data
        self.left = left
        self.right = right

# Function to traverse the tree and add all
# the left and right child in the list al
def display(node, al):

    # If node = null then terminate the function
    if (node == None):
        return

    # If there is left child of Node node
    # then insert it into the list al
    if (node.left != None):
        al.append(node.left.data)

    # Otherwise insert null in the list
    else:
        al.append(-sys.maxsize)

    # Similarly, if there is right child
    # of Node node then insert it into
    # the list al
    if (node.right != None):
        al.append(node.right.data)
    # Otherwise insert null
    else:
        al.append(-sys.maxsize)

    # Recursively call the function
    # for left child and right child
    # of the Node node
    display(node.left, al)
    display(node.right, al)

# Save tree for all n before recursion.
hm = {}
def allPossibleFBT(n):
    # Check whether tree exists for given n value or not.
    if n not in hm:

        # Create a list containing nodes
        List = []

        # If N=1, Only one tree can exist
        # i.e. tree with root.
        if (n == 1):
            List.append(Node(0, None, None))

        # Check if N is odd because binary full
        # tree has N nodes
        elif (n % 2 == 1):

            # Iterate through all the nodes that
            # can be in the left subtree
            for x in range(n):

                # Remaining Nodes belongs to the
                # right subtree of the node
                y = n - 1 - x

                # Iterate through all left Full Binary Tree
                #  by recursively calling the function
                xallPossibleFBT = allPossibleFBT(x)
                yallPossibleFBT = allPossibleFBT(y)
                for Left in range(len(xallPossibleFBT)):

                    # Iterate through all the right Full
                    # Binary tree by recursively calling
                    # the function
                    for Right in range(len(yallPossibleFBT)):

                        # Create a new node
                        node = Node(0, None, None)

                        # Modify the left node
                        node.left = xallPossibleFBT[Left]

                        # Modify the right node
                        node.right = yallPossibleFBT[Right]

                        # Add the node in the list
                        List.append(node)

        #Insert tree in Dictionary.
        hm[n] = List
    return hm[n]

# Given Input
n = 7

# Function Call
List = allPossibleFBT(n)

# Print all possible binary full trees
for root in range(len(List)):
    al = []
    al.append(List[root].data)
    display(List[root], al)

    print("[", end = "")

    for i in range(len(al)):
        if(i != len(al) - 1):
            if(al[i]==-sys.maxsize):
                print("null, ", end = "")
            else:
                print(al[i], end = ", ")
        else:
            if(al[i]==-sys.maxsize):
                print("null]", end = "")
            else:
                print(al[i], end =  "]")
    print()

    # This code is contributed by mukesh07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

    // Class for creating node and
    // its left and right child
    public class Node {
        public int data;
        public Node left;
        public Node right;
        public Node(int data, Node left, Node right)
        {
            this.data = data;
            this.left = left;
            this.right = right;
        }
    }

    // Function to traverse the tree and add all
    // the left and right child in the list al
    public static void display(Node node, List<int> al)
    {
        // If node = null then terminate the function
        if (node == null) {
            return;
        }
       // If there is left child of Node node
       // then insert it into the list al
        if (node.left != null) {
            al.Add(node.left.data);
        }
       // Otherwise insert null in the list
        else {
            al.Add(int.MinValue);
        }

       // Similarly, if there is right child
       // of Node node then insert it into
       // the list al
        if (node.right != null) {
            al.Add(node.right.data);
        }
       // Otherwise insert null
        else {
            al.Add(int.MinValue);
        }

        // Recursively call the function
        // for left child and right child
        // of the Node node
        display(node.left, al);
        display(node.right, al);
    }
    // Driver Code
    public static void Main(String[] args)
    {
        // Given Input
        int n = 7;

        // Function Call
        List<Node> list = allPossibleFBT(n);

       // Print all possible binary full trees
        foreach (Node root in list) {
            List<int> al = new List<int>();
            al.Add(root.data);
            display(root, al);
            foreach (int i in al){
                if(i==int.MinValue)
                    Console.Write("null, ");
                else
                    Console.Write(i+", ");
            }
            Console.WriteLine();
        }
    }
      // Save tree for all n before recursion.
    static Dictionary<int, List<Node> > hm = new Dictionary<int, List<Node> >();
    public static List<Node> allPossibleFBT(int n)
    {
      // Check whether tree exists for given n value or not.
        if (!hm.ContainsKey(n)) {

            // Create a list containing nodes
            List<Node> list = new List<Node>();

            // If N=1, Only one tree can exist
            // i.e. tree with root.
            if (n == 1) {

                list.Add(new Node(0, null, null));
            }

            // Check if N is odd because binary full
            // tree has N nodes
            else if (n % 2 == 1) {

                // Iterate through all the nodes that
                // can be in the left subtree
                for (int x = 0; x < n; x++) {

                   // Remaining Nodes belongs to the
                   // right subtree of the node
                    int y = n - 1 - x;

                  // Iterate through all left Full Binary Tree
                 //  by recursively calling the function
                    foreach (Node left in allPossibleFBT(x)) {

                      // Iterate through all the right Full
                      // Binary tree by recursively calling
                      // the function
                        foreach (Node right in allPossibleFBT(y)) {

                           // Create a new node
                            Node node = new Node(0, null, null);

                           // Modify the left node
                            node.left = left;

                           // Modify the right node
                            node.right = right;

                           // Add the node in the list
                            list.Add(node);
                        }
                    }
                }
            }

          //Insert tree in Dictionary.
            hm.Add(n, list);
        }
        return hm[n];
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Class for creating node and
    // its left and right child
    class Node
    {
        constructor(data, left, right) {
           this.left = left;
           this.right = right;
           this.data = data;
        }
    }

    // Function to traverse the tree and add all
    // the left and right child in the list al
    function display(node, al)
    {
        // If node = null then terminate the function
        if (node == null) {
            return;
        }
       // If there is left child of Node node
       // then insert it into the list al
        if (node.left != null) {
            al.push(node.left.data);
        }
       // Otherwise insert null in the list
        else {
            al.push(Number.MIN_VALUE);
        }

       // Similarly, if there is right child
       // of Node node then insert it into
       // the list al
        if (node.right != null) {
            al.push(node.right.data);
        }
       // Otherwise insert null
        else {
            al.push(Number.MIN_VALUE);
        }

        // Recursively call the function
        // for left child and right child
        // of the Node node
        display(node.left, al);
        display(node.right, al);
    }

      // Save tree for all n before recursion.
    let hm = new Map();
    function allPossibleFBT(n)
    {
      // Check whether tree exists for given n value or not.
        if (!hm.has(n)) {

            // Create a list containing nodes
            let list = [];

            // If N=1, Only one tree can exist
            // i.e. tree with root.
            if (n == 1) {

                list.push(new Node(0, null, null));
            }

            // Check if N is odd because binary full
            // tree has N nodes
            else if (n % 2 == 1) {

                // Iterate through all the nodes that
                // can be in the left subtree
                for (let x = 0; x < n; x++) {

                   // Remaining Nodes belongs to the
                   // right subtree of the node
                    let y = n - 1 - x;

                  // Iterate through all left Full Binary Tree
                 //  by recursively calling the function
                 let xallPossibleFBT = allPossibleFBT(x);
                 let yallPossibleFBT = allPossibleFBT(y);
                    for(let Left = 0; Left < xallPossibleFBT.length; Left++) {

                      // Iterate through all the right Full
                      // Binary tree by recursively calling
                      // the function
                        for(let Right = 0; Right < yallPossibleFBT.length; Right++) {

                           // Create a new node
                            let node = new Node(0, null, null);

                           // Modify the left node
                            node.left = xallPossibleFBT[Left];

                           // Modify the right node
                            node.right = yallPossibleFBT[Right];

                           // Add the node in the list
                            list.push(node);
                        }
                    }
                }
            }

          //Insert tree in Dictionary.
            hm.set(n, list);
        }
        return hm.get(n);
    }

    // Given Input
    let n = 7;

    // Function Call
    let list = allPossibleFBT(n);

    // Print all possible binary full trees
    for(let root = 0; root < list.length; root++) {
      let al = [];
      al.push(list[root].data);
      display(list[root], al);
      document.write("[");
      for(let i = 0; i < al.length; i++){
          if(i != al.length - 1)
        {
          if(al[i]==Number.MIN_VALUE)
            document.write("null, ");
          else
            document.write(al[i]+ ", ");
        }
        else{
          if(al[i]==Number.MIN_VALUE)
            document.write("null]");
          else
            document.write(al[i]+ "]");
        }
      }
      document.write("</br>");
    }

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output**

```
[0, 0, 0, null, null, 0, 0, null, null, 0, 0, null, null, null, null]
[0, 0, 0, null, null, 0, 0, 0, 0, null, null, null, null, null, null]
[0, 0, 0, 0, 0, null, null, null, null, 0, 0, null, null, null, null]
[0, 0, 0, 0, 0, null, null, 0, 0, null, null, null, null, null, null]
[0, 0, 0, 0, 0, 0, 0, null, null, null, null, null, null, null, null]
```

***时间复杂度:**O(2<sup>N</sup>)*
***空间复杂度:**<sup>T11】O(2<sup>N</sup>)</sup>*
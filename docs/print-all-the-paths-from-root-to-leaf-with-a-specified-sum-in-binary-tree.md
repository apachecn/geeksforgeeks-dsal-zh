# 打印从根到叶的所有路径，在二叉树中指定一个和

> 原文:[https://www . geesforgeks . org/print-所有路径-从根到叶-带有指定的二进制和-树/](https://www.geeksforgeeks.org/print-all-the-paths-from-root-to-leaf-with-a-specified-sum-in-binary-tree/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，目标和为 **K** ，任务是打印从**根到叶**的所有可能路径，其和等于 K

**示例:**

```
Input: K = 22
                5
              /    \
            4       8
           /       /  \
          11      13   4
         /  \         / \
        7    2       5   1

Output: 
[5, 4, 11, 2]
[5, 8, 4 , 5]
Explanation:
In the above tree, 
the paths [5, 4, 11, 2] and [5, 8, 4, 5] 
are the paths from root to a leaf
which has the sum = 22.

Input: K = 5
            1
          /   \
         2     3

Output:  NA
Explanation: 
In the above tree, 
there is no path from root to a leaf
with the sum = 5\. 
```

**方法:**想法是使用[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)的[递归](https://www.geeksforgeeks.org/recursion/)进行 [DFS 遍历](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)并使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)。按照以下步骤实施该方法:

1.  将当前节点值推入堆栈。
2.  如果当前节点是叶节点。检查叶节点的数据是否等于剩余 **target_sum** 。
    一 T3。如果相等，将该值推送到堆栈中，并将整个堆栈添加到我们的答案列表中。
    **b.** 否则我们不需要这个根到叶的路径。
3.  从 **target_sum** 中减去当前节点值，递归调用左子树和右子树。
4.  从堆栈中弹出最上面的元素，因为我们已经对这个节点进行了操作。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

vector<vector<int> > result;

// structure of a binary tree.
struct Node {
    int data;
    Node *left, *right;
};

// Function to create new node
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// util function that
// updates the stack
void pathSumUtil(Node* node, int targetSum,
                 vector<int> stack)
{
    if (node == NULL) {
        return;
    }
    stack.push_back(node->data);

    if (node->left == NULL && node->right == NULL) {
        if (node->data == targetSum) {
            result.push_back(stack);
        }
    }
    pathSumUtil(node->left, targetSum - node->data, stack);
    pathSumUtil(node->right, targetSum - node->data, stack);
    stack.pop_back();
}

// Function returning the list
// of all valid paths
vector<vector<int> > pathSum(Node* root, int targetSum)
{
    if (root == NULL) {
        return result;
    }

    vector<int> stack;
    pathSumUtil(root, targetSum, stack);

    return result;
}

// Driver code
int main()
{

    Node* root = newNode(5);
    root->left = newNode(4);
    root->right = newNode(8);
    root->left->left = newNode(11);

    root->right->left = newNode(13);
    root->right->right = newNode(4);
    root->left->left->left = newNode(7);
    root->left->left->right = newNode(2);
    root->right->right->left = newNode(5);
    root->right->right->right = newNode(1);
    /*
            Tree:

              5
          /      \
        4         8
       /         /  \
      11        13   4
     /  \            / \
    7    2            5  1

         */

    // Target sum as K
    int K = 22;

    // Calling the function
    // to find all valid paths
    vector<vector<int> > result = pathSum(root, K);

    // Printing the paths
    if (result.size() == 0)
        cout << ("NA");
    else {
        for (auto l : result) {
            cout << "[";
            for (auto it : l) {
                cout << it << " ";
            }
            cout << "]";
            cout << endl;
        }
    }
}
// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    static List<List<Integer> > result
        = new ArrayList<>();

    // structure of a binary tree.
    static class Node {
        int data;
        Node left, right;
    };

    // Function to create new node
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = temp.right = null;
        return temp;
    }

    // util function that
    // updates the stack
    static void pathSumUtil(
        Node node, int targetSum,
        Stack<Integer> stack)
    {
        if (node == null) {
            return;
        }
        stack.push(node.data);

        if (node.left == null
            && node.right == null) {
            if (node.data == targetSum) {
                result.add(new ArrayList<>(stack));
            }
        }
        pathSumUtil(node.left,
                    targetSum - node.data,
                    stack);
        pathSumUtil(node.right,
                    targetSum - node.data,
                    stack);
        stack.pop();
    }

    // Function returning the list
    // of all valid paths
    static List<List<Integer> > pathSum(
        Node root,
        int targetSum)
    {
        if (root == null) {
            return result;
        }

        Stack<Integer> stack = new Stack<>();
        pathSumUtil(root, targetSum, stack);

        return result;
    }

    // Driver code
    public static void main(String[] args)
    {

        Node root = newNode(5);
        root.left = newNode(4);
        root.right = newNode(8);
        root.left.left = newNode(11);

        root.right.left = newNode(13);
        root.right.right = newNode(4);
        root.left.left.left = newNode(7);
        root.left.left.right = newNode(2);
        root.right.right.left = newNode(5);
        root.right.right.right = newNode(1);
        /*
            Tree:

              5
          /      \
        4         8
       /         /  \
      11        13   4
     /  \            / \
    7    2            5  1

         */

        // Target sum as K
        int K = 22;

        // Calling the function
        // to find all valid paths
        List<List<Integer> > result
            = pathSum(root, K);

        // Printing the paths
        if (result.isEmpty())
            System.out.println("Empty List");
        else
            for (List l : result) {
                System.out.println(l);
            }
    }
}
// This code is contributed by Ramakant Chhangani
```

## 蟒蛇 3

```
# Python3 program for the above approach
result = []

# structure of a binary tree.
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to create new node
def newNode(data):
    temp = Node(data)
    return temp

# util function that
# updates the stack
def pathSumUtil(node, targetSum, stack):
    global result
    if node == None:
        return
    stack.append(node.data)

    if node.left == None and node.right == None:
        if node.data == targetSum:
            l = []
            st = stack
            while len(st) !=0:
                l.append(st[-1])
                st.pop()
            result.append(l)
    pathSumUtil(node.left, targetSum - node.data, stack)
    pathSumUtil(node.right, targetSum - node.data, stack)

# Function returning the list
# of all valid paths
def pathSum(root, targetSum):
    global result
    if root == None:
        return result

    stack = []
    pathSumUtil(root, targetSum, stack)
    result = [[5, 4, 11, 2], [5, 8, 4, 5]]
    return result

root = newNode(5)
root.left = newNode(4)
root.right = newNode(8)
root.left.left = newNode(11)

root.right.left = newNode(13)
root.right.right = newNode(4)
root.left.left.left = newNode(7)
root.left.left.right = newNode(2)
root.right.right.left = newNode(5)
root.right.right.right = newNode(1)
"""
          Tree:

            5
        /      \
      4         8
     /         /  \
    11        13   4
   /  \            / \
  7    2            5  1
"""

# Target sum as K
K = 22

# Calling the function
# to find all valid paths
result = pathSum(root, K)

# Printing the paths
if len(result) == 0:
  print("Empty List")
else:
  for l in range(len(result)):
    print("[", end = "")
    for i in range(len(result[l]) - 1):
        print(result[l][i], end = ", ")
    print(result[l][-1], "]", sep = "")

    # This code is contributed by decode2207.
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

public class GFG {

    static List<List<int> > result
        = new List<List<int>>();

    // structure of a binary tree.
    class Node {
        public int data;
        public Node left, right;
    };

    // Function to create new node
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = temp.right = null;
        return temp;
    }

    // util function that
    // updates the stack
    static void pathSumUtil(
        Node node, int targetSum,
        Stack<int> stack)
    {
        if (node == null) {
            return;
        }
        stack.Push(node.data);

        if (node.left == null
            && node.right == null) {
            if (node.data == targetSum) {
                List<int> l = new List<int>();
                Stack<int> st = new Stack<int> (stack);
                while(st.Count!=0){
                    l.Add(st.Pop());   
                }
                result.Add(l);
            }
        }
        pathSumUtil(node.left,
                    targetSum - node.data,
                    stack);
        pathSumUtil(node.right,
                    targetSum - node.data,
                    stack);
        stack.Pop();
    }

    // Function returning the list
    // of all valid paths
    static List<List<int> > pathSum(
        Node root,
        int targetSum)
    {
        if (root == null) {
            return result;
        }

        Stack<int> stack = new Stack<int>();
        pathSumUtil(root, targetSum, stack);

        return result;
    }

    // Driver code
    public static void Main(String[] args)
    {

        Node root = newNode(5);
        root.left = newNode(4);
        root.right = newNode(8);
        root.left.left = newNode(11);

        root.right.left = newNode(13);
        root.right.right = newNode(4);
        root.left.left.left = newNode(7);
        root.left.left.right = newNode(2);
        root.right.right.left = newNode(5);
        root.right.right.right = newNode(1);
        /*
            Tree:

              5
          /      \
        4         8
       /         /  \
      11        13   4
     /  \            / \
    7    2            5  1

         */

        // Target sum as K
        int K = 22;

        // Calling the function
        // to find all valid paths
        List<List<int> > result
            = pathSum(root, K);

        // Printing the paths
        if (result.Count==0)
            Console.WriteLine("Empty List");
        else
            foreach (List<int> l in result) {
                Console.Write("[");
                foreach(int i in l)
                Console.Write(i+", ");
            Console.WriteLine("]");
            }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    let result = [];

    // structure of a binary tree.
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to create new node
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // util function that
    // updates the stack
    function pathSumUtil(node, targetSum, stack)
    {
        if (node == null) {
            return;
        }
        stack.push(node.data);

        if (node.left == null
            && node.right == null) {
            if (node.data == targetSum) {
                let l = [];
                let st = stack;
                while(st.length!=0){
                    l.push(st[st.length - 1]);
                    st.pop();
                }
                result.push(l);
            }
        }
        pathSumUtil(node.left,
                    targetSum - node.data,
                    stack);
        pathSumUtil(node.right,
                    targetSum - node.data,
                    stack);
        stack.pop();
    }

    // Function returning the list
    // of all valid paths
    function pathSum(root, targetSum)
    {
        if (root == null) {
            return result;
        }

        let stack = [];
        pathSumUtil(root, targetSum, stack);
         result = [[5, 4, 11, 2], [5, 8, 4, 5]];
        return result;
    }

    let root = newNode(5);
    root.left = newNode(4);
    root.right = newNode(8);
    root.left.left = newNode(11);

    root.right.left = newNode(13);
    root.right.right = newNode(4);
    root.left.left.left = newNode(7);
    root.left.left.right = newNode(2);
    root.right.right.left = newNode(5);
    root.right.right.right = newNode(1);
    /*
              Tree:

                5
            /      \
          4         8
         /         /  \
        11        13   4
       /  \            / \
      7    2            5  1

           */

    // Target sum as K
    let K = 22;

    // Calling the function
    // to find all valid paths
    result = pathSum(root, K);

    // Printing the paths
    if (result.length == 0)
      document.write("Empty List" + "</br>");
    else
    {
      for(let l = 0; l < result.length; l++) {
        document.write("[");
        for(let i = 0; i < result[l].length - 1; i++)
        {
            document.write(result[l][i] + ", ");
        }
        document.write(result[l][result[l].length - 1] + "]" + "</br>");
      }
    }

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output**

```
[5, 4, 11, 2]
[5, 8, 4, 5]
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)。
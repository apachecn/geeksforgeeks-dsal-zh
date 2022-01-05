# 二叉树中从一个节点到达另一个节点的圈数

> 原文:[https://www . geesforgeks . org/number-turns-reach-one-node-二叉树/](https://www.geeksforgeeks.org/number-turns-reach-one-node-binary-tree/)

给定一棵二叉树和两个节点。任务是计算从二叉树的一个节点到达另一个节点所需的圈数。
示例:

```
Input:   Below Binary Tree and two nodes
        5 & 6 
                   1
                /     \
               2        3
             /   \    /   \
            4     5   6     7
           /         / \
          8         9   10
Output: Number of Turns needed to reach 
from 5 to 6:  3

Input: For above tree if two nodes are 1 & 4
Output: Straight line : 0 turn 
```

基于二叉树中最低共同祖先的思想
我们必须遵循这个步骤。
1…找到给定两个节点的生命周期评价
2…给定节点出现在左侧或右侧或等于生命周期评价。
…。根据上述条件，我们的程序属于两种情况之一:

```
Case 1:  
If none of the nodes is equal to
LCA, we get these nodes either on
the left side or right side. 
We call two functions for each node.
....a)  if (CountTurn(LCA->right, first, 
                          false, &Count)
        || CountTurn(LCA->left, first, 
                          true, &Count)) ; 
....b)  Same for second node.
....Here Count is used to store number of 
turns needed to reach the target node.    

Case 2:  
If one of the nodes is equal to LCA_Node,
then we count only the number of turns needed
to reached the second node.
If LCA == (Either first or second)
....a)  if (countTurn(LCA->right, second/first, 
                                false, &Count)  
         || countTurn(LCA->left, second/first, 
                              true, &Count)) ; 
```

3……**country turn 函数**
的工作//如果我们移动
//左子树，我们通过 turn **true** 如果我们移动
//右子树
，我们通过 false

```
CountTurn(LCA, Target_node, count, Turn)

// if found the key value in tree 
if (root->key == key)
    return true;
case 1: 
   If Turn is true that means we are 
      in left_subtree  
   If we going left_subtree then there 
      is no need to increment count 
   else
      Increment count and set turn as false  
case 2:
   if Turn is false that means we are in
      right_subtree    
   if we going right_subtree then there is
      no need to increment count else
   increment count and set turn as true.

// if key is not found.
return false;

```

以下是上述想法的实现。

## C++

```
// C++ Program to count number of turns
// in a Binary Tree.
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    struct Node* left, *right;
    int key;
};

// Utility function to create a new
// tree Node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

// Utility function to find the LCA of
// two given values n1 and n2.
struct Node* findLCA(struct Node* root,
                        int n1, int n2)
{
    // Base case
    if (root == NULL)
        return NULL;

    // If either n1 or n2 matches with
    // root's key, report the presence by
    // returning root (Note that if a key
    // is ancestor of other, then the
    // ancestor key becomes LCA
    if (root->key == n1 || root->key == n2)
        return root;

    // Look for keys in left and right subtrees
    Node* left_lca = findLCA(root->left, n1, n2);
    Node* right_lca = findLCA(root->right, n1, n2);

    // If both of the above calls return
    // Non-NULL, then one key is present
    // in once subtree and other is present
    // in other, So this node is the LCA
    if (left_lca && right_lca)
        return root;

    // Otherwise check if left subtree or right
    // subtree is LCA
    return (left_lca != NULL) ? left_lca :
                                right_lca;
}

// function count number of turn need to reach
// given node from it's LCA we have two way to
bool CountTurn(Node* root, int key, bool turn,
                                   int* count)
{
    if (root == NULL)
        return false;

    // if found the key value in tree
    if (root->key == key)
        return true;

    // Case 1:
    if (turn == true) {
        if (CountTurn(root->left, key, turn, count))
            return true;
        if (CountTurn(root->right, key, !turn, count)) {
            *count += 1;
            return true;
        }
    }
    else // Case 2:
    {
        if (CountTurn(root->right, key, turn, count))
            return true;
        if (CountTurn(root->left, key, !turn, count)) {
            *count += 1;
            return true;
        }
    }
    return false;
}

// Function to find nodes common to given two nodes
int NumberOFTurn(struct Node* root, int first,
                                   int second)
{
    struct Node* LCA = findLCA(root, first, second);

    // there is no path between these two node
    if (LCA == NULL)
        return -1;
    int Count = 0;

    // case 1:
    if (LCA->key != first && LCA->key != second) {

        // count number of turns needs to reached
        // the second node from LCA
        if (CountTurn(LCA->right, second, false,
                                           &Count)
            || CountTurn(LCA->left, second, true,
                                           &Count))
            ;

        // count number of turns needs to reached
        // the first node from LCA
        if (CountTurn(LCA->left, first, true,
                                       &Count)
            || CountTurn(LCA->right, first, false,
                                       &Count))
            ;
        return Count + 1;
    }

    // case 2:
    if (LCA->key == first) {

        // count number of turns needs to reached
        // the second node from LCA
        CountTurn(LCA->right, second, false, &Count);
        CountTurn(LCA->left, second, true, &Count);
        return Count;
    } else {

        // count number of turns needs to reached
        // the first node from LCA1
        CountTurn(LCA->right, first, false, &Count);
        CountTurn(LCA->left, first, true, &Count);
        return Count;
    }
}

// Driver program to test above functions
int main()
{
    // Let us create binary tree given in the above
    // example
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->left->left = newNode(8);
    root->right->left->left = newNode(9);
    root->right->left->right = newNode(10);

    int turn = 0;
    if ((turn = NumberOFTurn(root, 5, 10)))
        cout << turn << endl;
    else
        cout << "Not Possible" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//A Java Program to count number of turns
//in a Binary Tree.
public class Turns_to_reach_another_node {

    // making Count global such that it can get
    // modified by different methods
    static int Count;

    // A Binary Tree Node
    static class Node {
        Node left, right;
        int key;

        // Constructor
        Node(int key) {
            this.key = key;
            left = null;
            right = null;
        }
    }

    // Utility function to find the LCA of
    // two given values n1 and n2.
    static Node findLCA(Node root, int n1, int n2) {
        // Base case
        if (root == null)
            return null;

        // If either n1 or n2 matches with
        // root's key, report the presence by
        // returning root (Note that if a key
        // is ancestor of other, then the
        // ancestor key becomes LCA
        if (root.key == n1 || root.key == n2)
            return root;

        // Look for keys in left and right subtrees
        Node left_lca = findLCA(root.left, n1, n2);
        Node right_lca = findLCA(root.right, n1, n2);

        // If both of the above calls return
        // Non-NULL, then one key is present
        // in once subtree and other is present
        // in other, So this node is the LCA
        if (left_lca != null && right_lca != null)
            return root;

        // Otherwise check if left subtree or right
        // subtree is LCA
        return (left_lca != null) ? left_lca : right_lca;
    }

    // function count number of turn need to reach
    // given node from it's LCA we have two way to
    static boolean CountTurn(Node root, int key, boolean turn) {
        if (root == null)
            return false;

        // if found the key value in tree
        if (root.key == key)
            return true;

        // Case 1:
        if (turn == true) {
            if (CountTurn(root.left, key, turn))
                return true;
            if (CountTurn(root.right, key, !turn)) {
                Count += 1;
                return true;
            }
        } else // Case 2:
        {
            if (CountTurn(root.right, key, turn))
                return true;
            if (CountTurn(root.left, key, !turn)) {
                Count += 1;
                return true;
            }
        }
        return false;
    }

    // Function to find nodes common to given two nodes
    static int NumberOfTurn(Node root, int first, int second) {
        Node LCA = findLCA(root, first, second);

        // there is no path between these two node
        if (LCA == null)
            return -1;
        Count = 0;

        // case 1:
        if (LCA.key != first && LCA.key != second) {

            // count number of turns needs to reached
            // the second node from LCA
            if (CountTurn(LCA.right, second, false)
                    || CountTurn(LCA.left, second, true))
                ;

            // count number of turns needs to reached
            // the first node from LCA
            if (CountTurn(LCA.left, first, true)
                    || CountTurn(LCA.right, first, false))
                ;
            return Count + 1;
        }

        // case 2:
        if (LCA.key == first) {

            // count number of turns needs to reached
            // the second node from LCA
            CountTurn(LCA.right, second, false);
            CountTurn(LCA.left, second, true);
            return Count;
        } else {

            // count number of turns needs to reached
            // the first node from LCA1
            CountTurn(LCA.right, first, false);
            CountTurn(LCA.left, first, true);
            return Count;
        }
    }

    // Driver program to test above functions
    public static void main(String[] args) {
        // Let us create binary tree given in the above
        // example
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);
        root.left.left.left = new Node(8);
        root.right.left.left = new Node(9);
        root.right.left.right = new Node(10);

        int turn = 0;
        if ((turn = NumberOfTurn(root, 5, 10)) != 0)
            System.out.println(turn);
        else
            System.out.println("Not Possible");
    }

}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python Program to count number of turns
# in a Binary Tree.

# A Binary Tree Node
class Node:
    def __init__(self):
        self.key = 0
        self.left = None
        self.right = None

# Utility function to create a new
# tree Node
def newNode(key: int) -> Node:
    temp = Node()
    temp.key = key
    temp.left = None
    temp.right = None
    return temp

# Utility function to find the LCA of
# two given values n1 and n2.
def findLCA(root: Node, n1: int, n2: int) -> Node:

    # Base case
    if root is None:
        return None

    # If either n1 or n2 matches with
    # root's key, report the presence by
    # returning root (Note that if a key
    # is ancestor of other, then the
    # ancestor key becomes LCA
    if root.key == n1 or root.key == n2:
        return root

    # Look for keys in left and right subtrees
    left_lca = findLCA(root.left, n1, n2)
    right_lca = findLCA(root.right, n1, n2)

    # If both of the above calls return
    # Non-NULL, then one key is present
    # in once subtree and other is present
    # in other, So this node is the LCA
    if left_lca and right_lca:
        return root

    # Otherwise check if left subtree or right
    # subtree is LCA
    return (left_lca if left_lca is not None else right_lca)

# function count number of turn need to reach
# given node from it's LCA we have two way to
def countTurn(root: Node, key: int, turn: bool) -> bool:
    global count
    if root is None:
        return False

    # if found the key value in tree
    if root.key == key:
        return True

    # Case 1:
    if turn is True:
        if countTurn(root.left, key, turn):
            return True
        if countTurn(root.right, key, not turn):
            count += 1
            return True

    # Case 2:
    else:
        if countTurn(root.right, key, turn):
            return True
        if countTurn(root.left, key, not turn):
            count += 1
            return True
    return False

# Function to find nodes common to given two nodes
def numberOfTurn(root: Node, first: int, second: int) -> int:
    global count
    LCA = findLCA(root, first, second)

    # there is no path between these two node
    if LCA is None:
        return -1

    count = 0

    # case 1:
    if LCA.key != first and LCA.key != second:

        # count number of turns needs to reached
        # the second node from LCA
        if countTurn(LCA.right, second, False) or countTurn(
                LCA.left, second, True):
            pass

        # count number of turns needs to reached
        # the first node from LCA
        if countTurn(LCA.left, first, True) or countTurn(
                LCA.right, first, False):
            pass
        return count + 1

    # case 2:
    if LCA.key == first:

        # count number of turns needs to reached
        # the second node from LCA
        countTurn(LCA.right, second, False)
        countTurn(LCA.left, second, True)
        return count
    else:

        # count number of turns needs to reached
        # the first node from LCA1
        countTurn(LCA.right, first, False)
        countTurn(LCA.left, first, True)
        return count

# Driver Code
if __name__ == "__main__":
    count = 0

    # Let us create binary tree given in the above
    # example
    root = Node()
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(6)
    root.right.right = newNode(7)
    root.left.left.left = newNode(8)
    root.right.left.left = newNode(9)
    root.right.left.right = newNode(10)

    turn = numberOfTurn(root, 5, 10)
    if turn:
        print(turn)
    else:
        print("Not possible")

# This code is contributed by
# sanjeev2552
```

## C#

```
using System;

//A C# Program to count number of turns
//in a Binary Tree.
public class Turns_to_reach_another_node
{

    // making Count global such that it can get
    // modified by different methods
    public static int Count;

    // A Binary Tree Node
    public class Node
    {
        public Node left, right;
        public int key;

        // Constructor
        public Node(int key)
        {
            this.key = key;
            left = null;
            right = null;
        }
    }

    // Utility function to find the LCA of
    // two given values n1 and n2.
    public static Node findLCA(Node root, int n1, int n2)
    {
        // Base case
        if (root == null)
        {
            return null;
        }

        // If either n1 or n2 matches with
        // root's key, report the presence by
        // returning root (Note that if a key
        // is ancestor of other, then the
        // ancestor key becomes LCA
        if (root.key == n1 || root.key == n2)
        {
            return root;
        }

        // Look for keys in left and right subtrees
        Node left_lca = findLCA(root.left, n1, n2);
        Node right_lca = findLCA(root.right, n1, n2);

        // If both of the above calls return
        // Non-NULL, then one key is present
        // in once subtree and other is present
        // in other, So this node is the LCA
        if (left_lca != null && right_lca != null)
        {
            return root;
        }

        // Otherwise check if left subtree or right
        // subtree is LCA
        return (left_lca != null) ? left_lca : right_lca;
    }

    // function count number of turn need to reach
    // given node from it's LCA we have two way to
    public static bool CountTurn(Node root, int key, bool turn)
    {
        if (root == null)
        {
            return false;
        }

        // if found the key value in tree
        if (root.key == key)
        {
            return true;
        }

        // Case 1:
        if (turn == true)
        {
            if (CountTurn(root.left, key, turn))
            {
                return true;
            }
            if (CountTurn(root.right, key, !turn))
            {
                Count += 1;
                return true;
            }
        }
        else // Case 2:
        {
            if (CountTurn(root.right, key, turn))
            {
                return true;
            }
            if (CountTurn(root.left, key, !turn))
            {
                Count += 1;
                return true;
            }
        }
        return false;
    }

    // Function to find nodes common to given two nodes
    public static int NumberOfTurn(Node root, int first, int second)
    {
        Node LCA = findLCA(root, first, second);

        // there is no path between these two node
        if (LCA == null)
        {
            return -1;
        }
        Count = 0;

        // case 1:
        if (LCA.key != first && LCA.key != second)
        {

            // count number of turns needs to reached
            // the second node from LCA
            if (CountTurn(LCA.right, second, false)
                || CountTurn(LCA.left, second, true))
            {
                ;
            }

            // count number of turns needs to reached
            // the first node from LCA
            if (CountTurn(LCA.left, first, true)
                || CountTurn(LCA.right, first, false))
            {
                ;
            }
            return Count + 1;
        }

        // case 2:
        if (LCA.key == first)
        {

            // count number of turns needs to reached
            // the second node from LCA
            CountTurn(LCA.right, second, false);
            CountTurn(LCA.left, second, true);
            return Count;
        }
        else
        {

            // count number of turns needs to reached
            // the first node from LCA1
            CountTurn(LCA.right, first, false);
            CountTurn(LCA.left, first, true);
            return Count;
        }
    }

    // Driver program to test above functions
    public static void Main(string[] args)
    {
        // Let us create binary tree given in the above
        // example
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);
        root.left.left.left = new Node(8);
        root.right.left.left = new Node(9);
        root.right.left.right = new Node(10);

        int turn = 0;
        if ((turn = NumberOfTurn(root, 5, 10)) != 0)
        {
            Console.WriteLine(turn);
        }
        else
        {
            Console.WriteLine("Not Possible");
        }
    }

}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    //A Javascript Program to count number of turns
    //in a Binary Tree.

    // making Count global such that it can get
    // modified by different methods
    let Count;

    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    // Utility function to find the LCA of
    // two given values n1 and n2.
    function findLCA(root, n1, n2) {
        // Base case
        if (root == null)
            return null;

        // If either n1 or n2 matches with
        // root's key, report the presence by
        // returning root (Note that if a key
        // is ancestor of other, then the
        // ancestor key becomes LCA
        if (root.key == n1 || root.key == n2)
            return root;

        // Look for keys in left and right subtrees
        let left_lca = findLCA(root.left, n1, n2);
        let right_lca = findLCA(root.right, n1, n2);

        // If both of the above calls return
        // Non-NULL, then one key is present
        // in once subtree and other is present
        // in other, So this node is the LCA
        if (left_lca != null && right_lca != null)
            return root;

        // Otherwise check if left subtree or right
        // subtree is LCA
        return (left_lca != null) ? left_lca : right_lca;
    }

    // function count number of turn need to reach
    // given node from it's LCA we have two way to
    function CountTurn(root, key, turn) {
        if (root == null)
            return false;

        // if found the key value in tree
        if (root.key == key)
            return true;

        // Case 1:
        if (turn == true) {
            if (CountTurn(root.left, key, turn))
                return true;
            if (CountTurn(root.right, key, !turn)) {
                Count += 1;
                return true;
            }
        } else // Case 2:
        {
            if (CountTurn(root.right, key, turn))
                return true;
            if (CountTurn(root.left, key, !turn)) {
                Count += 1;
                return true;
            }
        }
        return false;
    }

    // Function to find nodes common to given two nodes
    function NumberOfTurn(root, first, second) {
        let LCA = findLCA(root, first, second);

        // there is no path between these two node
        if (LCA == null)
            return -1;
        Count = 0;

        // case 1:
        if (LCA.key != first && LCA.key != second) {

            // count number of turns needs to reached
            // the second node from LCA
            if (CountTurn(LCA.right, second, false)
                    || CountTurn(LCA.left, second, true))
                ;

            // count number of turns needs to reached
            // the first node from LCA
            if (CountTurn(LCA.left, first, true)
                    || CountTurn(LCA.right, first, false))
                ;
            return Count + 1;
        }

        // case 2:
        if (LCA.key == first) {

            // count number of turns needs to reached
            // the second node from LCA
            CountTurn(LCA.right, second, false);
            CountTurn(LCA.left, second, true);
            return Count;
        } else {

            // count number of turns needs to reached
            // the first node from LCA1
            CountTurn(LCA.right, first, false);
            CountTurn(LCA.left, first, true);
            return Count;
        }
    }

    // Let us create binary tree given in the above
    // example
    let root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.left = new Node(6);
    root.right.right = new Node(7);
    root.left.left.left = new Node(8);
    root.right.left.left = new Node(9);
    root.right.left.right = new Node(10);

    let turn = 0;
    if ((turn = NumberOfTurn(root, 5, 10)) != 0)
      document.write(turn);
    else
      document.write("Not Possible");

 // This code is contributed by suresh07.
</script>
```

**Output**

```
4
```

**时间复杂度:** O(n)

**备选方案:**

我们必须按部就班。

1.  求给定两个节点的生命周期评价
2.  在字符串 S1 和 S2 中存储从 LCA 开始的两个节点的路径，如果我们必须在从 LCA 开始的路径中左转到该节点，则存储**‘l’**，如果我们在从 LCA 开始的路径中右转，则存储“r”。
3.  反转其中一个字符串并连接两个字符串。
4.  计算结果字符串中不等于其相邻字符的时间字符数。

## C++

```
// C++ Program to count number of turns
// in a Binary Tree.
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    struct Node* left, *right;
    int key;
};

// Utility function to create a new
// tree Node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

//Preorder traversal to store l or r in the string traversing
//from LCA to the given node key
void findPath(struct Node* root, int d,string str,string &s){
    if(root==NULL){
        return;
    }

    if(root->key==d){
        s=str;
        return;
    }
    findPath(root->left,d,str+"l",s);
    findPath(root->right,d,str+"r",s);
}

// Utility function to find the LCA of
// two given values n1 and n2.
struct Node* findLCAUtil(struct Node* root, int n1, int n2,bool&v1,bool&v2){
    // Base case
    if (root == NULL)
        return NULL;

    if (root->key == n1){
        v1=true;
        return root;
    }
    if(root->key == n2){
        v2=true;
        return root;
    }
    // Look for keys in left and right subtrees
    Node* left_lca = findLCAUtil(root->left, n1, n2,v1,v2);
    Node* right_lca = findLCAUtil(root->right, n1, n2,v1,v2);
    if (left_lca && right_lca){
        return root;
    }
    return (left_lca != NULL) ? left_lca : right_lca;
}

bool find(Node* root, int x){
    if(root==NULL){
        return false;
    }
    if((root->key==x) || find(root->left,x) || find(root->right,x)){
        return true;
    }
    return false;
}

//Function should return LCA of two nodes if both nodes are
//present otherwise should return NULL
Node* findLCA(struct Node* root, int first, int second){
    bool v1=false;
    bool v2=false;
    Node* lca = findLCAUtil(root,first,second,v1,v2);
    if((v1&&v2) || (v1&&find(lca,second)) || (v2&&find(lca,first))){
        return lca;
    }
    return NULL;
}

// function should return the number of turns required to go from
//first node to second node
int NumberOFTurns(struct Node* root, int first, int second){
  // base cases if root is not present or both node values are same
    if(root==NULL || (first==second)){
        return 0;
    }

    string s1 ="";
    string s2 = "";
    Node* lca = findLCA(root,first,second);

    findPath(lca,first,"",s1);
    findPath(lca,second,"",s2);
    if(s1.length()==0 && s2.length()==0){
       return -1;
    }
    reverse(s1.begin(),s1.end());
    s1+=s2;

    int cnt=0;
    bool flag=false;
    for(int i=0; i<(s1.length()-1); i++){
        if(s1[i]!=s1[i+1]){
            flag=true;
            cnt+=1;
        }
    }
    if(!flag){
       return -1;
    }
    return cnt;
}

// Driver program to test above functions
int main()
{
    // Let us create binary tree given in the above
    // example
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->left->left = newNode(8);
    root->right->left->left = newNode(9);
    root->right->left->right = newNode(10);

    int turn = 0;
    if ((turn = NumberOFTurns(root, 5, 10))!=-1)
        cout << turn << endl;
    else
        cout << "Not Possible" << endl;

    return 0;
}
```

**Output**

```
4
```

**时间复杂度** : O(n)

本文由 [**尼尚·辛格**](https://www.facebook.com/nishant.chaudhary.7334) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
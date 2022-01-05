# 移除类属树或 N 元树的所有叶节点

> 原文:[https://www . geesforgeks . org/从通用树或 n 元树中移除所有叶节点/](https://www.geeksforgeeks.org/remove-all-leaf-nodes-from-a-generic-tree-or-n-ary-tree/)

给定一个**类属树**，任务是**从**树**中删除**叶节点。

**示例:**

```
Input: 
              5
          /  /  \  \
         1   2   3   8
        /   / \   \
       15  4   5   6 

Output:  
5 : 1 2 3
1 :
2 :
3 :

Explanation: 
Deleted leafs are:
8, 15, 4, 5, 6

Input:      
              8
         /    |    \
       9      7       2
     / | \    |    / / | \ \
    4  5 6    10  11 1 2  2 3
Output:  
8: 9 7 2
9:
7:
2:
```

**方法:**按照下面给出的步骤解决问题

*   考虑一个返回更新树的根的函数。
*   遍历树并检查条件:
*   如果根为空，则返回空。
*   如果根本身是叶，则删除根并返回空值。
*   移动到其子节点上如果子节点是叶子，则
    *   删除该节点并更新子向量。
*   递归调用每个孩子。

下面是上述方法的实现:

## C++

```
// C++ program to delete the
// leaf from the generic tree

#include <bits/stdc++.h>
using namespace std;

// a treenode class
class TreeNode {
public:
    int data;
    vector<TreeNode*> children;

    TreeNode(int data)
    {
        this->data = data;
    }
};

// Recursive function which delete
// the leaf from tree

TreeNode* deleteleafnodes(TreeNode* root){
    if(root==NULL)return NULL;     //if root is NULL return NULL
    if(root->children.size()==0){  //if root itself is leaf then return NULL
        delete root;
        return NULL;
    }
    for(int i=0;i<root->children.size();i++){//moving onto its children
        TreeNode* child=root->children[i];
        if(child->children.size()==0){       // if leaf then delete that node
            delete child;
            for(int j=i;j<root->children.size()-1;j++){// update the children vector as well
                root->children[j]=root->children[j+1];
            }
            root->children.pop_back();
            i--;
        }
    }
    for(int i=0;i<root->children.size();i++){  //recursive call
        root->children[i]=deleteleafnodes(root->children[i]);
    }
    return root;
}

// Function which will print the
// tree level wise
void printTheTree(TreeNode* root)
{
    if (root == NULL)
        return;

    cout << root->data << " "
         << ":";
    for (int i = 0;
         i < root->children.size();
         i++)
        cout << root->children[i]->data

             << " ";
    cout << endl;

    for (int i = 0;
         i < root->children.size();
         i++)
        printTheTree(root->children[i]);
}

// Driver code
int main()
{
    // 5
    //      / / \ \
    // 1  2  3  8
    //    /   /\  \
    // 15  4  5  6

    TreeNode* root = new TreeNode(5);
    TreeNode* child1 = new TreeNode(1);
    root->children.push_back(child1);
    TreeNode* child11 = new TreeNode(15);
    child1->children.push_back(child11);
    TreeNode* child2 = new TreeNode(2);
    root->children.push_back(child2);
    TreeNode* child21 = new TreeNode(4);
    TreeNode* child22 = new TreeNode(5);
    child2->children.push_back(child21);
    child2->children.push_back(child22);
    TreeNode* child3 = new TreeNode(3);
    root->children.push_back(child3);
    TreeNode* child31 = new TreeNode(6);
    child3->children.push_back(child31);
    TreeNode* child4 = new TreeNode(8);
    root->children.push_back(child4);

    TreeNode* temp=deleteleafnodes(root);
    printTheTree(temp);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to delete the
// leaf from the generic tree
import java.util.*;

class GFG
{

// a treenode class
static class TreeNode {

    int data;
    ArrayList<TreeNode> children;

    TreeNode(int data)
    {
        this.data = data;
        this.children = new ArrayList<>();
    }
};

// Recursive function which delete
// the leaf from tree
static TreeNode removeLeaf(TreeNode root)
{   if(root==null){ return null;}// if root is null return null
    if(root.children.size()==0){// if root itself is leaf return null
     return null;}
    // if root.children is a leaf node
    // then delete it from children vector
    for (int i = 0; i < root.children.size(); i++) {

        TreeNode child= root.children.get(i);

        // if it is  a leaf
        if (child.children.size() == 0) {

            // shifting the vector to left
            // after the point i
            for (int j = i; j < root.children.size() - 1; j++)
                root.children.set(j, root.children.get(j + 1));

            // delete the last element
            root.children.remove(root.children.size()-1);

            i--;
        }
    }

    // Remove all leaf node
    // of children of root
    for (int i = 0;
         i < root.children.size();
         i++) {

        // call function for root.children
        root.children.set(i,removeLeaf(root.children.get(i)));
    }
 return root;
}

// Function which will print the
// tree level wise
static void printTheTree(TreeNode root)
{
    if (root == null)
        return;

    System.out.print(root.data+" :");

    for (int i = 0; i < root.children.size(); i++)
        System.out.print(root.children.get(i).data+" ");

    System.out.println();

    for (int i = 0; i < root.children.size(); i++)
        printTheTree(root.children.get(i));
}

// Driver code
public static void main(String []args)
{
    //     5
    //  / / \ \
    // 1  2  3  8
    //   /   /\  \
    // 15  4  5  6

    TreeNode root = new TreeNode(5);
    TreeNode child1 = new TreeNode(1);
    root.children.add(child1);
    TreeNode child11 = new TreeNode(15);
    child1.children.add(child11);
    TreeNode child2 = new TreeNode(2);
    root.children.add(child2);
    TreeNode child21 = new TreeNode(4);
    TreeNode child22 = new TreeNode(5);
    child2.children.add(child21);
    child2.children.add(child22);
    TreeNode child3 = new TreeNode(3);
    root.children.add(child3);
    TreeNode child31 = new TreeNode(6);
    child3.children.add(child31);
    TreeNode child4 = new TreeNode(8);
    root.children.add(child4);

    root=removeLeaf(root);
    printTheTree(root);
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python program to delete the
# leaf from the generic tree

# a treenode class
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.children = []

# Recursive function which delete
# the leaf from tree
def removeLeaf(root):
    if(root==None): return None #if root is None return None
    if(len(root.children)==0):return None #if root itself is leaf return None
    # if root.children is a leaf node
    # then delete it from children vector
    i = 0
    while i < len(root.children):
        child = root.children[i]

        # if it is  a leaf
        if (len(child.children) == 0):

            # shifting the vector to left
            # after the point i
            for j in range(i, len(root.children) - 1):
                root.children[j] = root.children[j + 1]

            # delete the last element
            root.children.pop()
            i -= 1
        i += 1

    # Remove all leaf node
    # of children of root
    for i in range(len(root.children)):

        # call function for root.children
        root.children[i]=removeLeaf(root.children[i])
    return root
# Function which will print the
# tree level wise
def printTheTree(root):
    if (root == None):
        return
    print("{} :".format(root.data), end="")
    for i in range(len(root.children)):
        print("{} ".format(root.children[i].data), end="")
    print()
    for i in range(len(root.children)):
        printTheTree(root.children[i])

# Driver code
if __name__ == "__main__":

    #         5
    #      / / \ \
    #    1  2  3  8
    #   /   /\  \
    #  15  4  5  6

    root = TreeNode(5)
    child1 = TreeNode(1)
    root.children.append(child1)
    child11 = TreeNode(15)
    child1.children.append(child11)
    child2 = TreeNode(2)
    root.children.append(child2)
    child21 = TreeNode(4)
    child22 = TreeNode(5)
    child2.children.append(child21)
    child2.children.append(child22)
    child3 = TreeNode(3)
    root.children.append(child3)
    child31 = TreeNode(6)
    child3.children.append(child31)
    child4 = TreeNode(8)
    root.children.append(child4)

    root=removeLeaf(root)
    printTheTree(root)

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to delete the
// leaf from the generic tree
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// a treenode class
public class TreeNode {

    public int data;
    public ArrayList children;

    public TreeNode(int data)
    {
        this.data = data;
        this.children = new ArrayList();
    }
};

// Recursive function which delete
// the leaf from tree
public static TreeNode removeLeaf(TreeNode root)
{   if(root==null) {return null;}//if root is null return null
    if(root.children.Count==0){//if root itself is leaf return null
     return null;}
    // if root.children is a leaf node
    // then delete it from children vector
    for (int i = 0; i < root.children.Count; i++) {

        TreeNode child= (TreeNode)root.children[i];

        // if it is  a leaf
        if (child.children.Count == 0) {

            // shifting the vector to left
            // after the point i
            for (int j = i; j < root.children.Count - 1; j++)
            {
                root.children[j]= root.children[j + 1];
            }

            // delete the last element
            root.children.RemoveAt(root.children.Count - 1);

            i--;
        }
    }

    // Remove all leaf node
    // of children of root
    for (int i = 0; i < root.children.Count; i++)
    {
        // call function for root.children
        root.children[i]=removeLeaf((TreeNode)root.children[i]);
    }
 return root;
}

// Function which will print the
// tree level wise
static void printTheTree(TreeNode root)
{
    if (root == null)
        return;

    Console.Write(root.data+" :");

    for (int i = 0; i < root.children.Count; i++)
        Console.Write(((TreeNode)root.children[i]).data + " ");

    Console.WriteLine();

    for (int i = 0; i < root.children.Count; i++)
        printTheTree((TreeNode)root.children[i]);
}

// Driver code
public static void Main(string []args)
{
    //     5
    //  / / \ \
    // 1  2  3  8
    //   /   /\  \
    // 15  4  5  6

    TreeNode root = new TreeNode(5);
    TreeNode child1 = new TreeNode(1);
    root.children.Add(child1);
    TreeNode child11 = new TreeNode(15);
    child1.children.Add(child11);
    TreeNode child2 = new TreeNode(2);
    root.children.Add(child2);
    TreeNode child21 = new TreeNode(4);
    TreeNode child22 = new TreeNode(5);
    child2.children.Add(child21);
    child2.children.Add(child22);
    TreeNode child3 = new TreeNode(3);
    root.children.Add(child3);
    TreeNode child31 = new TreeNode(6);
    child3.children.Add(child31);
    TreeNode child4 = new TreeNode(8);
    root.children.Add(child4);

    root=removeLeaf(root);
    printTheTree(root);
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

// Javascript program to delete the
// leaf from the generic tree

// a treenode class
class TreeNode {

    constructor(data)
    {
        this.data = data;
        this.children = []
    }
};

// Recursive function which delete
// the leaf from tree
function removeLeaf(root)
{
    if(root==null){
        return null;
    } //if root is null return null
    if(root.children.length==0){
        //if root itself is leaf return null
         return null;
    }
    // if root.children is a leaf node
    // then delete it from children vector
    for (var i = 0; i < root.children.length; i++) {

        var child= root.children[i];

        // if it is  a leaf
        if (child.children.length == 0) {

            // shifting the vector to left
            // after the point i
            for (var j = i; j < root.children.length - 1; j++)
            {
                root.children[j]= root.children[j + 1];
            }

            // delete the last element
            root.children.pop();

            i--;
        }
    }

    // Remove all leaf node
    // of children of root
    for (var i = 0; i < root.children.length; i++)
    {
        // call function for root.children
        root.children[i]=removeLeaf(root.children[i]);
    }
     return root;
}

// Function which will print the
// tree level wise
function printTheTree(root)
{
    if (root == null)
        return;

    document.write(root.data+" :");

    for (var i = 0; i < root.children.length; i++)
        document.write((root.children[i]).data + " ");

    document.write("<br>");

    for (var i = 0; i < root.children.length; i++)
        printTheTree(root.children[i]);
}

// Driver code
//     5
//  / / \ \
// 1  2  3  8
//   /   /\  \
// 15  4  5  6

var root = new TreeNode(5);
var child1 = new TreeNode(1);
root.children.push(child1);
var child11 = new TreeNode(15);
child1.children.push(child11);
var child2 = new TreeNode(2);
root.children.push(child2);
var child21 = new TreeNode(4);
var child22 = new TreeNode(5);
child2.children.push(child21);
child2.children.push(child22);
var child3 = new TreeNode(3);
root.children.push(child3);
var child31 = new TreeNode(6);
child3.children.push(child31);
var child4 = new TreeNode(8);
root.children.push(child4);

root=removeLeaf(root);
printTheTree(root);

</script>
```

**Output:** 

```
5 :1 2 3 
1 :
2 :
3 :
```

***时间复杂度:** O(N)*
***辅助空间** : O(N)*
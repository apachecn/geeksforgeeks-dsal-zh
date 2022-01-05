# N 元树的迭代预序遍历

> 原文:[https://www . geeksforgeeks . org/迭代-前序-遍历-a-n-ary-tree/](https://www.geeksforgeeks.org/iterative-preorder-traversal-of-a-n-ary-tree/)

给定一棵 K 元树。任务是编写一个迭代程序来执行给定 n 元树的[前序遍历](https://www.geeksforgeeks.org/iterative-preorder-traversal/)。

**示例:**

```
Input: 3-Array Tree  
                   1
                 / | \
                /  |   \
              2    3     4
             / \       / | \
            5    6    7  8  9
           /   / | \ 
          10  11 12 13

Output: 1 2 5 10 6 11 12 13 3 4 7 8 9

Input:  3-Array Tree
                   1
                 / | \
                /  |   \
              2    3     4
             / \       / | \
            5    6    7  8  9

Output: 1 2 5 6 3 4 7 8 9
```

N 元树的前序遍历类似于二叉查找树树或二叉树的前序遍历，唯一不同的是，父树的所有子节点都是按顺序从左向右遍历的。
[二叉树的迭代前序遍历](https://www.geeksforgeeks.org/iterative-preorder-traversal/)。

**遍历期间要处理的情况:**在这个迭代预序遍历算法中已经处理了两种情况:

1.  从堆栈中弹出顶部节点–从堆栈中弹出顶部节点，并将其插入节点访问列表。
2.  将 Top 的所有子节点从右向左推入堆栈，因为从堆栈开始的遍历将以相反的顺序进行。结果，实现了正确的前序遍历。

**注意**:在下面的 python 实现中，使用了“出列”来实现堆栈，而不是列表，因为它具有高效的追加和弹出操作。

下面是上述方法的实现:

## C++

```
// C++ program for Iterative Preorder
// Traversal of N-ary Tree.
// Preorder{ Root, print children
// from left to right.
#include <bits/stdc++.h>
using namespace std;

// Node Structure of K-ary Tree
class NewNode {
public:
    int key;

    // All children are stored in a list
    vector<NewNode*> child;
    NewNode(int val)
        : key(val)
    {
    }
};

// Utility function to print the
// preorder of the given K-Ary Tree
void preorderTraversal(NewNode* root)
{
    stack<NewNode*> Stack;

    // 'Preorder'-> contains all the
    // visited nodes
    vector<int> Preorder;

    Stack.push(root);

    while (!Stack.empty()) {
        NewNode* temp = Stack.top();
        Stack.pop();
        // store the key in preorder vector(visited list)
        Preorder.push_back(temp->key);
        // Push all of the child nodes of temp into
        // the stack from right to left.
        for (int i = temp->child.size() - 1; i >= 0; i--) {
            Stack.push(temp->child[i]);
        }
    }
    for (auto i : Preorder) {
        cout << i << " ";
    }
    cout << endl;
}

// Driver Code
int main()
{

    // input nodes
    /*
             1
          /  |  \
         /   |   \
        2    3    4
       / \      / | \
      /   \    7  8  9
     5     6
    /    / | \
   10   11 12 13
    */

    NewNode* root = new NewNode(1);
    root->child.push_back(new NewNode(2));
    root->child.push_back(new NewNode(3));
    root->child.push_back(new NewNode(4));

    root->child[0]->child.push_back(new NewNode(5));
    root->child[0]->child[0]->child.push_back(
        new NewNode(10));
    root->child[0]->child.push_back(new NewNode(6));
    root->child[0]->child[1]->child.push_back(
        new NewNode(11));
    root->child[0]->child[1]->child.push_back(
        new NewNode(12));
    root->child[0]->child[1]->child.push_back(
        new NewNode(13));
    root->child[2]->child.push_back(new NewNode(7));
    root->child[2]->child.push_back(new NewNode(8));
    root->child[2]->child.push_back(new NewNode(9));

    preorderTraversal(root);
}

// This code is contributed by sarangiswastika5
```

## 蟒蛇 3

```
# Python3 program for Iterative Preorder
# Traversal of N-ary Tree.
# Preorder: Root, print children
# from left to right.

from collections import deque

# Node Structure of K-ary Tree
class NewNode():

    def __init__(self, val):
        self.key = val
        # all children are stored in a list
        self.child =[]

# Utility function to print the
# preorder of the given K-Ary Tree
def preorderTraversal(root):

    Stack = deque([])
    # 'Preorder'-> contains all the
    # visited nodes.
    Preorder =[]
    Preorder.append(root.key)
    Stack.append(root)
    while len(Stack)>0:
        # 'Flag' checks whether all the child
        # nodes have been visited.
        flag = 0
        # CASE 1- If Top of the stack is a leaf
        # node then remove it from the stack:
        if len((Stack[len(Stack)-1]).child)== 0:
            X = Stack.pop()
            # CASE 2- If Top of the stack is
            # Parent with children:
        else:
            Par = Stack[len(Stack)-1]
        # a)As soon as an unvisited child is 
        # found(left to right sequence),
        # Push it to Stack and Store it in 
        # Auxillary List(Marked Visited)
        # Start Again from Case-1, to explore
        # this newly visited child
        for i in range(0, len(Par.child)):
            if Par.child[i].key not in Preorder:
                flag = 1
                Stack.append(Par.child[i])
                Preorder.append(Par.child[i].key)
                break;
                # b)If all Child nodes from left to right
                # of a Parent have been visited
                # then remove the parent from the stack.
        if flag == 0:
            Stack.pop()
    print(Preorder)

# Execution Start From here
if __name__=='__main__':
# input nodes
                '''

                  1
               /  |  \
              /   |   \
             2    3    4
            / \      / | \
           /   \    7  8  9
          5     6    
         /    / | \ 
        10   11 12 13

                '''

root = NewNode(1)
root.child.append(NewNode(2))
root.child.append(NewNode(3))
root.child.append(NewNode(4)) 
root.child[0].child.append(NewNode(5)) 
root.child[0].child[0].child.append(NewNode(10)) 
root.child[0].child.append(NewNode(6)) 
root.child[0].child[1].child.append(NewNode(11))
root.child[0].child[1].child.append(NewNode(12))
root.child[0].child[1].child.append(NewNode(13)) 
root.child[2].child.append(NewNode(7))
root.child[2].child.append(NewNode(8))
root.child[2].child.append(NewNode(9))

preorderTraversal(root)
```

**Output:** 

```
[1, 2, 5, 10, 6, 11, 12, 13, 3, 4, 7, 8, 9]
```
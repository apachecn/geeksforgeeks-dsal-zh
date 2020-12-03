# 钻石树

> 原文： [https://www.geeksforgeeks.org/diamond-tree/](https://www.geeksforgeeks.org/diamond-tree/)

给定数字`K`，任务是创建树的菱形结构，该结构遵循以下两个条件：

1.  树的前 K 个级别应该是平衡的二叉树，节点的值应从 1 开始并从左到右递增。

2.  接下来的 K – 1 级应该通过合并每对节点及其总和作为子节点来形成菱形结构。

**示例**：

```
Input: K = 2
Output:
1 
2 3 
5
Explanation: 
Structre will look like
          1                            
        /   \    
       2     3     
        \   /
          5

For the given value k = 2
First, create a balanced
binary tree of level 2 
with a value starting from 1.
Then on level 3 merge both
the node with a node 
having value 2 + 3 = 5\.  

Input: K = 3
Output:
1 
2 3 
4 5 6 7 
9 13 
22
Explanation: 
Structre will look like
          1                            
        /   \    
      2       3     
     /  \    /  \               
    4    5  6    7
     \   /   \  /   
       9      13
        \    /
          22

Input: K = 4 
Output:
1 
2 3 
4 5 6 7 
8 9 10 11 12 13 14 15 
17 21 25 29 
38 54 
92
Explanation: 
Structre will look like
             1                            
        /        \    
      2            3     
     /  \        /    \               
    4    5       6      7
  /  \  /  \    / \    / \
  8   9 10  11 12  13 14  15
  \  /  \  /   \  /    \  / 
   17    21     25      29
     \  /         \    /
      38            54
        \          /
             92    

```

**方法**：

1.  首先使用[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)创建 [K 级平衡二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)，并给出从 1 开始并从左向右递增的值。

2.  现在开始通过使用级别顺序对两个节点求和来合并级别

3.  最后，打印二叉树的每个级别

下面是上述方法的实现：

## C++

```cpp

// C++ programm to create the diamond 
// like structre of Binary Tree 
// for a given value of K 

#include <bits/stdc++.h> 
using namespace std; 

// A Tree node 
struct Node { 
    int data; 
    Node* left; 
    Node* right; 
}; 

// Utility function to create a new node 
Node* createNewNode(int value) 
{ 
    Node* temp = NULL; 
    temp = new Node(); 
    temp->data = value; 
    temp->left = NULL; 
    temp->right = NULL; 
    return temp; 
} 

// Utility function to create the diamond 
// like structre of Binary tree 
void createStructreUtil(queue<Node*>& qu, 
                        int k) 
{ 
    int num = 1; 
    int level = k - 1; 

    // Run the outer while loop 
    // and create structre up to 
    // the k levels 
    while (level--) { 

        int qsize = qu.size(); 

        // Run inner while loop to 
        // create current level 
        while (qsize--) { 

            Node* temp = qu.front(); 
            qu.pop(); 
            num += 1; 

            // Create left child 
            temp->left = createNewNode(num); 
            num += 1; 

            // Create right child 
            temp->right = createNewNode(num); 

            // Push the left child into 
            // the queue 
            qu.push(temp->left); 

            // Push the right child into 
            // the queue 
            qu.push(temp->right); 
        } 
    } 
    num += 1; 

    // Run the while loop 
    while (qu.size() > 1) { 

        // Pop first element from the queue 
        Node* first = qu.front(); 
        qu.pop(); 

        // Pop second element from the queue 
        Node* second = qu.front(); 
        qu.pop(); 

        // Create diamond structre 
        first->right 
            = createNewNode(first->data 
                            + second->data); 
        second->left = first->right; 

        // Push the node into the queue 
        qu.push(first->right); 
    } 
} 

// Function to print the Diamond 
// Structre of Binary Tree 
void printLevelOrder(Node* root, int k) 
{ 
    // Base Case 
    if (root == NULL) 
        return; 

    // Create an empty queue 
    queue<Node*> qu; 

    // Enqueue Root and initialize height 
    qu.push(root); 
    int level = k - 1; 

    // while loop to print the element 
    // up to the (k - 1) levels 
    while (level--) { 

        int qsize = qu.size(); 
        while (qsize--) { 

            Node* temp = qu.front(); 
            qu.pop(); 
            cout << temp->data << " "; 

            // Enqueue left child 
            if (temp->left != NULL) 
                qu.push(temp->left); 

            // Enqueue right child 
            if (temp->right != NULL) 
                qu.push(temp->right); 
        } 
        cout << endl; 
    } 

    // Loop to print the element 
    // rest all level except last 
    // level 
    while (qu.size() > 1) { 

        int qsize = qu.size(); 
        while (qsize) { 

            Node* first = qu.front(); 
            qu.pop(); 
            Node* second = qu.front(); 
            qu.pop(); 
            cout << first->data << " "
                 << second->data << " "; 
            qu.push(first->right); 
            qsize = qsize - 2; 
        } 
        cout << endl; 
    } 

    // Print the last element 
    Node* first = qu.front(); 
    qu.pop(); 
    cout << first->data << endl; 
} 

// Function to create the 
// structre 
void createStructre(int k) 
{ 
    queue<Node*> qu; 
    Node* root = createNewNode(1); 
    qu.push(root); 

    // Utility Function call to 
    // create structre 
    createStructreUtil(qu, k); 
    printLevelOrder(root, k); 
} 

// Driver code 
int main() 
{ 
    int k = 4; 

    // Print Structre 
    createStructre(k); 
} 

```
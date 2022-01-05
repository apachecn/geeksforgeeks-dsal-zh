# 通过在每个级别排列节点值来获得最大可能数量

> 原文:[https://www . geeksforgeeks . org/每级排列节点值的最大可能数量/](https://www.geeksforgeeks.org/largest-number-possible-by-arranging-node-values-at-each-level/)

给定一个在每个节点都有正值的二叉树，任务是打印通过在每个级别排列节点可以形成的最大数量。

**例:**

```
Input:                4
                    /   \
                   2    59
                  / \   / \
                 1   3  2  6
Output: 
Maximum number at 0'th level is 4
Maximum number at 1'st level is 592
Maximum number at 2'nd level is 6321

Input:           1
               /   \
              2     3
             / \     \
            4   5     8
                     /  \
                    6    79  
Output:
Explanation :
The maximum number at the 0'th level is 1
The maximum number at 1'st level is 32
The maximum number at 2'nd level is 854
The maximum number at 3'rd level is 796
```

**方法:**

*   Use [level sequential traversal](https://www.geeksforgeeks.org/level-order-tree-traversal/) to traverse all nodes of each level one by one.
*   Store their values in a string vector.
*   Use [comparison method](https://www.geeksforgeeks.org/given-an-array-of-numbers-arrange-the-numbers-to-form-the-biggest-number/) to sort the vectors to generate as many numbers as possible.
*   Display numbers and repeat all levels of procedures.

下面的代码是上述方法的实现:

## c++

```
// C++ program to find maximum number
// possible from nodes at each level.
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node representation */
struct Node {
    int data;
    struct Node *left, *right;
};

int myCompare(string X, string Y)
{
    // first append Y at the end of X
    string XY = X.append(Y);

    // then append X at the end of Y
    string YX = Y.append(X);

    // Now see which of the two formed numbers is greater
    return XY.compare(YX) > 0 ? 1 : 0;
}

// Function to print the largest value
// from the vector of strings
void printLargest(vector<string> arr)
{
    // Sort the numbers using comparison function
    // myCompare() to compare two strings.
    // Refer http:// www.cplusplus.com/reference/algorithm/sort/
    sort(arr.begin(), arr.end(), myCompare);

    for (int i = 0; i < arr.size(); i++)
        cout << arr[i];

    cout << "\n";
}

// Function to return the maximum number
// possible from nodes at each level
// using level order traversal
int maxLevelNumber(struct Node* root)
{
    // Base case
    if (root == NULL)
        return 0;

    // Initialize result
    int result = root->data;

    // Level Order Traversal
    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {

        // Get the size of the queue for the level
        int count = q.size();
        vector<string> v;
        // Iterate over all the nodes
        while (count--) {

            // Dequeue nodes from queue
            Node* temp = q.front();
            q.pop();

            // push that node to vector
            v.push_back(to_string(temp->data));
            // Push left and right nodes to queue
            // if present
            if (temp->left != NULL)
                q.push(temp->left);
            if (temp->right != NULL)
                q.push(temp->right);
        }

        // Print the maximum number at that level
        printLargest(v);
    }

    return result;
}

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Driver code
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(8);
    root->right->right->left = newNode(6);
    root->right->right->right = newNode(7);

   /* Constructed Binary tree is:
            1
           / \
          2   3
         / \   \
        4   5   8
               / \
               6 7              */
    maxLevelNumber(root);
    return 0;
}
```

## Java

```
// Java program to find maximum number
// possible from nodes at each level
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Node structure
static class node
{
    int data;
    node left = null;
    node right = null;
}

// Creates and initialize a new node
static node newNode(int ch)
{

    // Allocating memory to a new node
    node n = new node();
    n.data = ch;
    n.left = null;
    n.right = null;
    return n;
}

// Function to print the largest value
// from the vector of strings
static void printLargest(ArrayList<String> arr)
{

    // Sort the numbers using comparison function
    // myCompare() to compare two strings.
    // Refer http:// www.cplusplus.com/reference/algorithm/sort/
    Collections.sort(arr,new Comparator<>()
    {
        public int compare(String X, String Y)
        {

            // First append Y at the end of X
            String XY = X + Y;

            // Then append X at the end of Y
            String YX = Y + X;

            // Now see which of the two
            // formed numbers is greater
            return XY.compareTo(YX) > 0 ? -1 : 1;
       }
    });

    for(int i = 0; i < arr.size(); i++)
        System.out.print(arr.get(i));

    System.out.println();
}

// Function to return the maximum number
// possible from nodes at each level
// using level order traversal
static int maxLevelNumber(node root)
{

    // Base case
    if (root == null)
        return 0;

    // Initialize result
    int result = root.data;

    // Level Order Traversal
    Queue<node> q = new LinkedList<>();
    q.add(root);

    while (!q.isEmpty())
    {

        // Get the size of the queue
        // for the level
        int count = q.size();
        ArrayList<String> v = new ArrayList<>();

        // Iterate over all the nodes
        while (count-->0)
        {

            // Dequeue nodes from queue
            node temp = q.peek();
            q.poll();

            // push that node to vector
            v.add(Integer.toString(temp.data));

            // Push left and right nodes to queue
            // if present
            if (temp.left != null)
                q.add(temp.left);
            if (temp.right != null)
                q.add(temp.right);
        }

        // Print the maximum number at that level
        printLargest(v);
    }
    return result;
}

// Driver code
public static void main (String[] args)
{
    node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(8);
    root.right.right.left = newNode(6);
    root.right.right.right = newNode(7);

    /* Constructed Binary tree is:
            1
           / \
          2   3
         / \   \
        4   5   8
               / \
              6   7 */
    maxLevelNumber(root);
}
}

// This code is contributed by offbeat
```

**输出:**

```
1
32
854
76
```
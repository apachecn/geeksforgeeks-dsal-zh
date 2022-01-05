# 检查值是否存在于等级排序的完整二叉树中

> 原文:[https://www . geesforgeks . org/check-if-value-in-level-order-sorted-complete-二叉树/](https://www.geeksforgeeks.org/check-if-value-exists-in-level-order-sorted-complete-binary-tree/)

给定一个级别顺序排序的完整二叉树，任务是检查其中是否存在一个键。一个**完整的二叉树**有每一层，除了可能是最后一层，完全填充，所有节点尽可能的靠左。

**示例:**

```
             7
          /     \
         10      15
       /   \    /  \
      17   20  30  35
     / \   /     
    40 41 50      
Input: Node = 3
Output: No

Input: Node = 7
Output: Yes

Input: Node = 30
Output: Yes
```

**接近**一个简单的 **O(n)** 解决方案是完全遍历树并检查键值。然而，我们可以利用树被排序的信息，并且在时间复杂度方面做得更好。

*   找出密钥可能存在的级别。从根节点开始，一直向左，直到遇到大于键值的值**。如果密钥存在于树中，则在此之前的级别将包含密钥。让我们假设这是水平 *l* 。**
*   现在，在 *l* 的节点上执行**二分搜索法**。与传统的二分搜索法不同，这个级别的节点不能直接访问。然而，从根到该级别中每个节点的**路径**可以使用二进制逻辑进行编码。例如，考虑示例树中的第三级。它最多可以包含 2 <sup>3</sup> = 8 个节点。这些节点可以通过向左、向左、向左从根节点到达；或者向左，向左，向右；等等。如果左边用 <sup>0</sup> 表示，右边用 <sup>1</sup> 表示，那么到达该级别节点的可能方式可以编码为*arr*=【000，001，010，011，100，101，110，111】。
*   不过这个数组不需要创建，递归选择中间索引，简单生成这个索引的 *l* 位格雷码就可以应用二分搜索法(参考这篇[文章](https://www.geeksforgeeks.org/generate-n-bit-gray-codes-set-2/))。
*   如果路径不完整，只需检查数组的左边部分。例如，编码路径 011 不对应于样本树中的任何值。由于树是完整的，它确保右边不再有元素。
*   如果找到密钥，返回 true，否则返回 false。

下面是上述方法的实现:

## C++14

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std; 

/* Class containing left and right 
child of current node and key value*/
class Node 
{
    public :
    int data;
    Node *left, *right;

    Node(int item)
    {
        data = item;
        left = right = NULL;
    }
};

/* Function to locate which level to check
for the existence of key. */
int findLevel(Node *root, int data)
{

    // If the key is less than the root,
    // it will certainly not exist in the tree
    // because tree is level-order sorted
    if (data < root->data)
        return -1;

    // If the key is equal to the root then
    // simply return 0 (zero'th level)
    if (data == root->data)
        return 0;

    int cur_level = 0;

    while (true) 
    {
        cur_level++;
        root = root->left;

        // If the key is found in any leftmost element
        // then simply return true
        // No need for any extra searching
        if (root->data == data)
            return -2;

        // If key lies between the root data and
        // the left child's data OR if key is greater
        // than root data and there is no level
        // underneath it, return the current level
        if (root->data < data
            && (root->left == NULL
            || root->left->data > data)) 
        {
            break;
        }
    }

    return cur_level;
}

/* Function to traverse a binary
encoded path and return the value
encountered after traversal. */
int traversePath(Node *root,vector<int> path)
{
    for (int i = 0; i < path.size(); i++) 
    {
        int direction = path[i];

        // Go left
        if (direction == 0) 
        {

            // Incomplete path
            if (root->left == NULL)
                return -1;
            root = root->left;
        }

        // Go right
        else 
        {

            // Incomplete path
            if (root->right == NULL)
                return -1;
            root = root->right;
        }
    }

    // Return the data at the node
    return root->data;
}

/* Function to generate gray code of 
corresponding binary number of integer i */
vector<int> generateGray(int n, int x)
{

    // Create new arraylist to store
    // the gray code
    vector<int> gray ;

    int i = 0;
    while (x > 0)
    {
        gray.push_back(x % 2);
        x = x / 2;
        i++;
    }

    // Reverse the encoding till here
    reverse(gray.begin(),gray.end());

    // Leftmost digits are filled with 0
    for (int j = 0; j < n - i; j++)
        gray.insert(gray.begin(), 0);

    return gray;
}

/* Function to search the key in a 
particular level of the tree. */
bool binarySearch(Node *root, int start,
                    int end, int data,
                    int level)
{
    if (end >= start) 
    {

        // Find the middle index
        int mid = (start + end) / 2;

        // Encode path from root to this index
        // in the form of 0s and 1s where
        // 0 means LEFT and 1 means RIGHT
        vector<int> encoding = generateGray(level, mid);

        // Traverse the path in the tree
        // and check if the key is found
        int element_found = traversePath(root, encoding);

        // If path is incomplete
        if (element_found == -1)

            // Check the left part of the level
            return binarySearch(root, start,
                                mid - 1, data, level);

        if (element_found == data)
            return true;

        // Check the right part of the level
        if (element_found < data)
            return binarySearch(root, mid + 1, 
                                end, data, level);

        // Check the left part of the level
        else
            return binarySearch(root, start, 
                                mid - 1, data, level);
    }

    // Key not found in that level
    return false;
}

// Function that returns true if the
// key is found in the tree
bool findKey(Node *root, int data)
{
    // Find the level where the key may lie
    int level = findLevel(root, data);

    // If level is -1 then return false
    if (level == -1)
        return false;

    // If level is -2 i.e. key was found in any
    // leftmost element then simply return true
    if (level == -2)
        return true;

    // Apply binary search on the elements
    // of that level
    return binarySearch(root, 0, (int)pow(2, level) -
                        1, data, level);
}

// Driver code
int main()
{
    /* Consider the following level-order sorted tree

                    5
                / \ 
                8     10 
                / \ / \
            13 23 25 30
            / \ /
            32 40 50 
    */

    Node* root = new Node(5);
    root->left = new Node(8);
    root->right = new Node(10);
    root->left->left = new Node(13);
    root->left->right = new Node(23);
    root->right->left = new Node(25);
    root->right->right = new Node(30);
    root->left->left->left = new Node(32);
    root->left->left->right = new Node(40);
    root->left->right->left = new Node(50);

    // Keys to be searched
    int arr[] = { 5, 8, 9 };
    int n = sizeof(arr)/sizeof(int);

    for (int i = 0; i < n; i++)
    {
        if (findKey(root, arr[i]))
            cout << ("Yes") << endl;
        else
            cout << ("No") << endl;
    }
}

// This code is contributed by Arnab Kundu

```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.io.*;

/* Class containing left and right 
child of current node and key value*/
class Node {
    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class GFG {

    /* Function to locate which level to check
    for the existence of key. */
    public static int findLevel(Node root, int data)
    {

        // If the key is less than the root,
        // it will certainly not exist in the tree
        // because tree is level-order sorted
        if (data < root.data)
            return -1;

        // If the key is equal to the root then
        // simply return 0 (zero'th level)
        if (data == root.data)
            return 0;

        int cur_level = 0;

        while (true) {
            cur_level++;
            root = root.left;

            // If the key is found in any leftmost element
            // then simply return true
            // No need for any extra searching
            if (root.data == data)
                return -2;

            // If key lies between the root data and
            // the left child's data OR if key is greater
            // than root data and there is no level
            // underneath it, return the current level
            if (root.data < data
                && (root.left == null
                    || root.left.data > data)) {
                break;
            }
        }

        return cur_level;
    }

    /* Function to traverse a binary
    encoded path and return the value
    encountered after traversal. */
    public static int traversePath(Node root,
                                   ArrayList<Integer> path)
    {
        for (int i = 0; i < path.size(); i++) {
            int direction = path.get(i);

            // Go left
            if (direction == 0) {

                // Incomplete path
                if (root.left == null)
                    return -1;
                root = root.left;
            }

            // Go right
            else {

                // Incomplete path
                if (root.right == null)
                    return -1;
                root = root.right;
            }
        }

        // Return the data at the node
        return root.data;
    }

    /* Function to generate gray code of 
    corresponding binary number of integer i */
    static ArrayList<Integer> generateGray(int n, int x)
    {

        // Create new arraylist to store
        // the gray code
        ArrayList<Integer> gray = new ArrayList<Integer>();

        int i = 0;
        while (x > 0) {
            gray.add(x % 2);
            x = x / 2;
            i++;
        }

        // Reverse the encoding till here
        Collections.reverse(gray);

        // Leftmost digits are filled with 0
        for (int j = 0; j < n - i; j++)
            gray.add(0, 0);

        return gray;
    }

    /* Function to search the key in a 
    particular level of the tree. */
    public static boolean binarySearch(Node root,
                                       int start,
                                       int end,
                                       int data,
                                       int level)
    {
        if (end >= start) {

            // Find the middle index
            int mid = (start + end) / 2;

            // Encode path from root to this index
            // in the form of 0s and 1s where
            // 0 means LEFT and 1 means RIGHT
            ArrayList<Integer> encoding = generateGray(level, mid);

            // Traverse the path in the tree
            // and check if the key is found
            int element_found = traversePath(root, encoding);

            // If path is incomplete
            if (element_found == -1)

                // Check the left part of the level
                return binarySearch(root, start, mid - 1, data, level);

            if (element_found == data)
                return true;

            // Check the right part of the level
            if (element_found < data)
                return binarySearch(root, mid + 1, end, data, level);

            // Check the left part of the level
            else
                return binarySearch(root, start, mid - 1, data, level);
        }

        // Key not found in that level
        return false;
    }

    // Function that returns true if the
    // key is found in the tree
    public static boolean findKey(Node root, int data)
    {
        // Find the level where the key may lie
        int level = findLevel(root, data);

        // If level is -1 then return false
        if (level == -1)
            return false;

        // If level is -2 i.e. key was found in any
        // leftmost element then simply return true
        if (level == -2)
            return true;

        // Apply binary search on the elements
        // of that level
        return binarySearch(root, 0, (int)Math.pow(2, level) - 1, data, level);
    }

    // Driver code
    public static void main(String[] args)
    {
        /* Consider the following level-order sorted tree

                          5
                       /    \ 
                      8      10 
                    /  \    /  \
                  13    23 25   30
                 / \   /
                32 40 50 
        */

        Node root = new Node(5);
        root.left = new Node(8);
        root.right = new Node(10);
        root.left.left = new Node(13);
        root.left.right = new Node(23);
        root.right.left = new Node(25);
        root.right.right = new Node(30);
        root.left.left.left = new Node(32);
        root.left.left.right = new Node(40);
        root.left.right.left = new Node(50);

        // Keys to be searched
        int arr[] = { 5, 8, 9 };
        int n = arr.length;

        for (int i = 0; i < n; i++) {
            if (findKey(root, arr[i]))
                System.out.println("Yes");
            else
                System.out.println("No");
        }
    }
}

```

## 蟒蛇 3

```
# Python3 implementation of the approach
from sys import maxsize
from collections import deque

INT_MIN = -maxsize

# Class containing left and right
# child of current node and key value
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function to locate which level to check
# for the existence of key.
def findLevel(root: Node, data: int) -> int:

    # If the key is less than the root,
    # it will certainly not exist in the tree
    # because tree is level-order sorted
    if (data < root.data):
        return -1

    # If the key is equal to the root then
    # simply return 0 (zero'th level)
    if (data == root.data):
        return 0

    cur_level = 0

    while True:

        cur_level += 1
        root = root.left

        # If the key is found in any leftmost
        # element then simply return true
        # No need for any extra searching
        if (root.data == data):
            return -2

        # If key lies between the root data and
        # the left child's data OR if key is greater
        # than root data and there is no level
        # underneath it, return the current level
        if (root.data < data and 
           (root.left == None or
            root.left.data > data)):
            break

    return cur_level

# Function to traverse a binary
# encoded path and return the value
# encountered after traversal.
def traversePath(root: Node, path: list) -> int:

    for i in range(len(path)):
        direction = path[i]

        # Go left
        if (direction == 0):

            # Incomplete path
            if (root.left == None):
                return -1

            root = root.left

        # Go right
        else:

            # Incomplete path
            if (root.right == None):
                return -1

            root = root.right

    # Return the data at the node
    return root.data

# Function to generate gray code of
# corresponding binary number of integer i
def generateGray(n: int, x: int) -> list:

    # Create new arraylist to store
    # the gray code
    gray = []

    i = 0
    while (x > 0):
        gray.append(x % 2)
        x = x / 2
        i += 1

    # Reverse the encoding till here
    gray.reverse()

    # Leftmost digits are filled with 0
    for j in range(n - i):
        gray.insert(0, gray[0])

    return gray

# Function to search the key in a
# particular level of the tree.
def binarySearch(root: Node, start: int,
                  end: int, data: int,
                level: int) -> bool:

    if (end >= start):

        # Find the middle index
        mid = (start + end) / 2

        # Encode path from root to this index
        # in the form of 0s and 1s where
        # 0 means LEFT and 1 means RIGHT
        encoding = generateGray(level, mid)

        # Traverse the path in the tree
        # and check if the key is found
        element_found = traversePath(root, encoding)

        # If path is incomplete
        if (element_found == -1):

            # Check the left part of the level
            return binarySearch(root, start, 
                                mid - 1, data,
                                level)

        if (element_found == data):
            return True

        # Check the right part of the level
        if (element_found < data):
            return binarySearch(root, mid + 1, 
                                end, data, level)

        # Check the left part of the level
        else:
            return binarySearch(root, start, 
                                mid - 1, data,
                                level)

    # Key not found in that level
    return False

# Function that returns true if the
# key is found in the tree
def findKey(root: Node, data: int) -> bool:

    # Find the level where the key may lie
    level = findLevel(root, data)

    # If level is -1 then return false
    if (level == -1):
        return False

    # If level is -2 i.e. key was found in any
    # leftmost element then simply return true
    if (level == -2):
        return True

    # Apply binary search on the elements
    # of that level
    return binarySearch(root, 0, 
                        int(pow(2, level) - 1),
                        data, level)

# Driver code
if __name__ == "__main__":

    # Consider the following level 
    # order sorted tree
    '''

                5
               /  \ 
              8    10 
            /  \  /  \
           13  23 25  30
          / \  /
        32  40 50 
    '''

    root = Node(5)
    root.left = Node(8)
    root.right = Node(10)
    root.left.left = Node(13)
    root.left.right = Node(23)
    root.right.left = Node(25)
    root.right.right = Node(30)
    root.left.left.left = Node(32)
    root.left.left.right = Node(40)
    root.left.right.left = Node(50)

    # Keys to be searched
    arr = [ 5, 8, 9 ]
    n = len(arr)

    for i in range(n):
        if (findKey(root, arr[i])):
            print("Yes")
        else:
            print("No")

# This code is contributed by sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Collections.Generic;

/* Class containing left and right 
child of current node and key value*/
class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class GFG{

/* Function to locate which level to check
for the existence of key. */
public static int findLevel(Node root, int data)
{

    // If the key is less than the root,
    // it will certainly not exist in the tree
    // because tree is level-order sorted
    if (data < root.data)
        return -1;

    // If the key is equal to the root then
    // simply return 0 (zero'th level)
    if (data == root.data)
        return 0;

    int cur_level = 0;

    while (true)
    {
        cur_level++;
        root = root.left;

        // If the key is found in any leftmost element
        // then simply return true
        // No need for any extra searching
        if (root.data == data)
            return -2;

        // If key lies between the root data and
        // the left child's data OR if key is greater
        // than root data and there is no level
        // underneath it, return the current level
        if (root.data < data && (root.left == null || 
            root.left.data > data))
        {
            break;
        }
    }
    return cur_level;
}

/* Function to traverse a binary
encoded path and return the value
encountered after traversal. */
public static int traversePath(Node root, List<int> path)
{
    for(int i = 0; i < path.Count; i++)
    {
        int direction = path[i];

        // Go left
        if (direction == 0)
        {

            // Incomplete path
            if (root.left == null)
                return -1;

            root = root.left;
        }

        // Go right
        else
        {

            // Incomplete path
            if (root.right == null)
                return -1;

            root = root.right;
        }
    }

    // Return the data at the node
    return root.data;
}

/* Function to generate gray code of 
corresponding binary number of integer i */
static List<int> generateGray(int n, int x)
{

    // Create new arraylist to store
    // the gray code
    List<int> gray = new List<int>();

    int i = 0;
    while (x > 0)
    {
        gray.Add(x % 2);
        x = x / 2;
        i++;
    }

    // Reverse the encoding till here
    gray.Reverse();

    // Leftmost digits are filled with 0
    for(int j = 0; j < n - i; j++)
        gray.Insert(0, 0);

    return gray;
}

/* Function to search the key in a 
particular level of the tree. */
public static bool binarySearch(Node root, int start,
                                int end, int data,
                                int level)
{
    if (end >= start)
    {

        // Find the middle index
        int mid = (start + end) / 2;

        // Encode path from root to this index
        // in the form of 0s and 1s where
        // 0 means LEFT and 1 means RIGHT
        List<int> encoding = generateGray(level, mid);

        // Traverse the path in the tree
        // and check if the key is found
        int element_found = traversePath(root, encoding);

        // If path is incomplete
        if (element_found == -1)

            // Check the left part of the level
            return binarySearch(root, start, mid - 1, 
                                data, level);

        if (element_found == data)
            return true;

        // Check the right part of the level
        if (element_found < data)
            return binarySearch(root, mid + 1, end,
                                data, level);

        // Check the left part of the level
        else
            return binarySearch(root, start, mid - 1, 
                                data, level);
    }

    // Key not found in that level
    return false;
}

// Function that returns true if the
// key is found in the tree
public static bool findKey(Node root, int data)
{

    // Find the level where the key may lie
    int level = findLevel(root, data);

    // If level is -1 then return false
    if (level == -1)
        return false;

    // If level is -2 i.e. key was found in any
    // leftmost element then simply return true
    if (level == -2)
        return true;

    // Apply binary search on the elements
    // of that level
    return binarySearch(root, 0, (int)Math.Pow(2, level) - 1,
                        data, level);
}

// Driver code
static void Main()
{

    /* Consider the following level-order sorted tree

                      5
                   /    \ 
                  8      10 
                /  \    /  \
              13    23 25   30
             / \   /
            32 40 50 
    */
    Node root = new Node(5);
    root.left = new Node(8);
    root.right = new Node(10);
    root.left.left = new Node(13);
    root.left.right = new Node(23);
    root.right.left = new Node(25);
    root.right.right = new Node(30);
    root.left.left.left = new Node(32);
    root.left.left.right = new Node(40);
    root.left.right.left = new Node(50);

    // Keys to be searched
    int []arr = { 5, 8, 9 };
    int n = arr.Length;

    for(int i = 0; i < n; i++) 
    {
        if (findKey(root, arr[i]))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

      // JavaScript implementation of the approach

      /* Class containing left and right
      child of current node and key value*/
      class Node {
          constructor(item) {
             this.left = null;
             this.right = null;
             this.data = item;
          }
      }

      /* Function to locate which level to check
        for the existence of key. */
      function findLevel(root, data)
      {

        // If the key is less than the root,
        // it will certainly not exist in the tree
        // because tree is level-order sorted
        if (data < root.data)
          return -1;

        // If the key is equal to the root then
        // simply return 0 (zero'th level)
        if (data == root.data)
          return 0;

        let cur_level = 0;

        while (true) {
          cur_level++;
          root = root.left;

          // If the key is found in any leftmost element
          // then simply return true
          // No need for any extra searching
          if (root.data == data)
            return -2;

          // If key lies between the root data and
          // the left child's data OR if key is greater
          // than root data and there is no level
          // underneath it, return the current level
          if (root.data < data
              && (root.left == null
                  || root.left.data > data)) {
            break;
          }
        }

        return cur_level;
      }

      /* Function to traverse a binary
        encoded path and return the value
        encountered after traversal. */
      function traversePath(root, path)
      {
        for (let i = 0; i < path.length; i++) {
          let direction = path[i];

          // Go left
          if (direction == 0) {

            // Incomplete path
            if (root.left == null)
              return -1;
            root = root.left;
          }

          // Go right
          else {

            // Incomplete path
            if (root.right == null)
              return -1;
            root = root.right;
          }
        }

        // Return the data at the node
        return root.data;
      }

      /* Function to generate gray code of
        corresponding binary number of integer i */
      function generateGray(n, x)
      {

        // Create new arraylist to store
        // the gray code
        let gray = [];

        let i = 0;
        while (x > 0) {
          gray.push(x % 2);
          x = parseInt(x / 2, 10);
          i++;
        }

        // Reverse the encoding till here
        gray.reverse();

        // Leftmost digits are filled with 0
        for (let j = 0; j < n - i; j++)
          gray.push(0, 0);

        return gray;
      }

      /* Function to search the key in a
            particular level of the tree. */
      function binarySearch(root, start, end, data, level)
      {
        if (end >= start) {

          // Find the middle index
          let mid = parseInt((start + end) / 2, 10);

          // Encode path from root to this index
          // in the form of 0s and 1s where
          // 0 means LEFT and 1 means RIGHT
          let encoding = generateGray(level, mid);

          // Traverse the path in the tree
          // and check if the key is found
          let element_found = traversePath(root, encoding);

          // If path is incomplete
          if (element_found == -1)

            // Check the left part of the level
            return binarySearch(root, start, mid - 1, data, level);

          if (element_found == data)
            return true;

          // Check the right part of the level
          if (element_found < data)
            return binarySearch(root, mid + 1, end, data, level);

          // Check the left part of the level
          else
            return binarySearch(root, start, mid - 1, data, level);
        }

        // Key not found in that level
        return false;
      }

      // Function that returns true if the
      // key is found in the tree
      function findKey(root, data)
      {
        // Find the level where the key may lie
        let level = findLevel(root, data);

        // If level is -1 then return false
        if (level == -1)
          return false;

        // If level is -2 i.e. key was found in any
        // leftmost element then simply return true
        if (level == -2)
          return true;

        // Apply binary search on the elements
        // of that level
        return binarySearch(root, 0, 
        Math.pow(2, level) - 1, data, level);
      }

      /* Consider the following level-order sorted tree

                                    5
                                 /    \
                                8      10
                              /  \    /  \
                            13    23 25   30
                           / \   /
                          32 40 50
                  */

      let root = new Node(5);
      root.left = new Node(8);
      root.right = new Node(10);
      root.left.left = new Node(13);
      root.left.right = new Node(23);
      root.right.left = new Node(25);
      root.right.right = new Node(30);
      root.left.left.left = new Node(32);
      root.left.left.right = new Node(40);
      root.left.right.left = new Node(50);

      // Keys to be searched
      let arr = [ 5, 8, 9 ];
      let n = arr.length;

      for (let i = 0; i < n; i++) {
        if (findKey(root, arr[i]))
          document.write("Yes" + "<br>");
        else
          document.write("No" + "<br>");
      }

</script>
```

**Output:** 

```
Yes
Yes
No
```

**时间复杂度**:等级可以在 O(logn)时间内找到。遍历任意路径执行二分搜索法的时间为 0(logn)。此外，在最坏的情况下，该级别最多可以有 n/2 个节点。
因此，执行搜索的时间复杂度变为 o(logn)* o(log(n/2))=**o(logn)^2**。
**辅助空间** : O(1)。
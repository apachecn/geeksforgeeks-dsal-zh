# 使用递归的二叉树的仰视图

> 原文:[https://www . geeksforgeeks . org/使用递归的二叉树底部视图/](https://www.geeksforgeeks.org/bottom-view-of-a-binary-tree-using-recursion/)

给定一棵二叉树，任务是使用递归找到二叉树的底部视图。

**示例:**

```
Input:
1 
  \
    2
      \
        4
       /  \
      3    5
Output: 1 3 4 5

Input:
        20
      /    \
    8       22
  /   \    /   \
5      10 21     25
      / \      
    9    14

Output: 5 9 21 14 25
```

**方法:**
我们可以通过使用递归和 2 个数组来实现，每个数组的大小为 2n+1(最坏的情况)，其中 n =给定树中的元素数量。这里，我们取一个变量 x，它决定了它的水平距离。设 x 是节点的水平距离。现在，左边孩子的水平距离为 x-1(x 减 1)，右边孩子的水平距离为 x+1(x 加 1)。将另一个变量“p”作为决定该元素属于哪个级别的优先级。

```
    1 (x=0, p=0)
      \
        2 (x=1, p=1)
          \
            4 (x=2, p=2)
          /  \
(x=1, p=3) 3     5 (x=3, p=3)
```

当以右->节点->左的方式遍历树时，为每个节点分配 x 和 p，如果数组在位置(mid+x)为空，则同时插入第一个数组中节点的数据。如果阵列不为空，并且具有较高优先级(p)的节点用该节点的数据作为位置(mid+x)来更新阵列。为了更好地理解，第二个数组将保持第一个数组校验码中每个插入节点的优先级(p)。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    // left and right references
    Node *left, *right;
    // Constructor of tree Node
    Node(int key)
    {
        data = key;
        left = right = NULL;
    }
};

int l = 0, r = 0;
int N;

// Function to generate
// bottom view of
// binary tree
void Bottom(Node* root, int arr[], int arr2[], int x, int p, int mid)
{
    // Base case
    if (root == NULL) {
        return;
    }

    if (x < l) {
        // To store leftmost
        // value of x in l
        l = x;
    }

    // To store rightmost
    // value of x in r
    if (x > r) {
        r = x;
    }

    // To check if arr
    // is empty at mid+x
    if (arr[mid + x] == INT_MIN) {
        // Insert data of Node
        // at arr[mid+x]
        arr[mid + x] = root->data;
        // Insert priority of
        // that Node at arr2[mid+x]
        arr2[mid + x] = p;
    }

    // If not empty and priotiy
    // of previously inserted
    // Node is less than current*/
    else if (arr2[mid + x] < p) {
        // Insert current
        // Node data at arr[mid+x]
        arr[mid + x] = root->data;

        // Insert priotiy of
        // that Node at arr2[mid +x]
        arr2[mid + x] = p;
    }

    // Go right first
    // then left
    Bottom(root->right, arr, arr2, x + 1, p + 1, mid);
    Bottom(root->left, arr, arr2, x - 1, p + 1, mid);
}

// Utility function
// to generate bottom
// view of a biany tree
void bottomView(struct Node* root)
{
    int arr[2 * N + 1];
    int arr2[2 * N + 1];

    for (int i = 0; i < 2 * N + 1; i++) {
        arr[i] = INT_MIN;
        arr2[i] = INT_MIN;
    }

    int mid = N, x = 0, p = 0;

    Bottom(root, arr, arr2, x, p, mid);

    for (int i = mid + l; i <= mid + r; i++) {
        cout << arr[i] << " ";
    }
}

// Driver code
int main()
{

    N = 5;
    Node* root = new Node(1);
    root->right = new Node(2);
    root->right->right = new Node(4);
    root->right->right->left = new Node(3);
    root->right->right->right = new Node(5);

    bottomView(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG{

static class Node
{
    int data;

    // left and right references
    Node left, right;

    // Constructor of tree Node
    public Node(int key)
    {
        data = key;
        left = right = null;
    }
};

static int l = 0, r = 0, N;

// Function to generate
// bottom view of binary tree
static void Bottom(Node root, int arr[],
                  int arr2[], int x,
                       int p, int mid)
{

    // Base case
    if (root == null)
    {
        return;
    }

    if (x < l)
    {

        // To store leftmost
        // value of x in l
        l = x;
    }

    // To store rightmost
    // value of x in r
    if (x > r)
    {
        r = x;
    }

    // To check if arr
    // is empty at mid+x
    if (arr[mid + x] == Integer.MIN_VALUE)
    {

        // Insert data of Node
        // at arr[mid+x]
        arr[mid + x] = root.data;

        // Insert priority of
        // that Node at arr2[mid+x]
        arr2[mid + x] = p;
    }

    // If not empty and priotiy
    // of previously inserted
    // Node is less than current*/
    else if (arr2[mid + x] < p)
    {

        // Insert current
        // Node data at arr[mid+x]
        arr[mid + x] = root.data;

        // Insert priotiy of
        // that Node at arr2[mid +x]
        arr2[mid + x] = p;
    }

    // Go right first
    // then left
    Bottom(root.right, arr, arr2,
           x + 1, p + 1, mid);
    Bottom(root.left, arr, arr2,
           x - 1, p + 1, mid);
}

// Utility function to generate
// bottom view of a biany tree
static void bottomView(Node root)
{
    int[] arr = new int[2 * N + 1];
    int[] arr2 = new int[2 * N + 1];

    for(int i = 0; i < 2 * N + 1; i++)
    {
        arr[i] = Integer.MIN_VALUE;
        arr2[i] = Integer.MIN_VALUE;
    }

    int mid = N, x = 0, p = 0;

    Bottom(root, arr, arr2, x, p, mid);

    for(int i = mid + l; i <= mid + r; i++)
    {
        System.out.print(arr[i] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    N = 5;

    Node root = new Node(1);
    root.right = new Node(2);
    root.right.right = new Node(4);
    root.right.right.left = new Node(3);
    root.right.right.right = new Node(5);

    bottomView(root);
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

l = 0
r = 0
INT_MIN = -(2**32)

# Function to generate
# bottom view of
# binary tree
def Bottom(root, arr, arr2, x, p, mid):
    global INT_MIN, l, r

    # Base case
    if (root == None):
        return

    if (x < l):

        # To store leftmost
        # value of x in l
        l = x

    # To store rightmost
    # value of x in r
    if (x > r):
        r = x

    # To check if arr
    # is empty at mid+x
    if (arr[mid + x] == INT_MIN):

        # Insert data of Node
        # at arr[mid+x]
        arr[mid + x] = root.data

        # Insert priority of
        # that Node at arr2[mid+x]
        arr2[mid + x] = p

    # If not empty and priotiy
    # of previously inserted
    # Node is less than current*/
    elif (arr2[mid + x] < p):

        # Insert current
        # Node data at arr[mid+x]
        arr[mid + x] = root.data

        # Insert priotiy of
        # that Node at arr2[mid +x]
        arr2[mid + x] = p

    # Go right first
    # then left
    Bottom(root.right, arr, arr2, x + 1, p + 1, mid)
    Bottom(root.left, arr, arr2, x - 1, p + 1, mid)

# Utility function
# to generate bottom
# view of a biany tree
def bottomView(root):
    global INT_MIN
    arr = [0]*(2 * N + 1)
    arr2 = [0]*(2 * N + 1)

    for i in range(2 * N + 1):
        arr[i] = INT_MIN
        arr2[i] = INT_MIN
    mid = N
    x = 0
    p = 0
    Bottom(root, arr, arr2, x, p, mid)

    for i in range(mid + l,mid + r + 1):
        print(arr[i], end = " ")

# Driver code
N = 5
root = Node(1)
root.right = Node(2)
root.right.right = Node(4)
root.right.right.left = Node(3)
root.right.right.right = Node(5)

bottomView(root)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
using System;

class GFG{

class Node{

public int data;

// left and right references
public Node left, right;

// Constructor of tree Node
public Node(int key)
{
    data = key;
    left = right = null;
}
};

static int l = 0, r = 0, N;

// Function to generate
// bottom view of binary tree
static void Bottom(Node root, int []arr,
                  int []arr2, int x,
                       int p, int mid)
{

    // Base case
    if (root == null)
    {
        return;
    }

    if (x < l)
    {

        // To store leftmost
        // value of x in l
        l = x;
    }

    // To store rightmost
    // value of x in r
    if (x > r)
    {
        r = x;
    }

    // To check if arr
    // is empty at mid+x
    if (arr[mid + x] == Int32.MinValue)
    {

        // Insert data of Node
        // at arr[mid+x]
        arr[mid + x] = root.data;

        // Insert priority of
        // that Node at arr2[mid+x]
        arr2[mid + x] = p;
    }

    // If not empty and priotiy
    // of previously inserted
    // Node is less than current*/
    else if (arr2[mid + x] < p)
    {

        // Insert current
        // Node data at arr[mid+x]
        arr[mid + x] = root.data;

        // Insert priotiy of
        // that Node at arr2[mid +x]
        arr2[mid + x] = p;
    }

    // Go right first
    // then left
    Bottom(root.right, arr, arr2,
           x + 1, p + 1, mid);
    Bottom(root.left, arr, arr2,
           x - 1, p + 1, mid);
}

// Utility function to generate
// bottom view of a biany tree
static void bottomView(Node root)
{
    int[] arr = new int[2 * N + 1];
    int[] arr2 = new int[2 * N + 1];

    for(int i = 0; i < 2 * N + 1; i++)
    {
        arr[i] = Int32.MinValue;
        arr2[i] = Int32.MinValue;
    }

    int mid = N, x = 0, p = 0;

    Bottom(root, arr, arr2, x, p, mid);

    for(int i = mid + l; i <= mid + r; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver code
public static void Main(string[] args)
{
    N = 5;

    Node root = new Node(1);
    root.right = new Node(2);
    root.right.right = new Node(4);
    root.right.right.left = new Node(3);
    root.right.right.right = new Node(5);

    bottomView(root);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

class Node{

    // Constructor of tree Node
    constructor(key)
    {
        this.data = key;
        this.left = null;
        this.right = null;
    }

};

var l = 0, r = 0, N;

// Function to generate
// bottom view of binary tree
function Bottom(root, arr, arr2, x, p, mid)
{

    // Base case
    if (root == null)
    {
        return;
    }

    if (x < l)
    {

        // To store leftmost
        // value of x in l
        l = x;
    }

    // To store rightmost
    // value of x in r
    if (x > r)
    {
        r = x;
    }

    // To check if arr
    // is empty at mid+x
    if (arr[mid + x] == -1000000000)
    {

        // Insert data of Node
        // at arr[mid+x]
        arr[mid + x] = root.data;

        // Insert priority of
        // that Node at arr2[mid+x]
        arr2[mid + x] = p;
    }

    // If not empty and priotiy
    // of previously inserted
    // Node is less than current*/
    else if (arr2[mid + x] < p)
    {

        // Insert current
        // Node data at arr[mid+x]
        arr[mid + x] = root.data;

        // Insert priotiy of
        // that Node at arr2[mid +x]
        arr2[mid + x] = p;
    }

    // Go right first
    // then left
    Bottom(root.right, arr, arr2,
           x + 1, p + 1, mid);
    Bottom(root.left, arr, arr2,
           x - 1, p + 1, mid);
}

// Utility function to generate
// bottom view of a biany tree
function bottomView(root)
{
    var arr = Array(2*N +1).fill(-1000000000);
    var arr2 = Array(2*N +1).fill(-1000000000);

    var mid = N, x = 0, p = 0;

    Bottom(root, arr, arr2, x, p, mid);

    for(var i = mid + l; i <= mid + r; i++)
    {
        document.write(arr[i] + " ");
    }
}

// Driver code
N = 5;

var root = new Node(1);
root.right = new Node(2);
root.right.right = new Node(4);
root.right.right.left = new Node(3);
root.right.right.right = new Node(5);
bottomView(root);

</script>
```

**Output:** 

```
1 3 4 5
```
# 找到给定步骤的阿尔法分数(使用 BST)

> 原文:[https://www . geeksforgeeks . org/find-the-alpha-score-of-the-给定步骤-using-bst/](https://www.geeksforgeeks.org/find-the-alpha-score-of-the-given-steps-using-bst/)

给定一个由表示写在 **N** 步上的数值的 **N** 个数字组成的数组**A【】**，任务是找出爬上所有楼梯的总路程的α分数。由于答案可能会很大，所以以 **10 <sup>9</sup> + 7** 为模打印答案。

> **阿尔法分数:**每一步的**阿尔法分数是先前在爬楼梯时看到的所有数字的总和，这些数字比当前楼梯上的数字小**。**
> **总路程的 alpha 分值是每一步的 alpha 分值之和。****

****示例:****

> ****输入:** A[] = {13，14，20}
> **输出:** 87
> **解释:**
> 第一级楼梯的 Alpha 评分= 13
> 第二级楼梯的 Alpha 评分= 13 + 14 = 27
> 第三级楼梯的 Alpha 评分= 13 + 14 + 20 = 47
> 所有 Alpha 评分之和=13 + 27 + 47 = 87
> 因此，Alpha**
> 
>  ****输入:** A[] = {10，11，12}
> **输出:** 64
> **解释:**
> 第一级楼梯的 Alpha 评分= 10
> 第二级楼梯的 Alpha 评分= 10 + 11 = 21
> 第三级楼梯的 Alpha 评分= 10+11 + 12 = 33
> 所有 Alpha 评分之和=10 + 21 + 33
> 因此**

****天真方法:**
解决问题最简单的方法是遍历数组中的每个元素，计算所有比当前元素小的元素在先前索引处的**和**，计算当前楼梯的 ***Alpha Score。***对于每一个计算出来的总和，更新 **total_sum** ( ***总路程的 Alpha Score***)。最后打印 **total_sum** 作为完整旅程的 Alpha Score。**

*****时间复杂度**:O(N<sup>2</sup>)*
***辅助空间** : O(1)***

****高效方法:**
上述方法可以使用[二分搜索法树](https://www.geeksforgeeks.org/binary-search-tree-data-structure/)进行优化。请遵循以下步骤:**

*   **[**排序**](https://www.geeksforgeeks.org/merge-sort/) 给定数组。**
*   **[从排序后的数组](https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/)中构建一个 BST。**
*   **递归遍历 **BST** 并遵循以下步骤:

    *   遍历**左子树。**
    *   将**当前节点**的值加到**总和** ( ***当前楼梯*** 的 Alpha 分数)并更新 **total_sum** ( ***到现在为止的路程的 Alpha 分数*** )。
    *   遍历**右子树。**** 
*   **完成 BST 遍历后，打印 **total_sum** 。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

static long sum = 0, total_sum = 0;
static long mod = 1000000007;

// Structure of a node
struct Node
{
    Node *left, *right;
    int data;

    Node(int x)
    {
        data = x;
        left = NULL;
        right = NULL;
    }
};

// Function to calculate and return
// the Alpha Score of the journey
long getAlphaScore(Node* node)
{

    // Traverse left subtree
    if (node->left != NULL)
        getAlphaScore(node->left);

    // Calculate the alpha score
    // of the current step
    sum = (sum + node->data) % mod;

    // Update alpha score of
    // the journey
    total_sum = (total_sum + sum) % mod;

    // Traverse right subtree
    if (node->right != NULL)
        getAlphaScore(node->right);

    // Return
    return total_sum;
}

// Function to construct a BST
// from the sorted array arr[]
Node* constructBST(int arr[], int start,
                   int end, Node* root)
{
    if (start > end)
        return NULL;

    int mid = (start + end) / 2;

    // Insert root
    if (root == NULL)
        root = new Node(arr[mid]);

    // Construct left subtree
    root->left = constructBST(arr, start,
                              mid - 1, root->left);

    // Construct right subtree
    root->right = constructBST(arr, mid + 1, end,
                               root->right);

    // Return root
    return root;
}

// Driver Code
int main()
{
    int arr[] = { 10, 11, 12 };
    int length = 3;

    // Sort the array
    sort(arr, arr + length);

    Node *root = NULL;

    // Construct BST from the sorted array
    root = constructBST(arr, 0, length - 1, root);

    cout << (getAlphaScore(root));
}

// This code is contributed by mohit kumar 29
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to implement
// the above approach
import java.lang.*;
import java.util.*;

// Structure of a node
class Node {
    Node left, right;
    int data;
    public Node(int data)
    {
        this.data = data;
        left = null;
        right = null;
    }
}

class AlphaScore {

    Node root;

    AlphaScore() { root = null; }

    static long sum = 0, total_sum = 0;
    static long mod = 1000000007;

    // Function to calculate and return
    // the Alpha Score of the journey
    public static long getAlphaScore(Node node)
    {
        // Traverse left subtree
        if (node.left != null)
            getAlphaScore(node.left);

        // Calculate the alpha score
        // of the current step
        sum = (sum + node.data) % mod;

        // Update alpha score of
        // the journey
        total_sum = (total_sum + sum) % mod;

        // Traverse right subtree
        if (node.right != null)
            getAlphaScore(node.right);

        // Return
        return total_sum;
    }

    // Function to construct a BST
    // from the sorted array arr[]
    public static Node constructBST(int[] arr, int start,
                                    int end, Node root)
    {
        if (start > end)
            return null;

        int mid = (start + end) / 2;

        // Insert root
        if (root == null)
            root = new Node(arr[mid]);

        // Construct left subtree
        root.left
            = constructBST(arr, start, mid - 1, root.left);

        // Construct right subtree
        root.right
            = constructBST(arr, mid + 1, end, root.right);

        // Return root
        return root;
    }

    // Driver Code
    public static void main(String args[])
    {

        int arr[] = { 10, 11, 12 };
        int length = arr.length;

        // Sort the array
        Arrays.sort(arr);

        Node root = null;

        // Construct BST from the sorted array
        root = constructBST(arr, 0, length - 1, root);

        System.out.println(getAlphaScore(root));
    }
}
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach

# Structure of a node
class Node:
    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

sum = 0
total_sum = 0
mod = 1000000007

# Function to calculate and return
# the Alpha Score of the journey
def getAlphaScore(node):

    global sum
    global total_sum

    # Traverse left subtree
    if node.left != None:
        getAlphaScore(node.left)

    # Calculate the alpha score
    # of the current step
    sum = (sum + node.data) % mod

    # Update alpha score of
    # the journey
    total_sum = (total_sum + sum) % mod

    # Traverse right subtree
    if node.right != None:
        getAlphaScore(node.right)

    # Return
    return total_sum

# Function to construct a BST
# from the sorted array arr[]
def constructBST(arr, start, end, root):

    if start > end:
        return None

    mid = (start + end) // 2

    # Insert root
    if root == None:
        root = Node(arr[mid])

    # Construct left subtree
    root.left = constructBST(arr, start,
                             mid - 1,
                             root.left)

    # Construct right subtree
    root.right = constructBST(arr, mid + 1,
                              end, root.right)

    # Return root
    return root

# Driver code
arr = [ 10, 11, 12 ]
length = len(arr)

# Sort the array
arr.sort()

root = None

# Construct BST from the sorted array
root = constructBST(arr, 0, length - 1, root)

print(getAlphaScore(root))

# This code is contributed by Shivam Singh
```

## **C#**

```
// C# program to implement
// the above approach
using System;

// Structure of a node
class Node
{
    public Node left, right;
    public int data;
    public Node(int data)
    {
        this.data = data;
        left = null;
        right = null;
    }
}

class AlphaScore{

Node root;

AlphaScore(){root = null;}

static long sum = 0, total_sum = 0;
static long mod = 1000000007;

// Function to calculate and return
// the Alpha Score of the journey
static long getAlphaScore(Node node)
{

    // Traverse left subtree
    if (node.left != null)
        getAlphaScore(node.left);

    // Calculate the alpha score
    // of the current step
    sum = (sum + node.data) % mod;

    // Update alpha score of
    // the journey
    total_sum = (total_sum + sum) % mod;

    // Traverse right subtree
    if (node.right != null)
        getAlphaScore(node.right);

    // Return
    return total_sum;
}

// Function to construct a BST
// from the sorted array []arr
static Node constructBST(int[] arr, int start,
                         int end, Node root)
{
    if (start > end)
        return null;

    int mid = (start + end) / 2;

    // Insert root
    if (root == null)
        root = new Node(arr[mid]);

    // Construct left subtree
    root.left = constructBST(arr, start,
                             mid - 1, root.left);

    // Construct right subtree
    root.right = constructBST(arr, mid + 1,
                              end, root.right);

    // Return root
    return root;
}

// Driver Code
public static void Main(String []args)
{

    int []arr = { 10, 11, 12 };
    int length = arr.Length;

    // Sort the array
    Array.Sort(arr);

    Node root = null;

    // Construct BST from the sorted array
    root = constructBST(arr, 0, length - 1, root);

    Console.WriteLine(getAlphaScore(root));
}
}

// This is code contributed by PrinciRaj1992
```

## **java 描述语言**

```
<script>

// Javascript program to implement
// the above approach

// Structure of a node
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

var root = null;

function AlphaScore(){root = null;}

var sum = 0, total_sum = 0;
var mod = 1000000007;

// Function to calculate and return
// the Alpha Score of the journey
function getAlphaScore(node)
{

    // Traverse left subtree
    if (node.left != null)
        getAlphaScore(node.left);

    // Calculate the alpha score
    // of the current step
    sum = (sum + node.data) % mod;

    // Update alpha score of
    // the journey
    total_sum = (total_sum + sum) % mod;

    // Traverse right subtree
    if (node.right != null)
        getAlphaScore(node.right);

    // Return
    return total_sum;
}

// Function to construct a BST
// from the sorted array []arr
function constructBST(arr, start, end, root)
{
    if (start > end)
        return null;

    var mid = parseInt((start + end) / 2);

    // Insert root
    if (root == null)
        root = new Node(arr[mid]);

    // Construct left subtree
    root.left = constructBST(arr, start,
                             mid - 1, root.left);

    // Construct right subtree
    root.right = constructBST(arr, mid + 1,
                              end, root.right);

    // Return root
    return root;
}

// Driver Code
var arr = [10, 11, 12];
var length = arr.length;

// Sort the array
arr.sort();
var root = null;

// Construct BST from the sorted array
root = constructBST(arr, 0, length - 1, root);
document.write(getAlphaScore(root));

// This code is contributed by rrrtnx.
</script>
```

****Output:** 

```
64
```** 

*****时间复杂度:** O(NlogN)*
***辅助空间** : O(N)***
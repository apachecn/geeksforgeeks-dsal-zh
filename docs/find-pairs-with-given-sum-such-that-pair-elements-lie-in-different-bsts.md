# 找到给定和的配对，使得配对元素位于不同的 BST 中

> 原文:[https://www . geesforgeks . org/find-pairs-with-given-sum-so-pair-elements-lie-in-different-bsts/](https://www.geeksforgeeks.org/find-pairs-with-given-sum-such-that-pair-elements-lie-in-different-bsts/)

给定两个[二分搜索法树(BST)](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/) 和一个给定的和。任务是找到具有给定和的对，使得每个对元素必须位于不同的 BST 中。
**例:**

```
Input : sum = 10
     8                    5
   /   \                /   \
  3     10             2    18
 /  \      \         /   \  
1    6      14      1     3
    / \     /              \  
   5   7   13              4          
Output : (5,5), (6,4), (7,3), (8,2)
In above pairs first element lies in first
BST and second element lies in second BST
```

这个问题的一个简单的解决方案是将一棵树的有序遍历存储在辅助数组中，然后从数组中一个接一个地选择元素，并在另一棵树中为给定的和找到它的对。如果两个树中的总节点相等，则该方法的时间复杂度为 0(n<sup>2</sup>)。
该解决方案的有效解决方案**是将两个 BST 的有序遍历存储在两个不同的辅助阵列中 **vect1[]** 和 vect2[]。现在我们按照[的**方法 1** 来做这篇](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)的文章。因为 BST 的有序遍历总是给出排序的序列，所以我们不需要对数组进行排序。** 

*   将迭代器**向左**移动，并将其指向左上角向量 t1[]。
*   向右取迭代器**并指向右下角向量 2[]。**
*   **现在如果**向量 11[左] +向量 2[右] <求和**，那么向前移动向量 1[]中的左迭代器，即；**左++** 。**
*   **现在如果**向量 1[左] +向量 2[右] >和**，则在向量[]中向后移动右迭代器，即；**右–**。**

**下面是上述想法的实现。** 

## **C++**

```
// C++ program to find pairs with given sum such
// that one element of pair exists in one BST and
// other in other BST.
#include<bits/stdc++.h>
using namespace std;

// A binary Tree node
struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to create a new BST node
// with key as given num
struct Node* newNode(int num)
{
    struct Node* temp = new Node;
    temp->data = num;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to insert a given key to BST
Node* insert(Node* root, int key)
{
    if (root == NULL)
        return newNode(key);
    if (root->data > key)
        root->left = insert(root->left, key);
    else
        root->right = insert(root->right, key);
    return root;
}

// store storeInorder traversal in auxiliary array
void storeInorder(Node *ptr, vector<int> &vect)
{
    if (ptr==NULL)
        return;
    storeInorder(ptr->left, vect);
    vect.push_back(ptr->data);
    storeInorder(ptr->right, vect);
}

// Function to find pair for given sum in different bst
// vect1[]  --> stores storeInorder traversal of first bst
// vect2[]  --> stores storeInorder traversal of second bst
void pairSumUtil(vector<int> &vect1, vector<int> &vect2,
                                                int sum)
{
    // Initialize two indexes to two different corners
    // of two vectors.
    int left = 0;
    int right = vect2.size() - 1;

    // find pair by moving two corners.
    while (left < vect1.size() && right >= 0)
    {
        // If we found a pair
        if (vect1[left] + vect2[right] == sum)
        {
            cout << "(" << vect1[left] << ", "
                 << vect2[right] << "), ";
            left++;
            right--;
        }

        // If sum is more, move to higher value in
        // first vector.
        else if (vect1[left] + vect2[right] < sum)
            left++;

        // If sum is less, move to lower value in
        // second vector.
        else
            right--;
    }
}

// Prints all pairs with given "sum" such that one
// element of pair is in tree with root1 and other
// node is in tree with root2.
void pairSum(Node *root1, Node *root2, int sum)
{
    // Store inorder traversals of two BSTs in two
    // vectors.
    vector<int> vect1, vect2;
    storeInorder(root1, vect1);
    storeInorder(root2, vect2);

    // Now the problem reduces to finding a pair
    // with given sum such that one element is in
    // vect1 and other is in vect2.
    pairSumUtil(vect1, vect2, sum);
}

// Driver program to run the case
int main()
{
    // first BST
    struct Node* root1 = NULL;
    root1 = insert(root1, 8);
    root1 = insert(root1, 10);
    root1 = insert(root1, 3);
    root1 = insert(root1, 6);
    root1 = insert(root1, 1);
    root1 = insert(root1, 5);
    root1 = insert(root1, 7);
    root1 = insert(root1, 14);
    root1 = insert(root1, 13);

    // second BST
    struct Node* root2 = NULL;
    root2 = insert(root2, 5);
    root2 = insert(root2, 18);
    root2 = insert(root2, 2);
    root2 = insert(root2, 1);
    root2 = insert(root2, 3);
    root2 = insert(root2, 4);

    int sum = 10;
    pairSum(root1, root2, sum);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find pairs with given sum such
// that one element of pair exists in one BST and
// other in other BST.
import java.util.*;
class solution
{

// A binary Tree node
static class Node
{
    int data;
     Node left, right;
};

// A utility function to create a new BST node
// with key as given num
static Node newNode(int num)
{
     Node temp = new Node();
    temp.data = num;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert a given key to BST
static Node insert(Node root, int key)
{
    if (root == null)
        return newNode(key);
    if (root.data > key)
        root.left = insert(root.left, key);
    else
        root.right = insert(root.right, key);
    return root;
}

// store storeInorder traversal in auxiliary array
static void storeInorder(Node ptr, Vector<Integer> vect)
{
    if (ptr==null)
        return;
    storeInorder(ptr.left, vect);
    vect.add(ptr.data);
    storeInorder(ptr.right, vect);
}

// Function to find pair for given sum in different bst
// vect1.get()  -. stores storeInorder traversal of first bst
// vect2.get()  -. stores storeInorder traversal of second bst
static void pairSumUtil(Vector<Integer> vect1, Vector<Integer> vect2,
                                                int sum)
{
    // Initialize two indexes to two different corners
    // of two Vectors.
    int left = 0;
    int right = vect2.size() - 1;

    // find pair by moving two corners.
    while (left < vect1.size() && right >= 0)
    {
        // If we found a pair
        if (vect1.get(left) + vect2.get(right) == sum)
        {
            System.out.print( "(" +vect1.get(left) + ", "+ vect2.get(right) + "), ");
            left++;
            right--;
        }

        // If sum is more, move to higher value in
        // first Vector.
        else if (vect1.get(left) + vect2.get(right) < sum)
            left++;

        // If sum is less, move to lower value in
        // second Vector.
        else
            right--;
    }
}

// Prints all pairs with given "sum" such that one
// element of pair is in tree with root1 and other
// node is in tree with root2.
static void pairSum(Node root1, Node root2, int sum)
{
    // Store inorder traversals of two BSTs in two
    // Vectors.
    Vector<Integer> vect1= new Vector<Integer>(), vect2= new Vector<Integer>();
    storeInorder(root1, vect1);
    storeInorder(root2, vect2);

    // Now the problem reduces to finding a pair
    // with given sum such that one element is in
    // vect1 and other is in vect2.
    pairSumUtil(vect1, vect2, sum);
}

// Driver program to run the case
public static void  main(String args[])
{
    // first BST
     Node root1 = null;
    root1 = insert(root1, 8);
    root1 = insert(root1, 10);
    root1 = insert(root1, 3);
    root1 = insert(root1, 6);
    root1 = insert(root1, 1);
    root1 = insert(root1, 5);
    root1 = insert(root1, 7);
    root1 = insert(root1, 14);
    root1 = insert(root1, 13);

    // second BST
     Node root2 = null;
    root2 = insert(root2, 5);
    root2 = insert(root2, 18);
    root2 = insert(root2, 2);
    root2 = insert(root2, 1);
    root2 = insert(root2, 3);
    root2 = insert(root2, 4);

    int sum = 10;
    pairSum(root1, root2, sum);
}
}
//contributed by Arnab Kundu
```

## **蟒蛇 3**

```
# Python3 program to find pairs with given
# sum such that one element of pair exists
# in one BST and other in other BST.

# A utility function to create a new
# BST node with key as given num
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# A utility function to insert a
# given key to BST
def insert(root, key):
    if root == None:
        return newNode(key)
    if root.data > key:
        root.left = insert(root.left, key)
    else:
        root.right = insert(root.right, key)
    return root

# store storeInorder traversal in
# auxiliary array
def storeInorder(ptr, vect):
    if ptr == None:
        return
    storeInorder(ptr.left, vect)
    vect.append(ptr.data)
    storeInorder(ptr.right, vect)

# Function to find pair for given
# sum in different bst
# vect1[] --> stores storeInorder traversal
#             of first bst
# vect2[] --> stores storeInorder traversal
#             of second bst
def pairSumUtil(vect1, vect2, Sum):

    # Initialize two indexes to two
    # different corners of two lists.
    left = 0
    right = len(vect2) - 1

    # find pair by moving two corners.
    while left < len(vect1) and right >= 0:

        # If we found a pair
        if vect1[left] + vect2[right] == Sum:
            print("(", vect1[left], ",",
                       vect2[right], "),", end = " ")
            left += 1
            right -= 1

        # If sum is more, move to higher
        # value in first lists.
        elif vect1[left] + vect2[right] < Sum:
            left += 1

        # If sum is less, move to lower
        # value in second lists.
        else:
            right -= 1

# Prints all pairs with given "sum" such that one
# element of pair is in tree with root1 and other
# node is in tree with root2.
def pairSum(root1, root2, Sum):

    # Store inorder traversals of
    # two BSTs in two lists.
    vect1 = []
    vect2 = []
    storeInorder(root1, vect1)
    storeInorder(root2, vect2)

    # Now the problem reduces to finding a
    # pair with given sum such that one 
    # element is in vect1 and other is in vect2.
    pairSumUtil(vect1, vect2, Sum)

# Driver Code
if __name__ == '__main__':

    # first BST
    root1 = None
    root1 = insert(root1, 8)
    root1 = insert(root1, 10)
    root1 = insert(root1, 3)
    root1 = insert(root1, 6)
    root1 = insert(root1, 1)
    root1 = insert(root1, 5)
    root1 = insert(root1, 7)
    root1 = insert(root1, 14)
    root1 = insert(root1, 13)

    # second BST
    root2 = None
    root2 = insert(root2, 5)
    root2 = insert(root2, 18)
    root2 = insert(root2, 2)
    root2 = insert(root2, 1)
    root2 = insert(root2, 3)
    root2 = insert(root2, 4)

    Sum = 10
    pairSum(root1, root2, Sum)

# This code is contributed by PranchalK
```

## **C#**

```
using System;
using System.Collections.Generic;

// C# program to find pairs with given sum such
// that one element of pair exists in one BST and
// other in other BST.
public class solution
{

// A binary Tree node
public class Node
{
    public int data;
     public Node left, right;
}

// A utility function to create a new BST node
// with key as given num
public static Node newNode(int num)
{
     Node temp = new Node();
    temp.data = num;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert a given key to BST
public static Node insert(Node root, int key)
{
    if (root == null)
    {
        return newNode(key);
    }
    if (root.data > key)
    {
        root.left = insert(root.left, key);
    }
    else
    {
        root.right = insert(root.right, key);
    }
    return root;
}

// store storeInorder traversal in auxiliary array
public static void storeInorder(Node ptr, List<int> vect)
{
    if (ptr == null)
    {
        return;
    }
    storeInorder(ptr.left, vect);
    vect.Add(ptr.data);
    storeInorder(ptr.right, vect);
}

// Function to find pair for given sum in different bst
// vect1.get()  -. stores storeInorder traversal of first bst
// vect2.get()  -. stores storeInorder traversal of second bst
public static void pairSumUtil(List<int> vect1, List<int> vect2, int sum)
{
    // Initialize two indexes to two different corners
    // of two Vectors.
    int left = 0;
    int right = vect2.Count - 1;

    // find pair by moving two corners.
    while (left < vect1.Count && right >= 0)
    {
        // If we found a pair
        if (vect1[left] + vect2[right] == sum)
        {
            Console.Write("(" + vect1[left] + ", " + vect2[right] + "), ");
            left++;
            right--;
        }

        // If sum is more, move to higher value in
        // first Vector.
        else if (vect1[left] + vect2[right] < sum)
        {
            left++;
        }

        // If sum is less, move to lower value in
        // second Vector.
        else
        {
            right--;
        }
    }
}

// Prints all pairs with given "sum" such that one
// element of pair is in tree with root1 and other
// node is in tree with root2.
public static void pairSum(Node root1, Node root2, int sum)
{
    // Store inorder traversals of two BSTs in two
    // Vectors.
    List<int> vect1 = new List<int>(), vect2 = new List<int>();
    storeInorder(root1, vect1);
    storeInorder(root2, vect2);

    // Now the problem reduces to finding a pair
    // with given sum such that one element is in
    // vect1 and other is in vect2.
    pairSumUtil(vect1, vect2, sum);
}

// Driver program to run the case
public static void Main(string[] args)
{
    // first BST
     Node root1 = null;
    root1 = insert(root1, 8);
    root1 = insert(root1, 10);
    root1 = insert(root1, 3);
    root1 = insert(root1, 6);
    root1 = insert(root1, 1);
    root1 = insert(root1, 5);
    root1 = insert(root1, 7);
    root1 = insert(root1, 14);
    root1 = insert(root1, 13);

    // second BST
     Node root2 = null;
    root2 = insert(root2, 5);
    root2 = insert(root2, 18);
    root2 = insert(root2, 2);
    root2 = insert(root2, 1);
    root2 = insert(root2, 3);
    root2 = insert(root2, 4);

    int sum = 10;
    pairSum(root1, root2, sum);
}
}

  // This code is contributed by Shrikant13
```

## **java 描述语言**

```
<script>

// JavaScript program to find pairs with given sum such
// that one element of pair exists in one BST and
// other in other BST.

// A binary Tree node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
}

// A utility function to create a new BST node
// with key as given num
function newNode(num)
{
     var temp = new Node();
    temp.data = num;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert a given key to BST
function insert(root, key)
{
    if (root == null)
    {
        return newNode(key);
    }
    if (root.data > key)
    {
        root.left = insert(root.left, key);
    }
    else
    {
        root.right = insert(root.right, key);
    }
    return root;
}

// store storeInorder traversal in auxiliary array
function storeInorder(ptr, vect)
{
    if (ptr == null)
    {
        return;
    }
    storeInorder(ptr.left, vect);
    vect.push(ptr.data);
    storeInorder(ptr.right, vect);
}

// Function to find pair for given sum in different bst
// vect1.get()  -. stores storeInorder traversal of first bst
// vect2.get()  -. stores storeInorder traversal of second bst
function pairSumUtil(vect1, vect2, sum)
{
    // Initialize two indexes to two different corners
    // of two Vectors.
    var left = 0;
    var right = vect2.length - 1;

    // find pair by moving two corners.
    while (left < vect1.length && right >= 0)
    {
        // If we found a pair
        if (vect1[left] + vect2[right] == sum)
        {
            document.write("(" + vect1[left] + ", " +
            vect2[right] + "), ");
            left++;
            right--;
        }

        // If sum is more, move to higher value in
        // first Vector.
        else if (vect1[left] + vect2[right] < sum)
        {
            left++;
        }

        // If sum is less, move to lower value in
        // second Vector.
        else
        {
            right--;
        }
    }
}

// Prints all pairs with given "sum" such that one
// element of pair is in tree with root1 and other
// node is in tree with root2.
function pairSum(root1, root2, sum)
{
    // Store inorder traversals of two BSTs in two
    // Vectors.
    var vect1 = [], vect2 = [];
    storeInorder(root1, vect1);
    storeInorder(root2, vect2);

    // Now the problem reduces to finding a pair
    // with given sum such that one element is in
    // vect1 and other is in vect2.
    pairSumUtil(vect1, vect2, sum);
}

// Driver program to run the case
// first BST
 var root1 = null;
root1 = insert(root1, 8);
root1 = insert(root1, 10);
root1 = insert(root1, 3);
root1 = insert(root1, 6);
root1 = insert(root1, 1);
root1 = insert(root1, 5);
root1 = insert(root1, 7);
root1 = insert(root1, 14);
root1 = insert(root1, 13);
// second BST
 var root2 = null;
root2 = insert(root2, 5);
root2 = insert(root2, 18);
root2 = insert(root2, 2);
root2 = insert(root2, 1);
root2 = insert(root2, 3);
root2 = insert(root2, 4);
var sum = 10;
pairSum(root1, root2, sum);

</script>
```

****输出:****

```
(5,5),(6,4),(7,3),(8,2)
```

****时间复杂度:**O(n)
T3】辅助空间: O(n)
我们还有另一种**空间优化**的方法来解决这个问题。思路是[将 bst 转换为双链表](https://www.geeksforgeeks.org/convert-given-binary-tree-doubly-linked-list-set-3/)并将上述方法应用于双链表。参见[本](https://www.geeksforgeeks.org/find-pairs-given-sum-doubly-linked-list/)篇。
**时间复杂度:** O(n)
**辅助空间:** O(1)
本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。**
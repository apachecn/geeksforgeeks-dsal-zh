# 从根节点到叶节点的最长路径上的节点之和

> 原文:[https://www . geesforgeks . org/sum-nodes-最长路径-根-叶-node/](https://www.geeksforgeeks.org/sum-nodes-longest-path-root-leaf-node/)

给定一个包含 **n 个**节点的二叉树。问题是找到从根节点到叶节点的最长路径上所有节点的和。如果两条或多条路径竞争最长的路径，则考虑具有最大节点总数的路径。
**例:**

```
Input : Binary tree:
        4        
       / \       
      2   5      
     / \ / \     
    7  1 2  3    
      /
     6
Output : 13

        4        
       / \       
      2   5      
     / \ / \     
    7  1 2  3 
      /
     6

The highlighted nodes (4, 2, 1, 6) above are 
part of the longest root to leaf path having
sum = (4 + 2 + 1 + 6) = 13
```

**方法:**递归求每个根到叶路径的节点长度和和，并相应更新最大和。
**算法:**

```
sumOfLongRootToLeafPath(root, sum, len, maxLen, maxSum)
    if root == NULL
        if maxLen < len
        maxLen = len
        maxSum = sum
    else if maxLen == len && maxSum is less than sum
        maxSum = sum
        return

    sumOfLongRootToLeafPath(root-left, sum + root-data,
                           len + 1, maxLen, maxSum)
    sumOfLongRootToLeafPath(root-right, sum + root-data,
                           len + 1, maxLen, maxSum)

sumOfLongRootToLeafPathUtil(root)
    if (root == NULL)
        return 0

    Declare maxSum = Minimum Integer
    Declare maxLen = 0
    sumOfLongRootToLeafPath(root, 0, 0, maxLen, maxSum)
    return maxSum
```

## C++

```
// C++ implementation to find the sum of nodes
// on the longest path from root to leaf node
#include <bits/stdc++.h>

using namespace std;

// Node of a binary tree
struct Node {
    int data;
    Node* left, *right;
};

// function to get a new node
Node* getNode(int data)
{
    // allocate memory for the node
    Node* newNode = (Node*)malloc(sizeof(Node));

    // put in the data
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// function to find the sum of nodes on the
// longest path from root to leaf node
void sumOfLongRootToLeafPath(Node* root, int sum,
                      int len, int& maxLen, int& maxSum)
{
    // if true, then we have traversed a
    // root to leaf path
    if (!root) {
        // update maximum length and maximum sum
        // according to the given conditions
        if (maxLen < len) {
            maxLen = len;
            maxSum = sum;
        } else if (maxLen == len && maxSum < sum)
            maxSum = sum;
        return;
    }

    // recur for left subtree
    sumOfLongRootToLeafPath(root->left, sum + root->data,
                            len + 1, maxLen, maxSum);

    // recur for right subtree
    sumOfLongRootToLeafPath(root->right, sum + root->data,
                            len + 1, maxLen, maxSum);
}

// utility function to find the sum of nodes on
// the longest path from root to leaf node
int sumOfLongRootToLeafPathUtil(Node* root)
{
    // if tree is NULL, then sum is 0
    if (!root)
        return 0;

    int maxSum = INT_MIN, maxLen = 0;

    // finding the maximum sum 'maxSum' for the
    // maximum length root to leaf path
    sumOfLongRootToLeafPath(root, 0, 0, maxLen, maxSum);

    // required maximum sum
    return maxSum;
}

// Driver program to test above
int main()
{
    // binary tree formation
    Node* root = getNode(4);         /*        4        */
    root->left = getNode(2);         /*       / \       */
    root->right = getNode(5);        /*      2   5      */
    root->left->left = getNode(7);   /*     / \ / \     */
    root->left->right = getNode(1);  /*    7  1 2  3    */
    root->right->left = getNode(2);  /*      /          */
    root->right->right = getNode(3); /*     6           */
    root->left->right->left = getNode(6);

    cout << "Sum = "
         << sumOfLongRootToLeafPathUtil(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the sum of nodes
// on the longest path from root to leaf node
public class GFG
{                       
    // Node of a binary tree
    static class Node {
        int data;
        Node left, right;

        Node(int data){
            this.data = data;
            left = null;
            right = null;
        }
    }
    static int maxLen;
    static int maxSum;

    // function to find the sum of nodes on the
    // longest path from root to leaf node
    static void sumOfLongRootToLeafPath(Node root, int sum,
                                         int len)
    {
        // if true, then we have traversed a
        // root to leaf path
        if (root == null) {
            // update maximum length and maximum sum
            // according to the given conditions
            if (maxLen < len) {
                maxLen = len;
                maxSum = sum;
            } else if (maxLen == len && maxSum < sum)
                maxSum = sum;
            return;
        }

        // recur for left subtree
        sumOfLongRootToLeafPath(root.left, sum + root.data,
                                len + 1);

        sumOfLongRootToLeafPath(root.right, sum + root.data,
                                len + 1);

    }

    // utility function to find the sum of nodes on
    // the longest path from root to leaf node
    static int sumOfLongRootToLeafPathUtil(Node root)
    {
        // if tree is NULL, then sum is 0
        if (root == null)
            return 0;

        maxSum = Integer.MIN_VALUE;
        maxLen = 0;

        // finding the maximum sum 'maxSum' for the
        // maximum length root to leaf path
        sumOfLongRootToLeafPath(root, 0, 0);

        // required maximum sum
        return maxSum;
    }

    // Driver program to test above
    public static void main(String args[])
    {
        // binary tree formation
        Node root = new Node(4);         /*        4        */
        root.left = new Node(2);         /*       / \       */
        root.right = new Node(5);        /*      2   5      */
        root.left.left = new Node(7);    /*     / \ / \     */
        root.left.right = new Node(1);   /*    7  1 2  3    */
        root.right.left = new Node(2);   /*      /          */
        root.right.right = new Node(3);  /*     6           */
        root.left.right.left = new Node(6);

        System.out.println( "Sum = "
             + sumOfLongRootToLeafPathUtil(root));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 implementation to find the 
# Sum of nodes on the longest path
# from root to leaf nodes

# function to get a new node
class getNode:
    def __init__(self, data):

        # put in the data
        self.data = data
        self.left = self.right = None

# function to find the Sum of nodes on the
# longest path from root to leaf node
def SumOfLongRootToLeafPath(root, Sum, Len,
                            maxLen, maxSum):

    # if true, then we have traversed a
    # root to leaf path
    if (not root):

        # update maximum Length and maximum Sum
        # according to the given conditions
        if (maxLen[0] < Len):
            maxLen[0] = Len
            maxSum[0] = Sum
        elif (maxLen[0]== Len and
              maxSum[0] < Sum):
            maxSum[0] = Sum
        return

    # recur for left subtree
    SumOfLongRootToLeafPath(root.left, Sum + root.data,
                            Len + 1, maxLen, maxSum)

    # recur for right subtree
    SumOfLongRootToLeafPath(root.right, Sum + root.data,
                            Len + 1, maxLen, maxSum)

# utility function to find the Sum of nodes on
# the longest path from root to leaf node
def SumOfLongRootToLeafPathUtil(root):

    # if tree is NULL, then Sum is 0
    if (not root):
        return 0

    maxSum = [-999999999999]
    maxLen = [0]

    # finding the maximum Sum 'maxSum' for
    # the maximum Length root to leaf path
    SumOfLongRootToLeafPath(root, 0, 0,
                            maxLen, maxSum)

    # required maximum Sum
    return maxSum[0]

# Driver Code
if __name__ == '__main__':

    # binary tree formation
    root = getNode(4)         #     4    
    root.left = getNode(2)         #     / \    
    root.right = getNode(5)     #     2 5    
    root.left.left = getNode(7) #     / \ / \    
    root.left.right = getNode(1) # 7 1 2 3
    root.right.left = getNode(2) #     /        
    root.right.right = getNode(3) #     6        
    root.left.right.left = getNode(6)

    print("Sum = ", SumOfLongRootToLeafPathUtil(root))

# This code is contributed by PranchalK
```

## C#

```
using System;

// c# implementation to find the sum of nodes
// on the longest path from root to leaf node
public class GFG
{
    // Node of a binary tree
    public class Node
    {
        public int data;
        public Node left, right;

        public Node(int data)
        {
            this.data = data;
            left = null;
            right = null;
        }
    }
    public static int maxLen;
    public static int maxSum;

    // function to find the sum of nodes on the
    // longest path from root to leaf node
    public static void sumOfLongRootToLeafPath(Node root, int sum, int len)
    {
        // if true, then we have traversed a
        // root to leaf path
        if (root == null)
        {
            // update maximum length and maximum sum
            // according to the given conditions
            if (maxLen < len)
            {
                maxLen = len;
                maxSum = sum;
            }
            else if (maxLen == len && maxSum < sum)
            {
                maxSum = sum;
            }
            return;
        }

        // recur for left subtree
        sumOfLongRootToLeafPath(root.left, sum + root.data, len + 1);

        sumOfLongRootToLeafPath(root.right, sum + root.data, len + 1);

    }

    // utility function to find the sum of nodes on
    // the longest path from root to leaf node
    public static int sumOfLongRootToLeafPathUtil(Node root)
    {
        // if tree is NULL, then sum is 0
        if (root == null)
        {
            return 0;
        }

        maxSum = int.MinValue;
        maxLen = 0;

        // finding the maximum sum 'maxSum' for the
        // maximum length root to leaf path
        sumOfLongRootToLeafPath(root, 0, 0);

        // required maximum sum
        return maxSum;
    }

    // Driver program to test above
    public static void Main(string[] args)
    {
        // binary tree formation
        Node root = new Node(4); //        4
        root.left = new Node(2); //       / \
        root.right = new Node(5); //      2   5
        root.left.left = new Node(7); //     / \ / \
        root.left.right = new Node(1); //    7  1 2  3
        root.right.left = new Node(2); //      /
        root.right.right = new Node(3); //     6
        root.left.right.left = new Node(6);

        Console.WriteLine("Sum = " + sumOfLongRootToLeafPathUtil(root));
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript implementation to find the sum of nodes
// on the longest path from root to leaf node

    // Node of a binary tree
     class Node {
            constructor(val) {
                this.data = val;
                this.left = null;
                this.right = null;
            }
        }
    var maxLen;
    var maxSum;

    // function to find the sum of nodes on the
    // longest path from root to leaf node
    function sumOfLongRootToLeafPath(root , sum,
                                          len)
    {
        // if true, then we have traversed a
        // root to leaf path
        if (root == null)
        {

            // update maximum length and maximum sum
            // according to the given conditions
            if (maxLen < len) {
                maxLen = len;
                maxSum = sum;
            } else if (maxLen == len && maxSum < sum)
                maxSum = sum;
            return;
        }

        // recur for left subtree
        sumOfLongRootToLeafPath(root.left, sum + root.data,
                                len + 1);

        sumOfLongRootToLeafPath(root.right, sum + root.data,
                                len + 1);

    }

    // utility function to find the sum of nodes on
    // the longest path from root to leaf node
    function sumOfLongRootToLeafPathUtil(root)
    {

        // if tree is NULL, then sum is 0
        if (root == null)
            return 0;

        maxSum = Number.MIN_VALUE;
        maxLen = 0;

        // finding the maximum sum 'maxSum' for the
        // maximum length root to leaf path
        sumOfLongRootToLeafPath(root, 0, 0);

        // required maximum sum
        return maxSum;
    }

    // Driver program to test above

        // binary tree formation
        var root = new Node(4);         /*        4        */
        root.left = new Node(2);         /*       / \       */
        root.right = new Node(5);        /*      2   5      */
        root.left.left = new Node(7);    /*     / \ / \     */
        root.left.right = new Node(1);   /*    7  1 2  3    */
        root.right.left = new Node(2);   /*      /          */
        root.right.right = new Node(3);  /*     6           */
        root.left.right.left = new Node(6);

        document.write( "Sum = "
             + sumOfLongRootToLeafPathUtil(root));

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
Sum = 13
```

**时间复杂度:** O(n)

**另一种方法:**使用级别顺序遍历

1.  创建包含路径中当前节点、级别和总和的结构。
2.  将级别为 0 和 sum 的根元素作为根元素的数据。
3.  如果需要，弹出前面的元素并更新最大级别总和和最大级别。
4.  如果存在，则推左和右节点。
5.  对树中的所有节点执行相同的操作。

## C++

```
#include <bits/stdc++.h>
using namespace std;

//Building a tree node having left and right pointers set to null initially
struct Node
{
  Node* left;
  Node* right;
  int data;
  //constructor to set the data of the newly created tree node
  Node(int element){
     data = element;
     this->left = nullptr;
     this->right = nullptr;
  }
};

int longestPathLeaf(Node* root){

  /* structure to store current Node,it's level and sum in the path*/
  struct Element{
    Node* data;
    int level;
    int sum;
  };

  /*
    maxSumLevel stores maximum sum so far in the path
    maxLevel stores maximum level so far
  */
  int maxSumLevel = root->data,maxLevel = 0;

  /* queue to implement level order traversal */

  list<Element> que;
  Element e;

  /* Each element variable stores the current Node, it's level, sum in the path */

  e.data = root;
  e.level = 0;
  e.sum = root->data;

  /* push the root element*/
  que.push_back(e);

  /* do level order traversal on the tree*/
  while(!que.empty()){

     Element front = que.front();
     Node* curr = front.data;
     que.pop_front();

     /* if the level of current front element is greater than the maxLevel so far then update maxSum*/
     if(front.level > maxLevel){
        maxSumLevel = front.sum;
        maxLevel = front.level;
     }
     /* if another path competes then update if the sum is greater than the previous path of same height*/
     else if(front.level == maxLevel && front.sum > maxSumLevel)
        maxSumLevel = front.sum;

     /* push the left element if exists*/ 
     if(curr->left){
        e.data = curr->left;
        e.sum = e.data->data;
        e.sum +=  front.sum;
        e.level = front.level+1;
        que.push_back(e);
     }
     /*push the right element if exists*/
     if(curr->right){
        e.data = curr->right;
        e.sum = e.data->data;
        e.sum +=  front.sum;
        e.level = front.level+1;
        que.push_back(e);
     }
  }

  /*return the answer*/
  return maxSumLevel;
}
//Helper function
int main() {

  Node* root = new Node(4);        
  root->left = new Node(2);        
  root->right = new Node(5);       
  root->left->left = new Node(7);  
  root->left->right = new Node(1); 
  root->right->left = new Node(2);
  root->right->right = new Node(3);
  root->left->right->left = new Node(6);

  cout << longestPathLeaf(root) << "\n";

  return 0;
}
```

**Output**

```
13
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

由 Manjukrishna 供稿

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
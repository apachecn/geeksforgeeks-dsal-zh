# 二叉树

中具有相同长度的叶路径的根

给定一棵二叉树，打印具有相等长度的根到叶路径的数量。

**示例：**

```
Input : Root of below tree
                   10
                  /   \
                8      2
              /  \    /  \
            3     5  2    4
Output : 4 paths are of length 3.

Input : Root of below tree 
                  10
                 /   \
               8      2
             /  \    /  \
            3    5  2    4
           /               \
          9                 1
Output : 2 paths are of length 3
         2 paths are of length 4

```

想法是遍历树并跟踪路径长度。 每当到达叶节点时，我们都会在哈希图中增加路径长度计数。
一旦我们遍历了树，哈希图就会具有不同路径长度的计数。 最后，我们打印哈希图的内容。

## C ++

```

// C++ program to count root to leaf paths of different 
// lengths. 
#include<bits/stdc++.h> 
using namespace std; 

/* A binary tree node */
struct Node 
{ 
    int data; 
    struct Node* left, *right; 
}; 

/* utility that allocates a new node with the 
   given data and NULL left and right pointers. */
struct Node* newnode(int data) 
{ 
    struct Node* node = new Node; 
    node->data = data; 
    node->left = node->right  = NULL; 
    return (node); 
} 

// Function to store counts of different root to leaf 
// path lengths in hash map m. 
void pathCountUtil(Node *node, unordered_map<int, int> &m, 
                                             int path_len) 
{ 
    // Base condition 
    if (node == NULL) 
        return; 

    // If leaf node reached, increment count of path 
    // length of this root to leaf path. 
    if (node->left == NULL && node->right == NULL) 
    { 
         m[path_len]++; 
         return; 
    } 

    // Recursively call for left and right subtrees with 
    // path lengths more than 1\. 
    pathCountUtil(node->left, m, path_len+1); 
    pathCountUtil(node->right, m, path_len+1); 
} 

// A wrapper over pathCountUtil() 
void pathCounts(Node *root) 
{ 
   // create an empty hash table 
   unordered_map<int, int> m; 

   // Recursively check in left and right subtrees. 
   pathCountUtil(root, m, 1); 

   // Print all path lenghts and their counts. 
   for (auto itr=m.begin(); itr != m.end(); itr++) 
      cout << itr->second << " paths have length "
           << itr->first << endl; 
} 

// Driver program to run the case 
int main() 
{ 
    struct Node *root = newnode(8); 
    root->left    = newnode(5); 
    root->right   = newnode(4); 
    root->left->left = newnode(9); 
    root->left->right = newnode(7); 
    root->right->right = newnode(11); 
    root->right->right->left = newnode(3); 
    pathCounts(root); 
    return 0; 
} 

```

## Python3

```

# Python3 program to count root to leaf  
# paths of different lengths. 

# Binary Tree Node  
""" utility that allocates a newNode  
with the given key """
class newnode:  

    # Construct to create a newNode  
    def __init__(self, key):  
        self.key = key 
        self.left = None
        self.right = None

# Function to store counts of different  
# root to leaf path lengths in hash map m.  
def pathCountUtil(node, m,path_len) : 

    # Base condition  
    if (node == None) : 
        return

    # If leaf node reached, increment count of  
    # path length of this root to leaf path.  
    if (node.left == None and node.right == None):      
        if path_len[0] not in m: 
            m[path_len[0]] = 0
        m[path_len[0]] += 1
        return

    # Recursively call for left and right  
    # subtrees with path lengths more than 1\. 
    pathCountUtil(node.left, m, [path_len[0] + 1]) 
    pathCountUtil(node.right, m, [path_len[0] + 1])  

# A wrapper over pathCountUtil()  
def pathCounts(root) : 

    # create an empty hash table  
    m = {} 
    path_len = [1] 

    # Recursively check in left and right subtrees.  
    pathCountUtil(root, m, path_len)  

    # Print all path lenghts and their counts.  
    for itr in sorted(m, reverse = True): 
        print(m[itr], " paths have length ", itr)  

# Driver Code  
if __name__ == '__main__': 

    root = newnode(8)  
    root.left = newnode(5)  
    root.right = newnode(4)  
    root.left.left = newnode(9)  
    root.left.right = newnode(7)  
    root.right.right = newnode(11)  
    root.right.right.left = newnode(3)  
    pathCounts(root) 

# This code is contributed by 
# Shubham Singh(SHUBHAMSINGH10) 

```

**输出：**

```
1 paths have length 4
2 paths have length 3

```

本文由 **[Sahil Chhabra（KILLER）](https://www.facebook.com/sahil.chhabra.965)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。
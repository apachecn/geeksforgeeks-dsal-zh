# 计算右侧较小的元素数量

> 原文： [https://www.geeksforgeeks.org/count-smaller-elements-on-right-side/](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side/)

在数组中每个元素的右边编写一个函数以计算较小元素的数量。 给定一个不同整数的未排序数组`arr[]`，请构造另一个数组`countSmaller[]`，以便`countSmaller[i]`在数组中每个元素`arr[i]`的右侧包含较小元素的数量。

例子：

```
Input:   arr[] =  {12, 1, 2, 3, 0, 11, 4}
Output:  countSmaller[]  =  {6, 1, 1, 1, 0, 1, 0} 

(Corner Cases)
Input:   arr[] =  {5, 4, 3, 2, 1}
Output:  countSmaller[]  =  {4, 3, 2, 1, 0} 

Input:   arr[] =  {1, 2, 3, 4, 5}
Output:  countSmaller[]  =  {0, 0, 0, 0, 0}

```

[](https://practice.geeksforgeeks.org/problem-page.php?pid=585)

## 强烈建议您在继续解决方案之前，单击这里进行练习。

**方法 1（简单）**：

使用两个循环。 外循环从左到右拾取所有元素。 内部循环遍历选中元素右侧的所有元素，并更新`countSmaller[]`。

## C

```c

void constructLowerArray (int *arr[], int *countSmaller, int n) 
{ 
  int i, j; 

  // initialize all the counts in countSmaller array as 0 
  for  (i = 0; i < n; i++) 
     countSmaller[i] = 0; 

  for (i = 0; i < n; i++) 
  { 
    for (j = i+1; j < n; j++) 
    { 
       if (arr[j] < arr[i]) 
         countSmaller[i]++; 
    } 
  } 
} 

/* Utility function that prints out an array on a line */
void printArray(int arr[], int size) 
{ 
  int i; 
  for (i=0; i < size; i++) 
    printf("%d ", arr[i]); 

  printf("\n"); 
} 

// Driver program to test above functions 
int main() 
{ 
  int arr[] = {12, 10, 5, 4, 2, 20, 6, 1, 0, 2}; 
  int n = sizeof(arr)/sizeof(arr[0]); 
  int *low = (int *)malloc(sizeof(int)*n); 
  constructLowerArray(arr, low, n); 
  printArray(low, n); 
  return 0; 
} 

```

## Java

```java
class CountSmaller 
{
    void constructLowerArray(int arr[], int countSmaller[], int n) 
    {
        int i, j;
 
        // initialize all the counts in countSmaller array as 0
        for (i = 0; i < n; i++)
            countSmaller[i] = 0;
 
        for (i = 0; i < n; i++) 
        {
            for (j = i + 1; j < n; j++) 
            {
                if (arr[j] < arr[i])
                    countSmaller[i]++;
            }
        }
    }
 
    /* Utility function that prints out an array on a line */
    void printArray(int arr[], int size) 
    {
        int i;
        for (i = 0; i < size; i++)
            System.out.print(arr[i] + " ");
 
        System.out.println("");
    }
 
    // Driver program to test above functions
    public static void main(String[] args) 
    {
        CountSmaller small = new CountSmaller();
        int arr[] = {12, 10, 5, 4, 2, 20, 6, 1, 0, 2};
        int n = arr.length;
        int low[] = new int[n];
        small.constructLowerArray(arr, low, n);
        small.printArray(low, n);
    }
}
```

## Python3

```py
def constructLowerArray (arr, countSmaller, n):
 
    # initialize all the counts in countSmaller array as 0 
    for i in range(n): 
        countSmaller[i] = 0; 
 
    for i in range(n):
        for j in range(i + 1,n):
            if (arr[j] < arr[i]):
                countSmaller[i] += 1
 
# Utility function that prints out an array on a line
def printArray(arr, size):
    for i in range(size):
        print(arr[i],end=" ")
    print() 
 
# Driver code 
arr = [12, 10, 5, 4, 2, 20, 6, 1, 0, 2]
n = len(arr)
low = [0]*n
constructLowerArray(arr, low, n)
printArray(low, n)
 
# This code is contributed by ApurvaRaj
```

## C#

```cs
using System;
 
class GFG {
     
    static void constructLowerArray(int []arr,
                    int []countSmaller, int n) 
    {
        int i, j;
 
        // initialize all the counts in
        // countSmaller array as 0
        for (i = 0; i < n; i++)
            countSmaller[i] = 0;
 
        for (i = 0; i < n; i++) 
        {
            for (j = i + 1; j < n; j++) 
            {
                if (arr[j] < arr[i])
                    countSmaller[i]++;
            }
        }
    }
     
    /* Utility function that prints out
    an array on a line */
    static void printArray(int []arr, int size) 
    {
        int i;
        for (i = 0; i < size; i++)
            Console.Write(arr[i] + " ");
 
        Console.WriteLine("");
    }
     
    // Driver function
    public static void Main()
    {
        int []arr = new int[]{12, 10, 5, 4, 
                            2, 20, 6, 1, 0, 2};
        int n = arr.Length;
        int []low = new int[n];
         
        constructLowerArray(arr, low, n);
        printArray(low, n);
    }
}
 
// This code is contributed by Sam007
```

时间复杂度：`O(n ^ 2)`。

辅助空间：`O(1)`。

方法 2（使用自平衡BST）：

自平衡二进制搜索树（AVL，红黑等）可用于获得`O(nLogn)`时间复杂度的解决方案。 我们可以扩充这些树，以便每个节点`N`都包含以`N`为根的子树的大小。我们在以下实现中使用了 AVL 树。

我们从右到左遍历数组，并将所有元素一一插入到 AVL 树中。 在 AVL 树中插入新密钥时，我们首先将键与`root`进行比较。 如果键大于`root`，则它大于`root`左子树中的所有节点。 因此，我们将左侧子树的大小添加到要插入的键的较小元素的数量中。 对于所有节点，我们都递归地遵循相同的方法。

以下是C的实现。

## C

```c
#include<stdio.h>
#include<stdlib.h>
 
// An AVL tree node
struct node
{
    int key;
    struct node *left;
    struct node *right;
    int height;
    int size; // size of the tree rooted with this node
};
 
// A utility function to get maximum of two integers
int max(int a, int b);
 
// A utility function to get height of the tree rooted with N
int height(struct node *N)
{
    if (N == NULL)
        return 0;
    return N->height;
}
 
// A utility function to size of the tree of rooted with N
int size(struct node *N)
{
    if (N == NULL)
        return 0;
    return N->size;
}
 
// A utility function to get maximum of two integers
int max(int a, int b)
{
    return (a > b)? a : b;
}
 
/* Helper function that allocates a new node with the given key and
    NULL left and right pointers. */
struct node* newNode(int key)
{
    struct node* node = (struct node*)
                        malloc(sizeof(struct node));
    node->key   = key;
    node->left   = NULL;
    node->right  = NULL;
    node->height = 1;  // new node is initially added at leaf
    node->size = 1;
    return(node);
}
 
// A utility function to right rotate subtree rooted with y
struct node *rightRotate(struct node *y)
{
    struct node *x = y->left;
    struct node *T2 = x->right;
 
    // Perform rotation
    x->right = y;
    y->left = T2;
 
    // Update heights
    y->height = max(height(y->left), height(y->right))+1;
    x->height = max(height(x->left), height(x->right))+1;
 
    // Update sizes
    y->size = size(y->left) + size(y->right) + 1;
    x->size = size(x->left) + size(x->right) + 1;
 
    // Return new root
    return x;
}
 
// A utility function to left rotate subtree rooted with x
struct node *leftRotate(struct node *x)
{
    struct node *y = x->right;
    struct node *T2 = y->left;
 
    // Perform rotation
    y->left = x;
    x->right = T2;
 
    //  Update heights
    x->height = max(height(x->left), height(x->right))+1;
    y->height = max(height(y->left), height(y->right))+1;
 
    // Update sizes
    x->size = size(x->left) + size(x->right) + 1;
    y->size = size(y->left) + size(y->right) + 1;
 
    // Return new root
    return y;
}
 
// Get Balance factor of node N
int getBalance(struct node *N)
{
    if (N == NULL)
        return 0;
    return height(N->left) - height(N->right);
}
 
// Inserts a new key to the tree rotted with node. Also, updates *count
// to contain count of smaller elements for the new key
struct node* insert(struct node* node, int key, int *count)
{
    /* 1.  Perform the normal BST rotation */
    if (node == NULL)
        return(newNode(key));
 
    if (key < node->key)
        node->left  = insert(node->left, key, count);
    else
    {
        node->right = insert(node->right, key, count);
 
        // UPDATE COUNT OF SMALLER ELEMENTS FOR KEY
        *count = *count + size(node->left) + 1;
    }
 
 
    /* 2. Update height and size of this ancestor node */
    node->height = max(height(node->left), height(node->right)) + 1;
    node->size   = size(node->left) + size(node->right) + 1;
 
    /* 3. Get the balance factor of this ancestor node to check whether
       this node became unbalanced */
    int balance = getBalance(node);
 
    // If this node becomes unbalanced, then there are 4 cases
 
    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);
 
    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);
 
    // Left Right Case
    if (balance > 1 && key > node->left->key)
    {
        node->left =  leftRotate(node->left);
        return rightRotate(node);
    }
 
    // Right Left Case
    if (balance < -1 && key < node->right->key)
    {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }
 
    /* return the (unchanged) node pointer */
    return node;
}
 
// The following function updates the countSmaller array to contain count of
// smaller elements on right side.
void constructLowerArray (int arr[], int countSmaller[], int n)
{
  int i, j;
  struct node *root = NULL;
 
  // initialize all the counts in countSmaller array as 0
  for  (i = 0; i < n; i++)
     countSmaller[i] = 0;
 
  // Starting from rightmost element, insert all elements one by one in
  // an AVL tree and get the count of smaller elements
  for (i = n-1; i >= 0; i--)
  {
     root = insert(root, arr[i], &countSmaller[i]);
  }
}
 
/* Utility function that prints out an array on a line */
void printArray(int arr[], int size)
{
  int i;
  printf("\n");
  for (i=0; i < size; i++)
    printf("%d ", arr[i]);
}
 
// Driver program to test above functions
int main()
{
  int arr[] = {10, 6, 15, 20, 30, 5, 7};
  int n = sizeof(arr)/sizeof(arr[0]);
 
  int *low = (int *)malloc(sizeof(int)*n);
 
  constructLowerArray(arr, low, n);
 
  printf("Following is the constructed smaller count array");
  printArray(low, n);
  return 0;
}
```

输出：

```
Following is the constructed smaller count array
3 1 2 2 2 0 0
```

时间复杂度：`O(nLogn)`。

辅助空间：`O(n)`。

方法 3（使用带有 2 个额外字段的 BST）：

解决上述问题的另一种方法是使用带有2个额外字段的简单二进制搜索树：

1.  将元素保留在节点的左侧
2.  存储元素的频率。

在这种方法中，我们从结尾到乞求遍历输入数组，并将元素添加到 BST 中。

在将元素插入 BST 时，如果我们移到BST的右侧，我们可以简单地通过计算元素的频率和当前节点左侧的元素数量之和来计算较小元素的数量。 当前节点。

将元素放置在正确的位置后，我们可以返回此总和值。

## C++14

```
#include<bits/stdc++.h>
using namespace std;
 
// BST node structure
class Node{
     
public:
    int val;
    int count;
    Node* left;
    Node* right;
     
    // Constructor
    Node(int num1, int num2)
    {
        this->val = num1;
        this->count = num2;
        this->left = this->right = NULL;
    }
};
 
// Function to addNode and find the smaller 
// elements on the right side
int addNode(Node*& root, int value, 
                         int countSmaller)
{
     
    // Base case
    if (root == NULL)
    {
        root = new Node(value, 0);
        return countSmaller;
    }
    if (root->val < value)
    {
        return root->count + 
       addNode(root->right, 
               value, 
               countSmaller + 1);
    }
    else
    {
        root->count++;
        return addNode(root->left, value,
                       countSmaller);
    }
}
 
// Driver code
int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(0);
    int data[] = { 10, 6, 15, 20, 30, 5, 7 };
    int size = sizeof(data) / sizeof(data[0]);
    int ans[size] = {0};
 
    Node* root = NULL;
     
    for(int i = size - 1; i >= 0; i--)
    {
        ans[i] = addNode(root, data[i], 0);
    }
 
    for(int i = 0; i < size; i++)
        cout << ans[i] << " ";
 
    return 0;
}
 
// This code is contributed by divyanshu gupta
```

## Python

```py
class Node: 
    def __init__(self,val): 
        self.val = val 
        self.left = None
        self.right = None
 
        # denotes number of times (frequency) 
        # an element has occurred. 
        self.elecount = 1
 
        # denotes the number of nodes on left 
        # side of the node encountered so far. 
        self.lcount = 0
 
class Tree: 
    def __init__(self,root): 
        self.root = root 
    def insert(self,node): 
 
        """This function helps to place an element at 
            its correct position in the BST and returns 
            the count of elements which are smaller than 
            the elements which are already inserted into the BST. 
        """
        curr = self.root 
        cnt = 0
        while curr!=None: 
            prev = curr 
            if node.val>curr.val: 
 
                # This step computes the number of elements 
                # which are less than the current Node. 
                cnt += (curr.elecount+curr.lcount) 
                curr=curr.right 
            elif node.val<curr.val: 
                curr.lcount+=1
                curr=curr.left 
            else: 
                prev=curr 
                prev.elecount+=1
                break
        if prev.val>node.val: 
            prev.left = node 
        elif prev.val<node.val: 
            prev.right = node 
        else: 
            return cnt+prev.lcount 
        return cnt 
 
def constructArray(arr,n): 
    t = Tree(Node(arr[-1])) 
    ans = [0] 
    for i in range(n-2,-1,-1): 
        ans.append(t.insert(Node(arr[i]))) 
    return reversed(ans) 
 
# Driver function for above code     
def main(): 
    n = 7
    arr = [10, 6, 15, 20, 30, 5, 7] 
    print(" ".join(list(map(str,constructArray(arr,n))))) 
if __name__ == "__main__": 
    main() 
 
# Code Contributed by Tarun Gudipati
```

输出：

```
3 1 2 2 2 0 0
```

时间复杂度：`O(nLogn)`。

辅助空间：`O(n)`。

[使用 C++ STL 中的集合计算右侧较小的元素](https://www.geeksforgeeks.org/count-smaller-elements-right-side-using-set-c-stl/)。
# 检查给定的数组是否能够表示二叉查找树的水平顺序遍历

> 原文:[https://www . geesforgeks . org/check-given-array-can-representative-level-order-遍历-binary-search-tree/](https://www.geeksforgeeks.org/check-given-array-can-represent-level-order-traversal-binary-search-tree/)

给定大小为 **n** 的数组。问题是检查给定的数组是否能表示二叉查找树的水平顺序遍历。

示例:

```
Input : arr[] = {7, 4, 12, 3, 6, 8, 1, 5, 10}
Output : Yes
For the given arr[] the Binary Search Tree is:
         7        
       /    \       
      4     12      
     / \    /     
    3   6  8    
   /   /    \
  1   5     10

Input : arr[] = {11, 6, 13, 5, 12, 10}
Output : No
The given arr[] do not represent the level
order traversal of a BST.
```

想法是使用队列数据结构。队列的每个元素都有一个结构，比如**节点详细信息**，它存储了树节点的详细信息。详细信息是节点的数据，以及两个变量**最小值**和**最大值**，其中**最小值**存储节点值的下限，该节点值可以是左子树的一部分，**最大值**存储节点值的上限，该节点值可以是**节点详细信息**结构变量中指定节点的右子树的一部分。对于第一个数组值 arr[0]，创建一个**节点详细信息**结构，将 arr[0]作为节点的数据， **min** = INT_MIN， **max** = INT_MAX。将此结构变量添加到队列中。此节点将是树的根。移动到 arr[]中的第二个元素，然后执行以下步骤:

1.  从**温度**的队列中弹出**节点详细信息**。
2.  借助 **min** 和**temp data**值，检查当前数组元素是否可以是 **temp** 中节点的左子元素。如果可以，则为这个新的数组元素值创建一个新的**节点详细信息**结构，并使用其适当的“最小值”和“最大值”值，将其推入队列，并移动到 arr[]中的下一个元素。
3.  借助 **max** 和**temp data**值，检查当前数组元素是否可以是 **temp** 中节点的右子元素。如果可以，则为这个新的数组元素值创建一个新的**节点详细信息**结构，并使用其适当的“最小值”和“最大值”值，将其推入队列，并移动到 arr[]中的下一个元素。
4.  重复步骤 1、2 和 3，直到 arr[]中不再有元素，或者队列中不再有元素。

最后，如果数组的所有元素都被遍历了，那么这个数组就代表了一个 BST 的水平顺序遍历，否则就不是。

## C++

```
// C++ implementation to check if the given array
// can represent Level Order Traversal of Binary
// Search Tree
#include <bits/stdc++.h>

using namespace std;

// to store details of a node like
// node's data, 'min' and 'max' to obtain the
// range of values where node's left and
// right child's should lie
struct NodeDetails
{
    int data;
    int min, max;
};

// function to check if the given array
// can represent Level Order Traversal
// of Binary Search Tree
bool levelOrderIsOfBST(int arr[], int n)
{
    // if tree is empty
    if (n == 0)
        return true;

    // queue to store NodeDetails
    queue<NodeDetails> q;

    // index variable to access array elements
    int i=0;

    // node details for the
    // root of the BST
    NodeDetails newNode;
    newNode.data = arr[i++];
    newNode.min = INT_MIN;
    newNode.max = INT_MAX;
    q.push(newNode);

    // until there are no more elements
    // in arr[] or queue is not empty
    while (i != n && !q.empty())       
    {
        // extracting NodeDetails of a
        // node from the queue
        NodeDetails temp = q.front();
        q.pop();

        // check whether there are more elements
        // in the arr[] and arr[i] can be left child
        // of 'temp.data' or not
        if (i < n && (arr[i] < temp.data &&
                     arr[i] > temp.min))
        {
            // Create NodeDetails for newNode
            /// and add it to the queue
            newNode.data = arr[i++];
            newNode.min = temp.min;
            newNode.max = temp.data;
            q.push(newNode);               
        }

        // check whether there are more elements
        // in the arr[] and arr[i] can be right child
        // of 'temp.data' or not
        if (i < n && (arr[i] > temp.data &&
                      arr[i] < temp.max))
        {
            // Create NodeDetails for newNode
            /// and add it to the queue
            newNode.data = arr[i++];
            newNode.min = temp.data;
            newNode.max = temp.max;
            q.push(newNode);           
        }       
    }

    // given array represents level
    // order traversal of BST
    if (i == n)
        return true;

    // given array do not represent
    // level order traversal of BST   
    return false;       
}

// Driver program to test above
int main()
{
    int arr[] = {7, 4, 12, 3, 6, 8, 1, 5, 10};   
    int n = sizeof(arr) / sizeof(arr[0]);   
    if (levelOrderIsOfBST(arr, n))
        cout << "Yes";
    else
        cout << "No";       
    return 0;   
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if the given array
// can represent Level Order Traversal of Binary
// Search Tree
import java.util.*;

class Solution
{

// to store details of a node like
// node's data, 'min' and 'max' to obtain the
// range of values where node's left and
// right child's should lie
static class NodeDetails
{
    int data;
    int min, max;
};

// function to check if the given array
// can represent Level Order Traversal
// of Binary Search Tree
static boolean levelOrderIsOfBST(int arr[], int n)
{
    // if tree is empty
    if (n == 0)
        return true;

    // queue to store NodeDetails
    Queue<NodeDetails> q = new LinkedList<NodeDetails>();

    // index variable to access array elements
    int i = 0;

    // node details for the
    // root of the BST
    NodeDetails newNode=new NodeDetails();
    newNode.data = arr[i++];
    newNode.min = Integer.MIN_VALUE;
    newNode.max = Integer.MAX_VALUE;
    q.add(newNode);

    // until there are no more elements
    // in arr[] or queue is not empty
    while (i != n && q.size() > 0)    
    {
        // extracting NodeDetails of a
        // node from the queue
        NodeDetails temp = q.peek();
        q.remove();
        newNode = new NodeDetails();

        // check whether there are more elements
        // in the arr[] and arr[i] can be left child
        // of 'temp.data' or not
        if (i < n && (arr[i] < (int)temp.data &&
                    arr[i] > (int)temp.min))
        {
            // Create NodeDetails for newNode
            /// and add it to the queue
            newNode.data = arr[i++];
            newNode.min = temp.min;
            newNode.max = temp.data;
            q.add(newNode);            
        }

        newNode=new NodeDetails();

        // check whether there are more elements
        // in the arr[] and arr[i] can be right child
        // of 'temp.data' or not
        if (i < n && (arr[i] > (int)temp.data &&
                    arr[i] < (int)temp.max))
        {
            // Create NodeDetails for newNode
            /// and add it to the queue
            newNode.data = arr[i++];
            newNode.min = temp.data;
            newNode.max = temp.max;
            q.add(newNode);        
        }    
    }

    // given array represents level
    // order traversal of BST
    if (i == n)
        return true;

    // given array do not represent
    // level order traversal of BST
    return false;    
}

// Driver code
public static void main(String args[])
{
    int arr[] = {7, 4, 12, 3, 6, 8, 1, 5, 10};
    int n = arr.length;
    if (levelOrderIsOfBST(arr, n))
        System.out.print( "Yes");
    else
        System.out.print( "No");    

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation to check if the
# given array can represent Level Order
# Traversal of Binary Search Tree
INT_MIN, INT_MAX = float('-inf'), float('inf')

# To store details of a node like node's
# data, 'min' and 'max' to obtain the
# range of values where node's left
# and right child's should lie
class NodeDetails:

    def __init__(self, data, min, max):
        self.data = data
        self.min = min
        self.max = max

# function to check if the given array
# can represent Level Order Traversal
# of Binary Search Tree
def levelOrderIsOfBST(arr, n):

    # if tree is empty
    if n == 0:
        return True

    # queue to store NodeDetails
    q = []

    # index variable to access array elements
    i = 0

    # node details for the root of the BST
    newNode = NodeDetails(arr[i], INT_MIN, INT_MAX)
    i += 1
    q.append(newNode)

    # until there are no more elements
    # in arr[] or queue is not empty
    while i != n and len(q) != 0:    

        # extracting NodeDetails of a
        # node from the queue
        temp = q.pop(0)

        # check whether there are more elements
        # in the arr[] and arr[i] can be left
        # child of 'temp.data' or not
        if i < n and (arr[i] < temp.data and
                    arr[i] > temp.min):

            # Create NodeDetails for newNode
            #/ and add it to the queue
            newNode = NodeDetails(arr[i], temp.min, temp.data)
            i += 1
            q.append(newNode)            

        # check whether there are more elements
        # in the arr[] and arr[i] can be right
        # child of 'temp.data' or not
        if i < n and (arr[i] > temp.data and
                    arr[i] < temp.max):

            # Create NodeDetails for newNode
            #/ and add it to the queue
            newNode = NodeDetails(arr[i], temp.data, temp.max)
            i += 1
            q.append(newNode)        

    # given array represents level
    # order traversal of BST
    if i == n:
        return True

    # given array do not represent
    # level order traversal of BST
    return False       

# Driver code
if __name__ == "__main__":

    arr = [7, 4, 12, 3, 6, 8, 1, 5, 10]
    n = len(arr)    
    if levelOrderIsOfBST(arr, n):
        print("Yes")
    else:
        print("No")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation to check if the given array
// can represent Level Order Traversal of Binary
// Search Tree
using System;
using System.Collections.Generic;

class GFG
{

// to store details of a node like
// node's data, 'min' and 'max' to obtain the
// range of values where node's left and
// right child's should lie
public class NodeDetails
{
    public int data;
    public int min, max;
};

// function to check if the given array
// can represent Level Order Traversal
// of Binary Search Tree
static Boolean levelOrderIsOfBST(int []arr, int n)
{
    // if tree is empty
    if (n == 0)
        return true;

    // queue to store NodeDetails
    Queue<NodeDetails> q = new Queue<NodeDetails>();

    // index variable to access array elements
    int i = 0;

    // node details for the
    // root of the BST
    NodeDetails newNode=new NodeDetails();
    newNode.data = arr[i++];
    newNode.min = int.MinValue;
    newNode.max = int.MaxValue;
    q.Enqueue(newNode);

    // until there are no more elements
    // in arr[] or queue is not empty
    while (i != n && q.Count > 0)    
    {
        // extracting NodeDetails of a
        // node from the queue
        NodeDetails temp = q.Peek();
        q.Dequeue();
        newNode = new NodeDetails();

        // check whether there are more elements
        // in the arr[] and arr[i] can be left child
        // of 'temp.data' or not
        if (i < n && (arr[i] < (int)temp.data &&
                    arr[i] > (int)temp.min))
        {
            // Create NodeDetails for newNode
            /// and add it to the queue
            newNode.data = arr[i++];
            newNode.min = temp.min;
            newNode.max = temp.data;
            q.Enqueue(newNode);            
        }

        newNode=new NodeDetails();

        // check whether there are more elements
        // in the arr[] and arr[i] can be right child
        // of 'temp.data' or not
        if (i < n && (arr[i] > (int)temp.data &&
                    arr[i] < (int)temp.max))
        {
            // Create NodeDetails for newNode
            /// and add it to the queue
            newNode.data = arr[i++];
            newNode.min = temp.data;
            newNode.max = temp.max;
            q.Enqueue(newNode);        
        }    
    }

    // given array represents level
    // order traversal of BST
    if (i == n)
        return true;

    // given array do not represent
    // level order traversal of BST
    return false;    
}

// Driver code
public static void Main(String []args)
{
    int []arr = {7, 4, 12, 3, 6, 8, 1, 5, 10};
    int n = arr.Length;
    if (levelOrderIsOfBST(arr, n))
        Console.Write( "Yes");
    else
        Console.Write( "No");    

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation to check if
// the given array can represent Level
// Order Traversal of Binary Search Tree

// To store details of a node like node's
// data, 'min' and 'max' to obtain the
// range of values where node's left and
// right child's should lie
class NodeDetails
{
    constructor()
    {
       this.min;
       this.max;
       this.data;
    }
}

// Function to check if the given array
// can represent Level Order Traversal
// of Binary Search Tree
function levelOrderIsOfBST(arr, n)
{

    // If tree is empty
    if (n == 0)
        return true;

    // Queue to store NodeDetails
    let q = [];

    // Index variable to access array elements
    let i = 0;

    // Node details for the
    // root of the BST
    let newNode = new NodeDetails();
    newNode.data = arr[i++];
    newNode.min = Number.MIN_VALUE;
    newNode.max = Number.MAX_VALUE;
    q.push(newNode);

    // Until there are no more elements
    // in arr[] or queue is not empty
    while (i != n && q.length > 0)    
    {

        // Extracting NodeDetails of a
        // node from the queue
        let temp = q[0];
        q.shift();
        newNode = new NodeDetails();

        // Check whether there are more elements
        // in the arr[] and arr[i] can be left child
        // of 'temp.data' or not
        if (i < n && (arr[i] < temp.data &&
                      arr[i] > temp.min))
        {

            // Create NodeDetails for newNode
            // and add it to the queue
            newNode.data = arr[i++];
            newNode.min = temp.min;
            newNode.max = temp.data;
            q.push(newNode);            
        }

        newNode = new NodeDetails();

        // Check whether there are more elements
        // in the arr[] and arr[i] can be right child
        // of 'temp.data' or not
        if (i < n && (arr[i] > temp.data &&
                      arr[i] < temp.max))
        {

            // Create NodeDetails for newNode
            // and add it to the queue
            newNode.data = arr[i++];
            newNode.min = temp.data;
            newNode.max = temp.max;
            q.push(newNode);        
        }    
    }

    // Given array represents level
    // order traversal of BST
    if (i == n)
        return true;

    // Given array do not represent
    // level order traversal of BST
    return false;    
}

// Driver code
let arr = [ 7, 4, 12, 3, 6, 8, 1, 5, 10 ];
let n = arr.length;

if (levelOrderIsOfBST(arr, n))
    document.write("Yes");
else
    document.write("No");   

// This code is contributed by vaibhavrabadiya3

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(n)

本文由 [**阿育什·乔哈里**](https://auth.geeksforgeeks.org/profile.php?user=ayushjauhari14) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
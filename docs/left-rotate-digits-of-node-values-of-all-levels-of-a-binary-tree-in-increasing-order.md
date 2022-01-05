# 二叉树各级节点值的左旋转位数递增

> 原文:[https://www . geesforgeks . org/left-按递增顺序旋转各级二叉树的节点值位数/](https://www.geeksforgeeks.org/left-rotate-digits-of-node-values-of-all-levels-of-a-binary-tree-in-increasing-order/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是通过向左旋转每个节点任意次数来修改树，使得每个级别由从左到右递增的节点值组成。如果无法按递增顺序排列任何级别的节点值，则打印**-1”**。

**示例:**

> **输入:**
> **341
> /\
> 241 123
> /\ \
> 324 235 161
> **输出:**
> **341
> /\
> 124 231
> /\ \
> 243 352 611
> **解释:**
> T23
> **2 级:**节点值为 241 和 123。向左旋转 241 两次和 231 一次将节点值修改为 124 和 231。
> **三级:**节点值为 342、235、161。342 一次、235 一次和 161 一次的左旋转数字分别将节点值修改为{243、352、611}。****
> 
> ******输入:**
> **12
> /\
> 89 15******
> 
>  ********输出:** -1******

******方法:**给定的问题可以通过执行[级别顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)并向左旋转节点值的数字以使值以递增的顺序进入每个级别来解决。按照以下步骤解决问题:****

*   ****初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)，比如说 **Q** ，用来执行等级顺序遍历。****
*   ****[推送队列中树的根节点](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)。****
*   ****迭代直到[队列不为空](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)并执行以下步骤:

    *   找到队列的[大小，并将其存储在变量 **L** 中。](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)
    *   初始化一个变量，比如 **prev** ，用来存储当前层次树中的前一个元素。
    *   迭代范围**【0，L】**，并执行以下步骤:
        *   [弹出队列的前节点](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)并将其存储在变量中，比如 **temp** 。
        *   现在，向左移动元素 **temp** ，如果存在大于 **prev** 且更接近 **prev** 的排列，则更新当前节点的值作为 **temp** 的值。
    *   将 **prev** 的值更新为**温度**的当前值。
    *   如果**温度**有左或右子，则将其推入队列。**** 
*   ****完成上述步骤后，如果当前节点集没有按递增顺序排序，则打印**“否”**。否则，检查下一次迭代。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// TreeNode class
struct TreeNode
{
    int val;
    TreeNode* left,*right;

    TreeNode(int v)
    {
        val = v;
        left = NULL;
        right = NULL;
    }
};

// Function to check if the nodes
// are in increasing order or not
bool isInc(TreeNode *root)
{

    // Perform Level Order Traversal
    queue<TreeNode*> que;
    que.push(root);

    while (true)
    {

        // Current length of queue
        int length = que.size();

        // If queue is empty
        if (length == 0)
            break;

        auto pre = que.front();

        // Level order traversal
        while (length > 0)
        {

            // Pop element from
            // front of the queue
            auto temp = que.front();
            que.pop();

            // If previous value exceeds
            // current value, return false
            if (pre->val > temp->val)
                return false;

            pre = temp;
            if (temp->left)
                que.push(temp->left);

            if (temp->right)
                que.push(temp->right);

            length -= 1;
        }
    }
    return true;
}

// Function to print the Tree
// after modification
void levelOrder(TreeNode *root)
{

    // Performs level
    // order traversal
    queue<TreeNode*> que;
    que.push(root);

    while (true)
    {

        // Calculate size of the queue
        int length = que.size();

        if (length == 0)
            break;

        // Iterate until queue is empty
        while (length)
        {
            auto temp = que.front();
            que.pop();
            cout << temp->val << " ";

            if (temp->left)
                que.push(temp->left);

            if (temp->right)
                que.push(temp->right);

            length -= 1;
        }
        cout << endl;
    }
    cout << endl;
}

// Function to arrange node values
// of each level in increasing order
void makeInc(TreeNode *root)
{

    // Perform level order traversal
    queue<TreeNode*> que;
    que.push(root);

    while (true)
    {

        // Calculate length of queue
        int length = que.size();

        // If queue is empty
        if (length == 0)
            break;

        int prev = -1;

        // Level order traversal
        while (length > 0)
        {
            //cout<<"loop";

            // Pop element from
            // front of the queue
            auto temp = que.front();
            que.pop();

            // Initialize the optimal
            // element by the initial
            // element
            auto optEle = temp->val;
            auto strEle = to_string(temp->val);

            // Check for all left
            // shift operations
            bool flag = true;
            int yy = strEle.size();
            for(int idx = 0; idx < strEle.size(); idx++)
            {

                // Left shift
                int ls = stoi(strEle.substr(idx, yy) +
                              strEle.substr(0, idx));

                if (ls >= prev and flag)
                {
                    optEle = ls;
                    flag = false;
                }

                // If the current shifting
                // gives optimal solution
                if (ls >= prev)
                    optEle = min(optEle, ls);
            }

            // Replacing initial element
            // by the optimal element
            temp->val = optEle;
            prev = temp->val;

            // Push the LST
            if (temp->left)
                que.push(temp->left);

            // Push the RST
            if (temp->right)
                que.push(temp->right);

            length -= 1;
        }
    }

    // Print the result
    if (isInc(root))
        levelOrder(root);
    else
        cout << (-1);
}

// Driver Code
int main()
{
    TreeNode *root = new TreeNode(341);
    root->left = new TreeNode(241);
    root->right = new TreeNode(123);
    root->left->left = new TreeNode(324);
    root->left->right = new TreeNode(235);
    root->right->right = new TreeNode(161);

    makeInc(root);
}

// This code is contributed by mohit kumar 29**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;

class GFG{

// TreeNode class
static class TreeNode
{
    public int val;
    public TreeNode left,right;
};

static TreeNode newNode(int v)
{
    TreeNode temp = new TreeNode();
    temp.val = v;
    temp.left = temp.right = null;
    return temp;
}

// Function to check if the nodes
// are in increasing order or not
static boolean isInc(TreeNode root)
{

    // Perform Level Order Traversal
    Queue<TreeNode> que = new LinkedList<>();
    que.add(root);

    while (true)
    {

        // Current len of queue
        int len = que.size();

        // If queue is empty
        if (len == 0)
            break;

        TreeNode pre = que.peek();

        // Level order traversal
        while (len > 0)
        {

            // Pop element from
            // front of the queue
            TreeNode temp = que.peek();
            que.poll();

            // If previous value exceeds
            // current value, return false
            if (pre.val > temp.val)
                return false;

            pre = temp;
            if (temp.left != null)
                que.add(temp.left);

            if (temp.right != null)
                que.add(temp.right);

            len -= 1;
        }
    }
    return true;
}

// Function to print the Tree
// after modification
static void levelOrder(TreeNode root)
{

    // Performs level
    // order traversal
    Queue<TreeNode> que = new LinkedList<>();
    que.add(root);

    while (true)
    {

        // Calculate size of the queue
        int len = que.size();

        if (len == 0)
            break;

        // Iterate until queue is empty
        while (len > 0)
        {
            TreeNode temp = que.peek();
            que.poll();
            System.out.print(temp.val+" ");

            if (temp.left != null)
                que.add(temp.left);

            if (temp.right != null)
                que.add(temp.right);

            len -= 1;
        }
       System.out.println();
    }
    System.out.println();
}

// Function to arrange node values
// of each level in increasing order
static void makeInc(TreeNode root)
{

    // Perform level order traversal
    Queue<TreeNode> que = new LinkedList<>();
    que.add(root);

    while (true)
    {

        // Calculate len of queue
        int len = que.size();

        // If queue is empty
        if (len == 0)
            break;

        int prev = -1;

        // Level order traversal
        while (len > 0)
        {

            //cout<<"loop";

            // Pop element from
            // front of the queue
            TreeNode temp = que.peek();
            que.poll();

            // Initialize the optimal
            // element by the initial
            // element
            int optEle = temp.val;
            String strEle = String.valueOf(optEle);

            // Check for all left
            // shift operations
            boolean flag = true;
            int yy = strEle.length();

            for(int idx = 0; idx < strEle.length(); idx++)
            {

                // Left shift
                String s1 = strEle.substring(idx, yy);
                String s2 = strEle.substring(0, idx);
                String s = s1+ s2;
                int ls = Integer.valueOf(s);

                if (ls >= prev && flag)
                {
                    optEle = ls;
                    flag = false;
                }

                // If the current shifting
                // gives optimal solution
                if (ls >= prev)
                    optEle = Math.min(optEle, ls);
            }

            // Replacing initial element
            // by the optimal element
            temp.val = optEle;
            prev = temp.val;

            // Push the LST
            if (temp.left != null)
                que.add(temp.left);

            // Push the RST
            if (temp.right != null)
                que.add(temp.right);

            len -= 1;
        }
    }

    // Print the result
    if (isInc(root) == true)
        levelOrder(root);
    else
       System.out.print(-1);
}

// Driver code
public static void main (String[] args)
{
    TreeNode root = newNode(341);
    root.left = newNode(241);
    root.right = newNode(123);
    root.left.left = newNode(324);
    root.left.right = newNode(235);
    root.right.right = newNode(161);

    makeInc(root);
}
}

// This code is contributed by offbeat**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# TreeNode class
class TreeNode:
    def __init__(self, val = 0, left = None, right = None):
        self.val = val
        self.left = left
        self.right = right

# Function to check if the nodes
# are in increasing order or not
def isInc(root):

    # Perform Level Order Traversal
    que = [root]
    while True:

        # Current length of queue
        length = len(que)

        # If queue is empty
        if not length:
            break
        pre = que[0]

        # Level order traversal
        while length:

            # Pop element from
            # front of the queue
            temp = que.pop(0)

            # If previous value exceeds
            # current value, return false
            if pre.val > temp.val:
                return False

            pre = temp
            if temp.left:
                que.append(temp.left)

            if temp.right:
                que.append(temp.right)

            length -= 1

    return True

# Function to arrange node values
# of each level in increasing order
def makeInc(root):

    # Perform level order traversal
    que = [root]
    while True:

        # Calculate length of queue
        length = len(que)

        # If queue is empty
        if not length:
            break
        prev = -1

        # Level order traversal
        while length:

            # Pop element from
            # front of the queue
            temp = que.pop(0)

            # Initialize the optimal
            # element by the initial
            # element
            optEle = temp.val
            strEle = str(temp.val)

            # Check for all left
            # shift operations
            flag = True
            for idx in range(len(strEle)):

                # Left shift
                ls = int(strEle[idx:] + strEle[:idx])

                if ls >= prev and flag:
                    optEle = ls
                    flag = False

                # If the current shifting
                # gives optimal solution
                if ls >= prev:
                    optEle = min(optEle, ls)

            # Replacing initial element
            # by the optimal element
            temp.val = optEle
            prev = temp.val

            # Push the LST
            if temp.left:
                que.append(temp.left)

            # Push the RST
            if temp.right:
                que.append(temp.right)
            length -= 1

    # Print the result
    if isInc(root):
        levelOrder(root)
    else:
        print(-1)

# Function to print the Tree
# after modification
def levelOrder(root):

    # Performs level
    # order traversal
    que = [root]
    while True:

        # Calculate size of the queue
        length = len(que)

        if not length:
            break

        # Iterate until queue is empty
        while length:
            temp = que.pop(0)
            print(temp.val, end =' ')

            if temp.left:
                que.append(temp.left)

            if temp.right:
                que.append(temp.right)
            length -= 1
        print()

# Driver Code
root = TreeNode(341)
root.left = TreeNode(241)
root.right = TreeNode(123)
root.left.left = TreeNode(324)
root.left.right = TreeNode(235)
root.right.right = TreeNode(161)

makeInc(root)**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// TreeNode class
class TreeNode
{
    public int val;
    public TreeNode left,right;
};

static TreeNode newNode(int v)
{
    TreeNode temp = new TreeNode();
    temp.val = v;
    temp.left = temp.right = null;
    return temp;
}

// Function to check if the nodes
// are in increasing order or not
static bool isInc(TreeNode root)
{

    // Perform Level Order Traversal
    Queue<TreeNode> que = new Queue<TreeNode>();
    que.Enqueue(root);

    while (true)
    {

        // Current len of queue
        int len = que.Count;

        // If queue is empty
        if (len == 0)
            break;

        TreeNode pre = que.Peek();

        // Level order traversal
        while (len > 0)
        {

            // Pop element from
            // front of the queue
            TreeNode temp = que.Peek();
            que.Dequeue();

            // If previous value exceeds
            // current value, return false
            if (pre.val > temp.val)
                return false;

            pre = temp;
            if (temp.left != null)
                que.Enqueue(temp.left);

            if (temp.right != null)
                que.Enqueue(temp.right);

            len -= 1;
        }
    }
    return true;
}

// Function to print the Tree
// after modification
static void levelOrder(TreeNode root)
{

    // Performs level
    // order traversal
    Queue<TreeNode> que = new Queue<TreeNode>();
    que.Enqueue(root);

    while (true)
    {

        // Calculate size of the queue
        int len = que.Count;

        if (len == 0)
            break;

        // Iterate until queue is empty
        while (len > 0)
        {
            TreeNode temp = que.Peek();
            que.Dequeue();
            Console.Write(temp.val+" ");

            if (temp.left != null)
                que.Enqueue(temp.left);

            if (temp.right != null)
                que.Enqueue(temp.right);

            len -= 1;
        }
        Console.Write("\n");
    }
     Console.Write("\n");
}

// Function to arrange node values
// of each level in increasing order
static void makeInc(TreeNode root)
{

    // Perform level order traversal
    Queue<TreeNode> que = new Queue<TreeNode>();
    que.Enqueue(root);

    while (true)
    {

        // Calculate len of queue
        int len = que.Count;

        // If queue is empty
        if (len == 0)
            break;

        int prev = -1;

        // Level order traversal
        while (len > 0)
        {

            //cout<<"loop";

            // Pop element from
            // front of the queue
            TreeNode temp = que.Peek();
            que.Dequeue();

            // Initialize the optimal
            // element by the initial
            // element
            int optEle = temp.val;
            string strEle = optEle.ToString();

            // Check for all left
            // shift operations
            bool flag = true;
            int yy = strEle.Length;

            for(int idx = 0; idx < strEle.Length; idx++)
            {

                // Left shift
                string s1 = strEle.Substring(idx, yy - idx);
                string s2 = strEle.Substring(0, idx);
                string s = String.Concat(s1, s2);
                int ls = Int32.Parse(s);

                if (ls >= prev && flag)
                {
                    optEle = ls;
                    flag = false;
                }

                // If the current shifting
                // gives optimal solution
                if (ls >= prev)
                    optEle = Math.Min(optEle, ls);
            }

            // Replacing initial element
            // by the optimal element
            temp.val = optEle;
            prev = temp.val;

            // Push the LST
            if (temp.left != null)
                que.Enqueue(temp.left);

            // Push the RST
            if (temp.right != null)
                que.Enqueue(temp.right);

            len -= 1;
        }
    }

    // Print the result
    if (isInc(root) == true)
        levelOrder(root);
    else
        Console.Write(-1);
}

// Driver Code
public static void Main()
{
    TreeNode root = newNode(341);
    root.left = newNode(241);
    root.right = newNode(123);
    root.left.left = newNode(324);
    root.left.right = newNode(235);
    root.right.right = newNode(161);

    makeInc(root);
}
}

// This code is contributed by ipg2016107**
```

## ****java 描述语言****

```
**<script>
// Javascript program for the above approach

// TreeNode class
class Node
{
    constructor(v)
    {
        this.val=v;
        this.left=this.right=null;
    }
}

// Function to check if the nodes
// are in increasing order or not
function isInc(root)
{
    // Perform Level Order Traversal
    let que = [];
    que.push(root);

    while (true)
    {

        // Current len of queue
        let len = que.length;

        // If queue is empty
        if (len == 0)
            break;

        let pre = que[0];

        // Level order traversal
        while (len > 0)
        {

            // Pop element from
            // front of the queue
            let temp = que[0];
            que.shift();

            // If previous value exceeds
            // current value, return false
            if (pre.val > temp.val)
                return false;

            pre = temp;
            if (temp.left != null)
                que.push(temp.left);

            if (temp.right != null)
                que.push(temp.right);

            len -= 1;
        }
    }
    return true;
}

// Function to print the Tree
// after modification
function levelOrder(root)
{
    // Performs level
    // order traversal
    let que = [];
    que.push(root);

    while (true)
    {

        // Calculate size of the queue
        let len = que.length;

        if (len == 0)
            break;

        // Iterate until queue is empty
        while (len > 0)
        {
            let temp = que[0];
            que.shift();
            document.write(temp.val+" ");

            if (temp.left != null)
                que.push(temp.left);

            if (temp.right != null)
                que.push(temp.right);

            len -= 1;
        }
       document.write("<br>");
    }
    document.write("<br>");
}

// Function to arrange node values
// of each level in increasing order
function makeInc(root)
{
    // Perform level order traversal
    let que = [];
    que.push(root);

    while (true)
    {

        // Calculate len of queue
        let len = que.length;

        // If queue is empty
        if (len == 0)
            break;

        let prev = -1;

        // Level order traversal
        while (len > 0)
        {

            //cout<<"loop";

            // Pop element from
            // front of the queue
            let temp = que[0];
            que.shift();

            // Initialize the optimal
            // element by the initial
            // element
            let optEle = temp.val;
            let strEle = (optEle).toString();

            // Check for all left
            // shift operations
            let flag = true;
            let yy = strEle.length;

            for(let idx = 0; idx < strEle.length; idx++)
            {

                // Left shift
                let s1 = strEle.substring(idx, yy);
                let s2 = strEle.substring(0, idx);
                let s = s1+ s2;
                let ls = parseInt(s);

                if (ls >= prev && flag)
                {
                    optEle = ls;
                    flag = false;
                }

                // If the current shifting
                // gives optimal solution
                if (ls >= prev)
                    optEle = Math.min(optEle, ls);
            }

            // Replacing initial element
            // by the optimal element
            temp.val = optEle;
            prev = temp.val;

            // Push the LST
            if (temp.left != null)
                que.push(temp.left);

            // Push the RST
            if (temp.right != null)
                que.push(temp.right);

            len -= 1;
        }
    }

    // Print the result
    if (isInc(root) == true)
        levelOrder(root);
    else
       document.write(-1);
}

// Driver code
let root = new Node(341);
root.left = new Node(241);
root.right = new Node(123);
root.left.left = new Node(324);
root.left.right = new Node(235);
root.right.right = new Node(161);

makeInc(root);

// This code is contributed by patel2127
</script>**
```

******Output:** 

```
134 
124 231 
243 352 611
```**** 

*******时间复杂度:**O(N)*
T5**辅助空间:** O(N)****
# 二叉树每一级中二进制节点值的十进制等值之和

> 原文:[https://www . geeksforgeeks . org/二进制树的每一级中二进制节点值的十进制等值之和/](https://www.geeksforgeeks.org/sum-of-decimal-equivalents-of-binary-node-values-in-each-level-of-a-binary-tree/)

给定一个仅由值为 **0** 和 **1** 的节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)，任务是在每一级上找出由[从左到右连接同级节点](https://www.geeksforgeeks.org/connect-nodes-at-same-level/)形成的二进制数的[十进制等价数的总和。](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)

**示例:**

> **输入:**下面是给定的树:
> **0
> /\
> 1 0
> /\/\
> 0 1 1 1
> **输出:** 9
> **说明:**
> 1 级形成的二进制数为“0”，其十进制等价数为 0。
> 2 级形成的二进制数为“10”，其十进制等效值为 2。
> 三级形成的二进制数为“0111”，其十进制等效值为 7。
> 因此，总和= 0 + 2 + 7 = 9。**
> 
> ****输入:**下面是给定的树:
> **0
> /
> 1
> /\
> 1 0
> **输出:** 3****

******方法:**思路是使用[队列](https://www.geeksforgeeks.org/queue-data-structure/)执行[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)，找出每一级形成的数字之和。按照以下步骤解决问题:****

*   ****初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)，比如说 **Q** ，执行[级次遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)和一个变量，比如说 **ans** ，存储形成的数的和。****
*   ****[将**根节点**推至队列](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)T4q****
*   ****迭代直到[队列变空](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)**并执行以下步骤:

    *   迭代范围**【1，Q . size()】**[连接该级别](https://www.geeksforgeeks.org/connect-nodes-at-same-level/)的所有节点，并推送队列中各个节点的子节点 **Q** 。
    *   找到形成的二进制数的十进制等效值，并将该数加到**和**中。****** 
*   ****完成上述步骤后，打印**和**的值作为结果总和。****

****下面是上述方法的实现:****

## ****C++****

```
**// CPP program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a Tree Node
class TreeNode {
 public:
  int val;
  TreeNode *left, *right;

  TreeNode(int key) {
    val = key;
    left = right = NULL;
  }
};

// Function to convert binary number
// to its equivalent decimal value
int convertBinaryToDecimal(vector<int> arr) {
  int ans = 0;
  for (int i : arr) ans = (ans << 1) | i;

  return ans;
}

// Function to calculate sum of
// decimal equivalent of binary numbers
// of node values present at each level
void decimalEquilvalentAtEachLevel(TreeNode *root) {
  int ans = 0;

  queue<TreeNode *> que;

  // Push root node into queue
  que.push(root);

  while (true) {
    int length = que.size();
    if (length == 0) break;
    vector<int> eachLvl;

    // Connect nodes at the same
    // level to form a binary number
    while (length > 0) {
      TreeNode *temp = que.front();
      que.pop();

      // Append the value of the
      // current node to eachLvl
      eachLvl.push_back(temp->val);

      // Insert the Left child to
      // queue, if its not NULL
      if (temp->left != NULL) que.push(temp->left);

      // Insert the Right child to
      // queue, if its not NULL
      if (temp->right != NULL) que.push(temp->right);

      // Decrement length by one
      length -= 1;

      // Stores the front
      // element of the queue
    }

    // Add decimal equivalent of the
    // binary number formed on the
    // current level to ans
    ans += convertBinaryToDecimal(eachLvl);
  }

  // Finally print ans
  cout << ans << endl;
}

// Driver Code
int main()
{

  // Given Tree
  TreeNode *root = new TreeNode(0);
  root->left = new TreeNode(1);
  root->right = new TreeNode(0);
  root->left->left = new TreeNode(0);
  root->left->right = new TreeNode(1);
  root->right->left = new TreeNode(1);
  root->right->right = new TreeNode(1);

  // Function Call
  decimalEquilvalentAtEachLevel(root);

  return 0;
}

// This code is contributed by sanjeev2552**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach

import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

class GFG {

    // Structure of a Tree Node
    static class TreeNode {
        int val;
        TreeNode left, right;

        public TreeNode(int key) {
            val = key;
            left = right = null;
        }
    }

    // Function to convert binary number
    // to its equivalent decimal value
    static int convertBinaryToDecimal(ArrayList<Integer> arr) {
        int ans = 0;
        for (int i : arr)
            ans = (ans << 1) | i;

        return ans;

    }

    // Function to calculate sum of
    // decimal equivalent of binary numbers
    // of node values present at each level
    static void decimalEquilvalentAtEachLevel(TreeNode root) {

        int ans = 0;

        Queue<TreeNode> que = new LinkedList<>();

        // Push root node into queue
        que.add(root);

        while (true) {
            int length = que.size();
            if (length == 0)
                break;
            ArrayList<Integer> eachLvl = new ArrayList<>();

            // Connect nodes at the same
            // level to form a binary number
            while (length > 0) {

                TreeNode temp = que.poll();

                // Append the value of the
                // current node to eachLvl
                eachLvl.add(temp.val);

                // Insert the Left child to
                // queue, if its not NULL
                if (temp.left != null)
                    que.add(temp.left);

                // Insert the Right child to
                // queue, if its not NULL
                if (temp.right != null)
                    que.add(temp.right);

                // Decrement length by one
                length -= 1;

                // Stores the front
                // element of the queue
            }

            // Add decimal equivalent of the
            // binary number formed on the
            // current level to ans
            ans += convertBinaryToDecimal(eachLvl);
        }

        // Finally print ans
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args) {

        // Given Tree
        TreeNode root = new TreeNode(0);
        root.left = new TreeNode(1);
        root.right = new TreeNode(0);
        root.left.left = new TreeNode(0);
        root.left.right = new TreeNode(1);
        root.right.left = new TreeNode(1);
        root.right.right = new TreeNode(1);

        // Function Call
        decimalEquilvalentAtEachLevel(root);
    }

    // This code is contributed by sanjeev2552
}**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Structure of a Tree Node
class TreeNode:
    def __init__(self, val = 0,
                 left = None, right = None):
        self.val = val
        self.left = left
        self.right = right

# Function to convert binary number
# to its equivalent decimal value
def convertBinaryToDecimal(arr):

    ans = 0

    for i in arr:
        ans = (ans << 1) | i

    return ans

# Function to calculate sum of
# decimal equivalent of binary numbers
# of node values present at each level
def decimalEquilvalentAtEachLevel(root):

    ans = 0

    # Push root node into queue
    que = [root]

    while True:
        length = len(que)
        if not length:
            break
        eachLvl = []

        # Connect nodes at the same
        # level to form a binary number
        while length:

            # Stores the front
            # element of the queue
            temp = que.pop(0)

            # Append the value of the
            # current node to eachLvl
            eachLvl.append(temp.val)

            # Insert the Left child to
            # queue, if its not NULL
            if temp.left:
                que.append(temp.left)

            # Insert the Right child to
            # queue, if its not NULL
            if temp.right:
                que.append(temp.right)

            # Decrement length by one
            length -= 1

        # Add decimal equivalent of the
        # binary number formed on the
        # current level to ans
        ans += convertBinaryToDecimal(eachLvl)

    # Finally print ans
    print(ans)

# Driver Code

# Given Tree
root = TreeNode(0)
root.left = TreeNode(1)
root.right = TreeNode(0)
root.left.left = TreeNode(0)
root.left.right = TreeNode(1)
root.right.left = TreeNode(1)
root.right.right = TreeNode(1)

# Function Call
decimalEquilvalentAtEachLevel(root)**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

   // Structure of a Tree Node
class TreeNode{
  public int val;
  public TreeNode left,right;
};

static TreeNode newNode(int key){
  TreeNode temp = new TreeNode();
  temp.val = key;
  temp.left = temp.right = null;
  return temp;
}
// Function to convert binary number
// to its equivalent decimal value
static int convertBinaryToDecimal(List<int> arr)
{  
   int ans = 0;
    foreach(int i in arr)
        ans = (ans << 1) | i;

    return ans;

}

// Function to calculate sum of
// decimal equivalent of binary numbers
// of node values present at each level
static void decimalEquilvalentAtEachLevel(TreeNode root){

    int ans = 0;

    Queue<TreeNode> que = new Queue<TreeNode>();

    // Push root node into queue
    que.Enqueue(root);

    while(true){
       int length = que.Count;
        if (length == 0)
            break;
        List<int> eachLvl = new List<int>();

        // Connect nodes at the same
        // level to form a binary number
        while(length > 0){

          TreeNode temp = que.Peek();
          que.Dequeue();

            // Append the value of the
            // current node to eachLvl
            eachLvl.Add(temp.val);

            // Insert the Left child to
            // queue, if its not NULL
            if (temp.left != null)
                que.Enqueue(temp.left);

            // Insert the Right child to
            // queue, if its not NULL
            if (temp.right!=null)
                que.Enqueue(temp.right);

            // Decrement length by one
            length -= 1;

            // Stores the front
            // element of the queue
        }

        // Add decimal equivalent of the
        // binary number formed on the
        // current level to ans
        ans += convertBinaryToDecimal(eachLvl);
    }

    // Finally print ans
    Console.WriteLine(ans);
}

// Driver Code
public static void Main()
{

    // Given Tree
TreeNode root = newNode(0);
root.left = newNode(1);
root.right = newNode(0);
root.left.left = newNode(0);
root.left.right = newNode(1);
root.right.left = newNode(1);
root.right.right = newNode(1);

// Function Call
decimalEquilvalentAtEachLevel(root);
}
}

// This code is contributed by SURENDRA_GANGWAR.**
```

## ****java 描述语言****

```
**<script>

// JavaScript program for the above approach

   // Structure of a Tree Node
class TreeNode{

  constructor()
  {
    this.val = 0;
    this.left = null;
    this.right = null;
  }
};

function newNode( key){
  var temp = new TreeNode();
  temp.val = key;
  temp.left = temp.right = null;
  return temp;
}
// Function to convert binary number
// to its equivalent decimal value
function convertBinaryToDecimal(arr)
{  
   var ans = 0;
    for(var i of arr)
        ans = (ans << 1) | i;

    return ans;

}

// Function to calculate sum of
// decimal equivalent of binary numbers
// of node values present at each level
function decimalEquilvalentAtEachLevel( root){

    var ans = 0;

    var que = [];

    // Push root node into queue
    que.push(root);

    while(true){
       var length = que.length;
        if (length == 0)
            break;
        var eachLvl = [];

        // Connect nodes at the same
        // level to form a binary number
        while(length > 0){

          var temp = que[0];
          que.shift();

            // Append the value of the
            // current node to eachLvl
            eachLvl.push(temp.val);

            // Insert the Left child to
            // queue, if its not NULL
            if (temp.left != null)
                que.push(temp.left);

            // Insert the Right child to
            // queue, if its not NULL
            if (temp.right!=null)
                que.push(temp.right);

            // Decrement length by one
            length -= 1;

            // Stores the front
            // element of the queue
        }

        // Add decimal equivalent of the
        // binary number formed on the
        // current level to ans
        ans += convertBinaryToDecimal(eachLvl);
    }

    // Finally print ans
    document.write(ans);
}

// Driver Code

// Given Tree
var root = newNode(0);
root.left = newNode(1);
root.right = newNode(0);
root.left.left = newNode(0);
root.left.right = newNode(1);
root.right.left = newNode(1);
root.right.right = newNode(1);

// Function Call
decimalEquilvalentAtEachLevel(root);

</script>**
```

******Output:** 

```
9
```**** 

*******时间复杂度:**O(N)*
T5**辅助空间:** O(1)****
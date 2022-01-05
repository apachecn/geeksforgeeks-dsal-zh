# 检查二叉树的最大和级别是否将树分成两个相等的和部分

> 原文:[https://www . geesforgeks . org/check-if-max-sum-level-of-二叉树-将树分成两个相等的半和/](https://www.geeksforgeeks.org/check-if-max-sum-level-of-binary-tree-divides-tree-into-two-equal-sum-halves/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是检查最大和水平是否将二叉树分成两个相等和的两部分。
**例:**

```
Input: 
                1 
              /   \ 
             2      3 
           /  \      \ 
          4    5      8 
                    /   \ 
                   2     4 
Output: YES
Explanation:
The maximum sum level is 2 and 
its sum is (4 + 5 + 8 = 17)
Sum of the upper half (1 + 2 + 3) = 6
Sum of the Lower half (2 + 4) = 6

Input:
                10 
              /    \ 
             20     30 
            /  \      \ 
           4    5      1 
Output: YES
Explanation:
The maximum sum level is 1 and 
its sum is (20 + 30 = 50)
Sum of the upper half (10) = 10
Sum of the lower half (5 + 4 + 1) = 10
```

**方法:**思路是用[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)计算二叉树每一级的和。然后，求所有级别的最大和。最后，检查小于最大级别总和的所有级别的总和是否等于大于最大级别总和的级别的总和。

下面是上述方法的实现:

## C++

```
// C++ implementation to check if
// maximum level sum divides the
// Binary tree into two equal sum halves

#include <bits/stdc++.h>
using namespace std;

// Structure of the node
struct Node {
    int data;
    struct Node *left, *right;
};

// Utility function to
// create a new node
struct Node* newNode(int x)
{
    struct Node* temp = new Node;
    temp->data = x;
    temp->left = temp->right = NULL;
    return temp;
};

// Function to  check if
// maximum level sum divides the
// Binary tree into two equal sum halves
bool check_horizontal(struct Node* root)
{
    // Vector used to store the sum
    // of all levels of the Binary Tree
    vector<int> sumLevel;

    // In index variable we store the
    // level of the maximum level sum
    int index = -1, maxSum = 0, level = 0;

    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {

        // Variable to store the
        // current level sum.
        int sum = 0;

        // Size of the Queue
        int n = q.size();

        // Loop to iterate over the
        // elements nodes of current level
        for (int i = 0; i < n; i++) {

            // Inserting the next level
            // elements to the Queue
            Node* temp = q.front();
            sum += temp->data;
            if (temp->left != NULL)
                q.push(temp->left);
            if (temp->right != NULL)
                q.push(temp->right);

            // Popping out the current
            // level element from the Queue
            q.pop();
        }

        // Storing the current level
        // sum into the vector
        sumLevel.push_back(sum);

        // Level of maximum
        // horizontal sum line
        if (sum > maxSum) {
            maxSum = sum;
            index = level;
        }
        level++;
    }
    // Find the left half and right
    // half sum and check if they are equal
    int leftSum = 0, rightSum = 0;
    for (int i = 0; i < index; i++) {
        leftSum += sumLevel[i];
    }

    for (int i = index + 1;
         i < sumLevel.size(); i++) {
        rightSum += sumLevel[i];
    }
    return (leftSum == rightSum);
}

// Driver Code
int main()
{

    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(8);
    root->right->right->left = newNode(2);
    root->right->right->right = newNode(4);

    // Condition to check if the
    // maxumum sum level divides
    // it into two equal half
    if (check_horizontal(root))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if
// maximum level sum divides the
// Binary tree into two equal sum halves
import java.util.*;

class GFG{

// Structure of the node
static class Node
{
    int data;
    Node left, right;
};

// Utility function to
// create a new node
static Node newNode(int x)
{
    Node temp = new Node();
    temp.data = x;
    temp.left = temp.right = null;
    return temp;
};

// Function to  check if maximum
// level sum divides the Binary
// tree into two equal sum halves
static boolean check_horizontal(Node root)
{

    // Vector used to store the sum
    // of all levels of the Binary Tree
    Vector<Integer> sumLevel = new Vector<Integer>();

    // In index variable we store the
    // level of the maximum level sum
    int index = -1, maxSum = 0, level = 0;

    Queue<Node> q = new LinkedList<Node>();
    q.add(root);

    while (!q.isEmpty())
    {

        // Variable to store the
        // current level sum.
        int sum = 0;

        // Size of the Queue
        int n = q.size();

        // Loop to iterate over the
        // elements nodes of current level
        for(int i = 0; i < n; i++)
        {

            // Inserting the next level
            // elements to the Queue
            Node temp = q.peek();
            sum += temp.data;

            if (temp.left != null)
                q.add(temp.left);
            if (temp.right != null)
                q.add(temp.right);

            // Popping out the current
            // level element from the Queue
            q.remove();
        }

        // Storing the current level
        // sum into the vector
        sumLevel.add(sum);

        // Level of maximum
        // horizontal sum line
        if (sum > maxSum)
        {
            maxSum = sum;
            index = level;
        }
        level++;
    }

    // Find the left half and right
    // half sum and check if they are equal
    int leftSum = 0, rightSum = 0;
    for(int i = 0; i < index; i++)
    {
        leftSum += sumLevel.get(i);
    }

    for(int i = index + 1;
            i < sumLevel.size(); i++)
    {
        rightSum += sumLevel.get(i);
    }
    return (leftSum == rightSum);
}

// Driver Code
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(8);
    root.right.right.left = newNode(2);
    root.right.right.right = newNode(4);

    // Condition to check if the
    // maxumum sum level divides
    // it into two equal half
    if (check_horizontal(root))
        System.out.print("YES" + "\n");
    else
        System.out.print("NO" + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python 3 implementation to
# check if maximum level sum
# divides the Binary tree into
# two equal sum halves

# Structure of the node
class newNode:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

# Function to  check if
# maximum level sum divides
# the Binary tree into two
# equal sum halves
def check_horizontal(root):

    # Vector used to store the sum
    # of all levels of the Binary Tree
    sumLevel = []

    # In index variable we store the
    # level of the maximum level sum
    index = -1
    maxSum = 0
    level = 0

    q = []
    q.append(root)

    while (len(q)):

        # Variable to store the
        # current level sum.
        sum = 0

        # Size of the Queue
        n = len(q)

        # Loop to iterate over the
        # elements nodes of current
        # level
        for i in range(n):

            # Inserting the next level
            # elements to the Queue
            temp = q[0]
            sum += temp.data
            if (temp.left != None):
                q.append(temp.left)
            if (temp.right != None):
                q.append(temp.right)

            # Popping out the current
            # level element from the
            # Queue
            q.remove(q[0])

        # Storing the current level
        # sum into the vector
        sumLevel.append(sum)

        # Level of maximum
        # horizontal sum line
        if (sum > maxSum):
            maxSum = sum
            index = level
        level += 1

    # Find the left half and right
    # half sum and check if they
    # are equal
    leftSum = 0
    rightSum = 0

    for i in range(index):
        leftSum += sumLevel[i]

    for i in range(index + 1,
                   len(sumLevel), 1):
        rightSum += sumLevel[i]

    return (leftSum == rightSum)

# Driver Code
if __name__ == '__main__':

    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.right = newNode(8)
    root.right.right.left = newNode(2)
    root.right.right.right = newNode(4)

    # Condition to check if the
    # maxumum sum level divides
    # it into two equal half
    if (check_horizontal(root)):
        print("YES")
    else:
        print("NO")

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# implementation to check if
// maximum level sum divides the
// Binary tree into two equal sum halves
using System;
using System.Collections.Generic;
class GFG{

// Structure of
// the node
public class Node
{
  public int data;
  public Node left, right;
};

// Utility function to
// create a new node
static Node newNode(int x)
{
  Node temp = new Node();
  temp.data = x;
  temp.left = temp.right = null;
  return temp;
}

// Function to  check if maximum
// level sum divides the Binary
// tree into two equal sum halves
static bool check_horizontal(Node root)
{
  // List used to store the sum
  // of all levels of the Binary Tree
  List<int> sumLevel = new List<int>();

  // In index variable we store the
  // level of the maximum level sum
  int index = -1, maxSum = 0, level = 0;

  Queue<Node> q = new Queue<Node>();
  q.Enqueue(root);

  while (q.Count != 0)
  {
    // Variable to store the
    // current level sum.
    int sum = 0;

    // Size of the Queue
    int n = q.Count;

    // Loop to iterate over the
    // elements nodes of current level
    for(int i = 0; i < n; i++)
    {
      // Inserting the next level
      // elements to the Queue
      Node temp = q.Peek();
      sum += temp.data;

      if (temp.left != null)
        q.Enqueue(temp.left);
      if (temp.right != null)
        q.Enqueue(temp.right);

      // Popping out the current
      // level element from the Queue
      q.Dequeue();
    }

    // Storing the current level
    // sum into the vector
    sumLevel.Add(sum);

    // Level of maximum
    // horizontal sum line
    if (sum > maxSum)
    {
      maxSum = sum;
      index = level;
    }

    level++;
  }

  // Find the left half and right
  // half sum and check if they are equal
  int leftSum = 0, rightSum = 0;
  for(int i = 0; i < index; i++)
  {
    leftSum += sumLevel[i];
  }

  for(int i = index + 1;
          i < sumLevel.Count; i++)
  {
    rightSum += sumLevel[i];
  }
  return (leftSum == rightSum);
}

// Driver Code
public static void Main(String[] args)
{
  Node root = newNode(1);
  root.left = newNode(2);
  root.right = newNode(3);
  root.left.left = newNode(4);
  root.left.right = newNode(5);
  root.right.right = newNode(8);
  root.right.right.left = newNode(2);
  root.right.right.right = newNode(4);

  // Condition to check if the
  // maxumum sum level divides
  // it into two equal half
  if (check_horizontal(root))
    Console.Write("YES" + "\n");
  else
    Console.Write("NO" + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // JavaScript implementation to check if
      // maximum level sum divides the
      // Binary tree into two equal sum halves
      // Structure of
      // the node
      class Node {
        constructor() {
          this.data = 0;
          this.left = null;
          this.right = null;
        }
      }

      // Utility function to
      // create a new node
      function newNode(x) {
        var temp = new Node();
        temp.data = x;
        temp.left = temp.right = null;
        return temp;
      }

      // Function to check if maximum
      // level sum divides the Binary
      // tree into two equal sum halves
      function check_horizontal(root) {
        // List used to store the sum
        // of all levels of the Binary Tree
        var sumLevel = [];

        // In index variable we store the
        // level of the maximum level sum
        var index = -1,
          maxSum = 0,
          level = 0;

        var q = [];
        q.push(root);

        while (q.length != 0) {
          // Variable to store the
          // current level sum.
          var sum = 0;

          // Size of the Queue
          var n = q.length;

          // Loop to iterate over the
          // elements nodes of current level
          for (var i = 0; i < n; i++) {
            // Inserting the next level
            // elements to the Queue
            var temp = q[0];
            sum += temp.data;

            if (temp.left != null) q.push(temp.left);
            if (temp.right != null) q.push(temp.right);

            // Popping out the current
            // level element from the Queue
            q.shift();
          }

          // Storing the current level
          // sum into the vector
          sumLevel.push(sum);

          // Level of maximum
          // horizontal sum line
          if (sum > maxSum) {
            maxSum = sum;
            index = level;
          }

          level++;
        }

        // Find the left half and right
        // half sum and check if they are equal
        var leftSum = 0,
          rightSum = 0;
        for (var i = 0; i < index; i++) {
          leftSum += sumLevel[i];
        }

        for (var i = index + 1; i < sumLevel.length; i++) {
          rightSum += sumLevel[i];
        }
        return leftSum == rightSum;
      }

      // Driver Code
      var root = newNode(1);
      root.left = newNode(2);
      root.right = newNode(3);
      root.left.left = newNode(4);
      root.left.right = newNode(5);
      root.right.right = newNode(8);
      root.right.right.left = newNode(2);
      root.right.right.right = newNode(4);

      // Condition to check if the
      // maxumum sum level divides
      // it into two equal half
      if (check_horizontal(root)) document.write("YES" + "<br>");
      else document.write("NO" + "<br>");

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
YES
```
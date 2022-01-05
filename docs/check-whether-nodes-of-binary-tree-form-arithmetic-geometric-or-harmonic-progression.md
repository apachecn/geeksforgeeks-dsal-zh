# 检查二叉树节点是否形成算术、几何或调和级数

> 原文:[https://www . geeksforgeeks . org/check-二叉树形式的节点-算术-几何-或-调和-级数/](https://www.geeksforgeeks.org/check-whether-nodes-of-binary-tree-form-arithmetic-geometric-or-harmonic-progression/)

给定一个 [**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) ，任务是检查这个树上的节点是形成[等差级数](https://www.geeksforgeeks.org/arithmetic-progression/)、[几何级数](https://www.geeksforgeeks.org/geometric-progression/)还是[调和级数](https://www.geeksforgeeks.org/harmonic-progression/)。
**举例:**

```
Input:               
                      4
                    /   \
                   2     16
                  / \    / \
                 1   8  64  32
Output: Geometric Progression
Explanation:
The nodes of the binary tree can be used
to form a Geometric Progression as follows - 
{1, 2, 4, 8, 16, 32, 64}

Input:          
                 15
               /   \
              5     10
             / \      \
            25   35   20
Output: Arithmetic Progression
Explanation:
The nodes of the binary tree can be used
to form a Arithmetic Progression as follows - 
{5, 10, 15, 20, 25, 35}
```

**方法:**想法是[使用水平顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)遍历二叉树，并将所有节点存储在一个数组中，然后检查该数组是否可以用于形成[算术、几何或调和级数](https://www.geeksforgeeks.org/progressions-ap-gp-hp/)。

*   检查一个序列是否在[](https://www.geeksforgeeks.org/arithmetic-progression/)**等差数列中，对序列进行排序，检查数组中连续元素之间的公共差是否相同。**
*   **要检查序列是否处于 [**几何级数**](https://www.geeksforgeeks.org/geometric-progression/) 中，请对序列进行排序，并检查数组中连续元素之间的公共比率是否相同。**
*   **检查一个序列是否处于 [**调和级数**](https://www.geeksforgeeks.org/harmonic-progression/) 中，找到每个元素的倒数，然后对数组进行排序，检查连续元素之间的公共差是否相同。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation to check that
// nodes of binary tree form AP/GP/HP

#include <bits/stdc++.h>
using namespace std;

// Structure of the
// node of the binary tree
struct Node {
    int data;
    struct Node *left, *right;
};

// Function to find the size
// of the Binary Tree
int size(Node* node)
{
    // Base Case
    if (node == NULL)
        return 0;
    else
        return (size(node->left) + 1 + size(node->right));
}

// Function to check if the permutation
// of the sequence form Arithmetic Progression
bool checkIsAP(double arr[], int n)
{
    // If the sequence contains
    // only one element
    if (n == 1)
        return true;

    // Sorting the array
    sort(arr, arr + n);

    double d = arr[1] - arr[0];

    // Loop to check if the sequence
    // have same common difference
    // between its consecutive elements
    for (int i = 2; i < n; i++)
        if (arr[i] - arr[i - 1] != d)
            return false;

    return true;
}

// Function to check if the permutation
// of the sequence form
// Geometric progression
bool checkIsGP(double arr[], int n)
{
    // Condition when the length
    // of the sequence is 1
    if (n == 1)
        return true;

    // Sorting the array
    sort(arr, arr + n);
    double r = arr[1] / arr[0];

    // Loop to check if the the
    // sequence have same common
    // ratio in consecutive elements
    for (int i = 2; i < n; i++) {
        if (arr[i] / arr[i - 1] != r)
            return false;
    }
    return true;
}

// Function to check if the permutation
// of the sequence form
// Harmonic Progression
bool checkIsHP(double arr[], int n)
{
    // Condition when length of
    // sequence in 1
    if (n == 1) {
        return true;
    }
    double rec[n];

    // Loop to find the reciprocal
    // of the sequence
    for (int i = 0; i < n; i++) {
        rec[i] = ((1 / arr[i]));
    }

    // Sorting the array
    sort(rec, rec + n);
    double d = (rec[1]) - (rec[0]);

    // Loop to check if the common
    // difference of the sequence is same
    for (int i = 2; i < n; i++) {
        if (rec[i] - rec[i - 1] != d) {
            return false;
        }
    }
    return true;
}

// Function to check if the nodes
// of the Binary tree forms AP/GP/HP
void checktype(Node* root)
{

    int n = size(root);
    double arr[n];
    int i = 0;

    // Base Case
    if (root == NULL)
        return;

    // Create an empty queue
    // for level order traversal
    queue<Node*> q;

    // Enqueue Root and initialize height
    q.push(root);

    // Loop to traverse the tree using
    // Level order Traversal
    while (q.empty() == false) {
        Node* node = q.front();
        arr[i] = node->data;
        i++;
        q.pop();

        // Enqueue left child
        if (node->left != NULL)
            q.push(node->left);

        // Enqueue right child
        if (node->right != NULL)
            q.push(node->right);
    }

    int flag = 0;

    // Condition to check if the
    // sequence form Arithmetic Progression
    if (checkIsAP(arr, n)) {
        cout << "Arithmetic Progression"
             << endl;
        flag = 1;
    }

    // Condition to check if the
    // sequence form Geometric Progression
    else if (checkIsGP(arr, n)) {
        cout << "Geometric Progression"
             << endl;
        flag = 1;
    }

    // Condition to check if the
    // sequence form Geometric Progression
    else if (checkIsHP(arr, n)) {
        cout << "Geometric Progression"
             << endl;
        flag = 1;
    }
    else if (flag == 0) {
        cout << "No";
    }
}

// Function to create new node
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Driver Code
int main()
{
    /* Constructed Binary tree is:
             1
            / \
           2   3
          / \   \
         4   5   8
                / \
                6  7
    */
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(8);
    root->right->right->left = newNode(6);
    root->right->right->right = newNode(7);

    checktype(root);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation to check that
// nodes of binary tree form AP/GP/HP
import java.util.*;

class GFG {
    // Structure of the
    // node of the binary tree
    static class Node {
        int data;
        Node left, right;

        Node(int data) {
            this.data = data;
            this.left = this.right = null;
        }
    };

    // Function to find the size
    // of the Binary Tree
    static int size(Node node) {
        // Base Case
        if (node == null)
            return 0;
        else
            return (size(node.left) + 1 + size(node.right));
    }

    // Function to check if the permutation
    // of the sequence form Arithmetic Progression
    static boolean checkIsAP(double[] arr, int n) {
        // If the sequence contains
        // only one element
        if (n == 1)
            return true;

        // Sorting the array
        Arrays.sort(arr);

        double d = arr[1] - arr[0];

        // Loop to check if the sequence
        // have same common difference
        // between its consecutive elements
        for (int i = 2; i < n; i++)
            if (arr[i] - arr[i - 1] != d)
                return false;

        return true;
    }

    // Function to check if the permutation
    // of the sequence form
    // Geometric progression
    static boolean checkIsGP(double[] arr, int n) {
        // Condition when the length
        // of the sequence is 1
        if (n == 1)
            return true;

        // Sorting the array
        Arrays.sort(arr);
        double r = arr[1] / arr[0];

        // Loop to check if the the
        // sequence have same common
        // ratio in consecutive elements
        for (int i = 2; i < n; i++) {
            if (arr[i] / arr[i - 1] != r)
                return false;
        }
        return true;
    }

    // Function to check if the permutation
    // of the sequence form
    // Harmonic Progression
    static boolean checkIsHP(double[] arr, int n) {
        // Condition when length of
        // sequence in 1
        if (n == 1) {
            return true;
        }
        double[] rec = new double[n];

        // Loop to find the reciprocal
        // of the sequence
        for (int i = 0; i < n; i++) {
            rec[i] = ((1 / arr[i]));
        }

        // Sorting the array
        Arrays.sort(rec);
        double d = (rec[1]) - (rec[0]);

        // Loop to check if the common
        // difference of the sequence is same
        for (int i = 2; i < n; i++) {
            if (rec[i] - rec[i - 1] != d) {
                return false;
            }
        }
        return true;
    }

    // Function to check if the nodes
    // of the Binary tree forms AP/GP/HP
    static void checktype(Node root) {

        int n = size(root);
        double[] arr = new double[n];
        int i = 0;

        // Base Case
        if (root == null)
            return;

        // Create an empty queue
        // for level order traversal
        Queue<Node> q = new LinkedList<>();

        // Enqueue Root and initialize height
        q.add(root);

        // Loop to traverse the tree using
        // Level order Traversal
        while (q.isEmpty() == false) {
            Node node = q.poll();
            arr[i] = node.data;
            i++;

            // Enqueue left child
            if (node.left != null)
                q.add(node.left);

            // Enqueue right child
            if (node.right != null)
                q.add(node.right);
        }

        int flag = 0;

        // Condition to check if the
        // sequence form Arithmetic Progression
        if (checkIsAP(arr, n)) {
            System.out.println("Arithmetic Progression");
            flag = 1;
        }

        // Condition to check if the
        // sequence form Geometric Progression
        else if (checkIsGP(arr, n)) {
            System.out.println("Geometric Progression");
            flag = 1;
        }

        // Condition to check if the
        // sequence form Geometric Progression
        else if (checkIsHP(arr, n)) {
            System.out.println("Geometric Progression");
            flag = 1;
        } else if (flag == 0) {
            System.out.println("No");
        }
    }

    // Driver Code
    public static void main(String[] args) {

        /* Constructed Binary tree is:
                 1
                / \
               2   3
              / \   \
             4   5   8
                    / \
                   6   7
        */
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.right = new Node(8);
        root.right.right.left = new Node(6);
        root.right.right.right = new Node(7);

        checktype(root);
    }
}

// This code is contributed by
// sanjeev2552
```

## **C#**

```
// C# implementation to check that
// nodes of binary tree form AP/GP/HP
using System;
using System.Collections.Generic;

public class GFG {
    // Structure of the
    // node of the binary tree
    public class Node {
        public int data;
        public Node left, right;

        public Node(int data) {
            this.data = data;
            this.left = this.right = null;
        }
    };

    // Function to find the size
    // of the Binary Tree
    static int size(Node node) {
        // Base Case
        if (node == null)
            return 0;
        else
            return (size(node.left) + 1 + size(node.right));
    }

    // Function to check if the permutation
    // of the sequence form Arithmetic Progression
    static bool checkIsAP(double[] arr, int n) {
        // If the sequence contains
        // only one element
        if (n == 1)
            return true;

        // Sorting the array
        Array.Sort(arr);

        double d = arr[1] - arr[0];

        // Loop to check if the sequence
        // have same common difference
        // between its consecutive elements
        for (int i = 2; i < n; i++)
            if (arr[i] - arr[i - 1] != d)
                return false;

        return true;
    }

    // Function to check if the permutation
    // of the sequence form
    // Geometric progression
    static bool checkIsGP(double[] arr, int n) {
        // Condition when the length
        // of the sequence is 1
        if (n == 1)
            return true;

        // Sorting the array
        Array.Sort(arr);
        double r = arr[1] / arr[0];

        // Loop to check if the the
        // sequence have same common
        // ratio in consecutive elements
        for (int i = 2; i < n; i++) {
            if (arr[i] / arr[i - 1] != r)
                return false;
        }
        return true;
    }

    // Function to check if the permutation
    // of the sequence form
    // Harmonic Progression
    static bool checkIsHP(double[] arr, int n) {
        // Condition when length of
        // sequence in 1
        if (n == 1) {
            return true;
        }
        double[] rec = new double[n];

        // Loop to find the reciprocal
        // of the sequence
        for (int i = 0; i < n; i++) {
            rec[i] = ((1 / arr[i]));
        }

        // Sorting the array
        Array.Sort(rec);
        double d = (rec[1]) - (rec[0]);

        // Loop to check if the common
        // difference of the sequence is same
        for (int i = 2; i < n; i++) {
            if (rec[i] - rec[i - 1] != d) {
                return false;
            }
        }
        return true;
    }

    // Function to check if the nodes
    // of the Binary tree forms AP/GP/HP
    static void checktype(Node root) {

        int n = size(root);
        double[] arr = new double[n];
        int i = 0;

        // Base Case
        if (root == null)
            return;

        // Create an empty queue
        // for level order traversal
        Queue<Node> q = new Queue<Node>();

        // Enqueue Root and initialize height
        q.Enqueue(root);

        // Loop to traverse the tree using
        // Level order Traversal
        while (q.Count!=0 == false) {
            Node node = q.Dequeue();
            arr[i] = node.data;
            i++;

            // Enqueue left child
            if (node.left != null)
                q.Enqueue(node.left);

            // Enqueue right child
            if (node.right != null)
                q.Enqueue(node.right);
        }

        int flag = 0;

        // Condition to check if the
        // sequence form Arithmetic Progression
        if (checkIsAP(arr, n)) {
            Console.WriteLine("Arithmetic Progression");
            flag = 1;
        }

        // Condition to check if the
        // sequence form Geometric Progression
        else if (checkIsGP(arr, n)) {
            Console.WriteLine("Geometric Progression");
            flag = 1;
        }

        // Condition to check if the
        // sequence form Geometric Progression
        else if (checkIsHP(arr, n)) {
            Console.WriteLine("Geometric Progression");
            flag = 1;
        } else if (flag == 0) {
            Console.WriteLine("No");
        }
    }

    // Driver Code
    public static void Main(String[] args) {

        /* Constructed Binary tree is:
                 1
                / \
               2   3
              / \   \
             4   5   8
                    / \
                   6   7
        */
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.right = new Node(8);
        root.right.right.left = new Node(6);
        root.right.right.right = new Node(7);

        checktype(root);
    }
}
// This code contributed by sapnasingh4991
```

## **java 描述语言**

```
<script>

    // JavaScript implementation to check that
    // nodes of binary tree form AP/GP/HP

    // Structure of the
    // node of the binary tree
    class Node {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to find the size
    // of the Binary Tree
    function size(node) {
        // Base Case
        if (node == null)
            return 0;
        else
            return (size(node.left) + 1 + size(node.right));
    }

    // Function to check if the permutation
    // of the sequence form Arithmetic Progression
    function checkIsAP(arr, n) {
        // If the sequence contains
        // only one element
        if (n == 1)
            return true;

        // Sorting the array
        arr.sort();

        let d = arr[1] - arr[0];

        // Loop to check if the sequence
        // have same common difference
        // between its consecutive elements
        for (let i = 2; i < n; i++)
            if (arr[i] - arr[i - 1] != d)
                return false;

        return true;
    }

    // Function to check if the permutation
    // of the sequence form
    // Geometric progression
    function checkIsGP(arr, n) {
        // Condition when the length
        // of the sequence is 1
        if (n == 1)
            return true;

        // Sorting the array
        arr.sort();
        let r = arr[1] / arr[0];

        // Loop to check if the the
        // sequence have same common
        // ratio in consecutive elements
        for (let i = 2; i < n; i++) {
            if (arr[i] / arr[i - 1] != r)
                return false;
        }
        return true;
    }

    // Function to check if the permutation
    // of the sequence form
    // Harmonic Progression
    function checkIsHP(arr, n) {
        // Condition when length of
        // sequence in 1
        if (n == 1) {
            return true;
        }
        let rec = new Array(n);

        // Loop to find the reciprocal
        // of the sequence
        for (let i = 0; i < n; i++) {
            rec[i] = ((1 / arr[i]));
        }

        // Sorting the array
        rec.sort();
        let d = (rec[1]) - (rec[0]);

        // Loop to check if the common
        // difference of the sequence is same
        for (let i = 2; i < n; i++) {
            if (rec[i] - rec[i - 1] != d) {
                return false;
            }
        }
        return true;
    }

    // Function to check if the nodes
    // of the Binary tree forms AP/GP/HP
    function checktype(root) {

        let n = size(root);
        let arr = new Array(n);
        let i = 0;

        // Base Case
        if (root == null)
            return;

        // Create an empty queue
        // for level order traversal
        let q = [];

        // Enqueue Root and initialize height
        q.push(root);

        // Loop to traverse the tree using
        // Level order Traversal
        while (q.length > 0) {
            let node = q[0];
            q.shift();
            arr[i] = node.data;
            i++;

            // Enqueue left child
            if (node.left != null)
                q.push(node.left);

            // Enqueue right child
            if (node.right != null)
                q.push(node.right);
        }

        let flag = 0;

        // Condition to check if the
        // sequence form Arithmetic Progression
        if (checkIsAP(arr, n)) {
            document.write("Arithmetic Progression");
            flag = 1;
        }

        // Condition to check if the
        // sequence form Geometric Progression
        else if (checkIsGP(arr, n)) {
            document.write("Geometric Progression");
            flag = 1;
        }

        // Condition to check if the
        // sequence form Geometric Progression
        else if (checkIsHP(arr, n)) {
            document.write("Geometric Progression");
            flag = 1;
        } else if (flag == 0) {
            document.write("No");
        }
    }

    /* Constructed Binary tree is:
                   1
                  / \
                 2   3
                / \   \
               4   5   8
                      / \
                     6   7
          */
    let root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.right = new Node(8);
    root.right.right.left = new Node(6);
    root.right.right.right = new Node(7);

    checktype(root);

</script>
```

****Output:** 

```
Arithmetic Progression
```** 

****业绩分析:**** 

*   ****时间复杂度:**和上面的方法一样，遍历节点并对其进行排序，在最坏的情况下需要 O(N*logN)个时间。因此时间复杂度将是 **O(N*logN)** 。**
*   ****辅助空间复杂度:**和上面的方法一样，有额外的空间用来存储节点的数据。因此辅助空间的复杂性将是 **O(N)** 。**
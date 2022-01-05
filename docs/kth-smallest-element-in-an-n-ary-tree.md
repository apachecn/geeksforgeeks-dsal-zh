# N 元树中的第几个最小元素

> 原文:[https://www . geesforgeks . org/kth-n 元树中最小元素/](https://www.geeksforgeeks.org/kth-smallest-element-in-an-n-ary-tree/)

给定一个 [N 数组树(类属树)](https://www.geeksforgeeks.org/generic-treesn-array-trees/)和一个整数 **K** ，任务是在 [N 数组树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)中找到 **K <sup>第</sup>T7】个最小**个**元素。**

**示例:**

> **输入:**10
> /\ \
> 2 34 56 100
> /\ |/| \
> 77 88 1 7 8 9
> K = 3
> **输出:** 7
> **说明:** 7 是树中第三小的元素。前两个最小的元素分别是 1 和 2。
> 
> **输入:**1
> /\ \
> 2 3 4
> /\
> 5 6
> K = 4
> T8】输出 : 4

**方法:**在给定的范围内 **K** 次找到最小元素，并不断更新范围的上限到目前为止找到的最小元素，就可以解决这个问题。按照以下步骤解决问题:

*   初始化一个全局变量，说 **MinimumElement** 为 **INT_MAX** 。
*   声明一个函数 **smallestEleUnderRange(根，数据)**，并执行以下操作:
    *   如果**根数据**大于**数据**，则更新**微量元素**为**微量元素**和**根数据**的 [min](https://www.geeksforgeeks.org/stdmin_element-in-cpp/)
    *   迭代**根**的所有子级。调用[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **smallestEleUnderRange(子，数据)。**
*   声明一个函数**kthsmalletelement(根，k)** 来执行以下操作:
    *   初始化一个变量，说 **ans** 为 **INT_MIN** ，存储**K<sup>th</sup>T7】最小元素**。****
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K–1】**，并执行以下操作:
        *   调用 **smallestEleUnderRange(root，ans)** 函数，然后将 **ans** 更新为 **MinimumElement** ，再将 **MinimumElement** 更新为 **INT_MAX。**
    *   最后打印 **ans** 作为所需答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a node
class Node {
public:
    int data;
    vector<Node*> childs;
};

// Global variable set to Maximum
int MinimumElement = INT_MAX;

// Function that gives the smallest
// element under the range of key
void smallestEleUnderRange(Node* root,
                           int data)
{
    if (root->data > data) {
        MinimumElement = min(
            root->data, MinimumElement);
    }
    for (Node* child : root->childs) {
        smallestEleUnderRange(child, data);
    }
}

// Function to find the Kth smallest element
int kthSmallestElement(Node* root, int k)
{
    int ans = INT_MIN;
    for (int i = 0; i < k; i++) {
        smallestEleUnderRange(root, ans);
        ans = MinimumElement;
        MinimumElement = INT_MAX;
    }
    return ans;
}

// Function to create a new node
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    return temp;
}

// Driver Code
int main()
{
    /*   Let us create below tree
     *              10
     *        /   /    \   \
     *        2  34    56   100
     *       / \         |   /  | \
     *      77  88       1   7  8  9
     */

    Node* root = newNode(10);
    (root->childs).push_back(newNode(2));
    (root->childs).push_back(newNode(34));
    (root->childs).push_back(newNode(56));
    (root->childs).push_back(newNode(100));
    (root->childs[0]->childs).push_back(newNode(77));
    (root->childs[0]->childs).push_back(newNode(88));
    (root->childs[2]->childs).push_back(newNode(1));
    (root->childs[3]->childs).push_back(newNode(7));
    (root->childs[3]->childs).push_back(newNode(8));
    (root->childs[3]->childs).push_back(newNode(9));

    cout << kthSmallestElement(root, 3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Class containing left and
    // right child of current
    // node and key value
    static class Node {

        public int data;
        public Vector<Node> childs;

        public Node(int data)
        {
            this.data = data;
            childs = new Vector<Node>();
        }
    }

    // Global variable set to Maximum
    static int MinimumElement = Integer.MAX_VALUE;

    // Function that gives the smallest
    // element under the range of key
    static void smallestEleUnderRange(Node root, int data)
    {
        if (root.data > data) {
            MinimumElement = Math.min(root.data, MinimumElement);
        }
        for(Node child : root.childs) {
            smallestEleUnderRange(child, data);
        }
    }

    // Function to find the Kth smallest element
    static int kthSmallestElement(Node root, int k)
    {
        int ans = Integer.MIN_VALUE;
        for (int i = 0; i < k; i++) {
            smallestEleUnderRange(root, ans);
            ans = MinimumElement;
            MinimumElement = Integer.MAX_VALUE;
        }
        return ans;
    }

    // Function to create a new node
    static Node newNode(int data)
    {
        Node temp = new Node(data);
        return temp;
    }

    public static void main(String[] args) {
        /*   Let us create below tree
         *              10
         *        /   /    \   \
         *        2  34    56   100
         *       / \         |   /  | \
         *      77  88       1   7  8  9
         */

        Node root = newNode(10);
        (root.childs).add(newNode(2));
        (root.childs).add(newNode(34));
        (root.childs).add(newNode(56));
        (root.childs).add(newNode(100));
        (root.childs.get(0).childs).add(newNode(77));
        (root.childs.get(0).childs).add(newNode(88));
        (root.childs.get(2).childs).add(newNode(1));
        (root.childs.get(3).childs).add(newNode(7));
        (root.childs.get(3).childs).add(newNode(8));
        (root.childs.get(3).childs).add(newNode(9));

        System.out.print(kthSmallestElement(root, 3));
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Structure of a node
class Node:
    def __init__(self, data):
        self.data = data
        self.childs = []

# Global variable set to Maximum
MinimumElement = sys.maxsize

# Function that gives the smallest
# element under the range of key
def smallestEleUnderRange(root, data):
    global MinimumElement
    if root.data > data:
        MinimumElement = min(root.data, MinimumElement)
    for child in range(len(root.childs)):
        smallestEleUnderRange(root.childs[child], data)

# Function to find the Kth smallest element
def kthSmallestElement(root, k):
    global MinimumElement
    ans = -sys.maxsize
    for i in range(k):
        smallestEleUnderRange(root, ans)
        ans = MinimumElement
        MinimumElement = sys.maxsize
    return ans

# Function to create a new node
def newNode(data):
    temp = Node(data)
    return temp

"""   Let us create below tree
 *              10
 *        /   /    \   \
 *        2  34    56   100
 *       / \         |   /  | \
 *      77  88       1   7  8  9
"""

root = newNode(10)
(root.childs).append(newNode(2))
(root.childs).append(newNode(34))
(root.childs).append(newNode(56))
(root.childs).append(newNode(100))
(root.childs[0].childs).append(newNode(77))
(root.childs[0].childs).append(newNode(88))
(root.childs[2].childs).append(newNode(1))
(root.childs[3].childs).append(newNode(7))
(root.childs[3].childs).append(newNode(8))
(root.childs[3].childs).append(newNode(9))

print(kthSmallestElement(root, 3))

# This code is contributed by divyesh072019.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Class containing left and
    // right child of current
    // node and key value
    class Node {

        public int data;
        public List<Node> childs;

        public Node(int data)
        {
            this.data = data;
            childs = new List<Node>();
        }
    }

    // Global variable set to Maximum
    static int MinimumElement = Int32.MaxValue;

    // Function that gives the smallest
    // element under the range of key
    static void smallestEleUnderRange(Node root, int data)
    {
        if (root.data > data) {
            MinimumElement = Math.Min(root.data, MinimumElement);
        }
        foreach(Node child in root.childs) {
            smallestEleUnderRange(child, data);
        }
    }

    // Function to find the Kth smallest element
    static int kthSmallestElement(Node root, int k)
    {
        int ans = Int32.MinValue;
        for (int i = 0; i < k; i++) {
            smallestEleUnderRange(root, ans);
            ans = MinimumElement;
            MinimumElement = Int32.MaxValue;
        }
        return ans;
    }

    // Function to create a new node
    static Node newNode(int data)
    {
        Node temp = new Node(data);
        return temp;
    }

  static void Main() {
    /*   Let us create below tree
     *              10
     *        /   /    \   \
     *        2  34    56   100
     *       / \         |   /  | \
     *      77  88       1   7  8  9
     */

    Node root = newNode(10);
    (root.childs).Add(newNode(2));
    (root.childs).Add(newNode(34));
    (root.childs).Add(newNode(56));
    (root.childs).Add(newNode(100));
    (root.childs[0].childs).Add(newNode(77));
    (root.childs[0].childs).Add(newNode(88));
    (root.childs[2].childs).Add(newNode(1));
    (root.childs[3].childs).Add(newNode(7));
    (root.childs[3].childs).Add(newNode(8));
    (root.childs[3].childs).Add(newNode(9));

    Console.Write(kthSmallestElement(root, 3));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Structure of a node
    class Node
    {
        constructor(data) {
           this.childs = [];
           this.data = data;
        }
    }

    // Global variable set to Maximum
    let MinimumElement = Number.MAX_VALUE;

    // Function that gives the smallest
    // element under the range of key
    function smallestEleUnderRange(root, data)
    {
        if (root.data > data) {
            MinimumElement = Math.min(root.data, MinimumElement);
        }
        for(let child = 0; child < (root.childs).length; child++) {
            smallestEleUnderRange(root.childs[child], data);
        }
    }

    // Function to find the Kth smallest element
    function kthSmallestElement(root, k)
    {
        let ans = Number.MIN_VALUE;
        for (let i = 0; i < k; i++) {
            smallestEleUnderRange(root, ans);
            ans = MinimumElement;
            MinimumElement = Number.MAX_VALUE;
        }
        return ans;
    }

    // Function to create a new node
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    /*   Let us create below tree
     *              10
     *        /   /    \   \
     *        2  34    56   100
     *       / \         |   /  | \
     *      77  88       1   7  8  9
     */

    let root = newNode(10);
    (root.childs).push(newNode(2));
    (root.childs).push(newNode(34));
    (root.childs).push(newNode(56));
    (root.childs).push(newNode(100));
    (root.childs[0].childs).push(newNode(77));
    (root.childs[0].childs).push(newNode(88));
    (root.childs[2].childs).push(newNode(1));
    (root.childs[3].childs).push(newNode(7));
    (root.childs[3].childs).push(newNode(8));
    (root.childs[3].childs).push(newNode(9));

    document.write(kthSmallestElement(root, 3));

    // This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N * K)其中 **N** 是给定树中的节点数。*
***辅助空间:** O(1)，但递归栈最多使用 O(N)个空间。*
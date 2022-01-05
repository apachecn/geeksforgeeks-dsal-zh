# 生成一个数组，表示二叉树的每个垂直层次的节点的 GCD

> 原文:[https://www . geeksforgeeks . org/generate-a-array-representative-gcd-of-of-nodes-of-of-of-foreign-level-of-a-a-二叉树/](https://www.geeksforgeeks.org/generate-an-array-representing-gcd-of-nodes-of-each-vertical-level-of-a-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是构造一个数组，使得数组的第 i <sup>个</sup>索引包含存在于给定二叉树的第 i <sup>个</sup>垂直层次的所有节点的[个](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)个。

**示例:**

> ***输入:**下面是给定的树:*
> ***5*** ***/\*
> *4 7*
> */\ \*
> *8 10 6*
> *\*
> *8***
> 
> *****输出:** {8，4，5，7，6}***
> 
> *****说明:***
> *垂直一级- > GCD(8) = 8。*
> *垂直二级- > GCD(4，8) = 4。*
> *垂直二级- > GCD(5，10) = 5。*
> *垂直四级- > GCD(7) = 7。*
> *垂直水平 V - > GCD(6) = 6***
> 
> *****输入:**下面是给定的树:*
> ***4*** ***/\*
> *2 3*
> */\/\*
> *3 2 4 5*****
> 
> *******输出:** {3，2，2，3，5}*****

******方法:**给定的问题可以通过对给定的树执行[垂直顺序遍历来解决，并存储出现在相同垂直线中的每个节点的值，然后打印为每个级别存储的所有值](https://www.geeksforgeeks.org/print-binary-tree-vertical-order/)的 [GCD。请按照以下步骤解决此问题:](https://www.geeksforgeeks.org/gcd-two-array-numbers/)****

*   ****初始化一个[图](https://www.geeksforgeeks.org/python-map-function/) **M** 来存储执行遍历时每条垂直线的所有节点的 GCD。****
*   ****初始化一个变量，将 **hd** 设为 **0** 来记录水平距离。****
*   ****[递归遍历给定的树](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)并执行以下步骤:

    *   将当前节点的值存储在地图中 **M** 作为**键**作为**HD****值**作为**节点的值**。
    *   将变量 **hd** 递减 **1** ，并递归调用左子树。
    *   将变量 **hd** 增加 **1** ，并递归调用右子树。**** 
*   ****[遍历地图](https://www.geeksforgeeks.org/iterate-over-a-dictionary-in-python/)找到地图中存储的每个水平距离的所有节点的 GCD 作为关键，打印得到的 GCD 值。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Class for node of binary tree
struct TreeNode
{
    int val;
    TreeNode *left, *right;

    TreeNode(int x)
    {
        val = x;
        left = right = NULL;
    }
};

// Function to find GCD of two numbers
int GCD(int a, int b)
{
    if (!b)
        return a;

    // Recursively find the GCD
    return GCD(b, a % b);
}

// Stores the element for each
// vertical distance
unordered_map<int, int> mp;

// Function to traverse the tree
void Trav(TreeNode *root, int hd)
{
    if (!root)
        return;

    // Store the values in the map
    if (mp[hd] == 0)
        mp[hd] = root->val;
    else
        mp[hd] = GCD(mp[hd], root->val);

    // Recursive Calls
    Trav(root->left, hd - 1);
    Trav(root->right, hd + 1);
}

// Function to construct array from
// vertically positioned nodes
void constructArray(TreeNode *root)
{
    Trav(root, 0);

    // Get range of horizontal distances
    int lower = INT_MAX, upper = 0;
    for(auto it:mp)
    {
        lower = min(lower, it.first);
        upper = max(upper, it.first);
    }

    vector<int> ans;

    // Extract the array of values
    for(int i = lower; i < upper + 1; i++)
        ans.push_back(mp[i]);

    // Print the constructed array
    cout << "[";
    for(int i = 0; i < ans.size() - 1; i++)
        cout << ans[i] << ", ";

    cout << ans[ans.size() - 1] << "]";
}

// Driver code
int main()
{
    TreeNode *root = new TreeNode(5);
    root->left = new TreeNode(4);
    root->right = new TreeNode(7);
    root->left->left = new TreeNode(8);
    root->left->left->right = new TreeNode(8);
    root->left->right = new TreeNode(10);
    root->right->right = new TreeNode(6);

    // Function Call
    constructArray(root);

    return 0;
}

// This code is contributed by mohit kumar 29**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.lang.*;
import java.util.*;

// Class containing the left and right
// child of current node and the
// key value
class Node
{
    int val;
    Node left, right;

    // Constructor of the class
    public Node(int item)
    {
        val = item;
        left = right = null;
    }
}

class GFG{

Node root;

// Stores the element for each
// vertical distance
static Map<Integer, Integer> mp = new HashMap<>();

// Function to find GCD of two numbers
static int GCD(int a, int b)
{
    if (b == 0)
        return a;

    // Recursively find the GCD
    return GCD(b, a % b);
}

// Function to traverse the tree
static void Trav(Node root, int hd)
{
    if (root == null)
        return;

    // Store the values in the map
    if (!mp.containsKey(hd))
        mp.put(hd, root.val);
    else
        mp.put(hd, GCD(mp.get(hd), root.val));

    // Recursive Calls
    Trav(root.left, hd - 1);
    Trav(root.right, hd + 1);
}

// Function to construct array from
// vertically positioned nodes
static void constructArray(Node root)
{
    Trav(root, 0);

    // Get range of horizontal distances
    int lower = Integer.MAX_VALUE, upper = 0;
    for(Map.Entry<Integer, Integer> it:mp.entrySet())
    {
        lower = Math.min(lower, it.getKey());
        upper = Math.max(upper, it.getKey());
    }

    ArrayList<Integer> ans = new ArrayList<>();

    // Extract the array of values
    for(int i = lower; i < upper + 1; i++)
        ans.add(mp.getOrDefault(i,0));

    // Print the constructed array
    System.out.print("[");
    for(int i = 0; i < ans.size() - 1; i++)
        System.out.print(ans.get(i) + ", ");

    System.out.print(ans.get(ans.size() - 1) + "]");
}

// Driver code
public static void main(String[] args)
{
    GFG tree = new GFG();

    Node root = new Node(5);
    root.left = new Node(4);
    root.right = new Node(7);
    root.left.left = new Node(8);
    root.left.left.right = new Node(8);
    root.left.right = new Node(10);
    root.right.right = new Node(6);

    // Function Call
    constructArray(root);
}
}

// This code is contributed by offbeat**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Class for node of binary tree
class TreeNode:
    def __init__(self, val ='', left = None, right = None):
        self.val = val
        self.left = left
        self.right = right

# Function to find GCD of two numbers
def GCD(a, b):
    if not b:
        return a

    # Recursively find the GCD
    return GCD(b, a % b)

# Function to construct array from
# vertically positioned nodes
def constructArray(root):

    # Stores the element for each
    # vertical distance
    mp = {}

    # Function to traverse the tree
    def Trav(root, hd):
        if not root:
            return

        # Store the values in the map
        if hd not in mp:
            mp[hd] = root.val
        else:
            mp[hd] = GCD(mp[hd], root.val)

        # Recursive Calls
        Trav(root.left, hd-1)
        Trav(root.right, hd + 1)

    Trav(root, 0)

    # Get range of horizontal distances
    lower = min(mp.keys())
    upper = max(mp.keys())

    ans = []

    # Extract the array of values
    for i in range(lower, upper + 1):
        ans.append(mp[i])

    # Print the constructed array
    print(ans)

# Driver Code

# Given Tree
root = TreeNode(5)
root.left = TreeNode(4)
root.right = TreeNode(7)
root.left.left = TreeNode(8)
root.left.left.right = TreeNode(8)
root.left.right = TreeNode(10)
root.right.right = TreeNode(6)

# Function Call
constructArray(root)**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;

// Class containing the left and right
// child of current node and the
// key value
public class Node
{
    public int val;
    public Node left, right;

    // Constructor of the class
    public Node(int item)
    {
        val = item;
        left = right = null;
    }
}

class GFG{

// Stores the element for each
// vertical distance
static Dictionary<int,
                  int> mp = new Dictionary<int,
                                           int>();

// Function to find GCD of two numbers
static int GCD(int a, int b)
{
    if (b == 0)
        return a;

    // Recursively find the GCD
    return GCD(b, a % b);
}

// Function to traverse the tree
static void Trav(Node root, int hd)
{
    if (root == null)
        return;

    // Store the values in the map
    if (!mp.ContainsKey(hd))
        mp.Add(hd, root.val);
    else
        mp[hd] = GCD(mp[hd], root.val);

    // Recursive Calls
    Trav(root.left, hd - 1);
    Trav(root.right, hd + 1);
}

// Function to construct array from
// vertically positioned nodes
static void constructArray(Node root)
{
    Trav(root, 0);

    // Get range of horizontal distances
    int lower = Int32.MaxValue, upper = 0;
    foreach(KeyValuePair<int, int> it in mp)
    {
        lower = Math.Min(lower, it.Key);
        upper = Math.Max(upper, it.Key);
    }

    List<int> ans = new List<int>();

    // Extract the array of values
    for(int i = lower; i < upper + 1; i++)
        if(mp.ContainsKey(i))
            ans.Add(mp[i]);
        else
            ans.Add(0);

    // Print the constructed array
    Console.Write("[");
    for(int i = 0; i < ans.Count - 1; i++)
        Console.Write(ans[i] + ", ");

    Console.Write(ans[ans.Count - 1] + "]");
}

// Driver code
static public void Main()
{

    Node root = new Node(5);
    root.left = new Node(4);
    root.right = new Node(7);
    root.left.left = new Node(8);
    root.left.left.right = new Node(8);
    root.left.right = new Node(10);
    root.right.right = new Node(6);

    // Function Call
    constructArray(root);
}
}

// This code is contributed by rishavmahato348**
```

## ****java 描述语言****

```
**<script>
    // Javascript program for the above approach

    // Class containing the left and right
    // child of current node and the
    // key value
    class Node
    {
        constructor(item) {
           this.left = null;
           this.right = null;
           this.val = item;
        }
    }

    // Stores the element for each
    // vertical distance
    let mp = new Map();

    // Function to find GCD of two numbers
    function GCD(a, b)
    {
        if (b == 0)
            return a;

        // Recursively find the GCD
        return GCD(b, a % b);
    }

    // Function to traverse the tree
    function Trav(root, hd)
    {
        if (root == null)
            return;

        // Store the values in the map
        if (!mp.has(hd))
            mp.set(hd, root.val);
        else
            mp.set(hd, GCD(mp.get(hd), root.val));

        // Recursive Calls
        Trav(root.left, hd - 1);
        Trav(root.right, hd + 1);
    }

    // Function to construct array from
    // vertically positioned nodes
    function constructArray(root)
    {
        Trav(root, 0);

        // Get range of horizontal distances
        let lower = Number.MAX_VALUE, upper = 0;
        mp.forEach((values,keys)=>{
            lower = Math.min(lower, keys);
            upper = Math.max(upper, keys);
        })

        let ans = [];

        // Extract the array of values
        for(let i = lower; i < upper + 1; i++)
        {
            if(mp.has(i))
            {
                ans.push(mp.get(i));
            }
            else{
                ans.push(0);
            }
        }

        // Print the constructed array
        document.write("[");
        for(let i = 0; i < ans.length - 1; i++)
            document.write(ans[i] + ", ");

        document.write(ans[ans.length - 1] + "]");
    }

    let root = new Node(5);
    root.left = new Node(4);
    root.right = new Node(7);
    root.left.left = new Node(8);
    root.left.left.right = new Node(8);
    root.left.right = new Node(10);
    root.right.right = new Node(6);

    // Function Call
    constructArray(root);

// This code is contributed by suresh07.
</script>**
```

******Output:** 

```
[8, 4, 5, 7, 6]
```**** 

*******时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*****
# 二叉树所有垂直层次的和

> 原文:[https://www . geeksforgeeks . org/二叉树所有垂直层次之和/](https://www.geeksforgeeks.org/sum-of-all-vertical-levels-of-a-binary-tree/)

给定一个由 **1** 或 **0** 组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)作为其节点值，任务是找到二叉树的所有[垂直层级的总和，将每个值视为二进制表示。](https://www.geeksforgeeks.org/print-binary-tree-vertical-order-set-2/)

**示例:**

> **输入:**1
> /\
> 1 0
> /\/\
> 1 0 1 0
> **输出:** 7
> **解释:**/T12】从左到右取垂直级别:
> 为垂直级别 1: (1) <sub>2</sub> = 1
> 为垂直级别 2: (1) <sub>2</sub> = 1
> 为垂直级别 3: (101)
> 
> **输入:**0
> /\
> 1 0
> /\ \
> 1 1 0
> /\ \/\
> 1 1 1 0 0
> **输出:** 8
> **解释:**
> 从左到右取垂直标高:
> 对于垂直标高 1: (1) <sub>2</sub> = 1
> 对于垂直标高 2: (1) <sub>2</sub> = 1
> 对于垂直标高 3: (11) <sub>2</sub> = 3
> 对于垂直标高 4 <sub>2</sub> = 2
> 对于垂直标高 6: (0) <sub>2</sub> = 0
> 对于垂直标高 7: (0) <sub>2</sub> = 0
> 总和= 1+1+3+1+2+0+0 = 8

**方法:**按照以下步骤解决问题:

1.  执行[树遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，同时跟踪与根节点的水平和垂直距离
2.  将与其水平距离对应的节点值存储在 [Hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中。
3.  初始化一个变量，比如**和**，来存储需要的结果。
4.  创建一个 [Hashmap](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) ，比如说 **M** ，来存储水平距离作为关键字和一个对数组**{节点值，节点到根的距离}** 。
5.  每个节点的高度也被存储，因为垂直级别需要按排序顺序(从上到下)排列，以获得其二进制表示的正确十进制值。
6.  执行[前序树遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，并传递垂直高度和水平距离作为参数。
    *   如果根不是[空](https://www.geeksforgeeks.org/few-bytes-on-null-pointer-in-c/)，执行以下操作:
        *   在 **M** 中追加[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)**{节点值，水平距离中的垂直高度}** 。
        *   遍历**左子树**，将**水平距离**递减 **1** 。
        *   遍历**右子树**，将**水平距离**增加 **1** 。
        *   对于两个递归调用，将**垂直高度**增加 **1** 。
7.  现在，[遍历 Hashmap](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) ，说出 **M** ，对于每个键，执行以下步骤:
    *   [根据从根节点开始的高度](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)对值进行排序，然后[将获得的二进制数转换为其十进制等价物](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)并将其存储在一个变量中，比如 **B** 。
    *   将 **B** 的值加到 **ans** 上。
8.  打印**和**的值

下面是上述方法的实现:

## C++

```
// C++ program for super ugly number
#include<bits/stdc++.h>
using namespace std;

// Structure of a Tree node
struct TreeNode
{
  int val = 0;
  TreeNode *left;
  TreeNode *right;
  TreeNode(int x)
  {
    val = x;
    left = right = NULL;
  }
};

// Function to convert
// binary number to decimal
int getDecimal(vector<pair<int, int> > arr)
{

  // Sort the array on
  // the basis of the
  // first index i.e, height
  sort(arr.begin(), arr.end());

  // Store the required
  // decimal equivalent
  // of the number
  int ans = 0;

  // Traverse the array
  for (int i = 0; i < arr.size(); i++)
  {
    ans <<= 1;
    ans |= arr[i].second;
  }

  // Return the answer
  return ans;
}

// Function to traverse the tree
void Traverse(TreeNode *root, int hd, int ht,
              map<int, vector<pair<int, int> > > &mp)
{

  // If root is NULL, return
  if (!root)
    return;
  mp[hd].push_back({ht, root->val});

  // Make recursive calls to the left and
  // right subtree
  Traverse(root->left, hd - 1, ht + 1, mp);
  Traverse(root->right, hd + 1, ht + 1, mp);
}

// Function to calculate
// sum of vertical levels
// of a Binary Tree
void getSum(TreeNode *root)
{

  // Dictionary to store the
  // vertical level as key and
  // its corresponding
  // binary number as value
  map<int,vector<pair<int,int> > > mp;

  // Function Call to perform traverse the tree
  Traverse(root, 0, 0, mp);

  // Store the required answer
  int ans = 0;

  // Get decimal values for each vertical level
  // and add it to ans
  for (auto i:mp)
    ans += getDecimal(i.second);

  // Print the answer
  cout<<(ans);
}

/* Driver program to test above functions */
int main()
{

  TreeNode *root = new TreeNode(1);
  root->left = new TreeNode(1);
  root->right = new TreeNode(0);
  root->left->left = new TreeNode(1);
  root->left->right = new TreeNode(0);
  root->right->left = new TreeNode(1);
  root->right->right = new TreeNode(0);

  // Function call to get the
  // sum of vertical level
  // of the tree
  getSum(root);

  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for super ugly number
import java.io.*;
import java.util.*;

// Structure of a Tree node
class TreeNode
{
  int val = 0;
  TreeNode left;
  TreeNode right;

  TreeNode(int x)
  {
    val = x;
    left = right = null;
  }
}

class GFG {

  static Map<Integer, ArrayList<ArrayList<Integer>>> mp = new HashMap<Integer, ArrayList<ArrayList<Integer>>>();

  // Function to convert
  // binary number to decimal
  static int getDecimal(ArrayList<ArrayList<Integer> > arr)
  {

    // Sort the array on
    // the basis of the
    // first index i.e, height
    Collections.sort(arr, new Comparator<ArrayList<Integer>>() {   
      @Override
      public int compare(ArrayList<Integer> o1, ArrayList<Integer> o2) {
        return o1.get(0).compareTo(o2.get(0));
      }              
    });

    // Store the required
    // decimal equivalent
    // of the number
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < arr.size(); i++)
    {
      ans <<= 1;
      ans |= arr.get(i).get(1);
    }

    // Return the answer
    return ans;
  }

  // Function to traverse the tree
  static void Traverse(TreeNode root, int hd, int ht)
  {

    // If root is NULL, return
    if (root == null)
      return;

    if(mp.containsKey(hd))
    {
      mp.get(hd).add(new ArrayList<Integer>(Arrays.asList(ht, root.val)));
    }
    else
    {
      mp.put(hd,new ArrayList<ArrayList<Integer>>());
      mp.get(hd).add(new ArrayList<Integer>(Arrays.asList(ht, root.val)));
    }

    // Make recursive calls to the left and
    // right subtree
    Traverse(root.left, hd - 1, ht + 1);
    Traverse(root.right, hd + 1, ht + 1);
  }

  // Function to calculate
  // sum of vertical levels
  // of a Binary Tree
  static void getSum(TreeNode root)
  {

    // Function Call to perform traverse the tree
    Traverse(root, 0, 0);

    // Store the required answer
    int ans = 0;

    // Get decimal values for each vertical level
    // and add it to ans
    for(Integer key : mp.keySet())
    {
      ans += getDecimal(mp.get(key));
    }

    // Print the answer
    System.out.print(ans);
  }

  // Driver code
  public static void main (String[] args)
  {
    TreeNode root = new TreeNode(1);
    root.left = new TreeNode(1);
    root.right = new TreeNode(0);
    root.left.left = new TreeNode(1);
    root.left.right = new TreeNode(0);
    root.right.left = new TreeNode(1);
    root.right.right = new TreeNode(0);

    // Function call to get the
    // sum of vertical level
    // of the tree
    getSum(root);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python program
# for the above approach

# Structure of a Tree node
class TreeNode:
    def __init__(self, val ='',
                 left = None, right = None):
        self.val = val
        self.left = left
        self.right = right

# Function to convert
# binary number to decimal
def getDecimal(arr):

    # Sort the array on
    # the basis of the
    # first index i.e, height
    arr.sort()

    # Store the required
    # decimal equivalent
    # of the number
    ans = 0

    # Traverse the array
    for i in range(len(arr)):
        ans <<= 1
        ans |= arr[i][1]

    # Return the answer
    return ans

# Function to calculate
# sum of vertical levels
# of a Binary Tree
def getSum(root):

    # Dictionary to store the
    # vertical level as key and
    # its corresponding
    # binary number as value
    mp = {}

    # Function to traverse the tree
    def Traverse(root, hd, ht):

        # If root is NULL, return
        if not root:
            return

        # Store the value in the map
        if hd not in mp:
            mp[hd] = [[ht, root.val]]
        else:
            mp[hd].append([ht, root.val])

        # Make recursive calls to the left and
        # right subtree
        Traverse(root.left, hd - 1, ht + 1)
        Traverse(root.right, hd + 1, ht + 1)

    # Function Call to perform traverse the tree
    Traverse(root, 0, 0)

    # Store the required answer
    ans = 0

    # Get decimal values for each vertical level
    # and add it to ans
    for i in mp:
        ans += getDecimal(mp[i])

    # Print the answer
    print(ans)

# Driver Code

# Given Tree
root = TreeNode(1)
root.left = TreeNode(1)
root.right = TreeNode(0)
root.left.left = TreeNode(1)
root.left.right = TreeNode(0)
root.right.left = TreeNode(1)
root.right.right = TreeNode(0)

# Function call to get the
# sum of vertical level
# of the tree
getSum(root)
```

## C#

```
// C# program for super ugly number
using System;
using System.Linq;
using System.Collections.Generic;

// Structure of a Tree node
public class TreeNode
{
  public int val = 0;
  public TreeNode left, right;

  public TreeNode(int x)
  {
    val = x;
    left = right = null;
  }
}

public class GFG
{

  static Dictionary<int,List<List<int>>> mp =
    new Dictionary<int,List<List<int>>>();

  // Function to convert
  // binary number to decimal
  static int getDecimal(List<List<int> > arr)
  {

    // Sort the array on
    // the basis of the
    // first index i.e, height
    arr.OrderBy( l => l[0]);

    // Store the required
    // decimal equivalent
    // of the number
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < arr.Count; i++)
    {
      ans <<= 1;
      ans |= arr[i][1];
    }

    // Return the answer
    return ans;
  }

  // Function to traverse the tree
  static void Traverse(TreeNode root, int hd, int ht)
  {

    // If root is NULL, return
    if (root == null)
      return;

    if(mp.ContainsKey(hd))
    {
      mp[hd].Add(new List<int>(){ht, root.val});
    }
    else
    {
      mp.Add(hd,new List<List<int>>());
      mp[hd].Add(new List<int>(){ht, root.val});
    }

    // Make recursive calls to the left and
    // right subtree
    Traverse(root.left, hd - 1, ht + 1);
    Traverse(root.right, hd + 1, ht + 1);
  }

  // Function to calculate
  // sum of vertical levels
  // of a Binary Tree
  static void getSum(TreeNode root)
  {

    // Function Call to perform traverse the tree
    Traverse(root, 0, 0);

    // Store the required answer
    int ans = 0;

    // Get decimal values for each vertical level
    // and add it to ans
    foreach(int key in mp.Keys)
    {
      ans += getDecimal(mp[key]);
    }

    // Print the answer
    Console.Write(ans);
  }

  // Driver code
  static public void Main ()
  {
    TreeNode root = new TreeNode(1);
    root.left = new TreeNode(1);
    root.right = new TreeNode(0);
    root.left.left = new TreeNode(1);
    root.left.right = new TreeNode(0);
    root.right.left = new TreeNode(1);
    root.right.right = new TreeNode(0);

    // Function call to get the
    // sum of vertical level
    // of the tree
    getSum(root);
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program for super ugly number

// Structure of a Tree node
class TreeNode
{
    constructor(x)
    {
        this.val = x;
        this.left = this.right = null;
    }
}

let mp = new Map();

// Function to convert
  // binary number to decimal
function getDecimal(arr)
{
    arr.sort(function(a,b){return a[0]-b[0]});

    // Store the required
    // decimal equivalent
    // of the number
    let ans = 0;

    // Traverse the array
    for (let i = 0; i < arr.length; i++)
    {
      ans <<= 1;
      ans |= arr[i][1];
    }

    // Return the answer
    return ans;
}

// Function to traverse the tree
function Traverse(root, hd, ht)
{

    // If root is NULL, return
    if (root == null)
      return;

    if(mp.has(hd))
    {
      mp.get(hd).push([ht, root.val]);
    }
    else
    {
      mp.set(hd,[]);
      mp.get(hd).push([ht, root.val]);
    }

    // Make recursive calls to the left and
    // right subtree
    Traverse(root.left, hd - 1, ht + 1);
    Traverse(root.right, hd + 1, ht + 1);
}

// Function to calculate
  // sum of vertical levels
  // of a Binary Tree
function getSum(root)
{

    // Function Call to perform traverse the tree
    Traverse(root, 0, 0);

    // Store the required answer
    let ans = 0;

    // Get decimal values for each vertical level
    // and add it to ans
    for(let [key, value] of mp.entries())
    {
      ans += getDecimal(value);
    }

    // Print the answer
    document.write(ans);
}

// Driver code
let root = new TreeNode(1);
root.left = new TreeNode(1);
root.right = new TreeNode(0);
root.left.left = new TreeNode(1);
root.left.right = new TreeNode(0);
root.right.left = new TreeNode(1);
root.right.right = new TreeNode(0);

// Function call to get the
// sum of vertical level
// of the tree
getSum(root);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*
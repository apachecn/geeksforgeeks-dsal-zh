# 用重叠条件从上到下压缩二叉树

> 原文:[https://www . geeksforgeeks . org/compress-a-二叉树-从上到下-带重叠条件/](https://www.geeksforgeeks.org/compress-a-binary-tree-from-top-to-bottom-with-overlapping-condition/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是将同一条垂直线上的所有节点压缩成一个节点，这样，如果在任何位置的垂直线上所有节点的设置位的计数大于该位置的清除位的计数，则该位置的单个节点的位被设置。

**示例:**

> **输入:**
> 
> ```
>      1
>       \
>        2
>       /
>      1
>       \
>        3
> ```
> 
> **输出:** 1 2
> **说明:**
> 1 和 1 处于相同的垂直距离，第 0 <sup>个</sup>位置的设置位计数= 2，清零位计数= 0。因此，结果节点的第 0<sup>位被置位。
> 2 和 3 处于相同的垂直距离，设置位的计数为 0 <sup>第</sup>个位置= 1，清零位的计数为 1。因此，结果节点的 0 位被设置，而不是被设置。
> 2 和 3 处于相同的垂直距离，第一个位置的设置位计数= 2，清除位计数= 0。因此，结果节点的第 1 位被置位。</sup> 
> 
> **输入:**
> 
> ```
>        1
>      /   \
>     3     2
>    / \   /  \
>   1   4 1    2
> ```
> 
> **输出:** 1 3 5 2 2

**方法:**想法是[遍历树](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)并为每个访问节点保持**到根节点的水平距离**的轨迹。以下是步骤:

*   一张[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 可以用来存储根节点的水平距离作为**键**，节点的值作为**值**。
*   将值存储在地图中后，检查每个位置的设置位和非设置位的**数量，并相应地计算值。**

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program for the above approach

# Structure of a node
# of th tree
class TreeNode:
    def __init__(self, val ='', left = None, right = None):
        self.val = val
        self.left = left
        self.right = right

# Function to compress all the nodes
# on the same vertical line
def evalComp(arr):

    # Stores node by compressing all
    # nodes on the current vertical line
    ans = 0

    # Check if i-th bit of current bit
    # set or not
    getBit = 1

    # Iterate over the range [0, 31]
    for i in range(32):

        # Stores count of set bits
        # at i-th positions
        S = 0

        # Stores count of clear bits
        # at i-th positions
        NS = 0

        # Traverse the array
        for j in arr:

            # If i-th bit of current element
            # is set
            if getBit & j:

                # Update S
                S += 1
            else:

                # Update NS
                NS += 1

        # If count of set bits at i-th position
        # is greater than count of clear bits
        if S > NS:

            # Update ans
            ans += 2**i

        # Update getBit   
        getBit <<= 1

    print(ans, end = " ")

# Function to compress all the nodes on
# the same vertical line with a single node
# that satisfies the condition
def compressTree(root):

    # Map all the nodes on the same vertical line
    mp = {}

    # Function to traverse the tree and map
    # all the nodes of same vertical line
    # to vertical distance
    def Trav(root, hd):
        if not root:
            return

        # Storing the values in the map
        if hd not in mp:
            mp[hd] = [root.val]
        else:
            mp[hd].append(root.val)

        # Recursive calls on left and right subtree
        Trav(root.left, hd-1)
        Trav(root.right, hd + 1)

    Trav(root, 0)

    # Getting the range of
    # horizontal distances
    lower = min(mp.keys())
    upper = max(mp.keys())

    for i in range(lower, upper + 1):
        evalComp(mp[i])

# Driver Code
if __name__ == '__main__':

    root = TreeNode(5)
    root.left = TreeNode(3)
    root.right = TreeNode(2)
    root.left.left = TreeNode(1)
    root.left.right = TreeNode(4)
    root.right.left = TreeNode(1)
    root.right.right = TreeNode(2)

    # Function Call
    compressTree(root)
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Structure of a node
// of th tree
class TreeNode {
  constructor(val = "", left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

// Function to compress all the nodes
// on the same vertical line
function evalComp(arr) {
  // Stores node by compressing all
  // nodes on the current vertical line
  let ans = 0;

  // Check if i-th bit of current bit
  // set or not
  let getBit = 1;

  // Iterate over the range [0, 31]
  for (let i = 0; i < 32; i++) {
    // Stores count of set bits
    // at i-th positions
    let S = 0;

    // Stores count of clear bits
    // at i-th positions
    let NS = 0;

    // Traverse the array
    for (j of arr) {
      // If i-th bit of current element
      // is set
      if (getBit & j)
        // Update S
        S += 1;
      // Update NS
      else NS += 1;
    }

    // If count of set bits at i-th position
    // is greater than count of clear bits
    if (S > NS)
      // Update ans
      ans += 2 ** i;

    // Update getBit
    getBit <<= 1;
  }

  document.write(ans + " ");
}

// Function to compress all the nodes on
// the same vertical line with a single node
// that satisfies the condition
function compressTree(root) {
  // Map all the nodes on the same vertical line
  let mp = new Map();

  // Function to traverse the tree and map
  // all the nodes of same vertical line
  // to vertical distance
  function Trav(root, hd) {
    if (!root) return;

    // Storing the values in the map
    if (!mp.has(hd)) mp.set(hd, [root.val]);
    else {
      let temp = mp.get(hd);
      temp.push(root.val);
      mp.set(hd, temp);
    }

    // Recursive calls on left and right subtree
    Trav(root.left, hd - 1);
    Trav(root.right, hd + 1);
  }

  Trav(root, 0);

  // Getting the range of
  // horizontal distances
  let lower = [...mp.keys()].sort((a, b) => a - b)[0];
  let upper = [...mp.keys()].sort((a, b) => b - a)[0];

  for (let i = lower; i <= upper; i++) evalComp(mp.get(i));
}

// Driver Code

let root = new TreeNode(5);
root.left = new TreeNode(3);
root.right = new TreeNode(2);
root.left.left = new TreeNode(1);
root.left.right = new TreeNode(4);
root.right.left = new TreeNode(1);
root.right.right = new TreeNode(2);

// Function Call
compressTree(root);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
1 3 5 2 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
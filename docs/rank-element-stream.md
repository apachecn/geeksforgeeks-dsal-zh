# 流中元素的等级

> 原文:[https://www.geeksforgeeks.org/rank-element-stream/](https://www.geeksforgeeks.org/rank-element-stream/)

给定一个整数流，查找给定整数 x 的秩。流中整数的秩是“小于或等于 x(不包括 x)的元素总数”。
如果在流中找不到元素或者元素在流中最小，返回-1。
**例:**

```
Input :  arr[] = {10, 20, 15, 3, 4, 4, 1}
              x = 4;
Output : Rank of 4 in stream is: 3
There are total three elements less than
or equal to x (and not including x)

Input : arr[] = {5, 1, 14, 4, 15, 9, 7, 20, 11}, 
           x = 20;
Output : Rank of 20 in stream is: 8
```

实现这一点的一个相对简单的方法是使用一个按排序顺序保存所有元素的数组。当插入新元素时，我们会移动元素。然后我们对数组执行二分搜索法运算，得到 x 的最右边的索引，并返回该索引。getRank(x)可以在 O(log n)中工作，但是插入会很昂贵。
一个**高效的方式**就是使用一个[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)。每个节点将保存其左子树的数据值和大小。
我们从根开始遍历树，并将根值与 x 进行比较。

1.  如果根->数据== x，返回根的左子树的大小。
2.  如果 x < root->数据，返回 getRank(根->左)
3.  如果 x >根->数据，返回 getRank(根->右)leftSubtree 的大小+ 1。

以下是解决方案。

## C++

```
// CPP program to find rank of an
// element in a stream.
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node *left, *right;
    int leftSize;
};

Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    temp->leftSize = 0;
    return temp;
}

// Inserting a new Node.
Node* insert(Node*& root, int data)
{
    if (!root)
        return newNode(data);

    // Updating size of left subtree.
    if (data <= root->data) {
        root->left = insert(root->left, data);
        root->leftSize++;
    }
    else
        root->right = insert(root->right, data);

    return root;
}

// Function to get Rank of a Node x.
int getRank(Node* root, int x)
{
    // Step 1.
    if (root->data == x)
        return root->leftSize;

    // Step 2.
    if (x < root->data) {
        if (!root->left)
            return -1;
        else
            return getRank(root->left, x);
    }

    // Step 3.
    else {
        if (!root->right)
            return -1;
        else {
            int rightSize = getRank(root->right, x);
              if(rightSize == -1 ) return -1;
            return root->leftSize + 1 + rightSize;
        }
    }
}

// Driver code
int main()
{
    int arr[] = { 5, 1, 4, 4, 5, 9, 7, 13, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 4;

    Node* root = NULL;
    for (int i = 0; i < n; i++)
        root = insert(root, arr[i]);

    cout << "Rank of " << x << " in stream is: "
         << getRank(root, x) << endl;

    x = 13;
    cout << "Rank of " << x << " in stream is: "
         << getRank(root, x) << endl;

    x = 8;
    cout << "Rank of " << x << " in stream is: "
         << getRank(root, x) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find rank of an
// element in a stream.
class GfG {

static class Node {
    int data;
    Node left, right;
    int leftSize;
}

static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    temp.leftSize = 0;
    return temp;
}

// Inserting a new Node.
static Node insert(Node root, int data)
{
    if (root == null)
        return newNode(data);

    // Updating size of left subtree.
    if (data <= root.data) {
        root.left = insert(root.left, data);
        root.leftSize++;
    }
    else
        root.right = insert(root.right, data);

    return root;
}

// Function to get Rank of a Node x.
static int getRank(Node root, int x)
{
    // Step 1.
    if (root.data == x)
        return root.leftSize;

    // Step 2.
    if (x < root.data) {
        if (root.left == null)
            return -1;
        else
            return getRank(root.left, x);
    }

    // Step 3.
    else {
        if (root.right == null)
            return -1;
        else {
            int rightSize = getRank(root.right, x);
          if(rightSize == -1) return -1;
            return root.leftSize + 1 + rightSize;
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 1, 4, 4, 5, 9, 7, 13, 3 };
    int n = arr.length;
    int x = 4;

    Node root = null;
    for (int i = 0; i < n; i++)
        root = insert(root, arr[i]);

    System.out.println("Rank of " + x + " in stream is : "+getRank(root, x));

    x = 13;
    System.out.println("Rank of " + x + " in stream is : "+getRank(root, x));

}
}
```

## 蟒蛇 3

```
# Python3 program to find rank of an
# element in a stream.

class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None
        self.leftSize = 0

# Inserting a new Node.
def insert(root, data):
    if root is None:
        return newNode(data)

    # Updating size of left subtree.
    if data <= root.data:
        root.left = insert(root.left, data)
        root.leftSize += 1
    else:
        root.right = insert(root.right, data)
    return root

# Function to get Rank of a Node x.
def getRank(root, x):

    # Step 1.
    if root.data == x:
        return root.leftSize

    # Step 2.
    if x < root.data:
        if root.left is None:
            return -1
        else:
            return getRank(root.left, x)

    # Step 3.
    else:
        if root.right is None:
            return -1
        else:
            rightSize = getRank(root.right, x)
            if rightSize == -1:
                # x not found in right sub tree, i.e. not found in stream
                return -1
            else:
                return root.leftSize + 1 + rightSize

# Driver code
if __name__ == '__main__':
    arr = [5, 1, 4, 4, 5, 9, 7, 13, 3]
    n = len(arr)
    x = 4

    root = None
    for i in range(n):
        root = insert(root, arr[i])

    print("Rank of", x, "in stream is:",
                       getRank(root, x))
    x = 13
    print("Rank of", x, "in stream is:",
                       getRank(root, x))
    x = 8
    print("Rank of", x, "in stream is:",
                       getRank(root, x))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find rank of an
// element in a stream.
using System;

class GFG
{
public class Node
{
    public int data;
    public Node left, right;
    public int leftSize;
}

static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    temp.leftSize = 0;
    return temp;
}

// Inserting a new Node.
static Node insert(Node root, int data)
{
    if (root == null)
        return newNode(data);

    // Updating size of left subtree.
    if (data <= root.data)
    {
        root.left = insert(root.left, data);
        root.leftSize++;
    }
    else
        root.right = insert(root.right, data);

    return root;
}

// Function to get Rank of a Node x.
static int getRank(Node root, int x)
{
    // Step 1.
    if (root.data == x)
        return root.leftSize;

    // Step 2.
    if (x < root.data)
    {
        if (root.left == null)
            return -1;
        else
            return getRank(root.left, x);
    }

    // Step 3.
    else
    {
        if (root.right == null)
            return -1;
        else
        {
            int rightSize = getRank(root.right, x);
              if(rightSize == -1) return -1;
            return root.leftSize + 1 + rightSize;
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 5, 1, 4, 4, 5, 9, 7, 13, 3 };
    int n = arr.Length;
    int x = 4;

    Node root = null;
    for (int i = 0; i < n; i++)
        root = insert(root, arr[i]);

    Console.WriteLine("Rank of " + x +
                      " in stream is : " +
                      getRank(root, x));

    x = 13;
    Console.WriteLine("Rank of " + x +
                      " in stream is : " +
                      getRank(root, x));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find rank of an
// element in a stream.

class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
        this.leftSize = 0;
    }
}

function newNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    temp.leftSize = 0;
    return temp;
}

// Inserting a new Node.
function insert(root, data)
{
    if (root == null)
        return newNode(data);

    // Updating size of left subtree.
    if (data <= root.data)
    {
        root.left = insert(root.left, data);
        root.leftSize++;
    }
    else
        root.right = insert(root.right, data);

    return root;
}

// Function to get Rank of a Node x.
function getRank(root, x)
{
    // Step 1.
    if (root.data == x)
        return root.leftSize;

    // Step 2.
    if (x < root.data)
    {
        if (root.left == null)
            return -1;
        else
            return getRank(root.left, x);
    }

    // Step 3.
    else
    {
        if (root.right == null)
            return -1;
        else
        {
            var rightSize = getRank(root.right, x);
              if(rightSize == -1) return -1;
            return root.leftSize + 1 + rightSize;
        }
    }
}

// Driver code
var arr = [5, 1, 4, 4, 5, 9, 7, 13, 3];
var n = arr.length;
var x = 4;
var root = null;
for (var i = 0; i < n; i++)
    root = insert(root, arr[i]);
document.write("Rank of " + x +
                  " in stream is : " +
                  getRank(root, x) + "<br>");
x = 13;
document.write("Rank of " + x +
                  " in stream is : " +
                  getRank(root, x)+"<br>");
x = 8;
document.write("Rank of " + x +
                  " in stream is : " +
                  getRank(root, x));

</script>
```

**Output**

```
Rank of 4 in stream is: 3
Rank of 13 in stream is: 8
Rank of 8 in stream is: -1
```

**另一种方法:**
从头遍历数组。遍历时，计算等于或小于给定键的节点数。打印计数(等级)。

## C++

```
// C++ program to find rank of an
// element in a stream.
#include <bits/stdc++.h>
using namespace std;

// Driver code
int main()
{
    int a[] = {5, 1, 14, 4, 15, 9, 7, 20, 11};
    int key = 20;
    int arraySize = sizeof(a)/sizeof(a[0]);
    int count = 0;
    for(int i = 0; i < arraySize; i++)
    {
        if(a[i] <= key)
        {
            count += 1;
        }
    }
    cout << "Rank of " << key << " in stream is: "
            << count-1 << endl;
    return 0;
}

// This code is contributed by
// Ashwin Loganathan.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find rank of an
// element in a stream.
class GFG
{

// Driver code
public static void main(String[] args)
{
    int a[] = {5, 1, 14, 4, 15, 9, 7, 20, 11};
    int key = 20;
    int arraySize = a.length;
    int count = 0;
    for(int i = 0; i < arraySize; i++)
    {
        if(a[i] <= key)
        {
            count += 1;
        }
    }
    System.out.println("Rank of " + key +
                    " in stream is: " + (count - 1));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find rank of an
# element in a stream.

# Driver code
if __name__ == '__main__':
    a = [5, 1, 14, 4, 15,
            9, 7, 20, 11]
    key = 20
    arraySize = len(a)
    count = 0
    for i in range(arraySize):
        if a[i] <= key:
            count += 1

    print("Rank of", key,
          "in stream is:", count - 1)

# This code is contributed by PranchalK
```

## C#

```
// C# program to find rank of an
// element in a stream.
using System;

class GFG
{
// Driver code
public static void Main()
{
    int []a = {5, 1, 14, 4, 15, 9, 7, 20, 11};
    int key = 20;
    int arraySize = a.Length;
    int count = 0;
    for(int i = 0; i < arraySize; i++)
    {
        if(a[i] <= key)
        {
            count += 1;
        }
    }
    Console.WriteLine("Rank of " + key +
                      " in stream is: " +
                            (count - 1));
}
}

// This code is contributed by
// Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find rank of an
// element in a stream.

// Driver code
$a = array(5, 1, 14, 4, 15, 9, 7, 20, 11);
$key = 20;
$arraySize = sizeof($a);
$count = 0;
for($i = 0; $i < $arraySize; $i++)
{
    if($a[$i] <= $key)
    {
        $count += 1;
    }
}
echo "Rank of " . $key . " in stream is: " .
      ($count - 1) . "\n";

// This code is contributed by
// Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript program to find rank of an
// element in a stream.    // Driver code

        var a = [ 5, 1, 14, 4, 15, 9, 7, 20, 11 ];
        var key = 20;
        var arraySize = a.length;
        var count = 0;
        for (i = 0; i < arraySize; i++) {
            if (a[i] <= key) {
                count += 1;
            }
        }
        document.write("Rank of " + key + " in stream is: " + (count - 1));

// This code contributed by umadevi9616
</script>
```

**输出:**

```
Rank of 20 in stream is: 8
```
# 从给定的顺序遍历和顺序遍历中打印顺序遍历

> 原文:[https://www . geesforgeks . org/print-post-order-from-given-in order-preorder-traversals/](https://www.geeksforgeeks.org/print-postorder-from-given-inorder-and-preorder-traversals/)

给定二叉树的有序遍历和前序遍历，打印后序遍历。

**示例:**

```
Input:
Inorder traversal in[] = {4, 2, 5, 1, 3, 6}
Preorder traversal pre[] = {1, 2, 4, 5, 3, 6}

Output:
Postorder traversal is {4, 5, 2, 6, 3, 1}
```

上例中的 travelsals 代表以下树

```
         1
      /    \    
     2       3
   /   \      \
  4     5      6
```

一个**天真的方法**是先构造树，然后用简单的递归方法打印构造树的后序遍历。

**我们不需要构造树**就可以打印后序遍历。其思想是，根总是前序遍历中的第一项，它必须是后序遍历中的最后一项。我们先递归打印左子树，然后递归打印右子树。最后，打印根。为了找到 pre[]和 in[]中左右子树的边界，我们在[]中搜索 root in，在[]中 root in 之前的所有元素都是左子树的元素，root 之后的所有元素都是右子树的元素。在 pre[]中，[]中根的索引之后的所有元素都是右子树的元素。索引之前的元素(包括索引处的元素，不包括第一个元素)是左子树的元素。

## C++

```
// C++ program to print postorder traversal from preorder and inorder traversals
#include <iostream>
using namespace std;

// A utility function to search x in arr[] of size n
int search(int arr[], int x, int n)
{
    for (int i = 0; i < n; i++)
        if (arr[i] == x)
            return i;
    return -1;
}

// Prints postorder traversal from given inorder and preorder traversals
void printPostOrder(int in[], int pre[], int n)
{
    // The first element in pre[] is always root, search it
    // in in[] to find left and right subtrees
    int root = search(in, pre[0], n);

    // If left subtree is not empty, print left subtree
    if (root != 0)
        printPostOrder(in, pre + 1, root);

    // If right subtree is not empty, print right subtree
    if (root != n - 1)
        printPostOrder(in + root + 1, pre + root + 1, n - root - 1);

    // Print root
    cout << pre[0] << " ";
}

// Driver program to test above functions
int main()
{
    int in[] = { 4, 2, 5, 1, 3, 6 };
    int pre[] = { 1, 2, 4, 5, 3, 6 };
    int n = sizeof(in) / sizeof(in[0]);
    cout << "Postorder traversal " << endl;
    printPostOrder(in, pre, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print postorder
// traversal from preorder and
// inorder traversals
import java.util.Arrays;

class GFG
{

// A utility function to search x in arr[] of size n
static int search(int arr[], int x, int n)
{
    for (int i = 0; i < n; i++)
        if (arr[i] == x)
            return i;
    return -1;
}

// Prints postorder traversal from
// given inorder and preorder traversals
static void printPostOrder(int in1[],
                    int pre[], int n)
{
    // The first element in pre[] is
    // always root, search it in in[]
    // to find left and right subtrees
    int root = search(in1, pre[0], n);

    // If left subtree is not empty,
    // print left subtree
    if (root != 0)
        printPostOrder(in1, Arrays.copyOfRange(pre, 1, n), root);

    // If right subtree is not empty,
    // print right subtree
    if (root != n - 1)
        printPostOrder(Arrays.copyOfRange(in1, root+1, n),
            Arrays.copyOfRange(pre, 1+root, n), n - root - 1);

    // Print root
    System.out.print( pre[0] + " ");
}

// Driver code
public static void main(String args[])
{
    int in1[] = { 4, 2, 5, 1, 3, 6 };
    int pre[] = { 1, 2, 4, 5, 3, 6 };
    int n = in1.length;
    System.out.println("Postorder traversal " );
    printPostOrder(in1, pre, n);
}
}
// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to print postorder
# traversal from preorder and inorder
# traversals

# A utility function to search x in
# arr[] of size n
def search(arr, x, n):

    for i in range(n):
        if (arr[i] == x):
            return i

    return -1

# Prints postorder traversal from
# given inorder and preorder traversals
def printPostOrder(In, pre, n):

    # The first element in pre[] is always
    # root, search it in in[] to find left
    # and right subtrees
    root = search(In, pre[0], n)

    # If left subtree is not empty,
    # print left subtree
    if (root != 0):
        printPostOrder(In, pre[1:n], root)

    # If right subtree is not empty,
    # print right subtree
    if (root != n - 1):
        printPostOrder(In[root + 1 : n],
                      pre[root + 1 : n],
                      n - root - 1)

    # Print root
    print(pre[0], end = " ")

# Driver code
In = [ 4, 2, 5, 1, 3, 6 ]
pre = [ 1, 2, 4, 5, 3, 6 ]
n = len(In)

print("Postorder traversal ")

printPostOrder(In, pre, n)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to print postorder
// traversal from preorder and
// inorder traversals
using System;

class GFG
{

// A utility function to search x
// in []arr of size n
static int search(int []arr,
                  int x, int n)
{
    for (int i = 0; i < n; i++)
        if (arr[i] == x)
            return i;
    return -1;
}

// Prints postorder traversal from
// given inorder and preorder traversals
static void printPostOrder(int []in1,
                    int []pre, int n)
{
    // The first element in pre[] is
    // always root, search it in in[]
    // to find left and right subtrees
    int root = search(in1, pre[0], n);

    // If left subtree is not empty,
    // print left subtree
    int []ar;
    if (root != 0)
    {
        ar = new int[n - 1];
        Array.Copy(pre, 1, ar, 0, n - 1);
        printPostOrder(in1, ar, root);
    }

    // If right subtree is not empty,
    // print right subtree
    if (root != n - 1)
    {
        ar = new int[n - (root + 1)];
        Array.Copy(in1, root + 1, ar, 0,
                        n - (root + 1));
        int []ar1 = new int[n - (root + 1)];
        Array.Copy(pre, root + 1, ar1, 0,
                         n - (root + 1));
        printPostOrder(ar, ar1, n - root - 1);
    }

    // Print root
    Console.Write(pre[0] + " ");
}

// Driver code
public static void Main(String []args)
{
    int []in1 = { 4, 2, 5, 1, 3, 6 };
    int []pre = { 1, 2, 4, 5, 3, 6 };
    int n = in1.Length;
    Console.WriteLine("Postorder traversal " );
    printPostOrder(in1, pre, n);
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
Postorder traversal 
4 5 2 6 3 1
```

下面是实现。

## C++

```
// C++ program to print Postorder
// traversal from given Inorder
// and Preorder traversals.
#include <iostream>
using namespace std;

int preIndex = 0;

int search(int arr[], int startIn,int endIn, int data)
{
    int i = 0;
    for (i = startIn; i < endIn; i++)
    {
        if (arr[i] == data)
        {
            return i;
        }
    }
    return i;
}
void printPost(int arr[], int pre[],int inStrt, int inEnd)
{
    if (inStrt > inEnd)
    {
        return;
    }

    // Find index of next item in preorder
    // traversal in inorder.
    int inIndex = search(arr, inStrt, inEnd,pre[preIndex++]);

    // traverse left tree
    printPost(arr, pre, inStrt, inIndex - 1);

    // traverse right tree
    printPost(arr, pre, inIndex + 1, inEnd);

    // print root node at the end of traversal
    cout << arr[inIndex] << " ";
}

// Driver code
int main()
{
    int arr[] = {4, 2, 5, 1, 3, 6};
    int pre[] = {1, 2, 4, 5, 3, 6};
    int len = sizeof(arr)/sizeof(arr[0]);
    printPost(arr, pre, 0, len - 1);
}

// This code is contributed by SHUBHAMSINGH10
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print Postorder traversal from given Inorder
// and Preorder traversals.

public class PrintPost {
    static int preIndex = 0;
    void printPost(int[] in, int[] pre, int inStrt, int inEnd)
    {
        if (inStrt > inEnd)
            return;       

        // Find index of next item in preorder traversal in
        // inorder.
        int inIndex = search(in, inStrt, inEnd, pre[preIndex++]);

        // traverse left tree
        printPost(in, pre, inStrt, inIndex - 1);

        // traverse right tree
        printPost(in, pre, inIndex + 1, inEnd);

        // print root node at the end of traversal
        System.out.print(in[inIndex] + " ");
    }

    int search(int[] in, int startIn, int endIn, int data)
    {
        int i = 0;
        for (i = startIn; i < endIn; i++)
            if (in[i] == data)
                return i;           
        return i;
    }

    // Driver code
    public static void main(String ars[])
    {
        int in[] = { 4, 2, 5, 1, 3, 6 };
        int pre[] = { 1, 2, 4, 5, 3, 6 };
        int len = in.length;
        PrintPost tree = new PrintPost();
        tree.printPost(in, pre, 0, len - 1);
    }
}
```

## C#

```
// C# program to print Postorder
// traversal from given Inorder
// and Preorder traversals.
using System;

class GFG
{
public static int preIndex = 0;
public virtual void printPost(int[] arr, int[] pre,
                              int inStrt, int inEnd)
{
    if (inStrt > inEnd)
    {
        return;
    }

    // Find index of next item in preorder
    // traversal in inorder.
    int inIndex = search(arr, inStrt, inEnd,
                         pre[preIndex++]);

    // traverse left tree
    printPost(arr, pre, inStrt, inIndex - 1);

    // traverse right tree
    printPost(arr, pre, inIndex + 1, inEnd);

    // print root node at the end of traversal
    Console.Write(arr[inIndex] + " ");
}

public virtual int search(int[] arr, int startIn,
                          int endIn, int data)
{
    int i = 0;
    for (i = startIn; i < endIn; i++)
    {
        if (arr[i] == data)
        {
            return i;
        }
    }
    return i;
}

// Driver code
public static void Main(string[] ars)
{
    int[] arr = new int[] {4, 2, 5, 1, 3, 6};
    int[] pre = new int[] {1, 2, 4, 5, 3, 6};
    int len = arr.Length;
    GFG tree = new GFG();
    tree.printPost(arr, pre, 0, len - 1);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

      // JavaScript program to print Postorder
      // traversal from given Inorder
      // and Preorder traversals.
      class GFG {
        constructor() {
          this.preIndex = 0;
        }
        printPost(arr, pre, inStrt, inEnd) {
          if (inStrt > inEnd) {
            return;
          }

          // Find index of next item in preorder
          // traversal in inorder.
          var inIndex = this.search(arr, inStrt, inEnd,
          pre[this.preIndex++]);

          // traverse left tree
          this.printPost(arr, pre, inStrt, inIndex - 1);

          // traverse right tree
          this.printPost(arr, pre, inIndex + 1, inEnd);

          // print root node at the end of traversal
          document.write(arr[inIndex] + " ");
        }

        search(arr, startIn, endIn, data) {
          var i = 0;
          for (i = startIn; i < endIn; i++) {
            if (arr[i] == data) {
              return i;
            }
          }
          return i;
        }
      }
      // Driver code
      var arr = [4, 2, 5, 1, 3, 6];
      var pre = [1, 2, 4, 5, 3, 6];
      var len = arr.length;
      var tree = new GFG();
      tree.printPost(arr, pre, 0, len - 1);

</script>
```

**Output:** 

```
4 5 2 6 3 1
```

**时间复杂度:**上述函数访问数组中的每个节点。对于每次访问，它都调用搜索，这需要 O(n)个时间。因此，该功能的整体时间复杂度为 O(n <sup>2</sup>

上述解决方案可以使用哈希进行优化。我们使用一个 HashMap 来存储元素及其索引，这样我们就可以快速找到一个元素的索引。

## C++

```
// C++ program to print Postorder traversal from
// given Inorder and Preorder traversals.
#include<bits/stdc++.h>
using namespace std;

int preIndex = 0;
void printPost(int in[], int pre[], int inStrt,
               int inEnd, map<int, int> hm)
{
    if (inStrt > inEnd)
        return;        

    // Find index of next item in preorder traversal in
    // inorder.
    int inIndex = hm[pre[preIndex++]];

    // traverse left tree
    printPost(in, pre, inStrt, inIndex - 1, hm);

    // traverse right tree
    printPost(in, pre, inIndex + 1, inEnd, hm);

    // print root node at the end of traversal
    cout << in[inIndex] << " ";
}

void printPostMain(int in[], int pre[],int n)
{
    map<int,int> hm ;
    for (int i = 0; i < n; i++)
    hm[in[i]] = i;

    printPost(in, pre, 0, n - 1, hm);
}

// Driver code
int main()
{
    int in[] = { 4, 2, 5, 1, 3, 6 };
    int pre[] = { 1, 2, 4, 5, 3, 6 };
    int n = sizeof(pre)/sizeof(pre[0]);

    printPostMain(in, pre, n);
    return 0;
}

// This code is contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print Postorder traversal from
// given Inorder and Preorder traversals.
import java.util.*;

public class PrintPost {
    static int preIndex = 0;
    void printPost(int[] in, int[] pre, int inStrt,
               int inEnd, HashMap<Integer, Integer> hm)
    {
        if (inStrt > inEnd)
            return;        

        // Find index of next item in preorder traversal in
        // inorder.
        int inIndex = hm.get(pre[preIndex++]);

        // traverse left tree
        printPost(in, pre, inStrt, inIndex - 1, hm);

        // traverse right tree
        printPost(in, pre, inIndex + 1, inEnd, hm);

        // print root node at the end of traversal
        System.out.print(in[inIndex] + " ");
    }

    void printPostMain(int[] in, int[] pre)
    {
        int n = pre.length;
        HashMap<Integer, Integer> hm = new HashMap<Integer, Integer>();
        for (int i=0; i<n; i++)
           hm.put(in[i], i);

        printPost(in, pre, 0, n-1, hm);
    }

    // Driver code
    public static void main(String ars[])
    {
        int in[] = { 4, 2, 5, 1, 3, 6 };
        int pre[] = { 1, 2, 4, 5, 3, 6 };
        PrintPost tree = new PrintPost();
        tree.printPostMain(in, pre);
    }
}
```

## 蟒蛇 3

```
# Python3 program to prPostorder traversal from
# given Inorder and Preorder traversals.

def printPost(inn, pre, inStrt, inEnd):
    global preIndex, hm
    if (inStrt > inEnd):
        return

    # Find index of next item in preorder traversal in
    # inorder.
    inIndex = hm[pre[preIndex]]
    preIndex += 1

    # traverse left tree
    printPost(inn, pre, inStrt, inIndex - 1)

    # traverse right tree
    printPost(inn, pre, inIndex + 1, inEnd)

    # prroot node at the end of traversal
    print(inn[inIndex], end = " ")

def printPostMain(inn, pre, n):

    for i in range(n):
        hm[inn[i]] = i

    printPost(inn, pre, 0, n - 1)

# Driver code
if __name__ == '__main__':
    hm = {}
    preIndex = 0
    inn = [4, 2, 5, 1, 3, 6]
    pre = [1, 2, 4, 5, 3, 6]

    n = len(pre)

    printPostMain(inn, pre, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print Postorder
// traversal from given Inorder
// and Preorder traversals.
using System;

class GFG
{
public static int preIndex = 0;
public virtual void printPost(int[] arr, int[] pre,
                              int inStrt, int inEnd)
{
    if (inStrt > inEnd)
    {
        return;
    }

    // Find index of next item in preorder
    // traversal in inorder.
    int inIndex = search(arr, inStrt, inEnd,
                         pre[preIndex++]);

    // traverse left tree
    printPost(arr, pre, inStrt, inIndex - 1);

    // traverse right tree
    printPost(arr, pre, inIndex + 1, inEnd);

    // print root node at the
    // end of traversal
    Console.Write(arr[inIndex] + " ");
}

public virtual int search(int[] arr, int startIn,
                          int endIn, int data)
{
    int i = 0;
    for (i = startIn; i < endIn; i++)
    {
        if (arr[i] == data)
        {
            return i;
        }
    }
    return i;
}

// Driver code
public static void Main(string[] ars)
{
    int[] arr = new int[] {4, 2, 5, 1, 3, 6};
    int[] pre = new int[] {1, 2, 4, 5, 3, 6};
    int len = arr.Length;
    GFG tree = new GFG();
    tree.printPost(arr, pre, 0, len - 1);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to print
// Postorder traversal from given
// Inorder and Preorder traversals.
let preIndex = 0;

function printPost(In, pre, inStrt, inEnd, hm)
{
    if (inStrt > inEnd)
        return;       

    // Find index of next item in
    // preorder traversal in inorder.
    let inIndex = hm.get(pre[preIndex++]);

    // Traverse left tree
    printPost(In, pre, inStrt, inIndex - 1, hm);

    // Traverse right tree
    printPost(In, pre, inIndex + 1, inEnd, hm);

    // Print root node at the end of traversal
    document.write(In[inIndex] + " ");
}

function printPostMain(In, pre)
{
    let n = pre.length;
    let hm = new Map();

    for(let i = 0; i < n; i++)
       hm.set(In[i], i);

    printPost(In, pre, 0, n - 1, hm);
}

// Driver code
let In = [ 4, 2, 5, 1, 3, 6 ];
let pre = [ 1, 2, 4, 5, 3, 6 ];

printPostMain(In, pre);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
4 5 2 6 3 1
```

**时间复杂度:** O(n)
如果发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息
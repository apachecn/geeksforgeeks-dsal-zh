# 检查给定的数组是否可以表示二叉查找树的前序遍历

> 原文:[https://www . geesforgeks . org/check-if-a-给定-array-can-representative-preorder-遍历二进制搜索树/](https://www.geeksforgeeks.org/check-if-a-given-array-can-represent-preorder-traversal-of-binary-search-tree/)

给定一个数字数组，如果给定数组可以表示二叉查找树的前序遍历，则返回 true，否则返回 false。预期时间复杂度为 0(n)。

**示例:**

```
Input:  pre[] = {2, 4, 3}
Output: true
Given array can represent preorder traversal
of below tree
    2
     \
      4
     /
    3

Input:  pre[] = {2, 4, 1}
Output: false
Given array cannot represent preorder traversal
of a Binary Search Tree.

Input:  pre[] = {40, 30, 35, 80, 100}
Output: true
Given array can represent preorder traversal
of below tree
     40
   /   \
 30    80 
  \      \
  35     100 

Input:  pre[] = {40, 30, 35, 20, 80, 100}
Output: false
Given array cannot represent preorder traversal
of a Binary Search Tree.
```

一个**简单的解决方案**是从第一个节点开始对每个节点进行以下操作。

```
1) Find the first greater value on right side of current node. 
   Let the index of this node be j. Return true if following 
   conditions hold. Else return false
    (i)  All values after the above found greater value are 
         greater than current node.
    (ii) Recursive calls for the subarrays pre[i+1..j-1] and 
         pre[j+1..n-1] also return true. 
```

上述解的时间复杂度为 O(n <sup>2</sup> )

一个**高效解**可以在 O(n)时间内解决这个问题。想法是使用堆栈。这个问题类似于[下一个(或最接近的)大元素问题](https://www.geeksforgeeks.org/next-greater-element/)。这里我们找到下一个更大的元素，在找到下一个更大的元素之后，如果我们找到一个更小的元素，那么返回 false。

```
1) Create an empty stack.
2) Initialize root as INT_MIN.
3) Do following for every element pre[i]
     a) If pre[i] is smaller than current root, return false.
     b) Keep removing elements from stack while pre[i] is greater
        then stack top. Make the last removed item as new root (to
        be compared next).
        At this point, pre[i] is greater than the removed root
        (That is why if we see a smaller element in step a), we 
        return false)
     c) push pre[i] to stack (All elements in stack are in decreasing
        order)  
```

以下是上述想法的实现。

## C++

```
// C++ program for an efficient solution to check if
// a given array can represent Preorder traversal of
// a Binary Search Tree
#include<bits/stdc++.h>
using namespace std;

bool canRepresentBST(int pre[], int n)
{
    // Create an empty stack
    stack<int> s;

    // Initialize current root as minimum possible
    // value
    int root = INT_MIN;

    // Traverse given array
    for (int i=0; i<n; i++)
    {
        // If we find a node who is on right side
        // and smaller than root, return false
        if (pre[i] < root)
            return false;

        // If pre[i] is in right subtree of stack top,
        // Keep removing items smaller than pre[i]
        // and make the last removed item as new
        // root.
        while (!s.empty() && s.top()<pre[i])
        {
            root = s.top();
            s.pop();
        }

        // At this point either stack is empty or
        // pre[i] is smaller than root, push pre[i]
        s.push(pre[i]);
    }
    return true;
}

// Driver program
int main()
{
    int pre1[] = {40, 30, 35, 80, 100};
    int n = sizeof(pre1)/sizeof(pre1[0]);
    canRepresentBST(pre1, n)? cout << "true\n":
                              cout << "false\n";

    int pre2[] = {40, 30, 35, 20, 80, 100};
    n = sizeof(pre2)/sizeof(pre2[0]);
    canRepresentBST(pre2, n)? cout << "true\n":
                              cout << "false\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for an efficient solution to check if
// a given array can represent Preorder traversal of
// a Binary Search Tree
import java.util.Stack;

class BinarySearchTree {

    boolean canRepresentBST(int pre[], int n) {
        // Create an empty stack
        Stack<Integer> s = new Stack<Integer>();

        // Initialize current root as minimum possible
        // value
        int root = Integer.MIN_VALUE;

        // Traverse given array
        for (int i = 0; i < n; i++) {
            // If we find a node who is on right side
            // and smaller than root, return false
            if (pre[i] < root) {
                return false;
            }

            // If pre[i] is in right subtree of stack top,
            // Keep removing items smaller than pre[i]
            // and make the last removed item as new
            // root.
            while (!s.empty() && s.peek() < pre[i]) {
                root = s.peek();
                s.pop();
            }

            // At this point either stack is empty or
            // pre[i] is smaller than root, push pre[i]
            s.push(pre[i]);
        }
        return true;
    }

    public static void main(String args[]) {
        BinarySearchTree bst = new BinarySearchTree();
        int[] pre1 = new int[]{40, 30, 35, 80, 100};
        int n = pre1.length;
        if (bst.canRepresentBST(pre1, n) == true) {
            System.out.println("true");
        } else {
            System.out.println("false");
        }
        int[] pre2 = new int[]{40, 30, 35, 20, 80, 100};
        int n1 = pre2.length;
        if (bst.canRepresentBST(pre2, n) == true) {
            System.out.println("true");
        } else {
            System.out.println("false");
        }
    }
}

//This code is contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program for an efficient solution to check if
# a given array can represent Preorder traversal of
# a Binary Search Tree

INT_MIN = -2**32

def canRepresentBST(pre):

    # Create an empty stack
    s = []

    # Initialize current root as minimum possible value
    root = INT_MIN

    # Traverse given array
    for value in pre:
        #NOTE:value is equal to pre[i] according to the
        #given algo  

        # If we find a node who is on the right side
        # and smaller than root, return False
        if value < root :
            return False

        # If value(pre[i]) is in right subtree of stack top,
        # Keep removing items smaller than value
        # and make the last removed items as new root
        while(len(s) > 0 and s[-1] < value) :
            root = s.pop()

        # At this point either stack is empty or value
        # is smaller than root, push value
        s.append(value)

    return True

# Driver Program
pre1 = [40 , 30 , 35 , 80 , 100]
print "true" if canRepresentBST(pre1) == True else "false"
pre2 = [40 , 30 , 35 , 20 ,  80 , 100]
print "true" if canRepresentBST(pre2) == True else "false"

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program for an efficient solution
// to check if a given array can represent 
// Preorder traversal of a Binary Search Tree
using System;
using System.Collections.Generic;

class GFG
{

public virtual bool canRepresentBST(int[] pre, int n)
{
    // Create an empty stack
    Stack<int> s = new Stack<int>();

    // Initialize current root as minimum
    // possible value
    int root = int.MinValue;

    // Traverse given array
    for (int i = 0; i < n; i++)
    {
        // If we find a node who is on right side
        // and smaller than root, return false
        if (pre[i] < root)
        {
            return false;
        }

        // If pre[i] is in right subtree of stack top,
        // Keep removing items smaller than pre[i]
        // and make the last removed item as new
        // root.
        while (s.Count > 0 && s.Peek() < pre[i])
        {
            root = s.Peek();
            s.Pop();
        }

        // At this point either stack is empty or
        // pre[i] is smaller than root, push pre[i]
        s.Push(pre[i]);
    }
    return true;
}

// Driver Code
public static void Main(string[] args)
{
    GFG bst = new GFG();
    int[] pre1 = new int[]{40, 30, 35, 80, 100};
    int n = pre1.Length;
    if (bst.canRepresentBST(pre1, n) == true)
    {
        Console.WriteLine("true");
    }
    else
    {
        Console.WriteLine("false");
    }
    int[] pre2 = new int[]{40, 30, 35, 20, 80, 100};
    int n1 = pre2.Length;
    if (bst.canRepresentBST(pre2, n) == true)
    {
        Console.WriteLine("true");
    }
    else
    {
        Console.WriteLine("false");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program for an efficient
// solution to check if a given array
// can represent Preorder traversal of
// a Binary Search Tree
function canRepresentBST(pre, n)
{

    // Create an empty stack
    var s = [];

    // Initialize current root as minimum possible
    // value
    var root = -1000000000;

    // Traverse given array
    for(var i = 0; i < n; i++)
    {

        // If we find a node who is on right side
        // and smaller than root, return false
        if (pre[i] < root)
            return false;

        // If pre[i] is in right subtree of stack top,
        // Keep removing items smaller than pre[i]
        // and make the last removed item as new
        // root.
        while (s.length != 0 && s[s.length - 1] < pre[i])
        {
            root = s[s.length - 1];
            s.pop();
        }

        // At this point either stack is empty or
        // pre[i] is smaller than root, push pre[i]
        s.push(pre[i]);
    }
    return true;
}

// Driver code
var pre1 = [ 40, 30, 35, 80, 100 ];
var n = pre1.length;
canRepresentBST(pre1, n) ? document.write("true<br>"):
                           document.write("false<br>");
var pre2 = [ 40, 30, 35, 20, 80, 100 ];
n = pre2.length;
canRepresentBST(pre2, n) ? document.write("true"):
                           document.write("false");

// This code is contributed by importantly

</script>
```

**Output**

```
true
false
```

**另一种方法:**

我们可以在不使用堆栈的情况下检查给定的前序遍历对于一个 BST 是否有效。这个想法是使用类似的概念[“使用收缩边界算法构建一个 BST”](https://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversa/)。我们将递归访问所有节点，但不会构建节点。最后，如果没有遍历完整的数组，那么这意味着数组不能代表任何二叉树的前序遍历。

下面是上述想法的实现:

## C++

```
// C++ program to illustrate if a given array can represent
// a preorder traversal of a BST or not

#include <bits/stdc++.h>
using namespace std;

// We are actually not building the tree
void buildBST_helper(int& preIndex, int n, int pre[],
                     int min, int max)
{
    if (preIndex >= n)
        return;

    if (min <= pre[preIndex] && pre[preIndex] <= max) {
        // build node
        int rootData = pre[preIndex];
        preIndex++;

        // build left subtree
        buildBST_helper(preIndex, n, pre, min, rootData);

        // build right subtree
        buildBST_helper(preIndex, n, pre, rootData, max);
    }
    // else
    // return NULL;
}

bool canRepresentBST(int arr[], int N)
{
    // code here
    int min = INT_MIN, max = INT_MAX;
    int preIndex = 0;

    buildBST_helper(preIndex, N, arr, min, max);

    return preIndex == N;
}

// Driver Code
int main()
{

    int preorder1[] = { 2, 4, 3 };
    /*
            2
            \
             4
            /
           3

*/
    int n1 = sizeof(preorder1) / sizeof(preorder1[0]);

    if (canRepresentBST(preorder1, n1))
        cout << "\npreorder1 can represent BST";
    else
        cout << "\npreorder1 can not represent BST  :(";

    int preorder2[] = { 5, 3, 4, 1, 6, 10 };
    int n2 = sizeof(preorder2) / sizeof(preorder2[0]);
    /*
                    5
         /     \
       3         1
         \     /  \
         4    6    10

*/
    if (canRepresentBST(preorder2, n2))
        cout << "\npreorder2 can represent BST";
    else
        cout << "\npreorder2 can not represent BST  :(";

    int preorder3[] = { 5, 3, 4, 8, 6, 10 };
    int n3 = sizeof(preorder3) / sizeof(preorder3[0]);
    /*
                    5
         /     \
       3         8
         \     /  \
         4    6    10

*/
    if (canRepresentBST(preorder3, n3))
        cout << "\npreorder3 can represent BST";
    else
        cout << "\npreorder3 can not represent BST  :(";

    return 0;
}

// This code is contributed by Sourashis Mondal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate if a given array can represent
// a preorder traversal of a BST or not
public class Main
{
    static int preIndex = 0;

    // We are actually not building the tree
    static void buildBST_helper(int n, int[] pre, int min, int max)
    {
        if (preIndex >= n)
            return;

        if (min <= pre[preIndex] && pre[preIndex] <= max) {

            // build node
            int rootData = pre[preIndex];
            preIndex++;

            // build left subtree
            buildBST_helper(n, pre, min, rootData);

            // build right subtree
            buildBST_helper(n, pre, rootData, max);
        }
        // else
        // return NULL;
    }

    static boolean canRepresentBST(int[] arr, int N)
    {
        // code here
        int min = Integer.MIN_VALUE, max = Integer.MAX_VALUE;

        buildBST_helper(N, arr, min, max);

        return preIndex == N;
    }

    public static void main(String[] args) {
        int[] preorder1 = { 2, 4, 3 };
        /*
                2
                \
                 4
                /
               3
        */
        int n1 = preorder1.length;
        System.out.println();
        if (canRepresentBST(preorder1, n1))
            System.out.print("preorder1 can represent BST");
        else
            System.out.print("preorder1 can not represent BST  :(");

        int[] preorder2 = { 5, 3, 4, 1, 6, 10 };
        int n2 = preorder2.length;
        System.out.println();
        /*
                        5
             /     \
           3         1
             \     /  \
             4    6    10
        */
        if (!canRepresentBST(preorder2, n2))
            System.out.print("preorder2 can represent BST");
        else
            System.out.print("preorder2 can not represent BST  :(");

        int[] preorder3 = { 5, 3, 4, 8, 6, 10 };
        int n3 = preorder3.length;
        System.out.println();
        /*
                        5
             /     \
           3         8
             \     /  \
             4    6    10
        */
        if (canRepresentBST(preorder3, n3))
            System.out.print("preorder3 can represent BST");
        else
            System.out.print("preorder3 can not represent BST  :(");
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program to illustrate if a given array can represent
# a preorder traversal of a BST or not
import sys

preIndex = 0

# We are actually not building the tree
def buildBST_helper(n, pre, Min, Max):
    global preIndex
    if (preIndex >= n):
        return

    if (Min <= pre[preIndex] and pre[preIndex] <= Max):
        # build node
        rootData = pre[preIndex]
        preIndex+=1

        # build left subtree
        buildBST_helper(n, pre, Min, rootData)

        # build right subtree
        buildBST_helper(n, pre, rootData, Max)
    # else
    # return NULL

def canRepresentBST(arr, N):
    global preIndex
    # code here
    Min, Max = sys.maxsize, -sys.maxsize

    buildBST_helper(N, arr, Min, Max)

    if preIndex == N:
        return True

    return False

preorder1 = [ 2, 4, 3 ]
"""
        2
        \
         4
        /
       3

"""
n1 = len(preorder1)

if (not canRepresentBST(preorder1, n1)):
  print("preorder1 can represent BST");
else:
  print("preorder1 can not represent BST  :(")

preorder2 = [ 5, 3, 4, 1, 6, 10 ]
n2 = len(preorder2)
"""
                      5
           /     \
         3         1
           \     /  \
           4    6    10

"""
if (canRepresentBST(preorder2, n2)):
  print("preorder2 can represent BST")
else:
  print("preorder2 can not represent BST  :(")

preorder3 = [ 5, 3, 4, 8, 6, 10 ]
n3 = len(preorder3)
"""
                      5
           /     \
         3         8
           \     /  \
           4    6    10
"""
if (not canRepresentBST(preorder3, n3)):
  print("preorder3 can represent BST")
else:
  print("preorder3 can not represent BST  :(")
```

## C#

```
// C# program to illustrate if a given array can represent
// a preorder traversal of a BST or not
using System;
class GFG {

    static int preIndex = 0;

    // We are actually not building the tree
    static void buildBST_helper(int n, int[] pre, int min, int max)
    {
        if (preIndex >= n)
            return;

        if (min <= pre[preIndex] && pre[preIndex] <= max) {
            // build node
            int rootData = pre[preIndex];
            preIndex++;

            // build left subtree
            buildBST_helper(n, pre, min, rootData);

            // build right subtree
            buildBST_helper(n, pre, rootData, max);
        }
        // else
        // return NULL;
    }

    static bool canRepresentBST(int[] arr, int N)
    {
        // code here
        int min = Int32.MinValue, max = Int32.MaxValue;

        buildBST_helper(N, arr, min, max);

        return preIndex == N;
    }

  static void Main() {
    int[] preorder1 = { 2, 4, 3 };
    /*
            2
            \
             4
            /
           3
    */
    int n1 = preorder1.Length;
    Console.WriteLine();
    if (canRepresentBST(preorder1, n1))
        Console.Write("preorder1 can represent BST");
    else
        Console.Write("preorder1 can not represent BST  :(");

    int[] preorder2 = { 5, 3, 4, 1, 6, 10 };
    int n2 = preorder2.Length;
    Console.WriteLine();
    /*
                    5
         /     \
       3         1
         \     /  \
         4    6    10
    */
    if (!canRepresentBST(preorder2, n2))
        Console.Write("preorder2 can represent BST");
    else
        Console.Write("preorder2 can not represent BST  :(");

    int[] preorder3 = { 5, 3, 4, 8, 6, 10 };
    int n3 = preorder3.Length;
    Console.WriteLine();
    /*
                    5
         /     \
       3         8
         \     /  \
         4    6    10
    */
    if (canRepresentBST(preorder3, n3))
        Console.Write("preorder3 can represent BST");
    else
        Console.Write("preorder3 can not represent BST  :(");
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>
    // Javascript program to illustrate if a given array can represent
    // a preorder traversal of a BST or not

    let preIndex = 0;

    // We are actually not building the tree
    function buildBST_helper(n, pre, min, max)
    {
        if (preIndex >= n)
            return;

        if (min <= pre[preIndex] && pre[preIndex] <= max) {
            // build node
            let rootData = pre[preIndex];
            preIndex++;

            // build left subtree
            buildBST_helper(n, pre, min, rootData);

            // build right subtree
            buildBST_helper(n, pre, rootData, max);
        }
        // else
        // return NULL;
    }

    function canRepresentBST(arr, N)
    {
        // code here
        let min = Number.MIN_VALUE, max = Number.MAX_VALUE;

        buildBST_helper(N, arr, min, max);

        return preIndex == N;
    }

    let preorder1 = [ 2, 4, 3 ];
    /*
            2
            \
             4
            /
           3

    */
    let n1 = preorder1.length;

    if (canRepresentBST(preorder1, n1))
      document.write("</br>" + "preorder1 can represent BST");
    else
      document.write("</br>" + "preorder1 can not represent BST  :(");

    let preorder2 = [ 5, 3, 4, 1, 6, 10 ];
    let n2 = preorder2.length;
    /*
                          5
               /     \
             3         1
               \     /  \
               4    6    10

      */
    if (!canRepresentBST(preorder2, n2))
      document.write("</br>" + "preorder2 can represent BST");
    else
      document.write("</br>" + "preorder2 can not represent BST  :(");

    let preorder3 = [ 5, 3, 4, 8, 6, 10 ];
    let n3 = preorder3.length;
    /*
                          5
               /     \
             3         8
               \     /  \
               4    6    10

      */
    if (canRepresentBST(preorder3, n3))
      document.write("</br>" + "preorder3 can represent BST");
    else
      document.write("</br>" + "preorder3 can not represent BST  :(");

// This code is contributed by decode2207.
</script>
```

**Output**

```
preorder1 can represent BST
preorder2 can not represent BST  :(
preorder3 can represent BST
```

**时间复杂度:**O(N)
T3】辅助空间: O(可能二叉树的高度)

本文由 [**罗米尔·普那沙**](https://www.facebook.com/romilpunetha) 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息
# 在不建立树的情况下检查相同的基站

> 原文:[https://www . geeksforgeeks . org/check-for-相同-bsts-无需构建树/](https://www.geeksforgeeks.org/check-for-identical-bsts-without-building-the-trees/)

给定两个代表一系列键的数组。假设我们用每个数组做一个二叉查找树。我们需要在不实际构建树的情况下判断两个 BST 是否相同。
示例
例如，输入数组为{2，4，3，1}和{2，1，4，3}将构建同一棵树

```
 Let the input arrays be a[] and b[]

Example 1:
a[] = {2, 4, 1, 3} will construct following tree.
   2
 /  \
1    4
    /
   3
b[] = {2, 4, 3, 1} will also also construct the same tree.
   2
 /  \
1    4
    /
   3 
So the output is "True"

Example 2:
a[] = {8, 3, 6, 1, 4, 7, 10, 14, 13}
b[] = {8, 10, 14, 3, 6, 4, 1, 7, 13}

They both construct the same following BST, so output is "True"
            8
         /    \
       3       10
     /  \        \
    1     6       14
        /   \     /
       4     7   13  
```

**解法:**
根据 BST 性质，左子树的元素必须小于，右子树的元素必须大于根。
如果对于每个元素 x，x 的左右子树中的元素在两个数组中都出现在它之后，则两个数组表示相同的 BST。左右子树的根也是如此。
这个想法是检查下一个更小和更大的元素在两个数组中是否相同。递归检查左右子树的相同属性。这个想法看起来很简单，但是实现需要检查所有元素的所有条件。下面是这个想法的一个有趣的递归实现。

## C++

```
// A C++ program to check for Identical
// BSTs without building the trees
#include <bits/stdc++.h>
using namespace std;

/* The main function that checks if two
arrays a[] and b[] of size n construct
same BST. The two values 'min' and 'max'
decide whether the call is made for left
subtree or right subtree of a parent
element. The indexes i1 and i2 are the
indexes in (a[] and b[]) after which we
search the left or right child. Initially,
the call is made for INT_MIN and INT_MAX
as 'min' and 'max' respectively, because
root has no parent. i1 and i2 are just
after the indexes of the parent element in a[] and b[]. */
bool isSameBSTUtil(int a[], int b[],
                int n, int i1, int i2,
                    int min, int max)
{
int j, k;

/* Search for a value satisfying the
constraints of min and max in a[] and
b[]. If the parent element is a leaf
node then there must be some elements
in a[] and b[] satisfying constraint. */
for (j = i1; j < n; j++)
    if (a[j] > min && a[j] < max)
        break;
for (k = i2; k < n; k++)
    if (b[k] > min && b[k] < max)
        break;

/* If the parent element is leaf in both arrays */
if (j==n && k==n)
    return true;

/* Return false if any of the following is true
    a) If the parent element is leaf in one array,
        but non-leaf in other.
    b) The elements satisfying constraints are
        not same. We either search for left
        child or right child of the parent
        element (decinded by min and max values).
        The child found must be same in both arrays */
if (((j==n)^(k==n)) || a[j]!=b[k])
    return false;

/* Make the current child as parent and
recursively check for left and right
subtrees of it. Note that we can also
pass a[k] in place of a[j] as they
are both are same */
return isSameBSTUtil(a, b, n, j+1, k+1, a[j], max) && // Right Subtree
        isSameBSTUtil(a, b, n, j+1, k+1, min, a[j]); // Left Subtree
}

// A wrapper over isSameBSTUtil()
bool isSameBST(int a[], int b[], int n)
{
return isSameBSTUtil(a, b, n, 0, 0, INT_MIN, INT_MAX);
}

// Driver code
int main()
{
    int a[] = {8, 3, 6, 1, 4, 7, 10, 14, 13};
    int b[] = {8, 10, 14, 3, 6, 4, 1, 7, 13};
    int n=sizeof(a)/sizeof(a[0]);
    if(isSameBST(a, b, n))
    {
        cout << "BSTs are same";
    }
    else
    {
        cout << "BSTs not same";
    }
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// A C program to check for Identical BSTs without building the trees
#include<stdio.h>
#include<limits.h>
#include<stdbool.h>

/* The main function that checks if two arrays a[] and b[] of size n construct
  same BST. The two values 'min' and 'max' decide whether the call is made for
  left subtree or right subtree of a parent element. The indexes i1 and i2 are
  the indexes in (a[] and b[]) after which we search the left or right child.
  Initially, the call is made for INT_MIN and INT_MAX as 'min' and 'max'
  respectively, because root has no parent.
  i1 and i2 are just after the indexes of the parent element in a[] and b[]. */
bool isSameBSTUtil(int a[], int b[], int n, int i1, int i2, int min, int max)
{
   int j, k;

   /* Search for a value satisfying the constraints of min and max in a[] and
      b[]. If the parent element is a leaf node then there must be some
      elements in a[] and b[] satisfying constraint. */
   for (j=i1; j<n; j++)
       if (a[j]>min && a[j]<max)
           break;
   for (k=i2; k<n; k++)
       if (b[k]>min && b[k]<max)
           break;

   /* If the parent element is leaf in both arrays */
   if (j==n && k==n)
       return true;

   /* Return false if any of the following is true
      a) If the parent element is leaf in one array, but non-leaf in other.
      b) The elements satisfying constraints are not same. We either search
         for left child or right child of the parent element (decinded by min
         and max values). The child found must be same in both arrays */
   if (((j==n)^(k==n)) || a[j]!=b[k])
       return false;

   /* Make the current child as parent and recursively check for left and right
      subtrees of it. Note that we can also pass a[k] in place of a[j] as they
      are both are same */
   return isSameBSTUtil(a, b, n, j+1, k+1, a[j], max) &&  // Right Subtree
          isSameBSTUtil(a, b, n, j+1, k+1, min, a[j]);    // Left Subtree
}

// A wrapper over isSameBSTUtil()
bool isSameBST(int a[], int b[], int n)
{
   return isSameBSTUtil(a, b, n, 0, 0, INT_MIN, INT_MAX);
}

// Driver program to test above functions
int main()
{
   int a[] = {8, 3, 6, 1, 4, 7, 10, 14, 13};
   int b[] = {8, 10, 14, 3, 6, 4, 1, 7, 13};
   int n=sizeof(a)/sizeof(a[0]);
   printf("%s\n", isSameBST(a, b, n)?
             "BSTs are same":"BSTs not same");
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to check for Identical
// BSTs without building the trees
class GFG
{

/* The main function that checks
if two arrays a[] and b[] of size
n construct same BST. The two values
'min' and 'max' decide whether the
call is made for left subtree or
right subtree of a parent element.
The indexes i1 and i2 are the indexes
in (a[] and b[]) after which we search
the left or right child. Initially, the
call is made for INT_MIN and INT_MAX as
'min' and 'max' respectively, because
root has no parent. i1 and i2 are just
after the indexes of the parent element in a[] and b[]. */
static boolean isSameBSTUtil(int a[], int b[], int n,
                        int i1, int i2, int min, int max)
{
    int j, k;

    /* Search for a value satisfying the
    constraints of min and max in a[] and
    b[]. If the parent element is a leaf
    node then there must be some elements
    in a[] and b[] satisfying constraint. */
    for (j = i1; j < n; j++)
    if (a[j] > min && a[j] < max)
        break;
    for (k = i2; k < n; k++)
        if (b[k] > min && b[k] < max)
            break;

    /* If the parent element is
    leaf in both arrays */
    if (j == n && k == n)
        return true;

    /* Return false if any of the following is true
    a) If the parent element is leaf in
    one array, but non-leaf in other.
    b) The elements satisfying constraints
    are not same. We either search for left
    child or right child of the parent element
    (decinded by min and max values). The child
    found must be same in both arrays */
    if (((j==n)^(k==n)) || a[j]!=b[k])
        return false;

    /* Make the current child as parent and
    recursively check for left and right
    subtrees of it. Note that we can also
    pass a[k] in place of a[j] as they
    are both are same */
    return isSameBSTUtil(a, b, n, j+1, k+1, a[j], max) && // Right Subtree
            isSameBSTUtil(a, b, n, j+1, k+1, min, a[j]); // Left Subtree
}

// A wrapper over isSameBSTUtil()
static boolean isSameBST(int a[], int b[], int n)
{
    return isSameBSTUtil(a, b, n, 0, 0,
                    Integer.MIN_VALUE,Integer.MAX_VALUE);
}

// Driver code
public static void main(String[] args)
{
    int a[] = {8, 3, 6, 1, 4, 7, 10, 14, 13};
    int b[] = {8, 10, 14, 3, 6, 4, 1, 7, 13};
    int n=a.length;
    System.out.printf("%s\n", isSameBST(a, b, n)?
                "BSTs are same":"BSTs not same");
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# A Python3 program to check for Identical
# BSTs without building the trees

# # The main function that checks if two
# arrays a[] and b[] of size n construct
# same BST. The two values 'min' and 'max'
# decide whether the call is made for left
# subtree or right subtree of a parent
# element. The indexes i1 and i2 are the
# indexes in (a[] and b[]) after which we
# search the left or right child. Initially,
# the call is made for INT_MIN and INT_MAX
# as 'min' and 'max' respectively, because
# root has no parent. i1 and i2 are just
# after the indexes of the parent element in a[] and b[]. */
def isSameBSTUtil(a, b, n, i1, i2, min, max):

    # # Search for a value satisfying the
    # constraints of min and max in a[] and
    # b[]. If the parent element is a leaf
    # node then there must be some elements
    # in a[] and b[] satisfying constraint. */
    j, k = i1, i2
    while j < n:
        if (a[j] > min and a[j] < max):
            break;
        j += 1
    while k<n:
        if (b[k] > min and b[k] < max):
            break
        k += 1

    # If the parent element is leaf in both arrays */
    if (j == n and k == n):
        return True

    # Return false if any of the following is true
        # a) If the parent element is leaf in one array,
        #     but non-leaf in other.
        # b) The elements satisfying constraints are
        #     not same. We either search for left
        #     child or right child of the parent
        #     element (decinded by min and max values).
        #     The child found must be same in both arrays */
    if (((j == n) ^ (k == n)) or a[j] != b[k]):
        return False

    # Make the current child as parent and
    # recursively check for left and right
    # subtrees of it. Note that we can also
    # pass a[k] in place of a[j] as they
    # are both are same */
    return isSameBSTUtil(a, b, n, j + 1, k + 1, a[j], max) and isSameBSTUtil(a, b, n, j + 1, k + 1, min, a[j]) #Left Subtree

# A wrapper over isSameBSTUtil()
def isSameBST(a, b, n):
    return isSameBSTUtil(a, b, n, 0, 0, -10**9, 10**9)

# Driver code
if __name__ == '__main__':
    a = [8, 3, 6, 1, 4, 7, 10, 14, 13]
    b = [8, 10, 14, 3, 6, 4, 1, 7, 13]
    n = len(a)

    if(isSameBST(a, b, n)):
        print("BSTs are same")
    else:
        print("BSTs not same")

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program to check for Identical
// BSTs without building the trees
using System;

class GFG
{

/* The main function that checks
if two arrays a[] and b[] of size
n construct same BST. The two values
'min' and 'max' decide whether the
call is made for left subtree or
right subtree of a parent element.
The indexes i1 and i2 are the indexes
in (a[] and b[]) after which we search
the left or right child. Initially, the
call is made for INT_MIN and INT_MAX as
'min' and 'max' respectively, because
root has no parent. i1 and i2 are just
after the indexes of the parent element in a[] and b[]. */
static bool isSameBSTUtil(int []a, int []b, int n,
                        int i1, int i2, int min, int max)
{
    int j, k;

    /* Search for a value satisfying the
    constraints of min and max in a[] and
    b[]. If the parent element is a leaf
    node then there must be some elements
    in a[] and b[] satisfying constraint. */
    for (j = i1; j < n; j++)
    if (a[j] > min && a[j] < max)
        break;
    for (k = i2; k < n; k++)
        if (b[k] > min && b[k] < max)
            break;

    /* If the parent element is
    leaf in both arrays */
    if (j == n && k == n)
        return true;

    /* Return false if any of the following is true
    a) If the parent element is leaf in
    one array, but non-leaf in other.
    b) The elements satisfying constraints
    are not same. We either search for left
    child or right child of the parent element
    (decinded by min and max values). The child
    found must be same in both arrays */
    if (((j == n)^(k == n)) || a[j] != b[k])
        return false;

    /* Make the current child as parent and
    recursively check for left and right
    subtrees of it. Note that we can also
    pass a[k] in place of a[j] as they
    are both are same */
    return isSameBSTUtil(a, b, n, j + 1, k + 1, a[j], max) && // Right Subtree
            isSameBSTUtil(a, b, n, j + 1, k + 1, min, a[j]); // Left Subtree
}

// A wrapper over isSameBSTUtil()
static bool isSameBST(int []a, int []b, int n)
{
    return isSameBSTUtil(a, b, n, 0, 0,
                    int.MinValue,int.MaxValue);
}

// Driver code
public static void Main(String[] args)
{
    int []a = {8, 3, 6, 1, 4, 7, 10, 14, 13};
    int []b = {8, 10, 14, 3, 6, 4, 1, 7, 13};
    int n=a.Length;
    Console.WriteLine("{0}\n", isSameBST(a, b, n)?
                "BSTs are same":"BSTs not same");
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// A Javascript program to check for Identical
// BSTs without building the trees

    /* The main function that checks
if two arrays a[] and b[] of size
n construct same BST. The two values
'min' and 'max' decide whether the
call is made for left subtree or
right subtree of a parent element.
The indexes i1 and i2 are the indexes
in (a[] and b[]) after which we search
the left or right child. Initially, the
call is made for INT_MIN and INT_MAX as
'min' and 'max' respectively, because
root has no parent. i1 and i2 are just
after the indexes of the parent element in a[] and b[]. */
    function isSameBSTUtil(a,b,n,i1,i2,min,max)
    {
        let j, k;

    /* Search for a value satisfying the
    constraints of min and max in a[] and
    b[]. If the parent element is a leaf
    node then there must be some elements
    in a[] and b[] satisfying constraint. */
    for (j = i1; j < n; j++)
    if (a[j] > min && a[j] < max)
        break;
    for (k = i2; k < n; k++)
        if (b[k] > min && b[k] < max)
            break;

    /* If the parent element is
    leaf in both arrays */
    if (j == n && k == n)
        return true;

    /* Return false if any of the following is true
    a) If the parent element is leaf in
    one array, but non-leaf in other.
    b) The elements satisfying constraints
    are not same. We either search for left
    child or right child of the parent element
    (decinded by min and max values). The child
    found must be same in both arrays */
    if (((j==n)^(k==n)) || a[j]!=b[k])
        return false;

    /* Make the current child as parent and
    recursively check for left and right
    subtrees of it. Note that we can also
    pass a[k] in place of a[j] as they
    are both are same */
    return isSameBSTUtil(a, b, n, j+1, k+1, a[j], max) && // Right Subtree
            isSameBSTUtil(a, b, n, j+1, k+1, min, a[j]); // Left Subtree
    }

    // A wrapper over isSameBSTUtil()
    function isSameBST(a,b,n)
    {
        return isSameBSTUtil(a, b, n, 0, 0,
                    Number.MIN_VALUE,Number.MAX_VALUE);
    }

    // Driver code
    let a=[8, 3, 6, 1, 4, 7, 10, 14, 13];
    let b=[8, 10, 14, 3, 6, 4, 1, 7, 13];
    let n=a.length;
    document.write( isSameBST(a, b, n)?
                "BSTs are same":"BSTs not same");

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
BSTs are same
```

本文由 [**阿米特·贾恩**](http://in.linkedin.com/in/amitjainju/) 整理。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息
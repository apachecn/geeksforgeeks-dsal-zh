# 计数数组中的反转|集合 4(使用 Trie )

> 原文:[https://www . geesforgeks . org/count-inversion-in-a-a-set-4-using-trie/](https://www.geeksforgeeks.org/count-inversions-in-an-array-set-4-using-trie/)

数组的反转计数表示数组离排序有多远(或多近)。如果数组已经排序，则反转计数为 0。如果数组按相反的顺序排序，则反转计数为最大值。

> 两个元素 a[i]和 a[j]形成一个**反转**如果 a[i] > a[j]和 i < j.
> 为了简单起见，我们可以假设所有元素都是唯一的。

所以，我们的任务是计算数组中的逆序数。这是一对元素(a[i]，a[j])的数量，使得:

*   a[i] > a[j],
*   i < j。

**例** :

```
Input: arr[] = {8, 4, 2, 1}
Output: 6
Given array has six inversions (8, 4), (4, 2),
(8, 2), (8, 1), (4, 1), (2, 1). 

Input: arr[] = { 1, 20, 6, 4, 5 }    
Output: 5
```

1.  [初始和修改合并排序](https://www.geeksforgeeks.org/counting-inversions/)
2.  [使用 AVL 树](https://www.geeksforgeeks.org/count-inversions-in-an-array-set-2-using-self-balancing-bst/)
3.  [使用 BIT](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit/)

**方法:**
我们将在数组中向后迭代，并将每个元素存储到 Trie 中。要在 Trie 中存储一个数字，我们
必须将该数字分解为二进制形式，如果该位是 **0** ，则表示我们将该位存储到当前节点的左指针中，如果是 **1** ，则存储到当前节点的右指针中，并相应地改变当前节点。我们还将维护计数，它表示有多少个数字沿着相同的路径直到那个节点。
**特里节点的结构**

```
struct node{
  int count; 
  node* left;
  node* right;
};
```

在任何时候，当我们存储位时，我们碰巧移动到右边的指针(即位为 1)，我们将检查左边的子级是否存在，这意味着有比当前数字小的数字已经存储到 Trie 中，这些数字只是反转计数，因此我们将把它们添加到计数中。
以下是实施办法

## C++

```
// C++ implementation
#include <iostream>
using namespace std;

// Structure of the node
struct Node {
    int count;
    Node* left;
    Node* right;
};

// function to initialize
// new node
Node* makeNewNode()
{
    Node* temp = new Node;
    temp->count = 1;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// Insert element in trie
void insertElement(int num,
                   Node* root,
                   int& ans)
{
    // Converting the number
    // into binary form
    for (int i = 63; i >= 0; i--) {
        // Checking if the i-th
        // bit ios set or not
        int a = (num & (1 << i));

        // If the bit is 1
        if (a != 0) {
            // if the bit is 1 that means
            // we have to go to the right
            // but we also checks if left
            // pointer  exists i.e there is
            // at least a number smaller than
            // the current number already in
            // the trie we add that count
            // to ans
            if (root->left != NULL)
                ans += root->left->count;

            // If right pointer is not NULL
            // we just iterate to that
            // position and increment the count
            if (root->right != NULL) {
                root = root->right;
                root->count += 1;
            }

            // If right is NULL we add a new
            // node over there and initialize
            // the count with 1
            else {
                Node* temp = makeNewNode();
                root->right = temp;
                root = root->right;
            }
        }

        // if the bit is 0
        else {
            // We have to iterate to left,
            // we first check if left
            // exists? if yes then change
            // the root and the count
            if (root->left != NULL) {
                root = root->left;
                root->count++;
            }

            // otherwise we create
            // the left node
            else {
                Node* temp = makeNewNode();
                root->left = temp;
                root = root->left;
            }
        }
    }
}

// function to count
// the inversions
int getInvCount(int arr[], int n)
{
    Node* head = makeNewNode();
    int ans = 0;
    for (int i = n - 1; i >= 0; i--) {
        // inserting each element in Trie
        insertElement(arr[i],
                      head,
                      ans);
    }

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 8, 4, 2, 1 };
    int n = sizeof(arr) / sizeof(int);

    cout << "Number of inversions are : "
         << getInvCount(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above idea
import java.util.*;

class GFG
{

// Structure of the node
static class Node
{
    int count;
    Node left;
    Node right;
};
static int ans;

// function to initialize
// new node
static Node makeNewNode()
{
    Node temp = new Node();
    temp.count = 1;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Insert element in trie
static void insertElement(int num,
                Node root)
{
    // Converting the number
    // into binary form
    for (int i = 63; i >= 0; i--)
    {
        // Checking if the i-th
        // bit ios set or not
        int a = (num & (1 << i));

        // If the bit is 1
        if (a != 0)
        {
            // if the bit is 1 that means
            // we have to go to the right
            // but we also checks if left
            // pointer exists i.e there is
            // at least a number smaller than
            // the current number already in
            // the trie we add that count
            // to ans
            if (root.left != null)
                ans += root.left.count;

            // If right pointer is not null
            // we just iterate to that
            // position and increment the count
            if (root.right != null)
            {
                root = root.right;
                root.count += 1;
            }

            // If right is null we add a new
            // node over there and initialize
            // the count with 1
            else
            {
                Node temp = makeNewNode();
                root.right = temp;
                root = root.right;
            }
        }

        // if the bit is 0
        else
        {
            // We have to iterate to left,
            // we first check if left
            // exists? if yes then change
            // the root and the count
            if (root.left != null)
            {
                root = root.left;
                root.count++;
            }

            // otherwise we create
            // the left node
            else
            {
                Node temp = makeNewNode();
                root.left = temp;
                root = root.left;
            }
        }
    }
}

// function to count
// the inversions
static int getInvCount(int arr[], int n)
{
    Node head = makeNewNode();
    ans = 0;
    for (int i = n - 1; i >= 0; i--)
    {
        // inserting each element in Trie
        insertElement(arr[i],
                    head);
    }

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 8, 4, 2, 1 };
    int n = arr.length;

    System.out.print("Number of inversions are : "
        + getInvCount(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation

# Structure of the node
class Node:

    def __init__(self):

        self.left = self.right = None
        self.count = 1

# function to initialize
# new node
def makeNewNode():

    temp = Node()
    return temp

# Insert element in trie
def insertElement(num, root, ans):

    # Converting the number
    # into binary form
    for i in range(63, -1, -1):

        # Checking if the i-th
        # bit ios set or not
        a = (num & (1 << i));

        # If the bit is 1
        if (a != 0):

            # if the bit is 1 that means
            # we have to go to the right
            # but we also checks if left
            # pointer  exists i.e there is
            # at least a number smaller than
            # the current number already in
            # the trie we add that count
            # to ans
            if (root.left != None):
                ans += root.left.count;

            # If right pointer is not None
            # we just iterate to that
            # position and increment the count
            if (root.right != None):
                root = root.right;
                root.count += 1;

            # If right is None we add a new
            # node over there and initialize
            # the count with 1
            else:
                temp = makeNewNode();
                root.right = temp;
                root = root.right;

        # if the bit is 0
        else:

            # We have to iterate to left,
            # we first check if left
            # exists? if yes then change
            # the root and the count
            if (root.left != None):
                root = root.left;
                root.count += 1

            # otherwise we create
            # the left node
            else:
                temp = makeNewNode();
                root.left = temp;
                root = root.left;
    return ans

# function to count
# the inversions
def getInvCount(arr, n):

    head = makeNewNode();
    ans = 0;

    for i in range(n - 1 ,-1, -1):

        # inserting each element in Trie
        ans = insertElement(arr[i], head, ans);

    return ans;

# Driver Code
if __name__=='__main__':

    arr = [ 8, 4, 2, 1 ]

    n = len(arr)

    print("Number of inversions are : " + str(getInvCount(arr, n)))

    # This code is contributed by rutvik_56
```

## C#

```
// C# implementation of above idea
using System;

class GFG
{

// Structure of the node
public class Node
{
    public int count;
    public Node left;
    public Node right;
};
static int ans;

// function to initialize
// new node
static Node makeNewNode()
{
    Node temp = new Node();
    temp.count = 1;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Insert element in trie
static void insertElement(int num,
                         Node root)
{
    // Converting the number
    // into binary form
    for (int i = 63; i >= 0; i--)
    {
        // Checking if the i-th
        // bit ios set or not
        int a = (num & (1 << i));

        // If the bit is 1
        if (a != 0)
        {
            // if the bit is 1 that means
            // we have to go to the right
            // but we also checks if left
            // pointer exists i.e there is
            // at least a number smaller than
            // the current number already in
            // the trie we add that count
            // to ans
            if (root.left != null)
                ans += root.left.count;

            // If right pointer is not null
            // we just iterate to that
            // position and increment the count
            if (root.right != null)
            {
                root = root.right;
                root.count += 1;
            }

            // If right is null we add a new
            // node over there and initialize
            // the count with 1
            else
            {
                Node temp = makeNewNode();
                root.right = temp;
                root = root.right;
            }
        }

        // if the bit is 0
        else
        {
            // We have to iterate to left,
            // we first check if left
            // exists? if yes then change
            // the root and the count
            if (root.left != null)
            {
                root = root.left;
                root.count++;
            }

            // otherwise we create
            // the left node
            else
            {
                Node temp = makeNewNode();
                root.left = temp;
                root = root.left;
            }
        }
    }
}

// function to count the inversions
static int getInvCount(int []arr, int n)
{
    Node head = makeNewNode();
    ans = 0;
    for (int i = n - 1; i >= 0; i--)
    {
        // inserting each element in Trie
        insertElement(arr[i], head);
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 8, 4, 2, 1 };
    int n = arr.Length;

    Console.Write("Number of inversions are : " +
                            getInvCount(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of above idea

// Structure of the node
class Node
{
    constructor()
    {
        this.count = 0;
        this.left = null;
        this.right = null;
    }
};

var ans = 0;

// function to initialize
// new node
function makeNewNode()
{
    var temp = new Node();
    temp.count = 1;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Insert element in trie
function insertElement(num, root)
{
    // Converting the number
    // into binary form
    for (var i = 63; i >= 0; i--)
    {
        // Checking if the i-th
        // bit ios set or not
        var a = (num & (1 << i));

        // If the bit is 1
        if (a != 0)
        {
            // if the bit is 1 that means
            // we have to go to the right
            // but we also checks if left
            // pointer exists i.e there is
            // at least a number smaller than
            // the current number already in
            // the trie we add that count
            // to ans
            if (root.left != null)
                ans += root.left.count;

            // If right pointer is not null
            // we just iterate to that
            // position and increment the count
            if (root.right != null)
            {
                root = root.right;
                root.count += 1;
            }

            // If right is null we add a new
            // node over there and initialize
            // the count with 1
            else
            {
                var temp = makeNewNode();
                root.right = temp;
                root = root.right;
            }
        }

        // if the bit is 0
        else
        {
            // We have to iterate to left,
            // we first check if left
            // exists? if yes then change
            // the root and the count
            if (root.left != null)
            {
                root = root.left;
                root.count++;
            }

            // otherwise we create
            // the left node
            else
            {
                var temp = makeNewNode();
                root.left = temp;
                root = root.left;
            }
        }
    }
}

// function to count the inversions
function getInvCount(arr, n)
{
    var head = makeNewNode();
    ans = 0;
    for (var i = n - 1; i >= 0; i--)
    {
        // inserting each element in Trie
        insertElement(arr[i], head);
    }
    return ans;
}

// Driver Code
var arr = [8, 4, 2, 1];
var n = arr.length;
document.write("Number of inversions are : " +
                        getInvCount(arr, n));

</script>
```

**Output:** 

```
Number of inversions are : 6
```

**时间复杂度:** ![O(Nlog(N))      ](img/669a345d3cdc8096fb110fbf866c4565.png "Rendered by QuickLaTeX.com")
**辅助空间** : ![O(Nlog(N))      ](img/669a345d3cdc8096fb110fbf866c4565.png "Rendered by QuickLaTeX.com")
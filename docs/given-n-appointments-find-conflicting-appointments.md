# 给定 n 个约会，找出所有冲突的约会

> 原文:[https://www . geesforgeks . org/given-n-约会-查找-冲突-约会/](https://www.geeksforgeeks.org/given-n-appointments-find-conflicting-appointments/)

给定 n 个约会，找出所有冲突的约会。

示例:

```
Input: appointments[] = { {1, 5} {3, 7}, {2, 6}, {10, 15}, {5, 6}, {4, 100}}
Output: Following are conflicting intervals
[3,7] Conflicts with [1,5]
[2,6] Conflicts with [1,5]
[5,6] Conflicts with [3,7]
[4,100] Conflicts with [1,5]
```

如果约会与阵列中任何以前的约会冲突，则该约会是冲突的。

**强烈建议尽量减少浏览器，先自己试试这个。**

一个**简单的解决方法**就是从第二次约会到最后一次约会逐一处理所有约会。对于每个约会 I，检查它是否与 i-1、i-2、… 0 冲突。该方法的时间复杂度为 O(n <sup>2</sup> )。
我们可以用 [**区间树**](https://www.geeksforgeeks.org/interval-tree/) 在 O(nLogn)时间内解决这个问题。下面是详细的算法。

```
1) Create an Interval Tree, initially with the first appointment.
2) Do following for all other appointments starting from the second one.
   a) Check if the current appointment conflicts with any of the existing 
     appointments in Interval Tree.  If conflicts, then print the current
     appointment.  This step can be done O(Logn) time.
   b) Insert the current appointment in Interval Tree. This step also can
      be done O(Logn) time.
```

以下是上述想法的实现。

## C++

```
// C++ program to print all conflicting appointments in a
// given set of appointments
#include <bits/stdc++.h>
using namespace std;

// Structure to represent an interval
struct Interval
{
    int low, high;
};

// Structure to represent a node in Interval Search Tree
struct ITNode
{
    Interval *i;  // 'i' could also be a normal variable
    int max;
    ITNode *left, *right;
};

// A utility function to create a new Interval Search Tree Node
ITNode * newNode(Interval i)
{
    ITNode *temp = new ITNode;
    temp->i = new Interval(i);
    temp->max = i.high;
    temp->left = temp->right = NULL;
      return temp;
};

// A utility function to insert a new Interval Search Tree
// Node. This is similar to BST Insert.  Here the low value
//  of interval is used tomaintain BST property
ITNode *insert(ITNode *root, Interval i)
{
    // Base case: Tree is empty, new node becomes root
    if (root == NULL)
        return newNode(i);

    // Get low value of interval at root
    int l = root->i->low;

    // If root's low value is smaller, then new interval
    //  goes to left subtree
    if (i.low < l)
        root->left = insert(root->left, i);

    // Else, new node goes to right subtree.
    else
        root->right = insert(root->right, i);

    // Update the max value of this ancestor if needed
    if (root->max < i.high)
        root->max = i.high;

    return root;
}

// A utility function to check if given two intervals overlap
bool doOVerlap(Interval i1, Interval i2)
{
    if (i1.low < i2.high && i2.low < i1.high)
        return true;
    return false;
}

// The main function that searches a given interval i
// in a given Interval Tree.
Interval *overlapSearch(ITNode *root, Interval i)
{
    // Base Case, tree is empty
    if (root == NULL) return NULL;

    // If given interval overlaps with root
    if (doOVerlap(*(root->i), i))
        return root->i;

    // If left child of root is present and max of left child
    // is greater than or equal to given interval, then i may
    // overlap with an interval is left subtree
    if (root->left != NULL && root->left->max >= i.low)
        return overlapSearch(root->left, i);

    // Else interval can only overlap with right subtree
    return overlapSearch(root->right, i);
}

// This function prints all conflicting appointments in a given
// array of appointments.
void printConflicting(Interval appt[], int n)
{
     // Create an empty Interval Search Tree, add first
     // appointment
     ITNode *root = NULL;
     root = insert(root, appt[0]);

     // Process rest of the intervals
     for (int i=1; i<n; i++)
     {
         // If current appointment conflicts with any of the
         // existing intervals, print it
         Interval *res = overlapSearch(root, appt[i]);
         if (res != NULL)
            cout << "[" << appt[i].low << "," << appt[i].high
                 << "] Conflicts with [" << res->low << ","
                 << res->high << "]\n";

         // Insert this appointment
         root = insert(root, appt[i]);
     }
}

// Driver program to test above functions
int main()
{
    // Let us create interval tree shown in above figure
    Interval appt[] = { {1, 5}, {3, 7}, {2, 6}, {10, 15},
                        {5, 6}, {4, 100}};
    int n = sizeof(appt)/sizeof(appt[0]);
    cout << "Following are conflicting intervals\n";
    printConflicting(appt, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all conflicting
// appointments in a given set of appointments
class GfG{

// Structure to represent an interval
static class Interval
{
    int low, high;
}

static class ITNode
{

    // 'i' could also be a normal variable
    Interval i;
    int max;
    ITNode left, right;
}

// A utility function to create a new node
static Interval newNode(int l, int h)
{
    Interval temp = new Interval();
    temp.low = l;
    temp.high = h;
    return temp;
}

// A utility function to create a new node
static ITNode newNode(Interval i)
{
    ITNode temp = new ITNode();
    temp.i = i;
    temp.max = i.high;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert a new
// Interval Search Tree Node. This is
// similar to BST Insert. Here the
// low value of interval is used to
// maintain BST property
static ITNode insert(ITNode root, Interval i)
{

    // Base case: Tree is empty,
    // new node becomes root
    if (root == null)
        return newNode(i);

    // Get low value of interval at root
    int l = root.i.low;

    // If root's low value is smaller,
    // then new interval goes to left subtree
    if (i.low < l)
        root.left = insert(root.left, i);

    // Else, new node goes to right subtree.
    else
        root.right = insert(root.right, i);

    // Update the max value of this
    // ancestor if needed
    if (root.max < i.high)
        root.max = i.high;

    return root;
}

// A utility function to check if given
// two intervals overlap
static boolean doOVerlap(Interval i1, Interval i2)
{
    if (i1.low < i2.high && i2.low < i1.high)
        return true;

    return false;
}

// The main function that searches a given
// interval i in a given Interval Tree.
static Interval overlapSearch(ITNode root,
                              Interval i)
{

    // Base Case, tree is empty
    if (root == null)
        return null;

    // If given interval overlaps with root
    if (doOVerlap(root.i, i))
        return root.i;

    // If left child of root is present
    // and max of left child is greater
    // than or equal to given interval,
    // then i may overlap with an interval
    // is left subtree
    if (root.left != null &&
        root.left.max >= i.low)
        return overlapSearch(root.left, i);

    // Else interval can only
    // overlap with right subtree
    return overlapSearch(root.right, i);
}

// This function prints all conflicting
// appointments in a given array of appointments.
static void printConflicting(Interval appt[], int n)
{

    // Create an empty Interval Search
    // Tree, add first appointment
    ITNode root = null;
    root = insert(root, appt[0]);

    // Process rest of the intervals
    for(int i = 1; i < n; i++)
    {

        // If current appointment conflicts
        // with any of the existing intervals,
        // print it
        Interval res = overlapSearch(root, appt[i]);

        if (res != null)
            System.out.print("[" + appt[i].low +
                             "," + appt[i].high +
                             "] Conflicts with [" +
                             res.low + "," +
                             res.high + "]\n");

        // Insert this appointment
        root = insert(root, appt[i]);
    }
}

// Driver code
public static void main(String[] args)
{
    Interval appt[] = new Interval[6];
    appt[0] = newNode(1, 5);
    appt[1] = newNode(3, 7);
    appt[2] = newNode(2, 6);
    appt[3] = newNode(10, 15);
    appt[4] = newNode(5, 6);
    appt[5] = newNode(4, 100);

    int n = appt.length;
    System.out.print(
        "Following are conflicting intervals\n");

    printConflicting(appt, n);
}
}

// This code is contributed by tushar_bansal
```

## 蟒蛇 3

```
# Python3 program to print all conflicting
# appointments in a given set of appointments

# Structure to represent an interval
class Interval:

    def __init__(self):

        self.low = None
        self.high = None

# Structure to represent a node
# in Interval Search Tree
class ITNode:

    def __init__(self):

        self.max = None
        self.i = None
        self.left = None
        self.right = None

def newNode(j):

    #print(j)
    temp = ITNode()
    temp.i = j
    temp.max = j[1]

    return temp

# A utility function to check if
# given two intervals overlap
def doOVerlap(i1, i2):

    if (i1[0] < i2[1] and i2[0] < i1[1]):
        return True

    return False

# Function to create a new node
def insert(node, data):

    global succ

    # If the tree is empty, return a new node
    root = node

    if (node == None):
        return newNode(data)

    # If key is smaller than root's key, go to left
    # subtree and set successor as current node
    # print(node)
    if (data[0] < node.i[0]):

        # print(node)
        root.left = insert(node.left, data)

    # Go to right subtree
    else:
        root.right = insert(node.right, data)
    if root.max < data[1]:
        root.max = data[1]

    return root

# The main function that searches a given
# interval i in a given Interval Tree.
def overlapSearch(root, i):

    # Base Case, tree is empty
    if (root == None):
        return None

    # If given interval overlaps with root
    if (doOVerlap(root.i, i)):
        return root.i

    # If left child of root is present and
    # max of left child is greater than or
    # equal to given interval, then i may
    # overlap with an interval is left subtree
    if (root.left != None and root.left.max >= i[0]):
        return overlapSearch(root.left, i)

    # Else interval can only overlap
    # with right subtree
    return overlapSearch(root.right, i)

# This function prints all conflicting
# appointments in a given array of
# appointments.
def printConflicting(appt, n):

    # Create an empty Interval Search Tree,
    # add first appointment
    root = None
    root = insert(root, appt[0])

    # Process rest of the intervals
    for i in range(1, n):

        # If current appointment conflicts
        # with any of the existing intervals,
        # print it
        res = overlapSearch(root, appt[i])

        if (res != None):
            print("[", appt[i][0], ",", appt[i][1],
                  "] Conflicts with [", res[0],
                  ",", res[1], "]")

        # Insert this appointment
        root = insert(root, appt[i])

# Driver code
if __name__ == '__main__':

    # Let us create interval tree
    # shown in above figure
    appt = [ [ 1, 5 ], [ 3, 7 ],
             [ 2, 6 ], [ 10, 15 ],
             [ 5, 6 ], [ 4, 100 ] ]

    n = len(appt)

    print("Following are conflicting intervals")

    printConflicting(appt, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print all conflicting
// appointments in a given set of appointments
using System;
public class GfG
{

// Structure to represent an interval
public
class Interval
{
    public
int low, high;
}
public
class ITNode
{

    // 'i' could also be a normal variable
   public
  Interval i;
    public
 int max;
    public
ITNode left, right;
}

// A utility function to create a new node
static Interval newNode(int l, int h)
{
    Interval temp = new Interval();
    temp.low = l;
    temp.high = h;
    return temp;
}

// A utility function to create a new node
static ITNode newNode(Interval i)
{
    ITNode temp = new ITNode();
    temp.i = i;
    temp.max = i.high;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert a new
// Interval Search Tree Node. This is
// similar to BST Insert. Here the
// low value of interval is used to
// maintain BST property
static ITNode insert(ITNode root, Interval i)
{

    // Base case: Tree is empty,
    // new node becomes root
    if (root == null)
        return newNode(i);

    // Get low value of interval at root
    int l = root.i.low;

    // If root's low value is smaller,
    // then new interval goes to left subtree
    if (i.low < l)
        root.left = insert(root.left, i);

    // Else, new node goes to right subtree.
    else
        root.right = insert(root.right, i);

    // Update the max value of this
    // ancestor if needed
    if (root.max < i.high)
        root.max = i.high;
    return root;
}

// A utility function to check if given
// two intervals overlap
static bool doOVerlap(Interval i1, Interval i2)
{
    if (i1.low < i2.high && i2.low < i1.high)
        return true;     
    return false;
}

// The main function that searches a given
// interval i in a given Interval Tree.
static Interval overlapSearch(ITNode root,
                              Interval i)
{

    // Base Case, tree is empty
    if (root == null)
        return null;

    // If given interval overlaps with root
    if (doOVerlap(root.i, i))
        return root.i;

    // If left child of root is present
    // and max of left child is greater
    // than or equal to given interval,
    // then i may overlap with an interval
    // is left subtree
    if (root.left != null &&
        root.left.max >= i.low)
        return overlapSearch(root.left, i);

    // Else interval can only
    // overlap with right subtree
    return overlapSearch(root.right, i);
}

// This function prints all conflicting
// appointments in a given array of appointments.
static void printConflicting(Interval []appt, int n)
{

    // Create an empty Interval Search
    // Tree, add first appointment
    ITNode root = null;
    root = insert(root, appt[0]);

    // Process rest of the intervals
    for(int i = 1; i < n; i++)
    {

        // If current appointment conflicts
        // with any of the existing intervals,
        // print it
        Interval res = overlapSearch(root, appt[i]);

        if (res != null)
            Console.Write("[" + appt[i].low +
                             "," + appt[i].high +
                             "] Conflicts with [" +
                             res.low + "," +
                             res.high + "]\n");

        // Insert this appointment
        root = insert(root, appt[i]);
    }
}

// Driver code
public static void Main(String[] args)
{
    Interval []appt = new Interval[6];
    appt[0] = newNode(1, 5);
    appt[1] = newNode(3, 7);
    appt[2] = newNode(2, 6);
    appt[3] = newNode(10, 15);
    appt[4] = newNode(5, 6);
    appt[5] = newNode(4, 100);  
    int n = appt.Length;
    Console.Write(
        "Following are conflicting intervals\n");
    printConflicting(appt, n);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to print all conflicting
// appointments in a given set of appointments

// Structure to represent an interval
class Interval
{
    constructor()
    {
        this.low = 0;
        this.high = 0;
    }
}

class ITNode
{
    // 'i' could also be a normal variable
    constructor()
    {
        this.max = 0;
        this.left = null;
        this.right = null;
        this.i = null;
    }
}

// A utility function to create a new node
function newNodeDouble(l, h)
{
    var temp = new Interval();
    temp.low = l;
    temp.high = h;
    return temp;
}

// A utility function to create a new node
function newNodeSingle(i)
{
    var temp = new ITNode();
    temp.i = i;
    temp.max = i.high;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert a new
// Interval Search Tree Node. This is
// similar to BST Insert. Here the
// low value of interval is used to
// maintain BST property
function insert(root, i)
{

    // Base case: Tree is empty,
    // new node becomes root
    if (root == null)
        return newNodeSingle(i);

    // Get low value of interval at root
    var l = root.i.low;

    // If root's low value is smaller,
    // then new interval goes to left subtree
    if (i.low < l)
        root.left = insert(root.left, i);

    // Else, new node goes to right subtree.
    else
        root.right = insert(root.right, i);

    // Update the max value of this
    // ancestor if needed
    if (root.max < i.high)
        root.max = i.high;
    return root;
}

// A utility function to check if given
// two intervals overlap
function doOVerlap(i1, i2)
{
    if (i1.low < i2.high && i2.low < i1.high)
        return true;     
    return false;
}

// The main function that searches a given
// interval i in a given Interval Tree.
function overlapSearch(root, i)
{

    // Base Case, tree is empty
    if (root == null)
        return null;

    // If given interval overlaps with root
    if (doOVerlap(root.i, i))
        return root.i;

    // If left child of root is present
    // and max of left child is greater
    // than or equal to given interval,
    // then i may overlap with an interval
    // is left subtree
    if (root.left != null &&
        root.left.max >= i.low)
        return overlapSearch(root.left, i);

    // Else interval can only
    // overlap with right subtree
    return overlapSearch(root.right, i);
}

// This function prints all conflicting
// appointments in a given array of appointments.
function printConflicting(appt, n)
{

    // Create an empty Interval Search
    // Tree, add first appointment
    var root = null;
    root = insert(root, appt[0]);

    // Process rest of the intervals
    for(var i = 1; i < n; i++)
    {

        // If current appointment conflicts
        // with any of the existing intervals,
        // print it
        var res = overlapSearch(root, appt[i]);

        if (res != null)
            document.write("[" + appt[i].low +
                             "," + appt[i].high +
                             "] Conflicts with [" +
                             res.low + "," +
                             res.high + "]<br>");

        // Insert this appointment
        root = insert(root, appt[i]);
    }
}

// Driver code
var appt = Array(6);
appt[0] = newNodeDouble(1, 5);
appt[1] = newNodeDouble(3, 7);
appt[2] = newNodeDouble(2, 6);
appt[3] = newNodeDouble(10, 15);
appt[4] = newNodeDouble(5, 6);
appt[5] = newNodeDouble(4, 100);  
var n = appt.length;
document.write(
    "Following are conflicting intervals<br>");
printConflicting(appt, n);

</script>
```

**输出:**

```
Following are conflicting intervals
[3,7] Conflicts with [1,5]
[2,6] Conflicts with [1,5]
[5,6] Conflicts with [3,7]
[4,100] Conflicts with [1,5]
```

注意，上面的实现使用了简单的二叉查找树插入操作。因此，上述实现的时间复杂度大于 O(nLogn)。我们可以使用[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)或者 [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)的平衡技巧来做上面的实现 O(nLogn)。

本文由**安摩尔**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息
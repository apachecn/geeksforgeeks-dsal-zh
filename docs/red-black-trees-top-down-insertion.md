# 红黑树|自上而下插入

> 原文:[https://www . geesforgeks . org/red-black-trees-top-down-insert/](https://www.geeksforgeeks.org/red-black-trees-top-down-insertion/)

在[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)的自下而上插入中，使用了“简单”的二叉查找树插入，随后在返回根的过程中纠正了 RB 树违规。借助递归可以很容易地做到这一点。在自上而下插入中，校正是在沿树向下遍历到插入点时完成的。当实际插入完成时，不需要进一步的校正，因此不需要遍历树。
因此，自顶向下插入的目标是以保持 RB 属性的方式从根遍历到插入点。因此，这种迭代方法使得自顶向下插入比自底向上插入更快。

修复违规和平衡需要执行的两个基本操作是-

*   重新着色
*   旋转

**下面是详细的算法**
这个算法的主要目标是创建一个插入点，在这个点上新节点的父节点是 black，或者新节点的叔叔是 Black。
设 N 为要插入的新节点。

1.  **如果 Y 和 Z 为黑色:**
2.  **如果 X 的父母是黑人:**
3.  **X 的父母 P 为红色，祖父母为黑色，X 和 P 都是祖父母 G 的左或右子女:**
    *   重新着色 X，Y，Z
    *   围绕重力旋转
    *   彩色 P 黑
    *   红色
4.  **X 的父母是红的，祖父母是黑的，X 和 P 是祖父母 G 的对生子女**
    *   重新着色 X，Y，Z
    *   绕轴旋转
    *   围绕 G 旋转 X
    *   重新着色 X 和 G

下面执行以下方法:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for Top-Down
// Red-Black Tree Insertion creating
// a red black tree and storing an
// English sentence into it using Top
// down insertion approach

import static java.lang.Integer.max;

// Class for performing
// RBTree operations
public class RbTree {
    TreeNode Root = null;

    // Function to calculate
    // the height of the tree
    int HeightT(TreeNode Root)
    {
        int lefth, righth;

        if (Root == null
            || (Root.children == null
                && Root.children[1] == null)) {
            return 0;
        }
        lefth = HeightT(Root.children[0]);
        righth = HeightT(Root.children[1]);

        return (max(lefth, righth) + 1);
    }

    // Function to check if
    // dir is equal to 0
    int check(int dir)
    {
        return dir == 0 ? 1 : 0;
    }

    // Function to check if a
    // node's color is red or not
    boolean isRed(TreeNode Node)
    {
        return Node != null
            && Node.color.equals("R");
    }

    // Function to perform
    // single rotation
    TreeNode SingleRotate(TreeNode Node,
                          int dir)
    {
        TreeNode temp
            = Node.children[check(dir)];
        Node.children[check(dir)]
            = temp.children[dir];
        temp.children[dir] = Node;
        Root.color = "R";
        temp.color = "B";

        return temp;
    }

    // Function to perform double rotation
    TreeNode DoubleRotate(TreeNode Node,
                          int dir)
    {
        Node.children[check(dir)]
            = SingleRotate(Node.children[check(dir)],
                           check(dir));
        return SingleRotate(Node, dir);
    }

    // Function to insert a new
    // node with given data
    TreeNode Insert(RbTree tree,
                    String data)
    {
        if (tree.Root == null) {
            tree.Root
                = new TreeNode(data);
            if (tree.Root == null)
                return null;
        }
        else {

            // A temporary root
            TreeNode temp = new TreeNode("");

            // Grandparent and Parent
            TreeNode g, t;
            TreeNode p, q;

            int dir = 0, last = 0;

            t = temp;

            g = p = null;

            t.children[1] = tree.Root;

            q = t.children[1];
            while (true) {

                if (q == null) {

                    // Inserting root node
                    q = new TreeNode(data);
                    p.children[dir] = q;
                }

                // Sibling is red
                else if (isRed(q.children[0])
                         && isRed(q.children[1])) {

                    // Recoloring if both
                    // children are red
                    q.color = "R";
                    q.children[0].color = "B";
                    q.children[1].color = "B";
                }

                if (isRed(q) && isRed(p)) {

                    // Resolving red-red
                    // violation
                    int dir2;
                    if (t.children[1] == g) {
                        dir2 = 1;
                    }
                    else {
                        dir2 = 0;
                    }

                    // If children and parent
                    // are left-left or
                    // right-right of grand-parent
                    if (q == p.children[last]) {
                        t.children[dir2]
                            = SingleRotate(g,
                                           last == 0
                                               ? 1
                                               : 0);
                    }

                    // If they are opposite
                    // childs i.e left-right
                    // or right-left
                    else {
                        t.children[dir2]
                            = DoubleRotate(g,
                                           last == 0
                                               ? 1
                                               : 0);
                    }
                }

                // Checking for correct
                // position of node
                if (q.data.equals(data)) {
                    break;
                }
                last = dir;

                // Finding the path to
                // traverse [Either left
                // or right ]
                dir = q.data.compareTo(data) < 0
                          ? 1
                          : 0;

                if (g != null) {
                    t = g;
                }

                // Rearranging pointers
                g = p;
                p = q;
                q = q.children[dir];
            }

            tree.Root = temp.children[1];
        }

        // Assign black color
        // to the root node
        tree.Root.color = "B";

        return tree.Root;
    }

    // Print nodes at each
    // level in level order
    // traversal
    void PrintLevel(TreeNode root, int i)
    {
        if (root == null) {
            return;
        }

        if (i == 1) {
            System.out.print("| "
                             + root.data
                             + " | "
                             + root.color
                             + " |");

            if (root.children[0] != null) {
                System.out.print(" "
                                 + root.children[0].data
                                 + " |");
            }
            else {
                System.out.print(" "
                                 + "NULL"
                                 + " |");
            }
            if (root.children[1] != null) {
                System.out.print(" "
                                 + root.children[1].data
                                 + " |");
            }
            else {
                System.out.print(" "
                                 + "NULL"
                                 + " |");
            }

            System.out.print(" ");

            return;
        }

        PrintLevel(root.children[0],
                   i - 1);
        PrintLevel(root.children[1],
                   i - 1);
    }

    // Utility Function to
    // perform level order
    // traversal
    void LevelOrder(TreeNode root)
    {
        int i;

        for (i = 1;
             i < HeightT(root) + 1;
             i++) {
            PrintLevel(root, i);
            System.out.print("\n\n");
        }
    }
}

// Class for representing
// a node of the tree
class TreeNode {

    // Class variables
    String data, color;
    TreeNode children[];

    public TreeNode(String data)
    {
        // Color R- Red
        // and B - Black
        this.data = data;
        this.color = "R";
        children
            = new TreeNode[2];
        children[0] = null;
        children[1] = null;
    }
}

// Driver Code
class Driver {
    public static void main(String[] args)
    {
        // Tree Node Representation
        // -------------------------------------------
        // DATA | COLOR | LEFT CHILD | RIGHT CHILD |
        // -------------------------------------------

        RbTree Tree = new RbTree();
        String Sentence, Word;
        Sentence = "old is gold";
        String Word_Array[]
            = Sentence.split(" ");

        for (int i = 0;
             i < Word_Array.length;
             i++) {
            Tree.Root
                = Tree.Insert(Tree,
                              Word_Array[i]);
        }

        // Print Level Order Traversal
        System.out.println("The Level"
                           + "Order Traversal"
                           + "of the tree is:");
        Tree.LevelOrder(Tree.Root);
        System.out.println("\nInserting a"
                           + " word in the tree:");
        Word = "forever";
        Tree.Root = Tree.Insert(Tree,
                                Word);

        System.out.println("");
        Tree.LevelOrder(Tree.Root);
    }
}
```

## C#

```
// C# implementation for Top-Down
// Red-Black Tree Insertion creating
// a red black tree and storing an
// English sentence into it using Top
// down insertion approach
using System;

// Class for performing
// RBTree operations
class RbTree
{
    public TreeNode Root = null;

    // Function to calculate
    // the height of the tree
    public int HeightT(TreeNode Root)
    {
        int lefth, righth;

        if (Root == null ||
           (Root.children == null &&
            Root.children[1] == null))
        {
            return 0;
        }
        lefth = HeightT(Root.children[0]);
        righth = HeightT(Root.children[1]);

        return (Math.Max(lefth, righth) + 1);
    }

    // Function to check if
    // dir is equal to 0
    public int check(int dir)
    {
        return dir == 0 ? 1 : 0;
    }

    // Function to check if a
    // node's color is red or not
    public bool isRed(TreeNode Node)
    {
        return Node != null &&
               Node.color.Equals("R");
    }

    // Function to perform
    // single rotation
    public TreeNode SingleRotate(TreeNode Node, int dir)
    {
        TreeNode temp = Node.children[check(dir)];
        Node.children[check(dir)] = temp.children[dir];
        temp.children[dir] = Node;
        Root.color = "R";
        temp.color = "B";

        return temp;
    }

    // Function to perform double rotation
    public TreeNode DoubleRotate(TreeNode Node, int dir)
    {
        Node.children[check(dir)] =
             SingleRotate(Node.children[check(dir)],
                                        check(dir));
        return SingleRotate(Node, dir);
    }

    // Function to insert a new
    // node with given data
    public TreeNode Insert(RbTree tree,
                           String data)
    {
        if (tree.Root == null)
        {
            tree.Root = new TreeNode(data);
            if (tree.Root == null)
                return null;
        }
        else
        {

            // A temporary root
            TreeNode temp = new TreeNode("");

            // Grandparent and Parent
            TreeNode g, t;
            TreeNode p, q;

            int dir = 0, last = 0;

            t = temp;

            g = p = null;

            t.children[1] = tree.Root;

            q = t.children[1];
            while (true)
            {
                if (q == null)
                {

                    // Inserting root node
                    q = new TreeNode(data);
                    p.children[dir] = q;
                }

                // Sibling is red
                else if (isRed(q.children[0]) &&
                         isRed(q.children[1]))
                {

                    // Recoloring if both
                    // children are red
                    q.color = "R";
                    q.children[0].color = "B";
                    q.children[1].color = "B";
                }

                if (isRed(q) && isRed(p))
                {

                    // Resolving red-red
                    // violation
                    int dir2;
                    if (t.children[1] == g)
                    {
                        dir2 = 1;
                    }
                    else
                    {
                        dir2 = 0;
                    }

                    // If children and parent
                    // are left-left or
                    // right-right of grand-parent
                    if (q == p.children[last])
                    {
                        t.children[dir2] =
                          SingleRotate(g, last == 0 ? 1 : 0);
                    }

                    // If they are opposite
                    // childs i.e left-right
                    // or right-left
                    else
                    {
                        t.children[dir2] =
                          DoubleRotate(g, last == 0 ? 1 : 0);
                    }
                }

                // Checking for correct
                // position of node
                if (q.data.Equals(data))
                {
                    break;
                }
                last = dir;

                // Finding the path to
                // traverse [Either left
                // or right ]
                dir = q.data.CompareTo(data) < 0 ? 1 : 0;

                if (g != null)
                {
                    t = g;
                }

                // Rearranging pointers
                g = p;
                p = q;
                q = q.children[dir];
            }
            tree.Root = temp.children[1];
        }

        // Assign black color
        // to the root node
        tree.Root.color = "B";

        return tree.Root;
    }

    // Print nodes at each
    // level in level order
    // traversal
    public void PrintLevel(TreeNode root, int i)
    {
        if (root == null)
        {
            return;
        }

        if (i == 1)
        {
            Console.Write("| " + root.data +
                         " | " + root.color + " |");

            if (root.children[0] != null)
            {
                Console.Write(" " +
                   root.children[0].data + " |");
            }
            else
            {
                Console.Write(" " + "NULL" + " |");
            }
            if (root.children[1] != null)
            {
                Console.Write(" " +
                   root.children[1].data + " |");
            }
            else
            {
                Console.Write(" " + "NULL" + " |");
            }

            Console.Write(" ");

            return;
        }

        PrintLevel(root.children[0], i - 1);
        PrintLevel(root.children[1], i - 1);
    }

    // Utility Function to perform
    // level order traversal
    public void LevelOrder(TreeNode root)
    {
        int i;

        for (i = 1; i < HeightT(root) + 1; i++)
        {
            PrintLevel(root, i);
            Console.Write("\n\n");
        }
    }
}

// Class for representing
// a node of the tree
public class TreeNode
{

    // Class variables
    public String data, color;
    public TreeNode []children;

    public TreeNode(String data)
    {
        // Color R- Red
        // and B - Black
        this.data = data;
        this.color = "R";
        children = new TreeNode[2];
        children[0] = null;
        children[1] = null;
    }
}

// Driver Code
public class Driver
{
    public static void Main(String[] args)
    {
        // Tree Node Representation
        // -------------------------------------------
        // DATA | COLOR | LEFT CHILD | RIGHT CHILD |
        // -------------------------------------------
        RbTree Tree = new RbTree();
        String Sentence, Word;
        Sentence = "old is gold";
        char[] spearator = { ' ', ' ' };
        String []Word_Array = Sentence.Split(spearator,
                StringSplitOptions.RemoveEmptyEntries);

        for (int i = 0; i < Word_Array.Length; i++)
        {
            Tree.Root = Tree.Insert(Tree,
                            Word_Array[i]);
        }

        // Print Level Order Traversal
        Console.WriteLine("The Level" +
                          "Order Traversal" +
                          "of the tree is:");
        Tree.LevelOrder(Tree.Root);
        Console.WriteLine("\nInserting a" +
                          " word in the tree:");
        Word = "forever";
        Tree.Root = Tree.Insert(Tree, Word);

        Console.WriteLine("");
        Tree.LevelOrder(Tree.Root);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation for Top-Down
# Red-Black Tree Insertion creating
# a red black tree and storing an
# English sentence into it using Top
# down insertion approach

# Class for performing
# RBTree operations
class RbTree:

    Root = None

    # Function to calculate
    # the height of the tree
    def HeightT(self,Root):

        lefth, righth=0, 0

        if (Root == None or (Root.children == None and Root.children[1] == None)):
            return 0
        lefth = self.HeightT(Root.children[0])
        righth = self.HeightT(Root.children[1])

        return (max(lefth, righth) + 1)

    # Function to check if
    # dir is equal to 0
    @staticmethod
    def check(dir):
        return 1 if dir == 0 else 0

    # Function to check if a
    # node's color is red or not
    @staticmethod
    def isRed(Node):
        return Node != None and Node.color=="R"

    # Function to perform
    # single rotation
    def SingleRotate(self, Node, dir):

        temp = Node.children[self.check(dir)]
        Node.children[self.check(dir)] = temp.children[dir]
        temp.children[dir] = Node
        self.Root.color = "R"
        temp.color = "B"

        return temp

    # Function to perform double rotation
    def DoubleRotate(self, Node, dir):

        Node.children[self.check(dir)] = self.SingleRotate(Node.children[self.check(dir)], self.check(dir))
        return self.SingleRotate(Node, dir)

    # Function to insert a new
    # node with given data
    def Insert(self, tree, data):

        if (tree.Root == None):

            tree.Root = TreeNode(data)
            if (tree.Root == None):
                return None
        else:

            # A temporary root
            temp = TreeNode("")

            # Grandparent and Parent
            g, t=None,None
            p, q=None,None

            dir = 0; last = 0

            t = temp

            g = p = None

            t.children[1] = tree.Root

            q = t.children[1]
            while (True):

                if (q == None):

                    # Inserting root node
                    q = TreeNode(data)
                    p.children[dir] = q

                # Sibling is red
                elif (self.isRed(q.children[0]) and self.isRed(q.children[1])):

                    # Recoloring if both
                    # children are red
                    q.color = "R"
                    q.children[0].color = "B"
                    q.children[1].color = "B"

                if (self.isRed(q) and self.isRed(p)):

                    # Resolving red-red
                    # violation
                    dir2=0
                    if (t.children[1] == g):
                        dir2 = 1
                    else:
                        dir2 = 0

                    # If children and parent
                    # are left-left or
                    # right-right of grand-parent
                    if (q == p.children[last]):
                        t.children[dir2] = self.SingleRotate(g, 1 if last == 0 else 0)

                    # If they are opposite
                    # childs i.e left-right
                    # or right-left
                    else:
                        t.children[dir2] = self.DoubleRotate(g,1 if last == 0 else 0)

                # Checking for correct
                # position of node
                if (q.data==data):
                    break
                last = dir

                # Finding the path to
                # traverse [Either left
                # or right ]
                dir = 1 if q.data<data else 0

                if (g != None):
                    t = g

                # Rearranging pointers
                g = p
                p = q
                q = q.children[dir]

            tree.Root = temp.children[1]

        # Assign black color
        # to the root node
        tree.Root.color = "B"

        return tree.Root

    # Print nodes at each
    # level in level order
    # traversal
    def PrintLevel(self, root, i):
        if (root == None):
            return

        if (i == 1):
            print("| {} | {} |".format(root.data,root.color),end='')

            if (root.children[0] != None):
                print(" {} |".format(root.children[0].data),end='')
            else:
                print(" None |",end='')
            if (root.children[1] != None):
                print(" {} |".format(root.children[1].data),end='')
            else:
                print(" None |",end='')

            return

        self.PrintLevel(root.children[0], i - 1)
        self.PrintLevel(root.children[1], i - 1)

    # Utility Function to perform
    # level order traversal
    def LevelOrder(self, root):

        for i in range(self.HeightT(root) + 1):
            self.PrintLevel(root, i)
            print('\n')

# Class for representing
# a node of the tree
class TreeNode:
    def __init__(self, data):

        # Color R- Red
        # and B - Black
        self.data = data
        self.color = "R"
        self.children = [None,None]

# Driver Code
if __name__=='__main__':
    # Tree Node Representation
    # -------------------------------------------
    # DATA | COLOR | LEFT CHILD | RIGHT CHILD |
    # -------------------------------------------
    Tree = RbTree()
    Sentence, Word='',''
    Sentence = "old is gold"
    Word_Array = Sentence.split()

    for i in range(len(Word_Array)):
        Tree.Root = Tree.Insert(Tree, Word_Array[i])

    # Print Level Order Traversal
    print("The Level Order Traversal the tree is:")
    Tree.LevelOrder(Tree.Root)
    print("\nInserting a word in the tree:")
    Word = "forever"
    Tree.Root = Tree.Insert(Tree, Word)

    Tree.LevelOrder(Tree.Root)
# This code is contributed by Amartya Ghosh
```

**Output:** 

```
The LevelOrder Traversalof the tree is:
| is | B | gold | old | 

| gold | R | NULL | NULL | | old | R | NULL | NULL | 

Inserting a word in the tree:

| is | B | gold | old | 

| gold | B | forever | NULL | | old | B | NULL | NULL | 

| forever | R | NULL | NULL | 
```

**参考文献:**
[红黑树–UMBC CSEE](https://www.csee.umbc.edu/courses/341/fall04/Lectures/RedBlack/Red-Black-Trees-3.ppt)